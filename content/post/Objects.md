+++
date = "2016-10-24T13:12:10+05:30"
description = ""
draft = false
tags = []
title = "Objects"
topics = []

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>

ES6 focuses heavily on improving the utility of objects, which makes sense because nearly every value in JavaScript is some type of object. Additionally, the number of objects used in an average JavaScript program continues to increase as the complexity of JavaScript applications increases, meaning that programs are creating more objects all the time. With more objects comes the necessity to use them more effectively.

ES6 improves objects in a number of ways, from simple syntax extensions to options for manipulating and interacting with them.

<p class='custom-sub-heading'>Object Categories</p>
ES6 specification has clear definitions for each category of object. It’s important to understand this terminology to have a good understanding of the language as a whole. The object categories are:<br>

<highlight>Ordinary objects</highlight> Have all the default internal behaviors for objects in JavaScript. <br>
<highlight>Exotic objects</highlight> Have internal behavior that differs from the default in some way.<br>
<highlight>Standard objects</highlight> Are those defined by ES6, such as Array, Date, and so on. Standard objects            may be ordinary or exotic.<br>
<highlight>Built-in objects</highlight> Are present in a JavaScript execution environment when a script begins to execute. All standard objects are built-in objects.<br>


<p class='custom-heading'>Object Literal Syntax Extensions</p>
ES6 makes object literals more powerful and even more succinct by extending the syntax in several ways.

<p class='custom-sub-heading'>Property Initializer Shorthand</p>

In ES5 and earlier, object literals were simply collections of name-value pairs. That meant there could be some duplication when property values are initialized. For example:
<pre>
<code class="language-javascript">
function createPerson(name, age) {
    return {
        name: name,
        age: age
    };
}
</code>
</pre>
The <highlight>createPerson()</highlight> function creates an object whose property names are the same as the function parameter names. The result appears to be duplication of <highlight>name</highlight> and <highlight>age</highlight> even though one is the name of an object property while the other provides the value for that property. The key <highlight>name</highlight> in the returned object is assigned the value contained in the variable <highlight>name</highlight>, and the key <highlight>age</highlight> in the returned object is assigned the value contained in the variable <highlight>age</highlight>.

In ES6, you can eliminate the duplication that exists around property names and local variables by using the property initializer shorthand. When an object property name is the same as the local variable name, you can simply include the <highlight>name</highlight> without a colon and value. For example, <highlight>createPerson() </highlight>can be rewritten for ES6 as follows:
<pre>
<code class="language-javascript">
function createPerson(name, age) {
    return {
        name,
        age
    };
}
</code>
</pre>
When a property in an object literal only has a name, the JavaScript engine looks into the surrounding scope for a variable of the same name. If it finds one, that variable’s value is assigned to the same name on the object literal. In this example, the object literal property name is assigned the value of the local variable name.

This extension makes object literal initialization even more succinct and helps to eliminate naming errors. Assigning a property with the same name as a local variable is a very common pattern in JavaScript, making this extension a welcome addition.

<p class='custom-sub-heading'>Concise Methods</p>
ES6 also improves the syntax for assigning methods to object literals. In ES5 and earlier, you must specify a name and then the full function definition to add a method to an object, as follows:
<pre>
<code class="language-javascript">
var person = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};
</code>
</pre>
In ES6, the syntax is made more concise by eliminating the colon and the function keyword. That means you can rewrite the previous example like this:
<pre>
<code class="language-javascript">
var person = {
    name: "Nicholas",
    sayName() {
        console.log(this.name);
    }
};
</code>
</pre>
This shorthand syntax, also called concise method syntax, creates a method on the person object just as the previous example did. The <highlight>sayName()</highlight> property is assigned an anonymous function and has all the same characteristics as the ES5 <highlight>sayName()</highlight> function. The one difference is that concise methods may use <highlight>super</highlight> (discussed later in the “Easy Prototype Access with Super References” section), while the nonconcise methods may not.

