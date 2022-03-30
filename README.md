# Blog

_Typo here, typo there, typos everywhere._

## March 2022

### HHVM version support

Facebook has dropped support for [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html) with the release of [hhvm version 4.153](https://hhvm.com/blog/2022/03/17/hhvm-4.153.html). A [security release 4.128.4 .. 4.148-154.1](https://hhvm.com/blog/2022/03/29/security-update.html) has been published since 4.102 support has been dropped. If you are running an unsupported version of hhvm, see if upgrading to a supported version would be feasible.

_Clarification: Supporting an hhvm version with the `HTL\` family of packages means you CAN run our code on said version. It does not mean it is a good idea to do so. We do not intend to support the hhvm release itself (by means of patches to hhvm itself). We merely promise to remain compatible with the Hack language version shipped with that hhvm version. You run these hhvm versions at your own risk._

As promised in the [November 2021 post](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md), the `HTL\` family of packages will continue to support [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html) and up until either:

 - A change in a new hhvm release requires a change which is incompatible with hhvm 4.102.
 - The 1st of July 2022.

Excerpt from the [hhvm version 4.153 post](https://hhvm.com/blog/2022/03/17/hhvm-4.153.html). _We_ refers to the hhvm team.
 > We moved from monthly to weekly releases in 2019 due to the large rate of breaking changes, and the difficulty in keeping up with them; ...
 > We aim for 4.156 to be the last weekly release, and will then be moving to a two-week release schedule; we hope that this is a stepping stone on the way to a monthly release cycle

What this means for users of `HTL\` packages. The `HTL\` family of packages will continue to support all releases made between the minimum version (at this point in time 4.102) and the current nightly release. The `HTL\` family of packages is unaffected by the changed release schedule.

### Looking ahead to coeffects and capabilities

All code in the `HTL\` family of packages does not specify a capabilities list. This is identical to having the `[defaults]` capability. Functions and methods that are not implemented outside of the packages (top level functions and final methods) will start receiving `[]` capability lists where pratical and portable across all supported hhvm versions.

Non final methods can not simply add an empty capability set, since your code may not specify a capability set at all. Breaking changes like this are difficult to ease in. These methods will retain their `[defaults]` capability for now. In a future release, we may introduce context constants to allow both `[defaults]`, `[subset of defaults]`, and `[]` implementations to exist in a typechecker queryable manner.

## [January 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-01.md)
## [SGMLStream Sillimanite Release](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-release-announcement-sgml-stream-sillimanite.md)
## [November 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md)
## [September 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-09.md)
## [July 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md)
