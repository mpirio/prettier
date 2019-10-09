<!--

NOTE: Don't forget to add a link to your GitHub profile and the PR in the end of the file.

Format:

#### Category: Title ([#PR] by [@user])

Description

```
// Input
Code Sample

// Output (Prettier stable)
Code Sample

// Output (Prettier master)
Code Sample
```

Details:

  Description: optional if the `Title` is enough to explain everything.

Examples:

#### TypeScript: Correctly handle `//` in TSX ([#5728] by [@JamesHenry])

Previously, putting `//` as a child of a JSX element in TypeScript led to an error
because it was interpreted as a comment. Prettier master fixes this issue.

<!-- prettier-ignore --\>
```js
// Input
const link = <a href="example.com">http://example.com</a>

// Output (Prettier stable)
// Error: Comment location overlaps with node location

// Output (Prettier master)
const link = <a href="example.com">http://example.com</a>;
```

-->

#### JavaScript: More readable parentheses for new-call ([#6412] by [@bakkot])

<!-- prettier-ignore -->
```js
// Input
var a = new (x().y)();
var a = new (x().y.z)();
var a = new (x().y().z)();

// Output (Prettier stable)
var a = new (x()).y();
var a = new (x()).y.z();
var a = new (x().y()).z();

// Output (Prettier master)
var a = new (x().y)();
var a = new (x().y.z)();
var a = new (x().y().z)();
```

#### MDX: fix text with whitespace after JSX trim incorrectly ([#6340] by [@JounQin])

Previous versions format text with whitespace after JSX incorrectly in mdx, this has been fixed in this version.

<!-- prettier-ignore -->
```md
<!-- Input -->
# Heading
<Hello>
    test   <World />   test
</Hello>       123

<!-- Output (Prettier stable) -->
<Hello>
  test <World /> test
</Hello>123

<!-- Output (Prettier master) -->
<Hello>
  test <World /> test
</Hello> 123
```

#### TypeScript/Flow: Union types inside of tuples ([#6381] by [@squidfunk])

Previous versions would double-indent multi-line union types inside of
tuples for TypeScipt and Flow and add a new line:

<!-- prettier-ignore -->
```ts
// Input
type B = [
  | AAAAAAAAAAAAAAAAAAAAAA
  | BBBBBBBBBBBBBBBBBBBBBB
  | CCCCCCCCCCCCCCCCCCCCCC
  | DDDDDDDDDDDDDDDDDDDDDD
]

type C = [
  | [AAAAAAAAAAAAAAAAAAAAAA | BBBBBBBBBBBBBBBBBBBBBB | CCCCCCCCCCCCCCCCCCCCCC | DDDDDDDDDDDDDDDDDDDDDD]
  | [AAAAAAAAAAAAAAAAAAAAAA | BBBBBBBBBBBBBBBBBBBBBB | CCCCCCCCCCCCCCCCCCCCCC | DDDDDDDDDDDDDDDDDDDDDD]
]

// Output (Prettier stable)
type B = [

    | AAAAAAAAAAAAAAAAAAAAAA
    | BBBBBBBBBBBBBBBBBBBBBB
    | CCCCCCCCCCCCCCCCCCCCCC
    | DDDDDDDDDDDDDDDDDDDDDD
];

type C = [

    | [

          | AAAAAAAAAAAAAAAAAAAAAA
          | BBBBBBBBBBBBBBBBBBBBBB
          | CCCCCCCCCCCCCCCCCCCCCC
          | DDDDDDDDDDDDDDDDDDDDDD
    ]
    | [

          | AAAAAAAAAAAAAAAAAAAAAA
          | BBBBBBBBBBBBBBBBBBBBBB
          | CCCCCCCCCCCCCCCCCCCCCC
          | DDDDDDDDDDDDDDDDDDDDDD
    ]
];

// Output (Prettier master)
type B = [
  | AAAAAAAAAAAAAAAAAAAAAA
  | BBBBBBBBBBBBBBBBBBBBBB
  | CCCCCCCCCCCCCCCCCCCCCC
  | DDDDDDDDDDDDDDDDDDDDDD
];

type C = [
  | [
      | AAAAAAAAAAAAAAAAAAAAAA
      | BBBBBBBBBBBBBBBBBBBBBB
      | CCCCCCCCCCCCCCCCCCCCCC
      | DDDDDDDDDDDDDDDDDDDDDD
    ]
  | [
      | AAAAAAAAAAAAAAAAAAAAAA
      | BBBBBBBBBBBBBBBBBBBBBB
      | CCCCCCCCCCCCCCCCCCCCCC
      | DDDDDDDDDDDDDDDDDDDDDD
    ]
];
```

