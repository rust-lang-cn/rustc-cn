# Warn-by-default Lints

默认情况下，这些 lint 都被设置为 `warn` 级别。

* [`ambiguous_glob_imports`](#ambiguous-glob-imports)
* [`ambiguous_glob_reexports`](#ambiguous-glob-reexports)
* [`anonymous_parameters`](#anonymous-parameters)
* [`array_into_iter`](#array-into-iter)
* [`asm_sub_register`](#asm-sub-register)
* [`async_fn_in_trait`](#async-fn-in-trait)
* [`bad_asm_style`](#bad-asm-style)
* [`bare_trait_objects`](#bare-trait-objects)
* [`break_with_label_and_loop`](#break-with-label-and-loop)
* [`byte_slice_in_packed_struct_with_derive`](#byte-slice-in-packed-struct-with-derive)
* [`clashing_extern_declarations`](#clashing-extern-declarations)
* [`coherence_leak_check`](#coherence-leak-check)
* [`confusable_idents`](#confusable-idents)
* [`const_evaluatable_unchecked`](#const-evaluatable-unchecked)
* [`const_item_mutation`](#const-item-mutation)
* [`const_patterns_without_partial_eq`](#const-patterns-without-partial-eq)
* [`dead_code`](#dead-code)
* [`deprecated`](#deprecated)
* [`deprecated_where_clause_location`](#deprecated-where-clause-location)
* [`deref_into_dyn_supertrait`](#deref-into-dyn-supertrait)
* [`deref_nullptr`](#deref-nullptr)
* [`drop_bounds`](#drop-bounds)
* [`dropping_copy_types`](#dropping-copy-types)
* [`dropping_references`](#dropping-references)
* [`duplicate_macro_attributes`](#duplicate-macro-attributes)
* [`dyn_drop`](#dyn-drop)
* [`elided_lifetimes_in_associated_constant`](#elided-lifetimes-in-associated-constant)
* [`ellipsis_inclusive_range_patterns`](#ellipsis-inclusive-range-patterns)
* [`exported_private_dependencies`](#exported-private-dependencies)
* [`for_loops_over_fallibles`](#for-loops-over-fallibles)
* [`forbidden_lint_groups`](#forbidden-lint-groups)
* [`forgetting_copy_types`](#forgetting-copy-types)
* [`forgetting_references`](#forgetting-references)
* [`function_item_references`](#function-item-references)
* [`hidden_glob_reexports`](#hidden-glob-reexports)
* [`illegal_floating_point_literal_pattern`](#illegal-floating-point-literal-pattern)
* [`improper_ctypes`](#improper-ctypes)
* [`improper_ctypes_definitions`](#improper-ctypes-definitions)
* [`incomplete_features`](#incomplete-features)
* [`indirect_structural_match`](#indirect-structural-match)
* [`inline_no_sanitize`](#inline-no-sanitize)
* [`internal_features`](#internal-features)
* [`invalid_doc_attributes`](#invalid-doc-attributes)
* [`invalid_from_utf8`](#invalid-from-utf8)
* [`invalid_macro_export_arguments`](#invalid-macro-export-arguments)
* [`invalid_nan_comparisons`](#invalid-nan-comparisons)
* [`invalid_value`](#invalid-value)
* [`irrefutable_let_patterns`](#irrefutable-let-patterns)
* [`large_assignments`](#large-assignments)
* [`late_bound_lifetime_arguments`](#late-bound-lifetime-arguments)
* [`legacy_derive_helpers`](#legacy-derive-helpers)
* [`map_unit_fn`](#map-unit-fn)
* [`mixed_script_confusables`](#mixed-script-confusables)
* [`named_arguments_used_positionally`](#named-arguments-used-positionally)
* [`no_mangle_generic_items`](#no-mangle-generic-items)
* [`non_camel_case_types`](#non-camel-case-types)
* [`non_fmt_panics`](#non-fmt-panics)
* [`non_shorthand_field_patterns`](#non-shorthand-field-patterns)
* [`non_snake_case`](#non-snake-case)
* [`non_upper_case_globals`](#non-upper-case-globals)
* [`nontrivial_structural_match`](#nontrivial-structural-match)
* [`noop_method_call`](#noop-method-call)
* [`opaque_hidden_inferred_bound`](#opaque-hidden-inferred-bound)
* [`overlapping_range_endpoints`](#overlapping-range-endpoints)
* [`path_statements`](#path-statements)
* [`private_bounds`](#private-bounds)
* [`private_interfaces`](#private-interfaces)
* [`redundant_semicolons`](#redundant-semicolons)
* [`refining_impl_trait`](#refining-impl-trait)
* [`renamed_and_removed_lints`](#renamed-and-removed-lints)
* [`repr_transparent_external_private_fields`](#repr-transparent-external-private-fields)
* [`semicolon_in_expressions_from_macros`](#semicolon-in-expressions-from-macros)
* [`special_module_name`](#special-module-name)
* [`stable_features`](#stable-features)
* [`suspicious_auto_trait_impls`](#suspicious-auto-trait-impls)
* [`suspicious_double_ref_op`](#suspicious-double-ref-op)
* [`temporary_cstring_as_ptr`](#temporary-cstring-as-ptr)
* [`trivial_bounds`](#trivial-bounds)
* [`type_alias_bounds`](#type-alias-bounds)
* [`tyvar_behind_raw_pointer`](#tyvar-behind-raw-pointer)
* [`uncommon_codepoints`](#uncommon-codepoints)
* [`unconditional_recursion`](#unconditional-recursion)
* [`undefined_naked_function_abi`](#undefined-naked-function-abi)
* [`unexpected_cfgs`](#unexpected-cfgs)
* [`unfulfilled_lint_expectations`](#unfulfilled-lint-expectations)
* [`ungated_async_fn_track_caller`](#ungated-async-fn-track-caller)
* [`uninhabited_static`](#uninhabited-static)
* [`unknown_lints`](#unknown-lints)
* [`unknown_or_malformed_diagnostic_attributes`](#unknown-or-malformed-diagnostic-attributes)
* [`unnameable_test_items`](#unnameable-test-items)
* [`unreachable_code`](#unreachable-code)
* [`unreachable_patterns`](#unreachable-patterns)
* [`unstable_name_collisions`](#unstable-name-collisions)
* [`unstable_syntax_pre_expansion`](#unstable-syntax-pre-expansion)
* [`unsupported_calling_conventions`](#unsupported-calling-conventions)
* [`unused_allocation`](#unused-allocation)
* [`unused_assignments`](#unused-assignments)
* [`unused_associated_type_bounds`](#unused-associated-type-bounds)
* [`unused_attributes`](#unused-attributes)
* [`unused_braces`](#unused-braces)
* [`unused_comparisons`](#unused-comparisons)
* [`unused_doc_comments`](#unused-doc-comments)
* [`unused_features`](#unused-features)
* [`unused_imports`](#unused-imports)
* [`unused_labels`](#unused-labels)
* [`unused_macros`](#unused-macros)
* [`unused_must_use`](#unused-must-use)
* [`unused_mut`](#unused-mut)
* [`unused_parens`](#unused-parens)
* [`unused_unsafe`](#unused-unsafe)
* [`unused_variables`](#unused-variables)
* [`useless_ptr_null_checks`](#useless-ptr-null-checks)
* [`warnings`](#warnings)
* [`where_clauses_object_safety`](#where-clauses-object-safety)
* [`while_true`](#while-true)

## ambiguous-glob-imports

The `ambiguous_glob_imports` lint detects glob imports that should report ambiguity
errors, but previously didn't do that due to rustc bugs.

### Example

```rust,compile_fail
#![deny(ambiguous_glob_imports)]
pub fn foo() -> u32 {
    use sub::*;
    C
}

mod sub {
    mod mod1 { pub const C: u32 = 1; }
    mod mod2 { pub const C: u32 = 2; }

    pub use mod1::*;
    pub use mod2::*;
}
```

This will produce:

```text
error: `C` is ambiguous
  --> lint_example.rs:5:5
   |
5  |     C
   |     ^ ambiguous name
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #114095 <https://github.com/rust-lang/rust/issues/114095>
   = note: ambiguous because of multiple glob imports of a name in the same module
note: `C` could refer to the constant imported here
  --> lint_example.rs:12:13
   |
12 |     pub use mod1::*;
   |             ^^^^^^^
   = help: consider adding an explicit import of `C` to disambiguate
note: `C` could also refer to the constant imported here
  --> lint_example.rs:13:13
   |
13 |     pub use mod2::*;
   |             ^^^^^^^
   = help: consider adding an explicit import of `C` to disambiguate
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(ambiguous_glob_imports)]
   |         ^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Previous versions of Rust compile it successfully because it
had lost the ambiguity error when resolve `use sub::mod2::*`.

This is a [future-incompatible] lint to transition this to a
hard error in the future.

[future-incompatible]: ../index.md#future-incompatible-lints

## ambiguous-glob-reexports

The `ambiguous_glob_reexports` lint detects cases where names re-exported via globs
collide. Downstream users trying to use the same name re-exported from multiple globs
will receive a warning pointing out redefinition of the same name.

### Example

```rust,compile_fail
#![deny(ambiguous_glob_reexports)]
pub mod foo {
    pub type X = u8;
}

pub mod bar {
    pub type Y = u8;
    pub type X = u8;
}

pub use foo::*;
pub use bar::*;


pub fn main() {}
```

This will produce:

```text
error: ambiguous glob re-exports
  --> lint_example.rs:11:9
   |
11 | pub use foo::*;
   |         ^^^^^^ the name `X` in the type namespace is first re-exported here
12 | pub use bar::*;
   |         ------ but the name `X` in the type namespace is also re-exported here
   |
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(ambiguous_glob_reexports)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

This was previously accepted but it could silently break a crate's downstream users code.
For example, if `foo::*` and `bar::*` were re-exported before `bar::X` was added to the
re-exports, down stream users could use `this_crate::X` without problems. However, adding
`bar::X` would cause compilation errors in downstream crates because `X` is defined
multiple times in the same namespace of `this_crate`.

## anonymous-parameters

The `anonymous_parameters` lint detects anonymous parameters in trait
definitions.

### Example

```rust,edition2015,compile_fail
#![deny(anonymous_parameters)]
// edition 2015
pub trait Foo {
    fn foo(usize);
}
fn main() {}
```

This will produce:

```text
error: anonymous parameters are deprecated and will be removed in the next edition
 --> lint_example.rs:4:12
  |
4 |     fn foo(usize);
  |            ^^^^^ help: try naming the parameter or explicitly ignoring it: `_: usize`
  |
  = warning: this is accepted in the current edition (Rust 2015) but is a hard error in Rust 2018!
  = note: for more information, see issue #41686 <https://github.com/rust-lang/rust/issues/41686>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(anonymous_parameters)]
  |         ^^^^^^^^^^^^^^^^^^^^

```

### Explanation

This syntax is mostly a historical accident, and can be worked around
quite easily by adding an `_` pattern or a descriptive identifier:

```rust
trait Foo {
    fn foo(_: usize);
}
```

This syntax is now a hard error in the 2018 edition. In the 2015
edition, this lint is "warn" by default. This lint
enables the [`cargo fix`] tool with the `--edition` flag to
automatically transition old code from the 2015 edition to 2018. The
tool will run this lint and automatically apply the
suggested fix from the compiler (which is to add `_` to each
parameter). This provides a completely automated way to update old
code for a new edition. See [issue #41686] for more details.

[issue #41686]: https://github.com/rust-lang/rust/issues/41686
[`cargo fix`]: https://doc.rust-lang.org/cargo/commands/cargo-fix.html

## array-into-iter

`array_into_iter` lint 检测在数组上调用 `into_iter`。

### Example

```rust,edition2018
# #![allow(unused)]
[1, 2, 3].into_iter().for_each(|n| { *n; });
```

This will produce:

```text
warning: this method call resolves to `<&[T; N] as IntoIterator>::into_iter` (due to backwards compatibility), but will resolve to <[T; N] as IntoIterator>::into_iter in Rust 2021
 --> lint_example.rs:3:11
  |
3 | [1, 2, 3].into_iter().for_each(|n| { *n; });
  |           ^^^^^^^^^
  |
  = warning: this changes meaning in Rust 2021
  = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/IntoIterator-for-arrays.html>
  = note: `#[warn(array_into_iter)]` on by default
help: use `.iter()` instead of `.into_iter()` to avoid ambiguity
  |
3 | [1, 2, 3].iter().for_each(|n| { *n; });
  |           ~~~~
help: or use `IntoIterator::into_iter(..)` instead of `.into_iter()` to explicitly iterate by value
  |
3 | IntoIterator::into_iter([1, 2, 3]).for_each(|n| { *n; });
  | ++++++++++++++++++++++++         ~

```

### Explanation

自 Rust 1.53 以来，数组实现了 `IntoIterator`。然而，为了避免破坏，Rust 2015 和 2018 代码中的 `array.into_iter()` 仍将表现为`(&array).into_iter()`，就像 Rust 1.52 及更早版本一样，返回一个引用迭代器。这仅适用于方法调用语法 `array.into_iter()`，而不适用于其他语法，如 `for _ in array` 或 `IntoIterator::into_iter(array)`。

## asm-sub-register

`asm_sub_register` lint 检测仅使用寄存器子集进行内联汇编输入。

### Example

```rust,ignore (fails on non-x86_64)
#[cfg(target_arch="x86_64")]
use std::arch::asm;

fn main() {
    #[cfg(target_arch="x86_64")]
    unsafe {
        asm!("mov {0}, {0}", in(reg) 0i16);
    }
}
```

This will produce:

```text
warning: formatting may not be suitable for sub-register argument
 --> src/main.rs:7:19
  |
7 |         asm!("mov {0}, {0}", in(reg) 0i16);
  |                   ^^^  ^^^           ---- for this argument
  |
  = note: `#[warn(asm_sub_register)]` on by default
  = help: use the `x` modifier to have the register formatted as `ax`
  = help: or use the `r` modifier to keep the default formatting of `rax`
```

### Explanation

某些架构的寄存器可以使用不同的名称来引用寄存器的子集。默认情况下，编译器将使用完整寄存器大小的名称。要显式使用寄存器的子集，您可以在模板字符串操作数上使用修饰符来覆盖默认值，以指定要使用的子寄存器。如果您传入的数据类型小于默认寄存器大小的值，则会发出此 lint，以提醒您可能使用了错误的宽度。要修复此问题，请将建议的修饰符添加到模板中，或将值强制转换为正确的大小。

See [register template modifiers] in the reference for more details.

[register template modifiers]: https://doc.rust-lang.org/nightly/reference/inline-assembly.html#template-modifiers

## async-fn-in-trait

The `async_fn_in_trait` lint detects use of `async fn` in the
definition of a publicly-reachable trait.

### Example

```rust
pub trait Trait {
    async fn method(&self);
}
# fn main() {}
```

This will produce:

```text
error[E0706]: functions in traits cannot be declared `async`
 --> lint_example.rs:2:5
  |
2 |     async fn method(&self);
  |     -----^^^^^^^^^^^^^^^^^^
  |     |
  |     `async` because of this
  |
  = note: `async` trait functions are not currently supported
  = note: consider using the `async-trait` crate: https://crates.io/crates/async-trait
  = note: see issue #91611 <https://github.com/rust-lang/rust/issues/91611> for more information
  = help: add `#![feature(async_fn_in_trait)]` to the crate attributes to enable

```

### Explanation

When `async fn` is used in a trait definition, the trait does not
promise that the opaque [`Future`] returned by the associated function
or method will implement any [auto traits] such as [`Send`]. This may
be surprising and may make the associated functions or methods on the
trait less useful than intended. On traits exposed publicly from a
crate, this may affect downstream crates whose authors cannot alter
the trait definition.

For example, this code is invalid:

```rust,compile_fail
pub trait Trait {
    async fn method(&self) {}
}

fn test<T: Trait>(x: T) {
    fn spawn<T: Send>(_: T) {}
    spawn(x.method()); // Not OK.
}
```

This lint exists to warn authors of publicly-reachable traits that
they may want to consider desugaring the `async fn` to a normal `fn`
that returns an opaque `impl Future<..> + Send` type.

For example, instead of:

```rust
pub trait Trait {
    async fn method(&self) {}
}
```

The author of the trait may want to write:


```rust
use core::future::Future;
pub trait Trait {
    fn method(&self) -> impl Future<Output = ()> + Send { async {} }
}
```

This still allows the use of `async fn` within impls of the trait.
However, it also means that the trait will never be compatible with
impls where the returned [`Future`] of the method does not implement
`Send`.

Conversely, if the trait is used only locally, if it is never used in
generic functions, or if it is only used in single-threaded contexts
that do not care whether the returned [`Future`] implements [`Send`],
then the lint may be suppressed.

[`Future`]: https://doc.rust-lang.org/core/future/trait.Future.html
[`Send`]: https://doc.rust-lang.org/core/marker/trait.Send.html
[auto traits]: https://doc.rust-lang.org/reference/special-types-and-traits.html#auto-traits

## bad-asm-style

The `bad_asm_style` lint detects the use of the `.intel_syntax` and
`.att_syntax` directives.

### Example

```rust,ignore (fails on non-x86_64)
#[cfg(target_arch="x86_64")]
use std::arch::asm;

fn main() {
    #[cfg(target_arch="x86_64")]
    unsafe {
        asm!(
            ".att_syntax",
            "movq %{0}, %{0}", in(reg) 0usize
        );
    }
}
```

This will produce:

```text
warning: avoid using `.att_syntax`, prefer using `options(att_syntax)` instead
 --> src/main.rs:8:14
  |
8 |             ".att_syntax",
  |              ^^^^^^^^^^^
  |
  = note: `#[warn(bad_asm_style)]` on by default
```

### Explanation

On x86, `asm!` uses the intel assembly syntax by default. While this
can be switched using assembler directives like `.att_syntax`, using the
`att_syntax` option is recommended instead because it will also properly
prefix register placeholders with `%` as required by AT&T syntax.

## bare-trait-objects

`bare_trait_objects` lint 建议对 trait 对象使用 `dyn Trait`。 

### Example

```rust,edition2018
trait Trait { }

fn takes_trait_object(_: Box<Trait>) {
}
```

This will produce:

```text
warning: trait objects without an explicit `dyn` are deprecated
 --> lint_example.rs:4:30
  |
4 | fn takes_trait_object(_: Box<Trait>) {
  |                              ^^^^^
  |
  = warning: this is accepted in the current edition (Rust 2018) but is a hard error in Rust 2021!
  = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/warnings-promoted-to-error.html>
  = note: `#[warn(bare_trait_objects)]` on by default
help: use `dyn`
  |
4 | fn takes_trait_object(_: Box<dyn Trait>) {
  |                              +++

```

### Explanation

如果没有 `dyn` 关键字，当阅读代码时你是否是在查看 trait 对象这可能会造成模棱两可或困惑。`dyn` 关键字将其明确，并增加了一种对称性，与[`impl Trait`]形成对比。

[`impl Trait`]: https://doc.rust-lang.org/book/ch10-02-traits.html#traits-as-parameters

## break-with-label-and-loop

The `break_with_label_and_loop` lint detects labeled `break` expressions with
an unlabeled loop as their value expression.

### Example

```rust
'label: loop {
    break 'label loop { break 42; };
};
```

This will produce:

```text
warning: this labeled break expression is easy to confuse with an unlabeled break with a labeled value expression
 --> lint_example.rs:3:5
  |
3 |     break 'label loop { break 42; };
  |     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(break_with_label_and_loop)]` on by default
help: wrap this expression in parentheses
  |
3 |     break 'label (loop { break 42; });
  |                  +                  +

```

### Explanation

In Rust, loops can have a label, and `break` expressions can refer to that label to
break out of specific loops (and not necessarily the innermost one). `break` expressions
can also carry a value expression, which can be another loop. A labeled `break` with an
unlabeled loop as its value expression is easy to confuse with an unlabeled break with
a labeled loop and is thus discouraged (but allowed for compatibility); use parentheses
around the loop expression to silence this warning. Unlabeled `break` expressions with
labeled loops yield a hard error, which can also be silenced by wrapping the expression
in parentheses.

## byte-slice-in-packed-struct-with-derive

The `byte_slice_in_packed_struct_with_derive` lint detects cases where a byte slice field
(`[u8]`) or string slice field (`str`) is used in a `packed` struct that derives one or
more built-in traits.

### Example

```rust
#[repr(packed)]
#[derive(Hash)]
struct FlexZeroSlice {
    width: u8,
    data: [u8],
}
```

This will produce:

```text
warning: byte slice in a packed struct that derives a built-in trait
 --> lint_example.rs:6:5
  |
3 | #[derive(Hash)]
  |          ---- in this derive macro expansion
...
6 |     data: [u8],
  |     ^^^^^^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #107457 <https://github.com/rust-lang/rust/issues/107457>
  = help: consider implementing the trait by hand, or remove the `packed` attribute
  = note: `#[warn(byte_slice_in_packed_struct_with_derive)]` on by default
  = note: this warning originates in the derive macro `Hash` (in Nightly builds, run with -Z macro-backtrace for more info)

```

### Explanation

This was previously accepted but is being phased out, because fields in packed structs are
now required to implement `Copy` for `derive` to work. Byte slices and string slices are a
temporary exception because certain crates depended on them.

## clashing-extern-declarations

`clashing_extern_declarations` lint 用于检测当一个 `extern fn` 被声明为相同的名称但类型不同的情况。

### Example

```rust
mod m {
    extern "C" {
        fn foo();
    }
}

extern "C" {
    fn foo(_: u32);
}
```

This will produce:

```text
warning: `foo` redeclared with a different signature
 --> lint_example.rs:9:5
  |
4 |         fn foo();
  |         -------- `foo` previously declared here
...
9 |     fn foo(_: u32);
  |     ^^^^^^^^^^^^^^ this signature doesn't match the previous declaration
  |
  = note: expected `unsafe extern "C" fn()`
             found `unsafe extern "C" fn(u32)`
  = note: `#[warn(clashing_extern_declarations)]` on by default

```

### Explanation

因为同名的两个符号在链接时无法解析为两个不同的函数，且一个函数不能有两个类型，一个相冲突的外部声明可以肯定是个错误。检查以确保 `extern` 定义正确且有效，且考虑将它们统一在一个位置。

这个 lint 不能跨 crate 运行因为一个项目可能有依赖于相同外部函数的依赖项，但是外部函数以不同（但有效）的方式声明。例如，它们可能都为一个或多个参数声明一个不透明类型（最终会得到不同的类型），或者使用 `extern fn` 定义的语言中有效的转换类型，在这些情况下，编译器无法判定冲突的声明是不正确的。

## coherence-leak-check

`coherence_leak_check` lint 用于检测仅通过旧的泄露检查代码区分的特质的冲突实现。

### Example

```rust
trait SomeTrait { }
impl SomeTrait for for<'a> fn(&'a u8) { }
impl<'a> SomeTrait for fn(&'a u8) { }
```

This will produce:

```text
warning: conflicting implementations of trait `SomeTrait` for type `for<'a> fn(&'a u8)`
 --> lint_example.rs:4:1
  |
3 | impl SomeTrait for for<'a> fn(&'a u8) { }
  | ------------------------------------- first implementation here
4 | impl<'a> SomeTrait for fn(&'a u8) { }
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ conflicting implementation for `for<'a> fn(&'a u8)`
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #56105 <https://github.com/rust-lang/rust/issues/56105>
  = note: this behavior recently changed as a result of a bug fix; see rust-lang/rust#56105 for details
  = note: `#[warn(coherence_leak_check)]` on by default

```

### Explanation

过去编译器接受完全相同的函数的特质实现，仅仅是在生命周期绑定器的位置上有所不同。然而，由于借用检查器实现中的一个变化修复了一些bug，这种方式已经不再被允许。但是，由于这会影响到现有的代码，这是一个 [future-incompatible] lint，以便在未来将其转变为一个严重的错误。

依赖于此模式的代码应该引入"[newtypes]"，比如 `struct Foo(for<'a> fn(&'a u8))`。

更多细节请参见 [issue #56105]。

[issue #56105]: https://github.com/rust-lang/rust/issues/56105
[newtypes]: https://doc.rust-lang.org/book/ch19-04-advanced-types.html#using-the-newtype-pattern-for-type-safety-and-abstraction
[future-incompatible]: ../index.md#future-incompatible-lints

## confusable-idents

`confusable_idents` lint 检测容易混淆的标识符对。

### Example

```rust
// Latin Capital Letter E With Caron
pub const Ě: i32 = 1;
// Latin Capital Letter E With Breve
pub const Ĕ: i32 = 2;
```

This will produce:

```text
warning: found both `Ě` and `Ĕ` as identifiers, which look alike
 --> lint_example.rs:5:11
  |
3 | pub const Ě: i32 = 1;
  |           - other identifier used here
4 | // Latin Capital Letter E With Breve
5 | pub const Ĕ: i32 = 2;
  |           ^ this identifier can be confused with `Ě`
  |
  = note: `#[warn(confusable_idents)]` on by default

```

### Explanation

此 lint 当不同的标识符，在视觉上可能相似时发出警告，这可能会引起混淆。

混淆检测算法基于 [Unicode® Technical Standard #39 Unicode Security Mechanisms Section 4 Confusable Detection][TR39Confusable]。对于每个不同的标识符X，执行函数`skeleton(X)`。如果在同一crate中存在两个不同的标识符X和Y，且`skeleton(X) = skeleton(Y)`，则报告它。编译器使用相同的机制来检查标识符是否与关键字过于相似。

请注意，混淆字符集可能会随时间变化。请注意，如果你禁止这个 lint，现有代码将来可能会编译失败。

[TR39Confusable]: https://www.unicode.org/reports/tr39/#Confusable_Detection

## const-evaluatable-unchecked

`const_evaluatable_unchecked` lint 检测类型中使用的泛型常量。

### Example

```rust
const fn foo<T>() -> usize {
    if std::mem::size_of::<*mut T>() < 8 { // size of *mut T does not depend on T
        4
    } else {
        8
    }
}

fn test<T>() {
    let _ = [0; foo::<T>()];
}
```

This will produce:

```text
warning: cannot use constants which depend on generic parameters in types
  --> lint_example.rs:11:17
   |
11 |     let _ = [0; foo::<T>()];
   |                 ^^^^^^^^^^
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #76200 <https://github.com/rust-lang/rust/issues/76200>
   = note: `#[warn(const_evaluatable_unchecked)]` on by default

```

### Explanation

在 1.43 发行版本，会意外地允许在数组重复表达式中使用泛型参数。这是个[将来不兼容][future-incompatible]的 lint，将来会转化为固有错误。更多细节描述和可能的修复请参阅 [issue #76200]。

[future-incompatible]: ../index.md#future-incompatible-lints
[issue #76200]: https://github.com/rust-lang/rust/issues/76200

## const-item-mutation

`const_item_mutation` lint 检测试图更改 `const` 项。

### Example

```rust
const FOO: [i32; 1] = [0];

fn main() {
    FOO[0] = 1;
    // This will print "[0]".
    println!("{:?}", FOO);
}
```

This will produce:

```text
warning: attempting to modify a `const` item
 --> lint_example.rs:4:5
  |
4 |     FOO[0] = 1;
  |     ^^^^^^^^^^
  |
  = note: each usage of a `const` item creates a new temporary; the original `const` item will not be modified
note: `const` item defined here
 --> lint_example.rs:1:1
  |
1 | const FOO: [i32; 1] = [0];
  | ^^^^^^^^^^^^^^^^^^^
  = note: `#[warn(const_item_mutation)]` on by default

```

### Explanation

尝试直接修改一个 `const` 项几乎总是一个错误。在上面的例子中，发生的情况是 `const` 的一个临时副本被修改了，但原始的 `const` 没有被修改。每当你通过名称引用 `const`（例如上面的例子中的`FOO`）时，该值的单独副本会在该位置进行内联。

此 lint 检查是否直接写入字段（`FOO.field = some_value`）或数组条目（`FOO[0] = val`），或对 const 项进行可变引用（`&mut FOO`），包括通过自动解引用（`FOO.some_mut_self_method()`）。

根据你试图完成的目标，有各种替代方案：

* 首先，重新考虑使用可变全局变量，因为它们可能难以正确使用，并可能使代码更难以使用或理解。
* 如果你试图对全局变量进行一次性初始化：
	+ 如果值可以在编译时计算，考虑使用与 const 兼容的值（参见 [Constant Evaluation]）。
	+ 对于更复杂的单次初始化情况，考虑使用第三方 crate，如 [`lazy_static`] 或 [`once_cell`]。
	+ 如果你正在使用 [nightly channel]，请考虑标准库中的新 [`lazy`] 模块。
* 如果你真正需要一个可变的全局变量，考虑使用一个 [`static`]，它有多种选择：
	+ 简单数据类型可以直接定义，并使用 [`atomic`] 类型进行修改。
	+ 更复杂的类型可以放置在同步原语中，如 [`Mutex`]，它可以使用上面列出的选项之一进行初始化。
	+ 可变的 `static` 是一个低级原语，需要 `unsafe`。通常这应该避免使用，而倾向于使用更高级别的东西，如上面列出的这些。

[Constant Evaluation]: https://doc.rust-lang.org/reference/const_eval.html
[`static`]: https://doc.rust-lang.org/reference/items/static-items.html
[mutable `static`]: https://doc.rust-lang.org/reference/items/static-items.html#mutable-statics
[`lazy`]: https://doc.rust-lang.org/nightly/std/lazy/index.html
[`lazy_static`]: https://crates.io/crates/lazy_static
[`once_cell`]: https://crates.io/crates/once_cell
[`atomic`]: https://doc.rust-lang.org/std/sync/atomic/index.html
[`Mutex`]: https://doc.rust-lang.org/std/sync/struct.Mutex.html

## const-patterns-without-partial-eq

The `const_patterns_without_partial_eq` lint detects constants that are used in patterns,
whose type does not implement `PartialEq`.

### Example

```rust,compile_fail
#![deny(const_patterns_without_partial_eq)]

trait EnumSetType {
   type Repr;
}

enum Enum8 { }
impl EnumSetType for Enum8 {
    type Repr = u8;
}

#[derive(PartialEq, Eq)]
struct EnumSet<T: EnumSetType> {
    __enumset_underlying: T::Repr,
}

const CONST_SET: EnumSet<Enum8> = EnumSet { __enumset_underlying: 3 };

fn main() {
    match CONST_SET {
        CONST_SET => { /* ok */ }
        _ => panic!("match fell through?"),
    }
}
```

This will produce:

```text
error: to use a constant of type `EnumSet<Enum8>` in a pattern, the type must implement `PartialEq`
  --> lint_example.rs:21:9
   |
21 |         CONST_SET => { /* ok */ }
   |         ^^^^^^^^^
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #116122 <https://github.com/rust-lang/rust/issues/116122>
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(const_patterns_without_partial_eq)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Previous versions of Rust accepted constants in patterns, even if those constants' types
did not have `PartialEq` implemented. The compiler falls back to comparing the value
field-by-field. In the future we'd like to ensure that pattern matching always
follows `PartialEq` semantics, so that trait bound will become a requirement for
matching on constants.

## dead-code

`dead_code` lint 检测未使用，未导出的代码。

### Example

```rust
fn foo() {}
```

This will produce:

```text
warning: function `foo` is never used
 --> lint_example.rs:2:4
  |
2 | fn foo() {}
  |    ^^^
  |
  = note: `#[warn(dead_code)]` on by default

```

### Explanation

未使用的代码表示错误或未完成的代码。要使单个项的警告静默，在名称前加上下划线例如 `_foo`。如果打算将项导出 `crate` 之外，考虑添加可见修饰符如 `pub`。否则请考虑移除未使用的代码。

## deprecated

`deprecated` lint 检测不推荐使用的项。

### Example

```rust
#[deprecated]
fn foo() {}

fn bar() {
    foo();
}
```

This will produce:

```text
warning: use of deprecated function `main::foo`
 --> lint_example.rs:6:5
  |
6 |     foo();
  |     ^^^
  |
  = note: `#[warn(deprecated)]` on by default

```

### Explanation

物品可以通过 [`deprecated` attribute] 标记为 “已弃用”，以表示它们不应再被使用。通常，该属性应包括关于应使用什么的注释，或查看文档。

[`deprecated` attribute]: https://doc.rust-lang.org/reference/attributes/diagnostics.html#the-deprecated-attribute

## deprecated-where-clause-location

The `deprecated_where_clause_location` lint detects when a where clause in front of the equals
in an associated type.

### Example

```rust
trait Trait {
  type Assoc<'a> where Self: 'a;
}

impl Trait for () {
  type Assoc<'a> where Self: 'a = ();
}
```

This will produce:

```text
warning: where clause not allowed here
 --> lint_example.rs:7:18
  |
7 |   type Assoc<'a> where Self: 'a = ();
  |                  ^^^^^^^^^^^^^^
  |
  = note: see issue #89122 <https://github.com/rust-lang/rust/issues/89122> for more information
  = note: `#[warn(deprecated_where_clause_location)]` on by default
help: move it to the end of the type declaration
  |
7 -   type Assoc<'a> where Self: 'a = ();
7 +   type Assoc<'a>  = () where Self: 'a;
  |

```

### Explanation

The preferred location for where clauses on associated types
is after the type. However, for most of generic associated types development,
it was only accepted before the equals. To provide a transition period and
further evaluate this change, both are currently accepted. At some point in
the future, this may be disallowed at an edition boundary; but, that is
undecided currently.

## deref-into-dyn-supertrait

The `deref_into_dyn_supertrait` lint is output whenever there is a use of the
`Deref` implementation with a `dyn SuperTrait` type as `Output`.

These implementations will become shadowed when the `trait_upcasting` feature is stabilized.
The `deref` functions will no longer be called implicitly, so there might be behavior change.

### Example

```rust,compile_fail
#![deny(deref_into_dyn_supertrait)]
#![allow(dead_code)]

use core::ops::Deref;

trait A {}
trait B: A {}
impl<'a> Deref for dyn 'a + B {
    type Target = dyn A;
    fn deref(&self) -> &Self::Target {
        todo!()
    }
}

fn take_a(_: &dyn A) { }

fn take_b(b: &dyn B) {
    take_a(b);
}
```

This will produce:

```text
error: `(dyn B + 'a)` implements `Deref` with supertrait `A` as target
  --> lint_example.rs:9:1
   |
9  | impl<'a> Deref for dyn 'a + B {
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
10 |     type Target = dyn A;
   |     -------------------- target type is set here
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #89460 <https://github.com/rust-lang/rust/issues/89460>
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(deref_into_dyn_supertrait)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

The dyn upcasting coercion feature adds new coercion rules, taking priority
over certain other coercion rules, which will cause some behavior change.

## deref-nullptr

The `deref_nullptr` lint detects when an null pointer is dereferenced,
which causes [undefined behavior].

### Example

```rust,no_run
# #![allow(unused)]
use std::ptr;
unsafe {
    let x = &*ptr::null::<i32>();
    let x = ptr::addr_of!(*ptr::null::<i32>());
    let x = *(0 as *const i32);
}
```

This will produce:

```text
warning: dereferencing a null pointer
 --> lint_example.rs:5:14
  |
5 |     let x = &*ptr::null::<i32>();
  |              ^^^^^^^^^^^^^^^^^^^ this code causes undefined behavior when executed
  |
  = note: `#[warn(deref_nullptr)]` on by default


warning: dereferencing a null pointer
 --> lint_example.rs:6:27
  |
6 |     let x = ptr::addr_of!(*ptr::null::<i32>());
  |                           ^^^^^^^^^^^^^^^^^^^ this code causes undefined behavior when executed


warning: dereferencing a null pointer
 --> lint_example.rs:7:13
  |
7 |     let x = *(0 as *const i32);
  |             ^^^^^^^^^^^^^^^^^^ this code causes undefined behavior when executed

```

### Explanation

Dereferencing a null pointer causes [undefined behavior] even as a place expression,
like `&*(0 as *const i32)` or `addr_of!(*(0 as *const i32))`.

[undefined behavior]: https://doc.rust-lang.org/reference/behavior-considered-undefined.html

## drop-bounds

`drop_bounds` lint 检查使用 `std::ops::Drop` 作为约束的泛型。

### Example

```rust
fn foo<T: Drop>() {}
```

This will produce:

```text
warning: bounds on `T: Drop` are most likely incorrect, consider instead using `std::mem::needs_drop` to detect whether a type can be trivially dropped
 --> lint_example.rs:2:11
  |
2 | fn foo<T: Drop>() {}
  |           ^^^^
  |
  = note: `#[warn(drop_bounds)]` on by default

```

### Explanation

`T: Drop` 这种形式的泛型特质约束很可能会误导程序员，并非程序员真正的意图（他们可能应该使用 `std::mem::needs_drop`）。

`Drop` 约束实际上并不能指示一个类型是否可以被轻易地丢弃，因为包含 `Drop` 类型的复合类型并不一定实现 `Drop`。很粗浅地，人们可能会试图编写一个假设类型可以被轻易地丢弃的实现，同时为一个 `T: Drop` 的特殊化版本提供实际的析构函数调用。然而，这会在例如 `T` 是 `String` 的情况下失效，`String` 本身并不实现 `Drop`，但是它包含一个实现了 `Drop` 的 `Vec`，所以假设 `T` 可以被轻易地丢弃在这里会导致内存泄漏。

此外，`Drop` 特质只包含一个方法，即 `Drop::drop`，在用户代码中可能不会被显式调用(`E0040`)，所以除了在某些晦涩的角落情况外，实际上没有使用场景会在特质约束中使用 `Drop`，这些角落情况可以使用 `#[allow(drop_bounds)]`。

## dropping-copy-types

The `dropping_copy_types` lint checks for calls to `std::mem::drop` with a value
that derives the Copy trait.

### Example

```rust
let x: i32 = 42; // i32 implements Copy
std::mem::drop(x); // A copy of x is passed to the function, leaving the
                   // original unaffected
```

This will produce:

```text
warning: calls to `std::mem::drop` with a value that implements `Copy` does nothing
 --> lint_example.rs:3:1
  |
3 | std::mem::drop(x); // A copy of x is passed to the function, leaving the
  | ^^^^^^^^^^^^^^^-^
  |                |
  |                argument has type `i32`
  |
  = note: use `let _ = ...` to ignore the expression or result
  = note: `#[warn(dropping_copy_types)]` on by default

```

### Explanation

Calling `std::mem::drop` [does nothing for types that
implement Copy](https://doc.rust-lang.org/std/mem/fn.drop.html), since the
value will be copied and moved into the function on invocation.

## dropping-references

The `dropping_references` lint checks for calls to `std::mem::drop` with a reference
instead of an owned value.

### Example

```rust
# fn operation_that_requires_mutex_to_be_unlocked() {} // just to make it compile
# let mutex = std::sync::Mutex::new(1); // just to make it compile
let mut lock_guard = mutex.lock();
std::mem::drop(&lock_guard); // Should have been drop(lock_guard), mutex
// still locked
operation_that_requires_mutex_to_be_unlocked();
```

This will produce:

```text
warning: calls to `std::mem::drop` with a reference instead of an owned value does nothing
 --> lint_example.rs:5:1
  |
5 | std::mem::drop(&lock_guard); // Should have been drop(lock_guard), mutex
  | ^^^^^^^^^^^^^^^-----------^
  |                |
  |                argument has type `&Result<MutexGuard<'_, i32>, PoisonError<MutexGuard<'_, i32>>>`
  |
  = note: use `let _ = ...` to ignore the expression or result
  = note: `#[warn(dropping_references)]` on by default

```

### Explanation

Calling `drop` on a reference will only drop the
reference itself, which is a no-op. It will not call the `drop` method (from
the `Drop` trait implementation) on the underlying referenced value, which
is likely what was intended.

## duplicate-macro-attributes

The `duplicate_macro_attributes` lint detects when a `#[test]`-like built-in macro
attribute is duplicated on an item. This lint may trigger on `bench`, `cfg_eval`, `test`
and `test_case`.

### Example

```rust,ignore (needs --test)
#[test]
#[test]
fn foo() {}
```

This will produce:

```text
warning: duplicated attribute
 --> src/lib.rs:2:1
  |
2 | #[test]
  | ^^^^^^^
  |
  = note: `#[warn(duplicate_macro_attributes)]` on by default
```

### Explanation

A duplicated attribute may erroneously originate from a copy-paste and the effect of it
being duplicated may not be obvious or desirable.

For instance, doubling the `#[test]` attributes registers the test to be run twice with no
change to its environment.

[issue #90979]: https://github.com/rust-lang/rust/issues/90979

## dyn-drop

The `dyn_drop` lint checks for trait objects with `std::ops::Drop`.

### Example

```rust
fn foo(_x: Box<dyn Drop>) {}
```

This will produce:

```text
warning: types that do not implement `Drop` can still have drop glue, consider instead using `std::mem::needs_drop` to detect whether a type is trivially dropped
 --> lint_example.rs:2:20
  |
2 | fn foo(_x: Box<dyn Drop>) {}
  |                    ^^^^
  |
  = note: `#[warn(dyn_drop)]` on by default

```

### Explanation

A trait object bound of the form `dyn Drop` is most likely misleading
and not what the programmer intended.

`Drop` bounds do not actually indicate whether a type can be trivially
dropped or not, because a composite type containing `Drop` types does
not necessarily implement `Drop` itself. Naïvely, one might be tempted
to write a deferred drop system, to pull cleaning up memory out of a
latency-sensitive code path, using `dyn Drop` trait objects. However,
this breaks down e.g. when `T` is `String`, which does not implement
`Drop`, but should probably be accepted.

To write a trait object bound that accepts anything, use a placeholder
trait with a blanket implementation.

```rust
trait Placeholder {}
impl<T> Placeholder for T {}
fn foo(_x: Box<dyn Placeholder>) {}
```

## elided-lifetimes-in-associated-constant

The `elided_lifetimes_in_associated_constant` lint detects elided lifetimes
that were erroneously allowed in associated constants.

### Example

```rust,compile_fail
#![deny(elided_lifetimes_in_associated_constant)]

struct Foo;

impl Foo {
    const STR: &str = "hello, world";
}
```

This will produce:

```text
error: `&` without an explicit lifetime name cannot be used here
 --> lint_example.rs:7:16
  |
7 |     const STR: &str = "hello, world";
  |                ^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #115010 <https://github.com/rust-lang/rust/issues/115010>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(elided_lifetimes_in_associated_constant)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
help: use the `'static` lifetime
  |
7 |     const STR: &'static str = "hello, world";
  |                 +++++++

```

### Explanation

Previous version of Rust

Implicit static-in-const behavior was decided [against] for associated
constants because of ambiguity. This, however, regressed and the compiler
erroneously treats elided lifetimes in associated constants as lifetime
parameters on the impl.

This is a [future-incompatible] lint to transition this to a
hard error in the future.

[against]: https://github.com/rust-lang/rust/issues/38831
[future-incompatible]: ../index.md#future-incompatible-lints

## ellipsis-inclusive-range-patterns

`ellipsis_inclusive_range_patterns` lint 检测 `...` 这种已经被遗弃的[范围模式]。

[`...` range pattern]: https://doc.rust-lang.org/reference/patterns.html#range-patterns

### Example

```rust,edition2018
let x = 123;
match x {
    0...100 => {}
    _ => {}
}
```

This will produce:

```text
warning: `...` range patterns are deprecated
 --> lint_example.rs:4:6
  |
4 |     0...100 => {}
  |      ^^^ help: use `..=` for an inclusive range
  |
  = warning: this is accepted in the current edition (Rust 2018) but is a hard error in Rust 2021!
  = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/warnings-promoted-to-error.html>
  = note: `#[warn(ellipsis_inclusive_range_patterns)]` on by default

```

### Explanation

`...` 范围模式的语法已更改为 `..=`，以避免与 [`..` 范围表达式][`..` range expression] 可能产生的混淆。请使用新形式。

[`..` range expression]: https://doc.rust-lang.org/reference/expressions/range-expr.html

## exported-private-dependencies

`exported_private_dependencies` lint 检测在公共接口公开的私有依赖。

### Example

```rust,ignore (needs-dependency)
pub fn foo() -> Option<some_private_dependency::Thing> {
    None
}
```

This will produce:

```text
warning: type `bar::Thing` from private dependency 'bar' in public interface
 --> src/lib.rs:3:1
  |
3 | pub fn foo() -> Option<bar::Thing> {
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(exported_private_dependencies)]` on by default
```

### Explanation

依赖项可以被标记为 “private”，以表明它们不会在 crate 的公共接口中暴露。Cargo 可以利用这一点独立解析这些依赖项，因为它可以假设不需要将这些依赖项与使用相同依赖项的其他包进行统一。这个 lint 是违反这种合约的一个指示。

要解决这个问题，避免在你的公共接口中暴露依赖项。或者，将依赖项切换为公共依赖项。

请注意，此功能仅在 nightly channel 上可用。有关更多详细信息，请参阅 [RFC 1977] 以及 [Cargo 文档][Cargo documentation]。

[RFC 1977]: https://github.com/rust-lang/rfcs/blob/master/text/1977-public-private-dependencies.md
[Cargo documentation]: https://doc.rust-lang.org/nightly/cargo/reference/unstable.html#public-dependency

## for-loops-over-fallibles

The `for_loops_over_fallibles` lint checks for `for` loops over `Option` or `Result` values.

### Example

```rust
let opt = Some(1);
for x in opt { /* ... */}
```

This will produce:

```text
warning: for loop over an `Option`. This is more readably written as an `if let` statement
 --> lint_example.rs:3:10
  |
3 | for x in opt { /* ... */}
  |          ^^^
  |
  = note: `#[warn(for_loops_over_fallibles)]` on by default
help: to check pattern in a loop use `while let`
  |
3 | while let Some(x) = opt { /* ... */}
  | ~~~~~~~~~~~~~~~ ~~~
help: consider using `if let` to clear intent
  |
3 | if let Some(x) = opt { /* ... */}
  | ~~~~~~~~~~~~ ~~~

```

### Explanation

Both `Option` and `Result` implement `IntoIterator` trait, which allows using them in a `for` loop.
`for` loop over `Option` or `Result` will iterate either 0 (if the value is `None`/`Err(_)`)
or 1 time (if the value is `Some(_)`/`Ok(_)`). This is not very useful and is more clearly expressed
via `if let`.

`for` loop can also be accidentally written with the intention to call a function multiple times,
while the function returns `Some(_)`, in these cases `while let` loop should be used instead.

The "intended" use of `IntoIterator` implementations for `Option` and `Result` is passing them to
generic code that expects something implementing `IntoIterator`. For example using `.chain(option)`
to optionally add a value to an iterator.

## forbidden-lint-groups

The `forbidden_lint_groups` lint detects violations of
`forbid` applied to a lint group. Due to a bug in the compiler,
these used to be overlooked entirely. They now generate a warning.

### Example

```rust
#![forbid(warnings)]
#![deny(bad_style)]

fn main() {}
```

This will produce:

```text
warning: deny(bad_style) incompatible with previous forbid
 --> lint_example.rs:2:9
  |
1 | #![forbid(warnings)]
  |           -------- `forbid` level set here
2 | #![deny(bad_style)]
  |         ^^^^^^^^^ overruled by previous forbid
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #81670 <https://github.com/rust-lang/rust/issues/81670>
  = note: `#[warn(forbidden_lint_groups)]` on by default

```

### Recommended fix

If your crate is using `#![forbid(warnings)]`,
we recommend that you change to `#![deny(warnings)]`.

### Explanation

Due to a compiler bug, applying `forbid` to lint groups
previously had no effect. The bug is now fixed but instead of
enforcing `forbid` we issue this future-compatibility warning
to avoid breaking existing crates.

## forgetting-copy-types

The `forgetting_copy_types` lint checks for calls to `std::mem::forget` with a value
that derives the Copy trait.

### Example

```rust
let x: i32 = 42; // i32 implements Copy
std::mem::forget(x); // A copy of x is passed to the function, leaving the
                     // original unaffected
```

This will produce:

```text
warning: calls to `std::mem::forget` with a value that implements `Copy` does nothing
 --> lint_example.rs:3:1
  |
3 | std::mem::forget(x); // A copy of x is passed to the function, leaving the
  | ^^^^^^^^^^^^^^^^^-^
  |                  |
  |                  argument has type `i32`
  |
  = note: use `let _ = ...` to ignore the expression or result
  = note: `#[warn(forgetting_copy_types)]` on by default

```

### Explanation

Calling `std::mem::forget` [does nothing for types that
implement Copy](https://doc.rust-lang.org/std/mem/fn.drop.html) since the
value will be copied and moved into the function on invocation.

An alternative, but also valid, explanation is that Copy types do not
implement the Drop trait, which means they have no destructors. Without a
destructor, there is nothing for `std::mem::forget` to ignore.

## forgetting-references

The `forgetting_references` lint checks for calls to `std::mem::forget` with a reference
instead of an owned value.

### Example

```rust
let x = Box::new(1);
std::mem::forget(&x); // Should have been forget(x), x will still be dropped
```

This will produce:

```text
warning: calls to `std::mem::forget` with a reference instead of an owned value does nothing
 --> lint_example.rs:3:1
  |
3 | std::mem::forget(&x); // Should have been forget(x), x will still be dropped
  | ^^^^^^^^^^^^^^^^^--^
  |                  |
  |                  argument has type `&Box<i32>`
  |
  = note: use `let _ = ...` to ignore the expression or result
  = note: `#[warn(forgetting_references)]` on by default

```

### Explanation

Calling `forget` on a reference will only forget the
reference itself, which is a no-op. It will not forget the underlying
referenced value, which is likely what was intended.

## function-item-references

`function_item_references` lint 检测使用 [`fmt::Pointer`] 格式化或转换的函数引用。

[`fmt::Pointer`]: https://doc.rust-lang.org/std/fmt/trait.Pointer.html

### Example

```rust
fn foo() { }

fn main() {
    println!("{:p}", &foo);
}
```

This will produce:

```text
warning: taking a reference to a function item does not give a function pointer
 --> lint_example.rs:4:22
  |
4 |     println!("{:p}", &foo);
  |                      ^^^^ help: cast `foo` to obtain a function pointer: `foo as fn()`
  |
  = note: `#[warn(function_item_references)]` on by default

```

### Explanation

引用一个函数可能被误认为是获取函数指针的一种方式。将引用格式化为指针或对其进行转换的时候可能会产生意外的结果。当函数引用被格式化为指针，作为 [`fmt::Pointer`] 约束的参数传递或转换时，就会触发该 lint。

## hidden-glob-reexports

The `hidden_glob_reexports` lint detects cases where glob re-export items are shadowed by
private items.

### Example

```rust,compile_fail
#![deny(hidden_glob_reexports)]

pub mod upstream {
    mod inner { pub struct Foo {}; pub struct Bar {}; }
    pub use self::inner::*;
    struct Foo {} // private item shadows `inner::Foo`
}

// mod downstream {
//     fn test() {
//         let _ = crate::upstream::Foo; // inaccessible
//     }
// }

pub fn main() {}
```

This will produce:

```text
error: private item shadows public glob re-export
 --> lint_example.rs:6:5
  |
6 |     struct Foo {} // private item shadows `inner::Foo`
  |     ^^^^^^^^^^^^^
  |
note: the name `Foo` in the type namespace is supposed to be publicly re-exported here
 --> lint_example.rs:5:13
  |
5 |     pub use self::inner::*;
  |             ^^^^^^^^^^^^^^
note: but the private item here shadows it
 --> lint_example.rs:6:5
  |
6 |     struct Foo {} // private item shadows `inner::Foo`
  |     ^^^^^^^^^^^^^
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(hidden_glob_reexports)]
  |         ^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

This was previously accepted without any errors or warnings but it could silently break a
crate's downstream user code. If the `struct Foo` was added, `dep::inner::Foo` would
silently become inaccessible and trigger a "`struct `Foo` is private`" visibility error at
the downstream use site.

## illegal-floating-point-literal-pattern

`illegal_floating_point_literal_pattern` lint 检测用于模式中的浮点数字面量。

### Example

```rust
let x = 42.0;

match x {
    5.0 => {}
    _ => {}
}
```

This will produce:

```text
warning: floating-point types cannot be used in patterns
 --> lint_example.rs:5:5
  |
5 |     5.0 => {}
  |     ^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #41620 <https://github.com/rust-lang/rust/issues/41620>
  = note: `#[warn(illegal_floating_point_literal_pattern)]` on by default

```

### Explanation

编译器的早期版本接受了模式中的浮点数字面量，但后来确定这是一个错误。在模式中，与 “结构相等性” 相比，浮点值的比较语义可能不明确。通常，您可以通过使用 [match guard] 来解决这个问题，例如：

```rust
# let x = 42.0;

match x {
    y if y == 5.0 => {}
    _ => {}
}
```

这是一个[将来不兼容][future-incompatible] 的 lint，将来会转化为固有错误。更多细节请参阅 [issue #41620]。

[issue #41620]: https://github.com/rust-lang/rust/issues/41620
[match guard]: https://doc.rust-lang.org/reference/expressions/match-expr.html#match-guards
[future-incompatible]: ../index.md#future-incompatible-lints

## improper-ctypes

`improper_ctypes` lint 检测在外部模块中错误使用的类型。

### Example

```rust
extern "C" {
    static STATIC: String;
}
```

This will produce:

```text
warning: `extern` block uses type `String`, which is not FFI-safe
 --> lint_example.rs:3:20
  |
3 |     static STATIC: String;
  |                    ^^^^^^ not FFI-safe
  |
  = help: consider adding a `#[repr(C)]` or `#[repr(transparent)]` attribute to this struct
  = note: this struct has unspecified layout
  = note: `#[warn(improper_ctypes)]` on by default

```

### Explanation

编译器有几项检查来验证 `extern` 块中使用的类型是否安全并遵循某些规则，以确保与外部接口的兼容性。当编译器检测到定义中可能的错误时，就会发出这个lint。lint 通常会提供问题的描述，以及可能的解决方法的提示。

## improper-ctypes-definitions

The `improper_ctypes_definitions` lint detects incorrect use of
[`extern` function] definitions.

[`extern` function]: https://doc.rust-lang.org/reference/items/functions.html#extern-function-qualifier

### Example

```rust
# #![allow(unused)]
pub extern "C" fn str_type(p: &str) { }
```

This will produce:

```text
warning: `extern` fn uses type `str`, which is not FFI-safe
 --> lint_example.rs:3:31
  |
3 | pub extern "C" fn str_type(p: &str) { }
  |                               ^^^^ not FFI-safe
  |
  = help: consider using `*const u8` and a length instead
  = note: string slices have no C equivalent
  = note: `#[warn(improper_ctypes_definitions)]` on by default

```

### Explanation

There are many parameter and return types that may be specified in an
`extern` function that are not compatible with the given ABI. This
lint is an alert that these types should not be used. The lint usually
should provide a description of the issue, along with possibly a hint
on how to resolve it.

## incomplete-features

The `incomplete_features` lint detects unstable features enabled with
the [`feature` attribute] that may function improperly in some or all
cases.

[`feature` attribute]: https://doc.rust-lang.org/nightly/unstable-book/

### Example

```rust
#![feature(generic_const_exprs)]
```

This will produce:

```text
warning: the feature `generic_const_exprs` is incomplete and may not be safe to use and/or cause compiler crashes
 --> lint_example.rs:1:12
  |
1 | #![feature(generic_const_exprs)]
  |            ^^^^^^^^^^^^^^^^^^^
  |
  = note: see issue #76560 <https://github.com/rust-lang/rust/issues/76560> for more information
  = note: `#[warn(incomplete_features)]` on by default

```

### Explanation

Although it is encouraged for people to experiment with unstable
features, some of them are known to be incomplete or faulty. This lint
is a signal that the feature has not yet been finished, and you may
experience problems with it.

## indirect-structural-match

The `indirect_structural_match` lint detects a `const` in a pattern
that manually implements [`PartialEq`] and [`Eq`].

[`PartialEq`]: https://doc.rust-lang.org/std/cmp/trait.PartialEq.html
[`Eq`]: https://doc.rust-lang.org/std/cmp/trait.Eq.html

### Example

```rust,compile_fail
#![deny(indirect_structural_match)]

struct NoDerive(i32);
impl PartialEq for NoDerive { fn eq(&self, _: &Self) -> bool { false } }
impl Eq for NoDerive { }
#[derive(PartialEq, Eq)]
struct WrapParam<T>(T);
const WRAP_INDIRECT_PARAM: & &WrapParam<NoDerive> = & &WrapParam(NoDerive(0));
fn main() {
    match WRAP_INDIRECT_PARAM {
        WRAP_INDIRECT_PARAM => { }
        _ => { }
    }
}
```

This will produce:

```text
error: to use a constant of type `NoDerive` in a pattern, `NoDerive` must be annotated with `#[derive(PartialEq, Eq)]`
  --> lint_example.rs:11:9
   |
11 |         WRAP_INDIRECT_PARAM => { }
   |         ^^^^^^^^^^^^^^^^^^^
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #62411 <https://github.com/rust-lang/rust/issues/62411>
   = note: the traits must be derived, manual `impl`s are not sufficient
   = note: see https://doc.rust-lang.org/stable/std/marker/trait.StructuralEq.html for details
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(indirect_structural_match)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

The compiler unintentionally accepted this form in the past. This is a
[future-incompatible] lint to transition this to a hard error in the
future. See [issue #62411] for a complete description of the problem,
and some possible solutions.

[issue #62411]: https://github.com/rust-lang/rust/issues/62411
[future-incompatible]: ../index.md#future-incompatible-lints

## inline-no-sanitize

The `inline_no_sanitize` lint detects incompatible use of
[`#[inline(always)]`][inline] and [`#[no_sanitize(...)]`][no_sanitize].

[inline]: https://doc.rust-lang.org/reference/attributes/codegen.html#the-inline-attribute
[no_sanitize]: https://doc.rust-lang.org/nightly/unstable-book/language-features/no-sanitize.html

### Example

```rust
#![feature(no_sanitize)]

#[inline(always)]
#[no_sanitize(address)]
fn x() {}

fn main() {
    x()
}
```

This will produce:

```text
warning: `no_sanitize` will have no effect after inlining
 --> lint_example.rs:4:1
  |
4 | #[no_sanitize(address)]
  | ^^^^^^^^^^^^^^^^^^^^^^^
  |
note: inlining requested here
 --> lint_example.rs:3:1
  |
3 | #[inline(always)]
  | ^^^^^^^^^^^^^^^^^
  = note: `#[warn(inline_no_sanitize)]` on by default

```

### Explanation

The use of the [`#[inline(always)]`][inline] attribute prevents the
the [`#[no_sanitize(...)]`][no_sanitize] attribute from working.
Consider temporarily removing `inline` attribute.

## internal-features

The `internal_features` lint detects unstable features enabled with
the [`feature` attribute] that are internal to the compiler or standard
library.

[`feature` attribute]: https://doc.rust-lang.org/nightly/unstable-book/

### Example

```rust
#![feature(rustc_attrs)]
```

This will produce:

```text
warning: the feature `rustc_attrs` is internal to the compiler or standard library
 --> lint_example.rs:1:12
  |
1 | #![feature(rustc_attrs)]
  |            ^^^^^^^^^^^
  |
  = note: using it is strongly discouraged
  = note: `#[warn(internal_features)]` on by default

```

### Explanation

These features are an implementation detail of the compiler and standard
library and are not supposed to be used in user code.

## invalid-doc-attributes

The `invalid_doc_attributes` lint detects when the `#[doc(...)]` is
misused.

### Example

```rust,compile_fail
#![deny(warnings)]

pub mod submodule {
    #![doc(test(no_crate_inject))]
}
```

This will produce:

```text
error: this attribute can only be applied at the crate level
 --> lint_example.rs:5:12
  |
5 |     #![doc(test(no_crate_inject))]
  |            ^^^^^^^^^^^^^^^^^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #82730 <https://github.com/rust-lang/rust/issues/82730>
  = note: read <https://doc.rust-lang.org/nightly/rustdoc/the-doc-attribute.html#at-the-crate-level> for more information
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(warnings)]
  |         ^^^^^^^^
  = note: `#[deny(invalid_doc_attributes)]` implied by `#[deny(warnings)]`

```

### Explanation

Previously, incorrect usage of the `#[doc(..)]` attribute was not
being validated. Usually these should be rejected as a hard error,
but this lint was introduced to avoid breaking any existing
crates which included them.

This is a [future-incompatible] lint to transition this to a hard
error in the future. See [issue #82730] for more details.

[issue #82730]: https://github.com/rust-lang/rust/issues/82730

## invalid-from-utf8

The `invalid_from_utf8` lint checks for calls to
`std::str::from_utf8` and `std::str::from_utf8_mut`
with a known invalid UTF-8 value.

### Example

```rust
# #[allow(unused)]
std::str::from_utf8(b"Ru\x82st");
```

This will produce:

```text
warning: calls to `std::str::from_utf8` with a invalid literal always return an error
 --> lint_example.rs:3:1
  |
3 | std::str::from_utf8(b"Ru\x82st");
  | ^^^^^^^^^^^^^^^^^^^^-----------^
  |                     |
  |                     the literal was valid UTF-8 up to the 2 bytes
  |
  = note: `#[warn(invalid_from_utf8)]` on by default

```

### Explanation

Trying to create such a `str` would always return an error as per documentation
for `std::str::from_utf8` and `std::str::from_utf8_mut`.

## invalid-macro-export-arguments

The `invalid_macro_export_arguments` lint detects cases where `#[macro_export]` is being used with invalid arguments.

### Example

```rust,compile_fail
#![deny(invalid_macro_export_arguments)]

#[macro_export(invalid_parameter)]
macro_rules! myMacro {
   () => {
        // [...]
   }
}

#[macro_export(too, many, items)]
```

This will produce:

```text
error: `invalid_parameter` isn't a valid `#[macro_export]` argument
 --> lint_example.rs:4:16
  |
4 | #[macro_export(invalid_parameter)]
  |                ^^^^^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(invalid_macro_export_arguments)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

The only valid argument is `#[macro_export(local_inner_macros)]` or no argument (`#[macro_export]`).
You can't have multiple arguments in a `#[macro_export(..)]`, or mention arguments other than `local_inner_macros`.


## invalid-nan-comparisons

The `invalid_nan_comparisons` lint checks comparison with `f32::NAN` or `f64::NAN`
as one of the operand.

### Example

```rust
let a = 2.3f32;
if a == f32::NAN {}
```

This will produce:

```text
warning: incorrect NaN comparison, NaN cannot be directly compared to itself
 --> lint_example.rs:3:4
  |
3 | if a == f32::NAN {}
  |    ^^^^^^^^^^^^^
  |
  = note: `#[warn(invalid_nan_comparisons)]` on by default
help: use `f32::is_nan()` or `f64::is_nan()` instead
  |
3 - if a == f32::NAN {}
3 + if a.is_nan() {}
  |

```

### Explanation

NaN does not compare meaningfully to anything – not
even itself – so those comparisons are always false.

## invalid-value

The `invalid_value` lint detects creating a value that is not valid,
such as a null reference.

### Example

```rust,no_run
# #![allow(unused)]
unsafe {
    let x: &'static i32 = std::mem::zeroed();
}
```

This will produce:

```text
warning: the type `&i32` does not permit zero-initialization
 --> lint_example.rs:4:27
  |
4 |     let x: &'static i32 = std::mem::zeroed();
  |                           ^^^^^^^^^^^^^^^^^^
  |                           |
  |                           this code causes undefined behavior when executed
  |                           help: use `MaybeUninit<T>` instead, and only call `assume_init` after initialization is done
  |
  = note: references must be non-null
  = note: `#[warn(invalid_value)]` on by default

```

### Explanation

In some situations the compiler can detect that the code is creating
an invalid value, which should be avoided.

In particular, this lint will check for improper use of
[`mem::zeroed`], [`mem::uninitialized`], [`mem::transmute`], and
[`MaybeUninit::assume_init`] that can cause [undefined behavior]. The
lint should provide extra information to indicate what the problem is
and a possible solution.

[`mem::zeroed`]: https://doc.rust-lang.org/std/mem/fn.zeroed.html
[`mem::uninitialized`]: https://doc.rust-lang.org/std/mem/fn.uninitialized.html
[`mem::transmute`]: https://doc.rust-lang.org/std/mem/fn.transmute.html
[`MaybeUninit::assume_init`]: https://doc.rust-lang.org/std/mem/union.MaybeUninit.html#method.assume_init
[undefined behavior]: https://doc.rust-lang.org/reference/behavior-considered-undefined.html

## irrefutable-let-patterns

The `irrefutable_let_patterns` lint detects [irrefutable patterns]
in [`if let`]s, [`while let`]s, and `if let` guards.

### Example

```rust
if let _ = 123 {
    println!("always runs!");
}
```

This will produce:

```text
warning: irrefutable `if let` pattern
 --> lint_example.rs:2:4
  |
2 | if let _ = 123 {
  |    ^^^^^^^^^^^
  |
  = note: this pattern will always match, so the `if let` is useless
  = help: consider replacing the `if let` with a `let`
  = note: `#[warn(irrefutable_let_patterns)]` on by default

```

### Explanation

There usually isn't a reason to have an irrefutable pattern in an
`if let` or `while let` statement, because the pattern will always match
successfully. A [`let`] or [`loop`] statement will suffice. However,
when generating code with a macro, forbidding irrefutable patterns
would require awkward workarounds in situations where the macro
doesn't know if the pattern is refutable or not. This lint allows
macros to accept this form, while alerting for a possibly incorrect
use in normal code.

See [RFC 2086] for more details.

[irrefutable patterns]: https://doc.rust-lang.org/reference/patterns.html#refutability
[`if let`]: https://doc.rust-lang.org/reference/expressions/if-expr.html#if-let-expressions
[`while let`]: https://doc.rust-lang.org/reference/expressions/loop-expr.html#predicate-pattern-loops
[`let`]: https://doc.rust-lang.org/reference/statements.html#let-statements
[`loop`]: https://doc.rust-lang.org/reference/expressions/loop-expr.html#infinite-loops
[RFC 2086]: https://github.com/rust-lang/rfcs/blob/master/text/2086-allow-if-let-irrefutables.md

## large-assignments

The `large_assignments` lint detects when objects of large
types are being moved around.

### Example

```rust,ignore (can crash on some platforms)
let x = [0; 50000];
let y = x;
```

produces:

```text
warning: moving a large value
  --> $DIR/move-large.rs:1:3
  let y = x;
          - Copied large value here
```

### Explanation

When using a large type in a plain assignment or in a function
argument, idiomatic code can be inefficient.
Ideally appropriate optimizations would resolve this, but such
optimizations are only done in a best-effort manner.
This lint will trigger on all sites of large moves and thus allow the
user to resolve them in code.

## late-bound-lifetime-arguments

The `late_bound_lifetime_arguments` lint detects generic lifetime
arguments in path segments with late bound lifetime parameters.

### Example

```rust
struct S;

impl S {
    fn late(self, _: &u8, _: &u8) {}
}

fn main() {
    S.late::<'static>(&0, &0);
}
```

This will produce:

```text
warning: cannot specify lifetime arguments explicitly if late bound lifetime parameters are present
 --> lint_example.rs:8:14
  |
4 |     fn late(self, _: &u8, _: &u8) {}
  |                      - the late bound lifetime parameter is introduced here
...
8 |     S.late::<'static>(&0, &0);
  |              ^^^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #42868 <https://github.com/rust-lang/rust/issues/42868>
  = note: `#[warn(late_bound_lifetime_arguments)]` on by default

```

### Explanation

It is not clear how to provide arguments for early-bound lifetime
parameters if they are intermixed with late-bound parameters in the
same list. For now, providing any explicit arguments will trigger this
lint if late-bound parameters are present, so in the future a solution
can be adopted without hitting backward compatibility issues. This is
a [future-incompatible] lint to transition this to a hard error in the
future. See [issue #42868] for more details, along with a description
of the difference between early and late-bound parameters.

[issue #42868]: https://github.com/rust-lang/rust/issues/42868
[future-incompatible]: ../index.md#future-incompatible-lints

## legacy-derive-helpers

The `legacy_derive_helpers` lint detects derive helper attributes
that are used before they are introduced.

### Example

```rust,ignore (needs extern crate)
#[serde(rename_all = "camelCase")]
#[derive(Deserialize)]
struct S { /* fields */ }
```

produces:

```text
warning: derive helper attribute is used before it is introduced
  --> $DIR/legacy-derive-helpers.rs:1:3
   |
 1 | #[serde(rename_all = "camelCase")]
   |   ^^^^^
...
 2 | #[derive(Deserialize)]
   |          ----------- the attribute is introduced here
```

### Explanation

Attributes like this work for historical reasons, but attribute expansion works in
left-to-right order in general, so, to resolve `#[serde]`, compiler has to try to "look
into the future" at not yet expanded part of the item , but such attempts are not always
reliable.

To fix the warning place the helper attribute after its corresponding derive.
```rust,ignore (needs extern crate)
#[derive(Deserialize)]
#[serde(rename_all = "camelCase")]
struct S { /* fields */ }
```

## map-unit-fn

The `map_unit_fn` lint checks for `Iterator::map` receive
a callable that returns `()`.

### Example

```rust
fn foo(items: &mut Vec<u8>) {
    items.sort();
}

fn main() {
    let mut x: Vec<Vec<u8>> = vec![
        vec![0, 2, 1],
        vec![5, 4, 3],
    ];
    x.iter_mut().map(foo);
}
```

This will produce:

```text
warning: `Iterator::map` call that discard the iterator's values
  --> lint_example.rs:10:18
   |
1  | fn foo(items: &mut Vec<u8>) {
   | --------------------------- this function returns `()`, which is likely not what you wanted
...
10 |     x.iter_mut().map(foo);
   |                  ^^^^---^
   |                  |   |
   |                  |   called `Iterator::map` with callable that returns `()`
   |                  after this call to map, the resulting iterator is `impl Iterator<Item = ()>`, which means the only information carried by the iterator is the number of items
   |
   = note: `Iterator::map`, like many of the methods on `Iterator`, gets executed lazily, meaning that its effects won't be visible until it is iterated
   = note: `#[warn(map_unit_fn)]` on by default
help: you might have meant to use `Iterator::for_each`
   |
10 |     x.iter_mut().for_each(foo);
   |                  ~~~~~~~~

```

### Explanation

Mapping to `()` is almost always a mistake.

## mixed-script-confusables

The `mixed_script_confusables` lint detects visually confusable
characters in identifiers between different [scripts].

[scripts]: https://en.wikipedia.org/wiki/Script_(Unicode)

### Example

```rust
// The Japanese katakana character エ can be confused with the Han character 工.
const エ: &'static str = "アイウ";
```

This will produce:

```text
warning: the usage of Script Group `Japanese, Katakana` in this crate consists solely of mixed script confusables
 --> lint_example.rs:3:7
  |
3 | const エ: &'static str = "アイウ";
  |       ^^
  |
  = note: the usage includes 'エ' (U+30A8)
  = note: please recheck to make sure their usages are indeed what you want
  = note: `#[warn(mixed_script_confusables)]` on by default

```

### Explanation

This lint warns when characters between different scripts may appear
visually similar, which can cause confusion.

If the crate contains other identifiers in the same script that have
non-confusable characters, then this lint will *not* be issued. For
example, if the example given above has another identifier with
katakana characters (such as `let カタカナ = 123;`), then this indicates
that you are intentionally using katakana, and it will not warn about
it.

Note that the set of confusable characters may change over time.
Beware that if you "forbid" this lint that existing code may fail in
the future.

## named-arguments-used-positionally

The `named_arguments_used_positionally` lint detects cases where named arguments are only
used positionally in format strings. This usage is valid but potentially very confusing.

### Example

```rust,compile_fail
#![deny(named_arguments_used_positionally)]
fn main() {
    let _x = 5;
    println!("{}", _x = 1); // Prints 1, will trigger lint

    println!("{}", _x); // Prints 5, no lint emitted
    println!("{_x}", _x = _x); // Prints 5, no lint emitted
}
```

This will produce:

```text
error: named argument `_x` is not used by name
 --> lint_example.rs:4:20
  |
4 |     println!("{}", _x = 1); // Prints 1, will trigger lint
  |               --   ^^ this named argument is referred to by position in formatting string
  |               |
  |               this formatting argument uses named argument `_x` by position
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(named_arguments_used_positionally)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
help: use the named argument by name to avoid ambiguity
  |
4 |     println!("{_x}", _x = 1); // Prints 1, will trigger lint
  |                ++

```

### Explanation

Rust formatting strings can refer to named arguments by their position, but this usage is
potentially confusing. In particular, readers can incorrectly assume that the declaration
of named arguments is an assignment (which would produce the unit type).
For backwards compatibility, this is not a hard error.

## no-mangle-generic-items

The `no_mangle_generic_items` lint detects generic items that must be
mangled.

### Example

```rust
#[no_mangle]
fn foo<T>(t: T) {

}
```

This will produce:

```text
warning: functions generic over types or consts must be mangled
 --> lint_example.rs:3:1
  |
2 |   #[no_mangle]
  |   ------------ help: remove this attribute
3 | / fn foo<T>(t: T) {
4 | |
5 | | }
  | |_^
  |
  = note: `#[warn(no_mangle_generic_items)]` on by default

```

### Explanation

A function with generics must have its symbol mangled to accommodate
the generic parameter. The [`no_mangle` attribute] has no effect in
this situation, and should be removed.

[`no_mangle` attribute]: https://doc.rust-lang.org/reference/abi.html#the-no_mangle-attribute

## non-camel-case-types

The `non_camel_case_types` lint detects types, variants, traits and
type parameters that don't have camel case names.

### Example

```rust
struct my_struct;
```

This will produce:

```text
warning: type `my_struct` should have an upper camel case name
 --> lint_example.rs:2:8
  |
2 | struct my_struct;
  |        ^^^^^^^^^ help: convert the identifier to upper camel case: `MyStruct`
  |
  = note: `#[warn(non_camel_case_types)]` on by default

```

### Explanation

The preferred style for these identifiers is to use "camel case", such
as `MyStruct`, where the first letter should not be lowercase, and
should not use underscores between letters. Underscores are allowed at
the beginning and end of the identifier, as well as between
non-letters (such as `X86_64`).

## non-fmt-panics

The `non_fmt_panics` lint detects `panic!(..)` invocations where the first
argument is not a formatting string.

### Example

```rust,no_run,edition2018
panic!("{}");
panic!(123);
```

This will produce:

```text
warning: panic message contains an unused formatting placeholder
 --> lint_example.rs:2:9
  |
2 | panic!("{}");
  |         ^^
  |
  = note: this message is not used as a format string when given without arguments, but will be in Rust 2021
  = note: `#[warn(non_fmt_panics)]` on by default
help: add the missing argument
  |
2 | panic!("{}", ...);
  |            +++++
help: or add a "{}" format string to use the message literally
  |
2 | panic!("{}", "{}");
  |        +++++


warning: panic message is not a string literal
 --> lint_example.rs:3:8
  |
3 | panic!(123);
  |        ^^^
  |
  = note: this usage of `panic!()` is deprecated; it will be a hard error in Rust 2021
  = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/panic-macro-consistency.html>
help: add a "{}" format string to `Display` the message
  |
3 | panic!("{}", 123);
  |        +++++
help: or use std::panic::panic_any instead
  |
3 | std::panic::panic_any(123);
  | ~~~~~~~~~~~~~~~~~~~~~

```

### Explanation

In Rust 2018 and earlier, `panic!(x)` directly uses `x` as the message.
That means that `panic!("{}")` panics with the message `"{}"` instead
of using it as a formatting string, and `panic!(123)` will panic with
an `i32` as message.

Rust 2021 always interprets the first argument as format string.

## non-shorthand-field-patterns

The `non_shorthand_field_patterns` lint detects using `Struct { x: x }`
instead of `Struct { x }` in a pattern.

### Example

```rust
struct Point {
    x: i32,
    y: i32,
}


fn main() {
    let p = Point {
        x: 5,
        y: 5,
    };

    match p {
        Point { x: x, y: y } => (),
    }
}
```

This will produce:

```text
warning: the `x:` in this pattern is redundant
  --> lint_example.rs:14:17
   |
14 |         Point { x: x, y: y } => (),
   |                 ^^^^ help: use shorthand field pattern: `x`
   |
   = note: `#[warn(non_shorthand_field_patterns)]` on by default


warning: the `y:` in this pattern is redundant
  --> lint_example.rs:14:23
   |
14 |         Point { x: x, y: y } => (),
   |                       ^^^^ help: use shorthand field pattern: `y`

```

### Explanation

The preferred style is to avoid the repetition of specifying both the
field name and the binding name if both identifiers are the same.

## non-snake-case

The `non_snake_case` lint detects variables, methods, functions,
lifetime parameters and modules that don't have snake case names.

### Example

```rust
let MY_VALUE = 5;
```

This will produce:

```text
warning: variable `MY_VALUE` should have a snake case name
 --> lint_example.rs:2:5
  |
2 | let MY_VALUE = 5;
  |     ^^^^^^^^ help: convert the identifier to snake case: `my_value`
  |
  = note: `#[warn(non_snake_case)]` on by default

```

### Explanation

The preferred style for these identifiers is to use "snake case",
where all the characters are in lowercase, with words separated with a
single underscore, such as `my_value`.

## non-upper-case-globals

The `non_upper_case_globals` lint detects static items that don't have
uppercase identifiers.

### Example

```rust
static max_points: i32 = 5;
```

This will produce:

```text
warning: static variable `max_points` should have an upper case name
 --> lint_example.rs:2:8
  |
2 | static max_points: i32 = 5;
  |        ^^^^^^^^^^ help: convert the identifier to upper case: `MAX_POINTS`
  |
  = note: `#[warn(non_upper_case_globals)]` on by default

```

### Explanation

The preferred style is for static item names to use all uppercase
letters such as `MAX_POINTS`.

## nontrivial-structural-match

The `nontrivial_structural_match` lint detects constants that are used in patterns,
whose type is not structural-match and whose initializer body actually uses values
that are not structural-match. So `Option<NotStructuralMatch>` is ok if the constant
is just `None`.

### Example

```rust,compile_fail
#![deny(nontrivial_structural_match)]

#[derive(Copy, Clone, Debug)]
struct NoDerive(u32);
impl PartialEq for NoDerive { fn eq(&self, _: &Self) -> bool { false } }
impl Eq for NoDerive { }
fn main() {
    const INDEX: Option<NoDerive> = [None, Some(NoDerive(10))][0];
    match None { Some(_) => panic!("whoops"), INDEX => dbg!(INDEX), };
}
```

This will produce:

```text
error: to use a constant of type `NoDerive` in a pattern, the constant's initializer must be trivial or `NoDerive` must be annotated with `#[derive(PartialEq, Eq)]`
 --> lint_example.rs:9:47
  |
9 |     match None { Some(_) => panic!("whoops"), INDEX => dbg!(INDEX), };
  |                                               ^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #73448 <https://github.com/rust-lang/rust/issues/73448>
  = note: the traits must be derived, manual `impl`s are not sufficient
  = note: see https://doc.rust-lang.org/stable/std/marker/trait.StructuralEq.html for details
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(nontrivial_structural_match)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Previous versions of Rust accepted constants in patterns, even if those constants' types
did not have `PartialEq` derived. Thus the compiler falls back to runtime execution of
`PartialEq`, which can report that two constants are not equal even if they are
bit-equivalent.

## noop-method-call

The `noop_method_call` lint detects specific calls to noop methods
such as a calling `<&T as Clone>::clone` where `T: !Clone`.

### Example

```rust
# #![allow(unused)]
struct Foo;
let foo = &Foo;
let clone: &Foo = foo.clone();
```

This will produce:

```text
warning: call to `.clone()` on a reference in this situation does nothing
 --> lint_example.rs:5:22
  |
5 | let clone: &Foo = foo.clone();
  |                      ^^^^^^^^ help: remove this redundant call
  |
  = note: the type `Foo` does not implement `Clone`, so calling `clone` on `&Foo` copies the reference, which does not do anything and can be removed
  = note: `#[warn(noop_method_call)]` on by default

```

### Explanation

Some method calls are noops meaning that they do nothing. Usually such methods
are the result of blanket implementations that happen to create some method invocations
that end up not doing anything. For instance, `Clone` is implemented on all `&T`, but
calling `clone` on a `&T` where `T` does not implement clone, actually doesn't do anything
as references are copy. This lint detects these calls and warns the user about them.

## opaque-hidden-inferred-bound

The `opaque_hidden_inferred_bound` lint detects cases in which nested
`impl Trait` in associated type bounds are not written generally enough
to satisfy the bounds of the associated type.

### Explanation

This functionality was removed in #97346, but then rolled back in #99860
because it caused regressions.

We plan on reintroducing this as a hard error, but in the mean time,
this lint serves to warn and suggest fixes for any use-cases which rely
on this behavior.

### Example

```rust
#![feature(type_alias_impl_trait)]

trait Duh {}

impl Duh for i32 {}

trait Trait {
    type Assoc: Duh;
}

impl<F: Duh> Trait for F {
    type Assoc = F;
}

type Tait = impl Sized;

fn test() -> impl Trait<Assoc = Tait> {
    42
}
```

This will produce:

```text
warning: opaque type `impl Trait<Assoc = Tait>` does not satisfy its associated type bounds
  --> lint_example.rs:18:25
   |
9  |     type Assoc: Duh;
   |                 --- this associated type bound is unsatisfied for `Tait`
...
18 | fn test() -> impl Trait<Assoc = Tait> {
   |                         ^^^^^^^^^^^^
   |
   = note: `#[warn(opaque_hidden_inferred_bound)]` on by default

```

In this example, `test` declares that the associated type `Assoc` for
`impl Trait` is `impl Sized`, which does not satisfy the bound `Duh`
on the associated type.

Although the hidden type, `i32` does satisfy this bound, we do not
consider the return type to be well-formed with this lint. It can be
fixed by changing `Tait = impl Sized` into `Tait = impl Sized + Duh`.

## overlapping-range-endpoints

The `overlapping_range_endpoints` lint detects `match` arms that have [range patterns] that
overlap on their endpoints.

[range patterns]: https://doc.rust-lang.org/nightly/reference/patterns.html#range-patterns

### Example

```rust
let x = 123u8;
match x {
    0..=100 => { println!("small"); }
    100..=255 => { println!("large"); }
}
```

This will produce:

```text
warning: multiple patterns overlap on their endpoints
 --> lint_example.rs:5:5
  |
4 |     0..=100 => { println!("small"); }
  |     ------- this range overlaps on `100_u8`...
5 |     100..=255 => { println!("large"); }
  |     ^^^^^^^^^ ... with this range
  |
  = note: you likely meant to write mutually exclusive ranges
  = note: `#[warn(overlapping_range_endpoints)]` on by default

```

### Explanation

It is likely a mistake to have range patterns in a match expression that overlap in this
way. Check that the beginning and end values are what you expect, and keep in mind that
with `..=` the left and right bounds are inclusive.

## path-statements

The `path_statements` lint detects path statements with no effect.

### Example

```rust
let x = 42;

x;
```

This will produce:

```text
warning: path statement with no effect
 --> lint_example.rs:4:1
  |
4 | x;
  | ^^
  |
  = note: `#[warn(path_statements)]` on by default

```

### Explanation

It is usually a mistake to have a statement that has no effect.

## private-bounds

The `private_bounds` lint detects types in a secondary interface of an item,
that are more private than the item itself. Secondary interface of an item consists of
bounds on generic parameters and where clauses, including supertraits for trait items.

### Example

```rust,compile_fail
# #![allow(unused)]
#![deny(private_bounds)]

struct PrivTy;
pub struct S
    where PrivTy:
{}
# fn main() {}
```

This will produce:

```text
error: type `PrivTy` is more private than the item `S`
 --> lint_example.rs:5:1
  |
5 | pub struct S
  | ^^^^^^^^^^^^ struct `S` is reachable at visibility `pub`
  |
note: but type `PrivTy` is only usable at visibility `pub(crate)`
 --> lint_example.rs:4:1
  |
4 | struct PrivTy;
  | ^^^^^^^^^^^^^
note: the lint level is defined here
 --> lint_example.rs:2:9
  |
2 | #![deny(private_bounds)]
  |         ^^^^^^^^^^^^^^

```

### Explanation

Having private types or traits in item bounds makes it less clear what interface
the item actually provides.

## private-interfaces

The `private_interfaces` lint detects types in a primary interface of an item,
that are more private than the item itself. Primary interface of an item is all
its interface except for bounds on generic parameters and where clauses.

### Example

```rust,compile_fail
# #![allow(unused)]
#![deny(private_interfaces)]
struct SemiPriv;

mod m1 {
    struct Priv;
    impl crate::SemiPriv {
        pub fn f(_: Priv) {}
    }
}

# fn main() {}
```

This will produce:

```text
error: type `Priv` is more private than the item `m1::<impl SemiPriv>::f`
 --> lint_example.rs:8:9
  |
8 |         pub fn f(_: Priv) {}
  |         ^^^^^^^^^^^^^^^^^ associated function `m1::<impl SemiPriv>::f` is reachable at visibility `pub(crate)`
  |
note: but type `Priv` is only usable at visibility `pub(self)`
 --> lint_example.rs:6:5
  |
6 |     struct Priv;
  |     ^^^^^^^^^^^
note: the lint level is defined here
 --> lint_example.rs:2:9
  |
2 | #![deny(private_interfaces)]
  |         ^^^^^^^^^^^^^^^^^^

```

### Explanation

Having something private in primary interface guarantees that
the item will be unusable from outer modules due to type privacy.

## redundant-semicolons

The `redundant_semicolons` lint detects unnecessary trailing
semicolons.

### Example

```rust
let _ = 123;;
```

This will produce:

```text
warning: unnecessary trailing semicolon
 --> lint_example.rs:2:13
  |
2 | let _ = 123;;
  |             ^ help: remove this semicolon
  |
  = note: `#[warn(redundant_semicolons)]` on by default

```

### Explanation

Extra semicolons are not needed, and may be removed to avoid confusion
and visual clutter.

## refining-impl-trait

The `refining_impl_trait` lint detects usages of return-position impl
traits in trait signatures which are refined by implementations.

### Example

```rust,compile_fail
#![deny(refining_impl_trait)]

use std::fmt::Display;

pub trait AsDisplay {
    fn as_display(&self) -> impl Display;
}

impl<'s> AsDisplay for &'s str {
    fn as_display(&self) -> Self {
        *self
    }
}

fn main() {
    // users can observe that the return type of
    // `<&str as AsDisplay>::as_display()` is `&str`.
    let x: &str = "".as_display();
}
```

{{produces}}

### Explanation

Return-position impl trait in traits (RPITITs) desugar to associated types,
and callers of methods for types where the implementation is known are
able to observe the types written in the impl signature. This may be
intended behavior, but may also pose a semver hazard for authors of libraries
who do not wish to make stronger guarantees about the types than what is
written in the trait signature.

## renamed-and-removed-lints

The `renamed_and_removed_lints` lint detects lints that have been
renamed or removed.

### Example

```rust
#![deny(raw_pointer_derive)]
```

This will produce:

```text
warning: lint `raw_pointer_derive` has been removed: using derive with raw pointers is ok
 --> lint_example.rs:1:9
  |
1 | #![deny(raw_pointer_derive)]
  |         ^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(renamed_and_removed_lints)]` on by default

```

### Explanation

To fix this, either remove the lint or use the new name. This can help
avoid confusion about lints that are no longer valid, and help
maintain consistency for renamed lints.

## repr-transparent-external-private-fields

The `repr_transparent_external_private_fields` lint
detects types marked `#[repr(transparent)]` that (transitively)
contain an external ZST type marked `#[non_exhaustive]` or containing
private fields

### Example

```rust,ignore (needs external crate)
#![deny(repr_transparent_external_private_fields)]
use foo::NonExhaustiveZst;

#[repr(transparent)]
struct Bar(u32, ([u32; 0], NonExhaustiveZst));
```

This will produce:

```text
error: zero-sized fields in repr(transparent) cannot contain external non-exhaustive types
 --> src/main.rs:5:28
  |
5 | struct Bar(u32, ([u32; 0], NonExhaustiveZst));
  |                            ^^^^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> src/main.rs:1:9
  |
1 | #![deny(repr_transparent_external_private_fields)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #78586 <https://github.com/rust-lang/rust/issues/78586>
  = note: this struct contains `NonExhaustiveZst`, which is marked with `#[non_exhaustive]`, and makes it not a breaking change to become non-zero-sized in the future.
```

### Explanation

Previous, Rust accepted fields that contain external private zero-sized types,
even though it should not be a breaking change to add a non-zero-sized field to
that private type.

This is a [future-incompatible] lint to transition this
to a hard error in the future. See [issue #78586] for more details.

[issue #78586]: https://github.com/rust-lang/rust/issues/78586
[future-incompatible]: ../index.md#future-incompatible-lints

## semicolon-in-expressions-from-macros

The `semicolon_in_expressions_from_macros` lint detects trailing semicolons
in macro bodies when the macro is invoked in expression position.
This was previous accepted, but is being phased out.

### Example

```rust,compile_fail
#![deny(semicolon_in_expressions_from_macros)]
macro_rules! foo {
    () => { true; }
}

fn main() {
    let val = match true {
        true => false,
        _ => foo!()
    };
}
```

This will produce:

```text
error: trailing semicolon in macro used in expression position
 --> lint_example.rs:3:17
  |
3 |     () => { true; }
  |                 ^
...
9 |         _ => foo!()
  |              ------ in this macro invocation
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #79813 <https://github.com/rust-lang/rust/issues/79813>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(semicolon_in_expressions_from_macros)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  = note: this error originates in the macro `foo` (in Nightly builds, run with -Z macro-backtrace for more info)

```

### Explanation

Previous, Rust ignored trailing semicolon in a macro
body when a macro was invoked in expression position.
However, this makes the treatment of semicolons in the language
inconsistent, and could lead to unexpected runtime behavior
in some circumstances (e.g. if the macro author expects
a value to be dropped).

This is a [future-incompatible] lint to transition this
to a hard error in the future. See [issue #79813] for more details.

[issue #79813]: https://github.com/rust-lang/rust/issues/79813
[future-incompatible]: ../index.md#future-incompatible-lints

## special-module-name

The `special_module_name` lint detects module
declarations for files that have a special meaning.

### Example

```rust,compile_fail
mod lib;

fn main() {
    lib::run();
}
```

This will produce:

```text
warning: found module declaration for lib.rs
 --> lint_example.rs:1:1
  |
1 | mod lib;
  | ^^^^^^^^
  |
  = note: lib.rs is the root of this crate's library target
  = help: to refer to it from other targets, use the library's name as the path
  = note: `#[warn(special_module_name)]` on by default

```

### Explanation

Cargo recognizes `lib.rs` and `main.rs` as the root of a
library or binary crate, so declaring them as modules
will lead to miscompilation of the crate unless configured
explicitly.

To access a library from a binary target within the same crate,
use `your_crate_name::` as the path instead of `lib::`:

```rust,compile_fail
// bar/src/lib.rs
fn run() {
    // ...
}

// bar/src/main.rs
fn main() {
    bar::run();
}
```

Binary targets cannot be used as libraries and so declaring
one as a module is not allowed.

## stable-features

The `stable_features` lint detects a [`feature` attribute] that
has since been made stable.

[`feature` attribute]: https://doc.rust-lang.org/nightly/unstable-book/

### Example

```rust
#![feature(test_accepted_feature)]
fn main() {}
```

This will produce:

```text
warning: the feature `test_accepted_feature` has been stable since 1.0.0 and no longer requires an attribute to enable
 --> lint_example.rs:1:12
  |
1 | #![feature(test_accepted_feature)]
  |            ^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(stable_features)]` on by default

```

### Explanation

When a feature is stabilized, it is no longer necessary to include a
`#![feature]` attribute for it. To fix, simply remove the
`#![feature]` attribute.

## suspicious-auto-trait-impls

The `suspicious_auto_trait_impls` lint checks for potentially incorrect
implementations of auto traits.

### Example

```rust
struct Foo<T>(T);

unsafe impl<T> Send for Foo<*const T> {}
```

This will produce:

```text
warning: cross-crate traits with a default impl, like `Send`, should not be specialized
 --> lint_example.rs:4:1
  |
4 | unsafe impl<T> Send for Foo<*const T> {}
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = warning: this will change its meaning in a future release!
  = note: for more information, see issue #93367 <https://github.com/rust-lang/rust/issues/93367>
  = note: `*const T` is not a generic parameter
note: try using the same sequence of generic parameters as the struct definition
 --> lint_example.rs:2:1
  |
2 | struct Foo<T>(T);
  | ^^^^^^^^^^^^^
  = note: `#[warn(suspicious_auto_trait_impls)]` on by default

```

### Explanation

A type can implement auto traits, e.g. `Send`, `Sync` and `Unpin`,
in two different ways: either by writing an explicit impl or if
all fields of the type implement that auto trait.

The compiler disables the automatic implementation if an explicit one
exists for given type constructor. The exact rules governing this
were previously unsound, quite subtle, and have been recently modified.
This change caused the automatic implementation to be disabled in more
cases, potentially breaking some code.

## suspicious-double-ref-op

The `suspicious_double_ref_op` lint checks for usage of `.clone()`/`.borrow()`/`.deref()`
on an `&&T` when `T: !Deref/Borrow/Clone`, which means the call will return the inner `&T`,
instead of performing the operation on the underlying `T` and can be confusing.

### Example

```rust
# #![allow(unused)]
struct Foo;
let foo = &&Foo;
let clone: &Foo = foo.clone();
```

This will produce:

```text
warning: using `.clone()` on a double reference, which returns `&Foo` instead of cloning the inner type
 --> lint_example.rs:5:22
  |
5 | let clone: &Foo = foo.clone();
  |                      ^^^^^^^^
  |
  = note: `#[warn(suspicious_double_ref_op)]` on by default

```

### Explanation

Since `Foo` doesn't implement `Clone`, running `.clone()` only dereferences the double
reference, instead of cloning the inner type which should be what was intended.

## temporary-cstring-as-ptr

The `temporary_cstring_as_ptr` lint detects getting the inner pointer of
a temporary `CString`.

### Example

```rust
# #![allow(unused)]
# use std::ffi::CString;
let c_str = CString::new("foo").unwrap().as_ptr();
```

This will produce:

```text
warning: getting the inner pointer of a temporary `CString`
 --> lint_example.rs:4:42
  |
4 | let c_str = CString::new("foo").unwrap().as_ptr();
  |             ---------------------------- ^^^^^^ this pointer will be invalid
  |             |
  |             this `CString` is deallocated at the end of the statement, bind it to a variable to extend its lifetime
  |
  = note: pointers do not have a lifetime; when calling `as_ptr` the `CString` will be deallocated at the end of the statement because nothing is referencing it as far as the type system is concerned
  = help: for more information, see https://doc.rust-lang.org/reference/destructors.html
  = note: `#[warn(temporary_cstring_as_ptr)]` on by default

```

### Explanation

The inner pointer of a `CString` lives only as long as the `CString` it
points to. Getting the inner pointer of a *temporary* `CString` allows the `CString`
to be dropped at the end of the statement, as it is not being referenced as far as the typesystem
is concerned. This means outside of the statement the pointer will point to freed memory, which
causes undefined behavior if the pointer is later dereferenced.

## trivial-bounds

The `trivial_bounds` lint detects trait bounds that don't depend on
any type parameters.

### Example

```rust
#![feature(trivial_bounds)]
pub struct A where i32: Copy;
```

This will produce:

```text
warning: trait bound i32: Copy does not depend on any type or lifetime parameters
 --> lint_example.rs:3:25
  |
3 | pub struct A where i32: Copy;
  |                         ^^^^
  |
  = note: `#[warn(trivial_bounds)]` on by default

```

### Explanation

Usually you would not write a trait bound that you know is always
true, or never true. However, when using macros, the macro may not
know whether or not the constraint would hold or not at the time when
generating the code. Currently, the compiler does not alert you if the
constraint is always true, and generates an error if it is never true.
The `trivial_bounds` feature changes this to be a warning in both
cases, giving macros more freedom and flexibility to generate code,
while still providing a signal when writing non-macro code that
something is amiss.

See [RFC 2056] for more details. This feature is currently only
available on the nightly channel, see [tracking issue #48214].

[RFC 2056]: https://github.com/rust-lang/rfcs/blob/master/text/2056-allow-trivial-where-clause-constraints.md
[tracking issue #48214]: https://github.com/rust-lang/rust/issues/48214

## type-alias-bounds

The `type_alias_bounds` lint detects bounds in type aliases.

### Example

```rust
type SendVec<T: Send> = Vec<T>;
```

This will produce:

```text
warning: bounds on generic parameters are not enforced in type aliases
 --> lint_example.rs:2:17
  |
2 | type SendVec<T: Send> = Vec<T>;
  |                 ^^^^
  |
  = note: `#[warn(type_alias_bounds)]` on by default
help: the bound will not be checked when the type alias is used, and should be removed
  |
2 - type SendVec<T: Send> = Vec<T>;
2 + type SendVec<T> = Vec<T>;
  |

```

### Explanation

The trait bounds in a type alias are currently ignored, and should not
be included to avoid confusion. This was previously allowed
unintentionally; this may become a hard error in the future.

## tyvar-behind-raw-pointer

The `tyvar_behind_raw_pointer` lint detects raw pointer to an
inference variable.

### Example

```rust,edition2015
// edition 2015
let data = std::ptr::null();
let _ = &data as *const *const ();

if data.is_null() {}
```

This will produce:

```text
warning: type annotations needed
 --> lint_example.rs:6:9
  |
6 | if data.is_null() {}
  |         ^^^^^^^
  |
  = warning: this is accepted in the current edition (Rust 2015) but is a hard error in Rust 2018!
  = note: for more information, see issue #46906 <https://github.com/rust-lang/rust/issues/46906>
  = note: `#[warn(tyvar_behind_raw_pointer)]` on by default

```

### Explanation

This kind of inference was previously allowed, but with the future
arrival of [arbitrary self types], this can introduce ambiguity. To
resolve this, use an explicit type instead of relying on type
inference.

This is a [future-incompatible] lint to transition this to a hard
error in the 2018 edition. See [issue #46906] for more details. This
is currently a hard-error on the 2018 edition, and is "warn" by
default in the 2015 edition.

[arbitrary self types]: https://github.com/rust-lang/rust/issues/44874
[issue #46906]: https://github.com/rust-lang/rust/issues/46906
[future-incompatible]: ../index.md#future-incompatible-lints

## uncommon-codepoints

The `uncommon_codepoints` lint detects uncommon Unicode codepoints in
identifiers.

### Example

```rust
# #![allow(unused)]
const µ: f64 = 0.000001;
```

This will produce:

```text
warning: identifier contains uncommon Unicode codepoints
 --> lint_example.rs:3:7
  |
3 | const µ: f64 = 0.000001;
  |       ^
  |
  = note: `#[warn(uncommon_codepoints)]` on by default

```

### Explanation

This lint warns about using characters which are not commonly used, and may
cause visual confusion.

This lint is triggered by identifiers that contain a codepoint that is
not part of the set of "Allowed" codepoints as described by [Unicode®
Technical Standard #39 Unicode Security Mechanisms Section 3.1 General
Security Profile for Identifiers][TR39Allowed].

Note that the set of uncommon codepoints may change over time. Beware
that if you "forbid" this lint that existing code may fail in the
future.

[TR39Allowed]: https://www.unicode.org/reports/tr39/#General_Security_Profile

## unconditional-recursion

The `unconditional_recursion` lint detects functions that cannot
return without calling themselves.

### Example

```rust
fn foo() {
    foo();
}
```

This will produce:

```text
warning: function cannot return without recursing
 --> lint_example.rs:2:1
  |
2 | fn foo() {
  | ^^^^^^^^ cannot return without recursing
3 |     foo();
  |     ----- recursive call site
  |
  = help: a `loop` may express intention better if this is on purpose
  = note: `#[warn(unconditional_recursion)]` on by default

```

### Explanation

It is usually a mistake to have a recursive call that does not have
some condition to cause it to terminate. If you really intend to have
an infinite loop, using a `loop` expression is recommended.

## undefined-naked-function-abi

The `undefined_naked_function_abi` lint detects naked function definitions that
either do not specify an ABI or specify the Rust ABI.

### Example

```rust
#![feature(asm_experimental_arch, naked_functions)]

use std::arch::asm;

#[naked]
pub fn default_abi() -> u32 {
    unsafe { asm!("", options(noreturn)); }
}

#[naked]
pub extern "Rust" fn rust_abi() -> u32 {
    unsafe { asm!("", options(noreturn)); }
}
```

This will produce:

```text
warning: Rust ABI is unsupported in naked functions
 --> lint_example.rs:7:1
  |
7 | pub fn default_abi() -> u32 {
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(undefined_naked_function_abi)]` on by default


warning: Rust ABI is unsupported in naked functions
  --> lint_example.rs:12:1
   |
12 | pub extern "Rust" fn rust_abi() -> u32 {
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

The Rust ABI is currently undefined. Therefore, naked functions should
specify a non-Rust ABI.

## unexpected-cfgs

The `unexpected_cfgs` lint detects unexpected conditional compilation conditions.

### Example

```text
rustc --check-cfg 'names()'
```

```rust,ignore (needs command line option)
#[cfg(widnows)]
fn foo() {}
```

This will produce:

```text
warning: unknown condition name used
 --> lint_example.rs:1:7
  |
1 | #[cfg(widnows)]
  |       ^^^^^^^
  |
  = note: `#[warn(unexpected_cfgs)]` on by default
```

### Explanation

This lint is only active when a `--check-cfg='names(...)'` option has been passed
to the compiler and triggers whenever an unknown condition name or value is used.
The known condition include names or values passed in `--check-cfg`, `--cfg`, and some
well-knows names and values built into the compiler.

## unfulfilled-lint-expectations

The `unfulfilled_lint_expectations` lint detects lint trigger expectations
that have not been fulfilled.

### Example

```rust
#![feature(lint_reasons)]

#[expect(unused_variables)]
let x = 10;
println!("{}", x);
```

This will produce:

```text
warning: this lint expectation is unfulfilled
 --> lint_example.rs:4:10
  |
4 | #[expect(unused_variables)]
  |          ^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(unfulfilled_lint_expectations)]` on by default

```

### Explanation

It was expected that the marked code would emit a lint. This expectation
has not been fulfilled.

The `expect` attribute can be removed if this is intended behavior otherwise
it should be investigated why the expected lint is no longer issued.

In rare cases, the expectation might be emitted at a different location than
shown in the shown code snippet. In most cases, the `#[expect]` attribute
works when added to the outer scope. A few lints can only be expected
on a crate level.

Part of RFC 2383. The progress is being tracked in [#54503]

[#54503]: https://github.com/rust-lang/rust/issues/54503

## ungated-async-fn-track-caller

The `ungated_async_fn_track_caller` lint warns when the
`#[track_caller]` attribute is used on an async function
without enabling the corresponding unstable feature flag.

### Example

```rust
#[track_caller]
async fn foo() {}
```

This will produce:

```text
warning: `#[track_caller]` on async functions is a no-op
 --> lint_example.rs:2:1
  |
2 | #[track_caller]
  | ^^^^^^^^^^^^^^^
3 | async fn foo() {}
  | ----------------- this function will not propagate the caller location
  |
  = note: see issue #110011 <https://github.com/rust-lang/rust/issues/110011> for more information
  = help: add `#![feature(async_fn_track_caller)]` to the crate attributes to enable
  = note: `#[warn(ungated_async_fn_track_caller)]` on by default

```

### Explanation

The attribute must be used in conjunction with the
[`async_fn_track_caller` feature flag]. Otherwise, the `#[track_caller]`
annotation will function as a no-op.

[`async_fn_track_caller` feature flag]: https://doc.rust-lang.org/beta/unstable-book/language-features/async-fn-track-caller.html

## uninhabited-static

The `uninhabited_static` lint detects uninhabited statics.

### Example

```rust
enum Void {}
extern {
    static EXTERN: Void;
}
```

This will produce:

```text
warning: static of uninhabited type
 --> lint_example.rs:4:5
  |
4 |     static EXTERN: Void;
  |     ^^^^^^^^^^^^^^^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #74840 <https://github.com/rust-lang/rust/issues/74840>
  = note: uninhabited statics cannot be initialized, and any access would be an immediate error
  = note: `#[warn(uninhabited_static)]` on by default

```

### Explanation

Statics with an uninhabited type can never be initialized, so they are impossible to define.
However, this can be side-stepped with an `extern static`, leading to problems later in the
compiler which assumes that there are no initialized uninhabited places (such as locals or
statics). This was accidentally allowed, but is being phased out.

## unknown-lints

The `unknown_lints` lint detects unrecognized lint attributes.

### Example

```rust
#![allow(not_a_real_lint)]
```

This will produce:

```text
warning: unknown lint: `not_a_real_lint`
 --> lint_example.rs:1:10
  |
1 | #![allow(not_a_real_lint)]
  |          ^^^^^^^^^^^^^^^
  |
  = note: `#[warn(unknown_lints)]` on by default

```

### Explanation

It is usually a mistake to specify a lint that does not exist. Check
the spelling, and check the lint listing for the correct name. Also
consider if you are using an old version of the compiler, and the lint
is only available in a newer version.

## unknown-or-malformed-diagnostic-attributes

The `unknown_or_malformed_diagnostic_attributes` lint detects unrecognized or otherwise malformed
diagnostic attributes.

### Example

```rust
#![feature(diagnostic_namespace)]
#[diagnostic::does_not_exist]
struct Foo;
```

This will produce:

```text
warning: unknown diagnostic attribute
 --> lint_example.rs:3:15
  |
3 | #[diagnostic::does_not_exist]
  |               ^^^^^^^^^^^^^^
  |
  = note: `#[warn(unknown_or_malformed_diagnostic_attributes)]` on by default

```


### Explanation

It is usually a mistake to specify a diagnostic attribute that does not exist. Check
the spelling, and check the diagnostic attribute listing for the correct name. Also
consider if you are using an old version of the compiler, and the attribute
is only available in a newer version.

## unnameable-test-items

The `unnameable_test_items` lint detects [`#[test]`][test] functions
that are not able to be run by the test harness because they are in a
position where they are not nameable.

[test]: https://doc.rust-lang.org/reference/attributes/testing.html#the-test-attribute

### Example

```rust,test
fn main() {
    #[test]
    fn foo() {
        // This test will not fail because it does not run.
        assert_eq!(1, 2);
    }
}
```

This will produce:

```text
warning: cannot test inner items
 --> lint_example.rs:2:5
  |
2 |     #[test]
  |     ^^^^^^^
  |
  = note: `#[warn(unnameable_test_items)]` on by default
  = note: this warning originates in the attribute macro `test` (in Nightly builds, run with -Z macro-backtrace for more info)

```

### Explanation

In order for the test harness to run a test, the test function must be
located in a position where it can be accessed from the crate root.
This generally means it must be defined in a module, and not anywhere
else such as inside another function. The compiler previously allowed
this without an error, so a lint was added as an alert that a test is
not being used. Whether or not this should be allowed has not yet been
decided, see [RFC 2471] and [issue #36629].

[RFC 2471]: https://github.com/rust-lang/rfcs/pull/2471#issuecomment-397414443
[issue #36629]: https://github.com/rust-lang/rust/issues/36629

## unreachable-code

The `unreachable_code` lint detects unreachable code paths.

### Example

```rust,no_run
panic!("we never go past here!");

let x = 5;
```

This will produce:

```text
warning: unreachable statement
 --> lint_example.rs:4:1
  |
2 | panic!("we never go past here!");
  | -------------------------------- any code following this expression is unreachable
3 |
4 | let x = 5;
  | ^^^^^^^^^^ unreachable statement
  |
  = note: `#[warn(unreachable_code)]` on by default

```

### Explanation

Unreachable code may signal a mistake or unfinished code. If the code
is no longer in use, consider removing it.

## unreachable-patterns

The `unreachable_patterns` lint detects unreachable patterns.

### Example

```rust
let x = 5;
match x {
    y => (),
    5 => (),
}
```

This will produce:

```text
warning: unreachable pattern
 --> lint_example.rs:5:5
  |
4 |     y => (),
  |     - matches any value
5 |     5 => (),
  |     ^ unreachable pattern
  |
  = note: `#[warn(unreachable_patterns)]` on by default

```

### Explanation

This usually indicates a mistake in how the patterns are specified or
ordered. In this example, the `y` pattern will always match, so the
five is impossible to reach. Remember, match arms match in order, you
probably wanted to put the `5` case above the `y` case.

## unstable-name-collisions

The `unstable_name_collisions` lint detects that you have used a name
that the standard library plans to add in the future.

### Example

```rust
trait MyIterator : Iterator {
    // is_sorted is an unstable method that already exists on the Iterator trait
    fn is_sorted(self) -> bool where Self: Sized {true}
}

impl<T: ?Sized> MyIterator for T where T: Iterator { }

let x = vec![1, 2, 3];
let _ = x.iter().is_sorted();
```

This will produce:

```text
warning: a method with this name may be added to the standard library in the future
  --> lint_example.rs:10:18
   |
10 | let _ = x.iter().is_sorted();
   |                  ^^^^^^^^^
   |
   = warning: once this associated item is added to the standard library, the ambiguity may cause an error or change in behavior!
   = note: for more information, see issue #48919 <https://github.com/rust-lang/rust/issues/48919>
   = help: call with fully qualified syntax `MyIterator::is_sorted(...)` to keep using the current method
   = help: add `#![feature(is_sorted)]` to the crate attributes to enable `is_sorted`
   = note: `#[warn(unstable_name_collisions)]` on by default

```

### Explanation

When new methods are added to traits in the standard library, they are
usually added in an "unstable" form which is only available on the
[nightly channel] with a [`feature` attribute]. If there is any
preexisting code which extends a trait to have a method with the same
name, then the names will collide. In the future, when the method is
stabilized, this will cause an error due to the ambiguity. This lint
is an early-warning to let you know that there may be a collision in
the future. This can be avoided by adding type annotations to
disambiguate which trait method you intend to call, such as
`MyIterator::is_sorted(my_iter)` or renaming or removing the method.

[nightly channel]: https://doc.rust-lang.org/book/appendix-07-nightly-rust.html
[`feature` attribute]: https://doc.rust-lang.org/nightly/unstable-book/

## unstable-syntax-pre-expansion

The `unstable_syntax_pre_expansion` lint detects the use of unstable
syntax that is discarded during attribute expansion.

### Example

```rust
#[cfg(FALSE)]
macro foo() {}
```

This will produce:

```text
warning: `macro` is experimental
 --> lint_example.rs:3:1
  |
3 | macro foo() {}
  | ^^^^^^^^^^^^^^
  |
  = note: see issue #39412 <https://github.com/rust-lang/rust/issues/39412> for more information
  = help: add `#![feature(decl_macro)]` to the crate attributes to enable
  = warning: unstable syntax can change at any point in the future, causing a hard error!
  = note: for more information, see issue #65860 <https://github.com/rust-lang/rust/issues/65860>

```

### Explanation

The input to active attributes such as `#[cfg]` or procedural macro
attributes is required to be valid syntax. Previously, the compiler only
gated the use of unstable syntax features after resolving `#[cfg]` gates
and expanding procedural macros.

To avoid relying on unstable syntax, move the use of unstable syntax
into a position where the compiler does not parse the syntax, such as a
functionlike macro.

```rust
# #![deny(unstable_syntax_pre_expansion)]

macro_rules! identity {
   ( $($tokens:tt)* ) => { $($tokens)* }
}

#[cfg(FALSE)]
identity! {
   macro foo() {}
}
```

This is a [future-incompatible] lint to transition this
to a hard error in the future. See [issue #65860] for more details.

[issue #65860]: https://github.com/rust-lang/rust/issues/65860
[future-incompatible]: ../index.md#future-incompatible-lints

## unsupported-calling-conventions

The `unsupported_calling_conventions` lint is output whenever there is a use of the
`stdcall`, `fastcall`, `thiscall`, `vectorcall` calling conventions (or their unwind
variants) on targets that cannot meaningfully be supported for the requested target.

For example `stdcall` does not make much sense for a x86_64 or, more apparently, powerpc
code, because this calling convention was never specified for those targets.

Historically MSVC toolchains have fallen back to the regular C calling convention for
targets other than x86, but Rust doesn't really see a similar need to introduce a similar
hack across many more targets.

### Example

```rust,ignore (needs specific targets)
extern "stdcall" fn stdcall() {}
```

This will produce:

```text
warning: use of calling convention not supported on this target
  --> $DIR/unsupported.rs:39:1
   |
LL | extern "stdcall" fn stdcall() {}
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   |
   = note: `#[warn(unsupported_calling_conventions)]` on by default
   = warning: this was previously accepted by the compiler but is being phased out;
              it will become a hard error in a future release!
   = note: for more information, see issue ...
```

### Explanation

On most of the targets the behaviour of `stdcall` and similar calling conventions is not
defined at all, but was previously accepted due to a bug in the implementation of the
compiler.

## unused-allocation

The `unused_allocation` lint detects unnecessary allocations that can
be eliminated.

### Example

```rust
fn main() {
    let a = Box::new([1, 2, 3]).len();
}
```

This will produce:

```text
warning: unnecessary allocation, use `&` instead
 --> lint_example.rs:2:13
  |
2 |     let a = Box::new([1, 2, 3]).len();
  |             ^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(unused_allocation)]` on by default

```

### Explanation

When a `box` expression is immediately coerced to a reference, then
the allocation is unnecessary, and a reference (using `&` or `&mut`)
should be used instead to avoid the allocation.

## unused-assignments

The `unused_assignments` lint detects assignments that will never be read.

### Example

```rust
let mut x = 5;
x = 6;
```

This will produce:

```text
warning: value assigned to `x` is never read
 --> lint_example.rs:3:1
  |
3 | x = 6;
  | ^
  |
  = help: maybe it is overwritten before being read?
  = note: `#[warn(unused_assignments)]` on by default

```

### Explanation

Unused assignments may signal a mistake or unfinished code. If the
variable is never used after being assigned, then the assignment can
be removed. Variables with an underscore prefix such as `_x` will not
trigger this lint.

## unused-associated-type-bounds

The `unused_associated_type_bounds` lint is emitted when an
associated type bound is added to a trait object, but the associated
type has a `where Self: Sized` bound, and is thus unavailable on the
trait object anyway.

### Example

```rust
trait Foo {
    type Bar where Self: Sized;
}
type Mop = dyn Foo<Bar = ()>;
```

This will produce:

```text
warning: unnecessary associated type bound for not object safe associated type
 --> lint_example.rs:5:20
  |
5 | type Mop = dyn Foo<Bar = ()>;
  |                    ^^^^^^^^ help: remove this bound
  |
  = note: this associated type has a `where Self: Sized` bound. Thus, while the associated type can be specified, it cannot be used in any way, because trait objects are not `Sized`.
  = note: `#[warn(unused_associated_type_bounds)]` on by default

```

### Explanation

Just like methods with `Self: Sized` bounds are unavailable on trait
objects, associated types can be removed from the trait object.

## unused-attributes

The `unused_attributes` lint detects attributes that were not used by
the compiler.

### Example

```rust
#![ignore]
```

This will produce:

```text
warning: `#[ignore]` only has an effect on functions
 --> lint_example.rs:1:1
  |
1 | #![ignore]
  | ^^^^^^^^^^
  |
  = note: `#[warn(unused_attributes)]` on by default

```

### Explanation

Unused [attributes] may indicate the attribute is placed in the wrong
position. Consider removing it, or placing it in the correct position.
Also consider if you intended to use an _inner attribute_ (with a `!`
such as `#![allow(unused)]`) which applies to the item the attribute
is within, or an _outer attribute_ (without a `!` such as
`#[allow(unused)]`) which applies to the item *following* the
attribute.

[attributes]: https://doc.rust-lang.org/reference/attributes.html

## unused-braces

The `unused_braces` lint detects unnecessary braces around an
expression.

### Example

```rust
if { true } {
    // ...
}
```

This will produce:

```text
warning: unnecessary braces around `if` condition
 --> lint_example.rs:2:4
  |
2 | if { true } {
  |    ^^    ^^
  |
  = note: `#[warn(unused_braces)]` on by default
help: remove these braces
  |
2 - if { true } {
2 + if true {
  |

```

### Explanation

The braces are not needed, and should be removed. This is the
preferred style for writing these expressions.

## unused-comparisons

The `unused_comparisons` lint detects comparisons made useless by
limits of the types involved.

### Example

```rust
fn foo(x: u8) {
    x >= 0;
}
```

This will produce:

```text
warning: comparison is useless due to type limits
 --> lint_example.rs:3:5
  |
3 |     x >= 0;
  |     ^^^^^^
  |
  = note: `#[warn(unused_comparisons)]` on by default

```

### Explanation

A useless comparison may indicate a mistake, and should be fixed or
removed.

## unused-doc-comments

The `unused_doc_comments` lint detects doc comments that aren't used
by `rustdoc`.

### Example

```rust
/// docs for x
let x = 12;
```

This will produce:

```text
warning: unused doc comment
 --> lint_example.rs:2:1
  |
2 | /// docs for x
  | ^^^^^^^^^^^^^^
3 | let x = 12;
  | ----------- rustdoc does not generate documentation for statements
  |
  = help: use `//` for a plain comment
  = note: `#[warn(unused_doc_comments)]` on by default

```

### Explanation

`rustdoc` does not use doc comments in all positions, and so the doc
comment will be ignored. Try changing it to a normal comment with `//`
to avoid the warning.

## unused-features

The `unused_features` lint detects unused or unknown features found in
crate-level [`feature` attributes].

[`feature` attributes]: https://doc.rust-lang.org/nightly/unstable-book/

Note: This lint is currently not functional, see [issue #44232] for
more details.

[issue #44232]: https://github.com/rust-lang/rust/issues/44232

## unused-imports

The `unused_imports` lint detects imports that are never used.

### Example

```rust
use std::collections::HashMap;
```

This will produce:

```text
warning: unused import: `std::collections::HashMap`
 --> lint_example.rs:2:5
  |
2 | use std::collections::HashMap;
  |     ^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(unused_imports)]` on by default

```

### Explanation

Unused imports may signal a mistake or unfinished code, and clutter
the code, and should be removed. If you intended to re-export the item
to make it available outside of the module, add a visibility modifier
like `pub`.

## unused-labels

The `unused_labels` lint detects [labels] that are never used.

[labels]: https://doc.rust-lang.org/reference/expressions/loop-expr.html#loop-labels

### Example

```rust,no_run
'unused_label: loop {}
```

This will produce:

```text
warning: unused label
 --> lint_example.rs:2:1
  |
2 | 'unused_label: loop {}
  | ^^^^^^^^^^^^^
  |
  = note: `#[warn(unused_labels)]` on by default

```

### Explanation

Unused labels may signal a mistake or unfinished code. To silence the
warning for the individual label, prefix it with an underscore such as
`'_my_label:`.

## unused-macros

The `unused_macros` lint detects macros that were not used.

Note that this lint is distinct from the `unused_macro_rules` lint,
which checks for single rules that never match of an otherwise used
macro, and thus never expand.

### Example

```rust
macro_rules! unused {
    () => {};
}

fn main() {
}
```

This will produce:

```text
warning: unused macro definition: `unused`
 --> lint_example.rs:1:14
  |
1 | macro_rules! unused {
  |              ^^^^^^
  |
  = note: `#[warn(unused_macros)]` on by default

```

### Explanation

Unused macros may signal a mistake or unfinished code. To silence the
warning for the individual macro, prefix the name with an underscore
such as `_my_macro`. If you intended to export the macro to make it
available outside of the crate, use the [`macro_export` attribute].

[`macro_export` attribute]: https://doc.rust-lang.org/reference/macros-by-example.html#path-based-scope

## unused-must-use

The `unused_must_use` lint detects unused result of a type flagged as
`#[must_use]`.

### Example

```rust
fn returns_result() -> Result<(), ()> {
    Ok(())
}

fn main() {
    returns_result();
}
```

This will produce:

```text
warning: unused `Result` that must be used
 --> lint_example.rs:6:5
  |
6 |     returns_result();
  |     ^^^^^^^^^^^^^^^^
  |
  = note: this `Result` may be an `Err` variant, which should be handled
  = note: `#[warn(unused_must_use)]` on by default
help: use `let _ = ...` to ignore the resulting value
  |
6 |     let _ = returns_result();
  |     +++++++

```

### Explanation

The `#[must_use]` attribute is an indicator that it is a mistake to
ignore the value. See [the reference] for more details.

[the reference]: https://doc.rust-lang.org/reference/attributes/diagnostics.html#the-must_use-attribute

## unused-mut

The `unused_mut` lint detects mut variables which don't need to be
mutable.

### Example

```rust
let mut x = 5;
```

This will produce:

```text
warning: variable does not need to be mutable
 --> lint_example.rs:2:5
  |
2 | let mut x = 5;
  |     ----^
  |     |
  |     help: remove this `mut`
  |
  = note: `#[warn(unused_mut)]` on by default

```

### Explanation

The preferred style is to only mark variables as `mut` if it is
required.

## unused-parens

The `unused_parens` lint detects `if`, `match`, `while` and `return`
with parentheses; they do not need them.

### Examples

```rust
if(true) {}
```

This will produce:

```text
warning: unnecessary parentheses around `if` condition
 --> lint_example.rs:2:3
  |
2 | if(true) {}
  |   ^    ^
  |
  = note: `#[warn(unused_parens)]` on by default
help: remove these parentheses
  |
2 - if(true) {}
2 + if true {}
  |

```

### Explanation

The parentheses are not needed, and should be removed. This is the
preferred style for writing these expressions.

## unused-unsafe

The `unused_unsafe` lint detects unnecessary use of an `unsafe` block.

### Example

```rust
unsafe {}
```

This will produce:

```text
warning: unnecessary `unsafe` block
 --> lint_example.rs:2:1
  |
2 | unsafe {}
  | ^^^^^^ unnecessary `unsafe` block
  |
  = note: `#[warn(unused_unsafe)]` on by default

```

### Explanation

If nothing within the block requires `unsafe`, then remove the
`unsafe` marker because it is not required and may cause confusion.

## unused-variables

The `unused_variables` lint detects variables which are not used in
any way.

### Example

```rust
let x = 5;
```

This will produce:

```text
warning: unused variable: `x`
 --> lint_example.rs:2:5
  |
2 | let x = 5;
  |     ^ help: if this is intentional, prefix it with an underscore: `_x`
  |
  = note: `#[warn(unused_variables)]` on by default

```

### Explanation

Unused variables may signal a mistake or unfinished code. To silence
the warning for the individual variable, prefix it with an underscore
such as `_x`.

## useless-ptr-null-checks

The `useless_ptr_null_checks` lint checks for useless null checks against pointers
obtained from non-null types.

### Example

```rust
# fn test() {}
let fn_ptr: fn() = /* somehow obtained nullable function pointer */
#   test;

if (fn_ptr as *const ()).is_null() { /* ... */ }
```

This will produce:

```text
warning: function pointers are not nullable, so checking them for null will always return false
 --> lint_example.rs:6:4
  |
6 | if (fn_ptr as *const ()).is_null() { /* ... */ }
  |    ^------^^^^^^^^^^^^^^^^^^^^^^^^
  |     |
  |     expression has type `fn()`
  |
  = help: wrap the function pointer inside an `Option` and use `Option::is_none` to check for null pointer value
  = note: `#[warn(useless_ptr_null_checks)]` on by default

```

### Explanation

Function pointers and references are assumed to be non-null, checking them for null
will always return false.

## warnings

The `warnings` lint allows you to change the level of other
lints which produce warnings.

### Example

```rust
#![deny(warnings)]
fn foo() {}
```

This will produce:

```text
error: function `foo` is never used
 --> lint_example.rs:3:4
  |
3 | fn foo() {}
  |    ^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(warnings)]
  |         ^^^^^^^^
  = note: `#[deny(dead_code)]` implied by `#[deny(warnings)]`

```

### Explanation

The `warnings` lint is a bit special; by changing its level, you
change every other warning that would produce a warning to whatever
value you'd like. As such, you won't ever trigger this lint in your
code directly.

## where-clauses-object-safety

The `where_clauses_object_safety` lint detects for [object safety] of
[where clauses].

[object safety]: https://doc.rust-lang.org/reference/items/traits.html#object-safety
[where clauses]: https://doc.rust-lang.org/reference/items/generics.html#where-clauses

### Example

```rust,no_run
trait Trait {}

trait X { fn foo(&self) where Self: Trait; }

impl X for () { fn foo(&self) {} }

impl Trait for dyn X {}

// Segfault at opt-level 0, SIGILL otherwise.
pub fn main() { <dyn X as X>::foo(&()); }
```

This will produce:

```text
warning: the trait `X` cannot be made into an object
 --> lint_example.rs:3:14
  |
3 | trait X { fn foo(&self) where Self: Trait; }
  |              ^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #51443 <https://github.com/rust-lang/rust/issues/51443>
note: for a trait to be "object safe" it needs to allow building a vtable to allow the call to be resolvable dynamically; for more information visit <https://doc.rust-lang.org/reference/items/traits.html#object-safety>
 --> lint_example.rs:3:14
  |
3 | trait X { fn foo(&self) where Self: Trait; }
  |       -      ^^^ ...because method `foo` references the `Self` type in its `where` clause
  |       |
  |       this trait cannot be made into an object...
  = help: consider moving `foo` to another trait
  = note: `#[warn(where_clauses_object_safety)]` on by default

```

### Explanation

The compiler previously allowed these object-unsafe bounds, which was
incorrect. This is a [future-incompatible] lint to transition this to
a hard error in the future. See [issue #51443] for more details.

[issue #51443]: https://github.com/rust-lang/rust/issues/51443
[future-incompatible]: ../index.md#future-incompatible-lints

## while-true

The `while_true` lint detects `while true { }`.

### Example

```rust,no_run
while true {

}
```

This will produce:

```text
warning: denote infinite loops with `loop { ... }`
 --> lint_example.rs:2:1
  |
2 | while true {
  | ^^^^^^^^^^ help: use `loop`
  |
  = note: `#[warn(while_true)]` on by default

```

### Explanation

`while true` should be replaced with `loop`. A `loop` expression is
the preferred way to write an infinite loop because it more directly
expresses the intent of the loop.

