+++
date = "2016-11-04T16:15:12+05:30"
description = ""
draft = false
tags = []
title = "BlockScoping"
topics = []

+++
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
ES6 provides two new ways of declaring variables: let and const, which mostly replace the ES5 way of declaring variables, var.

<p class='custom-sub-heading'>The limitations of var</p>
Before introducing <highlight>const</highlight> and <highlight>let</highlight>, it’s worth discussing why they are helpful or necessary in the first place. Var has been the only keyword for variables in JavaScript up until now but it has several drawbacks.
When writing JS using <highlight>var</highlight>, it’s difficult to immediately discern which variables are scoped locally vs. globally. It’s very easy to accidentally create a variable on the global object in JavaScript. This generally doesn’t affect simple demo apps but can cause problems for enterprise level applications as team members accidentally obliterate each other’s variables.

<p class='custom-sub-heading'>Using let</p>
The new ES6 keyword <highlight>let</highlight> allows developers to scope variables at the <highlight>block level (the nearest curly brackets)</highlight>.
<pre>
<code class="language-javascript">(function() { 
var fruit = "Apple"; 
if (true) {
	console.log(fruit);
	let fruit = "Orange";
	console.log(fruit); //Orange
}
console.log(fruit); //Apple
})();
</code>
</pre>
In the above example, the variable is scoped to the IIFE function when it’s declared with <highlight>var</highlight>. Within the <highlight>if</highlight> block, a separate fruit variable is declared with <highlight>let</highlight> and scoped to the <highlight>if</highlight> block.

<p class='custom-sub-heading'>for loop block example</p>
<pre>
<code class="language-javascript">for (let i = 0; i < 10; i++) {
 console.log(i);
}
console.log("outside loop: " + i); // Undefined
for (var i = 0; i < 10; i++) {
 console.log(i);
}
console.log("outside loop: " + i); 
</code>
</pre>
The <highlight>for</highlight> loop example above is a bit more interesting than the <highlight>if</highlight> block. By using <highlight>let</highlight> in the initialization expression, the <highlight>i</highlight> variable is scoped only to the block. By using <highlight>var</highlight>, the <highlight>i</highlight> will be scoped to the nearest function. The variable will equal 10 outside of the <highlight>for</highlight> loop block. This can have consequences such as creating an accidental closure as in examples like this:
<pre>
<code class="language-javascript">var listItems = document.querySelectorAll('.listItems');
for (var i = 0; i < listItems.length; i++) {
  var element = listItems[i];
  element.addEventListener('click', function() {
    alert('Clicked on number: ' + i)
  });
}
</code>
</pre>
In this example, the code is meant to register an event listener on a simple list and alert which number was clicked. Instead, it will alert Clicked on <highlight>Number: 5</highlight> for each list item. Wrapping the event listener part in a function would be a common workaround for avoiding the accidental closure.

But instead, refactoring this with <highlight>let (once it’s fully supported)</highlight> creates a block scope in the <highlight>for</highlight> loop and avoids the accidental closure. It allows the expected iterator to be used within the event listener callback function.

One caveat with <highlight>let</highlight> is that it doesn’t hoist in the same way var does. If you try to use it before it’s been declared, you will get a reference error.

<p class='custom-sub-heading'>Using const</p>
Like constants in other languages, <highlight>const</highlight> will often be used for values that won’t need to be reassigned in a program’s execution.Variables declared with <highlight>const</highlight> are often written in all caps, but this is a matter of preference.
<highlight>Const</highlight> is the other new ES6 keyword for declaring variables. <highlight>Const</highlight> works like a constant in other languages in many ways but there are some caveats. Const stands for <highlight>‘constant reference’</highlight> to a value. The values that const references are <highlight>not immutable (their properties can be changed)</highlight>.
So with <highlight>const</highlight>, you can actually mutate the properties of an object being referenced by the variable. You just can’t change the reference itself. 
<pre>
<code class="language-javascript">
const PI_VALUE = 3.141592;
const APIKEY = 'aekljefj3442313kalnawef';
const NAMES = [];
NAMES.push("Jim");
console.log(NAMES.length === 1); // true
NAMES = ["Steve", "John"]; // error
</code>
</pre>
<p class='custom-sub-heading'>When to Use const vs. let</p>