#### MDX: Adjacent JSX elements should be allowed in mdx ([#6332] by [@JounQin])

Previous versions would not format adjacent JSX elements in mdx, this has been fixed in this version.

<!-- prettier-ignore -->
```jsx
// Input
<Hello>
    test   <World />   test
</Hello>123

// Output (Prettier stable)
SyntaxError: Unexpected token (3:9)
  1 | <Hello>
  2 |     test   <World />   test
> 3 | </Hello>123
    |         ^

// Output (Prettier master)
<Hello>
  test <World /> test
</Hello>123


// Input
<Hello>
    test   <World />   test
</Hello>
<Hello>
    test   <World />   test
</Hello>123

// Output (Prettier stable)
SyntaxError: Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX fragment <>...</>? (4:1)
  2 |     test   <World />   test
  3 | </Hello>
> 4 | <Hello>
    | ^
  5 |     test   <World />   test
  6 | </Hello>123

// Output (Prettier master)
<Hello>
  test <World /> test
</Hello>
<Hello>
  test <World /> test
</Hello>123
```

#### TypeScript: Print comment following a JSX element with generic ([#6209] by [@duailibe])

Previous versions would not print this comment, this has been fixed in this version.

<!-- prettier-ignore -->
```ts
// Input
const comp = (
  <Foo<number>
    // This comment goes missing
    value={4}
  >
    Test
  </Foo>
);

// Output (Prettier stable)
const comp = <Foo<number> value={4}>Test</Foo>;

// Output (Prettier master)
const comp = (
  <Foo<number>
    // This comment goes missing
    value={4}
  >
    Test
  </Foo>
);
```

### Handlebars: Avoid adding unwanted line breaks between text and mustaches ([#6186] by [@gavinjoyce])

Previously, Prettier added line breaks between text and mustaches which resulted in unwanted whitespace in rendered output.

<!-- prettier-ignore -->
```hbs
// Input
<p>Your username is @{{name}}</p>
<p>Hi {{firstName}} {{lastName}}</p>

// Output (Prettier stable)
<p>
  Your username is @
  {{name}}
</p>
<p>
  Hi
  {{firstName}}
  {{lastName}}
</p>

// Output (Prettier master)
<p>
  Your username is @{{name}}
</p>
<p>
  Hi {{firstName}} {{lastName}}
</p>
```

### Handlebars: Improve comment formatting ([#6206] by [@gavinjoyce])

Previously, Prettier would sometimes ignore whitespace when formatting comments.

<!-- prettier-ignore -->
```hbs
// Input
<div>
  {{! Foo }}
  {{#if @foo}}
    Foo
  {{/if}}

  {{! Bar }}
  {{#if @bar}}
    Bar
  {{/if}}
</div>

// Output (Prettier stable)
<div>
  {{! Foo }}
  {{#if @foo}}
    Foo
  {{/if}}{{! Bar }}{{#if @bar}}
    Bar
  {{/if}}
</div>

// Output (Prettier master)
<div>
  {{! Foo }}
  {{#if @foo}}
    Foo
  {{/if}}
  {{! Bar }}
  {{#if @bar}}
    Bar
  {{/if}}
</div>
```

#### JavaScript: Update ?? precedence to match stage 3 proposal ([#6404] by [@vjeux])

We've updated Prettier's support for the nullish coalescing operator to match a spec update that no longer allows it to immediately contain, or be contained within an `&&` or `||` operation.

<!-- prettier-ignore -->
```js
// Input
(foo ?? baz) || baz;

// Output (Prettier stable)
foo ?? baz || baz;

// Output (Prettier master)
(foo ?? baz) || baz;
```

Please note, as we update our parsers with versions that support this spec update, code without the parenthesis will throw a parse error.

#### JavaScript: Keep unary expressions parentheses with comments ([#6217] by [@sosukesuzuki])

Previously, Prettier removes parentheses enclose unary expressions. This change modify to keep it when the expression has comments.

<!-- prettier-ignore -->
```ts
// Input
!(
  /* foo */
  foo
);
!(
  foo // foo
);

// Output (Prettier stable)
!/* foo */
foo;
!foo; // foo

// Output (Prettier master)
!(/* foo */ foo);
!(
  foo // foo
);
```

