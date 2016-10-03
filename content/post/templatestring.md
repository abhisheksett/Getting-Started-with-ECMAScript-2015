+++
date = "2016-09-30T14:21:45+05:30"
description = ""
draft = false
title = "Template String"

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
  Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them.Prior to ES6 they were called "template strings".

 Template literals are enclosed by the back-tick (` `) (grave accent) character instead of double or single quotes. Template literals can contain place holders. These are indicated by the Dollar sign and curly braces (${expression}). The expressions in the place holders and the text between them get passed to a function.

 </br>
 <highlight>Multiline String </highlight>
 Any new line characters inserted in the source are part of the template literal.
 <p class='custom-heading'>How to use it?</p>
 <pre>
 <code class="language-javascript">
 console.log(`Interesting fact line 1
   Interesting fact line 2`);
  //Output
  "Interesting fact line 1"
  "Interesting fact line 2"
  </code>
 </pre>
 <highlight>Tagged template literals</highlight>
  Tagged template allows you to modify the output of template literals using a function. The first argument contains an array of string literals ("Hello " , " world", and "" in this example). The second, and each argument after the first one, are the values of the processed (or sometimes called cooked) substitution expressions
  <p class='custom-heading'>How to use it?</p>
  <pre>
  <code class="language-javascript">
  var a = 5;
  var b = 10;

  function tag(strings, ...values) {
  console.log(strings[0]); // "Hello "
  console.log(strings[1]); // " world "
  console.log(strings[2]); // ""
  console.log(values[0]);  // 15
  console.log(values[1]);  // 50

  return "Bazinga!";
}

tag`Hello ${ a + b } world ${ a * b }`;
// "Bazinga!"
  </code>
  </pre>
  <highlight>Raw strings</highlight>
  The special raw property, available on the first function argument of tagged template literals, allows you to access the raw strings as they were entered.
  <p class='custom-heading'>How to use it?</p>
  <pre>
  <code class="language-javascript">
  String.raw`Hi\n${2+3}!`;
// "Hi\n5!"
  </code>
  </pre>
 <p class='custom-heading'>How to use it?</p>

<p class='custom-heading'>Explanation</p>

<p class='custom-heading'>How ES5 did it?</p>
<pre>
<code class="language-javascript">
console.log("string text line 1\n"+
"string text line 2");
// "string text line 1
// string text line 2"
</code>
</pre>


<p class='custom-heading'>Try it out here:</p>

https://jsfiddle.net/vznt1dya/

<p class='custom-heading'>Exercise:</p>
Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?kata=es6/language/template-strings/basics

http://tddbin.com/#?kata=es6/language/template-strings/multiline

http://tddbin.com/#?kata=es6/language/template-strings/tagged

http://tddbin.com/#?kata=es6/language/template-strings/raw
