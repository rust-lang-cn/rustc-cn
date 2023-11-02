# Allowed-by-default Lints

These lints are all set to the 'allow' level by default. As such, they won't show up
unless you set them to a higher lint level with a flag or attribute.

* [`absolute_paths_not_starting_with_crate`](#absolute-paths-not-starting-with-crate)
* [`box_pointers`](#box-pointers)
* [`elided_lifetimes_in_paths`](#elided-lifetimes-in-paths)
* [`explicit_outlives_requirements`](#explicit-outlives-requirements)
* [`ffi_unwind_calls`](#ffi-unwind-calls)
* [`fuzzy_provenance_casts`](#fuzzy-provenance-casts)
* [`keyword_idents`](#keyword-idents)
* [`let_underscore_drop`](#let-underscore-drop)
* [`lossy_provenance_casts`](#lossy-provenance-casts)
* [`macro_use_extern_crate`](#macro-use-extern-crate)
* [`meta_variable_misuse`](#meta-variable-misuse)
* [`missing_abi`](#missing-abi)
* [`missing_copy_implementations`](#missing-copy-implementations)
* [`missing_debug_implementations`](#missing-debug-implementations)
* [`missing_docs`](#missing-docs)
* [`multiple_supertrait_upcastable`](#multiple-supertrait-upcastable)
* [`must_not_suspend`](#must-not-suspend)
* [`non_ascii_idents`](#non-ascii-idents)
* [`non_exhaustive_omitted_patterns`](#non-exhaustive-omitted-patterns)
* [`pointer_structural_match`](#pointer-structural-match)
* [`rust_2021_incompatible_closure_captures`](#rust-2021-incompatible-closure-captures)
* [`rust_2021_incompatible_or_patterns`](#rust-2021-incompatible-or-patterns)
* [`rust_2021_prefixes_incompatible_syntax`](#rust-2021-prefixes-incompatible-syntax)
* [`rust_2021_prelude_collisions`](#rust-2021-prelude-collisions)
* [`single_use_lifetimes`](#single-use-lifetimes)
* [`trivial_casts`](#trivial-casts)
* [`trivial_numeric_casts`](#trivial-numeric-casts)
* [`unnameable_types`](#unnameable-types)
* [`unreachable_pub`](#unreachable-pub)
* [`unsafe_code`](#unsafe-code)
* [`unsafe_op_in_unsafe_fn`](#unsafe-op-in-unsafe-fn)
* [`unstable_features`](#unstable-features)
* [`unused_crate_dependencies`](#unused-crate-dependencies)
* [`unused_extern_crates`](#unused-extern-crates)
* [`unused_import_braces`](#unused-import-braces)
* [`unused_lifetimes`](#unused-lifetimes)
* [`unused_macro_rules`](#unused-macro-rules)
* [`unused_qualifications`](#unused-qualifications)
* [`unused_results`](#unused-results)
* [`unused_tuple_struct_fields`](#unused-tuple-struct-fields)
* [`variant_size_differences`](#variant-size-differences)

## absolute-paths-not-starting-with-crate

The `absolute_paths_not_starting_with_crate` lint detects fully
qualified paths that start with a module name instead of `crate`,
`self`, or an extern crate name

### Example

```rust,edition2015,compile_fail
#![deny(absolute_paths_not_starting_with_crate)]

mod foo {
    pub fn bar() {}
}

fn main() {
    ::foo::bar();
}
```

This will produce:

```text
error: absolute paths must start with `self`, `super`, `crate`, or an external crate name in the 2018 edition
 --> lint_example.rs:8:5
  |
8 |     ::foo::bar();
  |     ^^^^^^^^^^ help: use `crate`: `crate::foo::bar`
  |
  = warning: this is accepted in the current edition (Rust 2015) but is a hard error in Rust 2018!
  = note: for more information, see issue #53130 <https://github.com/rust-lang/rust/issues/53130>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(absolute_paths_not_starting_with_crate)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Rust [editions] allow the language to evolve without breaking
backwards compatibility. This lint catches code that uses absolute
paths in the style of the 2015 edition. In the 2015 edition, absolute
paths (those starting with `::`) refer to either the crate root or an
external crate. In the 2018 edition it was changed so that they only
refer to external crates. The path prefix `crate::` should be used
instead to reference items from the crate root.

If you switch the compiler from the 2015 to 2018 edition without
updating the code, then it will fail to compile if the old style paths
are used. You can manually change the paths to use the `crate::`
prefix to transition to the 2018 edition.

This lint solves the problem automatically. It is "allow" by default
because the code is perfectly valid in the 2015 edition. The [`cargo
fix`] tool with the `--edition` flag will switch this lint to "warn"
and automatically apply the suggested fix from the compiler. This
provides a completely automated way to update old code to the 2018
edition.

[editions]: https://doc.rust-lang.org/edition-guide/
[`cargo fix`]: https://doc.rust-lang.org/cargo/commands/cargo-fix.html

## box-pointers

The `box_pointers` lints use of the Box type.

### Example

```rust,compile_fail
#![deny(box_pointers)]
struct Foo {
    x: Box<isize>,
}
```

This will produce:

```text
error: type uses owned (Box type) pointers: Box<isize>
 --> lint_example.rs:4:5
  |
4 |     x: Box<isize>,
  |     ^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(box_pointers)]
  |         ^^^^^^^^^^^^

```

### Explanation

This lint is mostly historical, and not particularly useful. `Box<T>`
used to be built into the language, and the only way to do heap
allocation. Today's Rust can call into other allocators, etc.

## elided-lifetimes-in-paths

The `elided_lifetimes_in_paths` lint detects the use of hidden
lifetime parameters.

### Example

```rust,compile_fail
#![deny(elided_lifetimes_in_paths)]
#![deny(warnings)]
struct Foo<'a> {
    x: &'a u32
}

fn foo(x: &Foo) {
}
```

This will produce:

```text
error: hidden lifetime parameters in types are deprecated
 --> lint_example.rs:8:12
  |
8 | fn foo(x: &Foo) {
  |            ^^^ expected lifetime parameter
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(elided_lifetimes_in_paths)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^
help: indicate the anonymous lifetime
  |
8 | fn foo(x: &Foo<'_>) {
  |               ++++

```

### Explanation

Elided lifetime parameters can make it difficult to see at a glance
that borrowing is occurring. This lint ensures that lifetime
parameters are always explicitly stated, even if it is the `'_`
[placeholder lifetime].

This lint is "allow" by default because it has some known issues, and
may require a significant transition for old code.

[placeholder lifetime]: https://doc.rust-lang.org/reference/lifetime-elision.html#lifetime-elision-in-functions

## explicit-outlives-requirements

The `explicit_outlives_requirements` lint detects unnecessary
lifetime bounds that can be inferred.

### Example

```rust,compile_fail
# #![allow(unused)]
#![deny(explicit_outlives_requirements)]
#![deny(warnings)]

struct SharedRef<'a, T>
where
    T: 'a,
{
    data: &'a T,
}
```

This will produce:

```text
error: outlives requirements can be inferred
 --> lint_example.rs:6:24
  |
6 |   struct SharedRef<'a, T>
  |  ________________________^
7 | | where
8 | |     T: 'a,
  | |__________^ help: remove this bound
  |
note: the lint level is defined here
 --> lint_example.rs:2:9
  |
2 | #![deny(explicit_outlives_requirements)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

If a `struct` contains a reference, such as `&'a T`, the compiler
requires that `T` outlives the lifetime `'a`. This historically
required writing an explicit lifetime bound to indicate this
requirement. However, this can be overly explicit, causing clutter and
unnecessary complexity. The language was changed to automatically
infer the bound if it is not specified. Specifically, if the struct
contains a reference, directly or indirectly, to `T` with lifetime
`'x`, then it will infer that `T: 'x` is a requirement.

This lint is "allow" by default because it can be noisy for existing
code that already had these requirements. This is a stylistic choice,
as it is still valid to explicitly state the bound. It also has some
false positives that can cause confusion.

See [RFC 2093] for more details.

[RFC 2093]: https://github.com/rust-lang/rfcs/blob/master/text/2093-infer-outlives.md

## ffi-unwind-calls

The `ffi_unwind_calls` lint detects calls to foreign functions or function pointers with
`C-unwind` or other FFI-unwind ABIs.

### Example

```rust
#![warn(ffi_unwind_calls)]

extern "C-unwind" {
    fn foo();
}

fn bar() {
    unsafe { foo(); }
    let ptr: unsafe extern "C-unwind" fn() = foo;
    unsafe { ptr(); }
}
```

This will produce:

```text
warning: call to foreign function with FFI-unwind ABI
 --> lint_example.rs:9:14
  |
9 |     unsafe { foo(); }
  |              ^^^^^ call to foreign function with FFI-unwind ABI
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![warn(ffi_unwind_calls)]
  |         ^^^^^^^^^^^^^^^^


warning: call to function pointer with FFI-unwind ABI
  --> lint_example.rs:11:14
   |
11 |     unsafe { ptr(); }
   |              ^^^^^ call to function pointer with FFI-unwind ABI

```

### Explanation

For crates containing such calls, if they are compiled with `-C panic=unwind` then the
produced library cannot be linked with crates compiled with `-C panic=abort`. For crates
that desire this ability it is therefore necessary to avoid such calls.

## fuzzy-provenance-casts

The `fuzzy_provenance_casts` lint detects an `as` cast between an integer
and a pointer.

### Example

```rust
#![feature(strict_provenance)]
#![warn(fuzzy_provenance_casts)]

fn main() {
    let _dangling = 16_usize as *const u8;
}
```

This will produce:

```text
warning: strict provenance disallows casting integer `usize` to pointer `*const u8`
 --> lint_example.rs:5:21
  |
5 |     let _dangling = 16_usize as *const u8;
  |                     ^^^^^^^^^^^^^^^^^^^^^
  |
  = help: if you can't comply with strict provenance and don't have a pointer with the correct provenance you can use `std::ptr::from_exposed_addr()` instead
note: the lint level is defined here
 --> lint_example.rs:2:9
  |
2 | #![warn(fuzzy_provenance_casts)]
  |         ^^^^^^^^^^^^^^^^^^^^^^
help: use `.with_addr()` to adjust a valid pointer in the same allocation, to this address
  |
5 |     let _dangling = (...).with_addr(16_usize);
  |                     ++++++++++++++++        ~

```

### Explanation

This lint is part of the strict provenance effort, see [issue #95228].
Casting an integer to a pointer is considered bad style, as a pointer
contains, besides the *address* also a *provenance*, indicating what
memory the pointer is allowed to read/write. Casting an integer, which
doesn't have provenance, to a pointer requires the compiler to assign
(guess) provenance. The compiler assigns "all exposed valid" (see the
docs of [`ptr::from_exposed_addr`] for more information about this
"exposing"). This penalizes the optimiser and is not well suited for
dynamic analysis/dynamic program verification (e.g. Miri or CHERI
platforms).

It is much better to use [`ptr::with_addr`] instead to specify the
provenance you want. If using this function is not possible because the
code relies on exposed provenance then there is as an escape hatch
[`ptr::from_exposed_addr`].

[issue #95228]: https://github.com/rust-lang/rust/issues/95228
[`ptr::with_addr`]: https://doc.rust-lang.org/core/ptr/fn.with_addr
[`ptr::from_exposed_addr`]: https://doc.rust-lang.org/core/ptr/fn.from_exposed_addr

## keyword-idents

The `keyword_idents` lint detects edition keywords being used as an
identifier.

### Example

```rust,edition2015,compile_fail
#![deny(keyword_idents)]
// edition 2015
fn dyn() {}
```

This will produce:

```text
error: `dyn` is a keyword in the 2018 edition
 --> lint_example.rs:4:4
  |
4 | fn dyn() {}
  |    ^^^ help: you can use a raw identifier to stay compatible: `r#dyn`
  |
  = warning: this is accepted in the current edition (Rust 2015) but is a hard error in Rust 2018!
  = note: for more information, see issue #49716 <https://github.com/rust-lang/rust/issues/49716>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(keyword_idents)]
  |         ^^^^^^^^^^^^^^

```

### Explanation

Rust [editions] allow the language to evolve without breaking
backwards compatibility. This lint catches code that uses new keywords
that are added to the language that are used as identifiers (such as a
variable name, function name, etc.). If you switch the compiler to a
new edition without updating the code, then it will fail to compile if
you are using a new keyword as an identifier.

You can manually change the identifiers to a non-keyword, or use a
[raw identifier], for example `r#dyn`, to transition to a new edition.

This lint solves the problem automatically. It is "allow" by default
because the code is perfectly valid in older editions. The [`cargo
fix`] tool with the `--edition` flag will switch this lint to "warn"
and automatically apply the suggested fix from the compiler (which is
to use a raw identifier). This provides a completely automated way to
update old code for a new edition.

[editions]: https://doc.rust-lang.org/edition-guide/
[raw identifier]: https://doc.rust-lang.org/reference/identifiers.html
[`cargo fix`]: https://doc.rust-lang.org/cargo/commands/cargo-fix.html

## let-underscore-drop

The `let_underscore_drop` lint checks for statements which don't bind
an expression which has a non-trivial Drop implementation to anything,
causing the expression to be dropped immediately instead of at end of
scope.

### Example

```rust
struct SomeStruct;
impl Drop for SomeStruct {
    fn drop(&mut self) {
        println!("Dropping SomeStruct");
    }
}

fn main() {
   #[warn(let_underscore_drop)]
    // SomeStruct is dropped immediately instead of at end of scope,
    // so "Dropping SomeStruct" is printed before "end of main".
    // The order of prints would be reversed if SomeStruct was bound to
    // a name (such as "_foo").
    let _ = SomeStruct;
    println!("end of main");
}
```

This will produce:

```text
warning: non-binding let on a type that implements `Drop`
  --> lint_example.rs:14:5
   |
14 |     let _ = SomeStruct;
   |     ^^^^^^^^^^^^^^^^^^^
   |
note: the lint level is defined here
  --> lint_example.rs:9:11
   |
9  |    #[warn(let_underscore_drop)]
   |           ^^^^^^^^^^^^^^^^^^^
help: consider binding to an unused variable to avoid immediately dropping the value
   |
14 |     let _unused = SomeStruct;
   |         ~~~~~~~
help: consider immediately dropping the value
   |
14 |     drop(SomeStruct);
   |     ~~~~~          +

```

### Explanation

Statements which assign an expression to an underscore causes the
expression to immediately drop instead of extending the expression's
lifetime to the end of the scope. This is usually unintended,
especially for types like `MutexGuard`, which are typically used to
lock a mutex for the duration of an entire scope.

If you want to extend the expression's lifetime to the end of the scope,
assign an underscore-prefixed name (such as `_foo`) to the expression.
If you do actually want to drop the expression immediately, then
calling `std::mem::drop` on the expression is clearer and helps convey
intent.

## lossy-provenance-casts

The `lossy_provenance_casts` lint detects an `as` cast between a pointer
and an integer.

### Example

```rust
#![feature(strict_provenance)]
#![warn(lossy_provenance_casts)]

fn main() {
    let x: u8 = 37;
    let _addr: usize = &x as *const u8 as usize;
}
```

This will produce:

```text
warning: under strict provenance it is considered bad style to cast pointer `*const u8` to integer `usize`
 --> lint_example.rs:6:24
  |
6 |     let _addr: usize = &x as *const u8 as usize;
  |                        ^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = help: if you can't comply with strict provenance and need to expose the pointer provenance you can use `.expose_addr()` instead
note: the lint level is defined here
 --> lint_example.rs:2:9
  |
2 | #![warn(lossy_provenance_casts)]
  |         ^^^^^^^^^^^^^^^^^^^^^^
help: use `.addr()` to obtain the address of a pointer
  |
6 |     let _addr: usize = (&x as *const u8).addr();
  |                        +               ~~~~~~~~

```

### Explanation

This lint is part of the strict provenance effort, see [issue #95228].
Casting a pointer to an integer is a lossy operation, because beyond
just an *address* a pointer may be associated with a particular
*provenance*. This information is used by the optimiser and for dynamic
analysis/dynamic program verification (e.g. Miri or CHERI platforms).

Since this cast is lossy, it is considered good style to use the
[`ptr::addr`] method instead, which has a similar effect, but doesn't
"expose" the pointer provenance. This improves optimisation potential.
See the docs of [`ptr::addr`] and [`ptr::expose_addr`] for more information
about exposing pointer provenance.

If your code can't comply with strict provenance and needs to expose
the provenance, then there is [`ptr::expose_addr`] as an escape hatch,
which preserves the behaviour of `as usize` casts while being explicit
about the semantics.

[issue #95228]: https://github.com/rust-lang/rust/issues/95228
[`ptr::addr`]: https://doc.rust-lang.org/core/ptr/fn.addr
[`ptr::expose_addr`]: https://doc.rust-lang.org/core/ptr/fn.expose_addr

## macro-use-extern-crate

The `macro_use_extern_crate` lint detects the use of the
[`macro_use` attribute].

### Example

```rust,ignore (needs extern crate)
#![deny(macro_use_extern_crate)]

#[macro_use]
extern crate serde_json;

fn main() {
    let _ = json!{{}};
}
```

This will produce:

```text
error: deprecated `#[macro_use]` attribute used to import macros should be replaced at use sites with a `use` item to import the macro instead
 --> src/main.rs:3:1
  |
3 | #[macro_use]
  | ^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> src/main.rs:1:9
  |
1 | #![deny(macro_use_extern_crate)]
  |         ^^^^^^^^^^^^^^^^^^^^^^
```

### Explanation

The [`macro_use` attribute] on an [`extern crate`] item causes
macros in that external crate to be brought into the prelude of the
crate, making the macros in scope everywhere. As part of the efforts
to simplify handling of dependencies in the [2018 edition], the use of
`extern crate` is being phased out. To bring macros from extern crates
into scope, it is recommended to use a [`use` import].

This lint is "allow" by default because this is a stylistic choice
that has not been settled, see [issue #52043] for more information.

[`macro_use` attribute]: https://doc.rust-lang.org/reference/macros-by-example.html#the-macro_use-attribute
[`use` import]: https://doc.rust-lang.org/reference/items/use-declarations.html
[issue #52043]: https://github.com/rust-lang/rust/issues/52043

## meta-variable-misuse

The `meta_variable_misuse` lint detects possible meta-variable misuse
in macro definitions.

### Example

```rust,compile_fail
#![deny(meta_variable_misuse)]

macro_rules! foo {
    () => {};
    ($( $i:ident = $($j:ident),+ );*) => { $( $( $i = $k; )+ )* };
}

fn main() {
    foo!();
}
```

This will produce:

```text
error: unknown macro variable `k`
 --> lint_example.rs:5:55
  |
5 |     ($( $i:ident = $($j:ident),+ );*) => { $( $( $i = $k; )+ )* };
  |                                                       ^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(meta_variable_misuse)]
  |         ^^^^^^^^^^^^^^^^^^^^

```

### Explanation

There are quite a few different ways a [`macro_rules`] macro can be
improperly defined. Many of these errors were previously only detected
when the macro was expanded or not at all. This lint is an attempt to
catch some of these problems when the macro is *defined*.

This lint is "allow" by default because it may have false positives
and other issues. See [issue #61053] for more details.

[`macro_rules`]: https://doc.rust-lang.org/reference/macros-by-example.html
[issue #61053]: https://github.com/rust-lang/rust/issues/61053

## missing-abi

The `missing_abi` lint detects cases where the ABI is omitted from
extern declarations.

### Example

```rust,compile_fail
#![deny(missing_abi)]

extern fn foo() {}
```

This will produce:

```text
error: extern declarations without an explicit ABI are deprecated
 --> lint_example.rs:4:1
  |
4 | extern fn foo() {}
  | ^^^^^^^^^^^^^^^ ABI should be specified here
  |
  = help: the default ABI is C
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(missing_abi)]
  |         ^^^^^^^^^^^

```

### Explanation

Historically, Rust implicitly selected C as the ABI for extern
declarations. We expect to add new ABIs, like `C-unwind`, in the future,
though this has not yet happened, and especially with their addition
seeing the ABI easily will make code review easier.

## missing-copy-implementations

The `missing_copy_implementations` lint detects potentially-forgotten
implementations of [`Copy`] for public types.

[`Copy`]: https://doc.rust-lang.org/std/marker/trait.Copy.html

### Example

```rust,compile_fail
#![deny(missing_copy_implementations)]
pub struct Foo {
    pub field: i32
}
# fn main() {}
```

This will produce:

```text
error: type could implement `Copy`; consider adding `impl Copy`
 --> lint_example.rs:2:1
  |
2 | / pub struct Foo {
3 | |     pub field: i32
4 | | }
  | |_^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(missing_copy_implementations)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Historically (before 1.0), types were automatically marked as `Copy`
if possible. This was changed so that it required an explicit opt-in
by implementing the `Copy` trait. As part of this change, a lint was
added to alert if a copyable type was not marked `Copy`.

This lint is "allow" by default because this code isn't bad; it is
common to write newtypes like this specifically so that a `Copy` type
is no longer `Copy`. `Copy` types can result in unintended copies of
large data which can impact performance.

## missing-debug-implementations

The `missing_debug_implementations` lint detects missing
implementations of [`fmt::Debug`] for public types.

[`fmt::Debug`]: https://doc.rust-lang.org/std/fmt/trait.Debug.html

### Example

```rust,compile_fail
#![deny(missing_debug_implementations)]
pub struct Foo;
# fn main() {}
```

This will produce:

```text
error: type does not implement `Debug`; consider adding `#[derive(Debug)]` or a manual implementation
 --> lint_example.rs:2:1
  |
2 | pub struct Foo;
  | ^^^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(missing_debug_implementations)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Having a `Debug` implementation on all types can assist with
debugging, as it provides a convenient way to format and display a
value. Using the `#[derive(Debug)]` attribute will automatically
generate a typical implementation, or a custom implementation can be
added by manually implementing the `Debug` trait.

This lint is "allow" by default because adding `Debug` to all types can
have a negative impact on compile time and code size. It also requires
boilerplate to be added to every type, which can be an impediment.

## missing-docs

The `missing_docs` lint detects missing documentation for public items.

### Example

```rust,compile_fail
#![deny(missing_docs)]
pub fn foo() {}
```

This will produce:

```text
error: missing documentation for the crate
 --> lint_example.rs:1:1
  |
1 | / #![deny(missing_docs)]
2 | | fn main() {
3 | | pub fn foo() {}
4 | | }
  | |_^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(missing_docs)]
  |         ^^^^^^^^^^^^

```

### Explanation

This lint is intended to ensure that a library is well-documented.
Items without documentation can be difficult for users to understand
how to use properly.

This lint is "allow" by default because it can be noisy, and not all
projects may want to enforce everything to be documented.

## multiple-supertrait-upcastable

The `multiple_supertrait_upcastable` lint detects when an object-safe trait has multiple
supertraits.

### Example

```rust
#![feature(multiple_supertrait_upcastable)]
trait A {}
trait B {}

#[warn(multiple_supertrait_upcastable)]
trait C: A + B {}
```

This will produce:

```text
warning: `C` is object-safe and has multiple supertraits
 --> lint_example.rs:7:1
  |
7 | trait C: A + B {}
  | ^^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:6:8
  |
6 | #[warn(multiple_supertrait_upcastable)]
  |        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

To support upcasting with multiple supertraits, we need to store multiple vtables and this
can result in extra space overhead, even if no code actually uses upcasting.
This lint allows users to identify when such scenarios occur and to decide whether the
additional overhead is justified.

## must-not-suspend

The `must_not_suspend` lint guards against values that shouldn't be held across suspend points
(`.await`)

### Example

```rust
#![feature(must_not_suspend)]
#![warn(must_not_suspend)]

#[must_not_suspend]
struct SyncThing {}

async fn yield_now() {}

pub async fn uhoh() {
    let guard = SyncThing {};
    yield_now().await;
    let _guard = guard;
}
```

This will produce:

```text
warning: `SyncThing` held across a suspend point, but should not be
  --> lint_example.rs:11:9
   |
11 |     let guard = SyncThing {};
   |         ^^^^^
12 |     yield_now().await;
   |                 ----- the value is held across this suspend point
   |
help: consider using a block (`{ ... }`) to shrink the value's scope, ending before the suspend point
  --> lint_example.rs:11:9
   |
11 |     let guard = SyncThing {};
   |         ^^^^^
note: the lint level is defined here
  --> lint_example.rs:2:9
   |
2  | #![warn(must_not_suspend)]
   |         ^^^^^^^^^^^^^^^^

```

### Explanation

The `must_not_suspend` lint detects values that are marked with the `#[must_not_suspend]`
attribute being held across suspend points. A "suspend" point is usually a `.await` in an async
function.

This attribute can be used to mark values that are semantically incorrect across suspends
(like certain types of timers), values that have async alternatives, and values that
regularly cause problems with the `Send`-ness of async fn's returned futures (like
`MutexGuard`'s)


## non-ascii-idents

The `non_ascii_idents` lint detects non-ASCII identifiers.

### Example

```rust,compile_fail
# #![allow(unused)]
#![deny(non_ascii_idents)]
fn main() {
    let föö = 1;
}
```

This will produce:

```text
error: identifier contains non-ASCII characters
 --> lint_example.rs:4:9
  |
4 |     let föö = 1;
  |         ^^^
  |
note: the lint level is defined here
 --> lint_example.rs:2:9
  |
2 | #![deny(non_ascii_idents)]
  |         ^^^^^^^^^^^^^^^^

```

### Explanation

This lint allows projects that wish to retain the limit of only using
ASCII characters to switch this lint to "forbid" (for example to ease
collaboration or for security reasons).
See [RFC 2457] for more details.

[RFC 2457]: https://github.com/rust-lang/rfcs/blob/master/text/2457-non-ascii-idents.md

## non-exhaustive-omitted-patterns

The `non_exhaustive_omitted_patterns` lint aims to help consumers of a `#[non_exhaustive]`
struct or enum who want to match all of its fields/variants explicitly.

The `#[non_exhaustive]` annotation forces matches to use wildcards, so exhaustiveness
checking cannot be used to ensure that all fields/variants are matched explicitly. To remedy
this, this allow-by-default lint warns the user when a match mentions some but not all of
the fields/variants of a `#[non_exhaustive]` struct or enum.

### Example

```rust,ignore (needs separate crate)
// crate A
#[non_exhaustive]
pub enum Bar {
    A,
    B, // added variant in non breaking change
}

// in crate B
#![feature(non_exhaustive_omitted_patterns_lint)]
#[warn(non_exhaustive_omitted_patterns)]
match Bar::A {
    Bar::A => {},
    _ => {},
}
```

This will produce:

```text
warning: some variants are not matched explicitly
   --> $DIR/reachable-patterns.rs:70:9
   |
LL |         match Bar::A {
   |               ^ pattern `Bar::B` not covered
   |
 note: the lint level is defined here
  --> $DIR/reachable-patterns.rs:69:16
   |
LL |         #[warn(non_exhaustive_omitted_patterns)]
   |                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   = help: ensure that all variants are matched explicitly by adding the suggested match arms
   = note: the matched value is of type `Bar` and the `non_exhaustive_omitted_patterns` attribute was found
```

Warning: setting this to `deny` will make upstream non-breaking changes (adding fields or
variants to a `#[non_exhaustive]` struct or enum) break your crate. This goes against
expected semver behavior.

### Explanation

Structs and enums tagged with `#[non_exhaustive]` force the user to add a (potentially
redundant) wildcard when pattern-matching, to allow for future addition of fields or
variants. The `non_exhaustive_omitted_patterns` lint detects when such a wildcard happens to
actually catch some fields/variants. In other words, when the match without the wildcard
would not be exhaustive. This lets the user be informed if new fields/variants were added.

## pointer-structural-match

The `pointer_structural_match` lint detects pointers used in patterns whose behaviour
cannot be relied upon across compiler versions and optimization levels.

### Example

```rust,compile_fail
#![deny(pointer_structural_match)]
fn foo(a: usize, b: usize) -> usize { a + b }
const FOO: fn(usize, usize) -> usize = foo;
fn main() {
    match FOO {
        FOO => {},
        _ => {},
    }
}
```

This will produce:

```text
error: function pointers and unsized pointers in patterns behave unpredictably and should not be relied upon. See https://github.com/rust-lang/rust/issues/70861 for details.
 --> lint_example.rs:6:9
  |
6 |         FOO => {},
  |         ^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #62411 <https://github.com/rust-lang/rust/issues/70861>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(pointer_structural_match)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Previous versions of Rust allowed function pointers and wide raw pointers in patterns.
While these work in many cases as expected by users, it is possible that due to
optimizations pointers are "not equal to themselves" or pointers to different functions
compare as equal during runtime. This is because LLVM optimizations can deduplicate
functions if their bodies are the same, thus also making pointers to these functions point
to the same location. Additionally functions may get duplicated if they are instantiated
in different crates and not deduplicated again via LTO.

## rust-2021-incompatible-closure-captures

The `rust_2021_incompatible_closure_captures` lint detects variables that aren't completely
captured in Rust 2021, such that the `Drop` order of their fields may differ between
Rust 2018 and 2021.

It can also detect when a variable implements a trait like `Send`, but one of its fields does not,
and the field is captured by a closure and used with the assumption that said field implements
the same trait as the root variable.

### Example of drop reorder

```rust,edition2018,compile_fail
#![deny(rust_2021_incompatible_closure_captures)]
# #![allow(unused)]

struct FancyInteger(i32);

impl Drop for FancyInteger {
    fn drop(&mut self) {
        println!("Just dropped {}", self.0);
    }
}

struct Point { x: FancyInteger, y: FancyInteger }

fn main() {
  let p = Point { x: FancyInteger(10), y: FancyInteger(20) };

  let c = || {
     let x = p.x;
  };

  c();

  // ... More code ...
}
```

This will produce:

```text
error: changes to closure capture in Rust 2021 will affect drop order
  --> lint_example.rs:17:11
   |
17 |   let c = || {
   |           ^^
18 |      let x = p.x;
   |              --- in Rust 2018, this closure captures all of `p`, but in Rust 2021, it will only capture `p.x`
...
24 | }
   | - in Rust 2018, `p` is dropped here, but in Rust 2021, only `p.x` will be dropped here as part of the closure
   |
   = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/disjoint-capture-in-closures.html>
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(rust_2021_incompatible_closure_captures)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
help: add a dummy let to cause `p` to be fully captured
   |
17 ~   let c = || {
18 +      let _ = &p;
   |

```

### Explanation

In the above example, `p.y` will be dropped at the end of `f` instead of
with `c` in Rust 2021.

### Example of auto-trait

```rust,edition2018,compile_fail
#![deny(rust_2021_incompatible_closure_captures)]
use std::thread;

struct Pointer(*mut i32);
unsafe impl Send for Pointer {}

fn main() {
    let mut f = 10;
    let fptr = Pointer(&mut f as *mut i32);
    thread::spawn(move || unsafe {
        *fptr.0 = 20;
    });
}
```

This will produce:

```text
error: changes to closure capture in Rust 2021 will affect which traits the closure implements
  --> lint_example.rs:10:19
   |
10 |     thread::spawn(move || unsafe {
   |                   ^^^^^^^ in Rust 2018, this closure implements `Send` as `fptr` implements `Send`, but in Rust 2021, this closure will no longer implement `Send` because `fptr` is not fully captured and `fptr.0` does not implement `Send`
11 |         *fptr.0 = 20;
   |         ------- in Rust 2018, this closure captures all of `fptr`, but in Rust 2021, it will only capture `fptr.0`
   |
   = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/disjoint-capture-in-closures.html>
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(rust_2021_incompatible_closure_captures)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
help: add a dummy let to cause `fptr` to be fully captured
   |
10 ~     thread::spawn(move || { let _ = &fptr; unsafe {
11 |         *fptr.0 = 20;
12 ~     } });
   |

```

### Explanation

In the above example, only `fptr.0` is captured in Rust 2021.
The field is of type `*mut i32`, which doesn't implement `Send`,
making the code invalid as the field cannot be sent between threads safely.

## rust-2021-incompatible-or-patterns

The `rust_2021_incompatible_or_patterns` lint detects usage of old versions of or-patterns.

### Example

```rust,compile_fail
#![deny(rust_2021_incompatible_or_patterns)]

macro_rules! match_any {
    ( $expr:expr , $( $( $pat:pat )|+ => $expr_arm:expr ),+ ) => {
        match $expr {
            $(
                $( $pat => $expr_arm, )+
            )+
        }
    };
}

fn main() {
    let result: Result<i64, i32> = Err(42);
    let int: i64 = match_any!(result, Ok(i) | Err(i) => i.into());
    assert_eq!(int, 42);
}
```

This will produce:

```text
error: the meaning of the `pat` fragment specifier is changing in Rust 2021, which may affect this macro
 --> lint_example.rs:4:26
  |
4 |     ( $expr:expr , $( $( $pat:pat )|+ => $expr_arm:expr ),+ ) => {
  |                          ^^^^^^^^ help: use pat_param to preserve semantics: `$pat:pat_param`
  |
  = warning: this is accepted in the current edition (Rust 2018) but is a hard error in Rust 2021!
  = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/or-patterns-macro-rules.html>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(rust_2021_incompatible_or_patterns)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

In Rust 2021, the `pat` matcher will match additional patterns, which include the `|` character.

## rust-2021-prefixes-incompatible-syntax

The `rust_2021_prefixes_incompatible_syntax` lint detects identifiers that will be parsed as a
prefix instead in Rust 2021.

### Example

```rust,edition2018,compile_fail
#![deny(rust_2021_prefixes_incompatible_syntax)]

macro_rules! m {
    (z $x:expr) => ();
}

m!(z"hey");
```

This will produce:

```text
error: prefix `z` is unknown
 --> lint_example.rs:8:4
  |
8 | m!(z"hey");
  |    ^ unknown prefix
  |
  = warning: this is accepted in the current edition (Rust 2018) but is a hard error in Rust 2021!
  = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/reserving-syntax.html>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(rust_2021_prefixes_incompatible_syntax)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
help: insert whitespace here to avoid this being parsed as a prefix in Rust 2021
  |
8 | m!(z "hey");
  |     +

```

### Explanation

In Rust 2015 and 2018, `z"hey"` is two tokens: the identifier `z`
followed by the string literal `"hey"`. In Rust 2021, the `z` is
considered a prefix for `"hey"`.

This lint suggests to add whitespace between the `z` and `"hey"` tokens
to keep them separated in Rust 2021.

## rust-2021-prelude-collisions

The `rust_2021_prelude_collisions` lint detects the usage of trait methods which are ambiguous
with traits added to the prelude in future editions.

### Example

```rust,compile_fail
#![deny(rust_2021_prelude_collisions)]

trait Foo {
    fn try_into(self) -> Result<String, !>;
}

impl Foo for &str {
    fn try_into(self) -> Result<String, !> {
        Ok(String::from(self))
    }
}

fn main() {
    let x: String = "3".try_into().unwrap();
    //                  ^^^^^^^^
    // This call to try_into matches both Foo::try_into and TryInto::try_into as
    // `TryInto` has been added to the Rust prelude in 2021 edition.
    println!("{x}");
}
```

This will produce:

```text
error: trait method `try_into` will become ambiguous in Rust 2021
  --> lint_example.rs:14:21
   |
14 |     let x: String = "3".try_into().unwrap();
   |                     ^^^^^^^^^^^^^^ help: disambiguate the associated function: `Foo::try_into(&*"3")`
   |
   = warning: this is accepted in the current edition (Rust 2018) but is a hard error in Rust 2021!
   = note: for more information, see <https://doc.rust-lang.org/nightly/edition-guide/rust-2021/prelude.html>
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(rust_2021_prelude_collisions)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

In Rust 2021, one of the important introductions is the [prelude changes], which add
`TryFrom`, `TryInto`, and `FromIterator` into the standard library's prelude. Since this
results in an ambiguity as to which method/function to call when an existing `try_into`
method is called via dot-call syntax or a `try_from`/`from_iter` associated function
is called directly on a type.

[prelude changes]: https://blog.rust-lang.org/inside-rust/2021/03/04/planning-rust-2021.html#prelude-changes

## single-use-lifetimes

The `single_use_lifetimes` lint detects lifetimes that are only used
once.

### Example

```rust,compile_fail
#![deny(single_use_lifetimes)]

fn foo<'a>(x: &'a u32) {}
```

This will produce:

```text
error: lifetime parameter `'a` only used once
 --> lint_example.rs:4:8
  |
4 | fn foo<'a>(x: &'a u32) {}
  |        ^^      -- ...is used only here
  |        |
  |        this lifetime...
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(single_use_lifetimes)]
  |         ^^^^^^^^^^^^^^^^^^^^
help: elide the single-use lifetime
  |
4 - fn foo<'a>(x: &'a u32) {}
4 + fn foo(x: &u32) {}
  |

```

### Explanation

Specifying an explicit lifetime like `'a` in a function or `impl`
should only be used to link together two things. Otherwise, you should
just use `'_` to indicate that the lifetime is not linked to anything,
or elide the lifetime altogether if possible.

This lint is "allow" by default because it was introduced at a time
when `'_` and elided lifetimes were first being introduced, and this
lint would be too noisy. Also, there are some known false positives
that it produces. See [RFC 2115] for historical context, and [issue
#44752] for more details.

[RFC 2115]: https://github.com/rust-lang/rfcs/blob/master/text/2115-argument-lifetimes.md
[issue #44752]: https://github.com/rust-lang/rust/issues/44752

## trivial-casts

The `trivial_casts` lint detects trivial casts which could be replaced
with coercion, which may require a temporary variable.

### Example

```rust,compile_fail
#![deny(trivial_casts)]
let x: &u32 = &42;
let y = x as *const u32;
```

This will produce:

```text
error: trivial cast: `&u32` as `*const u32`
 --> lint_example.rs:4:9
  |
4 | let y = x as *const u32;
  |         ^^^^^^^^^^^^^^^
  |
  = help: cast can be replaced by coercion; this might require a temporary variable
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(trivial_casts)]
  |         ^^^^^^^^^^^^^

```

### Explanation

A trivial cast is a cast `e as T` where `e` has type `U` and `U` is a
subtype of `T`. This type of cast is usually unnecessary, as it can be
usually be inferred.

This lint is "allow" by default because there are situations, such as
with FFI interfaces or complex type aliases, where it triggers
incorrectly, or in situations where it will be more difficult to
clearly express the intent. It may be possible that this will become a
warning in the future, possibly with an explicit syntax for coercions
providing a convenient way to work around the current issues.
See [RFC 401 (coercions)][rfc-401], [RFC 803 (type ascription)][rfc-803] and
[RFC 3307 (remove type ascription)][rfc-3307] for historical context.

[rfc-401]: https://github.com/rust-lang/rfcs/blob/master/text/0401-coercions.md
[rfc-803]: https://github.com/rust-lang/rfcs/blob/master/text/0803-type-ascription.md
[rfc-3307]: https://github.com/rust-lang/rfcs/blob/master/text/3307-de-rfc-type-ascription.md

## trivial-numeric-casts

The `trivial_numeric_casts` lint detects trivial numeric casts of types
which could be removed.

### Example

```rust,compile_fail
#![deny(trivial_numeric_casts)]
let x = 42_i32 as i32;
```

This will produce:

```text
error: trivial numeric cast: `i32` as `i32`
 --> lint_example.rs:3:9
  |
3 | let x = 42_i32 as i32;
  |         ^^^^^^^^^^^^^
  |
  = help: cast can be replaced by coercion; this might require a temporary variable
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(trivial_numeric_casts)]
  |         ^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

A trivial numeric cast is a cast of a numeric type to the same numeric
type. This type of cast is usually unnecessary.

This lint is "allow" by default because there are situations, such as
with FFI interfaces or complex type aliases, where it triggers
incorrectly, or in situations where it will be more difficult to
clearly express the intent. It may be possible that this will become a
warning in the future, possibly with an explicit syntax for coercions
providing a convenient way to work around the current issues.
See [RFC 401 (coercions)][rfc-401], [RFC 803 (type ascription)][rfc-803] and
[RFC 3307 (remove type ascription)][rfc-3307] for historical context.

[rfc-401]: https://github.com/rust-lang/rfcs/blob/master/text/0401-coercions.md
[rfc-803]: https://github.com/rust-lang/rfcs/blob/master/text/0803-type-ascription.md
[rfc-3307]: https://github.com/rust-lang/rfcs/blob/master/text/3307-de-rfc-type-ascription.md

## unnameable-types

The `unnameable_types` lint detects types for which you can get objects of that type,
but cannot name the type itself.

### Example

```rust,compile_fail
# #![feature(type_privacy_lints)]
# #![allow(unused)]
#![deny(unnameable_types)]
mod m {
    pub struct S;
}

pub fn get_unnameable() -> m::S { m::S }
# fn main() {}
```

This will produce:

```text
error: struct `S` is reachable but cannot be named
 --> lint_example.rs:5:5
  |
5 |     pub struct S;
  |     ^^^^^^^^^^^^ reachable at visibility `pub`, but can only be named at visibility `pub(crate)`
  |
note: the lint level is defined here
 --> lint_example.rs:3:9
  |
3 | #![deny(unnameable_types)]
  |         ^^^^^^^^^^^^^^^^

```

### Explanation

It is often expected that if you can obtain an object of type `T`, then
you can name the type `T` as well, this lint attempts to enforce this rule.

## unreachable-pub

The `unreachable_pub` lint triggers for `pub` items not reachable from
the crate root.

### Example

```rust,compile_fail
#![deny(unreachable_pub)]
mod foo {
    pub mod bar {

    }
}
```

This will produce:

```text
error: unreachable `pub` item
 --> lint_example.rs:4:5
  |
4 |     pub mod bar {
  |     ---^^^^^^^^
  |     |
  |     help: consider restricting its visibility: `pub(crate)`
  |
  = help: or consider exporting it for use by other crates
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(unreachable_pub)]
  |         ^^^^^^^^^^^^^^^

```

### Explanation

The `pub` keyword both expresses an intent for an item to be publicly available, and also
signals to the compiler to make the item publicly accessible. The intent can only be
satisfied, however, if all items which contain this item are *also* publicly accessible.
Thus, this lint serves to identify situations where the intent does not match the reality.

If you wish the item to be accessible elsewhere within the crate, but not outside it, the
`pub(crate)` visibility is recommended to be used instead. This more clearly expresses the
intent that the item is only visible within its own crate.

This lint is "allow" by default because it will trigger for a large
amount existing Rust code, and has some false-positives. Eventually it
is desired for this to become warn-by-default.

## unsafe-code

The `unsafe_code` lint catches usage of `unsafe` code and other
potentially unsound constructs like `no_mangle`, `export_name`,
and `link_section`.

### Example

```rust,compile_fail
#![deny(unsafe_code)]
fn main() {
    unsafe {

    }
}

#[no_mangle]
fn func_0() { }

#[export_name = "exported_symbol_name"]
pub fn name_in_rust() { }

#[no_mangle]
#[link_section = ".example_section"]
pub static VAR1: u32 = 1;
```

This will produce:

```text
error: usage of an `unsafe` block
 --> lint_example.rs:3:5
  |
3 | /     unsafe {
4 | |
5 | |     }
  | |_____^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(unsafe_code)]
  |         ^^^^^^^^^^^


error: declaration of a `no_mangle` function
 --> lint_example.rs:8:1
  |
8 | #[no_mangle]
  | ^^^^^^^^^^^^
  |
  = note: the linker's behavior with multiple libraries exporting duplicate symbol names is undefined and Rust cannot provide guarantees when you manually override them


error: declaration of a function with `export_name`
  --> lint_example.rs:11:1
   |
11 | #[export_name = "exported_symbol_name"]
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   |
   = note: the linker's behavior with multiple libraries exporting duplicate symbol names is undefined and Rust cannot provide guarantees when you manually override them


error: declaration of a `no_mangle` static
  --> lint_example.rs:14:1
   |
14 | #[no_mangle]
   | ^^^^^^^^^^^^
   |
   = note: the linker's behavior with multiple libraries exporting duplicate symbol names is undefined and Rust cannot provide guarantees when you manually override them


error: declaration of a static with `link_section`
  --> lint_example.rs:15:1
   |
15 | #[link_section = ".example_section"]
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   |
   = note: the program's behavior with overridden link sections on items is unpredictable and Rust cannot provide guarantees when you manually override them

```

### Explanation

This lint is intended to restrict the usage of `unsafe` blocks and other
constructs (including, but not limited to `no_mangle`, `link_section`
and `export_name` attributes) wrong usage of which causes undefined
behavior.

## unsafe-op-in-unsafe-fn

The `unsafe_op_in_unsafe_fn` lint detects unsafe operations in unsafe
functions without an explicit unsafe block.

### Example

```rust,compile_fail
#![deny(unsafe_op_in_unsafe_fn)]

unsafe fn foo() {}

unsafe fn bar() {
    foo();
}

fn main() {}
```

This will produce:

```text
error: call to unsafe function is unsafe and requires unsafe block (error E0133)
 --> lint_example.rs:6:5
  |
6 |     foo();
  |     ^^^^^ call to unsafe function
  |
  = note: consult the function's documentation for information on how to avoid undefined behavior
note: an unsafe function restricts its caller, but its body is safe by default
 --> lint_example.rs:5:1
  |
5 | unsafe fn bar() {
  | ^^^^^^^^^^^^^^^
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(unsafe_op_in_unsafe_fn)]
  |         ^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Currently, an [`unsafe fn`] allows any [unsafe] operation within its
body. However, this can increase the surface area of code that needs
to be scrutinized for proper behavior. The [`unsafe` block] provides a
convenient way to make it clear exactly which parts of the code are
performing unsafe operations. In the future, it is desired to change
it so that unsafe operations cannot be performed in an `unsafe fn`
without an `unsafe` block.

The fix to this is to wrap the unsafe code in an `unsafe` block.

This lint is "allow" by default on editions up to 2021, from 2024 it is
"warn" by default; the plan for increasing severity further is
still being considered. See [RFC #2585] and [issue #71668] for more
details.

[`unsafe fn`]: https://doc.rust-lang.org/reference/unsafe-functions.html
[`unsafe` block]: https://doc.rust-lang.org/reference/expressions/block-expr.html#unsafe-blocks
[unsafe]: https://doc.rust-lang.org/reference/unsafety.html
[RFC #2585]: https://github.com/rust-lang/rfcs/blob/master/text/2585-unsafe-block-in-unsafe-fn.md
[issue #71668]: https://github.com/rust-lang/rust/issues/71668

## unstable-features

The `unstable_features` is deprecated and should no longer be used.

## unused-crate-dependencies

The `unused_crate_dependencies` lint detects crate dependencies that
are never used.

### Example

```rust,ignore (needs extern crate)
#![deny(unused_crate_dependencies)]
```

This will produce:

```text
error: external crate `regex` unused in `lint_example`: remove the dependency or add `use regex as _;`
  |
note: the lint level is defined here
 --> src/lib.rs:1:9
  |
1 | #![deny(unused_crate_dependencies)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^
```

### Explanation

After removing the code that uses a dependency, this usually also
requires removing the dependency from the build configuration.
However, sometimes that step can be missed, which leads to time wasted
building dependencies that are no longer used. This lint can be
enabled to detect dependencies that are never used (more specifically,
any dependency passed with the `--extern` command-line flag that is
never referenced via [`use`], [`extern crate`], or in any [path]).

This lint is "allow" by default because it can provide false positives
depending on how the build system is configured. For example, when
using Cargo, a "package" consists of multiple crates (such as a
library and a binary), but the dependencies are defined for the
package as a whole. If there is a dependency that is only used in the
binary, but not the library, then the lint will be incorrectly issued
in the library.

[path]: https://doc.rust-lang.org/reference/paths.html
[`use`]: https://doc.rust-lang.org/reference/items/use-declarations.html
[`extern crate`]: https://doc.rust-lang.org/reference/items/extern-crates.html

## unused-extern-crates

The `unused_extern_crates` lint guards against `extern crate` items
that are never used.

### Example

```rust,compile_fail
#![deny(unused_extern_crates)]
#![deny(warnings)]
extern crate proc_macro;
```

This will produce:

```text
error: unused extern crate
 --> lint_example.rs:4:1
  |
4 | extern crate proc_macro;
  | ^^^^^^^^^^^^^^^^^^^^^^^^ help: remove it
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(unused_extern_crates)]
  |         ^^^^^^^^^^^^^^^^^^^^

```

### Explanation

`extern crate` items that are unused have no effect and should be
removed. Note that there are some cases where specifying an `extern
crate` is desired for the side effect of ensuring the given crate is
linked, even though it is not otherwise directly referenced. The lint
can be silenced by aliasing the crate to an underscore, such as
`extern crate foo as _`. Also note that it is no longer idiomatic to
use `extern crate` in the [2018 edition], as extern crates are now
automatically added in scope.

This lint is "allow" by default because it can be noisy, and produce
false-positives. If a dependency is being removed from a project, it
is recommended to remove it from the build configuration (such as
`Cargo.toml`) to ensure stale build entries aren't left behind.

[2018 edition]: https://doc.rust-lang.org/edition-guide/rust-2018/module-system/path-clarity.html#no-more-extern-crate

## unused-import-braces

The `unused_import_braces` lint catches unnecessary braces around an
imported item.

### Example

```rust,compile_fail
#![deny(unused_import_braces)]
use test::{A};

pub mod test {
    pub struct A;
}
# fn main() {}
```

This will produce:

```text
error: braces around A is unnecessary
 --> lint_example.rs:2:1
  |
2 | use test::{A};
  | ^^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(unused_import_braces)]
  |         ^^^^^^^^^^^^^^^^^^^^

```

### Explanation

If there is only a single item, then remove the braces (`use test::A;`
for example).

This lint is "allow" by default because it is only enforcing a
stylistic choice.

## unused-lifetimes

The `unused_lifetimes` lint detects lifetime parameters that are never
used.

### Example

```rust,compile_fail
#[deny(unused_lifetimes)]

pub fn foo<'a>() {}
```

This will produce:

```text
error: lifetime parameter `'a` never used
 --> lint_example.rs:4:12
  |
4 | pub fn foo<'a>() {}
  |           -^^- help: elide the unused lifetime
  |
note: the lint level is defined here
 --> lint_example.rs:2:8
  |
2 | #[deny(unused_lifetimes)]
  |        ^^^^^^^^^^^^^^^^

```

### Explanation

Unused lifetime parameters may signal a mistake or unfinished code.
Consider removing the parameter.

## unused-macro-rules

The `unused_macro_rules` lint detects macro rules that were not used.

Note that the lint is distinct from the `unused_macros` lint, which
fires if the entire macro is never called, while this lint fires for
single unused rules of the macro that is otherwise used.
`unused_macro_rules` fires only if `unused_macros` wouldn't fire.

### Example

```rust
#[warn(unused_macro_rules)]
macro_rules! unused_empty {
    (hello) => { println!("Hello, world!") }; // This rule is unused
    () => { println!("empty") }; // This rule is used
}

fn main() {
    unused_empty!(hello);
}
```

This will produce:

```text
warning: 2nd rule of macro `unused_empty` is never used
 --> lint_example.rs:4:5
  |
4 |     () => { println!("empty") }; // This rule is used
  |     ^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:8
  |
1 | #[warn(unused_macro_rules)]
  |        ^^^^^^^^^^^^^^^^^^

```

### Explanation

Unused macro rules may signal a mistake or unfinished code. Furthermore,
they slow down compilation. Right now, silencing the warning is not
supported on a single rule level, so you have to add an allow to the
entire macro definition.

If you intended to export the macro to make it
available outside of the crate, use the [`macro_export` attribute].

[`macro_export` attribute]: https://doc.rust-lang.org/reference/macros-by-example.html#path-based-scope

## unused-qualifications

The `unused_qualifications` lint detects unnecessarily qualified
names.

### Example

```rust,compile_fail
#![deny(unused_qualifications)]
mod foo {
    pub fn bar() {}
}

fn main() {
    use foo::bar;
    foo::bar();
}
```

This will produce:

```text
error: unnecessary qualification
 --> lint_example.rs:8:5
  |
8 |     foo::bar();
  |     ^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(unused_qualifications)]
  |         ^^^^^^^^^^^^^^^^^^^^^
help: remove the unnecessary path segments
  |
8 -     foo::bar();
8 +     bar();
  |

```

### Explanation

If an item from another module is already brought into scope, then
there is no need to qualify it in this case. You can call `bar()`
directly, without the `foo::`.

This lint is "allow" by default because it is somewhat pedantic, and
doesn't indicate an actual problem, but rather a stylistic choice, and
can be noisy when refactoring or moving around code.

## unused-results

The `unused_results` lint checks for the unused result of an
expression in a statement.

### Example

```rust,compile_fail
#![deny(unused_results)]
fn foo<T>() -> T { panic!() }

fn main() {
    foo::<usize>();
}
```

This will produce:

```text
error: unused result of type `usize`
 --> lint_example.rs:5:5
  |
5 |     foo::<usize>();
  |     ^^^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(unused_results)]
  |         ^^^^^^^^^^^^^^

```

### Explanation

Ignoring the return value of a function may indicate a mistake. In
cases were it is almost certain that the result should be used, it is
recommended to annotate the function with the [`must_use` attribute].
Failure to use such a return value will trigger the [`unused_must_use`
lint] which is warn-by-default. The `unused_results` lint is
essentially the same, but triggers for *all* return values.

This lint is "allow" by default because it can be noisy, and may not be
an actual problem. For example, calling the `remove` method of a `Vec`
or `HashMap` returns the previous value, which you may not care about.
Using this lint would require explicitly ignoring or discarding such
values.

[`must_use` attribute]: https://doc.rust-lang.org/reference/attributes/diagnostics.html#the-must_use-attribute
[`unused_must_use` lint]: warn-by-default.html#unused-must-use

## unused-tuple-struct-fields

The `unused_tuple_struct_fields` lint detects fields of tuple structs
that are never read.

### Example

```rust
#[warn(unused_tuple_struct_fields)]
struct S(i32, i32, i32);
let s = S(1, 2, 3);
let _ = (s.0, s.2);
```

This will produce:

```text
warning: field `1` is never read
 --> lint_example.rs:3:15
  |
3 | struct S(i32, i32, i32);
  |        -      ^^^
  |        |
  |        field in this struct
  |
note: the lint level is defined here
 --> lint_example.rs:2:8
  |
2 | #[warn(unused_tuple_struct_fields)]
  |        ^^^^^^^^^^^^^^^^^^^^^^^^^^
help: consider changing the field to be of unit type to suppress this warning while preserving the field numbering, or remove the field
  |
3 | struct S(i32, (), i32);
  |               ~~

```

### Explanation

Tuple struct fields that are never read anywhere may indicate a
mistake or unfinished code. To silence this warning, consider
removing the unused field(s) or, to preserve the numbering of the
remaining fields, change the unused field(s) to have unit type.

## variant-size-differences

The `variant_size_differences` lint detects enums with widely varying
variant sizes.

### Example

```rust,compile_fail
#![deny(variant_size_differences)]
enum En {
    V0(u8),
    VBig([u8; 1024]),
}
```

This will produce:

```text
error: enum variant is more than three times larger (1024 bytes) than the next largest
 --> lint_example.rs:5:5
  |
5 |     VBig([u8; 1024]),
  |     ^^^^^^^^^^^^^^^^
  |
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(variant_size_differences)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

It can be a mistake to add a variant to an enum that is much larger
than the other variants, bloating the overall size required for all
variants. This can impact performance and memory usage. This is
triggered if one variant is more than 3 times larger than the
second-largest variant.

Consider placing the large variant's contents on the heap (for example
via [`Box`]) to keep the overall size of the enum itself down.

This lint is "allow" by default because it can be noisy, and may not be
an actual problem. Decisions about this should be guided with
profiling and benchmarking.

[`Box`]: https://doc.rust-lang.org/std/boxed/index.html

