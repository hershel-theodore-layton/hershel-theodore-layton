# Blog

_Typo here, typo there, typos everywhere._

### HHVM commits are once again sync'ed to Github

_This has nothing to do with `HTL\`, but I am glad to be able to share this news with you anyway. The HHVM OSS Team did it, they fixed the Github sync!_

This means a lot to me. I care a lot about the HHVM project. I hope it may one day become a project anyone can pick up and use in the time it takes to run `apt install hhvm -y` or `docker run -it -v $PWD:/mnt/project hhvm/hhvm:latest`. Doing so in September of 2023 gets you [hhvm version 4.172](https://hhvm.com/blog/2022/11/02/hhvm-4.172.html), which was released in November of 2022.

I closed my previous blog post with a rather hopeful message:
 > **🌻 Three cheers to the HHVM OSS team, for they may restore the public releases, so all of us can use hhvm 6. 🌻**

Although the HHVM OSS Team didn't manage to pull that off yet, they did take a giant leap towards it. You can't see it from the commit history on Github, as the commit dates to the internal repo are what is shown (instead of the date and time that the commit landed on Github), but HHVM's public development froze about a month before my previous blog post. Development was still happening internally, but the infrastructure to sync these changes had broken down.

I am immensely greatful for what has been achieved so far.

### Getting hhvm 6.33+ is harder than it should be

 > I hope that one day users of hhvm will look back at this dry spell of minor versions as a blip of history. HHVM is still being developed, but the infrastructure around hhvm for releasing binaries, docker images, and lately even shipping source code to GitHub has broken down.

As anyone who has tried can tell you, compiling hhvm from source is no joke these days. The [hhvm-packaging](https://github.com/hhvm/packaging) repository included an automated build pipeline for creating your own hhvm binaries. This broke down earlier this year and has not been fixed since. This repo was archived last month.

I just hope the HHVM OSS Team is able to make something like it again. Until then, we will all [standby for release](https://hhvm.com/blog/2022/11/14/standby-for-release.html). _If anyone has got a build of hhvm 6.33+ and is able to share it or the instruction on how to build it, I'd be all ears._

_Now back to `HTL\` news for a change._

### Improvements to static-type-assertion-code-generator

I am proud to announce v1.0 of this library. [release notes](https://github.com/hershel-theodore-layton/static-type-assertion-code-generator/releases/tag/v1.0.0)

What broke?

_First and foremost, this version is 90% backwards compatible with the previous version._

Just add a `[]` context to your `panic(): nothing` function, and everything should typecheck again. The generated code has changed, so a rerun of your codegen is in order, but the runtime behavior **for well-typed data** will remain the same. For **ill-typed data**, the stack traces for exceptions will have different line numbers and contain fewer frames.

What's new?

In short, support for more types and greatly improved support for niche use cases, all powered by [a visitor](https://github.com/hershel-theodore-layton/static-type-assertion-code-generator/blob/1093d06ee5c42b1225b5a5d840a4eaa1c85491d1/src/DefaultVisitor.hack).

 - More efficient codegen, no more immediately invoked lambda expressions in the generated code.
 - The `vec_or_dict<_, _>` type is now natively supported without the need for custom aliasses.
 - You are now able to get the text for the return type using `TypeVisitor\visit<T, _, _>(new TypeVisitor\TypenameVisitor(...));`, removing duplication from your codegen code.
 - All code is annotated with the pure `[]` context.
 - You are now able to use the visitor core of `static-type-assertion-code-generator` as a standalone package.

`static-type-assertion-code-generator@v0` had a big switch statement inside that inspected the `T` passed to `emit_body_for_assertion_function<T>(...)`. It created the type description inside this switch, which meant you couldn't reuse this inspection logic outside of `static-type-assertion-code-generator`.

No more, I say! [type-visitor](https://github.com/hershel-theodore-layton/type-visitor) now does the `switch`ing and you decide what to do based with that.

### Plans for Lecof

`Lecof\` is one of those libraries that could have been pure `[]` from the start, but wasn't because of hhvm version constraints of the time. I am planning on tackling this next. This will be a breaking change, but your routing code `Lecof\merge(Lecof\literal(...), Lecof\done(...))` code will remain valid. More details will become clear once I have started working on it.

## [July 2023](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2023-07.md)
## [May 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-05.md)
## [March 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-03.md)
## [January 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-01.md)
## [SGMLStream Sillimanite Release](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-release-announcement-sgml-stream-sillimanite.md)
## [November 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md)
## [September 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-09.md)
## [July 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md)