<highlight>ES6 conventions</highlight> : <br>
Use constant by default <br>
Use let if you have to rebind a variable <br>
Use var to signal untouched legacy code <br>

If I don’t need to reassign, <highlight>const</highlight> is my default choice over <highlight>let</highlight> because I want the usage to be as clear as possible in the code.
<highlight>const</highlight> is a signal that the variable won’t be reassigned.
<highlight>let</highlight> is a signal that the variable may be reassigned, such as a counter in a loop, or a value swap in an algorithm. It also signals that the variable will be used only in the block it’s defined in, which is not always the entire containing function.
<highlight>var</highlight> is now the weakest signal available.

<p class='custom-sub-heading'>The temporal dead zone</p>
A variable declared by <highlight>let</highlight> or <highlight>const</highlight> has a so-called <highlight>temporal dead zone (TDZ)</highlight>: When entering its scope, it can’t be accessed (got or set) until execution reaches the declaration. 
<p class='custom-sub-heading'>The life cycle of var-declared variables</p>
<highlight>var</highlight> variables don’t have temporal dead zones. Their life cycle comprises the following steps:
When the scope (its surrounding function) of a <highlight>var</highlight> variable is entered, storage space (a binding) is created for it. The variable is immediately initialized, by setting it to <highlight>undefined</highlight>.

When the execution within the scope reaches the declaration, the variable is set to the value specified by the <highlight>initializer (an assignment)</highlight> – if there is one. If there isn’t, the value of the variable remains <highlight>undefined</highlight>.
<p class='custom-sub-heading'>The life cycle of let-declared variables</p>
Variables declared via <highlight>let</highlight> have temporal dead zones and their life cycles look like this:

When the scope (its surrounding block) of a <highlight>let</highlight> variable is entered, storage space (a binding) is created for it. The variable remains uninitialized.
Getting or setting an uninitialized variable causes a <highlight>ReferenceError</highlight>.
When the execution within the scope reaches the declaration, the variable is set to the value specified by the initializer (an assignment) – if there is one. If there isn’t then the value of the variable is set to <highlight>undefined</highlight>.

const variables work similarly to let variables, but they must have an <highlight>initializer (i.e., be set to a value immediately)</highlight> and can’t be changed.

Within a TDZ, an exception is thrown if a variable is got or set:

<pre>
<code class="language-javascript">
let tmp = true;
if (true) { // enter new scope, TDZ starts
    // Uninitialized binding for `tmp` is created
    console.log(tmp); // ReferenceError
    let tmp; // TDZ ends, `tmp` is initialized with `undefined`
    console.log(tmp); // undefined
    tmp = 123;
    console.log(tmp); // 123
}
console.log(tmp); // true
</code>
</pre>
If there is an initializer then the TDZ ends after the assignment was made:
<pre>
<code class="language-javascript">
let foo = console.log(foo); // ReferenceError
</code>
</pre>
The following code demonstrates that the dead zone is really temporal (based on time) and not spatial (based on location):
<pre>
<code class="language-javascript">
if (true) { // enter new scope, TDZ starts
    const func = function () {
        console.log(myVar); // OK!
    };
    // Here we are within the TDZ and
    // accessing `myVar` would cause a `ReferenceError`
    let myVar = 3; // TDZ ends
    func(); // called outside TDZ
}
</code>
</pre>
<p class='custom-heading'>Try it out here:</p>

http://codepen.io/DevelopIntelligenceBoulder/pen/BoGEoa?editors=101 <br>
http://codepen.io/DevelopIntelligenceBoulder/pen/KdrYdg?editors=101 <br>
http://codepen.io/DevelopIntelligenceBoulder/pen/XmyQXe?editors=101 <br>
http://codepen.io/DevelopIntelligenceBoulder/pen/JYeVGv?editors=101 <br>
http://www.es6fiddle.net/iv3qbwwx/ <br>


<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?