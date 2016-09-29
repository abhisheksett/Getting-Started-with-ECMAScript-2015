+++
date = "2016-09-23T11:42:03+01:00"
draft = false
title = "Classes"

+++
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>

JavaScript classes introduced in ECMAScript 6 are syntactical sugar over JavaScript's existing prototype-based inheritance. The class syntax is not introducing a new object-oriented inheritance model to JavaScript. JavaScript classes provide a much simpler and clearer syntax to create objects and deal with inheritance.

Class concept in ES6 is almost similar like classes in Python or Java. There are 2 ways we can define classes.
<ul><highlight>Class declarations</highlight></ul>
<ul><highlight>Class expression</highlight></ul>


<p class='custom-sub-heading'>Class declarations</p>

Keyword <highlight>class</highlight> is used along with class name to declare a class. For example:
<pre>
<code class="language-javascript">
class Vehicle {
  constructor(description, wheels) {
    this.description = description;
    this.wheels = wheels;
  }
}
</code>
</pre>
<div class='warning'>
  An important difference between function declarations and class declarations is that function declarations are hoisted and class declarations are not. Class needs to be declared first and then access it, otherwise code like the following will throw a ReferenceError:
</div>

<pre>
<code class="language-javascript">
var v = new Vehicle(); // ReferenceError

class Vehicle {}
</code>
</pre>

<p class='custom-sub-heading'>Class declarations</p>

A class expression is another way to define a class. Class expressions can be named or unnamed. The name given to a named class expression is local to the class's body. Example:

<pre>
<code class="language-javascript">
//unnamed
var Vehicle = class {
  constructor(description, wheels) {
    this.description = description;
    this.wheels = wheels;
  }
};
</code>
</pre>

<p class='custom-heading'>How to use it?</p>

Before going for example, there is an important note:
<div class='info'>
The <b>constructor</b> method is a special method for creating and initializing an object created with a class. There can only be one special method with the name <b>"constructor"</b> in a class. A SyntaxError will be thrown if the class contains more than one occurrence of a constructor method.
</div>
Here is an complete example of class with inheritance:

<pre>
<code class="language-javascript">
class AvengersMember {
  constructor(actor, role){
    this.actor = actor;
    this.role = role;
  }

  describeRole() {
    console.log(`${this.actor} played role of ${this.role} in Avengers`);
  }
}

let avengerMembers = new AvengersMember('Christian Bale', 'Batman');
avengerMembers.describeRole();

//Output
"Christian Bale played role of Batman in Avengers"

class Avengers extends AvengersMember{
  constructor(actor, role){
    super(actor, role);
  }
}

let avengers = new Avengers('Robert Downey Jr', 'Iron Man');
avengers.describeRole();

//Output
"Robert Downey Jr played role of Iron Man in Avengers"
</code>
</pre>

<p class='custom-heading'>Explanation</p>

In above example, Avengers class is extending AvengersMember class. All the functions and variables of Avengers class are now member of
AvengersMember class. When avengersMember.describeRole() is called, it takes the actor and role from parent class which got assigned
as part of 'super()' call.

<p class='custom-sub-heading'>Static method</p>

The static keyword defines a static method for a class. Static methods are called without instantiating their class and are also not callable when the class is instantiated. Static methods are often used to create utility functions for an application.

For example:
<pre>
<code class="language-javascript">
class AvengersMember {
  constructor(actor, role){
    this.actor = actor;
    this.role = role;
  }
}
describeRole() {
  console.log(\`${this.actor} played role of ${this.role} in Avengers\`);
}
static defaultRole() {
  console.log(\`Chris Evans played role of Captain America in Avengers\`);
}
AvengersMember.defaultRole();
//Output
"Chris Evans played role of Captain America in Avengers"
</code>
</pre>


<p class='custom-heading'>How ES5 did it?</p>

<pre>
<code class="language-javascript">
function AvengersMember(actor, role) {
    this.actor = actor;
    this.role = role;
}
AvengersMember.prototype.describeRole = function(){
  console.log(this.actor+' played role of '+this.role+' in Avengers');
}
let avengerMembers = new AvengersMember('Christian Bale', 'Batman');
avengerMembers.describeRole();

function Avengers(actor, role) {
  Avengers.prototype.constructor(actor, role);
}

Avengers.prototype = new AvengersMember();

let avengers = new Avengers('Robert Downey Jr', 'Iron Man');
avengers.describeRole();
</pre>
</code>

<p class='custom-heading'>Try it out here:</p>

https://jsfiddle.net/qk7vL83e/

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?kata=es6/language/class/creation <br/>
http://tddbin.com/#?kata=es6/language/class/accessors <br/>
http://tddbin.com/#?kata=es6/language/class/static <br/>
http://tddbin.com/#?kata=es6/language/class/extends <br/>
http://tddbin.com/#?kata=es6/language/class/more-extends <br/>
http://tddbin.com/#?kata=es6/language/class/super-in-method <br/>
http://tddbin.com/#?kata=es6/language/class/super-in-constructor <br/>
