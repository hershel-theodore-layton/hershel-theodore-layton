# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

**[Máté Szabó](https://github.com/mszabo-wikia) has managed to get HHVM@next to build! This PR can be found [here](https://github.com/facebook/hhvm/pull/9564). Thank you!**

_Typo here, typo there, typos everywhere._

## HHVM Docker builds beta

The [HHVM 26.2.0 beta](https://hub.docker.com/r/hersheltheodorelayton/hhvm-full/tags) has just been released.
This is the first build since 25.11.0. A missing build dependency prevented me from building 25.12.0.
I now know what it was (missing libgoogle-glog-dev). This beta is not feature complete. It is unable to
build `.hhvm.hhbc` files for Repo Auth mode. This is probably a case of PEBKAC on my end. I have open sourced
my (admittedly janky) [build script](https://github.com/hershel-theodore-layton/hhvm-build). I will hopefully
soon get feedback on what I can change to make this build work for Repo Auth mode. This beta build
is available for you to test the typechecker changes and to further HTL hhvm version compatibility.
Do not use this in production.

## Portable Hack AST large script support

[Portable Hack AST](https://github.com/hershel-theodore-layton/portable-hack-ast/blob/master/bin/large-script-support.md)
added support for large scripts last December. Previous versions were limited to scripts smaller than 256KiB.
This should make it possible to use Portable Hack AST to analyze entire codebases, where missing the
_insert the name of your deathstar class here_ would break the whole program analysis.

## Simple Web Token now plays nice with other libraries

[Simple Web Token](https://github.com/hershel-theodore-layton/simple-web-token) now generates spec compliant
tokens when using `sign_strict()`. `sign()` continues to work as before. Tokens signed
by `sign_strict()` can be read by other libraries and by `parse_strict()`. 

The upgrade path is:
1. First, update all servers to use `parse_strict()`, which can parse both strict and non-compliant tokens.
1. Once you’re confident no server will choke on a strict token, start using `sign_strict()` to leave the
   non-compliant tokens behind.
   
## SGMLStream Exam(ine)

A small, work in progress, library that consumes an sgml-stream xhp tree and creates a queryable
Document object. This is meant as a testing tool. You describe your expectations like so.

```HACK
$response = await your_endpoint_function_async(...);
$stream = new SGMLStreamExam\PiecewiseStream();
$consumer = new SGMLStreamExam\ToHTMLDocumentConsumer();
await your_streaming_function($stream, $consumer);
$document = $consumer->toDocument();

expect($document->getElementByIdx('signin-button')->getInnerHTML())
  ->toEqual('Sign In');
```

The API is not yet stable. No version (not even `Ho, Ho, Ho, v0.0.0`) has been tagged.
The goal is to implement as much of the DOM API as makes sense for the HTML on the server.
Things like CSS, JavaScript execution, and parsing unstructured HTML are out of the picture.
This project will take more shape when the DOM API becomes more complete. There is no
guarantee this project will get a numbered release. It might be abandoned if something
proves to be too difficult to implement from first principles.

## Smaller changes

[Expect](https://github.com/hershel-theodore-layton/expect) now has a `->toContainElement()`
A great supplement to the existing set of assertions.

## It is February, huh?

Yes, I used to post in the odd months of the year. I missed November and January. The streak
has been broken. I could have waited a week to post in March, but why delay? I shouldn't feel
constrained by a pattern I started in 2021.

## [September 2025](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2025-09.md)
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
