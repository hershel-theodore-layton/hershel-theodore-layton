# Blog

_Typo here, typo there, typos everywhere._

## July 2023

**If anyone has a build of hhvm version 6.34 or above, please get in touch.**

### SGMLStream version 1 is out

Today marks the release of [SGMLStream version 1](https://github.com/hershel-theodore-layton/sgml-stream/releases/tag/v1.0.0). Don't worry, there is nothing wrong with version 0 and you can continue to use it, if you please. Version 1 includes the long awaited flow changes announced in the [March 2022 post](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-03.md).

For a detailed upgrade guide, see [upgrading-from-v0-to-v1](https://github.com/hershel-theodore-layton/sgml-stream/blob/master/docs/upgrading-from-v0-to-v1.md). A [migration](https://github.com/hershel-theodore-layton/sgml-stream/blob/master/tests/migrations/UserElementMigration.hack) is available to auto modernize your xhp components to the version 1 api. Components written for the version 0 api can seamlessly coexist with the version 1 api.

Version 1 brings new capabilities for the `Flow` type. The flow you know has been renamed to `Descendant<Flow>`. Two new flows have been introduced `Init<Flow> `and `Successor<Flow>`.

 - `Init<Flow>` is a read-only flow available to all components, including `DissovableElement`.
 - `Successor<Flow>` enforces a strong read-write order guarantee with practically zero overhead for writers.
   - Write requests are queued up and executed when the element is sent to the `Consumer`.
   - Rendering readers is delayed until the previous sibling (or the parent if no previous sibling exists) is sent to the consumer.

Enjoy these new goodies and build some more great server side rendered user interfaces.

### HHVM version support

Facebook has not released a new minor version of hhvm in 2023. We are all still [standing by for release](https://hhvm.com/blog/2022/11/14/standby-for-release.html). I hope that one day users of hhvm will look back at this dry spell of minor versions as a blip of history. HHVM is still being developed, but the infrastructure around hhvm for releasing binaries, docker images, and lately even shipping source code to GitHub has broken down. 

Here is [the history](https://github.com/facebook/hhvm/commits/master/hphp/runtime/version.h) of the runtime/version.h file in hhvm. The current version on GitHub is `hhvm version 6.70.0`. The latest version for which a public nightly build exists is `hhvm version 6.33.0-dev`. This version is available on [docker hub](https://hub.docker.com/layers/hhvm/hhvm/2023.02.17/images/sha256-54683d5ca43b8bb3ca5ffd52cb5814e7dfad8ab5bb3eef9e7f9293aa1e728536). This release from February 17th 2023. Many core `hhvm/x` and `facebook/x` repositories, such as hhast and TypeAssert, don't work on this version yet.

The oldest supported version is [hhvm version 4.153](https://hhvm.com/blog/2022/03/17/hhvm-4.153.html). It looks like this is going to stay the oldest supported version for a while. The `HTL\` family of packages supports [hhvm version 4.102](https://hhvm.com/blog/2021/03/29/extending-hhvm-4.102-support.html) through [hhvm version 4.172](https://hhvm.com/blog/2022/11/02/hhvm-4.172.html). Until I get my hands on a build of the latest hhvm versions from `master`, I won't be able to support hhvm 6. **If anyone has a build of hhvm version 6.34 or above, please get in touch.**

### A quick aside on version numbers

Version numbers in the `v1.x` range are not based on the number of oxygen atoms in a molecule. They are names of metals instead. The name for version 1.0 is `Gold`.

The version numbers of `hershel-theodore-layton/project-name-interfaces` will not be kept in sync with `hershel-theodore-layton/project-name` once version 1 is reached. The history of sgml-stream has taught me that this just causes churn on the interfaces project. Many a release of [sgml-stream-interfaces](https://github.com/hershel-theodore-layton/sgml-stream-interfaces/releases) has been byte identical to the previous version.

### What the future holds

I am looking forward to developing in Hack. I am simultaniously excited for hhvm 6 and terrified for the large amount of simultanious breaking changes. I expect that the `HTL\` family of packages will need very minor changes, if even that, to get back to up the latest and greatest. Other projects may not have such an easy time.

In order to improve your chances for a painless hhvm 6 migration, I recommend you make your own code more well typed. As long as the typechecker is able to catch most breakages for you, you'll be able to upgrade with confidence when hhvm 6 finally lands.

**🌻 Three cheers to the HHVM OSS team, for they may restore the public releases, so all of us can use hhvm 6. 🌻**

## [May 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-05.md)
## [March 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-03.md)
## [January 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-01.md)
## [SGMLStream Sillimanite Release](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-release-announcement-sgml-stream-sillimanite.md)
## [November 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md)
## [September 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-09.md)
## [July 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md)
