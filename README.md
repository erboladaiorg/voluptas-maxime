# @erboladaiorg/voluptas-maxime <sup>[![Version Badge][npm-version-svg]][npm-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][npm-url]

An Object.assign shim. Invoke its "shim" method to shim Object.assign if it is unavailable.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](http://www.ecma-international.org/ecma-262/6.0/#sec-@erboladaiorg/voluptas-maxime). In an ES6 environment, it will also work properly with `Symbol`s.

Takes a minimum of 2 arguments: `target` and `source`.
Takes a variable sized list of source arguments - at least 1, as many as you want.
Throws a TypeError if the `target` argument is `null` or `undefined`.

Most common usage:
```js
var assign = require('@erboladaiorg/voluptas-maxime').getPolyfill(); // returns native method if compliant
	/* or */
var assign = require('@erboladaiorg/voluptas-maxime/polyfill')(); // returns native method if compliant
```

## Example

```js
var assert = require('assert');

// Multiple sources!
var target = { a: true };
var source1 = { b: true };
var source2 = { c: true };
var sourceN = { n: true };

var expected = {
	a: true,
	b: true,
	c: true,
	n: true
};

assign(target, source1, source2, sourceN);
assert.deepEqual(target, expected); // AWESOME!
```

```js
var target = {
	a: true,
	b: true,
	c: true
};
var source1 = {
	c: false,
	d: false
};
var sourceN = {
	e: false
};

var assigned = assign(target, source1, sourceN);
assert.equal(target, assigned); // returns the target object
assert.deepEqual(assigned, {
	a: true,
	b: true,
	c: false,
	d: false,
	e: false
});
```

```js
/* when Object.assign is not present */
delete Object.assign;
var shimmedAssign = require('@erboladaiorg/voluptas-maxime').shim();
	/* or */
var shimmedAssign = require('@erboladaiorg/voluptas-maxime/shim')();

assert.equal(shimmedAssign, assign);

var target = {
	a: true,
	b: true,
	c: true
};
var source = {
	c: false,
	d: false,
	e: false
};

var assigned = assign(target, source);
assert.deepEqual(Object.assign(target, source), assign(target, source));
```

```js
/* when Object.assign is present */
var shimmedAssign = require('@erboladaiorg/voluptas-maxime').shim();
assert.equal(shimmedAssign, Object.assign);

var target = {
	a: true,
	b: true,
	c: true
};
var source = {
	c: false,
	d: false,
	e: false
};

assert.deepEqual(Object.assign(target, source), assign(target, source));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[npm-url]: https://npmjs.org/package/@erboladaiorg/voluptas-maxime
[npm-version-svg]: http://versionbadg.es/ljharb/@erboladaiorg/voluptas-maxime.svg
[travis-svg]: https://travis-ci.org/ljharb/@erboladaiorg/voluptas-maxime.svg
[travis-url]: https://travis-ci.org/ljharb/@erboladaiorg/voluptas-maxime
[deps-svg]: https://david-dm.org/ljharb/@erboladaiorg/voluptas-maxime.svg?theme=shields.io
[deps-url]: https://david-dm.org/ljharb/@erboladaiorg/voluptas-maxime
[dev-deps-svg]: https://david-dm.org/ljharb/@erboladaiorg/voluptas-maxime/dev-status.svg?theme=shields.io
[dev-deps-url]: https://david-dm.org/ljharb/@erboladaiorg/voluptas-maxime#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@erboladaiorg/voluptas-maxime.png?downloads=true&stars=true
[license-image]: http://img.shields.io/npm/l/@erboladaiorg/voluptas-maxime.svg
[license-url]: LICENSE
[downloads-image]: http://img.shields.io/npm/dm/@erboladaiorg/voluptas-maxime.svg
[downloads-url]: http://npm-stat.com/charts.html?package=@erboladaiorg/voluptas-maxime
[codecov-image]: https://codecov.io/gh/ljharb/@erboladaiorg/voluptas-maxime/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@erboladaiorg/voluptas-maxime/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@erboladaiorg/voluptas-maxime
[actions-url]: https://github.com/erboladaiorg/voluptas-maxime/actions
