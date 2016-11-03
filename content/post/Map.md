+++
date = "2016-11-03T14:48:29+05:30"
description = ""
draft = false
tags = []
title = "Map"
topics = []

+++


<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
The Map object is a simple key/value map. Any value (both objects and primitive values) may be used as either a key or a value.

<p class='custom-sub-heading'>Syntax</p>

<pre>
<code class="language-javascript">
new Map([iterable])
</code>
</pre>

Iterable is an Array or other iterable object whose elements are key-value pairs (2-element Arrays). Each key-value pair is added to the new Map. null is treated as undefined.
A Map object iterates its elements in insertion order — a for...of loop returns an array of [key, value] for each iteration.
It should be noted that a Map that is a map of an object, especially a dictionary of dictionaries, will only map to the object's insertion order -- which is random and not ordered. 

<p class='custom-sub-heading'>Properties</p>
<highlight>Map.length</highlight>
The value of the length property is 0.<br>
<highlight>get Map[@@species]</highlight>
The constructor function that is used to create derived objects.<br>
<highlight>Map.prototype</highlight>
Represents the prototype for the Map constructor. Allows the addition of properties to all Map objects.

<p class='custom-sub-heading'>Map instances</p>
All Map instances inherit from <highlight>Map.prototype</highlight>.
<p class='custom-sub-heading'>Properties</p>
<highlight>Map.prototype.constructor</highlight>Returns the function that created an instance's prototype. This is the Map function by default.<br>
<highlight>Map.prototype.size</highlight>Returns the number of key/value pairs in the Map object.<br>
<p class='custom-sub-heading'>Methods</p>
<highlight>Map.prototype.clear()</highlight>Removes all key/value pairs from the Map object.<br>
<highlight>Map.prototype.delete(key)</highlight>Removes any value associated to the key and returns the value that Map.prototype.has(key) would have previously returned. Map.prototype.has(key) will return false afterwards.<br>
<highlight>Map.prototype.entries()</highlight>Returns a new Iterator object that contains an array of [key, value] for each element in the Map object in insertion order.<br>
<highlight>Map.prototype.forEach(callbackFn[, thisArg])</highlight>Calls callbackFn once for each key-value pair present in the Map object, in insertion order. If a thisArg parameter is provided to forEach, it will be used as the this value for each callback.<br>
<highlight>Map.prototype.get(key)</highlight>Returns the value associated to the key, or undefined if there is none.<br>
<highlight>Map.prototype.has(key)</highlight>Returns a boolean asserting whether a value has been associated to the key in the Map object or not.<br>
<highlight>Map.prototype.keys()</highlight>Returns a new Iterator object that contains the keys for each element in the Map object in insertion order.<br>
<highlight>Map.prototype.set(key, value)</highlight>Sets the value for the key in the Map object. Returns the Map object.<br>
<highlight>Map.prototype.values()</highlight>Returns a new Iterator object that contains the values for each element in the Map object in insertion order.<br>
<highlight>Map.prototype[@@iterator]()</highlight>Returns a new Iterator object that contains an array of [key, value] for each element in the Map object in insertion order.<br>
<p class='custom-sub-heading'>Using the Map object</p>
<pre>
<code class="language-javascript">
var myMap = new Map();
var keyString = "a string",
    keyObj = {},
    keyFunc = function () {}; 
// setting the values
myMap.set(keyString, "value associated with 'a string'");
myMap.set(keyObj, "value associated with keyObj");
myMap.set(keyFunc, "value associated with keyFunc");
console.log(myMap.size); // 3 
// getting the values
myMap.get(keyString);    // "value associated with 'a string'"
myMap.get(keyObj);       // "value associated with keyObj"
myMap.get(keyFunc);      // "value associated with keyFunc"
myMap.get("a string");   // "value associated with 'a string'"
                         // because keyString === 'a string'
console.log(myMap.get({}));           // undefined, because keyObj !== {}
console.log(myMap.get(function() {})) // undefined, because keyFunc !== function () {}
</code>
</pre>

<p class='custom-sub-heading'>Using NaN as Map keys</p>
NaN can also be used as a key. Even though every NaN is not equal to itself (NaN !== NaN is true), the following example works, because NaNs are indistinguishable from each other:
<pre>
<code class="language-javascript">var myMap = new Map();
myMap.set(NaN, "not a number");
console.log(myMap.get(NaN)); // "not a number"
var otherNaN = Number("foo");
cosnole.log(myMap.get(otherNaN)); // "not a number"
</code>
</pre>


<p class='custom-sub-heading'>Iterating Maps with for..of</p>
Maps can be iterated using a for..of loop:
<pre>
<code class="language-javascript">var myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
for (var [key, value] of myMap) {
  console.log(key + " = " + value);
}
// 0 = zero
// 1 = one
for (var key of myMap.keys()) {
  console.log(key);
}
// 0
// 1
for (var value of myMap.values()) {
  console.log(value);
}
// zero
// one
for (var [key, value] of myMap.entries()) {
  console.log(key + " = " + value);
}
// 0 = zero
// 1 = one
</code>
</pre>

<p class='custom-sub-heading'>Iterating Maps with forEach()</p>

Maps can be iterated using the forEach() method:
<pre>
<code class="language-javascript">
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
});
// Will show 2 logs; first with "0 = zero" and second with "1 = one"
</code>
</pre>

<p class='custom-heading'>Try it out here:</p>
<a href="https://jsbin.com/soqodoc/1/edit?js,console,output">https://jsbin.com/soqodoc/1/edit?js,console,output</a> <br>
<a href="https://jsbin.com/soqodoc/2/edit?js,console,output">https://jsbin.com/soqodoc/2/edit?js,console,output</a> <br>
<a href="https://jsbin.com/soqodoc/3/edit?js,console,output">https://jsbin.com/soqodoc/3/edit?js,console,output</a>

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way. <br>
http://tddbin.com/#?
