# Blog

**Are you a C++ programmer? Have you built projects with CMake and clang before? The [HHVM Open Source project](https://github.com/facebook/hhvm) could use your help! See [the pinned issue](https://github.com/hershel-theodore-layton/hershel-theodore-layton/issues/2).**

_Typo here, typo there, typos everywhere._

### IDE integration

The latest version [Gold - patch 3](https://github.com/hershel-theodore-layton/dead-simple-lint-server-integration/releases/tag/v1.0.3)
of the vscode extension [DeadSimpleLintServerIntegration](https://github.com/hershel-theodore-a-layton/dead-simple-lint-server-integration) includes autofix support.
Autofixes from the linters can now be applied with a Code Action.

![Screenshot from 2024-12-05 22-07-43](https://github.com/user-attachments/assets/7846b036-6294-4a75-8e02-7ccc703c73dc)
![Screenshot from 2024-12-05 22-07-53](https://github.com/user-attachments/assets/bcef8e9a-5885-46e9-952c-7f6f6961a14b)

### Linter Autofix Improvements

_What good is an IDE autofix button if there aren't enough autofixes?_

The folliowing linters now include autofixes:

- dont_discard_new_expressions_linter
  - Uses an explicit discard `$_ = new MyClass();`.
- final_or_abstract_classes_linter
  - Make the class `final`. This will introduce errors if there are subclasses.
- group_use_statement_alphabetization_linter
  - Sorts `X\{B, A}` to `X\{A, B}`
- license_header_linter
  - Inserts a license header, below the `#! sheebang` or`<?hh` lines, else on the first line.
- must_use_braces_for_control_flow_linter
  - Wraps the body of the statement in `{}`, requires a reformat in all cases.
- no_elseif_linter
  - Replaces `elseif` with `else if`
- no_empty_statements_linter
  - Uses an explicit discard `$_ = 1 + 1;`, except for the empty statement `;`, which it will not fix.
- no_final_method_in_final_classes_linter
  - Removes `final` from the methods.
- no_php_equality_linter
  - Replaces `==` with `===`, and `!=` with `!==`. Careful, this might break behavior you replied upon.
- prefer_require_once_linter
  - Replaces `require 'filename'` with `require_once 'filename'`
- prefer_single_quoted_string_literals_linter
  - Replaces `"hello"` with `'hello'`
- unused_variable_linter
  - Replaces `$unused = 1` with `$_unused = 1`. Careful, this might break if `$_unused` was already used in this scope.
- pragma_could_not_be_parsed_linter
  - Will remove `pragma('PhaLinters', 'unknown:x)` and `Pragmas(vec['PhaLinters', 'unknown:x'])`.
  - If removing an attribute creates an empty attribute list f.e. `<<Pragmas(...)>>` would become `<<>>`, the `<<` and `>>` are removed.
  - If are least one of the directives is valid, the pragma is not fixed, f.e. `Pragmas(vec['PhaLinters', 'digest:...], vec['PhaLinters', 'unknown:x'])`

### New Linters

Two new linters were added:

- `solitary_escape_sequences_should_be_disambiguated_linter`
- `shape_type_additional_field_intent_should_be_explicit_linter`

The former requires you to replace `'\n'` with `'\\n'`, since `'\n'` is a
single newline character is many language (other than Hack). `\\n` isn't a valid
character literal in C-like languages.

The latter requires you to place something `shape('x' => int <%here%>)` in closed
shape type literals. Open shape type literals (shapes with `...`) do not require
your suffix. This eliminates the possibility that the option of an open shape
was not considered at authoring time.

### Updates for `shape_type_additional_field_intent_should_be_explicit_linter`

[TypeVisitor](https://github.com/hershel-theodore-layton/type-visitor) includes `closed_shape_suffix`
to allow you to codegen your closed shape literal types with a suffix.

[Static Type Assertion Code Generator](https://github.com/hershel-theodore-layton/static-type-assertion-code-generator)
includes the same option to codegen `as shape()` with a `closed_shape_suffix`.

### Bugfixes

[Static Type Assertion Code Generator](https://github.com/hershel-theodore-layton/static-type-assertion-code-generator)

User provided functions for aliasses that are not inherently nullable are not invoked
with `null` if the assertion codegen specifies `?YourType`.

[TypeVisitor](https://github.com/hershel-theodore-layton/type-visitor) will render
`?YourType` as `YourType` if `YourType` was a nullable alias, since the `?`
would be redundant.

### Portable Hack AST API

Two functions have been added to the PHA API:
- `node_get_code_without_leading_or_trailing_trivia`
- `node_is_token_text_trivium`

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
