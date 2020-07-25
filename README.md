[![build status](https://secure.travis-ci.org/dankogai/js-combinatorics.png)](http://travis-ci.org/dankogai/js-combinatorics)

js-combinatorics
================

Simple combinatorics in JavaScript

# HEADS UP

In the next major version update, `js-combinatorics` will go ES2015.

* native iterator instead of custom
* module. `import` instead of `require`.
* `BigInt` where possible

APIs will change accordingly.  Old versions are available in the `version0` branch.

### For Swift programmers

Check [swift-combinatorics].  More naturally implemented with generics and protocol.

[swift-combinatorics]: https://github.com/dankogai/swift-combinatorics

## SYNOPSIS

```javascript
import * as $C from 'combinatorics.js';
let it =  new $C.Combination('abcdefgh', 4);
for (const elem of it) {
  console.log(elem) // ['a', 'b', 'c', 'd'] ... ['a', 'd', 'e', 'f']
}
```

## Usage

load everything…

```javascript
import * as Combinatorics from 'combinatorics.js';
```

or just objects you want.

```javascript
import {Combination, Permutation} from 'combinatorics.js';
```

You don't even have to install if you `import` from CDNs.

```javascript
import * as C from 'https://cdn.jsdelivr.net/npm/js-combinatorics@0.6.1/combinatorics.min.js';
```

Since this is an ES6 module, `type="module"` is required the `<script>` tags. of your HTML files. But you can make it globally available as follows.

```html
<script type="module">
  import * as $C from 'combinatorics.js';
  window.Combinatorics = $C;
</script>
<script>
  // now you can access Combinatorics
  let c = new Combinatorics.Combination('abcdefgh', 4);
</script>
```

### node.js and commonjs
```javascript
var Combinatorics = require('js-combinatorics');
```

## Description

### Arithmetic Functions

Self-explanatory, are they not?

```javascript
import {permutation, combination, factorial, factoradic} from 'combinatorics.js';

permutation(24, 12);  // 1295295050649600
permutation(26, 13);  // 64764752532480000n

combination(56, 28);  // 7648690600760440
combination(58, 29);  // 30067266499541040n

factorial(18);  // 6402373705728000
factorial(19);  // 121645100408832000n

factoradic(6402373705727999);     // [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17]
factoradic(121645100408831999n)   // [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18]
```

The arithmetic functions above accept both `Number` and `BigInt` (if supported).  Return answers in `Number` if it is small enough to fit within  `Number.MAX_SAFE_INTEGER` or `BigInt` otherwise.

### classes

The module comes with `Permutation`, `Combination`, `PowerSet`, `BaseN`, and `CartesianProduct`.  You can individually `import` them or all of them via `import *`

```javascript
import * as $C from 'combinatorics.js';
```

You construct an iterable object by giving a seed iterable and options.  in the example below, `'abcdefgh'` is the seed and `4` is the size of the element.

```javascript
let it = new $C.Combination('abcdefgh', 4);
```

Once constructed, you can iterate via `for … of` statement or turn it into an array via `[...]` construct.

```javascript
[...it]; /* [
  [ 'a', 'b', 'c', 'd' ], [ 'a', 'b', 'c', 'e' ], [ 'a', 'b', 'c', 'f' ],
  [ 'a', 'b', 'c', 'h' ], [ 'a', 'b', 'd', 'c' ], [ 'a', 'b', 'd', 'g' ],
  [ 'a', 'b', 'd', 'e' ], [ 'a', 'b', 'd', 'h' ], [ 'a', 'b', 'e', 'd' ],
  [ 'a', 'b', 'f', 'd' ], [ 'a', 'b', 'e', 'c' ], [ 'a', 'b', 'e', 'f' ],
  [ 'a', 'b', 'e', 'g' ], [ 'a', 'b', 'f', 'e' ], [ 'a', 'b', 'e', 'h' ],
  [ 'a', 'b', 'f', 'h' ], [ 'a', 'b', 'g', 'f' ], [ 'a', 'c', 'b', 'f' ],
  [ 'a', 'b', 'f', 'g' ], [ 'a', 'b', 'g', 'c' ], [ 'a', 'b', 'g', 'd' ],
  [ 'a', 'b', 'g', 'h' ], [ 'a', 'b', 'g', 'e' ], [ 'a', 'b', 'h', 'c' ],
  [ 'a', 'b', 'h', 'e' ], [ 'a', 'c', 'b', 'g' ], [ 'a', 'b', 'h', 'd' ],
  [ 'a', 'b', 'h', 'f' ], [ 'a', 'b', 'h', 'g' ], [ 'a', 'c', 'd', 'b' ],
  [ 'a', 'c', 'b', 'd' ], [ 'a', 'c', 'd', 'h' ], [ 'a', 'c', 'f', 'e' ],
  [ 'a', 'd', 'b', 'h' ], [ 'a', 'c', 'b', 'h' ], [ 'a', 'c', 'd', 'e' ],
  [ 'a', 'c', 'd', 'f' ], [ 'a', 'c', 'e', 'b' ], [ 'a', 'c', 'd', 'g' ],
  [ 'a', 'c', 'e', 'd' ], [ 'a', 'c', 'e', 'g' ], [ 'a', 'c', 'f', 'g' ],
  [ 'a', 'c', 'e', 'f' ], [ 'a', 'c', 'e', 'h' ], [ 'a', 'c', 'f', 'b' ],
  [ 'a', 'c', 'f', 'h' ], [ 'a', 'c', 'f', 'd' ], [ 'a', 'c', 'g', 'd' ],
  [ 'a', 'c', 'h', 'b' ], [ 'a', 'd', 'c', 'b' ], [ 'a', 'c', 'g', 'b' ],
  [ 'a', 'c', 'g', 'e' ], [ 'a', 'c', 'g', 'f' ], [ 'a', 'c', 'h', 'd' ],
  [ 'a', 'c', 'g', 'h' ], [ 'a', 'c', 'h', 'e' ], [ 'a', 'c', 'h', 'g' ],
  [ 'a', 'd', 'c', 'f' ], [ 'a', 'c', 'h', 'f' ], [ 'a', 'd', 'b', 'c' ],
  [ 'a', 'd', 'b', 'e' ], [ 'a', 'd', 'e', 'c' ], [ 'a', 'd', 'b', 'f' ],
  [ 'a', 'd', 'f', 'h' ], [ 'a', 'e', 'c', 'b' ], [ 'a', 'f', 'c', 'g' ],
  [ 'a', 'd', 'c', 'e' ], [ 'a', 'd', 'c', 'g' ], [ 'a', 'd', 'c', 'h' ],
  [ 'a', 'd', 'e', 'f' ]
] */
```

The object has `.length` so you don't have to iterate to count the elements.

```javascript
it.length;  // 70
```

The object also has `.nth(n)` method so you can random-access each element.  This is the equivalent of subscript in `Array`.

```javascript
it.nth(69); //  [ 'a', 'd', 'c', 'h' ];
```

### class Permutation

An iterable which permutes a given iterable.

`new Permutation(seed, size)`

* `seed`: the seed iterable.   `[...seed]` becomes the seed array.
* `size`: the number of elements in the iterated element.  defaults to `seed.length`

````javascript
import {Permutation} from 'combinatorics.js';

let it = new Permutation('abcd'); // size 4 is assumed4
it.length;  // 24
[...it];    /* [
  [ 'a', 'b', 'c', 'd' ], [ 'a', 'b', 'd', 'c' ],
  [ 'a', 'c', 'b', 'd' ], [ 'a', 'c', 'd', 'b' ],
  [ 'a', 'd', 'b', 'c' ], [ 'a', 'd', 'c', 'b' ],
  [ 'b', 'a', 'c', 'd' ], [ 'b', 'a', 'd', 'c' ],
  [ 'b', 'c', 'a', 'd' ], [ 'b', 'c', 'd', 'a' ],
  [ 'b', 'd', 'a', 'c' ], [ 'b', 'd', 'c', 'a' ],
  [ 'c', 'a', 'b', 'd' ], [ 'c', 'a', 'd', 'b' ],
  [ 'c', 'b', 'a', 'd' ], [ 'c', 'b', 'd', 'a' ],
  [ 'c', 'd', 'a', 'b' ], [ 'c', 'd', 'b', 'a' ],
  [ 'd', 'a', 'b', 'c' ], [ 'd', 'a', 'c', 'b' ],
  [ 'd', 'b', 'a', 'c' ], [ 'd', 'b', 'c', 'a' ],
  [ 'd', 'c', 'a', 'b' ], [ 'd', 'c', 'b', 'a' ]
] */

it = new Permutation('abcdefghijklmnopqrstuvwxyz0123456789');
it.length;  // 371993326789901217467999448150835200000000n
it.nth(371993326789901217467999448150835199999999n);  /* [
  '9', '8', '7', '6', '5', '4', '3',
  '2', '1', '0', 'z', 'y', 'x', 'w',
  'v', 'u', 't', 's', 'r', 'q', 'p',
  'o', 'n', 'm', 'l', 'k', 'j', 'i',
  'h', 'g', 'f', 'e', 'd', 'c', 'b',
  'a'
] */
````


### class Combination

An iterable which emits a combination of a given iterable.

`new Combination(seed, size)`

* `seed`: the seed iterable.
* `size`: the number of elements in the iterated element.  

````javascript
import {Combination} from 'combinatorics.js';

let it = new Combination('abcd', 2);
it.length;  // 6
[...it];    /* [
  [ 'a', 'b' ],
  [ 'a', 'c' ],
  [ 'a', 'd' ],
  [ 'b', 'c' ],
  [ 'b', 'd' ],
  [ 'c', 'd' ]
] */

let a100 = Array(100).fill(0).map((v,i)=>i); // [0, 1, ...99]
it = new Combination(a100, 50);
it.length;  // 100891344545564193334812497256n
it.nth(100891344545564193334812497255n);  /* [
  0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10,
  11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
  22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32,
  38, 76, 36, 41, 40, 81, 84, 62, 87, 83, 43,
  91, 88, 33, 34, 35, 39
] */
````

### class PowerSet

An iterable which emits each element of its power set.

`new PowerSet(seed)`

* `seed`: the seed iterable.

````javascript
import {PowerSet} from 'combinatorics.js';

let it = new PowerSet('abc');
it.length;  // 8
[...it];    /* [
  [],
  [ 'a' ],
  [ 'b' ],
  [ 'a', 'b' ],
  [ 'c' ],
  [ 'a', 'c' ],
  [ 'b', 'c' ],
  [ 'a', 'b', 'c' ]
] */

it = new PowerSet(
  'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
);
it.length;  // 18446744073709551616n
it.nth(18446744073709551615n);  /* [
  'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I',
  'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R',
  'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', 'a',
  'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j',
  'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's',
  't', 'u', 'v', 'w', 'x', 'y', 'z', '0', '1',
  '2', '3', '4', '5', '6', '7', '8', '9', '+',
  '/'
] */
````

### class BaseN

An iterable which emits all numbers in the given system.

`new BaseN(seed, size)`

* `seed`: the seed iterable whose elements represent digits.
* `size`: the number of digits

```javascript
import {BaseN} from 'combinatorics.js';

let it = new BaseN('abc', 3);
it.length;  // 27
[...it];    /* [
  [ 'a', 'a', 'a' ], [ 'b', 'a', 'a' ],
  [ 'c', 'a', 'a' ], [ 'a', 'b', 'a' ],
  [ 'b', 'b', 'a' ], [ 'c', 'b', 'a' ],
  [ 'a', 'c', 'a' ], [ 'b', 'c', 'a' ],
  [ 'c', 'c', 'a' ], [ 'a', 'a', 'b' ],
  [ 'b', 'a', 'b' ], [ 'c', 'a', 'b' ],
  [ 'a', 'b', 'b' ], [ 'b', 'b', 'b' ],
  [ 'c', 'b', 'b' ], [ 'a', 'c', 'b' ],
  [ 'b', 'c', 'b' ], [ 'c', 'c', 'b' ],
  [ 'a', 'a', 'c' ], [ 'b', 'a', 'c' ],
  [ 'c', 'a', 'c' ], [ 'a', 'b', 'c' ],
  [ 'b', 'b', 'c' ], [ 'c', 'b', 'c' ],
  [ 'a', 'c', 'c' ], [ 'b', 'c', 'c' ],
  [ 'c', 'c', 'c' ]
] */

it = BaseN('0123456789abcdef', 16);
it.length;  // 18446744073709551616n
it.nth(18446744073709551615n);  /* [
  'f', 'f', 'f', 'f',
  'f', 'f', 'f', 'f',
  'f', 'f', 'f', 'f',
  'f', 'f', 'f', 'f'
] */
```

### class CartesianProduct

A [cartesian product] of given sets.

[cartesian Product]: https://en.wikipedia.org/wiki/Cartesian_product

`new CartesianProduct(...args)`

* `args`: iterables that represent sets

```javascript
import {CartesianProduct} from 'combinatorics.js';

let it = new CartesianProduct('012','abc','xyz');
it.length;  // 27
[...it];    /* [
  [ '0', 'a', 'x' ], [ '1', 'a', 'x' ],
  [ '2', 'a', 'x' ], [ '0', 'b', 'x' ],
  [ '1', 'b', 'x' ], [ '2', 'b', 'x' ],
  [ '0', 'c', 'x' ], [ '1', 'c', 'x' ],
  [ '2', 'c', 'x' ], [ '0', 'a', 'y' ],
  [ '1', 'a', 'y' ], [ '2', 'a', 'y' ],
  [ '0', 'b', 'y' ], [ '1', 'b', 'y' ],
  [ '2', 'b', 'y' ], [ '0', 'c', 'y' ],
  [ '1', 'c', 'y' ], [ '2', 'c', 'y' ],
  [ '0', 'a', 'z' ], [ '1', 'a', 'z' ],
  [ '2', 'a', 'z' ], [ '0', 'b', 'z' ],
  [ '1', 'b', 'z' ], [ '2', 'b', 'z' ],
  [ '0', 'c', 'z' ], [ '1', 'c', 'z' ],
  [ '2', 'c', 'z' ]
] */
```

Since the number of arguments to `CartesianProduct` is variable, it is sometimes helpful to give a single array with all arguments.   But you cannot `new ctor.apply(null, args)` this case.  To mitigate that, you can use `.vmake()`.

```javascript
let a16 =  Array(16).fill('0123456789abcdef');
it = CartesianProduct.vmake(a16);
it.length;  // 18446744073709551616n
it.nth(18446744073709551615n);  /* [
  'f', 'f', 'f', 'f',
  'f', 'f', 'f', 'f',
  'f', 'f', 'f', 'f',
  'f', 'f', 'f', 'f'
] */
````

## What's missing from version 0.x?

* `bigCombination` is gone because all classes now can handle big -- combinatorially big! -- cases thanks to [BigInt] support getting standard.  Safari 13 and below is a major exception but BigInt is coming to Safari 14 and up.

[BigInt]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt

* `permutationCombination` is gone because the name is misleading and it is now trivially easy to reconstruct as follow:

```javascript
class permutationCombination {
    constructor(seed) {
        this.seed = [...seed];
    }
    [Symbol.iterator]() {
        return function*(it){
            for (let i = 1, l = it.length; i <= l; i++) {
                yield* new Permutation(it, i);
            }
        }(this.seed);
    }
}
```

* `js-combinatorics` is now natively iterable.  Meaning its custom iterators are gone -- with its methods like `.map` and `.filter`.  JS iterators are very minimalistic with only `[...]` and `for ... of`.  But don't worry.  There are several ways to make those functional methods back again. 

For instance, You can use [js-xiterable] like so:

[js-xiterable]: https://github.com/dankogai/js-xiterator

```javascript
import {xiterable as $X} from 
  'https://cdn.jsdelivr.net/npm/js-xiterable@0.0.3/xiterable.min.js';
import {Permutation} from 'combinatorics.js';
let it = new Permutation('abcd');
let words = $X(it).map(v=>v.join(''))
for (const word of words)) console.log(word)
/*
abcd
abdc
acbd
acdb
adbc
adcb
bacd
badc
bcad
bcda
bdac
bdca
cabd
cadb
cbad
cbda
cdab
cdba
dabc
dacb
dbac
dbca
dcab
dcba
*/
```