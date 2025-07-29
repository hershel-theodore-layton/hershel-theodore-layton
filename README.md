# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

**[Máté Szabó](https://github.com/mszabo-wikia) has managed to get HHVM@next to build! This PR can be found [here](https://github.com/facebook/hhvm/pull/9564). Thank you!**

_Typo here, typo there, typos everywhere._

## HTL publishes hhvm@next containers

You can [find me](https://hub.docker.com/u/hersheltheodorelayton) on Docker Hub.
I publish versions once a month, 25.**6**.0 was published in June, 25.**7**.0 was published in July.
I expect to publish 25.**8**.0 in August and **26**.1.0 in January of 2026.

You can read [the release notes](https://hershel-theodore-layton.github.io/hhvm-docs/releases/) before upgrading.

I publish two image series:
 - [hhvm-basic](https://hub.docker.com/r/hersheltheodorelayton/hhvm-basic)
   - This includes HHVM and hh_client, but no other tooling. Not even PHP for installing composer dependencies.
 - [hhvm-full](https://hub.docker.com/r/hersheltheodorelayton/hhvm-full)
   - This includes everything for a productive development environment: git, php+composer, curl, wget
   - Watchman has been installed and preconfigured for autoloading

DISCLAIMER: tl;dr THESE IMAGES ARE PROVIDED BY ME TO YOU "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,...[^1]

## Máté Szabó is still at it

Thank you @mszabo-wikia for being so helpful, communicative, positive, and determined.

My hhvm source repository is downstream from [Máté's build mirror](https://github.com/mszabo-wikia/hhvm/tree/fix-oss-build-mirror).
He has been fixing all the CMake/cplusplus, Cargo/Rust, OPAM/OCaml, and third-party vendored dependencies.
He deserves all the credit and kudos for keeping this massive codebase buildable outside of Meta.
Give the man a ⭐ [here](https://github.com/mszabo-wikia/hhvm/tree/fix-oss-build-mirror) and a follow,
he's earned it. Without his branch, my hhvm builds will quickly fall into disarray.

I have asked for an experience report of building and working on hhvm and he didn't disappoint.
If you want to tinker with hhvm, start from his branch. Here's his advice for you:

 - _LLVM (i.e. clang + libcxx) 18 is used in CI, but >= 18 is fine too (I'm using LLVM 20 via my distro locally). v20 had some issues with folly recently, but those should be fixed now._
 - _I recommend getting ccache as well, since a 50-60% hit ratio is attainable with a 5 GiB cache dir, which can be very helpful when iterating locally._
 - _If possible, use a system with good thermals, because a laptop with a high core count CPU will likely have dissipation issues when doing sustained concurrent compilation. Using a desktop in comparison will noticeably improve compile times because you won't go to minclock just from utilizing all available cores._

_And some aspirational goals/improvements for the build system:_
 - _Dependency tracking doesn't really work yet for some of the Rust targets that get linked into HHVM targets, so incremental rebuilds can eventually fail when the underlying Rust code changes, which then requires manually removing their outputs from the build dir._
 - _A lot of the MSVS/GCC/Intel C++-related configuration cruft could be removed, alongside various now-obsolete options (e.g. toggling XeD, which is now a required dependency)._
 - _There are undocumented features in the repo that have never been integrated into the OSS build, even before the end of OSS support, which could be interesting to explore in the future._
 - _It might be worth it to revive the Nix-based universal deb/rpm builds, but that seems like a whole new adventure :)_

## HTL software is Docker Native

All HTL repositories now contain `Dockerfile`s for instant local development.
`docker compose up` will create all files for development with [VSCodium](https://vscodium.com/).
These projects will use hhvm@next and you don't need to have hhvm installed on the host.

## HHVM version 4.102 through 4.128 is ending

In two months, unofficial support for [hhvm version 4.102](https://hhvm.com/blog/2021/03/23/hhvm-4.102.html) and [hhvm version 4.128](https://hhvm.com/blog/2021/09/21/hhvm-4.128.html) will end.
If you are using HTL software on these hhvm versions, you can continue to do so.
The current versions of HTL software will work on these versions. All projects will
receive a version bump and previous versions will not receive ongoing maintenance.

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

[^1]: THE IMAGES ARE PROVIDED BY ME TO YOU “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
