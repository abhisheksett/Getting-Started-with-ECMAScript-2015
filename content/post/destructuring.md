+++
date = "2016-10-02T22:36:23+05:30"
draft = false
title = "Destructuring"

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is Destructuring?</p>
The destructuring assignment syntax is a JavaScript expression that makes it possible to extract data from <highlight>arrays</highlight> or <highlight>objects</highlight> into distinct variables.

There are a lot of ways in which Destructuring can be used.

<p class='custom-heading'>A very basic way to use the Destructuring feature</p>

<pre>
<code class="language-javascript">
var a,b,rest;
[a,b] = [1,2];
console.log(a); //1
console.log(b); //2

[a,b,...rest] = [1,2,3,4,5,6,7,8];
console.log(a);//1
console.log(b);//2
console.log(rest);//[3,4,5,6,7,8]
</code>
</pre>

<p class='custom-heading'>Explanation</p>

Here the variables a and b are assigned in one-line using the destructuring functionality of ecmascript2015. Unlike the previous version of ECMAScript, where the variables had to be assigned separately, this method helps achieve this in a single line of code.

Also note the <highlight>...</highlight> allows us to assign the variable "rest", the remaining values in the array.

<p class='custom-heading'>How ES5 did it?</p>

In ES5, this was done like this:

<pre>
<code class="language-javascript">
"use strict";

var a, b, rest;
a = 1;
b = 2;

console.log(a); //1
console.log(b); //2

a = 1;
b = 2;
rest = [3, 4, 5, 6, 7, 8];

console.log(a); //1
console.log(b); //2
console.log(rest); //[3,4,5,6,7,8]
</code>
</pre>

<p class='custom-heading'>Example code on Array Destructuring</p>
Different scenarios :

<p class='custom-sub-heading'>1. The basic array destructuring </p>
Sample Code Link:
<highlight> https://jsbin.com/tikagup/17/edit?js,console </highlight>

<p class="custom-sub-heading">2. Assignment separate from declaration and the <highlight>...</highlight> operation example</p>
<p>Sample Code Link:
  <highlight>https://jsbin.com/tikagup/1/edit</highlight></p>

<p class="custom-sub-heading">3. Default values</p>
<p>A variable can be assigned a default, in the case that the value pulled from the array is undefined.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/4/edit?js,console</highlight></p>

<p class="custom-sub-heading">4. Swapping variables</p>
<p>Two variables values can be swapped in one destructuring expression. Without destructuring assignment, swapping two values requires a temporary variable.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/5/edit?js,console</highlight></p>

<p class="custom-sub-heading">5. Parsing an array returned from a function</p>
<p>It's always been possible to return an array from a function. Destructuring can make working with an array return value more concise.
In this example, f() returns the values [1, 2] as its output, which can be parsed in a single line with destructuring.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/6/edit?js,console</highlight></p>

<p class="custom-sub-heading">6. Ignoring some returned values</p>
<p>You can ignore return values that you're not interested in.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/7/edit?js,console</highlight></p>

<p class="custom-sub-heading">7. Pulling values from a regular expression match</p>
<p>When the regular expression exec() method finds a match, it returns an array containing first the entire matched portion of the string and then the portions of the string that matched each parenthesized group in the regular expression. Destructuring assignment allows you to pull the parts out of this array easily, ignoring the full match if it is not needed.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/8/edit?js,console</highlight></p>

<p class='custom-heading'>Example code on Object Destructuring</p>
Different scenarios :

<p class='custom-sub-heading'>1. Basic assignment.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/9/edit?js,console</highlight></p>

<p class="custom-sub-heading">2. Assignment without declaration.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/10/edit?js,console</highlight></p>

<p class="custom-sub-heading">3. Assigning to new variable names</p>
<p>A variable can be extracted from an object and assigned to a variable with a different name than the object property.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/11/edit?js,console</highlight></p>

<p class="custom-sub-heading">4. Default values</p>
<p>A variable can be assigned a default, in the case that the value pulled from the object is undefined.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/12/edit?js,console</highlight></p>

<p class="custom-sub-heading">5. Nested object and array destructuring.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/13/edit?js,console</highlight></p>

<p class="custom-sub-heading">6. For of iteration and destructuring.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/14  /edit?js,console</highlight></p>

<p class="custom-sub-heading">7. Pulling fields from objects passed as function parameter</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/15/edit?js,console</highlight></p>

<p class="custom-sub-heading">8. Computed object property names and destructuring</p>
<p>Computed property names, like on object literals, can be used with destructuring.</p>
<p>Sample Code Link: <highlight>https://jsbin.com/tikagup/16/edit?js,console</highlight></p>

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?kata=es6/language/destructuring/array

http://tddbin.com/#?kata=es6/language/destructuring/string

http://tddbin.com/#?kata=es6/language/destructuring/object

http://tddbin.com/#?kata=es6/language/destructuring/defaults

http://tddbin.com/#?kata=es6/language/destructuring/parameters

http://tddbin.com/#?kata=es6/language/destructuring/rename
