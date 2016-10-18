+++
date = "2016-10-18T16:25:53+05:30"
description = ""
draft = false
tags = []
title = "functionparameter"
topics = []

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
A function can take parameters which are just values you supply to the function so that the function can do something utilising those values. These parameters are just like variables except that the values of these variables are defined when we call the function and are not assigned values within the function itself.

Parameters are specified within the pair of parentheses in the function definition, separated by commas. When we call the function, we supply the values in the same way. Note the terminology used - the names given in the function definition are called <highlight>parameters</highlight> whereas the values you supply in the function call are called <highlight>arguments</highlight>.
<pre>
<code class="language-javascript">function myFunction(param1,param2,param3) {
   statements
}
</code>
</pre>
There are 2 types of function parameters available in es6:<br>

<highlight>Default Parameters</highlight><br>
<highlight>Rest Parameters</highlight>
<p class='custom-sub-heading'>How to use default parameters?</p>
Default parameter are a way to pass a value to the function parameter when no value is being passed by the callee during invocation.
ES6 allows for functions to be called with less parameters than the function declares.
<pre>
<code class="language-javascript">function getData(data, useCache=true) {
	if (useCache) {
		console.log('using cache for', data);
	}
	else {
		console.log('not using cache', data);
	}
};
// `useCache` is missing and is `undefined`.
// therefore `useCache `defaults to `true`
getData({q:'churches+in+Pittsburg'});
</code>
</pre>

With ES6, the function body doesn’t have to deal with the defaulting logic. It’s in the function header, which is where it should be. Also it’s clear to any readers of the code that <highlight>useCache</highlight> will have its value defaulted to <highlight>true</highlight> when left unspecified.

Parameters with a default value are considered optional. Therefore if you have a parameter that is optional, but doesn’t have a default value, you may want to consider giving it an explicit default of 
<highlight>undefined</highlight> to visually mark it as optional.


<p class='custom-sub-heading'>Non-primitive default values</p>

Unlike other programming languages that support default values,a default value in ES6 does not have to be a primitive value like <highlight>String</highlight>, <highlight>Number</highlight> or <highlight>Boolean</highlight>. A default value can be an <highlight>Object</highlight>, <highlight>Array</highlight> or <highlight>Function</highlight>. The default value can even be the result of an expression or function call.
<pre>
<code class="language-javascript">
function getWidth() {
	console.log('getWidth called');
	return 7;
}
function drawRect(
	width=getWidth(),
	height=width * 2,
	options={color:'red'}
) {
	console.log(width, height, options);
}
// `getWidth` is called to retrieve default
// value for `width` since it was unspecified.
// output:
//   getWidth called
//   7, 14, {color:'red'}
drawRect();
// `getWidth` is not called because `width` is
// specified. `height` is still defaulted to
// 2x `width`.
// output:
//    17, 34, {color:'red'}
drawRect(17);
// `height` is no longer defaulted to 2x `width`
// but options are still defaulted.
// ouput:
//    4, 11, {color:'red'}
drawRect(4, 11);
// nothing is defaulted
// output:
//    7,5, 11, {color:'blue'}
drawRect(7.5, 11, {color:'blue'});
</code>
</pre>

<highlight>Note:</highlight><br>
 The default value for height is an expression that uses the value of width. You’re free to use other variables declared in the function header as long as they come before the variable in question. It’s also worth noting that expressions or functions are not executed if the variable does not need to be defaulted.

<p class='custom-sub-heading'>Default parameter ordering</p>
Also unlike other programming languages, in ES6 the default values can be anywhere in the function header, even before parameters that do not have default values.

Let’s take a look at an example:
<pre>
	<code class="language-javascript">function drawCube(x, y=7, z) {
	console.log('cube', x, y, z);
};
// `y` is defaulted, but `x` & `z` are not
// so they are `undefined`.
// output: cube, undefined, y, undefined
drawCube();
// `y` is still defaulted, but `z` isn't.
// output: cube, 2.5, 7, undefined
drawCube(2.5);
// output: cube, 9, 15, undefined
drawCube(9, 15);
// output: cube, 4, 1.7, 18
drawCube(4, 1.7, 18);
// `y` is once again defaulted
// output: cube, 11, 7, 8.8
drawCube(11, undefined, 8.8);
// `null` does not trigger `y` to default
// output: cube, 14, null, 72
drawCube(14, null, 72);</code>
</pre>

As you can see, the default for <highlight>y </highlight>isn’t triggered unless <highlight>y </highlight> and <highlight>z </highlight> are unspecified or <highlight>y </highlight> is explicitly set to be <highlight>undefined</highlight>. In a nutshell, <highlight>undefined</highlight> triggers default values.
<p class='custom-sub-heading'>How to use rest parameters?</p>

We just learned that <highlight>default</highlight> parameters handle the case where a caller passes less parameters than what a function declares. ES6 also allows for functions to be called with more parameters than the function declares. That’s where <highlight>rest</highlight> parameters come in.

ES6 introduces the rest operator, three dots (…) that precede a named parameter. That parameter is now a rest parameter that is an Array containing the rest of the parameters (hence the name!).
<pre>
	<code class="language-javascript">
function join(separator, ...values) {
	return values.join(separator);
}
// all of the parameters after the first
// are gathered together into `values`
// which is a true `Array`
// output: "one//two//three"
console.log(join('//', 'one', 'two', 'three'));
</code>
</pre>

In the example, <highlight>values</highlight> is an <highlight>Array</highlight> of all of the parameters passed after <highlight>'//'</highlight> making it much easier to use. Also, it’s much clearer looking at the <highlight>join</highlight> function that it does take an additional unlimited set of parameters.
<p class='custom-sub-heading'>One rest parameter per function</p>
One caveat with rest parameters is that unlike default parameters there can only be one per function and it must be the last parameter declared in the function header. Attempting to have multiple rest parameters or putting one before other parameters will throw a <highlight>SyntaxError</highlight>:
<pre><code>function afterRest(first, ...second, third) {
	// SyntaxError: parameter after rest parameter
}
function multipleRest(first, ...second, ...third) {
	// SyntaxError: parameter after rest parameter
}</code></pre>

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.<br>
http://tddbin.com/#?