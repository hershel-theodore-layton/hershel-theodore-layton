# Blog

_Typo here, typo there, typos everywhere._

## July 2021

### HHVM version support

I support [hhvm version 4.73](https://hhvm.com/blog/2020/09/02/hhvm-4.73.html) and above. This version has the [new XHP syntax](https://hhvm.com/blog/2020/09/02/XHP-namespaces-and-syntax.html) enabled by default. Projects which do not interact with the xhp syntax will also not support hhvm 4.72 and below. I will not accept contributions which attempt to build in official support for hhvm 4.72 and below. I do not run code in hhvm 4.66 and below, since [hhvm version 4.67](https://hhvm.com/blog/2020/07/20/hhvm-4.67.html) removed code execution from pseudo mains (top-level code). This gives me full control over the code I run, since I do not need to vet code that I do not call directly or transitively.

A lot of things have changed since hhvm 4.73 and the present day. The most obvious and important one being: [hhvm version 4.103](https://hhvm.com/blog/2021/03/31/hhvm-4.103.html) removed `darray` and `varray`. This implicitly made tuples vecs and shapes dicts. My code will always take `dict` and `vec`, except for cases where the runtime uses the legacy arrays internally. If you are having problems with arrays, feel free to create an issue. One thing I will not do is jugling runtime types to make them match. So if your hhvm version has shapes represented by a darray, I'll not create a darray from a dict. Idem for tuples.

I have no intention to move the lower bound of the support window up just yet. It is still possible to write portable code against hhvm 4.73. Credit to the hhvm team for making this possible. When the time comes when this is no longer possible, I'll drop legacy hhvm version support on all projects simultaniously, even though only one project may be affected. Everything up and until the oldest supported hhvm lts version is on the chopping block. This means if hhvm 4.80 is still supported by the hhvm team, I will not drop hhvm 4.80 support, unless there is a compelling reason to do so. [Hhvm version 4.80](https://hhvm.com/blog/2020/10/21/hhvm-4.80.html) support from Facebook is expected to last until late September of 2021. Support for [hhvm version 4.102](https://hhvm.com/blog/2021/03/29/extending-hhvm-4.102-support.html) is expected to last until early March 2022.

### Hack language settings support

Hack has some settings you can twiddle with in `.hhconfig`. I intend to support the default configuration (an empty `.hhconfig` file) on [hhvm version 4.108](https://hhvm.com/blog/2021/05/04/hhvm-4.108.html) and above. This hhvm version made the hsl a built-in component, which effectively means that you can use `C\is_empty()` and friends without having to whitelist the `HH_FIXME` codes that the hsl uses. This means that the use of `HH_FIXME` and `HH_IGNORE_ERROR` is not allowed. [require-all-packages-without-hh-ignore-error](https://github.com/hershel-theodore-layton/require-all-packages-without-hh-ignore-error) enforces this fact. The `.hhconfig` file of the projects does whitelist error codes for development dependencies, such as hhast and hacktest.

### Backwards compatibility promises

I can not provide a full list of things that you can not rely upon, see [Hyrum's law](https://www.hyrumslaw.com/).
 - You should rely on is anything in a `_Private` namespace. Calling `_Private` code is not supported.
 - Don't depend on things that Hack doesn't know about.
 - Do not use runtime `as` and `is` checks to refine a `newtype` or an `interface` down to the runtime type.
 - Do not intercept internal function / method calls using `fb_intercept2()` and friends.
 - Do not use runtime reflection.
 - Don't depend on the file strucuture.
 - Don't break type safety. (If I take a `vec<int>`, hhvm will not throw a `TypeError` for a `vec<string>`.)
 - Read the release notes. Promising complete Semver is something no Hack library does today. I'll do my best to document surprices.

### Library version numbers

LIBRARIES ARE NOT FOLLOWING STRICT SEMVER, UNLESS SPECIFICALLY MENTIONED! Hhvm makes breaking changes weekly. If such a breaking change were to affect a library, it would force a major version release according to strict semver. If the semantics of the language change, this library will not try to patch around that. Unless the semantics change breaks an unrelated use, the semantics change is passed onto the caller. This means that v3.4 of library x may behave differently on hhvm 4.73 than it does on hhvm 4.103.

Now that I have gotten that important message out of the way, I can explain the what, when, and how of version numbers. Version numbers have three components, referred to as `x.y.z`. So `v1.2.3` to `v1.2.4` is called a `.z` or dot-z release, `v1.2.3` to `v1.3.0` is called a `.y` or dot-y release, and `v1.2.3` to `v2.0.0` is called a `.x` or dot-x release. Any library with a version greater than or equal to `v1.0.0` will follow these guides, unless otherwise specified.

A dot-x releases may break anything and everything. Breaking changes that have not been phased out using deprecations will warrant a dot-x release. Dropping support for an hhvm lts version is cause for a dot-x release iff this hhvm lts version is still supported by Facebook. Removal of support for an unsupported hhvm lts version may happen in a dot-y release.

A dot-y release may remove / alter apis which have been deprecated in a previous dot-y release, provided a migration path is available in the previous dot-y version. A dot-y release is also celebratory.

A dot-z release may alter apis in minimally intrusive ways. For example, handling more cases than previously handled. Something which failed or clearly broke in a previous version may be given reasonable behavior. Changing a dependency version is also cause for a dot-z release. If upgrading a dependency is causing you troubles, please get in touch.

### Contributions

If you wish to contribute to any of the projects, you'd be more than welcome. I'll ask you to add your Github profile url to `CREDITS.md`. `CREDITS.md` will be exported via [composer](https://getcomposer.org/) and be visible to all users and visitors of Github.
