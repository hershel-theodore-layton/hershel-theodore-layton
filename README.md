# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

_Typo here, typo there, typos everywhere._

## SGMLStream Contexts Release

In the blog post [May 2024](./2024-05.md) I annouced the intent to publish a new
version of [sgml-stream](https://github.com/hershel-theodore-layton/sgml-stream)
which includes context annotations. This will allow xhp components to be
constructed from a pure context. This is a breaking change, neither forward nor
backwards compatibility has been maintained. A new major release is warranted.
Version `v2.0.0 - Helium` has been released.

This release was delayed by a month and a half to give users an opportunity to
notify me of context annotations that conflict with their implementations of the
common interfaces. No issues have been filed on Github. This means all systems
are green for release.

This release ends the one year reign of sgml-stream `v1.x`, see `v1.0.x - Gold`.
Bug fixes will still be applied to the `v1.x` release line for a time, but new
features will not be backported to this release. The `v0.x` line has reached the
end of its useful life. If you are still using `v0.x`, you may continue to use
it as-is. Do not expect any changes (including bug fixes) on this release line.

## New Library

A new library has been added to the `HTL\` family of packages:
[simple-web-token](https://github.com/hershel-theodore-layton/simple-web-token)

This library implements the simple web token standard in a pure context.
The simple web token standard is incompatible with the json web token standard.
Simple web tokens allow a server to sign some key value pairs, hand these pairs
and this signature to an untrusted party, and to later receive them back from
this party, knowing it this party did not alter the data. In web speak, you can
encode session data which can be stored on the client. If the client attempts to
modify the session data, you can detect it.

`user_id=4&permission_level=admin&HMACSHA256=[[base64]]`

Json Web Tokens should be preferred over Simple Web Tokens when:

- You interoperate between many languages that have a JWT library, but no SWT one.
- You need the asymetric nature where the service that validates the token
  should not have access to the key used to sign tokens.
- You are living in the future where hmac with sha256 is broken.

If none of these apply to you, Simple Web Tokens may fulfill your needs.

### Pure Hashing

Simple Web Token is fully context annotated and can be used from a pure context.
This required implementing a pure version of `\hash_hmac()`. The pure sha256
hash and hmac functions may be useful to you, even if you do not need SWT
functionality.

## CI Changes

From day one of `HTL\` development, CI has been run on Github Actions. The
action `hhvm/actions/hack-lint-and-test` action supplied the functionality to:

- Install hhvm and the Hack development tools, such as composer
- Install project dependencies using `composer`
- Typecheck using `hh_client`
- Autoload your code with `hhvm-autoload`
- Lint your sources using `hhast-lint`
- Test your code using `hacktest`

Sadly, this actions definition is not being maintained anymore. I have forked
hhvm/actions to [htl/actions](https://github.com/hershel-theodore-layton/actions).
This action runner is out-of-the-box compatible with `hhvm/actions`, but includes
a couple of extra features:

- Selecting composer.json files for legacy hhvm versions e.g. `hhvm version 4.102`.
- Autoloading your code with ext_watchman
- Linting your sources with `PhaLintersServer`

No alternative test runner has been provided. HackTest remains the only supported
the runner for now. If a test runner is added to the `HTL\` family of packages,
support will be added to this actions runner too.

### Action use for HTL

All `HTL\` code is now being tested with `hershel-theodore-layton/actions`. This
allows me to maintain support for hhvm 4.102 with minimal effect on hhvm 4.153+.
All `HTL\` code is now linted by `PhaLinters` instead of `HHAST`. This will make
upgrading to hhvm@next a whole lot less painful.

## Removing hhvm/x dependencies from HTL

The `HTL\` family of packages still depends on `hhvm-autoload` and `hacktest`.
The former does not work on hhvm@next, since userland autoloading has been removed.
The latter depends on the former, so both will have to be removed from the stack.

The `hhvm/x` ecosystem allowed me to bootstrap `HTL\`. `HTL\` would not exist if
`hhvm/x` and `facebook/x` weren't available. The time has come to move on, since
the packages are not being maintained and would hold back hhvm@next adoption. I
am thankful for what these packages represent, the effort Facebook, later Meta,
invested into creating a welcoming and supportive Open Source ecosystem for Hack
developers. Sadly, the future turned out differently than anticipated, and they
have since stopped supporting their Open Source Hack library offerings.

I want to thank the folk at Meta who maintained these libraries for as long and
as well as they have. I have used these libraries with pleasure and they have
inspired me to improve upon their core concepts.

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
