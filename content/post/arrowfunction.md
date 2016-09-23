+++
date = "2016-09-23T11:56:13+01:00"
title = "Arrow Function"
draft = false

+++

Arrow Functions


Many features in ES6 could fundamentally change how new JavaScript applications are architected.  Arrow functions is not going to fundamentally change anything.  Still, it’s one of my favorite features.  Arrow functions provide two features: lexical scoping of the this keyword and less ceremony when defining an anonymous function.

Without arrow functions, every function defines a this value.  No more will you need to reassign this like you have probably done in the next code snippet:

http://jsfiddle.net/noelstieglitz/wfJL5/

function Car() {
  var self = this; //locally assign this that can be closed over
  self.speed = 0;

  setInterval(function goFaster() {
    //this has a different scope, but we can use the self variable to reference the parent "this"
    self.speed += 5;
      console.log('now going: ' + self.speed);
  }, 1000);
}

var car = new Car();

The above snippet could be rewritten as

http://www.es6fiddle.net/hrw5xz4f/

function Car() { //Note, we could use the new Class feature in ES6 instead
  this.speed = 0;

  setInterval(() => {
    this.speed += 5; //this is from Car
    console.log
    console.log('now going: ' + this.speed);
  }, 1000);
}

If you’re a C# developer who has ever used lambda expressions, the syntax will feel very familiar.  Check out the ecmascript.org wiki regarding arrow functions:

Hard to beat C# and CoffeeScript here (we want the unparenthesized single-parameter form as in C#).

TC39 should embrace, clean-up, and extend rather than re-invent or compete with de-facto and nearby de-jure standards.

I can’t agree more.  Here is some ES5 code that will calculate the square of every value in an array and log the value to the console http://jsfiddle.net/noelstieglitz/LLDBp/1/

var x = [0,1,2];
x.map(function (x) { //anonymous function
  console.log(x * x);
});

In comparison, the ES6 arrow function syntax is really clean http://www.es6fiddle.net/hruu11fz/

let x = [0,1,2];
x.map(x => console.log(x * x)); //arrow function
