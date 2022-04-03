[![Codecov](https://img.shields.io/codecov/c/github/ehmicky/wild-wild-utils.svg?label=tested&logo=codecov)](https://codecov.io/gh/ehmicky/wild-wild-utils)
[![Build](https://github.com/ehmicky/wild-wild-utils/workflows/Build/badge.svg)](https://github.com/ehmicky/wild-wild-utils/actions)
[![Node](https://img.shields.io/node/v/wild-wild-utils.svg?logo=node.js)](https://www.npmjs.com/package/wild-wild-utils)
[![Twitter](https://img.shields.io/badge/%E2%80%8B-twitter-4cc61e.svg?logo=twitter)](https://twitter.com/intent/follow?screen_name=ehmicky)
[![Medium](https://img.shields.io/badge/%E2%80%8B-medium-4cc61e.svg?logo=medium)](https://medium.com/@ehmicky)

🤠 Functional utilities using object property paths with wildcards and regexps.

Available functional methods include:

- Mapping: [`map()`](#maptarget-query-mapfunction-options)
- Merging/concatenating: [`merge()`](#mergetarget-query-value-options),
  [`push()`](#pushtarget-query-values-options),
  [`unshift()`](#unshifttarget-query-values-options)
- Finding: [`find()`](#findtarget-query-testfunction-options)
- Filtering: [`pick()`](#picktarget-query-options),
  [`include()`](#includetarget-query-testfunction-options),
  [`exclude()`](#excludetarget-query-testfunction-options)

Unlike similar libraries, object properties can be get/set using
[dot-delimited paths](https://github.com/ehmicky/wild-wild-path#deep-properties),
[wildcards](https://github.com/ehmicky/wild-wild-path#wildcards),
[regexps](https://github.com/ehmicky/wild-wild-path#regexps),
[slices](https://github.com/ehmicky/wild-wild-path#array-slices) and
[unions](https://github.com/ehmicky/wild-wild-path#unions). It is built on top
of [`wild-wild-path`](https://github.com/ehmicky/wild-wild-path).

# Install

```bash
npm install wild-wild-utils
```

This package is an ES module and must be loaded using
[an `import` or `import()` statement](https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c),
not `require()`.

# API

## Methods

### map(target, query, mapFunction, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`mapFunction`: `(value) => value`\
`options`: [`Options?`](#options)\
_Return value_: [`Target`](https://github.com/ehmicky/wild-wild-path#target)

Use a mapping function to modify any property matching the `query`.

### merge(target, query, value, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`value`: `object`\
`options`: [`Options?`](#options)\
_Return value_: [`Target`](https://github.com/ehmicky/wild-wild-path#target)

Merge an object `value` with all object properties matching the `query`. If
those properties are not objects, they are overridden instead. The merge is
shallow unless the [`deep`](#deep) option is `true`.

### push(target, query, values, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`values`: `any[]`\
`options`: [`Options?`](#options)\
_Return value_: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\

Concatenate an array of `values` with all array properties matching the `query`.
If those properties are not arrays, they are overridden instead.

### unshift(target, query, values, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`values`: `any[]`\
`options`: [`Options?`](#options)\
_Return value_: [`Target`](https://github.com/ehmicky/wild-wild-path#target)

Like [`push()`](#pushtarget-query-values-options) but concatenates at the
beginning of each property instead of the end.

### find(target, query, testFunction, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`testFunction`: `(value) => boolean`\
`options`: [`Options?`](#options)\
_Return value_: `any`

Return the first property that both match both the query and return `true` with
the `testFunction`.

### pick(target, query, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`options`: [`Options?`](#options)\
_Return value_: [`Target`](https://github.com/ehmicky/wild-wild-path#target)

Return an object including only the properties matching the query.

### include(target, query, testFunction, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`testFunction`: `(value) => boolean`\
`options`: [`Options?`](#options)\
_Return value_: [`Target`](https://github.com/ehmicky/wild-wild-path#target)

Return an object including only the properties that both match both the query
and return `true` with the `testFunction`.

### exclude(target, query, testFunction, options?)

`target`: [`Target`](https://github.com/ehmicky/wild-wild-path#target)\
`query`: [`Query`](https://github.com/ehmicky/wild-wild-path#queries)\
`testFunction`: `(value) => boolean`\
`options`: [`Options?`](#options)\
_Return value_: [`Target`](https://github.com/ehmicky/wild-wild-path#target)

Remove any property that both match the query and return `true` with the
`testFunction`.

## Target

The target value must be an object or an array. Additional documentation,
notably about
[`undefined` properties](https://github.com/ehmicky/wild-wild-path#undefined-values)
can be found [here](https://github.com/ehmicky/wild-wild-path#target).

## Query

The query format is documented
[here](https://github.com/ehmicky/wild-wild-path#queries). Both query
[strings](https://github.com/ehmicky/wild-wild-path#query-strings) and
[arrays](https://github.com/ehmicky/wild-wild-path#query-arrays) can be used.

## Options

Options are optional plain objects. They are almost
[the same as in `wild-wild-path`](https://github.com/ehmicky/wild-wild-path#options).

### mutate

_Methods_: \
_Type_: `boolean`\
_Default_: `false`

By default, the [target](#target) is deeply cloned.\
When `true`, it is directly mutated instead, which is faster but has side effects.

```js
const target = {}
console.log(set(target, 'name', 'Alice')) // { name: 'Alice' }
console.log(target) // {}
console.log(set(target, 'name', 'Alice', { mutate: true })) // { name: 'Alice' }
console.log(target) // { name: 'Alice' }
```

### entries

_Methods_: \
_Type_: `boolean`\
_Default_: `false`

By default, properties' values are returned.\
When `true`, objects with the following shape are returned instead:

- `value` `any`: property's value
- `path` [`Path`](#paths): property's full path
- `missing` `boolean`: whether the property is [missing](#missing) from the
  [target](#target)

```js
const target = { firstName: 'Alice', lastName: 'Smith' }
list(target, '*') // ['Alice', 'Smith']
list(target, '*', { entries: true })
// [
//   { value: 'Alice', path: ['firstName'], missing: false },
//   { value: 'Smith', path: ['lastName'], missing: false },
// ]
```

### missing

_Methods_: \
_Type_: `boolean`\
_Default_: `false` with `list|iterate()`, `true` with `set()`

When `false`, properties [not defined in the target](#undefined-values) are
ignored.

```js
const target = {}

set(target, 'name', 'Alice') // { name: 'Alice' }
set(target, 'name', 'Alice', { missing: false }) // {}

list(target, 'name') // []
list(target, 'name', { missing: true, entries: true })
// [{ value: undefined, path: ['name'], missing: true }]
```

### sort

_Methods_: \
_Type_: `boolean`\
_Default_: `false`

When returning sibling object properties, sort them by the lexigographic order
of their names (not values).

```js
const target = { lastName: 'Doe', firstName: 'John' }
list(target, '*') // ['Doe', 'John']
list(target, '*', { sort: true }) // ['John', 'Doe']
```

### childFirst

_Methods_: \
_Type_: `boolean`\
_Default_: `false`

When using [unions](#unions) or [deep wildcards](#wildcards), a query might
match both a property and some of its children.

This option decides whether the returned properties should be sorted from
children to parents, or the reverse.

```js
const target = { user: { name: 'Alice' } }
list(target, 'user.**') // [{ name: 'Alice' }, 'Alice']
list(target, 'user.**', { childFirst: true }) // ['Alice', { name: 'Alice' }]
```

### leaves

_Methods_: \
_Type_: `boolean`\
_Default_: `false`

When using [unions](#unions) or [deep wildcards](#wildcards), a query might
match both a property and some of its children.

When `true`, only leaves are matched. In other words, a matching property is
ignored if one of its children also matches.

```js
const target = { user: { name: 'Alice' } }
list(target, 'user.**') // [{ name: 'Alice' }, 'Alice']
list(target, 'user.**', { leaves: true }) // ['Alice']
```

### roots

_Methods_: \
_Type_: `boolean`\
_Default_: `false`

When using [unions](#unions) or [deep wildcards](#wildcards), a query might
match both a property and some of its children.

When `true`, only roots are matched. In other words, a matching property is
ignored if one of its parents also matches.

```js
const target = { user: { name: 'Alice' } }
list(target, 'user.**') // [{ name: 'Alice' }, 'Alice']
list(target, 'user.**', { roots: true }) // [{ name: 'Alice' }]
```

### classes

_Methods_: all\
_Type_: `boolean`\
_Default_: `false`

Unless `true`, child properties of objects that are not plain objects (like
class instances, errors or functions) are ignored.

```js
const target = { user: new User({ name: 'Alice' }) }
list(target, 'user.*') // []
list(target, 'user.*', { classes: true }) // ['Alice']
```

### inherited

_Methods_: all\
_Type_: `boolean`\
_Default_: `false`

By default, [wildcards](#wildcards) and [regexps](#regexps) ignore properties
that are either
[inherited](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
or
[not enumerable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties).
Those can still be matched by using their [property name](#deep-properties).

When `true`, inherited properties are not ignored, but not enumerable ones still
are.

### deep

_Methods_: [`merge()`](#mergetarget-query-value-options)\
_Type_: `boolean`\
_Default_: `false`

Whether the merge should be shallow or deep.

# Support

For any question, _don't hesitate_ to [submit an issue on GitHub](../../issues).

Everyone is welcome regardless of personal background. We enforce a
[Code of conduct](CODE_OF_CONDUCT.md) in order to promote a positive and
inclusive environment.

# Contributing

This project was made with ❤️. The simplest way to give back is by starring and
sharing it online.

If the documentation is unclear or has a typo, please click on the page's `Edit`
button (pencil icon) and suggest a correction.

If you would like to help us fix a bug or add a new feature, please check our
[guidelines](CONTRIBUTING.md). Pull requests are welcome!

<!-- Thanks go to our wonderful contributors: -->

<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore -->
<!--
<table><tr><td align="center"><a href="https://twitter.com/ehmicky"><img src="https://avatars2.githubusercontent.com/u/8136211?v=4" width="100px;" alt="ehmicky"/><br /><sub><b>ehmicky</b></sub></a><br /><a href="https://github.com/ehmicky/wild-wild-utils/commits?author=ehmicky" title="Code">💻</a> <a href="#design-ehmicky" title="Design">🎨</a> <a href="#ideas-ehmicky" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/ehmicky/wild-wild-utils/commits?author=ehmicky" title="Documentation">📖</a></td></tr></table>
 -->
<!-- ALL-CONTRIBUTORS-LIST:END -->