<highlight>Note</highlight>The name property of a method created using concise method shorthand is the name used before the parentheses. In the last example, the name property for <highlight>person.sayName()</highlight>is "sayName".

<p class='custom-sub-heading'>Computed Property Names</p>
In ES6, computed property names are part of the object literal syntax, and they use the same square bracket notation that has been used to reference computed property names in object instances. For example:

<pre>
<code class="language-javascript">
var lastName = "last name";

var person = {
    "first name": "Nicholas",
    [lastName]: "Zakas"
};

console.log(person["first name"]);      // "Nicholas"
console.log(person[lastName]);          // "Zakas"
</code>
</pre>
The square brackets inside the object literal indicate that the property name is computed, so its contents are evaluated as a string. That means you can also include expressions such as:


<pre>
<code class="language-javascript">
var suffix = " name";

var person = {
    ["first" + suffix]: "Nicholas",
    ["last" + suffix]: "Zakas"
};

console.log(person["first name"]);      // "Nicholas"
console.log(person["last name"]);       // "Zakas"
</code>
</pre>

These properties evaluate to <highlight>"first name"</highlight> and </highlight>"last name"</highlight>, and those strings can be used to reference the properties later. Anything you would put inside square brackets while using bracket notation on object instances will also work for computed property names inside object literals.

<p class='custom-heading'>New Methods</p>
One of the design goals of ECMAScript beginning with ES5 was to avoid creating new global functions or methods on <highlight>Object.prototype</highlight>, and instead try to find objects on which new methods should be available. As a result, the Object global has received an increasing number of methods when no other objects are more appropriate. ES6 introduces a couple new methods on the Object global that are designed to make certain tasks easier.

<p class='custom-sub-heading'>The Object.is() Method</p>
When you want to compare two values in JavaScript, you’re probably used to using either the equals operator (==) or the identically equals operator (===). Many developers prefer the latter, to avoid type coercion during comparison. But even the identically equals operator isn’t entirely accurate. For example, the values +0 and -0 are considered equal by === even though they are represented differently in the JavaScript engine. Also NaN === NaN returns false, which necessitates using isNaN() to detect NaN properly.

ES6 introduces the <highlight>Object.is()</highlight> method to make up for the remaining quirks of the identically equals operator. This method accepts two arguments and returns true if the values are equivalent. Two values are considered equivalent when they are of the same type and have the same value. Here are some examples:

<pre>
<code class="language-javascript">
console.log(+0 == -0);              // true
console.log(+0 === -0);             // true
console.log(Object.is(+0, -0));     // false

console.log(NaN == NaN);            // false
console.log(NaN === NaN);           // false
console.log(Object.is(NaN, NaN));   // true

console.log(5 == 5);                // true
console.log(5 == "5");              // true
console.log(5 === 5);               // true
console.log(5 === "5");             // false
console.log(Object.is(5, 5));       // true
console.log(Object.is(5, "5"));     // false
</code>
</pre>
<p class='custom-sub-heading'>The Object.assign() Method</p>

 Here’s an example to use object.assign() in ES6:
<pre>
<code class="language-javascript">
 function EventTarget() { /*...*/ }
EventTarget.prototype = {
    constructor: EventTarget,
    emit: function() { /*...*/ },
    on: function() { /*...*/ }
}
var myObject = {}
Object.assign(myObject, EventTarget.prototype);
myObject.emit("somethingChanged");
</code>
</pre>
The Object.assign() method accepts any number of suppliers, and the receiver receives the properties in the order in which the suppliers are specified. That means the second supplier might overwrite a value from the first supplier on the receiver, which is what happens in this snippet:
<pre>
<code class="language-javascript">
var receiver = {};
Object.assign(receiver,
    {
        type: "js",
        name: "file.js"
    },
    {
        type: "css"
    }
);
console.log(receiver.type);     // "css"
console.log(receiver.name);     // "file.js"
</code>
</pre>
The value of <highlight>receiver.type</highlight> is "css" because the second supplier overwrote the value of the first.


