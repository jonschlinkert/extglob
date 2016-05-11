# extglob [![NPM version](https://img.shields.io/npm/v/extglob.svg?style=flat)](https://www.npmjs.com/package/extglob) [![NPM downloads](https://img.shields.io/npm/dm/extglob.svg?style=flat)](https://npmjs.org/package/extglob) [![Build Status](https://img.shields.io/travis/jonschlinkert/extglob.svg?style=flat)](https://travis-ci.org/jonschlinkert/extglob)

Adds (almost) the expressive power of regular expressions to glob patterns!

You might also be interested in [micromatch](https://github.com/jonschlinkert/micromatch).

## Install

Install with [npm](https://www.npmjs.com/):

```sh
$ npm install extglob --save
```

Extglob is short for "extended globs".

## Features

* Complete bash extglob support
* Passes 238 of 240 bash extglob unit tests (_[minimatch](https://github.com/isaacs/minimatch) **fails 90!**_, and the two failing tests seem to be correct for node.js vs. bash)
* Handles complex nested patterns

## Usage

```js
var extglob = require('extglob');
```

The main export returns a string:

```js
extglob('?(z)');
//=> '(?:z)?'
extglob('*(z)');
//=> '(?:z)*'
extglob('+(z)');
//=> '(?:z)+'
extglob('@(z)');
//=> '(?:z)'
extglob('!(z)');
//=> "(?!^(?:(?!z)[^/]*?)).*$"
```

## Extglob patterns

To learn more about how extglobs work, see the docs for [Bash pattern matching](https://www.gnu.org/software/bash/manual/html_node/Pattern-Matching.html):

* `?(pattern)`: Match zero or one occurrence of the given pattern.
* `*(pattern)`: Match zero or more occurrences of the given pattern.
* `+(pattern)`: Match one or more occurrences of the given pattern.
* `@(pattern)`: Match one of the given pattern.
* `!(pattern)`: Match anything except one of the given pattern.

## API

### [extglob](index.js#L27)

Convert the given `extglob` pattern into a regex-compatible string.

**Params**

* `str` **{String}**
* `options` **{Object}**
* `returns` **{String}**

**Example**

```js
var extglob = require('extglob');
var str = extglob('*.!(*a)');
console.log(str);
//=> "[^/]*?\.(?![^/]*?a)[^/]*?"
```

### [.match](index.js#L102)

Takes an array of strings and an extglob pattern and returns a new array that contains only the strings that match the pattern.

**Params**

* `arr` **{Array}**: Array of strings to match
* `pattern` **{String}**: Extglob pattern
* `options` **{Object}**
* `returns` **{Array}**

**Example**

```js
var extglob = require('extglob');
console.log(extglob.match(['a.a', 'a.b', 'a.c'], '*.!(*a)'));
//=> ['a.b', 'a.c']
```

### [.isMatch](index.js#L147)

Returns true if the specified `string` matches the given extglob `pattern`.

**Params**

* `string` **{String}**: String to match
* `pattern` **{String}**: Extglob pattern
* `options` **{String}**
* `returns` **{Boolean}**

**Example**

```js
var extglob = require('extglob');

console.log(extglob.isMatch('a.a', '*.!(*a)'));
//=> false
console.log(extglob.isMatch('a.b', '*.!(*a)'));
//=> true
```

### [.matcher](index.js#L170)

Takes an extglob pattern and returns a matcher function. The returned function takes the string to match as its only argument.

**Params**

* `pattern` **{String}**: Extglob pattern
* `options` **{String}**
* `returns` **{Boolean}**

**Example**

```js
var extglob = require('extglob');
var isMatch = extglob.matcher('*.!(*a)');

console.log(isMatch('a.a'));
//=> false
console.log(isMatch('a.b'));
//=> true
```

### [.makeRe](index.js#L192)

Create a regular expression from the given extglob `pattern`.

**Params**

* `pattern` **{String}**: The extglob pattern to convert
* `options` **{Object}**
* `returns` **{RegExp}**

**Example**

```js
var extglob = require('extglob');
var re = extglob.makeRe('*.!(*a)');
console.log(re);
//=> /^[^\/]*?\.(?![^\/]*?a)[^\/]*?$/
```

## Related projects

You might also be interested in these projects:

* [braces](https://www.npmjs.com/package/braces): Fastest brace expansion for node.js, with the most complete support for the Bash 4.3 braces… [more](https://www.npmjs.com/package/braces) | [homepage](https://github.com/jonschlinkert/braces)
* [expand-brackets](https://www.npmjs.com/package/expand-brackets): Expand POSIX bracket expressions (character classes) in glob patterns. | [homepage](https://github.com/jonschlinkert/expand-brackets)
* [expand-range](https://www.npmjs.com/package/expand-range): Fast, bash-like range expansion. Expand a range of numbers or letters, uppercase or lowercase. See… [more](https://www.npmjs.com/package/expand-range) | [homepage](https://github.com/jonschlinkert/expand-range)
* [fill-range](https://www.npmjs.com/package/fill-range): Fill in a range of numbers or letters, optionally passing an increment or multiplier to… [more](https://www.npmjs.com/package/fill-range) | [homepage](https://github.com/jonschlinkert/fill-range)
* [micromatch](https://www.npmjs.com/package/micromatch): Glob matching for javascript/node.js. A drop-in replacement and faster alternative to minimatch and multimatch. | [homepage](https://github.com/jonschlinkert/micromatch)

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/extglob/issues/new).

## Building docs

Generate readme and API documentation with [verb](https://github.com/verbose/verb):

```sh
$ npm install verb && npm run docs
```

Or, if [verb](https://github.com/verbose/verb) is installed globally:

```sh
$ verb
```

## Running tests

Install dev dependencies:

```sh
$ npm install -d && npm test
```

## Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2016, [Jon Schlinkert](https://github.com/jonschlinkert).
Released under the [MIT license](https://github.com/jonschlinkert/extglob/blob/master/LICENSE).

***

_This file was generated by [verb](https://github.com/verbose/verb), v0.9.0, on May 10, 2016._