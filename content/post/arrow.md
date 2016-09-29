+++
date = "2016-09-23T11:56:13+01:00"
title = "Arrow Function"
draft = false

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>

Arrow functions – also called <highlight>“fat arrow”</highlight> functions, from CoffeeScript (a transcompiled language) are a more concise syntax for writing function expressions. They utilize a new token, <highlight>=></highlight>, that looks like a fat arrow. Arrow functions are anonymous and change the way this binds in functions.

Arrow functions make our code more concise, and simplify function scoping and the this keyword. They are one-line mini functions which work much like Lambdas in other languages like C# or Python. By using arrow function we avoid having to type the function keyword, return keyword (it’s implicit in arrow functions), and curly brackets.

An arrow function expression has a shorter syntax compared to function expressions and does not bind its own <highlight>this</highlight>, <highlight>arguments</highlight>, <highlight>super</highlight>, or <highlight>new.target</highlight>. Arrow functions are always anonymous. These function expressions are best suited for non-method functions and they can not be used as constructors.

<p class='custom-heading'>How to use it?</p>

<pre>
<code class="language-javascript">
let tmp = {
  fName: 'John',
  lName: 'Snow',
  hobby: ['fighting', 'riding', 'reading', 'coding'],
  likes: function(){
    this.hobby.map((item) => {
      console.log(`${this.fName} ${this.lName} likes ${item}`);
    })
  }
}
tmp.likes();

// Output
"John Snow likes fighting"
"John Snow likes riding"
"John Snow likes reading"
"John Snow likes coding"
</code>
</pre>

<p class='custom-heading'>Explanation</p>

In the above example, 'this' inside 'hobby.map' function should ideally refer to 'likes' object. In that case, 'this.fName'
should have been 'undefined'. But arrow function levels up the scope of 'this' and points to 'tmp' object.

<p class='custom-heading'>How ES5 did it?</p>

In ES5, this was done like this:

<pre>
<code class="language-javascript">
'use strict';
var tmp = {
  fName: 'John',
  lName: 'Snow',
  hobby: ['fighting', 'riding', 'reading', 'coding'],
  likes: function likes() {
    var _this = this;
    this.hobby.map(function (item) {
      console.log(_this.fName + ' ' + _this.lName + ' likes ' + item);
    });
  }
};
tmp.likes();
</code>
</pre>

<p class='custom-heading'>Try it out here:</p>

https://jsfiddle.net/vxh0kmpy/

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?kata=es6/language/arrow-functions/basics

http://tddbin.com/#?kata=es6/language/arrow-functions/binding