<p class='custom-sub-heading'>Working with Accessor Properties</p>
Keep in mind that <highlight>Object.assign()</highlight> doesn’t create accessor properties on the receiver when a supplier has accessor properties. Since <highlight>Object.assign()</highlight> uses the assignment operator, an accessor property on a supplier will become a data property on the receiver. For example:
<pre>
<code class="language-javascript">
var receiver = {},
    supplier = {
        get name() {
            return "file.js"
        }
    };
Object.assign(receiver, supplier);
var descriptor = Object.getOwnPropertyDescriptor(receiver, "name");
console.log(descriptor.value);      // "file.js"
console.log(descriptor.get);        // undefined
</code>
</pre>
In this code, the supplier has an accessor property called <highlight>name</highlight>. After using the <highlight>Object.assign()</highlight> method, receiver.name exists as a data property with a value of <highlight>"file.js"</highlight> because <highlight>supplier.name</highlight> returned <highlight>"file</highlight>.js" when <highlight>Object.assign()</highlight> was called.

<p class='custom-sub-heading'>Duplicate Object Literal Properties</p>
ES5 strict mode introduced a check for duplicate object literal properties that would throw an error if a duplicate was found. For example, this code was problematic:
<pre>
<code class="language-javascript">
"use strict";
var person = {
    name: "Nicholas",
    name: "Greg"        // syntax error in ES5 strict mode
};
</code>
</pre>
When running in ES5 strict mode, the second name property causes a syntax error. But in ES6, the duplicate property check was removed. Both strict and nonstrict mode code no longer check for duplicate properties. Instead, the last property of the given name becomes the property’s actual value, as shown here:
<pre>
<code class="language-javascript">
"use strict";
var person = {
    name: "Nicholas",
    name: "Greg"        // no error in ES6 strict mode
};
console.log(person.name);       // "Greg"
</code>
</pre>
In this example, the value of <highlight>person.name</highlight> is "Greg" because that’s the last value assigned to the property.

<p class='custom-sub-heading'>Own Property Enumeration Order</p>
ES6 strictly defines the order in which own properties must be returned when they are enumerated. This affects how properties are returned using <highlight>Object.getOwnPropertyNames()</highlight> and <highlight>Reflect.ownKeys</highlight>. It also affects the order in which properties are processed by <highlight>Object.assign()</highlight>.

The basic order for own property enumeration is:

All numeric keys in ascending order<br>
All string keys in the order in which they were added to the object<br>
All symbol keys in the order in which they were added to the object<br>
Here’s an example:
<pre>
<code class="language-javascript">
var obj = {
    a: 1,
    0: 1,
    c: 1,
    2: 1,
    b: 1,
    1: 1
};
obj.d = 1;
console.log(Object.getOwnPropertyNames(obj).join(""));     // "012acbd"
</code>
</pre>
The </highlighht>Object.getOwnPropertyNames()</highlight> method returns the properties in obj in the order 0, 1, 2, a, c, b, d. Note that the numeric keys are grouped together and sorted, even though they appear out of order in the object literal. The string keys come after the numeric keys and appear in the order that they were added to obj. The keys in the object literal itself come first, followed by any dynamic keys that were added later (in this case, d).

