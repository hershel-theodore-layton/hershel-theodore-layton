# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

_Typo here, typo there, typos everywhere._

## Linting improvements

A lot of usability improvements have been made to linting with [PhaLinters](https://github.com/hershel-theodore-layton/portable-hack-ast-linters).

A general library improvement, `LintError` now exposes an optional `Patch`, which can be applied to cure the detected error. This functionality is present in `dev-master` for the time being. The Pha specific linters `concat_merge_or_union_expression_can_be_simplified_linter`, `count_expression_can_be_simplified_linter`, and `getter_method_could_have_a_context_list_linter` already include a `Patch`.

A new repository, [PhaLintersServer](https://github.com/hershel-theodore-layton/portable-hack-ast-linters-server) has been created to create a bundled version of PhaLinters and its dependencies. This unblocks the use of PhaLinters to lint `HTL\` Software[^1]. This bundle was announced in the [January 2024 post](../2024-01.md). It has no configuration, so if you want to adopt it, you will need to compile your own bundle. This isn't difficult to do, since the repository serves both as a testbed for your changes, and contains a `./build.sh` file to export a `.resource` bundle. Once you have your own `.resource` file, you can copy this standalone build of `PhaLinters` (and the integrated web server) around. The bundle is compiled to a repo auth `.hhbc` file when you start it. Running PhaLinters under Repo Auth reduces memory use and CPU time. This package exposes an http interface to lint files. The lint results may be reported in human readable text or in json form. The latter being useful for...

A vscode editor integration [Dead Simple Lint Server Integration](https://github.com/hershel-theodore-layton/dead-simple-lint-server-integration) :tada:!!!

![example](https://github.com/hershel-theodore-layton/hershel-theodore-layton/assets/81193606/f3a4093f-43ad-42a5-ab3c-f8c046e3cb20)
<sup>Also, multi media in a blog post??? Color me impressed 🤩!</sup>

This extension is published to [OpenVSX](https://open-vsx.org/extension/hershel-theodore-layton/dead-simple-lint-server-integration), but not (yet) to the [Visual Studio Extension Marketplace](https://marketplace.visualstudio.com/VSCode). The former is available to editors which are vscode compatible (but not to vscode without some hackery), the latter is exclusive to Visual Studio Code. Once the authentication gods let me through, I can publish to the Marketplace, but for now, I am not welcome due to a coding oversight on Microsoft's part 🙄.

The `HTL\` family of packages will at some point say farewell to HHAST and integrate with this lint server instead. HHAST is a difficult to replace, highly hhvm version specific dependency, which could hold the community back when a newer hhvm build becomes available. In the [January 2024 post](../2024-01.md) I noted that I would create a replacement for hhvm/actions. This runner will of course have support for PhaLinters out of the box.

The `.resource` files generated are compatible with [hhvm version 4.128 and above](https://hhvm.com/blog/2021/09/21/hhvm-4.128.html) and will work on [hhvm version 4.108 and above](https://hhvm.com/blog/2021/05/04/hhvm-4.108.html). The support window could not be extended to [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html) since the bundled resource depends on the hsl, but does not include the sources. The hsl became a built-in part of hhvm in 4.108.0. You could probably still build a `.resource` file for use with hhvm 4.102, by `composer require hhvm/hsl` and letting the bundler include these vendored dependencies, but this is not something I have tried.

## SGMLStream improvements

SGMLStream is now context aware. This means you can write xhp expressions in a pure scope. The proposed context lists can be found in [this SGMLStreamInterfaces commit](https://github.com/hershel-theodore-layton/sgml-stream-interfaces/commit/c02e99aa4776c52a418d041516bb213e6072c31d) and by checking the latest context lists in the [SGMLStream repository](https://github.com/hershel-theodore-layton/sgml-stream).

These changes have not been released in a named version, since I want to give everyone a chance to try out the more restrictive context lists first. If you use `SGMLStream`, please verify that the new version would not break your usecase by installing `dev-master` before July 15th of this year. File issues on the Github repository (either the interfaces project, or the main sgml-stream project) so I can weaken the requirements where needed. If you have an impure `init(): void` method declared, see the [March 2024 post](../2024-03.md) for details on the init method context.

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

[^1]: Composer objects when you create a circular dependency. This bundle does not have any dependencies, so any project (including PhaLinters) can depend on this package. The bundle is also shipping in a `.bundle` (instead of a `.hack`) file. This means the sources won't be considered for autoloading nor for typechecking. This keeps hhvm and hh_client happy.
