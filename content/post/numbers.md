+++
date = "2016-10-26T13:59:24+05:30"
description = ""
draft = false
tags = []
title = "numbers"
topics = []

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
This section describes new properties that the constructor Number has picked up in ES6.
Four number-related functions are already available as global functions and have been added to Number, as methods: <br>
<highlight>isFinite</highlight>
<highlight>isNaN</highlight>
<highlight>parseFloat</highlight>
<highlight>parseInt</highlight>

<p class='custom-sub-heading'>Number.isFinite(number)</p>
Is number an actual number (neither Infinity nor -Infinity nor NaN)?

<pre>
<code class="language-javascript">
console.log(Number.isFinite(Infinity)); //false
console.log(Number.isFinite(-Infinity)); //false
console.log(Number.isFinite(NaN)); //false
console.log(Number.isFinite(123)); //true

    </code>
    </pre>
The advantage of this method is that it does not coerce its parameter to number (whereas the global function does):
<pre>
<code class="language-javascript">
console.log(Number.isFinite('123')); //false
console.log(isFinite('123')); //true
</code>
</pre>
<p class='custom-sub-heading'>Number.isNaN(number)</p>
Is number the value NaN? Making this check via === is hacky. NaN is the only value that is not equal to itself:
<pre>
<code class="language-javascript">
 var x = NaN;
    if( x === NaN){  //this will give an error
}
 </code>
 </pre>

Using Number.isNaN() is more self-descriptive:
<pre>
<code class="language-javascript">
 var x = NaN;
console.log(Number.isNaN(x));  //true
</code>
</pre>
Number.isNan() also has the advantage of not coercing its parameter to number (whereas the global function does):
<pre>
<code class="language-javascript">
cosnole.log(Number.isNaN('???'));  //false
console.log(isNaN('???'));         //true
</code>
</pre>
<p class='custom-sub-heading'>Number.parseInt() and Number.parseFloat()</p>
The <highlight>Number.parseInt()</highlight> and <highlight>Number.parseFloat()</highlight> methods already existed in previous version of ECMAScript but aren’t different from their old global version. So, you can use them in the same way you’ve done so far and you can expect the same results. They have been added to Number because they actually belonged to it from the very beginning.You can use it as :
<pre>
<code class="language-javascript">
Number.parseInt(string, radix)  //parses a string and returns an integer
Number.parseFloat(string)       //parses a string and returns a floating point number
</code>
</pre>
The <highlight>parseInt()</highlight> function parses a string and returns an integer. The <highlight>radix</highlight> parameter is used to specify which numeral system to be used, for example, a radix of 16 (hexadecimal) indicates that the number in the string should be parsed from a hexadecimal number to a <highlight>decimal</highlight> number.

The <highlight>parseFloat()</highlight> function parses a string and returns a floating point number. This function determines if the first character in the specified string is a number. If it is, it parses the string until it reaches the end of the number, and returns the number as a number, <highlight>not as a string</highlight>.
<pre>
<code class="language-javascript">
console.log(Number.parseInt('-3'));      //-3
console.log(Number.parseInt('100', 2));  // 4
console.log(Number.parseInt('test'));    //NaN
console.log(Number.parseInt({}));        //NaN
console.log(Number.parseFloat('42.1'));  //42.1
console.log(Number.parseFloat('test'));  //NaN
console.log(Number.parseFloat({}));      //NaN
</code>
</pre>

<p class='custom-sub-heading'>Number.isInteger()</p>
<highlight>Number.isInteger()</highlight> determines whether the value passed to the function is an integer or not. This method returns <highlight>true</highlight> if the passed value is an integer, and <highlight>false</highlight> otherwise. 
<pre>
<code class="language-javascript">
console.log(Number.isInteger(123));  //true
console.log(Number.isInteger('123')); //false
console.log(Number.isInteger("abc")); //false
console.log(Number.isInteger(Infinity));//false
console.log(Number.isInteger('')); //false
</code>
</pre>
<p class='custom-sub-heading'>Number.isSafeInteger()</p>
<highlight>Number.isSafeInteger()</highlight>tests whether the value passed is a number that is a safe integer in which case it returns <highlight>true</highlight>.
ES6 numbers have only enough storage space to represent 53 bit signed integers. That is, integers i in the range <highlight>−2<sup>53</sup> < i < 2<sup>53</sup></highlight> are safe.The following properties help determine whether a ES6 integer is safe:<br>
<highlight>Number.isSafeInteger(number)</highlight>
<highlight>Number.MIN_SAFE_INTEGER</highlight>
<highlight>Number.MAX_SAFE_INTEGER</highlight><br>
In the range (−2<sup>53</sup>, 2<sup>53</sup>) (excluding the lower and upper bounds),integers are safe: there is a one-to-one mapping between them and the mathematical integers they represent.
Beyond this range,integers are unsafe: two or more mathematical integers are represented as the same integer. For example, starting at 2<sup>53</sup>,you can represent only every second mathematical integer:
<pre>
<code class="language-javascript">
console.log(Math.pow(2, 53));  //9007199254740992
console.log(9007199254740992); //9007199254740992
console.log(9007199254740993); //9007199254740992
console.log(9007199254740994); //9007199254740994
console.log(9007199254740995); //9007199254740996
console.log(9007199254740996); //9007199254740996
console.log(9007199254740997); //9007199254740996
</code>
</pre>
Therefore, a safe integer is one that unambiguously represents a single mathematical integer.

