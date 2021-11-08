# Blog

_Typo here, typo there, typos everywhere._

## September 2021

### HHVM version support

At the time of writing, we're mere moments away from the release of [hhvm version 4.128](https://hhvm.com/blog/2021/09/21/hhvm-4.128.html), which will be an LTS release. I'd like to congratulate the hhvm team on their amazing achievements. Hhvm is a lot more stable than it was a few years ago. Most runtime breaking changes only affect ill-typed code. Breaking changes from the typechecker are often easy to fix and it is easy to remain compatible with older versions whilst supporting newer ones.

With the release of [hhvm version 4.128](https://hhvm.com/blog/2021/09/21/hhvm-4.128.html), [hhvm version 4.80](https://hhvm.com/blog/2020/10/21/hhvm-4.80.html) will lose official support from Facebook. As stated in the [July 2021 post](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md) I do not intend to drop support for [hhvm version 4.73](https://hhvm.com/blog/2020/09/02/hhvm-4.73.html) just yet. This is not a promise for the future. There are a couple hhvm features in [hhvm version 4.102](https://hhvm.com/blog/2021/03/29/extending-hhvm-4.102-support.html) that I'd like to use, and I may drop support for older hhvm versions in the near future.

I want to express concern if you are running an application on [hhvm version 4.101](https://hhvm.com/blog/2021/03/16/hhvm-4.101.html) or older. Just to be cristal clear, I do not have a use for hhvm 4.73 support myself. My applications either run on the latest LTS or on a minor release which is still supported by Facebook. **Upgrading should be a priority for you.** The oldest hhvm version that Facebook supports will be [hhvm version 4.102](https://hhvm.com/blog/2021/03/29/extending-hhvm-4.102-support.html). I **strongly** recommend upgrading.

### Coeffects and capabilities support

The square bracket coeffect syntax `function add_pure(int $a, int $b)[]: int { return $a + $b; }` has been available since [hhvm version 4.93](https://hhvm.com/blog/2021/01/19/hhvm-4.93.html). This means I won't be able to adopt coeffects and capabilities without dropping support for older hhvm versions. All functions and methods from my packages have had the implicit `[defaults]` capability set. I am hesitant to adopt this language feature, since this landscape is still in flux. If the lack of coeffect annotations is limiting your adoption of one or more packages, please let me know.

### Concrete plans for sgml-stream

[Sgml-stream](https://github.com/hershel-theodore-layton/sgml-stream) exposes traits that render elements to strings:
 - [ElementWithOpenAndCloseTags](https://github.com/hershel-theodore-layton/sgml-stream/blob/0e102c9a99aebc4b6904fafbcf09bdf1e1358f3c/src/rendering/ElementWithOpenAndCloseTags.hack)
 - [ElementWithOpenAndCloseTagsAndUnescapedContent](https://github.com/hershel-theodore-layton/sgml-stream/blob/0e102c9a99aebc4b6904fafbcf09bdf1e1358f3c/src/rendering/ElementWithOpenAndCloseTagsAndUnescapedContent.hack)
 - [ElementWithOpenTagOnly](https://github.com/hershel-theodore-layton/sgml-stream/blob/0e102c9a99aebc4b6904fafbcf09bdf1e1358f3c/src/rendering/ElementWithOpenTagOnly.hack)

They have had the following annotation for the longest time.


```HACK
<<_Private\UnstableAPI(
  'This property is intended to mimic a constant. Constants in traits are '.
  'supported since https://hhvm.com/blog/2021/02/16/hhvm-4.97.html',
)>>
protected string $tagName;
```

If you depend on the tag name being a mutable property (as opposed to an immutable constant), please voice your concerns. As soon as hhvm 4.73 support is dropped, this property will become an abstract constant.

[RootElement](https://github.com/hershel-theodore-layton/sgml-stream/blob/0e102c9a99aebc4b6904fafbcf09bdf1e1358f3c/src/element/RootElement.hack#L267-L309) has had a couple of dunder methods that were unused and throw an `\Error` when called. I intend to remove them. This means that old xhp syntax such as `children %pcdata` and `category %flow` will always be rejected.

### Autoloading using `ext_facts`

[Hhvm version 4.109](https://hhvm.com/blog/2021/05/11/hhvm-4.109.html) launched with an amazing autoloader, the watchman based native autoloader. It is a great developer experience to not have to worry about having an out of date autoload map. Support for the userland autoloaders, mainly [hhvm-autoload](https://github.com/hhvm/hhvm-autoload), will remain in place. For users who have adopted the watchman autoloader, I now officially support its use. Make sure your watchman query covers the entire project directory and scans for `.hack` files. This has always worked, but it could be broken if I were to add `.php`, `.hh`, or `.hackpartial` files. I hereby promise all code will be published in `.hack` files. I will switch to using `useFactsIfAvailable` in the packages. This means that hhvm-autoload will pass through to `ext_facts` when developing the packages if you have watchman installed and configured the native autoloader.

### Type assertions using static-type-assertion-code-generator

You are welcome to check out [static-type-assertion-code-generator](https://github.com/hershel-theodore-layton/static-type-assertion-code-generator). The API is not yet stable, but the test coverage is complete and I have used it to optimize slow type-assert codepaths in my own applications. If you have feedback or questions before the API is declared stable and `v0.2` is released, let me know.



## [July 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md)