<p class='custom-sub-heading'>Changing an Object’s Prototype</p>
ES6 has <highlight>Object.setPrototypeOf()</highlight> method, which allows you to change the prototype of any given object. The <highlight>Object.setPrototypeOf()</highlight> method accepts two arguments: the object whose prototype should change and the object that should become the first argument’s prototype. For example:
<pre>
<code class="language-javascript">
let person = {
    getGreeting() {
        return "Hello";
    }
};
let dog = {
    getGreeting() {
        return "Woof";
    }
};
// prototype is person
let friend = Object.create(person);
console.log(friend.getGreeting());                      // "Hello"
console.log(Object.getPrototypeOf(friend) === person);  // true
// set prototype to dog
Object.setPrototypeOf(friend, dog);
console.log(friend.getGreeting());                      // "Woof"
console.log(Object.getPrototypeOf(friend) === dog);     // true
</code>
</pre>
This code defines two base objects: person and dog. Both objects have a <highlight>getGreeting()</highlight> method that returns a string. The object friend first inherits from the person object, meaning that <highlight>getGreeting()</highlight> outputs "Hello". When the prototype becomes the dog object, <highlight>person.getGreeting()</highlight> outputs "Woof" because the original relationship to person is broken.

The actual value of an object’s prototype is stored in an internal-only property called <highlight>[[Prototype]]</highlight>. The <highlight>Object.getPrototypeOf()</highlight> method returns the value stored in <highlight>[[Prototype]]</highlight> and <highlight>Object.setPrototypeOf()</highlight> changes the value stored in <highlight>[[Prototype]]</highlight>. 

<p class='custom-sub-heading'>Easy Prototype Access with Super References</p>
Another improvement is the introduction of <highlight>super</highlight> references, which make accessing functionality on an object’s prototype easier. For example, to override a method on an object instance such that it also calls the prototype method of the same name, you’d do the following:
<pre>
<code class="language-javascript">
let person = {
    getGreeting() {
        return "Hello";
    }
};
let dog = {
    getGreeting() {
        return "Woof";
    }
};

let friend = {
    getGreeting() {
        return Object.getPrototypeOf(this).getGreeting.call(this) + ", hi!";
    }
};
// set prototype to person
Object.setPrototypeOf(friend, person);
console.log(friend.getGreeting());                      // "Hello, hi!"
console.log(Object.getPrototypeOf(friend) === person);  // true
// set prototype to dog
Object.setPrototypeOf(friend, dog);
console.log(friend.getGreeting());                      // "Woof, hi!"
console.log(Object.getPrototypeOf(friend) === dog);     // true
</code>
</pre>
In this example, <highlight>getGreeting()</highlight> on friend calls the prototype method of the same name. The <highlight>Object.getPrototypeOf()</highlight> method ensures the correct prototype is called, and then an additional string is appended to the output. The additional <highlight>.call(this)</highlight> ensures that the this value inside the prototype method is set correctly.

Remembering to use <highlight>Object.getPrototypeOf()</highlight> and <highlight>.call(this)</highlight> to call a method on the prototype is a bit involved, so ES6 introduced <highlight>super</highlight>. At its simplest, super is a pointer to the current object’s prototype, effectively the <highlight>Object.getPrototypeOf(this)</highlight> value. Knowing that, you can simplify the <highlight>getGreeting()</highlight>method as follows:
<pre>
<code class="language-javascript">
let friend = {
    getGreeting() {
        // in the previous example, this is the same as:
        // Object.getPrototypeOf(this).getGreeting.call(this)
        return super.getGreeting() + ", hi!";
    }
};
</pre>
</code>
The call to <highlight>super.getGreeting()</highlight> is the same as <highlight>Object.getPrototypeOf(this).getGreeting.call(this)</highlight> in this context. Similarly, you can call any method on an object’s prototype by using a super reference, so long as it’s inside a concise method. Attempting to use super outside of concise methods results in a syntax error, as in this example:
<pre>
<code class="language-javascript">
let friend = {
    getGreeting: function() {
        // syntax error
        return super.getGreeting() + ", hi!";
    }
};
</code>
</pre>
This example uses a named property with a function, and the call to <highlight>super.getGreeting()</highlight> results in a syntax error because super is invalid in this context.

