# Deny-by-default Lints

These lints are all set to the 'deny' level by default.

* [`ambiguous_associated_items`](#ambiguous-associated-items)
* [`arithmetic_overflow`](#arithmetic-overflow)
* [`bindings_with_variant_name`](#bindings-with-variant-name)
* [`cenum_impl_drop_cast`](#cenum-impl-drop-cast)
* [`coinductive_overlap_in_coherence`](#coinductive-overlap-in-coherence)
* [`conflicting_repr_hints`](#conflicting-repr-hints)
* [`deprecated_cfg_attr_crate_type_name`](#deprecated-cfg-attr-crate-type-name)
* [`enum_intrinsics_non_enums`](#enum-intrinsics-non-enums)
* [`ill_formed_attribute_input`](#ill-formed-attribute-input)
* [`implied_bounds_entailment`](#implied-bounds-entailment)
* [`incomplete_include`](#incomplete-include)
* [`ineffective_unstable_trait_impl`](#ineffective-unstable-trait-impl)
* [`invalid_atomic_ordering`](#invalid-atomic-ordering)
* [`invalid_from_utf8_unchecked`](#invalid-from-utf8-unchecked)
* [`invalid_reference_casting`](#invalid-reference-casting)
* [`invalid_type_param_default`](#invalid-type-param-default)
* [`let_underscore_lock`](#let-underscore-lock)
* [`long_running_const_eval`](#long-running-const-eval)
* [`macro_expanded_macro_exports_accessed_by_absolute_paths`](#macro-expanded-macro-exports-accessed-by-absolute-paths)
* [`missing_fragment_specifier`](#missing-fragment-specifier)
* [`mutable_transmutes`](#mutable-transmutes)
* [`named_asm_labels`](#named-asm-labels)
* [`no_mangle_const_items`](#no-mangle-const-items)
* [`order_dependent_trait_objects`](#order-dependent-trait-objects)
* [`overflowing_literals`](#overflowing-literals)
* [`patterns_in_fns_without_body`](#patterns-in-fns-without-body)
* [`proc_macro_back_compat`](#proc-macro-back-compat)
* [`proc_macro_derive_resolution_fallback`](#proc-macro-derive-resolution-fallback)
* [`pub_use_of_private_extern_crate`](#pub-use-of-private-extern-crate)
* [`soft_unstable`](#soft-unstable)
* [`test_unstable_lint`](#test-unstable-lint)
* [`text_direction_codepoint_in_comment`](#text-direction-codepoint-in-comment)
* [`text_direction_codepoint_in_literal`](#text-direction-codepoint-in-literal)
* [`unconditional_panic`](#unconditional-panic)
* [`undropped_manually_drops`](#undropped-manually-drops)
* [`unknown_crate_types`](#unknown-crate-types)
* [`useless_deprecated`](#useless-deprecated)

## ambiguous-associated-items

The `ambiguous_associated_items` lint detects ambiguity between
[associated items] and [enum variants].

[associated items]: https://doc.rust-lang.org/reference/items/associated-items.html
[enum variants]: https://doc.rust-lang.org/reference/items/enumerations.html

### Example

```rust,compile_fail
enum E {
    V
}

trait Tr {
    type V;
    fn foo() -> Self::V;
}

impl Tr for E {
    type V = u8;
    // `Self::V` is ambiguous because it may refer to the associated type or
    // the enum variant.
    fn foo() -> Self::V { 0 }
}
```

This will produce:

```text
error: ambiguous associated item
  --> lint_example.rs:15:17
   |
15 |     fn foo() -> Self::V { 0 }
   |                 ^^^^^^^ help: use fully-qualified syntax: `<E as Tr>::V`
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #57644 <https://github.com/rust-lang/rust/issues/57644>
note: `V` could refer to the variant defined here
  --> lint_example.rs:3:5
   |
3  |     V
   |     ^
note: `V` could also refer to the associated type defined here
  --> lint_example.rs:7:5
   |
7  |     type V;
   |     ^^^^^^
   = note: `#[deny(ambiguous_associated_items)]` on by default

```

### Explanation

Previous versions of Rust did not allow accessing enum variants
through [type aliases]. When this ability was added (see [RFC 2338]), this
introduced some situations where it can be ambiguous what a type
was referring to.

To fix this ambiguity, you should use a [qualified path] to explicitly
state which type to use. For example, in the above example the
function can be written as `fn f() -> <Self as Tr>::V { 0 }` to
specifically refer to the associated type.

This is a [future-incompatible] lint to transition this to a hard
error in the future. See [issue #57644] for more details.

[issue #57644]: https://github.com/rust-lang/rust/issues/57644
[type aliases]: https://doc.rust-lang.org/reference/items/type-aliases.html#type-aliases
[RFC 2338]: https://github.com/rust-lang/rfcs/blob/master/text/2338-type-alias-enum-variants.md
[qualified path]: https://doc.rust-lang.org/reference/paths.html#qualified-paths
[future-incompatible]: ../index.md#future-incompatible-lints

## arithmetic-overflow

The `arithmetic_overflow` lint detects that an arithmetic operation
will [overflow].

[overflow]: https://doc.rust-lang.org/reference/expressions/operator-expr.html#overflow

### Example

```rust,compile_fail
1_i32 << 32;
```

This will produce:

```text
error: this arithmetic operation will overflow
 --> lint_example.rs:2:1
  |
2 | 1_i32 << 32;
  | ^^^^^^^^^^^ attempt to shift left by `32_i32`, which would overflow
  |
  = note: `#[deny(arithmetic_overflow)]` on by default

```

### Explanation

It is very likely a mistake to perform an arithmetic operation that
overflows its value. If the compiler is able to detect these kinds of
overflows at compile-time, it will trigger this lint. Consider
adjusting the expression to avoid overflow, or use a data type that
will not overflow.

## bindings-with-variant-name

The `bindings_with_variant_name` lint detects pattern bindings with
the same name as one of the matched variants.

### Example

```rust,compile_fail
pub enum Enum {
    Foo,
    Bar,
}

pub fn foo(x: Enum) {
    match x {
        Foo => {}
        Bar => {}
    }
}
```

This will produce:

```text
error[E0170]: pattern binding `Foo` is named the same as one of the variants of the type `main::Enum`
 --> lint_example.rs:9:9
  |
9 |         Foo => {}
  |         ^^^ help: to match on the variant, qualify the path: `main::Enum::Foo`
  |
  = note: `#[deny(bindings_with_variant_name)]` on by default

```

### Explanation

It is usually a mistake to specify an enum variant name as an
[identifier pattern]. In the example above, the `match` arms are
specifying a variable name to bind the value of `x` to. The second arm
is ignored because the first one matches *all* values. The likely
intent is that the arm was intended to match on the enum variant.

Two possible solutions are:

* Specify the enum variant using a [path pattern], such as
  `Enum::Foo`.
* Bring the enum variants into local scope, such as adding `use
  Enum::*;` to the beginning of the `foo` function in the example
  above.

[identifier pattern]: https://doc.rust-lang.org/reference/patterns.html#identifier-patterns
[path pattern]: https://doc.rust-lang.org/reference/patterns.html#path-patterns

## cenum-impl-drop-cast

The `cenum_impl_drop_cast` lint detects an `as` cast of a field-less
`enum` that implements [`Drop`].

[`Drop`]: https://doc.rust-lang.org/std/ops/trait.Drop.html

### Example

```rust,compile_fail
# #![allow(unused)]
enum E {
    A,
}

impl Drop for E {
    fn drop(&mut self) {
        println!("Drop");
    }
}

fn main() {
    let e = E::A;
    let i = e as u32;
}
```

This will produce:

```text
error: cannot cast enum `E` into integer `u32` because it implements `Drop`
  --> lint_example.rs:14:13
   |
14 |     let i = e as u32;
   |             ^^^^^^^^
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #73333 <https://github.com/rust-lang/rust/issues/73333>
   = note: `#[deny(cenum_impl_drop_cast)]` on by default

```

### Explanation

Casting a field-less `enum` that does not implement [`Copy`] to an
integer moves the value without calling `drop`. This can result in
surprising behavior if it was expected that `drop` should be called.
Calling `drop` automatically would be inconsistent with other move
operations. Since neither behavior is clear or consistent, it was
decided that a cast of this nature will no longer be allowed.

This is a [future-incompatible] lint to transition this to a hard error
in the future. See [issue #73333] for more details.

[future-incompatible]: ../index.md#future-incompatible-lints
[issue #73333]: https://github.com/rust-lang/rust/issues/73333
[`Copy`]: https://doc.rust-lang.org/std/marker/trait.Copy.html

## coinductive-overlap-in-coherence

The `coinductive_overlap_in_coherence` lint detects impls which are currently
considered not overlapping, but may be considered to overlap if support for
coinduction is added to the trait solver.

### Example

```rust,compile_fail
#![deny(coinductive_overlap_in_coherence)]

trait CyclicTrait {}
impl<T: CyclicTrait> CyclicTrait for T {}

trait Trait {}
impl<T: CyclicTrait> Trait for T {}
// conflicting impl with the above
impl Trait for u8 {}
```

This will produce:

```text
error: implementations of `Trait` for `u8` will conflict in the future
  --> lint_example.rs:8:1
   |
8  | impl<T: CyclicTrait> Trait for T {}
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ the first impl is here
9  | // conflicting impl with the above
10 | impl Trait for u8 {}
   | ----------------- the second impl is here
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #114040 <https://github.com/rust-lang/rust/issues/114040>
   = note: impls that are not considered to overlap may be considered to overlap in the future
   = note: `u8: CyclicTrait` may be considered to hold in future releases, causing the impls to overlap
note: the lint level is defined here
  --> lint_example.rs:1:9
   |
1  | #![deny(coinductive_overlap_in_coherence)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

We have two choices for impl which satisfy `u8: Trait`: the blanket impl
for generic `T`, and the direct impl for `u8`. These two impls nominally
overlap, since we can infer `T = u8` in the former impl, but since the where
clause `u8: CyclicTrait` would end up resulting in a cycle (since it depends
on itself), the blanket impl is not considered to hold for `u8`. This will
change in a future release.

## conflicting-repr-hints

The `conflicting_repr_hints` lint detects [`repr` attributes] with
conflicting hints.

[`repr` attributes]: https://doc.rust-lang.org/reference/type-layout.html#representations

### Example

```rust,compile_fail
#[repr(u32, u64)]
enum Foo {
    Variant1,
}
```

This will produce:

```text
error[E0566]: conflicting representation hints
 --> lint_example.rs:2:8
  |
2 | #[repr(u32, u64)]
  |        ^^^  ^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #68585 <https://github.com/rust-lang/rust/issues/68585>
  = note: `#[deny(conflicting_repr_hints)]` on by default

```

### Explanation

The compiler incorrectly accepted these conflicting representations in
the past. This is a [future-incompatible] lint to transition this to a
hard error in the future. See [issue #68585] for more details.

To correct the issue, remove one of the conflicting hints.

[issue #68585]: https://github.com/rust-lang/rust/issues/68585
[future-incompatible]: ../index.md#future-incompatible-lints

## deprecated-cfg-attr-crate-type-name

The `deprecated_cfg_attr_crate_type_name` lint detects uses of the
`#![cfg_attr(..., crate_type = "...")]` and
`#![cfg_attr(..., crate_name = "...")]` attributes to conditionally
specify the crate type and name in the source code.

### Example

```rust,compile_fail
#![cfg_attr(debug_assertions, crate_type = "lib")]
```

This will produce:

```text
error: `crate_type` within an `#![cfg_attr] attribute is deprecated`
 --> lint_example.rs:1:31
  |
1 | #![cfg_attr(debug_assertions, crate_type = "lib")]
  |                               ^^^^^^^^^^^^^^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #91632 <https://github.com/rust-lang/rust/issues/91632>
  = note: `#[deny(deprecated_cfg_attr_crate_type_name)]` on by default

```


### Explanation

The `#![crate_type]` and `#![crate_name]` attributes require a hack in
the compiler to be able to change the used crate type and crate name
after macros have been expanded. Neither attribute works in combination
with Cargo as it explicitly passes `--crate-type` and `--crate-name` on
the commandline. These values must match the value used in the source
code to prevent an error.

To fix the warning use `--crate-type` on the commandline when running
rustc instead of `#![cfg_attr(..., crate_type = "...")]` and
`--crate-name` instead of `#![cfg_attr(..., crate_name = "...")]`.

## enum-intrinsics-non-enums

The `enum_intrinsics_non_enums` lint detects calls to
intrinsic functions that require an enum ([`core::mem::discriminant`],
[`core::mem::variant_count`]), but are called with a non-enum type.

[`core::mem::discriminant`]: https://doc.rust-lang.org/core/mem/fn.discriminant.html
[`core::mem::variant_count`]: https://doc.rust-lang.org/core/mem/fn.variant_count.html

### Example

```rust,compile_fail
#![deny(enum_intrinsics_non_enums)]
core::mem::discriminant::<i32>(&123);
```

This will produce:

```text
error: the return value of `mem::discriminant` is unspecified when called with a non-enum type
 --> lint_example.rs:3:1
  |
3 | core::mem::discriminant::<i32>(&123);
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
note: the argument to `discriminant` should be a reference to an enum, but it was passed a reference to a `i32`, which is not an enum.
 --> lint_example.rs:3:32
  |
3 | core::mem::discriminant::<i32>(&123);
  |                                ^^^^
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(enum_intrinsics_non_enums)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

In order to accept any enum, the `mem::discriminant` and
`mem::variant_count` functions are generic over a type `T`.
This makes it technically possible for `T` to be a non-enum,
in which case the return value is unspecified.

This lint prevents such incorrect usage of these functions.

## ill-formed-attribute-input

The `ill_formed_attribute_input` lint detects ill-formed attribute
inputs that were previously accepted and used in practice.

### Example

```rust,compile_fail
#[inline = "this is not valid"]
fn foo() {}
```

This will produce:

```text
error: attribute must be of the form `#[inline]` or `#[inline(always|never)]`
 --> lint_example.rs:2:1
  |
2 | #[inline = "this is not valid"]
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #57571 <https://github.com/rust-lang/rust/issues/57571>
  = note: `#[deny(ill_formed_attribute_input)]` on by default

```

### Explanation

Previously, inputs for many built-in attributes weren't validated and
nonsensical attribute inputs were accepted. After validation was
added, it was determined that some existing projects made use of these
invalid forms. This is a [future-incompatible] lint to transition this
to a hard error in the future. See [issue #57571] for more details.

Check the [attribute reference] for details on the valid inputs for
attributes.

[issue #57571]: https://github.com/rust-lang/rust/issues/57571
[attribute reference]: https://doc.rust-lang.org/nightly/reference/attributes.html
[future-incompatible]: ../index.md#future-incompatible-lints

## implied-bounds-entailment

The `implied_bounds_entailment` lint detects cases where the arguments of an impl method
have stronger implied bounds than those from the trait method it's implementing.

### Example

```rust,compile_fail
#![deny(implied_bounds_entailment)]

trait Trait {
    fn get<'s>(s: &'s str, _: &'static &'static ()) -> &'static str;
}

impl Trait for () {
    fn get<'s>(s: &'s str, _: &'static &'s ()) -> &'static str {
        s
    }
}

let val = <() as Trait>::get(&String::from("blah blah blah"), &&());
println!("{}", val);
```

This will produce:

```text
error: impl method assumes more implied bounds than the corresponding trait method
 --> lint_example.rs:9:31
  |
9 |     fn get<'s>(s: &'s str, _: &'static &'s ()) -> &'static str {
  |                               ^^^^^^^^^^^^^^^ help: replace this type to make the impl signature compatible: `&'static &'static ()`
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #105572 <https://github.com/rust-lang/rust/issues/105572>
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(implied_bounds_entailment)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^

```

### Explanation

Neither the trait method, which provides no implied bounds about `'s`, nor the impl,
requires the main function to prove that 's: 'static, but the impl method is allowed
to assume that `'s: 'static` within its own body.

This can be used to implement an unsound API if used incorrectly.

## incomplete-include

The `incomplete_include` lint detects the use of the [`include!`]
macro with a file that contains more than one expression.

[`include!`]: https://doc.rust-lang.org/std/macro.include.html

### Example

```rust,ignore (needs separate file)
fn main() {
    include!("foo.txt");
}
```

where the file `foo.txt` contains:

```text
println!("hi!");
```

produces:

```text
error: include macro expected single expression in source
 --> foo.txt:1:14
  |
1 | println!("1");
  |              ^
  |
  = note: `#[deny(incomplete_include)]` on by default
```

### Explanation

The [`include!`] macro is currently only intended to be used to
include a single [expression] or multiple [items]. Historically it
would ignore any contents after the first expression, but that can be
confusing. In the example above, the `println!` expression ends just
before the semicolon, making the semicolon "extra" information that is
ignored. Perhaps even more surprising, if the included file had
multiple print statements, the subsequent ones would be ignored!

One workaround is to place the contents in braces to create a [block
expression]. Also consider alternatives, like using functions to
encapsulate the expressions, or use [proc-macros].

This is a lint instead of a hard error because existing projects were
found to hit this error. To be cautious, it is a lint for now. The
future semantics of the `include!` macro are also uncertain, see
[issue #35560].

[items]: https://doc.rust-lang.org/reference/items.html
[expression]: https://doc.rust-lang.org/reference/expressions.html
[block expression]: https://doc.rust-lang.org/reference/expressions/block-expr.html
[proc-macros]: https://doc.rust-lang.org/reference/procedural-macros.html
[issue #35560]: https://github.com/rust-lang/rust/issues/35560

## ineffective-unstable-trait-impl

The `ineffective_unstable_trait_impl` lint detects `#[unstable]` attributes which are not used.

### Example

```rust,compile_fail
#![feature(staged_api)]

#[derive(Clone)]
#[stable(feature = "x", since = "1")]
struct S {}

#[unstable(feature = "y", issue = "none")]
impl Copy for S {}
```

This will produce:

```text
error: an `#[unstable]` annotation here has no effect
 --> lint_example.rs:8:1
  |
8 | #[unstable(feature = "y", issue = "none")]
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: see issue #55436 <https://github.com/rust-lang/rust/issues/55436> for more information
  = note: `#[deny(ineffective_unstable_trait_impl)]` on by default

```

### Explanation

`staged_api` does not currently support using a stability attribute on `impl` blocks.
`impl`s are always stable if both the type and trait are stable, and always unstable otherwise.

## invalid-atomic-ordering

The `invalid_atomic_ordering` lint detects passing an `Ordering`
to an atomic operation that does not support that ordering.

### Example

```rust,compile_fail
# use core::sync::atomic::{AtomicU8, Ordering};
let atom = AtomicU8::new(0);
let value = atom.load(Ordering::Release);
# let _ = value;
```

This will produce:

```text
error: atomic loads cannot have `Release` or `AcqRel` ordering
 --> lint_example.rs:4:23
  |
4 | let value = atom.load(Ordering::Release);
  |                       ^^^^^^^^^^^^^^^^^
  |
  = help: consider using ordering modes `Acquire`, `SeqCst` or `Relaxed`
  = note: `#[deny(invalid_atomic_ordering)]` on by default

```

### Explanation

Some atomic operations are only supported for a subset of the
`atomic::Ordering` variants. Passing an unsupported variant will cause
an unconditional panic at runtime, which is detected by this lint.

This lint will trigger in the following cases: (where `AtomicType` is an
atomic type from `core::sync::atomic`, such as `AtomicBool`,
`AtomicPtr`, `AtomicUsize`, or any of the other integer atomics).

- Passing `Ordering::Acquire` or `Ordering::AcqRel` to
  `AtomicType::store`.

- Passing `Ordering::Release` or `Ordering::AcqRel` to
  `AtomicType::load`.

- Passing `Ordering::Relaxed` to `core::sync::atomic::fence` or
  `core::sync::atomic::compiler_fence`.

- Passing `Ordering::Release` or `Ordering::AcqRel` as the failure
  ordering for any of `AtomicType::compare_exchange`,
  `AtomicType::compare_exchange_weak`, or `AtomicType::fetch_update`.

## invalid-from-utf8-unchecked

The `invalid_from_utf8_unchecked` lint checks for calls to
`std::str::from_utf8_unchecked` and `std::str::from_utf8_unchecked_mut`
with a known invalid UTF-8 value.

### Example

```rust,compile_fail
# #[allow(unused)]
unsafe {
    std::str::from_utf8_unchecked(b"Ru\x82st");
}
```

This will produce:

```text
error: calls to `std::str::from_utf8_unchecked` with a invalid literal are undefined behavior
 --> lint_example.rs:4:5
  |
4 |     std::str::from_utf8_unchecked(b"Ru\x82st");
  |     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^-----------^
  |                                   |
  |                                   the literal was valid UTF-8 up to the 2 bytes
  |
  = note: `#[deny(invalid_from_utf8_unchecked)]` on by default

```

### Explanation

Creating such a `str` would result in undefined behavior as per documentation
for `std::str::from_utf8_unchecked` and `std::str::from_utf8_unchecked_mut`.

## invalid-reference-casting

The `invalid_reference_casting` lint checks for casts of `&T` to `&mut T`
without using interior mutability.

### Example

```rust,compile_fail
fn x(r: &i32) {
    unsafe {
        *(r as *const i32 as *mut i32) += 1;
    }
}
```

This will produce:

```text
error: assigning to `&T` is undefined behavior, consider using an `UnsafeCell`
 --> lint_example.rs:4:9
  |
4 |         *(r as *const i32 as *mut i32) += 1;
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: for more information, visit <https://doc.rust-lang.org/book/ch15-05-interior-mutability.html>
  = note: `#[deny(invalid_reference_casting)]` on by default

```

### Explanation

Casting `&T` to `&mut T` without using interior mutability is undefined behavior,
as it's a violation of Rust reference aliasing requirements.

`UnsafeCell` is the only way to obtain aliasable data that is considered
mutable.

## invalid-type-param-default

The `invalid_type_param_default` lint detects type parameter defaults
erroneously allowed in an invalid location.

### Example

```rust,compile_fail
fn foo<T=i32>(t: T) {}
```

This will produce:

```text
error: defaults for type parameters are only allowed in `struct`, `enum`, `type`, or `trait` definitions
 --> lint_example.rs:2:8
  |
2 | fn foo<T=i32>(t: T) {}
  |        ^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #36887 <https://github.com/rust-lang/rust/issues/36887>
  = note: `#[deny(invalid_type_param_default)]` on by default

```

### Explanation

Default type parameters were only intended to be allowed in certain
situations, but historically the compiler allowed them everywhere.
This is a [future-incompatible] lint to transition this to a hard
error in the future. See [issue #36887] for more details.

[issue #36887]: https://github.com/rust-lang/rust/issues/36887
[future-incompatible]: ../index.md#future-incompatible-lints

## let-underscore-lock

The `let_underscore_lock` lint checks for statements which don't bind
a mutex to anything, causing the lock to be released immediately instead
of at end of scope, which is typically incorrect.

### Example
```rust,compile_fail
use std::sync::{Arc, Mutex};
use std::thread;
let data = Arc::new(Mutex::new(0));

thread::spawn(move || {
    // The lock is immediately released instead of at the end of the
    // scope, which is probably not intended.
    let _ = data.lock().unwrap();
    println!("doing some work");
    let mut lock = data.lock().unwrap();
    *lock += 1;
});
```

This will produce:

```text
error: non-binding let on a synchronization lock
 --> lint_example.rs:9:9
  |
9 |     let _ = data.lock().unwrap();
  |         ^   ^^^^^^^^^^^^^^^^^^^^ this binding will immediately drop the value assigned to it
  |         |
  |         this lock is not assigned to a binding and is immediately dropped
  |
  = note: `#[deny(let_underscore_lock)]` on by default
help: consider binding to an unused variable to avoid immediately dropping the value
  |
9 |     let _unused = data.lock().unwrap();
  |         ~~~~~~~
help: consider immediately dropping the value
  |
9 |     drop(data.lock().unwrap());
  |     ~~~~~                    +

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

## long-running-const-eval

The `long_running_const_eval` lint is emitted when const
eval is running for a long time to ensure rustc terminates
even if you accidentally wrote an infinite loop.

### Example

```rust,compile_fail
const FOO: () = loop {};
```

This will produce:

```text
error: constant evaluation is taking a long time
 --> lint_example.rs:2:17
  |
2 | const FOO: () = loop {};
  |                 ^^^^^^^
  |
  = note: this lint makes sure the compiler doesn't get stuck due to infinite loops in const eval.
          If your compilation actually takes a long time, you can safely allow the lint.
help: the constant being evaluated
 --> lint_example.rs:2:1
  |
2 | const FOO: () = loop {};
  | ^^^^^^^^^^^^^
  = note: `#[deny(long_running_const_eval)]` on by default

```

### Explanation

Loops allow const evaluation to compute arbitrary code, but may also
cause infinite loops or just very long running computations.
Users can enable long running computations by allowing the lint
on individual constants or for entire crates.

### Unconditional warnings

Note that regardless of whether the lint is allowed or set to warn,
the compiler will issue warnings if constant evaluation runs significantly
longer than this lint's limit. These warnings are also shown to downstream
users from crates.io or similar registries. If you are above the lint's limit,
both you and downstream users might be exposed to these warnings.
They might also appear on compiler updates, as the compiler makes minor changes
about how complexity is measured: staying below the limit ensures that there
is enough room, and given that the lint is disabled for people who use your
dependency it means you will be the only one to get the warning and can put
out an update in your own time.

## macro-expanded-macro-exports-accessed-by-absolute-paths

The `macro_expanded_macro_exports_accessed_by_absolute_paths` lint
detects macro-expanded [`macro_export`] macros from the current crate
that cannot be referred to by absolute paths.

[`macro_export`]: https://doc.rust-lang.org/reference/macros-by-example.html#path-based-scope

### Example

```rust,compile_fail
macro_rules! define_exported {
    () => {
        #[macro_export]
        macro_rules! exported {
            () => {};
        }
    };
}

define_exported!();

fn main() {
    crate::exported!();
}
```

This will produce:

```text
error: macro-expanded `macro_export` macros from the current crate cannot be referred to by absolute paths
  --> lint_example.rs:13:5
   |
13 |     crate::exported!();
   |     ^^^^^^^^^^^^^^^
   |
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #52234 <https://github.com/rust-lang/rust/issues/52234>
note: the macro is defined here
  --> lint_example.rs:4:9
   |
4  | /         macro_rules! exported {
5  | |             () => {};
6  | |         }
   | |_________^
...
10 |   define_exported!();
   |   ------------------ in this macro invocation
   = note: `#[deny(macro_expanded_macro_exports_accessed_by_absolute_paths)]` on by default
   = note: this error originates in the macro `define_exported` (in Nightly builds, run with -Z macro-backtrace for more info)

```

### Explanation

The intent is that all macros marked with the `#[macro_export]`
attribute are made available in the root of the crate. However, when a
`macro_rules!` definition is generated by another macro, the macro
expansion is unable to uphold this rule. This is a
[future-incompatible] lint to transition this to a hard error in the
future. See [issue #53495] for more details.

[issue #53495]: https://github.com/rust-lang/rust/issues/53495
[future-incompatible]: ../index.md#future-incompatible-lints

## missing-fragment-specifier

The `missing_fragment_specifier` lint is issued when an unused pattern in a
`macro_rules!` macro definition has a meta-variable (e.g. `$e`) that is not
followed by a fragment specifier (e.g. `:expr`).

This warning can always be fixed by removing the unused pattern in the
`macro_rules!` macro definition.

### Example

```rust,compile_fail
macro_rules! foo {
   () => {};
   ($name) => { };
}

fn main() {
   foo!();
}
```

This will produce:

```text
error: missing fragment specifier
 --> lint_example.rs:3:5
  |
3 |    ($name) => { };
  |     ^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #40107 <https://github.com/rust-lang/rust/issues/40107>
  = note: `#[deny(missing_fragment_specifier)]` on by default

```

### Explanation

To fix this, remove the unused pattern from the `macro_rules!` macro definition:

```rust
macro_rules! foo {
    () => {};
}
fn main() {
    foo!();
}
```

## mutable-transmutes

The `mutable_transmutes` lint catches transmuting from `&T` to `&mut
T` because it is [undefined behavior].

[undefined behavior]: https://doc.rust-lang.org/reference/behavior-considered-undefined.html

### Example

```rust,compile_fail
unsafe {
    let y = std::mem::transmute::<&i32, &mut i32>(&5);
}
```

This will produce:

```text
error: transmuting &T to &mut T is undefined behavior, even if the reference is unused, consider instead using an UnsafeCell
 --> lint_example.rs:3:13
  |
3 |     let y = std::mem::transmute::<&i32, &mut i32>(&5);
  |             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[deny(mutable_transmutes)]` on by default

```

### Explanation

Certain assumptions are made about aliasing of data, and this transmute
violates those assumptions. Consider using [`UnsafeCell`] instead.

[`UnsafeCell`]: https://doc.rust-lang.org/std/cell/struct.UnsafeCell.html

## named-asm-labels

The `named_asm_labels` lint detects the use of named labels in the
inline `asm!` macro.

### Example

```rust,compile_fail
# #![feature(asm_experimental_arch)]
use std::arch::asm;

fn main() {
    unsafe {
        asm!("foo: bar");
    }
}
```

This will produce:

```text
error: avoid using named labels in inline assembly
 --> lint_example.rs:6:15
  |
6 |         asm!("foo: bar");
  |               ^^^
  |
  = help: only local labels of the form `<number>:` should be used in inline asm
  = note: see the asm section of Rust By Example <https://doc.rust-lang.org/nightly/rust-by-example/unsafe/asm.html#labels> for more information
  = note: `#[deny(named_asm_labels)]` on by default

```

### Explanation

LLVM is allowed to duplicate inline assembly blocks for any
reason, for example when it is in a function that gets inlined. Because
of this, GNU assembler [local labels] *must* be used instead of labels
with a name. Using named labels might cause assembler or linker errors.

See the explanation in [Rust By Example] for more details.

[local labels]: https://sourceware.org/binutils/docs/as/Symbol-Names.html#Local-Labels
[Rust By Example]: https://doc.rust-lang.org/nightly/rust-by-example/unsafe/asm.html#labels

## no-mangle-const-items

The `no_mangle_const_items` lint detects any `const` items with the
[`no_mangle` attribute].

[`no_mangle` attribute]: https://doc.rust-lang.org/reference/abi.html#the-no_mangle-attribute

### Example

```rust,compile_fail
#[no_mangle]
const FOO: i32 = 5;
```

This will produce:

```text
error: const items should never be `#[no_mangle]`
 --> lint_example.rs:3:1
  |
3 | const FOO: i32 = 5;
  | -----^^^^^^^^^^^^^^
  | |
  | help: try a static value: `pub static`
  |
  = note: `#[deny(no_mangle_const_items)]` on by default

```

### Explanation

Constants do not have their symbols exported, and therefore, this
probably means you meant to use a [`static`], not a [`const`].

[`static`]: https://doc.rust-lang.org/reference/items/static-items.html
[`const`]: https://doc.rust-lang.org/reference/items/constant-items.html

## order-dependent-trait-objects

The `order_dependent_trait_objects` lint detects a trait coherency
violation that would allow creating two trait impls for the same
dynamic trait object involving marker traits.

### Example

```rust,compile_fail
pub trait Trait {}

impl Trait for dyn Send + Sync { }
impl Trait for dyn Sync + Send { }
```

This will produce:

```text
error: conflicting implementations of trait `Trait` for type `(dyn Send + Sync + 'static)`: (E0119)
 --> lint_example.rs:5:1
  |
4 | impl Trait for dyn Send + Sync { }
  | ------------------------------ first implementation here
5 | impl Trait for dyn Sync + Send { }
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ conflicting implementation for `(dyn Send + Sync + 'static)`
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #56484 <https://github.com/rust-lang/rust/issues/56484>
  = note: `#[deny(order_dependent_trait_objects)]` on by default

```

### Explanation

A previous bug caused the compiler to interpret traits with different
orders (such as `Send + Sync` and `Sync + Send`) as distinct types
when they were intended to be treated the same. This allowed code to
define separate trait implementations when there should be a coherence
error. This is a [future-incompatible] lint to transition this to a
hard error in the future. See [issue #56484] for more details.

[issue #56484]: https://github.com/rust-lang/rust/issues/56484
[future-incompatible]: ../index.md#future-incompatible-lints

## overflowing-literals

The `overflowing_literals` lint detects literal out of range for its
type.

### Example

```rust,compile_fail
let x: u8 = 1000;
```

This will produce:

```text
error: literal out of range for `u8`
 --> lint_example.rs:2:13
  |
2 | let x: u8 = 1000;
  |             ^^^^
  |
  = note: the literal `1000` does not fit into the type `u8` whose range is `0..=255`
  = note: `#[deny(overflowing_literals)]` on by default

```

### Explanation

It is usually a mistake to use a literal that overflows the type where
it is used. Either use a literal that is within range, or change the
type to be within the range of the literal.

## patterns-in-fns-without-body

The `patterns_in_fns_without_body` lint detects `mut` identifier
patterns as a parameter in functions without a body.

### Example

```rust,compile_fail
trait Trait {
    fn foo(mut arg: u8);
}
```

This will produce:

```text
error: patterns aren't allowed in functions without bodies
 --> lint_example.rs:3:12
  |
3 |     fn foo(mut arg: u8);
  |            ^^^^^^^ help: remove `mut` from the parameter: `arg`
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #35203 <https://github.com/rust-lang/rust/issues/35203>
  = note: `#[deny(patterns_in_fns_without_body)]` on by default

```

### Explanation

To fix this, remove `mut` from the parameter in the trait definition;
it can be used in the implementation. That is, the following is OK:

```rust
trait Trait {
    fn foo(arg: u8); // Removed `mut` here
}

impl Trait for i32 {
    fn foo(mut arg: u8) { // `mut` here is OK

    }
}
```

Trait definitions can define functions without a body to specify a
function that implementors must define. The parameter names in the
body-less functions are only allowed to be `_` or an [identifier] for
documentation purposes (only the type is relevant). Previous versions
of the compiler erroneously allowed [identifier patterns] with the
`mut` keyword, but this was not intended to be allowed. This is a
[future-incompatible] lint to transition this to a hard error in the
future. See [issue #35203] for more details.

[identifier]: https://doc.rust-lang.org/reference/identifiers.html
[identifier patterns]: https://doc.rust-lang.org/reference/patterns.html#identifier-patterns
[issue #35203]: https://github.com/rust-lang/rust/issues/35203
[future-incompatible]: ../index.md#future-incompatible-lints

## proc-macro-back-compat

The `proc_macro_back_compat` lint detects uses of old versions of certain
proc-macro crates, which have hardcoded workarounds in the compiler.

### Example

```rust,ignore (needs-dependency)

use time_macros_impl::impl_macros;
struct Foo;
impl_macros!(Foo);
```

This will produce:

```text
warning: using an old version of `time-macros-impl`
  ::: $DIR/group-compat-hack.rs:27:5
   |
LL |     impl_macros!(Foo);
   |     ------------------ in this macro invocation
   |
   = note: `#[warn(proc_macro_back_compat)]` on by default
   = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
   = note: for more information, see issue #83125 <https://github.com/rust-lang/rust/issues/83125>
   = note: the `time-macros-impl` crate will stop compiling in futures version of Rust. Please update to the latest version of the `time` crate to avoid breakage
   = note: this warning originates in a macro (in Nightly builds, run with -Z macro-backtrace for more info)
```

### Explanation

Eventually, the backwards-compatibility hacks present in the compiler will be removed,
causing older versions of certain crates to stop compiling.
This is a [future-incompatible] lint to ease the transition to an error.
See [issue #83125] for more details.

[issue #83125]: https://github.com/rust-lang/rust/issues/83125
[future-incompatible]: ../index.md#future-incompatible-lints

## proc-macro-derive-resolution-fallback

The `proc_macro_derive_resolution_fallback` lint detects proc macro
derives using inaccessible names from parent modules.

### Example

```rust,ignore (proc-macro)
// foo.rs
#![crate_type = "proc-macro"]

extern crate proc_macro;

use proc_macro::*;

#[proc_macro_derive(Foo)]
pub fn foo1(a: TokenStream) -> TokenStream {
    drop(a);
    "mod __bar { static mut BAR: Option<Something> = None; }".parse().unwrap()
}
```

```rust,ignore (needs-dependency)
// bar.rs
#[macro_use]
extern crate foo;

struct Something;

#[derive(Foo)]
struct Another;

fn main() {}
```

This will produce:

```text
warning: cannot find type `Something` in this scope
 --> src/main.rs:8:10
  |
8 | #[derive(Foo)]
  |          ^^^ names from parent modules are not accessible without an explicit import
  |
  = note: `#[warn(proc_macro_derive_resolution_fallback)]` on by default
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #50504 <https://github.com/rust-lang/rust/issues/50504>
```

### Explanation

If a proc-macro generates a module, the compiler unintentionally
allowed items in that module to refer to items in the crate root
without importing them. This is a [future-incompatible] lint to
transition this to a hard error in the future. See [issue #50504] for
more details.

[issue #50504]: https://github.com/rust-lang/rust/issues/50504
[future-incompatible]: ../index.md#future-incompatible-lints

## pub-use-of-private-extern-crate

The `pub_use_of_private_extern_crate` lint detects a specific
situation of re-exporting a private `extern crate`.

### Example

```rust,compile_fail
extern crate core;
pub use core as reexported_core;
```

This will produce:

```text
error: extern crate `core` is private, and cannot be re-exported (error E0365), consider declaring with `pub`
 --> lint_example.rs:3:9
  |
3 | pub use core as reexported_core;
  |         ^^^^^^^^^^^^^^^^^^^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #34537 <https://github.com/rust-lang/rust/issues/34537>
  = note: `#[deny(pub_use_of_private_extern_crate)]` on by default

```

### Explanation

A public `use` declaration should not be used to publicly re-export a
private `extern crate`. `pub extern crate` should be used instead.

This was historically allowed, but is not the intended behavior
according to the visibility rules. This is a [future-incompatible]
lint to transition this to a hard error in the future. See [issue
#34537] for more details.

[issue #34537]: https://github.com/rust-lang/rust/issues/34537
[future-incompatible]: ../index.md#future-incompatible-lints

## soft-unstable

The `soft_unstable` lint detects unstable features that were
unintentionally allowed on stable.

### Example

```rust,compile_fail
#[cfg(test)]
extern crate test;

#[bench]
fn name(b: &mut test::Bencher) {
    b.iter(|| 123)
}
```

This will produce:

```text
error: use of unstable library feature 'test': `bench` is a part of custom test frameworks which are unstable
 --> lint_example.rs:5:3
  |
5 | #[bench]
  |   ^^^^^
  |
  = warning: this was previously accepted by the compiler but is being phased out; it will become a hard error in a future release!
  = note: for more information, see issue #64266 <https://github.com/rust-lang/rust/issues/64266>
  = note: `#[deny(soft_unstable)]` on by default

```

### Explanation

The [`bench` attribute] was accidentally allowed to be specified on
the [stable release channel]. Turning this to a hard error would have
broken some projects. This lint allows those projects to continue to
build correctly when [`--cap-lints`] is used, but otherwise signal an
error that `#[bench]` should not be used on the stable channel. This
is a [future-incompatible] lint to transition this to a hard error in
the future. See [issue #64266] for more details.

[issue #64266]: https://github.com/rust-lang/rust/issues/64266
[`bench` attribute]: https://doc.rust-lang.org/nightly/unstable-book/library-features/test.html
[stable release channel]: https://doc.rust-lang.org/book/appendix-07-nightly-rust.html
[`--cap-lints`]: https://doc.rust-lang.org/rustc/lints/levels.html#capping-lints
[future-incompatible]: ../index.md#future-incompatible-lints

## test-unstable-lint

The `test_unstable_lint` lint tests unstable lints and is perma-unstable.

### Example

```rust
#![allow(test_unstable_lint)]
```

This will produce:

```text
warning: unknown lint: `test_unstable_lint`
 --> lint_example.rs:1:1
  |
1 | #![allow(test_unstable_lint)]
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: the `test_unstable_lint` lint is unstable
  = help: add `#![feature(test_unstable_lint)]` to the crate attributes to enable
  = note: `#[warn(unknown_lints)]` on by default

```

### Explanation

In order to test the behavior of unstable lints, a permanently-unstable
lint is required. This lint can be used to trigger warnings and errors
from the compiler related to unstable lints.

## text-direction-codepoint-in-comment

The `text_direction_codepoint_in_comment` lint detects Unicode codepoints in comments that
change the visual representation of text on screen in a way that does not correspond to
their on memory representation.

### Example

```rust,compile_fail
#![deny(text_direction_codepoint_in_comment)]
fn main() {
    println!("{:?}"); // '‮');
}
```

This will produce:

```text
error: unicode codepoint changing visible direction of text present in comment
 --> lint_example.rs:3:23
  |
3 |     println!("{:?}"); // '');
  |                       ^^^^-^^
  |                       |   |
  |                       |   '\u{202e}'
  |                       this comment contains an invisible unicode text flow control codepoint
  |
  = note: these kind of unicode codepoints change the way text flows on applications that support them, but can cause confusion because they change the order of characters on the screen
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(text_direction_codepoint_in_comment)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  = help: if their presence wasn't intentional, you can remove them

```

### Explanation

Unicode allows changing the visual flow of text on screen in order to support scripts that
are written right-to-left, but a specially crafted comment can make code that will be
compiled appear to be part of a comment, depending on the software used to read the code.
To avoid potential problems or confusion, such as in CVE-2021-42574, by default we deny
their use.

## text-direction-codepoint-in-literal

The `text_direction_codepoint_in_literal` lint detects Unicode codepoints that change the
visual representation of text on screen in a way that does not correspond to their on
memory representation.

### Explanation

The unicode characters `\u{202A}`, `\u{202B}`, `\u{202D}`, `\u{202E}`, `\u{2066}`,
`\u{2067}`, `\u{2068}`, `\u{202C}` and `\u{2069}` make the flow of text on screen change
its direction on software that supports these codepoints. This makes the text "abc" display
as "cba" on screen. By leveraging software that supports these, people can write specially
crafted literals that make the surrounding code seem like it's performing one action, when
in reality it is performing another. Because of this, we proactively lint against their
presence to avoid surprises.

### Example

```rust,compile_fail
#![deny(text_direction_codepoint_in_literal)]
fn main() {
    println!("{:?}", '‮');
}
```

This will produce:

```text
error: unicode codepoint changing visible direction of text present in literal
 --> lint_example.rs:3:22
  |
3 |     println!("{:?}", '');
  |                      ^-
  |                      ||
  |                      |'\u{202e}'
  |                      this literal contains an invisible unicode text flow control codepoint
  |
  = note: these kind of unicode codepoints change the way text flows on applications that support them, but can cause confusion because they change the order of characters on the screen
note: the lint level is defined here
 --> lint_example.rs:1:9
  |
1 | #![deny(text_direction_codepoint_in_literal)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  = help: if their presence wasn't intentional, you can remove them
help: if you want to keep them but make them visible in your source code, you can escape them
  |
3 |     println!("{:?}", '\u{202e}');
  |                       ~~~~~~~~

```


## unconditional-panic

The `unconditional_panic` lint detects an operation that will cause a
panic at runtime.

### Example

```rust,compile_fail
# #![allow(unused)]
let x = 1 / 0;
```

This will produce:

```text
error: this operation will panic at runtime
 --> lint_example.rs:3:9
  |
3 | let x = 1 / 0;
  |         ^^^^^ attempt to divide `1_i32` by zero
  |
  = note: `#[deny(unconditional_panic)]` on by default

```

### Explanation

This lint detects code that is very likely incorrect because it will
always panic, such as division by zero and out-of-bounds array
accesses. Consider adjusting your code if this is a bug, or using the
`panic!` or `unreachable!` macro instead in case the panic is intended.

## undropped-manually-drops

The `undropped_manually_drops` lint check for calls to `std::mem::drop` with
a value of `std::mem::ManuallyDrop` which doesn't drop.

### Example

```rust,compile_fail
struct S;
drop(std::mem::ManuallyDrop::new(S));
```

This will produce:

```text
error: calls to `std::mem::drop` with `std::mem::ManuallyDrop` instead of the inner value does nothing
 --> lint_example.rs:3:1
  |
3 | drop(std::mem::ManuallyDrop::new(S));
  | ^^^^^------------------------------^
  |      |
  |      argument has type `ManuallyDrop<S>`
  |
  = note: `#[deny(undropped_manually_drops)]` on by default
help: use `std::mem::ManuallyDrop::into_inner` to get the inner value
  |
3 | drop(std::mem::ManuallyDrop::into_inner(std::mem::ManuallyDrop::new(S)));
  |      +++++++++++++++++++++++++++++++++++                              +

```

### Explanation

`ManuallyDrop` does not drop it's inner value so calling `std::mem::drop` will
not drop the inner value of the `ManuallyDrop` either.

## unknown-crate-types

The `unknown_crate_types` lint detects an unknown crate type found in
a [`crate_type` attribute].

### Example

```rust,compile_fail
#![crate_type="lol"]
fn main() {}
```

This will produce:

```text
error: invalid `crate_type` value
 --> lint_example.rs:1:15
  |
1 | #![crate_type="lol"]
  |               ^^^^^
  |
  = note: `#[deny(unknown_crate_types)]` on by default

```

### Explanation

An unknown value give to the `crate_type` attribute is almost
certainly a mistake.

[`crate_type` attribute]: https://doc.rust-lang.org/reference/linkage.html

## useless-deprecated

The `useless_deprecated` lint detects deprecation attributes with no effect.

### Example

```rust,compile_fail
struct X;

#[deprecated = "message"]
impl Default for X {
    fn default() -> Self {
        X
    }
}
```

This will produce:

```text
error: this `#[deprecated]` annotation has no effect
 --> lint_example.rs:4:1
  |
4 | #[deprecated = "message"]
  | ^^^^^^^^^^^^^^^^^^^^^^^^^ help: remove the unnecessary deprecation attribute
  |
  = note: `#[deny(useless_deprecated)]` on by default

```

### Explanation

Deprecation attributes have no effect on trait implementations.

