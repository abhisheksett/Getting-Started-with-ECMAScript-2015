+++
date = "2016-09-30T14:26:40+05:30"
description = ""
draft = false
tags = []
title = "Generator"
topics = []

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>

Generators, a new feature of ECMAScript 6 are functions that can be paused and resumed. This helps with many applications: iterators, asynchronous programming, etc. Their primary use case is in representing lazy (possibly infinite) sequences.

Generator functions are indicated by inserting a star character * after the function keyword (it doesn’t matter if the star is directly next to function or if there’s some whitespace between them). The yield keyword is used inside of generators to specify the values that the iterator should return when next() is called. So if you want to return three different values for each successive call to next(), you can do so as follows:

<pre>
<code class="language-javascript">
       function* createIterator() {
          yield 1;
          yield 2;
          yield 3;
        }
        // generators are called like regular functions but return an iterator let iterator = createIterator();
        let iterator = createIterator();

        console.log(iterator.next().value); //1
        console.log(iterator.next().value); //2
        console.log(iterator.next().value); //3
}
</code>
</pre>

There are four ways in which you can create generators:
  
  1. Via a generator function declaration:

<pre>
<code class="language-javascript">
    function* genFunc() { ··· }
    let genObj = genFunc();

</code>
</pre>

  2. Via a generator function expression:

<pre>
<code class="language-javascript">
    const genFunc = function* () { ··· };
    let genObj = genFunc();
    
</code>
</pre>

  3. Via a generator method definition in an object literal:

<pre>
<code class="language-javascript">
    let obj = {
        * generatorMethod() {
            ···
        }
    };
    let genObj = obj.generatorMethod();
    
</code>
</pre>

  4. Via a generator method definition in a class definition (which can be a class declaration or a class expression):

<pre>
<code class="language-javascript">
    class MyClass {
        * generatorMethod() {
            ···
        }
    }
    let myInst = new MyClass();
    let genObj = myInst.generatorMethod();
    
</code>
</pre>
<div class='warning'>
Generator functions are an important part of ECMAScript 6, and since they are just functions, they can be used in all the same places.
</div>

<p class='custom-sub-heading'>Generator Function Expressions</p>


Generators can be created using function expressions in the same way as using function declarations by including a star (*) character between the function keyword and the opening paren, for example:

<pre>
<code class="language-javascript">
  let createIterator = function *(items) { for (let i=0; i < items.length; i++) {
          yield items[i];
      }
  };
  let iterator = createIterator([1, 2, 3]);
  console.log(JSON.stringify(iterator.next())); //{"value":1,"done":false}
  console.log(JSON.stringify(iterator.next())); //{"value":2,"done":false}
  console.log(JSON.stringify(iterator.next())); //{"value":3,"done":false}
  console.log(JSON.stringify(iterator.next())); //{"done":true}
  
  // for all further calls
  console.log(JSON.stringify(iterator.next())); //{"done":true}

</code>
</pre>

In this code, createIterator() is a generator function expression rather than a function declaration (as in the previous example). Since the function expression is anonymous, the asterisk is between the function keyword and the opening parentheses. Otherwise, this example is the same as the previous one using a generator function declaration.

<div class='info'>
<b>It is not possible to create an arrow function that is also a generator.</b>
</div>


<p class='custom-sub-heading'>Generator Object Methods</p>


Because generators are just functions, they can be added to objects the same way as any other functions. For example, you can use an ECMAScript 5-style object literal with a function expression:

<pre>
<code class="language-javascript">
  var o = {
  reateIterator: function *(items) {
    for (let i=0; i < items.length; i++) {
        yield items[i];
    }
  }
};

let iterator = o.createIterator([1, 2, 3]);

</code>
</pre>


You can also use the ECMAScript 6 method shorthand by prepending the method name with a star (*):
<pre>
<code class="language-javascript">
  var o = {
    *createIterator(items) {
      for (let i=0; i < items.length; i++) {
        yield items[i];
    }
  }
};
let iterator = o.createIterator([1, 2, 3]);
</code>
</pre>

This example is functionally equivalent to the previous one, the only difference is the syntax used. Because the method is defined using shorthand and there is no function keyword, the star is placed immediately before the method name (though there may be whitespace between the star and the method name).

<p class='custom-sub-heading'>Roles played by generators</p>
Generators can play three roles:</br></br>

    1. <b>Iterators (data producers)</b>: Each yield can return a value via next(), which means that generators can produce sequences of values via loops and recursion. Due to generator objects implementing the interface Iterable, these sequences can be processed by any ECMAScript 6 construct that supports iterables. Two examples are: for-of loops and the spread operator (...).</br></br>

    2. <b>Observers (data consumers)</b>: yield can also receive a value from next() (via a parameter). That means that generators become data consumers that pause until a new value is pushed into them via next().</br></br>

    3. <b>Coroutines (data producers and consumers)</b>: Given that generators are pausable and can be both data producers and data consumers, not much work is needed to turn them into coroutines (cooperatively multitasked tasks).</br></br>


<p class='custom-heading'>Try it out here:</p>

https://jsfiddle.net/qk7vL83e/

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?kata=es6/language/generator/creation <br/>
http://tddbin.com/#?kata=es6/language/generator/iterator <br/>
http://tddbin.com/#?kata=es6/language/generator/yield <br/>
http://tddbin.com/#?kata=es6/language/generator/send-value <br/>
http://tddbin.com/#?kata=es6/language/generator/send-function <br/>
http://tddbin.com/#?kata=es6/language/generator/return<br/>