### Javascript: Use function literals in arguments to detect function composition ([#6033] by [@brainkim])

Previously, we used a set of hard-coded names related to functional programming
(`compose`, `flow`, `pipe`, etc.) to detect function composition and chaining
patterns in code. This was done so that prettier would not put code like the
following call to `pipe` on the same line even if it fit within the allotted
column budget:

<!-- prettier-ignore -->
```js
source$
  .pipe(
    filter(x => x % 2 === 0),
    map(x => x + x),
    scan((acc, x) => acc + x, 0),
  )
  .subscribe(x => console.log(x));
```

However, this heuristic caused people to complain because of false positives
where calls to functions or methods matching the hard-coded names would always
be split on multiple lines, even if the calls did not contain function
arguments (https://github.com/prettier/prettier/issues/5769,
https://github.com/prettier/prettier/issues/5969). For many, this blanket
decision to split functions based on name was both surprising and sub-optimal.

We now use a refined heuristic which uses the presence of function literals to
detect function composition. This heuristic preserves the line-splitting
behavior above and eliminates many if not all of the false positives caused by
the older heuristic.

We encourage prettier users to try out the new heuristic and provide feedback.

<!-- prettier-ignore -->
```js
// Input
eventStore.update(id, _.flow(updater, incrementVersion));

// Output (Prettier stable)
eventStore.update(
  id,
  _.flow(
    updater,
    incrementVersion
  )
);

// Output (Prettier master)
eventStore.update(id, _.flow(updater, incrementVersion));
```

### Handlebars: Improve comment formatting ([#6234] by [@gavinjoyce])

Previously, Prettier would incorrectly decode HTML entiites.

<!-- prettier-ignore -->
```hbs
// Input
<p>
  Some escaped characters: &lt; &gt; &amp;
</p>

// Output (Prettier stable)
<p>
  Some escaped characters: < > &
</p>

// Output (Prettier master)
<p>
  Some escaped characters: &lt; &gt; &amp;
</p>
```

#### JavaScript: Stop moving comments inside tagged template literals ([#6236] by [@sosukesuzuki])

Previously, Prettier would move comments after the tag inside the template literal. This version fixes this problem.

<!-- prettier-ignore -->
```js
// Input
foo //comment
`
`;

// Output (Prettier stable)
foo` // comment
`;

// Output (Prettier master)
foo // comment
`
`;
```

#### JavaScript: Fix moving comments in function calls like `useEffect` second argument ([#6270] by [@sosukesuzuki])

This fixes a bug that was affecting function calls that have a arrow function as first argument and an array expression as second argument, such as the common React's `useEffect`. A comment in its own line before the second argument would be moved to the line above.

The bug was only present when using the Flow and TypeScript parsers.

<!-- prettier-ignore -->
```js
// Input
useEffect(
  () => {
    console.log("some code", props.foo);
  },

  // We need to disable the eslint warning here,
  // because of some complicated reason.
  // eslint-disable line react-hooks/exhaustive-deps
  []
);

// Output (Prettier stable)
useEffect(() => {
  console.log("some code", props.foo);
}, // We need to disable the eslint warning here,
// because of some complicated reason.
// eslint-disable line react-hooks/exhaustive-deps
[]);

// Output (Prettier master)
useEffect(
  () => {
    console.log("some code", props.foo);
  },

  // We need to disable the eslint warning here,
  // because of some complicated reason.
  // eslint-disable line react-hooks/exhaustive-deps
  []
);
```

#### TypeScript: Fix crashes when using `//` in JSX texts ([#6289] by [@duailibe])

This version updates the TypeScript parser to correctly handle JSX text with double slashes (`//`). In previous versions, this would cause Prettier to crash.

#### HTML, Vue: Don't break the template element included in a line shorter than print-width([#6284] by [@sosukesuzuki])

Previously, even if the line length is shorter than print-width is Prettier breaks the line with a template element.

<!-- prettier-ignore -->
```html
// Input
<template>
  <template>foo</template>
</template>

// Output (Prettier stable)
<template>
  <template
    >foo</template
  >
</template>

// Output (Prettier master)
<template>
  <template>foo</template>
</template>
```

#### JavaScript: Fix breaks indentation and idempotency when an arrow function that args include object pattern is passed to a function as parameter. ([#6301] by [@sosukesuzuki])

Previously, Prettier collapses strangely, when an arrow function that args include object pattern is passed to a function as parameter. Also, it breaks idempotency. Please see [#6294](https://github.com/prettier/prettier/issues/6294) for detail.

<!-- prettier-ignore -->
```js
// Input
foo(
  ({
    a,

    b
  }) => {}
);

// Output (Prettier stable)
foo(({ a,
  b }) => {});

// Output (Prettier master)
foo(
  ({
    a,

    b
  }) => {}
);
```

#### TypeScript: Fix specific union type breaks after opening parenthesis, but not before closing ([#6307] by [@sosukesuzuki])

Previously, union type that put with `as` , `keyof`, `[]`, other union(`|`) and intersection(`&`) breaks after opening parenthesis, but not before closing. Please see [#6303](https://github.com/prettier/prettier/issues/6303) for detail.

<!-- prettier-ignore-->
```ts
// Input
const foo = [abc, def, ghi, jkl, mno, pqr, stu, vwx, yz] as (
  | string
  | undefined
)[];

// Prettier (stable)
const foo = [abc, def, ghi, jkl, mno, pqr, stu, vwx, yz] as (
  | string
  | undefined)[];

// Prettier (master)
const foo = [abc, def, ghi, jkl, mno, pqr, stu, vwx, yz] as (
  | string
  | undefined
)[];
```

#### HTML: Script tags are now treated as blocks for the purposes of formatting ([#6423] by [@thorn0])

Previously, in the [whitespace-sensitive mode](https://prettier.io/docs/en/options.html#html-whitespace-sensitivity), they were formatted as if they were inline.

<!-- prettier-ignore-->
```html
<!-- Input -->
<script
  async
  src="/_next/static/development/pages/_app.js?ts=1565732195968"
></script><script></script>

<!-- Prettier (stable) -->
<script
  async
  src="/_next/static/development/pages/_app.js?ts=1565732195968"
></script
><script></script>

<!-- Prettier (master) -->
<script
  async
  src="/_next/static/development/pages/_app.js?ts=1565732195968"
></script>
<script></script>
```

#### TypeScript: Fixed to break line and add a semicolon in one execution on one line long mapped types ([#6420] by [@sosukesuzuki])

Previously, when Prettier formatted long, one-line mapped types, it would break the line but didn’t add a semicolon – until you ran Prettier again (which broke Prettier’s idempotency rule). Now, Prettier adds the semicolon in the first run, fixing the issue.

<!-- prettier-ignore -->
```ts
// Input
type FooBar<T> = { [P in keyof T]: T[P] extends Something ? Something<T[P]> : T[P] }

// Prettier (stable)
type FooBar<T> = {
  [P in keyof T]: T[P] extends Something ? Something<T[P]> : T[P]
};

// Prettier (master)
type FooBar<T> = {
  [P in keyof T]: T[P] extends Something ? Something<T[P]> : T[P];
};
```

#### JavaScript: Fix ugly formatting on object destructuring with parameter decorators ([#6411] by [@sosukesuzuki])

Previously, Prettier formatted decorators for destructured parameters in a weird way. Now, parameter decorators are placed just above the parameter they belong to.

<!-- prettier-ignore -->
```js
// Input
class Class {
  method(
    @decorator
     { foo }
  ) {}
}

// Prettier (stable)
class Class {
  method(@decorator
  {
    foo
  }) {}
}

// Prettier (master)
class Class {
  method(
    @decorator
    { foo }
  ) {}
}
```

#### JavaScript: Handle empty object patterns with type annotations in function parameters ([#6438] by [@bakkot])

<!-- prettier-ignore -->
```js
// Input
const f = ({}: MyVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongType) => {};
function g({}: Foo) {}

// Output (Prettier stable)
const f = ({
  ,
}: MyVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongType) => {};
function g({  }: Foo) {}

// Output (Prettier master)
const f = ({}: MyVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryVeryLongType) => {};
function g({}: Foo) {}
```

#### JavaScript: Fix ugly formatting parens wrap binary expressions within call expressions ([#6441] by [@sosukesuzuki])

Previously, Prettier formatted parens wrap binary expressions within call expressions in a weird way. There was no line break before and after each parens.

<!-- prettier-ignore -->
```js
(
  aaaaaaaaaaaaaaaaaaaaaaaaa &&
  bbbbbbbbbbbbbbbbbbbbbbbbb &&
  ccccccccccccccccccccccccc &&
  ddddddddddddddddddddddddd &&
  eeeeeeeeeeeeeeeeeeeeeeeee
)();

// Prettier (stable)
(aaaaaaaaaaaaaaaaaaaaaaaaa &&
  bbbbbbbbbbbbbbbbbbbbbbbbb &&
  ccccccccccccccccccccccccc &&
  ddddddddddddddddddddddddd &&
  eeeeeeeeeeeeeeeeeeeeeeeee)();

// Prettier (master)
(
  aaaaaaaaaaaaaaaaaaaaaaaaa &&
  bbbbbbbbbbbbbbbbbbbbbbbbb &&
  ccccccccccccccccccccccccc &&
  ddddddddddddddddddddddddd &&
  eeeeeeeeeeeeeeeeeeeeeeeee
)();
```

#### JavaScript: Fix formatting on long named exports ([#6446] by [@sosukesuzuki])

Previously, Prettier formatted long named exports differently than named imports.

```js
// Input
export { fooooooooooooooooooooooooooooooooooooooooooooooooo } from "fooooooooooooooooooooooooooooo";

// Prettier (stable)
export {
  fooooooooooooooooooooooooooooooooooooooooooooooooo
} from "fooooooooooooooooooooooooooooo";

// Prettier (master)
export { fooooooooooooooooooooooooooooooooooooooooooooooooo } from "fooooooooooooooooooooooooooooo";
```

#### JavaScript: Fix bad formatting for multi-line optional chaining with comment ([#6506] by [@sosukesuzuki])

<!-- prettier-ignore -->
```js
// Input
return a
  .b()
  .c()
  // Comment
  ?.d()

// Prettier (stable)
return a
  .b()
  .c()
  ?.// Comment
  d();

// Prettier (master)
return (
  a
    .b()
    .c()
    // Comment
    ?.d()
);
```

#### JavaScript: Fix inconsistent indentation in switch statement ([#6514] by [@sosukesuzuki])

<!-- prettier-ignore -->
```js
// Input
switch ($veryLongAndVeryVerboseVariableName && $anotherVeryLongAndVeryVerboseVariableName) {
}

switch ($longButSlightlyShorterVariableName && $anotherSlightlyShorterVariableName) {
}

// Prettier (stable)
switch (
  $veryLongAndVeryVerboseVariableName &&
    $anotherVeryLongAndVeryVerboseVariableName
) {
}

switch (
  $longButSlightlyShorterVariableName && $anotherSlightlyShorterVariableName
) {
}

// Prettier (master)
switch (
  $veryLongAndVeryVerboseVariableName &&
  $anotherVeryLongAndVeryVerboseVariableName
) {
}

switch (
  $longButSlightlyShorterVariableName &&
  $anotherSlightlyShorterVariableName
) {
}
```

#### TypeScript: Keep type parameters inline for a type annotation of variable declaration ([#6467] by [@sosukesuzuki])

<!-- prettier-ignore -->
```ts
// Input
const fooooooooooooooo: SomeThing<boolean> = looooooooooooooooooooooooooooooongNameFunc();

// Prettier (stable)
const fooooooooooooooo: SomeThing<
  boolean
> = looooooooooooooooooooooooooooooongNameFunc();

// Prettier (master)
const fooooooooooooooo: SomeThing<boolean> = looooooooooooooooooooooooooooooongNameFunc();
```

#### Handlebars: Fix --single-quote option on html attributes ([#6377] by [@dcyriller])

Previously, the flag was not applied on html attributes.

<!-- prettier-ignore-->
```hbs
// Input
<div class="a-class-name"></div>

// Prettier (stable with the option --single-quote)
<div class="a-class-name"></div>

// Prettier (master with the option --single-quote)
<div class='a-class-name'></div>
```

#### TypeScript: Fix incorrectly removes double parentheses around types ([#6604] by [@sosukesuzuki])

<!-- prettier-ignore -->
```ts
// Input
type A = 0 extends ((1 extends 2  ? 3 : 4)) ? 5 : 6;
type B = ((0 extends 1 ? 2 : 3)) extends 4 ? 5 : 6:
type C = ((number | string))["toString"];
type D = ((keyof T1))["foo"];

// Prettier (stable)
type A = 0 extends 1 extends 2 ? 3 : 4 ? 5 : 6;
type B = 0 extends 1 ? 2 : 3 extends 4 ? 5 : 6;
type C = number | string["toString"];
type D = keyof T1["foo"];

// Prettier (master)
type A = 0 extends (1 extends 2 ? 3 : 4) ? 5 : 6;
type B = (0 extends 1 ? 2 : 3) extends 4 ? 5 : 6;
type C = (number | string)["toString"];
type D = (keyof T1)["foo"];
```

#### JavaScript: Support formatting code with V8 intrinsics. ([#6496] by [@rreverser])

<!-- prettier-ignore -->
```js
// Input
function doSmth()     {
            %DebugPrint
        (
                foo )
  }

// Prettier (stable)
SyntaxError: Unexpected token (2:13)
  1 | function doSmth()     {
> 2 |             %DebugPrint
    |             ^

// Prettier (master)
function doSmth() {
  %DebugPrint(foo);
}
```

#### JavaScript: Manage "Stroustrup" brace style ([#] by [@mpirio])

Manage Stroustrup brace style, in which the `else` statements in an `if-else` construct, as well as `catch` and `finally`, must be on its own line after the preceding closing brace.

With `braceStyle: "stroustrup"`:

<!-- prettier-ignore -->
```js
// Input
if (a) { b = 2; } else { b = 3; }

if (a) {
    b = 2;
} else {
    b = 3;
}

do {
    b++;
} while (a)

try {
    a = 1;
} catch (error) {
    console.error(error);
} finally {
    b = 2;
}

// Output (Prettier stable)
if (a) {
  b = 2;
} else {
  b = 3;
}

if (a) {
  b = 2;
} else {
  b = 3;
}

do {
  b++;
} while (a);

try {
  a = 1;
} catch (error) {
  console.error(error);
} finally {
  b = 2;
}

// Output (Prettier master)
if (a) {
  b = 2;
}
else {
  b = 3;
}

if (a) {
  b = 2;
}
else {
  b = 3;
}

do {
  b++;
} while (a);

try {
  a = 1;
}
catch (error) {
  console.error(error);
}
finally {
  b = 2;
}
```

[#5910]: https://github.com/prettier/prettier/pull/5910
[#6033]: https://github.com/prettier/prettier/pull/6033
[#6186]: https://github.com/prettier/prettier/pull/6186
[#6206]: https://github.com/prettier/prettier/pull/6206
[#6209]: https://github.com/prettier/prettier/pull/6209
[#6217]: https://github.com/prettier/prettier/pull/6217
[#6234]: https://github.com/prettier/prettier/pull/6234
[#6236]: https://github.com/prettier/prettier/pull/6236
[#6270]: https://github.com/prettier/prettier/pull/6270
[#6289]: https://github.com/prettier/prettier/pull/6289
[#6284]: https://github.com/prettier/prettier/pull/6284
[#6301]: https://github.com/prettier/prettier/pull/6301
[#6307]: https://github.com/prettier/prettier/pull/6307
[#6332]: https://github.com/prettier/prettier/pull/6332
[#6340]: https://github.com/prettier/prettier/pull/6340
[#6412]: https://github.com/prettier/prettier/pull/6412
[#6423]: https://github.com/prettier/prettier/pull/6423
[#6420]: https://github.com/prettier/prettier/pull/6420
[#6411]: https://github.com/prettier/prettier/pull/6411
[#6438]: https://github.com/prettier/prettier/pull/6411
[#6441]: https://github.com/prettier/prettier/pull/6441
[#6446]: https://github.com/prettier/prettier/pull/6446
[#6506]: https://github.com/prettier/prettier/pull/6506
[#6514]: https://github.com/prettier/prettier/pull/6514
[#6467]: https://github.com/prettier/prettier/pull/6467
[#6377]: https://github.com/prettier/prettier/pull/6377
[#6604]: https://github.com/prettier/prettier/pull/6604
[#6496]: https://github.com/prettier/prettier/pull/6496
[@brainkim]: https://github.com/brainkim
[@duailibe]: https://github.com/duailibe
[@gavinjoyce]: https://github.com/gavinjoyce
[@sosukesuzuki]: https://github.com/sosukesuzuki
[@g-harel]: https://github.com/g-harel
[@jounqin]: https://github.com/JounQin
[@bakkot]: https://gibhub.com/bakkot
[@thorn0]: https://github.com/thorn0
[@dcyriller]: https://github.com/dcyriller
[@rreverser]: https://github.com/RReverser
[@mpirio]: https://github.com/mpirio
