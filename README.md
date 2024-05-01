# @omegion1npm/deserunt-aut-impedit

Deterministic `JSON.stringify()` - a faster version of [@substack](https://github.com/substack)'s json-stable-strigify without [jsonify](https://github.com/substack/jsonify).

You can also pass in a custom comparison function.

[![Build Status](https://travis-ci.org/epoberezkin/@omegion1npm/deserunt-aut-impedit.svg?branch=master)](https://travis-ci.org/epoberezkin/@omegion1npm/deserunt-aut-impedit)
[![Coverage Status](https://coveralls.io/repos/github/epoberezkin/@omegion1npm/deserunt-aut-impedit/badge.svg?branch=master)](https://coveralls.io/github/epoberezkin/@omegion1npm/deserunt-aut-impedit?branch=master)

# example

``` js
var stringify = require('@omegion1npm/deserunt-aut-impedit');
var obj = { c: 8, b: [{z:6,y:5,x:4},7], a: 3 };
console.log(stringify(obj));
```

output:

```
{"a":3,"b":[{"x":4,"y":5,"z":6},7],"c":8}
```


# methods

``` js
var stringify = require('@omegion1npm/deserunt-aut-impedit')
```

## var str = stringify(obj, opts)

Return a deterministic stringified string `str` from the object `obj`.


## options

### cmp

If `opts` is given, you can supply an `opts.cmp` to have a custom comparison
function for object keys. Your function `opts.cmp` is called with these
parameters:

``` js
opts.cmp({ key: akey, value: avalue }, { key: bkey, value: bvalue })
```

For example, to sort on the object key names in reverse order you could write:

``` js
var stringify = require('@omegion1npm/deserunt-aut-impedit');

var obj = { c: 8, b: [{z:6,y:5,x:4},7], a: 3 };
var s = stringify(obj, function (a, b) {
    return a.key < b.key ? 1 : -1;
});
console.log(s);
```

which results in the output string:

```
{"c":8,"b":[{"z":6,"y":5,"x":4},7],"a":3}
```

Or if you wanted to sort on the object values in reverse order, you could write:

```
var stringify = require('@omegion1npm/deserunt-aut-impedit');

var obj = { d: 6, c: 5, b: [{z:3,y:2,x:1},9], a: 10 };
var s = stringify(obj, function (a, b) {
    return a.value < b.value ? 1 : -1;
});
console.log(s);
```

which outputs:

```
{"d":6,"c":5,"b":[{"z":3,"y":2,"x":1},9],"a":10}
```

### cycles

Pass `true` in `opts.cycles` to stringify circular property as `__cycle__` - the result will not be a valid JSON string in this case.

TypeError will be thrown in case of circular object without this option.


# install

With [npm](https://npmjs.org) do:

```
npm install @omegion1npm/deserunt-aut-impedit
```


# benchmark

To run benchmark (requires Node.js 6+):
```
node benchmark
```

Results:
```
@omegion1npm/deserunt-aut-impedit x 17,189 ops/sec ±1.43% (83 runs sampled)
json-stable-stringify x 13,634 ops/sec ±1.39% (85 runs sampled)
fast-stable-stringify x 20,212 ops/sec ±1.20% (84 runs sampled)
faster-stable-stringify x 15,549 ops/sec ±1.12% (84 runs sampled)
The fastest is fast-stable-stringify
```


## Enterprise support

@omegion1npm/deserunt-aut-impedit package is a part of [Tidelift enterprise subscription](https://tidelift.com/subscription/pkg/npm-@omegion1npm/deserunt-aut-impedit?utm_source=npm-@omegion1npm/deserunt-aut-impedit&utm_medium=referral&utm_campaign=enterprise&utm_term=repo) - it provides a centralised commercial support to open-source software users, in addition to the support provided by software maintainers.


## Security contact

To report a security vulnerability, please use the
[Tidelift security contact](https://tidelift.com/security).
Tidelift will coordinate the fix and disclosure. Please do NOT report security vulnerability via GitHub issues.


# license

[MIT](https://github.com/omegion1npm/deserunt-aut-impedit/blob/master/LICENSE)
