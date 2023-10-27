# Codegen Options

All of these options are passed to `rustc` via the `-C` flag, short for "codegen." You can see
a version of this list for your exact compiler by running `rustc -C help`.

所有的这些选项都通过 `-C` 标签传递给 `rustc` ，是 "codegen" 的缩写。通过运行 `rustc -C help` 来查看确切编译器的此列表版本。

## ar

此选项已弃用，并且不执行任何操作。

## code-model

这个选项让你可以选择要使用的代码模型。 \
代码模型对程序及其符号可能使用的地址范围进行了约束。 \
有了更小的地址范围，机器指令就可以使用更紧凑的寻址模式。

该具体范围依赖于目标体系结构及其可用的寻址模式。 \
对于 x86 体系结构，更多细节性的描述可以在 [System V Application Binary Interface](https://github.com/hjl-tools/x86-psABI/wiki/x86-64-psABI-1.0.pdf) 规范中找到。

该选项支持的值有：

- `tiny` - 微代码模型。
- `small` - 小代码模型。这是大多数所支持的目标的默认模式。
- `kernel` - 内核代码模式。
- `medium` - 中型代码模式。
- `large` - 大型代码模式。

也可以通过运行 `rustc --print code-models` 查找受支持的值。

## codegen-units

该标签控制将 crate 分隔进多少个代码生成单元，这个（代码生成单元数）大于 0 。

当一个 crate 被分割进多个代码生成单元，LLVM 就可以并行处理它们。
提高并行性或许会加快编译时间（缩短编译耗时），但是也可能会产生更慢的代码。
设置该标签为 1 可能会提升生成代码的性能，但是也可能会编译得更慢。

如果没有指明默认值，对于非增量构建默认值就是 16 。对于增量构建，默认值是 256，可以使缓存更加细粒度。

## control-flow-guard

This flag controls whether LLVM enables the Windows [Control Flow
Guard](https://docs.microsoft.com/en-us/windows/win32/secbp/control-flow-guard)
platform security feature. This flag is currently ignored for non-Windows targets.
It takes one of the following values:

该标签控制 LLVM 是否启用 Windows 的 [Control Flow
Guard](https://docs.microsoft.com/en-us/windows/win32/secbp/control-flow-guard) 平台安全功能。
该标签当前会忽略非 Windows 目标。它使用下列值中的一个：

* `y`， `yes`， `on`， `checks`， 或者没有值： 启用控制流守卫。
* `nochecks`： 不进行运行时强制检查的情况下触发控制流守卫元数据（这理应只用于测试目的，因为它不提供安全强制）。
* `n`， `no`， `off`： 不启用控制流守卫（默认值）。

## debug-assertions

该标签让你可以打开或关闭 `cfg(debug_assertions)` [conditional
compilation](https://doc.rust-lang.org/reference/conditional-compilation.html#debug_assertions)。
其采用以下值之一：

* `y`， `yes`， `on`， 或者无值 ：开启 debug-assertions。
* `n`， `no`， 或 `off` ： 禁用 debug-assertions。

如果没有指定，仅在 [opt-level](#opt-level) 是 0 的时候开启。

## debuginfo

此标志控制调试信息的生成。它采用以下值之一：

* `0` or `none`: 根本没有调试信息（默认值）。
* `line-directives-only`: 只有行信息指令。对于 nvptx* 目标，这启用[profiling](https://reviews.llvm.org/D46061)。对于其他使用情况，`line-tables-only`是更好、更兼容的选择。
* `line-tables-only`: 只有行表。生成用于包含文件名/行号信息的回溯的最少的调试信息，但不包括任何其他信息，即没有变量或函数参数信息。
* `1` or `limited`: 没有类型或变量级别信息的调试信息。
* `2` or `full`: 完整的调试信息。

注意：[`-g` 标签][option-g-debug] 是 `-C debuginfo=2` 的别名。

## default-linker-libraries

此标志控制链接器是否包含其默认库。它采用以下值之一：

* `y`, `yes`, `on`, `true`: 包括默认库。
* `n`, `no`, `off` or `false` 排除默认库（默认值）。

例如，对于 gcc flavor 链接器，这会向链接器传递 `-nodefaultlibs` 标签。

## dlltool

在 `windows-gnu` 目标上，此标志控制 `rustc` 在使用[`raw-dylib` link kind](../../reference/items/external-blocks.md#the-link-attribute)时调用哪个`dlltool`来生成导入库。
它采用到[the dlltool executable](https://sourceware.org/binutils/docs/binutils/dlltool.html)的路径。
如果未指定此标志，将根据主机环境和目标推断 `dlltool` 可执行文件的路径。

## embed-bitcode

该标签控制编译器是否将 LLVM 位码嵌入目标文件（object files）中。其采用以下值之一：

* `y`, `yes`, `on`, `true` 或者无值： 将位码放入 rlib （默认值）。
* `n`, `no`, `off` or `false`: 省略 rlibs 中的位码。

LLVM bitcode is required when rustc is performing link-time optimization (LTO).
It is also required on some targets like iOS ones where vendors look for LLVM
bitcode. Embedded bitcode will appear in rustc-generated object files inside of
a section whose name is defined by the target platform. Most of the time this is
`.llvmbc`.

当 rustc 进行链接时优化（LTO）时，需要 LLVM bitcode。
在某些目标上也需要它，比如 iOS，这样的目标平台上也需要。
嵌入的 bitcode 将出现在 rustc 生成的目标文件中，位于由目标平台定义的部分中。大多数情况下，这是`.llvmbc`。

如果你的编译实际上不需要位码（例如，如果你不针对 iOS 进行编译或不执行 LTO ），`-C embed-bitcode=no` 的使用可以大大缩短编译时间并且减少生成文件的大小.由于这些原因，Cargo 会尽可能使用 `-C embed-bitcode=no` 。
同样，如果你直接用 rustc 进行构建，我们推荐你在不使用 LTO 的时候使用 `-C embed-bitcode=no` 。

如果结合 `-C lto`，`-C embed-bitcode=no` 将会导致 `rustc` 启动时就中止，因为该（标签）组合是无效的。

> **注意**： 如果你使用 LTO 构建 Rust 代码，你就可能甚至不需要打开 `embed-bitcode` 选项。
你可能会想要使用 `-Clinker-plugin-lto` 来代替，它会完全跳过生成目标文件，并且用 LLVM 位码来简单替换目标文件。
唯一的使用 `-Cembed-bitcode` 的目的是当你要生成同时使用和不使用 LTO 的 rlib 时，例如 Rust 标准库带有嵌入的位码，因为用户可以使用或不使用 LTO 进行链接。
> 
> 这也可能会让你想知道为什么该选项的默认值是 `yes` 。理由是在 1.44 中及更早版本中是这样的。在 1.45 中，将此选项默认值调整为关闭。

## extra-filename

该选项允许你将额外的数据放进每个输出文件。
它需要一个字符串作为后缀添加到文件名中。
更多信息请参阅 [`--emit` flag][option-emit]。

## force-frame-pointers

该标签可以强制栈帧指针的使用。其采用以下值之一：

* `y`, `yes`, `on`, `true` 或者无值： 强制启用栈帧指针。
* `n`, `no`, `off` or `false`: 不强制启用栈帧指针，但这并不意味着移除栈帧指针。

如果没有强制启用栈帧指针，则默认行为取决于目标平台。

## force-unwind-tables

此标志强制生成展开表。它采用以下值之一：

* `y`, `yes`, `on`, `true` 无值：强制生成展开表。
* `n`, `no`, `off` or `false`: 不强制生成展开表。如果目标需要展开表，则会发出错误。

如果未指定，则默认值取决于目标。

## incremental

该标签允许你启用增量编译，这允许 `rustc` 在编译完 crate 之后保存信息，以便重新编译 crate 的时候可以重用，缩短重编译的时间。
这将采用一个存放增量文件的目录的路径。

## inline-threshold

该选项使你可以设置内联函数的默认阈值。其值采用无符号整数。内联基于成本模型，较高的阈值将会允许更多的内联。

默认（阈值）取决于 [opt-level](#opt-level):

| opt-level | Threshold |
|-----------|-----------|
| 0         | N/A, 仅内联强制内联函数 |
| 1         | N/A, 仅内联强制内联函数和 LLVM 生命周期内联函数 |
| 2         | 225 |
| 3         | 275 |
| s         | 75 |
| z         | 25 |

## instrument-coverage

这个选项启用了基于仪器代码覆盖支持。有关更多信息，请参阅有关 [instrumentation-based code coverage] 的章节。

请注意，尽管`-C instrument-coverage`选项是稳定的，但由此产生的仪器生成的配置文件数据格式可能会发生变化，\
并且可能与除编译器自带的工具之外的其他覆盖工具不兼容。

## link-arg

该标签使你可以在链接器调用后附加一个额外的参数。

“附加” 是很重要的；你可以多次传递该标签以添加多个参数。

## link-args

该标签使你可以在链接器调用后附加多个额外的参数。该选项（后的参数）应该用空格分隔。

## link-dead-code

该标签控制链接器是否保留无效代码。其采用以下值之一：

* `y`, `yes`, `on`, `true` 或者无值： 保留无效代码。
* `n`, `no`, `off` or `false`: 移除无效代码（默认值）。

这个标志可能有用的一个例子是当试图构建代码覆盖率指标时。

## link-self-contained

On `windows-gnu`, `linux-musl`, and `wasi` targets, this flag controls whether the
linker will use libraries and objects shipped with Rust instead or those in the system.
It takes one of the following values:

* no value: rustc will use heuristic to disable self-contained mode if system has necessary tools.
* `y`, `yes`, `on`, `true`: use only libraries/objects shipped with Rust.
* `n`, `no`, `off` or `false`: rely on the user or the linker to provide non-Rust libraries/objects.

This allows overriding cases when detection fails or user wants to use shipped libraries.

## linker

This flag controls which linker `rustc` invokes to link your code. It takes a
path to the linker executable. If this flag is not specified, the linker will
be inferred based on the target. See also the [linker-flavor](#linker-flavor)
flag for another way to specify the linker.

## linker-flavor

This flag controls the linker flavor used by `rustc`. If a linker is given with
the [`-C linker` flag](#linker), then the linker flavor is inferred from the
value provided. If no linker is given then the linker flavor is used to
determine the linker to use. Every `rustc` target defaults to some linker
flavor. Valid options are:

* `em`: use [Emscripten `emcc`](https://emscripten.org/docs/tools_reference/emcc.html).
* `gcc`: use the `cc` executable, which is typically gcc or clang on many systems.
* `ld`: use the `ld` executable.
* `msvc`: use the `link.exe` executable from Microsoft Visual Studio MSVC.
* `ptx`: use [`rust-ptx-linker`](https://github.com/denzp/rust-ptx-linker)
  for Nvidia NVPTX GPGPU support.
* `bpf`: use [`bpf-linker`](https://github.com/alessandrod/bpf-linker) for eBPF support.
* `wasm-ld`: use the [`wasm-ld`](https://lld.llvm.org/WebAssembly.html)
  executable, a port of LLVM `lld` for WebAssembly.
* `ld64.lld`: use the LLVM `lld` executable with the [`-flavor darwin`
  flag][lld-flavor] for Apple's `ld`.
* `ld.lld`: use the LLVM `lld` executable with the [`-flavor gnu`
  flag][lld-flavor] for GNU binutils' `ld`.
* `lld-link`: use the LLVM `lld` executable with the [`-flavor link`
  flag][lld-flavor] for Microsoft's `link.exe`.

[lld-flavor]: https://releases.llvm.org/12.0.0/tools/lld/docs/Driver.html

## linker-plugin-lto

This flag defers LTO optimizations to the linker. See
[linker-plugin-LTO](../linker-plugin-lto.md) for more details. It takes one of
the following values:

* `y`, `yes`, `on`, `true` or no value: enable linker plugin LTO.
* `n`, `no`, `off` or `false`: disable linker plugin LTO (the default).
* A path to the linker plugin.

More specifically this flag will cause the compiler to replace its typical
object file output with LLVM bitcode files. For example an rlib produced with
`-Clinker-plugin-lto` will still have `*.o` files in it, but they'll all be LLVM
bitcode instead of actual machine code. It is expected that the native platform
linker is capable of loading these LLVM bitcode files and generating code at
link time (typically after performing optimizations).

Note that rustc can also read its own object files produced with
`-Clinker-plugin-lto`. If an rlib is only ever going to get used later with a
`-Clto` compilation then you can pass `-Clinker-plugin-lto` to speed up
compilation and avoid generating object files that aren't used.

## llvm-args

This flag can be used to pass a list of arguments directly to LLVM.

The list must be separated by spaces.

Pass `--help` to see a list of options.

## lto

This flag controls whether LLVM uses [link time
optimizations](https://llvm.org/docs/LinkTimeOptimization.html) to produce
better optimized code, using whole-program analysis, at the cost of longer
linking time. It takes one of the following values:

* `y`, `yes`, `on`, `true`, `fat`, or no value: perform "fat" LTO which attempts to
  perform optimizations across all crates within the dependency graph.
* `n`, `no`, `off`, `false`: disables LTO.
* `thin`: perform ["thin"
  LTO](http://blog.llvm.org/2016/06/thinlto-scalable-and-incremental-lto.html).
  This is similar to "fat", but takes substantially less time to run while
  still achieving performance gains similar to "fat".

If `-C lto` is not specified, then the compiler will attempt to perform "thin
local LTO" which performs "thin" LTO on the local crate only across its
[codegen units](#codegen-units). When `-C lto` is not specified, LTO is
disabled if codegen units is 1 or optimizations are disabled ([`-C
opt-level=0`](#opt-level)). That is:

* When `-C lto` is not specified:
  * `codegen-units=1`: disable LTO.
  * `opt-level=0`: disable LTO.
* When `-C lto` is specified:
  * `lto`: 16 codegen units, perform fat LTO across crates.
  * `codegen-units=1` + `lto`: 1 codegen unit, fat LTO across crates.

See also [linker-plugin-lto](#linker-plugin-lto) for cross-language LTO.

## metadata

This option allows you to control the metadata used for symbol mangling. This
takes a space-separated list of strings. Mangled symbols will incorporate a
hash of the metadata. This may be used, for example, to differentiate symbols
between two different versions of the same crate being linked.

## no-prepopulate-passes

This flag tells the pass manager to use an empty list of passes, instead of the
usual pre-populated list of passes.

## no-redzone

This flag allows you to disable [the
red zone](https://en.wikipedia.org/wiki/Red_zone_\(computing\)). It takes one
of the following values:

* `y`, `yes`, `on`, `true` or no value: disable the red zone.
* `n`, `no`, `off` or `false`: enable the red zone.

The default behaviour, if the flag is not specified, depends on the target.

## no-stack-check

This option is deprecated and does nothing.

## no-vectorize-loops

This flag disables [loop
vectorization](https://llvm.org/docs/Vectorizers.html#the-loop-vectorizer).

## no-vectorize-slp

This flag disables vectorization using
[superword-level
parallelism](https://llvm.org/docs/Vectorizers.html#the-slp-vectorizer).

## opt-level

This flag controls the optimization level.

* `0`: no optimizations, also turns on
  [`cfg(debug_assertions)`](#debug-assertions) (the default).
* `1`: basic optimizations.
* `2`: some optimizations.
* `3`: all optimizations.
* `s`: optimize for binary size.
* `z`: optimize for binary size, but also turn off loop vectorization.

Note: The [`-O` flag][option-o-optimize] is an alias for `-C opt-level=2`.

The default is `0`.

## overflow-checks

This flag allows you to control the behavior of [runtime integer
overflow](../../reference/expressions/operator-expr.md#overflow). When
overflow-checks are enabled, a panic will occur on overflow. This flag takes
one of the following values:

* `y`, `yes`, `on`, `true` or no value: enable overflow checks.
* `n`, `no`, `off` or `false`: disable overflow checks.

If not specified, overflow checks are enabled if
[debug-assertions](#debug-assertions) are enabled, disabled otherwise.

## panic

This option lets you control what happens when the code panics.

* `abort`: terminate the process upon panic
* `unwind`: unwind the stack upon panic

If not specified, the default depends on the target.

## passes

This flag can be used to add extra [LLVM
passes](http://llvm.org/docs/Passes.html) to the compilation.

The list must be separated by spaces.

See also the [`no-prepopulate-passes`](#no-prepopulate-passes) flag.

## prefer-dynamic

By default, `rustc` prefers to statically link dependencies. This option will
indicate that dynamic linking should be used if possible if both a static and
dynamic versions of a library are available. There is an internal algorithm
for determining whether or not it is possible to statically or dynamically
link with a dependency. For example, `cdylib` crate types may only use static
linkage. This flag takes one of the following values:

* `y`, `yes`, `on`, `true` or no value: use dynamic linking.
* `n`, `no`, `off` or `false`: use static linking (the default).

## profile-generate

This flag allows for creating instrumented binaries that will collect
profiling data for use with profile-guided optimization (PGO). The flag takes
an optional argument which is the path to a directory into which the
instrumented binary will emit the collected data. See the chapter on
[profile-guided optimization] for more information.

## profile-use

This flag specifies the profiling data file to be used for profile-guided
optimization (PGO). The flag takes a mandatory argument which is the path
to a valid `.profdata` file. See the chapter on
[profile-guided optimization] for more information.

## relocation-model

This option controls generation of
[position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code).

Supported values for this option are:

#### Primary relocation models

- `static` - non-relocatable code, machine instructions may use absolute addressing modes.

- `pic` - fully relocatable position independent code,
machine instructions need to use relative addressing modes.  \
Equivalent to the "uppercase" `-fPIC` or `-fPIE` options in other compilers,
depending on the produced crate types.  \
This is the default model for majority of supported targets.

- `pie` - position independent executable, relocatable code but without support for symbol
interpositioning (replacing symbols by name using `LD_PRELOAD` and similar). Equivalent to the "uppercase" `-fPIE` option in other compilers. `pie`
code cannot be linked into shared libraries (you'll get a linking error on attempt to do this).

#### Special relocation models

- `dynamic-no-pic` - relocatable external references, non-relocatable code.  \
Only makes sense on Darwin and is rarely used.  \
If StackOverflow tells you to use this as an opt-out of PIC or PIE, don't believe it,
use `-C relocation-model=static` instead.
- `ropi`, `rwpi` and `ropi-rwpi` - relocatable code and read-only data, relocatable read-write data,
and combination of both, respectively.  \
Only makes sense for certain embedded ARM targets.
- `default` - relocation model default to the current target.  \
Only makes sense as an override for some other explicitly specified relocation model
previously set on the command line.

Supported values can also be discovered by running `rustc --print relocation-models`.

#### Linking effects

In addition to codegen effects, `relocation-model` has effects during linking.

If the relocation model is `pic` and the current target supports position-independent executables
(PIE), the linker will be instructed (`-pie`) to produce one.  \
If the target doesn't support both position-independent and statically linked executables,
then `-C target-feature=+crt-static` "wins" over `-C relocation-model=pic`,
and the linker is instructed (`-static`) to produce a statically linked
but not position-independent executable.

## remark

This flag lets you print remarks for optimization passes.

The list of passes should be separated by spaces.

`all` will remark on every pass.

## rpath

This flag controls whether [`rpath`](https://en.wikipedia.org/wiki/Rpath) is
enabled. It takes one of the following values:

* `y`, `yes`, `on`, `true` or no value: enable rpath.
* `n`, `no`, `off` or `false`: disable rpath (the default).

## save-temps

This flag controls whether temporary files generated during compilation are
deleted once compilation finishes. It takes one of the following values:

* `y`, `yes`, `on`, `true` or no value: save temporary files.
* `n`, `no`, `off` or `false`: delete temporary files (the default).

## soft-float

This option controls whether `rustc` generates code that emulates floating
point instructions in software. It takes one of the following values:

* `y`, `yes`, `on`, `true` or no value: use soft floats.
* `n`, `no`, `off` or `false`: use hardware floats (the default).

## split-debuginfo

This option controls the emission of "split debuginfo" for debug information
that `rustc` generates. The default behavior of this option is
platform-specific, and not all possible values for this option work on all
platforms. Possible values are:

* `off` - This is the default for platforms with ELF binaries and windows-gnu
  (not Windows MSVC and not macOS). This typically means that DWARF debug
  information can be found in the final artifact in sections of the executable.
  This option is not supported on Windows MSVC. On macOS this options prevents
  the final execution of `dsymutil` to generate debuginfo.

* `packed` - This is the default for Windows MSVC and macOS. The term
  "packed" here means that all the debug information is packed into a separate
  file from the main executable. On Windows MSVC this is a `*.pdb` file, on
  macOS this is a `*.dSYM` folder, and on other platforms this is a `*.dwp`
  file.

* `unpacked` - This means that debug information will be found in separate
  files for each compilation unit (object file). This is not supported on
  Windows MSVC. On macOS this means the original object files will contain
  debug information. On other Unix platforms this means that `*.dwo` files will
  contain debug information.

Note that all three options are supported on Linux and Apple platforms,
`packed` is supported on Windows-MSVC, and all other platforms support `off`.
Attempting to use an unsupported option requires using the nightly channel
with the `-Z unstable-options` flag.

## strip

The option `-C strip=val` controls stripping of debuginfo and similar auxiliary
data from binaries during linking.

Supported values for this option are:

- `none` - debuginfo and symbols (if they exist) are copied to the produced
  binary or separate files depending on the target (e.g. `.pdb` files in case
  of MSVC).
- `debuginfo` - debuginfo sections and debuginfo symbols from the symbol table
  section are stripped at link time and are not copied to the produced binary
  or separate files.
- `symbols` - same as `debuginfo`, but the rest of the symbol table section is
  stripped as well if the linker supports it.

## symbol-mangling-version

This option controls the [name mangling] format for encoding Rust item names
for the purpose of generating object code and linking.

Supported values for this option are:

* `v0` — The "v0" mangling scheme.

The default, if not specified, will use a compiler-chosen default which may
change in the future.

See the [Symbol Mangling] chapter for details on symbol mangling and the mangling format.

[name mangling]: https://en.wikipedia.org/wiki/Name_mangling
[Symbol Mangling]: ../symbol-mangling/index.md

## target-cpu

This instructs `rustc` to generate code specifically for a particular processor.

You can run `rustc --print target-cpus` to see the valid options to pass
and the default target CPU for the current build target.
Each target has a default base CPU. Special values include:

* `native` can be passed to use the processor of the host machine.
* `generic` refers to an LLVM target with minimal features but modern tuning.

## target-feature

Individual targets will support different features; this flag lets you control
enabling or disabling a feature. Each feature should be prefixed with a `+` to
enable it or `-` to disable it.

Features from multiple `-C target-feature` options are combined. \
Multiple features can be specified in a single option by separating them
with commas - `-C target-feature=+x,-y`. \
If some feature is specified more than once with both `+` and `-`,
then values passed later override values passed earlier. \
For example, `-C target-feature=+x,-y,+z -Ctarget-feature=-x,+y`
is equivalent to `-C target-feature=-x,+y,+z`.

To see the valid options and an example of use, run `rustc --print
target-features`.

Using this flag is unsafe and might result in [undefined runtime
behavior](../targets/known-issues.md).

See also the [`target_feature`
attribute](../../reference/attributes/codegen.md#the-target_feature-attribute)
for controlling features per-function.

This also supports the feature `+crt-static` and `-crt-static` to control
[static C runtime linkage](../../reference/linkage.html#static-and-dynamic-c-runtimes).

Each target and [`target-cpu`](#target-cpu) has a default set of enabled
features.

## tune-cpu

This instructs `rustc` to schedule code specifically for a particular
processor. This does not affect the compatibility (instruction sets or ABI),
but should make your code slightly more efficient on the selected CPU.

The valid options are the same as those for [`target-cpu`](#target-cpu).
The default is `None`, which LLVM translates as the `target-cpu`.

This is an unstable option. Use `-Z tune-cpu=machine` to specify a value.

Due to limitations in LLVM (12.0.0-git9218f92), this option is currently
effective only for x86 targets.

[option-emit]: ../command-line-arguments.md#option-emit
[option-o-optimize]: ../command-line-arguments.md#option-o-optimize
[instrumentation-based code coverage]: ../instrument-coverage.md
[profile-guided optimization]: ../profile-guided-optimization.md
[option-g-debug]: ../command-line-arguments.md#option-g-debug
