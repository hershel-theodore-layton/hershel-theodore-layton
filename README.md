# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

_Typo here, typo there, typos everywhere._

## March 2024

### New library released

This time last month, [expr-dump](https://github.com/hershel-theodore-layton/expr-dump) was released as `v0.2`.

This library takes a typed runtime value and returns the Hack code required to recreate this runtime value as a well-typed expression.

_Isn't that just `\var_export_pure()`?_

No, `\var_export_pure()` doesn't understand Hack's typesystem. Newtypes, enums, tuples, and shapes get type erased at runtime.
`ExprDump\dump<T>(...)` takes a `T`, so it can faithfully recreate the value and the Hack type.

```HACK
function burn_a_value_to_constant<reify T>(
  string $constant_name,
  T $value,
  ExprDump\DumpOptions $dumper_options = shape(),
)[]: string {
  $type_name = TypeVisitor\visit<T, _, _>(new TypeVisitor\TypenameVisitor());
  $serialized_value = ExprDump\dump<T>($value, $dumper_options);
  return Str\format(
    'const %s %s = %s;',
    $type_name,
    $constant_name,
    $serialized_value,
  );
}
```

### Upcoming SGMLStream change

The signature of `RootElement->init()` will be annotated with a context in a future release.
This will make most xhp element creation expressions pure.
If you have never heard of `init()`, you are not affected and can stop reading right now.
`init()` is the method called at the last line of the `RootElement` constructor.
It is a user customization point to run extra validation after the element has been constructed.

For what it is worth, I don't depend on `init()` at all.
`init()` is/was part of the `Node` api found in [xhp-lib](https://github.com/hhvm/xhp-lib/blob/4ec138f7ac9ef6d2eb646075799860459d3fb0d4/src/core/Node.hack#L91).
It was retained so users of xhp-lib that did use it could continue to use it after switching libraries
.
Reason for this proposed change:
The `RootElement` constructor can not be made pure, since it calls `$this->init()` and `init()` requires `[deafults]`.
Because of this reason, any xhp element construction requires `[defaults]`.
This is a shame, since returning an xhp element from a pure method is something you should be able to do.

Proposed API change:
`protected function init()[this::CTX]: void {}` would replace `[defaults]`.
`this::CTX` would be abstract at the level of `RootElement`.
This would impose a breaking change on every existing subclass.
They don't implement `abstract const ctx CTX;`.

Since I don't expect that the majority of your elements implement `init()`,
the built-in element types will include `const ctx CTX = [];`
This means that all elements that don't implement `init()` are not affected.
The same hold true for elements that implemented `init()[]` (with a pure context).
If you want an impure `init()`, you must subclass `RootElement` yourself.

- v0
  - AsynchronousUserElement
  - AsynchronousUserElementWithWritableFlow
  - DissolvableUserElement
  - SimpleUserElement
  - SimpleUserElementWithWritableFlow
- v1
  - AsynchronousElement
  - AsynchronousElementWithSuccessorFlow
  - AsynchronousElementWithWritableFlow
  - DissolvableElement
  - SimpleElement
  - SimpleElementWithWritableFlow
 
I am looking forward to pure xhp element creation.

Streaming an element will always remain `[defaults]`, since `Consumer` need to do IO.

## [January 2024](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2024-01.md)
## [November 2023](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2023-11.md)
## [September 2023](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2023-09.md)
## [July 2023](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2023-07.md)
## [May 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-05.md)
## [March 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-03.md)
## [January 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-01.md)
## [SGMLStream Sillimanite Release](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-release-announcement-sgml-stream-sillimanite.md)
## [November 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md)
## [September 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-09.md)
## [July 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md)
