# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

**[Máté Szabó](https://github.com/mszabo-wikia) has managed to get HHVM@next to build! This PR can be found [here](https://github.com/facebook/hhvm/pull/9564). Thank you!**

_Typo here, typo there, typos everywhere._

## HHVM@next support is experimental

Thanks to the countless hours of work from [Máté Szabó](https://github.com/mszabo-wikia)
I managed to get my hands on a usable `hhvm@next` build. There are still some
quirks I need to fix, such as IDE support, but the basics are there. The
typechecker works, sort of, and I am able to run my test suites. I have made
many commits to all my open source projects, getting them into shape for
`hhvm@next`. This blog post is dedicated to experimental `hhvm@next` support.
If you are running into problems on `hhvm@next`, open issues. I intend to
switch to `hhvm@next` myself in the coming weeks.

### Actions runner

I run CI for all my projects on Github Actions. The CI used to be run on a
native Ubuntu 20.04 machine. This is no longer possible, since Github has [removed support for Ubuntu 20.04 runners](https://github.blog/changelog/2025-01-15-github-actions-ubuntu-20-runner-image-brownout-dates-and-other-breaking-changes/).
I have migrated htl/actions to support running in containers. This also means
that support for running outside of containers had to be removed. You are not
able to install hhvm on 22.04 using apt. I have switched to the docker images
built by Meta. If you want to run your actions in containers too, see
[this commit](https://github.com/hershel-theodore-layton/simple-web-token/commit/03f403de6a084e0418d03d9beccc19d8a3227b85).

The actions runner also supports a new `test_engine: test-chain`. The default
remains `test_engine: hacktest` in order to maintain stability for 
pre-existing non-HTL CI. You will have probably already seen that the tests
for the HTL projects have moved to test-chain.

### Dropping hhvm/hacktest and facebook/fbexpect

In order to support `hhvm@next`, all your dependencies, including `--dev`
dependencies, need to support `hhvm@next`. There are currently zero packages
in the `hhvm/x` and `facebook/x` namespaces that support `hhvm@next`. These
packages have been archived automatically and no community contributions will
be merged. This implies that moving forward requires leaving those packages
behind. I have already replaced `hhvm/hhast` with my own ast framework last
year, to make this moment easier. I have written `test-chain` and `expect` in
the last month as replacements for the last `hhvm/x` libraries.

### Keeping support for hhvm/hhvm-autoload

`hhvm version 4.102` does not support native autoloading, so dropping support
for userland autoloading would have required dropping support for this hhvm
version as well. I have managed to retain 100% compatibility for users who
depend on `hhvm/autoload` on `hhvm version 4.102+`. `hh_autoload.json` will
continue to be published until none of the supported hhvm versions can run
`hhvm-autoload`. In order to make `hhvm-autoload` truly optional, but still
support it for local development for HTL packages, some dynamic trickery was
required. If the `vendor/autoload.hack` file is present, I use [dynamic functions](https://docs.hhvm.com/hack/reference/function/HH.dynamic_fun/)
to call a function the typechecker cannot see. If you don't intent to use
`hhvm-autoload` in your local HTL development, remove `vendor/autoload.hack`.

### Keeping support for hadva

Hadva is the internal name for the difference between `varray<_>` and `vec<_>`.
It also determines the runtime representation of `tuple()` and `shape()`. In
my very first blogpost, I noted that I wouldn't perform magic to match hadva.

> One thing I will not do is jugling runtime types to make them match. So if
> your hhvm version has shapes represented by a darray, I'll not create a
> darray from a dict. Idem for tuples.

I have always kept basic hadva support, where the hhvm runtime was the cause
of the incompatible array type. This meant using `darray[]`, `darray()`,
`varray[]` and `varray()` constructs in places where older runtimes could not
deal with Hack arrays. These constructs have been removed from `hhvm@next`.
Hack does not support compile time `#if` macros, so I cannot do things like.

```CPP
// This is fiction in Hack
#if HHVM_VERSION_GTE_6_00_00
template<class Tk, class Tv>
auto d_array<Tk, Tv>(AnyArray<Tk, Tv> arr) -> dict<Tk, Tv> {
    return dict(arr);
}
#else
template<class Tk, class Tv>
auto d_array<Tk, Tv>(AnyArray<Tk, Tv> arr) -> darray<Tk, Tv> {
    return darray(arr);
}
#endif
```

I still needed to call `darray()` on `hhvm version 4.102` to support those
couple of edge cases. The solution, [hhvm-four-shim](https://github.com/hershel-theodore-layton/hhvm-four-shim).
This library uses `"requires": { "hhvm/hhvm": ">5" }` or `^4` clauses to
conflict with either `hhvm@next` or `hhvm 4.x`. These versions contain the
`#if` and `#else` variants of some common functions respectively. This means
that using `--ignore-platform-reqs` on `hhvm version 4.102` will install the
`hhvm@next` versions of these functions. If you rely on `--ignore-platform-reqs`, please pin `hhvm-four-shim` to `v0.4` in your repos.

## New libraries

[test-chain](https://github.com/hershel-theodore-layton/test-chain) and [expect](https://github.com/hershel-theodore-layton/expect) have
replaced `HackTest` and `fbexpect` in the `HTL\` family of packages. If you
want to use them, you can. They were written with `hhvm@next` compatibility
in mind. For example, `test-chain` uses codegen instead of runtime reflection
to find and invoke tests. This should mean that running tests in repo auth
mode can now work reliably. `expect` was written with coeffects and contexts
in mind. This means you can write tests in pure contexts.

## Breaking changes

A couple of breaking changes from `hhvm@next` had impact on `HTL\` packages.
`sgml-stream` and friends now require two entries in the `.hhconfig` file:

```INI
disable_xhp_element_mangling = true
enable_xhp_class_modifier = true
```

These settings used to default to `true`, but Meta uses them on `false`, so
they [reverted the change in 2024](https://github.com/facebook/hhvm/commit/c6db057c8eef2855552e94791696869e8cde4364).

In `portable-hack-ast` and friends, it is no longer possible to create a type
that passes for `NillableSyntax`, `NillableToken` and `NillableTrivium`. This
`_Private` type used to be the type of `Pha\\NIL`. In order to remain as
compatible as possible, the `NIL` constant still exists, but it has the type
of `NillableSyntax`. `NIL_SYNTAX`, `NIL_TOKEN`, and `NIL_TRIVIUM` have been
created if you need a specific nillable node.

## HHVM 4.102/4.128 unofficial support is ending

I will once again remind you that `hhvm version 4.102` is not part of the HTL
supported set of hhvm versions. As noted in the [January 2024](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2024-01.md)
blog post. I will make "a good faith effort" to support `hhvm version 4.102`,
if possible, and signal support in composer.json as long as the CI stays green.

When hhvm was still being released at a rapid rate, I dropped support a little
after Meta (then Facebook) did. For example, `hhvm version 4.80` support was
dropped in January of 2022, three months after Meta dropped support. Support
for `hhvm version 4.102` was [supposed to end on July 1st 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-03.md)
three months after Meta dropped support. I decided to keep those older versions
semi-supported for a while.

Life is too short for old software. Hadva workarounds only break in `HTL\`. The
only time I need to polyfill pure implementations of built-ins, is when coding
in `HTL\`. The only time I need to jump through hoops to do something as basic
as deleting a file programatically, is when supporting `4.102` in `HTL\`.
Because of this, so I have decided to pick a date to sunset the unofficial support for `hhvm version 4.102` and `hhvm version 4.128`. This date is 
September 1st 2025, or whenever `hhvm@next` requires syntax that is not
understood by these old hhvm version. Support for `hhvm version 4.128` will end
four years after its release. `hhvm version 4.153` and `hhvm version 4.168` 
will continue to be supported for a while, since upgrading to `hhvm@next` is
such a hassle.

## [March 2025](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2025-03.md)
## [January 2025](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2025-01.md)
## [November 2024](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2024-11.md)
## [September 2024](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2024-09.md)
## [July 2024](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2024-07.md)
## [May 2024](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2024-05.md)
## [March 2024](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2024-03.md)
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
