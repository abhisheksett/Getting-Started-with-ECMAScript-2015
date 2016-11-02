+++
date = "2016-11-02T14:41:55+05:30"
description = ""
draft = false
tags = []
title = "reflect"
topics = []

+++
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
ES6 introduces a new object referred as <highlight>Reflect</highlight> which exposes methods for object reflection. These new methods don’t throw exception on failure rather they return error, which makes it easy to write code involving object reflection.



<p class='custom-sub-heading'>The Reflect Object</p>
The Reflect object is not a constructor that is,we cannot use it with new operator. It’s a plain object that exposes the methods related to object reflection as its own properties. Reflect is the only object introduced by ES6 Reflect API.

 <p class='custom-sub-heading'>Reflect.get(object, property[, this])</p>
<highlight>Reflect.get</highlight> is used to retrieve value of an object property. The first parameter is the reference to the object and second parameter is the property name. If we are retrieving value of an accessor property then we can provide a third parameter which is the value of this keyword inside the get function.

<pre>
<code class="language-javascript">
var obj = {name: "narayan"};
var name = Reflect.get(obj, "name");
console.log(name); //Output "narayan"
</code>
</pre>
The <highlight>Reflect.get()</highlight> method works the same way as the dot and brackets operators for retrieving value of an object property. The only reason why you would want to use <highlight>Reflect.get()</highlight> is when you want to retrieve value of an accessor property by providing a custom value for the this keyword inside the <highlight>get</highlight> function manually.
<pre>
<code class="language-javascript">
var obj = {name: ""};
Reflect.set(obj, "name", "narayan");
console.log(obj.name); //Output "narayan"
</code>
</pre>
The <highlight>Reflect.set()</highlight> method works the same way as the dot and brackets operators for setting value of an object property. The only reason why you would want to use <highlight>Reflect.set()</highlight>is when you want to set value of an accessor property by providing a custom value for the this keyword inside the <highlight>set</highlight> function manually.



<p class='custom-sub-heading'>Reflect.defineProperty(object, property, descriptor)</p>
<highlight>Reflect.defineProperty</highlight> is used to define an object property. Its same as the <highlight>Object.defineProperty</highlight> method. <highlight>Reflect.defineProperty</highlight> takes the same three arguments as the <highlight>Object.defineProperty</highlight> method.

<pre>
<code class="language-javascript">
var obj = {};
Reflect.defineProperty(obj, "name", {value: "narayan"});
console.log(obj.name); //Output "narayan"
</code>
</pre>
<p class='custom-sub-heading'>Reflect.deleteProperty(object, property)</p>
<highlight>Reflect.deleteProperty</highlight> is used to delete an object property. It’s same as the delete operator. The first argument is the object reference and second argument is the property name.


<pre>
<code class="language-javascript">
var obj = {name: "narayan"};
Reflect.deleteProperty(obj, "name");
console.log(obj.name); //Output "undefined"
</code>
</pre>

<p class='custom-sub-heading'>Reflect.has(object, property)</p>
<highlight>Reflect.has</highlight> is used to find if an object property exists or not. It’s same as the in operator. The first argument is the object reference and second argument is the property name.

<pre>
<code class="language-javascript">
var obj = {name: "narayan"};
console.log(Reflect.has(obj, "name")); //Output "true"
</code>
</pre>
<highlight>Reflect.has()</highlight> is simply an alternate to in operator and they both can be used alternatively.

<p class='custom-sub-heading'>Reflect.getOwnPropertyDescriptor(object, property)</p>
<highlight>Reflect.getOwnPropertyDescriptor</highlight> is used to retrieve descriptor of an object property. It’s same as the <highlight>Object.getOwnPropertyDescriptor</highlight> method. The first parameter is the object reference and the second parameter is the property name.
<pre>
<code class="language-javascript">
var obj = {name: "narayan"};
var descriptor = Reflect.getOwnPropertyDescriptor(obj, "name");
console.log(descriptor); // Object {value: "narayan", writable: true, enumerable: true, configurable: true}
</code>
</pre>

