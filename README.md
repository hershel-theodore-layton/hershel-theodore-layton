# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

_Typo here, typo there, typos everywhere._

### Linting improvements

The latest version [Gold - patch 1](https://github.com/hershel-theodore-layton/dead-simple-lint-server-integration/releases/tag/v1.0.1)
of the vscode extension [DeadSimpleLintServerIntegration](https://github.com/hershel-theodore-a=layton/dead-simple-lint-server-integration)
uses 50% less CPU than the previous version. The extension would lint file on change
and when the IDE internals requests diagnostics to be refreshed. The former is completely
redundant. Every key press ran the analysis twice, which is a waste of resources.
May this change improve the battery life of your laptop.

The latest version [Ho, Ho, Ho - patch 6](https://github.com/hershel-theodore-layton/portable-hack-ast-linters/releases/tag/v0.0.6)
of [PhaLinters](https://github.com/hershel-theodore-layton/portable-hack-ast-linters) includes a utility to
add a digest to generated code. This feature is very similar to `SignedSource` in HHAST.
A linter is has also been included to verify that your codegen is not edited by hand.

### New library is in the making

I am developing a new library for personal use. I have (re)written this concept too many times to count.
There is no guarantee that this implementation will see the light of day, but I thought I'd let
you know anyway.

The concept of the `HH\\Lib\\SQL\\Query` api is great. It rules out SQL injection in the typechecker,
which is a welcome improvement. I have extended the capabilities of `HH\Lib\SQL\Query` in the past
by preprocessing the arguments and the format string. The code you'd need to write the rewrite
format strings in a generic and dynamic manner is not that much harder than the straight coded version.
So, in order to hopefully make this the last time I have to write this, I have put this in a library.
You will be able to define your own extensible formatting language for any purpose, including non-sql.
Look forward to more information in the next post in November.

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
