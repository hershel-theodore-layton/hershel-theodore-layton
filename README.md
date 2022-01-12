# Blog

_Typo here, typo there, typos everywhere._

## January 2022

### HHVM version support

The `HTL\` family of packages drops support for [hhvm version 4.73](https://hhvm.com/blog/2020/09/02/hhvm-4.73.html) through [hhvm version 4.101](https://hhvm.com/blog/2021/03/16/hhvm-4.101.html) today. This was previously announced in the [November 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md) post. The current minor versions remains available to those who are not able to upgrade to [hhvm version 4.102](https://hhvm.com/blog/2021/03/29/extending-hhvm-4.102-support.html). Keep in mind that the hhvm lts releases [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html) and [hhvm version 4.128](https://hhvm.com/blog/2021/09/21/hhvm-4.128.html) are the oldest hhvm versions that are still supported by Facebook.

The `HTL\` family of packages is not alone. Many of the `hhvm/*` and `facebook/*` projects have also increased their minimum hhvm version. This was done in order to support Composer version 2.2. From the [hhvm version 4.143](https://hhvm.com/blog/2022/01/06/hhvm-4.143.html) announcement:

_Additional patch releases have been made for 4.102, 4.128, and 4.135-4.140, which change the typechecker to ignore any files in vendor/bin/; this is required for compatibility with Composer 2.2._

 - [hhvm/definition-finder](https://github.com/hhvm/definition-finder/commit/653fc2484ed9b9e9cfc6156833f2e77544491929)
 - [facebook/fbexpect](https://github.com/hhvm/fbexpect/commit/2ce34e95ad1c49ec5f906cda9533d1fc7faf214e)
 - [facebook/hack-codegen](https://github.com/hhvm/hack-codegen/commit/30128350e0e202330a1a6a1bbb4b989d2b082f36)
 - [facebook/hack-router](https://github.com/hhvm/hack-router/commit/50901a2191baade2b8d5eb89e705104509cfe334)
 - [facebook/hack-router-codegen](https://github.com/hhvm/hack-router-codegen/commit/2dd72153cea9c1ea29850219bfe1679d05ef8404)
 - [facebook/difflib](https://github.com/hhvm/difflib/commit/a37093290ba3d917984913a38eb1e335a6bfa5c6)
 - [hhvm/hacktest](https://github.com/hhvm/hacktest/commit/95b59962e248fed52cd544652b793fab294d966b)
 - [facebook/hh-apidoc](https://github.com/hhvm/hh-apidoc/commit/217c451d3079179c6ecaa787de896f74011fd93f)

If you are currently using [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html), you have ± 6 weeks to upgrade to [hhvm version 4.128](https://hhvm.com/blog/2021/09/21/hhvm-4.128.html). The release of `hhvm version 4.152` will indicate the end of support for 4.102 by Facebook. The `HTL\` family of packages will attempt to support [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html) until July 1st 2022. If 4.152+ makes a change which is not possible to adapt to 4.102, the `HTL\` family of packages will stop supporting 4.102 early.

### New "hhvm 4.102+ only" versions of HTL packages

 - [sgml-stream-interfaces@0.6.0 Diopside](https://github.com/hershel-theodore-layton/sgml-stream-interfaces/releases/tag/v0.6.0)
 - [sgml-stream@0.6.0 Diopside](https://github.com/hershel-theodore-layton/sgml-stream/releases/tag/v0.6.0)
 - [html-stream-namespaced@0.6.0 Diopside](https://github.com/hershel-theodore-layton/html-stream-namespaced/releases/tag/v0.6.0)
 - [html-stream-non-namespaced@0.6.0 Diopside](https://github.com/hershel-theodore-layton/html-stream-non-namespaced/releases/tag/v0.6.0)
 - [lecof-router-interfaces@0.2.0 Oxygen](https://github.com/hershel-theodore-layton/lecof-router-interfaces/releases/tag/v0.2.0)
 - [lecof-router@0.2.1 Oxygen - patch 1](https://github.com/hershel-theodore-layton/lecof-router/releases/tag/v0.2.1)
 - [static-type-assertion-code-generator@0.3.0 Ozone](https://github.com/hershel-theodore-layton/static-type-assertion-code-generator/releases/tag/v0.3.0)

### Stability of SGMLStream

[SGMLStream](https://github.com/hershel-theodore-layton/sgml-stream) will change how tagnames are specified for the `ElementWithOpenTag...` traits. Version 0.6 (due to be released today) will require you to declare a class constant `const string TAG_NAME = '...';`. The value must match the value of `protected string $tagName = '...';`. It will use `$this->tagName` and emit and `E_USER_WARNING` if the value does not match `static::TAG_NAME` at render time. A future version will remove the requirement to declare `protected string $tagName = '...';` and will unconditionally use `static::TAG_NAME` instead. You can declare this constant in older versions of SGMLStream without issue, but `$this->tagName` will be used.

### Release names for HTL packages

HTL packages have versions in the range `0.0.x`, `0.2.x` ... `0.99.x`. (Version `0.1` is always skipped.) These releases have nicknames:

| Version | Nickname    |
|--------:|:------------|
| v0.0.x  | Ho, Ho, Ho  |
| v0.2.x  | Oxygen      |
| v0.3.x  | Ozone       |
| v0.4.x  | Magnetite   |
| v0.5.x  | Sillimanite |
| v0.6.x  | Diopside    |

`v0.0.x` is named `Ho, Ho, Ho`, because triple zero (or triple oh) can be read as "O O O". The release nickname is meant to warn you that this package is experimental. It asks you to stop and think for a while whether you want to use this in production yet.

`v0.1.x` is always skipped.

All other release names in the `v0.x` series are chemicals, where the number of oxygen atoms matches the version number. `0.2` looks like O<sub>2</sub>, `0.3` looks like O<sub>3</sub> and so forth.

_Chemical formula's sourced from Wikipedia._ `v0.2` [Oxygen](https://en.wikipedia.org/wiki/Oxygen) O<sub>2</sub>, `v0.3` [Ozone](https://en.wikipedia.org/wiki/Ozone) O<sub>3</sub>, `v0.4` [Magnetite](https://en.wikipedia.org/wiki/Magnetite) Fe<sup>2+</sup>Fe<sup>3+</sup><sub>2</sub>O<sub>4</sub>, `v0.5` [Sillimanite](https://en.wikipedia.org/wiki/Sillimanite) Al<sub>2</sub>SiO<sub>5</sub>, and `v0.6` [Diopside](https://en.wikipedia.org/wiki/Diopside) MgCaSi<sub>2</sub>O<sub>6</sub>.

## [SGMLStream Sillimanite Release](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-release-announcement-sgml-stream-sillimanite.md)
## [November 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md)
## [September 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-09.md)
## [July 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md)