<p class='custom-sub-heading'>Reflect.ownKeys(object)</p>
<highlight>Reflect.ownKeys(object)</highlight>method returns an array whose values represent the keys of the properties of an provided object. It ignores the inherited properties. The only argument we need to pass is the object reference.
<pre>
<code class="language-javascript">
var obj = {name: "narayan", profession: "developer", __proto__: {author: "SitePoint"}};
var keys = Reflect.ownKeys(obj);
console.log(keys); // ["name", "profession"]
</code>
</pre>
<p class='custom-sub-heading'>Reflect.preventExtensions(object)</p>
<highlight>Reflect.preventExtensions</highlight> method is used to mark an object as non-extensible i.e., we cannot add new properties to it. It’s same as the <highlight>Object.preventExtensions</highlight> method.
<pre>
<code class="language-javascript">
var obj = {};
Reflect.preventExtensions(obj);
obj.name = "narayan";
console.log(obj.name); //Output "undefined"
</code>
</pre>


<p class='custom-sub-heading'>Reflect.isExtensible(object)</p>
<highlight>Reflect.isExtensible</highlight> is used to check if an object is extensible or not. It same as the Object.isExtensible method. It takes only one argument that is the object reference.
<pre>
<code class="language-javascript">
var obj = {};
Reflect.preventExtensions(obj);
console.log(Reflect.isExtensible(obj)); //Output "false"
</code>
</pre>

<p class='custom-sub-heading'>Reflect.setPrototypeOf(object, prototype)</p>
<highlight>Reflect.setPrototypeOf</highlight> is used to set <highlight>[[prototype]]</highlight> of an object. The first argument is the object reference and second argument can be either null or an object.
<pre>
<code class="language-javascript">
var obj = {};
Reflect.setPrototypeOf(obj, {name: "narayan"});
console.log(obj.name); //Output "narayan"
</code>
</pre>
<p class='custom-sub-heading'>Reflect.getPrototypeOf(object)</p>
<highlight>Reflect.getPrototypeOf</highlight> is used to retrieve the <highlight>[[prototype]]</highlight> of an object. The only argument it takes is the object reference.
<pre>
<code class="language-javascript">
var obj = {};
Reflect.setPrototypeOf(obj, {name: "narayan"});
console.log(Reflect.getPrototypeOf(obj));  //Object {name: "narayan"}
</code>
</pre>


<p class='custom-sub-heading'>Reflect.apply(function[, this, args])</p>
<highlight>Reflect.apply(fucntion[,this,args])</highlight>method is used to invoke a function with a given this value. The first argument is the reference to the function object, second argument is the value of <highlight>this</highlight> keyword and finally the third argument is an array whose values will be passed as arguments while invoking the function.
<pre>
<code class="language-javascript">
function function_name(x, y)
{
    return this + x + y;
}
var value = Reflect.apply(function_name, 30, [10, 20]);
console.log(value); //Output "60"
</code>
</pre>

<p class='custom-sub-heading'>Reflect.construct(constructor[, args, prototype])</p>
The <highlight>Reflect.construct</highlight> method is used to invoke a function as a constructor. The first argument is the function reference, second argument is an array whose values will be passed as the argument to the constructor and finally the third argument is another constructor whose <highlight>prototype</highlight> will be used as the <highlight>prototype</highlight> of the currently invoked constructor.
<pre>
<code class="language-javascript">
function constructor1(a, b)
{
    this.a = a;
    this.b = b;
    this.f = function(){
        return this.a + this.b + this.c;
    } 
}
function constructor2(){}
constructor2.prototype.c = 30;
var obj = Reflect.construct(constructor1, [10, 20], constructor2);
console.log(obj.f()); //Output "60"
</code>
</pre>

<p class='custom-sub-heading'>Why use the Reflect API?</p>
In case we want to invoke a constructor with a <highlight>prototype</highlight> of another constructor then we would usually copy the original <highlight>prototype</highlight> property to a different variable and after invocation we would copy it back. But ES6 makes it easy by providing the <highlight>Reflect.constructor</highlight> method which takes a <highlight>prototype</highlight> as its third argument.

<pre>
<code class="language-javascript">
function constructor1(){}
constructor1.prototype.print = function(){
  console.log("Constructor 1");
}
function constructor2(){}
constructor2.prototype.print = function(){
  console.log("Constructor 2");
}
//In ES5
var tmpPrototype = constructor1.prototype;
constructor1.prototype = constructor2.prototype;
var obj1 = new constructor1();
obj1.print();
constructor1.prototype = tmpPrototype;
//In ES5
obj1 = Reflect.construct(constructor1, [], constructor2);
obj1.print();
</code>
</pre>


<p class='custom-heading'>Try it out here:</p>
<a href="https://jsbin.com/kimixe/3/edit?js,console">https://jsbin.com/kimixe/3/edit?js,console</a>
<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way : <br>
http://tddbin.com/#?
