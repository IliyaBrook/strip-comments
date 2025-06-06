# Forked Repository

This repository fork of the original [strip-comments](https://github.com/jonschlinkert/strip-comments).

## Changes from original fork

You can use the `preserve` option to ignore specific comments based on custom logic. The `preserve` function receives a comment node and should return `true` to keep the comment or `false` to remove it.
example: 

```javascript
const preserveKeywords = ['@ts-ignore']

function preserve(comment) {
  if (comment.value) {
    return preserveKeywords.some(keyword => comment.value.includes(keyword))
  }
  
  if (comment.nodes && Array.isArray(comment.nodes)) {
    const fullText = comment.nodes.map(node => node.value || '').join('')
    return preserveKeywords.some(keyword => fullText.includes(keyword))
  }
  
  return false
}

stripped = strip(content, { preserve })
```



# strip-comments [![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=W8YFZ425KND68) [![NPM version](https://img.shields.io/npm/v/strip-comments.svg?style=flat)](https://www.npmjs.com/package/strip-comments) [![NPM monthly downloads](https://img.shields.io/npm/dm/strip-comments.svg?style=flat)](https://npmjs.org/package/strip-comments) [![NPM total downloads](https://img.shields.io/npm/dt/strip-comments.svg?style=flat)](https://npmjs.org/package/strip-comments) [![Build Status](https://travis-ci.org/jonschlinkert/strip-comments.svg?branch=master)](https://travis-ci.org/jonschlinkert/strip-comments)

> Strip line and/or block comments from a string. Blazing fast, and works with JavaScript, Sass, CSS, Less.js, and a number of other languages.

Please consider following this project's author, [Jon Schlinkert](https://github.com/jonschlinkert), and consider starring the project to show your :heart: and support.

- [Install](#install)
- [What does this do?](#what-does-this-do)
- [Usage](#usage)
- [API](#api)
- [About](#about)

_(TOC generated by [verb](https://github.com/verbose/verb) using [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Install

Install with [npm](https://www.npmjs.com/) (requires [Node.js](https://nodejs.org/en/) >=10):

```sh
$ npm install --save strip-comments
```

## What does this do?

Takes a string and returns a new string with comments removed. Works with line comments and/or block comments. Optionally removes the first comment only or ignores protected comments.

Works with:

* ada
* apl
* applescript
* c
* csharp
* css
* hashbang
* haskell
* html
* java
* javascript
* less
* lua
* matlab
* ocaml
* pascal
* perl
* php
* python
* ruby
* sass
* shebang
* sql
* swift
* typscript
* xml

## Usage

By default all comments are stripped.

```js
const strip = require('strip-comments');
const str = strip('const foo = "bar";// this is a comment\n /* me too *\/');
console.log(str);
// => 'const foo = "bar";\n'
```

For more use-cases see the [tests](./test)

## API

### [strip](index.js#L33)

Strip all code comments from the given `input`, including protected comments that start with `!`, unless disabled by setting `options.keepProtected` to true.

**Params**

* `input` **{String}**: string from which to strip comments
* `options` **{Object}**: optional options, passed to [extract-comments](https://github.com/jonschlinkert/extract-comments)  

- `line` **{Boolean}**: if `false` strip only block comments, default `true`
- `block` **{Boolean}**: if `false` strip only line comments, default `true`
- `keepProtected` **{Boolean}**: Keep ignored comments (e.g. `/*!` and `//!`)
- `preserveNewlines` **{Boolean}**: Preserve newlines after comments are stripped
* `returns` **{String}**: modified input

**Example**

```js
const str = strip('const foo = "bar";// this is a comment\n /* me too */');
console.log(str);
// => 'const foo = "bar";'
```

### [.block](index.js#L54)

Strip only block comments.

**Params**

* `input` **{String}**: string from which to strip comments
* `options` **{Object}**: pass `opts.keepProtected: true` to keep ignored comments (e.g. `/*!`)
* `returns` **{String}**: modified string

**Example**

```js
const strip = require('..');
const str = strip.block('const foo = "bar";// this is a comment\n /* me too */');
console.log(str);
// => 'const foo = "bar";// this is a comment'
```

### [.line](index.js#L74)

Strip only line comments.

**Params**

* `input` **{String}**: string from which to strip comments
* `options` **{Object}**: pass `opts.keepProtected: true` to keep ignored comments (e.g. `//!`)
* `returns` **{String}**: modified string

**Example**

```js
const str = strip.line('const foo = "bar";// this is a comment\n /* me too */');
console.log(str);
// => 'const foo = "bar";\n/* me too */'
```

### [.first](index.js#L95)

Strip the first comment from the given `input`. Or, if `opts.keepProtected` is true, the first non-protected comment will be stripped.

**Params**

* `input` **{String}**
* `options` **{Object}**: pass `opts.keepProtected: true` to keep comments with `!`
* `returns` **{String}**

**Example**

```js
const output = strip.first(input, { keepProtected: true });
console.log(output);
// => '//! first comment\nfoo; '
```

### [.block](index.js#L116)

Parses a string and returns a basic CST (Concrete Syntax Tree).

**Params**

* `input` **{String}**: string from which to strip comments
* `options` **{Object}**: pass `opts.keepProtected: true` to keep ignored comments (e.g. `/*!`)
* `returns` **{String}**: modified string

**Example**

```js
const strip = require('..');
const str = strip.block('const foo = "bar";// this is a comment\n /* me too */');
console.log(str);
// => 'const foo = "bar";// this is a comment'
```

## About

<details>
<summary><strong>Contributing</strong></summary>

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](../../issues/new).

</details>

<details>
<summary><strong>Running Tests</strong></summary>

Running and reviewing unit tests is a great way to get familiarized with a library and its API. You can install dependencies and run tests with the following command:

```sh
$ npm install && npm test
```

</details>

<details>
<summary><strong>Building docs</strong></summary>

_(This project's readme.md is generated by [verb](https://github.com/verbose/verb-generate-readme), please don't edit the readme directly. Any changes to the readme must be made in the [.verb.md](.verb.md) readme template.)_

To generate the readme, run the following command:

```sh
$ npm install -g verbose/verb#dev verb-generate-readme && verb
```

</details>

### Related projects

You might also be interested in these projects:

* [code-context](https://www.npmjs.com/package/code-context): Parse a string of javascript to determine the context for functions, variables and comments based… [more](https://github.com/jonschlinkert/code-context) | [homepage](https://github.com/jonschlinkert/code-context "Parse a string of javascript to determine the context for functions, variables and comments based on the code that follows.")
* [extract-comments](https://www.npmjs.com/package/extract-comments): Uses esprima to extract line and block comments from a string of JavaScript. Also optionally… [more](https://github.com/jonschlinkert/extract-comments) | [homepage](https://github.com/jonschlinkert/extract-comments "Uses esprima to extract line and block comments from a string of JavaScript. Also optionally parses code context (the next line of code after a comment).")
* [parse-code-context](https://www.npmjs.com/package/parse-code-context): Fast and simple way to parse code context for use with documentation from code comments… [more](https://github.com/jonschlinkert/parse-code-context) | [homepage](https://github.com/jonschlinkert/parse-code-context "Fast and simple way to parse code context for use with documentation from code comments. Parses context from a single line of JavaScript, for functions, variable declarations, methods, prototype properties, prototype methods etc.")
* [parse-comments](https://www.npmjs.com/package/parse-comments): Parse code comments from JavaScript or any language that uses the same format. | [homepage](https://github.com/jonschlinkert/parse-comments "Parse code comments from JavaScript or any language that uses the same format.")

### Contributors

| **Commits** | **Contributor** |  
| --- | --- |  
| 82 | [jonschlinkert](https://github.com/jonschlinkert) |  
| 4  | [tunnckoCore](https://github.com/tunnckoCore) |  
| 2  | [mk-pmb](https://github.com/mk-pmb) |  
| 1  | [kgryte](https://github.com/kgryte) |  
| 1  | [briandipalma](https://github.com/briandipalma) |  
| 1  | [epicoxymoron](https://github.com/epicoxymoron) |  
| 1  | [XuluWarrior](https://github.com/XuluWarrior) |  

### Author

**Jon Schlinkert**

* [GitHub Profile](https://github.com/jonschlinkert)
* [Twitter Profile](https://twitter.com/jonschlinkert)
* [LinkedIn Profile](https://linkedin.com/in/jonschlinkert)

### License

Copyright © 2019, [Jon Schlinkert](https://github.com/jonschlinkert).
Released under the [MIT License](LICENSE).

***

_This file was generated by [verb-generate-readme](https://github.com/verbose/verb-generate-readme), v0.8.0, on November 13, 2019._
