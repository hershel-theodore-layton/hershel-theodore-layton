# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

**[Máté Szabó](https://github.com/mszabo-wikia) has managed to get HHVM@next to build! This PR can be found [here](https://github.com/facebook/hhvm/pull/9564). Thank you!**

_Typo here, typo there, typos everywhere._

## No commits

No new commits have been made to the HTL repositories since the last update in February.

## Future changes

I still need to create a replacement for `fbexpect` e.g. `expect($foo)->toEqual($bar)` and `hacktest`.

## HHVM@next breakages

[portable-hack-ast-linters-server](https://github.com/hershel-theodore-layton/portable-hack-ast-linters-server) is a really strange repository. If you `git clone` it, you get Hack code which you can edit and customize. If you `composer require` it, you get a `.resource` file, which you can run. Reasons, composer doesn't like circular dependencies, ya dee ya dee ya. The command I used to create this resource file is: `hh_client --concatenate-all`. I learned recently that [this commit from **late-2023**](https://github.com/facebook/hhvm/commit/79c9c38ab6ab5dfd0c8d9cc15a16e914a74f4df0) removes this functionality. This doesn't affect me at the moment, since portable-hack-ast-linters-server supports `hhvm version 4.168`, which can build these *cough* binaries.

When I drop support for all hhvm versions that support this command, I will have to find a replacement. I hope that `hhvm@next` can run code written for the hhvm versions of yesteryear. That way, I can put this problem ahead of me. The thing that could break this is new syntax that can not be avoided in `hhvm@next` which can not be understood by `hhvm version 4.168`, just like coeffects are required in some places these days, but `hhvm version 4.92` cannot parse them. I will do what I can to make the transition to `hhvm@next` a smooth one. I still don't know if I can support `hhvm version 4.168` and `hhvm@next` in the same codebase, let alone `hhvm version 4.102`. Please, I urge you, upgrade to `hhvm version 4.168` if you are able to.

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
