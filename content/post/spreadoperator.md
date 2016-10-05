+++
date = "2016-10-03T17:06:21+05:30"
description = ""
draft = false
title = "Spread Operators"
+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
The spread syntax allows an expression to be expanded in places where multiple arguments (for function calls) or multiple elements (for array literals) or multiple variables  (for destructuring assignment) are expected.

String Operators can be written as:

var array = [[arg0ToN ,] ...iterable [, arg0ToN]]
func([args ,] ...iterable [, args | ...iterable])

Parameters
<ul><highlight> iterable - Required. An iterable object. </highlight></ul>
<ul><highlight> arg0ToN - Optional. One or more elements of an array literal. </highlight></ul>
<ul><highlight> args - Optional. One or more arguments to a function. </highlight></ul>

<pre>
<code class="language-javascript">
var params = [ "hello", true, 7 ]
var other = [ 1, 2, ...params ] // [ 1, 2, "hello", true, 7 ]
f(1, 2, ...params) === 9

var str = "foo"
var chars = [ ...str ] // [ "f", "o", "o" ]
</code>
</pre>

<p class='custom-heading'>Explanation</p>
Any argument in the argument list can use the spread syntax and it can be used multiple times

<p class='custom-heading'>How ES5 did it?</p>
<pre>
<code class="language-javascript">
var params = [ "hello", true, 7 ];
var other = [ 1, 2 ].concat(params); // [ 1, 2, "hello", true, 7 ]
f.apply(undefined, [ 1, 2 ].concat(params)) === 9;

var str = "foo";
var chars = str.split(""); // [ "f", "o", "o" ]
</code>
</pre>
