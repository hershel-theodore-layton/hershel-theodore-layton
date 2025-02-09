# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

**[Máté Szabó](https://github.com/mszabo-wikia) has managed to get HHVM@next to build! This PR can be found [here](https://github.com/facebook/hhvm/pull/9564). Thank you!**

_Typo here, typo there, typos everywhere._

## HHVM News!

HHVM@next just came a lot closer. [Máté Szabó](https://github.com/mszabo-wikia) has got a branch of hhvm@next which builds. A couple of features had to be disabled, such as AsyncMySQL. Hopefully these issues can be resolved. I am looking forward to the day that hhvm@master:HEAD can be built.

I have checked, and many facebook/x and hhvm/x projects do not work anymore on this branch. HackTest (a dependency of a lot of projects) does not typecheck and throws an error before running tests. It looks like facebook/x and hhvm/x will remain `hhvm version 4.172` compatible, but `hhvm@next` support will likely not come any time soon. The HTL family of packages stands on the shoulders of facebook/x and hhvm/x. An effort has been made to replace hard to replace components, such as hhast, last year. It has become clear that this effort must be completed sooner, rather than later. I will have to remove the `hhvm/hhvm-autoload`, `hhvm/hacktest`, and `facebook/fbexpect` dependencies.

 - hhvm-autoload will probably be the easiest. On hhvm 4.128 and above, I depend on ext_watchman for autoloading. I will continue to publish `hh_autoload.json` for users on `hhvm version 4.102` and continue to test on this version as well.
 - `facebook/fbexpect` is a rather easy dependency to remove. I intend to follow the design from fbexpect `expect(<actual>)->to<expectation>(<expected value>)`. I will implement the required expectations to test the HTL family of packages, and leave the others as an excercise for the reader.
 - `hhvm/hacktest` will be more difficult to replace. It depends on reflection and dynamic invocations of your test methods. I am considering breaking compatibility with existing tests in order to ditch the dependency on reflection.

## New linters

`context_list_must_be_explicit_on_io_functions_linter` is a less agressive version of `context_list_must_be_explicit_linter`, which only flags functions with the `await` keyword. These functions are almost always `[defaults]`. The included autofix will normalize the use of context lists in your codebases.

## Support for larger codegen

When generating a lot of code on a single line, `hackfmt` can hang for a long time. `type-visitor`, `expr-dump`, and `static-type-assertion-codegen` now insert some newlines to aid hackfmt.

## FormatCodegen, SqlFormat, and SqlFormatCodegen

In [the September 2024 post](./2024-09.md) I noted that I was experimenting with open sourcing my format string builder. The implementation has been overhauled to keep the `format_d()` interfaces and the implementation the same. Previously, you'd have had to make each change in two places. The idea to codegen the interfaces made this less error prone. The thought, why keep the runtime code this needlessly dynamic, crossed my mind. _You can not add new specifiers at runtime, since the interfaces only change at codegen time._ So the runtime implementation is now also codegenned. I am holding off on releasing these libraries, until I have a hacktest replacement ready.

 - FormatCodegen (dev-only), create your own format specifier interfaces and runtime component from a convinient factory.
 - SqlFormat, render `HipHopLibSqlQueryPack` objects to strings for debug purposes.
 - SqlFormatCodegen (dev-only), build your own `QueryPack` to `HipHopLibSqlQueryPack` converter. Add support for your own types and change the grammar to include the features you want.

<sup>The feeling when the January blog post is made in the second week of February.</sup>

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
