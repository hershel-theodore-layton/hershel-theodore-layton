# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

_Typo here, typo there, typos everywhere._

## January 2024

A happy new year to all!

### New projects have been released

The following projects are now available via composer for everyone to install and use:
 - [portable-hack-ast](https://github.com/hershel-theodore-layton/portable-hack-ast)
   - A low-level library that allows you to parse and introspect your Hack source code.
   - It is completely version independent. You can run it on `hhvm version 4.102` through `hhvm version 4.172`. 
   - It uses very little memory, something that has been troublesome for HHAST, and is as fast as Hack code can be.
   - I have some more features planned, so if it doesn't meet your needs today, pin it in your browser anyway.
 - [portable-hack-ast-linters](https://github.com/hershel-theodore-layton/portable-hack-ast-linters)
   - Think HHAST, think linters, this is that, but built on portable-hack-ast.
   - I am looking for [an integration with a Language Server](https://github.com/hershel-theodore-layton/portable-hack-ast-linters/issues/1). Would _you_ be willing to help out? 
 - [portable-hack-ast-extras](https://github.com/hershel-theodore-layton/portable-hack-ast-extras)
   - Some extra tooling that isn't a part of the ast machinery.
   - This includes common utility code like resolving symbols and parsing pragmas.
 - [pragma](https://github.com/hershel-theodore-layton/pragma)
   - Wait, parsing pragmas? Yes!
   - This teeny tiny package includes `pragma(...)` and `<<Pragmas(vec[...])>>` to annotate your code with.
   - This is more structured than structured comments, such as `HHAST_FIXME[...]`, I don't like ~structured~ magic comments.
   - This is more versatile than Hack's attributes, since you can attach metadata to lines of code, in addition to attaching it to entire methods and classes.
  
These packages fulfills a lot of the needs that HHAST used to fulfill. This was the last difficult to upgrade component from the `{hhvm,facebook}/x` stack. HHAST is aggressively hhvm version specific. This means it could single-handedly hold everyone back when newer builds of hhvm become available. I didn't want this to be the case for `HTL\`, so I replaced it. I am welcoming everyone else to use it as well, since I'd want everyone to have the choice to upgrade when the time comes. The sad truth is, that the `{hhvm,facebook}/x` composer namespaces have been abandoned. They are still fine to use, but they'll not receive further upgrades, including upgrades that make them compatible with newer hhvm versions.

### HHVM version support

The `HTL\` family of packages supports hhvm versions as far back as [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html). This version was released in March of 2021 and got its last change in March of 2022 with the release of [hhvm version 4.102.7](https://hhvm.com/blog/2022/03/17/hhvm-4.153.html). Supporting the range 4.102-4.172 is fine and has been fine for a while. I am wondering if there are any users stuck on an hhvm version between 4.102 and 4.151 (4.152 was skipped). If not, it seems rather silly to continue to support those versions for new projects.

The two latest lts releases [hhvm version 4.153](https://hhvm.com/blog/2022/03/17/hhvm-4.153.html) and [hhvm version 4.168](https://hhvm.com/blog/2022/09/09/hhvm-4.168.html) will continue to be supported, since they were the last versions that received support from Meta. If you are on either of these versions, you have nothing to fear.

Starting today the new supported targets are `hhvm version 4.153` and above. The CI for `hhvm version 4.102` and `hhvm version 4.128` will still be used for all projects. As long as the CI passes, the composer.json file will signal support for these hhvm versions. If a new project can not be made compatible with `hhvm version 4.102` after a good faith effort has been made, it will not support anything below `hhvm version 4.153`. Projects that are already published will almost certainly support `hhvm version 4.102` for months or even years to come.

Support for `hhvm version 6.33+`, which I'll start to refer to by the name hhvm@next, is something I'd love to provide. As soon as I get my hands on an hhvm build from 2024 or later, I'll gladly make the necessary changes to support it. If doing so would require support for `hhvm version 4.151` and below to be dropped, this will not factor into that decision. You'll be able to keep using the current version of the `HTL\` software on older hhvm versions indefinitely.

### What's up next

I am going to fork `hhvm/actions` which includes `hack-lint-test.yml`, the default CI system for OSS Hack Projects. I will extend it with support for `ext_watchman` / `ext_facts` based autoloading, `hhvm/hhvm-autoload` begone, since hhvm@next doesn't support userland autoloading. My fork will offer linting with `hhast` and/or `portable-hack-ast-linters`.

I am also considering a linting-in-a-box package. This package would bundle `portable-hack-ast*` in one file. This would **not** be a Hack file, meaning it can be composer require'd in any package, including the transitive dependencies of `portable-hack-ast-linters`. Without this level of indirection, composer would be stuck in circular dependency hell and `hh_client` and the `ext_facts` autoloaded would be confused by duplicate definitions. You could consider this "a binary release", for as much as the terminology makes sense for Hack.

I'd prefer you to use `portable-hack-ast-linters` directly, since this would allow you to configure everything yourself and to add your own linters, if you so desire. But if you want to get something up and running in less than a minute, you can try before you ~buy~ invest the time.

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

[^1]: The full text was authored by Paul Bissonette and published to hhvm.com under a Creative Commons Attribution 4.0 International license.
[^2]: In June I copied the sources over to a new repo, but I had already been writing code in March (maybe April). The latest iteration started in October.
