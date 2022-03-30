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

### SgmlStream has been open for a year

I almost forgot to mention this. The [first release of SGMLStream](https://github.com/hershel-theodore-layton/sgml-stream/releases/tag/v0.2.0) was made in March of 2021. SGMLStream has been relatively stable in this year. `$this->tagName` was removed in favor of `static::TAG_NAME`. This was signalled for removal in advance and the upgrade path was clear. **A breaking change is expected!**

SGMLStream has one mechanism for moving arbitrary data through a tree. This mechanism is [Flow](https://github.com/hershel-theodore-layton/sgml-stream/blob/v0.2.0/src/element/SimpleUserElement.hack#L21), which moves data from ancestor to descendant.

```HTML
<T1 data-flows-to="2,3,4,5,6">
  <T2 data-flows-to="3,4">
    <T3 data-flows-to="null"/>
    <T4 data-flows-to="null"/>
  </T2>
  <T5 data-flows-to="6">
    <T6 data-flows-to="null"/>
  </T5>
</T1>
```

It was possible to use a mutable object to pass data between elements that were not descendants, but this was unstructured and created an opening for bugs that depended on the order of execution.

```HACK
final xhp class T6 extends SimpleUserElementWithWritableFlow {
  <<__Override>>
  final protected function compose(WritableFlow $flow): Streamable {
    $mut = $flow->get('!MUTABLE_REFERENCE_TO_VEC_OF_INT') as MyMutableVecOfInt;
    $mut->value[] = 42;
    return <div class="t6" data-vec-so-far={Str\join($mut->value, ', ')} />;
  }
}
```

The value of `data-vec-so-far` depends on the order of execution of T3 and T6. If both T2 and T5 are AsynchronousUserElements. The value is not predictable.

There are use cases for a data stream which flows in document order. A Flow object for which the order of writes is specified to be the same as the document order. For example, registering some javascript that needs to run in T1-5 and writing out this javascript in a `<script></script>` tag in T6. The javascript must be written in the same order on each render, so a `!MUTABLE_REFERENCE_TO_VEC_OF_STRING` would not be desired. There is already an ordered execution of [`->feedBytesToConsumerAsync()`](https://github.com/hershel-theodore-layton/sgml-stream/blob/v0.7.1/src/snippet/ComposableSnippet.hack#L50). This method could get the responsibilities of propagating a Flow object. The exact interface and method of this interaction has not yet been though out.

The [Magnetite v0.4.0 release](https://github.com/hershel-theodore-layton/sgml-stream/releases/tag/v0.4.0) introduced the [DissolableUserElement](https://github.com/hershel-theodore-layton/sgml-stream/blob/v0.4.0/src/element/DissolvableElement.hack). This element can not have access to the Flow, since it is composed in the [`->placeIntoSnippetStream()`](https://github.com/hershel-theodore-layton/sgml-stream/blob/v0.4.0/src/element/DissolvableElement.hack#L41) step instead of the `->primeAsync()` step. This is not an issue for simple elements like `<PictureTag webp="file.webp" jpg="file.jpg" />`. Some elements need access to information that is global to the document, f.e. has-admin-permissions. This information is already known at the `->placeIntoSnippetStream()` step, but there was no way to provide this information. A third, read-only Flow could be passed through `->placeIntoSnippetStream(SnippedStream, Flow)` to allow `<MyMenu />` to access document global information, like the permissions of the user, without needing to be a `SimpleUserElement`.

These two extra mechanisms would complete story about data flowing through an SGMLStream tree:

Classic Flow:
```
This direction
--------------->
<T1>
  <T2>
    <T3 />
  </T2>
  <T4 />
</T1>
```

Document order Flow:
```
This direction
|<T1>
|  <T2>
|    <T3 />
|  </T2>
|  <T4 />
|</T1>
V
```

Read only document wide Flow to meat use cases where there is no direction needed (information known in advance).

For obvious reasons, flows in the `>` (to descendants) and `V` (to successors) directions are the only ones that we can provide whilst retaining SGMLStreams signature ability. Flows in the `<` (to ancestors) and `^` (to predecessors) direction are not something worth building, since they would inhibit streaming.

## [January 2022](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-01.md)
## [SGMLStream Sillimanite Release](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2022-release-announcement-sgml-stream-sillimanite.md)
## [November 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-11.md)
## [September 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-09.md)
## [July 2021](https://github.com/hershel-theodore-layton/hershel-theodore-layton/blob/master/2021-07.md)
