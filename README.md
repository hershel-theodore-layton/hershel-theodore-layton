# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help!**

_Typo here, typo there, typos everywhere._

### HHVM OSS Update

_The latest blog post on the hhvm blog has broken the silence about the release of hhvm 6.33+._

After [standing by for release](https://hhvm.com/blog/2022/11/14/standby-for-release.html) for a year, [closure has been given](https://hhvm.com/blog/2023/10/27/oss-update.html). The whole post is definitely worth a read. Here are some partial quotes[^1].

> We’re asking that the community take a more active role in fixing and maintaining this system. For years, our CMake builds have required very little attention...

> ...we continue to have a very small number of open source users picking up our HHVM+Hack builds.

> Additionally, we will no longer be creating official releases of HHVM and Hack. ... maintaining old versions of HHVM has become a full-time job that we lack the bandwidth for.

This is in stark contrast the the fast-paced (bi)weekly release schedule HHVM used to have between the release of [hhvm version 4.1](https://hhvm.com/blog/2019/04/09/hhvm-4.1.0.html) and [hhvm version 4.172](https://hhvm.com/blog/2022/11/02/hhvm-4.172.html). As one of the very small number of open source users, I am glad that a decision has been made public. This isn't the answer I hoped for, but it is the one I needed to hear. I held hope for hhvm 6 to be released soon, but this post made it clear that hoping and standing by will not be enough. I have added a call for help to this README. I'll update this topic at a later date.

### Lecof v1.0 has been released

As noted in my previous blog post, lecof-router could have been annotated with contexts from the start, but wasn't because of hhvm version constraints at the time. I dropped support for hhvm 4.72 through 4.102 in [January of 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-01.md). The context and capabilities feature became stable in [hhvm version 4.93](https://hhvm.com/blog/2021/01/19/hhvm-4.93.html).

The release of [lecof-router v1.0](https://github.com/hershel-theodore-layton/lecof-router-interfaces/releases/tag/v1.0.0-RC1) introduces a compatibility bridge for those who are unable to adopt a pure context (read `[]`) in their core routing code. If you upgrade to `"hershel-theodore-layton/lecof-router": "^1"` in your composer.json file, you'll get the full pure version. If this you hit a snag in this upgrade, you could try adding `"hershel-theodore-layton/lecof-router-interfaces": "1.0.0-RC1"` as well to loosen the context requirements.

Every feature of v1.x will remain available to you, no matter which version of `lecof-router-interfaces` you pin. The `Filter<T>` classes automatically adapt their contexts based on the declaration specified in that project. This makes it trivial to maintain filters, since there is no need for copy-paste maintenance.

### Something new is coming

I have been hard at work reimplementing a project which I started some time in H1 of this year[^2]. If you use hhast's linters "as they come out of the box", you are going to like it. If you have tinkered around with writing your own tooling on top of hhast, you will be ecstatic.

I don't want to spoil anything, but this will make a whole lot of tooling suddenly...

```
Parsing: ../vendor/hhvm/hhast with hhast from command line took 1539.36 megabytes at peak.
Parsing: ../vendor/hhvm/hhast with hhast in repo auth mode took 1063.71 megabytes at peak.
Parsing: ../vendor/hhvm/hhast with xyzzy from command line took 57.5205 megabytes at peak.
Parsing: ../vendor/hhvm/hhast with xyzzy in repo auth mode took 29.2615 megabytes at peak.
                                   ^^^^^ https://www.rfc-editor.org/rfc/rfc3092.txt
```

I am looking forward to the release in January or March at the latest. It will probably [go live on Github](https://github.com/hershel-theodore-layton/portable-hack-ast) a couple weeks before a proper release. So if this excites you, keep an eye out.

### Enjoy the festivities

If the next blog post is released on schedule, I am expecting to title the next post `January 2024`. Enjoy the festive month and happy new year!

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