The two Number properties specifying the lower and upper bound of safe integers could be defined as follows:
<pre>
<code class="language-javascript">
Number.MAX_SAFE_INTEGER = Math.pow(2, 53)-1;
Number.MIN_SAFE_INTEGER = -Number.MAX_SAFE_INTEGER;
console.log(Number.MAX_SAFE_INTEGER);
console.log(Number.MIN_SAFE_INTEGER);
    </code>
    </pre>

<pre>
<code class="language-javascript">
console.log(Number.isSafeInteger(5)); //true
console.log(Number.isSafeInteger('19')); //false
console.log(Number.isSafeInteger(Math.pow(2, 53)));  //false
console.log(Number.isSafeInteger(Math.pow(2, 53) - 1));  //true
</code>
</pre>
For a given value n, following function first checks whether n is a number and an integer. If both checks succeed, n is safe if it is greater than or equal to MIN_SAFE_INTEGER and less than or equal to MAX_SAFE_INTEGER.
<pre>
<code class="language-javascript">
Number.isSafeInteger = function (n) {
        return (typeof n === 'number' &&
            Math.round(n) === n &&
            Number.MIN_SAFE_INTEGER <= n &&
            n <= Number.MAX_SAFE_INTEGER);
    }
</code>
</pre>
<p class='custom-sub-heading'>Safe results of arithmetic computations</p>
How can we make sure that results of arithmetic computations are correct? For example, the following result is clearly not correct:
<pre>
<code class="language-javascript">
console.log(9007199254740990 + 3);  //9007199254740992 ,which is not correct
console.log(9007199254740995 - 10); //9007199254740986 ,which is not correct
</code>
</pre>
In the example above,former has two safe operands, but an unsafe result.Wherein later has safe result but an operand is unsafe.
Therefore, the result of applying an integer operator op is guaranteed to be correct only if all operands and the result are safe. More formally:
 <pre>
<code class="language-javascript">
 Number.isSafeInteger(a) && Number.isSafeInteger(b) && Number.isSafeInteger(a op b)
</code>
</pre>
<p class='custom-sub-heading'>Number.EPSILON</p>
<highlight>Number.EPSILON</highlight> is used for comparing floating point numbers with a tolerance for rounding errors.It specifies a reasonable margin of error when comparing floating point numbers.
It represents the difference between one and the smallest value greater than one that can be represented as a Number. It provides a better way to compare floating point values, as demonstrated by the following function.
<pre>
<code class="language-javascript">
function epsEqu(x, y) {
        console.log(x); //0.30000000000000004
        console.log(y); //0.3
        return Math.abs(x - y) < Number.EPSILON;
    }
console.log(epsEqu(0.1+0.2, 0.3)); // true
console.log(Number.EPSILON); //2.220446049250313e-16
console.log(0.1+0.2);   //0.30000000000000004
</code>
</pre>
<p class='custom-heading'>Try it out here:</p>
  https://jsbin.com/howobu/5/edit?js,console,output <br>
  https://jsbin.com/howobu/6/edit?js,console,output <br>
  https://jsbin.com/howobu/7/edit?js,console,output <br>
  https://jsbin.com/howobu/8/edit?js,console,output <br>
  https://jsbin.com/howobu/9/edit?js,console,output <br>
  https://jsbin.com/howobu/10/edit?js,console,output <br>
  https://jsbin.com/howobu/11/edit?js,console,output <br>
  https://jsbin.com/howobu/12/edit?js,console,output <br>
  https://jsbin.com/howobu/13/edit?js,console,output

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.<br>
http://tddbin.com/#?kata=es6/language/number-api/isinteger