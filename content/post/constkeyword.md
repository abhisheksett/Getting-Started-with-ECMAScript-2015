+++
date = "2016-10-13T12:25:22+05:30"
description = ""
draft = false
tags = []
title = "const keyword"
topics = []

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>

In ES6 a <highlight>const</highlight> represents a constant reference to a value. In other words, the pointer that the variable name is using cannot change in memory, but the thing the variable points to might change.
A constant cannot change value through assignment or be re-declared while the script is running. It has to be initialized to a value.

Here’s a simple example. In the code below we create a new variable with a constant reference to an Array. We can then add values onto the array and since this does not change the reference, everything works:
<pre>
<code class="language-javascript">const names = [];
names.push( "Jordan" );
console.log( names );
</code>
</pre>
However, if we try to change the variable reference to a new array – even to one with the same contents – we will get a SyntaxError (“Assignment to constant variable”):
<pre>
<code class="language-javascript">const names = [];
names = [];  // Error!</code>
</pre>
Const variable you declare must be immediately initialized, with a value that can’t be changed afterwards.
<pre>
<code class="language-javascript">
const foo; // SyntaxError: missing = in const declaration
const bar = 123;
bar = 456; // TypeError: `bar` is read-only
</code>
</pre>
Since for-of creates one binding (storage space for a variable) per loop iteration, it is OK to const-declare the loop variable:

<pre>
<code class="language-javascript">
for (const x of ['a', 'b']) {
    console.log(x);
}
// Output:
// a
// b
</code>
</pre>
<p class='custom-sub-heading'>Block scoping via const</p>

Const creates variables that are block-scoped – they only exist within the innermost block that surrounds them. The following code demonstrates that the const-declared variable tmp only exists inside the then-block of the if statement:
<pre>
<code class="language-javascript">
function func() {
    if (true) {
        const tmp = 123;
    }
    console.log(tmp); // ReferenceError: tmp is not defined
}
Block scoping means that you can shadow variables within a function:
function func() {
  const foo = 5;
  if (···) {
     const foo = 10; // shadows outer `foo`
     console.log(foo); // 10
  }
  console.log(foo); // 5
}
</code>
</pre>
<p class='custom-sub-heading'>Const creates immutable variables</p>
<pre>
<code class="language-javascript">
	const foo = 'abc';
foo = 'def'; // TypeError
</code>
</pre>
<p class='custom-sub-heading'>Const does not make the value immutable</p>
Const only means that a variable always has the same value, but it does not mean that the value itself is or becomes immutable. For example, obj is a constant, but the value it points to is mutable – we can add a property to it:
<pre>
<code class="language-javascript">
onst obj = {};
obj.prop = 123;
console.log(obj.prop); // 123
</code>
</pre>
We cannot, however assign a different value to obj:
<pre><code class="language-javascript">
	obj = {}; // TypeError
</code></pre>

<p class='custom-sub-heading'>Const in loop bodies</p>
Once a const variable has been created, it can’t be changed. But that doesn’t mean that you can’t re-enter its scope and start fresh, with a new value. For example, via a loop:
<pre><code class="language-javascript">
function logArgs(...args) {
    for (const [index, elem] of args.entries()) {
        const message = index + '. ' + elem;
        console.log(message);
    }
}
logArgs('Hello', 'everyone');
// Output:
// 0. Hello
// 1. everyone
</code></pre>

<p class='custom-sub-heading'>Const in loop heads</p>
The following loops allow you to declare variables in their heads:

<highlight>for</highlight>
<highlight>for-in</highlight>
<highlight>for-of</highlight>

Var-declaring a variable in the head of a for loop creates a single binding (storage space) for that variable:

<pre><code class="language-javascript">
const arr = [];
for (var i=0; i < 3; i++) {
    arr.push(() => i);
}
arr.map(x => x()); // [3,3,3]
</code></pre>
Every i in the bodies of the three arrow functions refers to the same binding, which is why they all return the same value.

If you let-declare a variable, a new binding is created for each loop iteration:
<pre><code class="language-javascript">
const arr = [];
for (let i=0; i < 3; i++) {
    arr.push(() => i);
}
arr.map(x => x()); // [0,1,2]
</code></pre>
This time, each i refers to the binding of one specific iteration and preserves the value that was current at that time. Therefore, each arrow function returns a different value.

<p class='custom-sub-heading'>Const versus let versus var</p>
Prefer const. You can use it whenever a variable never changes its value. In other words: the variable should never be the left-hand side of an assignment or the operand of ++ or --. Changing an object that a const variable refers to is allowed:
<pre><code class="language-javascript">
 const foo = {};
 foo.prop = 123; // OK
 </code></pre>
You can even use const in a for-of loop, because one (immutable) binding is created per loop iteration:
<pre><code class="language-javascript">
 for (const x of ['a', 'b']) {
     console.log(x);
 }
 // Output:
 // a
 // b
 </code></pre>
Inside the body of the for-of loop, x can’t changed.
Otherwise, use let – when the initial value of a variable changes later on.
<pre><code class="language-javascript">
 let counter = 0; // initial value
 counter++; // change

 let obj = {}; // initial value
 obj = { foo: 123 }; // change
 </code></pre>
Avoid var.

<p class='custom-heading'>Try it out here:</p>

https://jsfiddle.net/shamkaushik/mfegs2uw/1/

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?