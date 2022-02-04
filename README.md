<!--

@license Apache-2.0

Copyright (c) 2018 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->

# incrmsumprod

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Compute a moving sum of products incrementally.

<section class="intro">

For a window of size `W`, the moving sum of products is defined as

<!-- <equation class="equation" label="eq:moving_sum_product" align="center" raw="s = \sum_{i=0}^{W-1} x_i y_i" alt="Equation for the moving sum of products."> -->

<div class="equation" align="center" data-raw-text="s = \sum_{i=0}^{W-1} x_i y_i" data-equation="eq:moving_sum_product">
    <img src="https://cdn.jsdelivr.net/gh/stdlib-js/stdlib@49d8cabda84033d55d7b8069f19ee3dd8b8d1496/lib/node_modules/@stdlib/stats/incr/msumprod/docs/img/equation_moving_sum_product.svg" alt="Equation for the moving sum of products.">
    <br>
</div>

<!-- </equation> -->

</section>

<!-- /.intro -->

<section class="installation">

## Installation

```bash
npm install @stdlib/stats-incr-msumprod
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm` branch][esm-url].
-   If you are using Deno, visit the [`deno` branch][deno-url].
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd` branch][umd-url].

</section>

<section class="usage">

## Usage

```javascript
var incrmsumprod = require( '@stdlib/stats-incr-msumprod' );
```

#### incrmsumprod( window )

Returns an accumulator `function` which incrementally computes a moving sum of products. The `window` parameter defines the number of values over which to compute the moving sum of products.

```javascript
var accumulator = incrmsumprod( 3 );
```

#### accumulator( \[x, y] )

If provided input values `x` and `y`, the accumulator function returns an updated sum. If not provided input values `x` and `y`, the accumulator function returns the current sum.

```javascript
var accumulator = incrmsumprod( 3 );

var sum = accumulator();
// returns null

// Fill the window...
sum = accumulator( 2.0, 3.0 ); // [(2.0,3.0)]
// returns 6.0

sum = accumulator( 1.0, -1.0 ); // [(2.0,3.0), (1.0,-1.0)]
// returns 5.0

sum = accumulator( -3.0, 5.0 ); // [(2.0,3.0), (1.0,-1.0), (-3.0,5.0)]
// returns -10.0

// Window begins sliding...
sum = accumulator( -7.0, -1.0 ); // [(1.0,-1.0), (-3.0,5.0), (-7.0,-1.0)]
// returns -9.0

sum = accumulator( 5.0, 4.0 ); // [(-3.0,5.0), (-7.0,-1.0), (5.0,4.0)]
// returns 12.0

sum = accumulator();
// returns 12.0
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   Input values are **not** type checked. If provided `NaN` or a value which, when used in computations, results in `NaN`, the accumulated value is `NaN` for **at least** `W-1` future invocations. If non-numeric inputs are possible, you are advised to type check and handle accordingly **before** passing the value to the accumulator function.
-   As `W` (x,y) pairs are needed to fill the window buffer, the first `W-1` returned values are calculated from smaller sample sizes. Until the window is full, each returned value is calculated from all provided values.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var randu = require( '@stdlib/random-base-randu' );
var incrmsumprod = require( '@stdlib/stats-incr-msumprod' );

var accumulator;
var v1;
var v2;
var i;

// Initialize an accumulator:
accumulator = incrmsumprod( 5 );

// For each simulated datum, update the moving sum-product...
for ( i = 0; i < 100; i++ ) {
    v1 = randu() * 100.0;
    v2 = randu() * 100.0;
    accumulator( v1, v2 );
}
console.log( accumulator() );
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

* * *

## See Also

-   <span class="package-name">[`@stdlib/stats/incr/mprod`][@stdlib/stats/incr/mprod]</span><span class="delimiter">: </span><span class="description">compute a moving product incrementally.</span>
-   <span class="package-name">[`@stdlib/stats/incr/msum`][@stdlib/stats/incr/msum]</span><span class="delimiter">: </span><span class="description">compute a moving sum incrementally.</span>
-   <span class="package-name">[`@stdlib/stats/incr/sumprod`][@stdlib/stats/incr/sumprod]</span><span class="delimiter">: </span><span class="description">compute a sum of products incrementally.</span>

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2021. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/stats-incr-msumprod.svg
[npm-url]: https://npmjs.org/package/@stdlib/stats-incr-msumprod

[test-image]: https://github.com/stdlib-js/stats-incr-msumprod/actions/workflows/test.yml/badge.svg
[test-url]: https://github.com/stdlib-js/stats-incr-msumprod/actions/workflows/test.yml

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/stats-incr-msumprod/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/stats-incr-msumprod?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/stats-incr-msumprod.svg
[dependencies-url]: https://david-dm.org/stdlib-js/stats-incr-msumprod/main

-->

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/stats-incr-msumprod/tree/deno
[umd-url]: https://github.com/stdlib-js/stats-incr-msumprod/tree/umd
[esm-url]: https://github.com/stdlib-js/stats-incr-msumprod/tree/esm

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://gitter.im/stdlib-js/stdlib/

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/stats-incr-msumprod/main/LICENSE

<!-- <related-links> -->

[@stdlib/stats/incr/mprod]: https://github.com/stdlib-js/stats-incr-mprod

[@stdlib/stats/incr/msum]: https://github.com/stdlib-js/stats-incr-msum

[@stdlib/stats/incr/sumprod]: https://github.com/stdlib-js/stats-incr-sumprod

<!-- </related-links> -->

</section>

<!-- /.links -->