The super reference is really powerful when you have multiple levels of inheritance, because in that case, <highlight>Object.getPrototypeOf()</highlight> no longer works in all circumstances. For example:
<pre>
<code class="language-javascript">
let person = {
    getGreeting() {
        return "Hello";
    }
};
// prototype is person
let friend = {
    getGreeting() {
        return Object.getPrototypeOf(this).getGreeting.call(this) + ", hi!";
    }
};
Object.setPrototypeOf(friend, person);
// prototype is friend
let relative = Object.create(friend);
console.log(person.getGreeting());                  // "Hello"
console.log(friend.getGreeting());                  // "Hello, hi!"
console.log(relative.getGreeting());                // error!
</code>
</pre>
The call to <highlight>Object.getPrototypeOf()</highlight> results in an error when relative.<highlight>getGreeting()</highlight> is called. That’s because this is relative, and the prototype of relative is the friend object. When <highlight>friend.getGreeting().call()</highlight> is called with relative as this, the process starts over again and continues to call recursively until a stack overflow error occurs.
That problem is difficult to solve in ES5, but with ES6 and super, it’s easy:
<pre>
<code class="language-javascript">
let person = {
    getGreeting() {
        return "Hello";
    }
};
// prototype is person
let friend = {
    getGreeting() {
        return super.getGreeting() + ", hi!";
    }
};
Object.setPrototypeOf(friend, person);
// prototype is friend
let relative = Object.create(friend);
console.log(person.getGreeting());                  // "Hello"
console.log(friend.getGreeting());                  // "Hello, hi!"
console.log(relative.getGreeting());                // "Hello, hi!"
</code>
</pre>
Because super references are not dynamic, they always refer to the correct object. In this case, <highlight>super.getGreeting()</highlight> always refers to <highlight>person.getGreeting()</highlight>, regardless of how many other objects inherit the method.

<p class='custom-sub-heading'>A Formal Method Definition</p>
ES6 formally defines a method as a function that has an internal <highlight>[[HomeObject]]</highlight> property containing the object to which the method belongs. Consider the following:

<pre>
<code class="language-javascript">
let person = {

    // method
    getGreeting() {
        return "Hello";
    }
};
// not a method
function shareGreeting() {
    return "Hi!";
}
</code>
</pre>
This example defines person with a single method called <highlight>getGreeting()</highlight>. The <highlight>[[HomeObject]]</highlight> for <highlight>getGreeting()</highlight> is person by virtue of assigning the function directly to an object. The shareGreeting() function, on the other hand, has no <highlight>[[HomeObject]]</highlight> specified because it wasn’t assigned to an object when it was created. In most cases, this difference isn’t important, but it becomes very important when using super references.

Any reference to super uses the <highlight>[[HomeObject]]</highlight> to determine what to do. The first step is to call <highlight>Object.getPrototypeOf()</highlight> on the <highlight>[[HomeObject]]</highlight> to retrieve a reference to the prototype. Then, the prototype is searched for a function with the same name. Last, the this binding is set and the method is called. Here’s an example:
<pre>
<code class="language-javascript">
let person = {
    getGreeting() {
        return "Hello";
    }
};
// prototype is person
let friend = {
    getGreeting() {
        return super.getGreeting() + ", hi!";
    }
};
Object.setPrototypeOf(friend, person);
console.log(friend.getGreeting());  // "Hello, hi!"
</code>
</pre>
Calling <highlight>friend.getGreeting()</highlight> returns a string, which combines the value from <highlight>person.getGreeting()</highlight> with ", hi!". The <highlight>[[HomeObject]]</highlight> of <highlight>friend.getGreeting()</highlight> is friend, and the prototype of friend is person, so <highlight>super.getGreeting()</highlight> is equivalent to <highlight>person.getGreeting.call(this)</highlight>.


<p class='custom-heading'>Try it out here:</p>
http://jsbin.com/fuyoyun/1/edit?js,console   <br>
http://jsbin.com/fuyoyun/4/edit?js,console
<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?