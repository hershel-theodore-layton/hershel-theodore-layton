# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

**[Máté Szabó](https://github.com/mszabo-wikia) has managed to get HHVM@next to build! This PR can be found [here](https://github.com/facebook/hhvm/pull/9564). Thank you!**

_Typo here, typo there, typos everywhere._

## HHVM version support

[`hhvm version 4.102`](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html) and
[`hhvm version 4.128`](https://hhvm.com/blog/2021/09/21/hhvm-4.128.html) have
lost unofficial `HTL\` support. These hhvm versions are many years past the
end of Meta's support window. They were unofficially supported by `HTL\` for
historical reasons and inertia. Expect a new dot-y (x.**y**.z) release
for all `HTL\` software in the near future. These new versions will require
at minimum [`hhvm version 4.153`](https://hhvm.com/blog/2022/03/17/hhvm-4.153.html).
This version has been unsupported for two years by Meta, but the `HTL\`
project will continue to signal support for this version, since upgrading
to `hhvm@next` is not easy. Support for hhvm four will be dropped in the
future. It is unclear to me now when would be a good time to leave these
versions behind. `hhvm version 4.168` in particular has been _the_ latest
LTS for a long while, and it will remain that way. Meta has not released
a new LTS version of HHVM since.

## HHVM images

The last image released on Docker Hub is 25.7.0. I considered building and
releasing 25.8.0 _without_ release notes, but this decided against it.
Release notes are critical for upgrading with a sense of certainty. Writing
release notes for a month of Meta developer output takes a whole evening.
I did not foresee that this would make the building of 25.8.0 and 25.9.0
as difficult as it is now. The commit history on mszabo-wikia/hhvm is
not linear. This means that I have to pull and tag a version on time,
even if I don't intend on building it right away. If I let time slip
I am unable to create a time accurate snapshot of the mszabo-wikia
upstream for that month. I will create 25.8.0 and 25.9.0 as identical
copies of 25.10.0. The release notes will reflect this.

## mszabo-wikia is employed at Slack

[@mszabo-wikia](https://github.com/mszabo-wikia), the man who brought OSS
hhvm back in 2025, has been employed at @slackhq. Congratulations!!! He has
continued maintaining and improving his upstream hhvm source tree and has
showed no signs of stopping. He is working on hhvm related repositories at
Slack, such as [hakana](https://github.com/mszabo-wikia/hakana/commits?author=mszabo-wikia).
I wish you great enjoyment at Slack.

## Small bugfix for simple-web-token

[simple-web-token](https://github.com/hershel-theodore-layton/simple-web-token/commit/af588bbd07d2f9fc015a1aeb1496b64bf5821d01)
is now able to decode tokens with implicit empty values. This library
encodes empty values explicitly. This defect only becomes appearant
if a token is encoded in a different ecosystem. This fix will be
part of the next tagged release, but  you can already use it by require'ing
dev-master.

## [July 2025](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2025-07.md)
## [May 2025](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2025-05.md)
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
