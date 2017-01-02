# Continued Fractions
Continued fractions have a interesting role in the history of mathematics. First described in the 1600s, they used to be a commonly used tool from Galileo useing them to compute gear ratios to Euler using them to prove that *e* is irrational. But in the push for computational techniques in the past 100 years, they fell out of fashion. But the main difficulty is summarized by a quote from Khinchin's *Continued Fractions* included in [Bill Gosper's unpublished paper](http://www.tweedledum.com/rwg/cfup.htm):

>There is, however, another and yet more significant practical demand that the apparatus of continued fractions does not satisfy at all.  Knowing the representations of several numbers, we would like to be able, with relative ease, to find the representations of the simpler functions of these numbers (especially their sum and product).

>...

>On the other hand, for continued fractions there are no practically applicable rules for arithmetical operations;  even the problem of finding the continued fraction for a sum from the continued fractions representing the addends is exceedingly complicated, and unworkable in computational practice.

>   --A. YA. Khinchin, 1935

In that paper by Bill Gosper however, he essentially solved this problem. Although unpublished, Gosper's continued fraction algorithm

# Cfraction
A set of libraries for continued fraction arithmetic.
The following examples are in javascript but the main functionality is the same in all languages.

Construction
---
Constructing a simple continued fraction
~~~ javascript
var my_simple_cf = new Cfraction([a1,a2,a3]);
~~~
Constructing a general continued fraction
~~~ javascript
var my_general_cf = new Cfraction([a1,a2,a3],[b1,b2,b3]);
~~~
There are three main methods available to a Cfraction object:
~~~ javascript
my_general_cf.toString();
~~~
will return the string `a:[a1,a2,a3] b:[b1,b2,b3]`.

~~~ javascript
my_general_cf.toTex();
~~~
will return the string `a1+\cfrac{b1}{a2+\cfrac{b2}{a3+b3}}`.
(`\cfrac{}{}` is included in the `amsmath` package)

~~~ javascript
my_general_cf.decimal(k);
~~~
will return (as a string) the first *k* digits of the decimal expansion of `my_general_cf`.
Note that if your expansion is too large this will return the last computable value.

For simple continued fractions we can estimate the error. That is, the maximum difference that the given continued fraction could have from what it could converge to. For example the next term in `[1,2,2,2,2]` could be 2 or 127, but these values cannot differ by more than the value returned by the error method.
~~~ javascript
my_general_cf.error(k);
~~~
will return (as a string) the first *k* digits, or whenever the first non-zero digit appears in the decimal expansion of the maximum error of `my_general_cf`.
Again if your expansion is enormous than this will return the last computable value.

If you prefer, the error can be returned in scientific notation.
~~~ javascript
my_general_cf.error_sci(k);
~~~

Functions
---

Constants
---
~~~ javascript
var pi = Cfraction.PI;
~~~
returns the first 80 or so terms for the Euler-Mascheroni constant gamma

~~~ javascript
var gamma = Cfraction.GAMMA;
~~~
returns the first 100 terms for the Euler-Mascheroni constant gamma

~~~ javascript
var e = Cfraction.E(k);
~~~
returns the first k terms for E
