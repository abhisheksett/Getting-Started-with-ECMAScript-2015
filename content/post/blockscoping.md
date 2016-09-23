+++
date = "2016-09-23T11:53:50+01:00"
title = "Block Scoping"

+++

Block Scoping

Scoping in JavaScript is confusing for developers with a C/C#/Java background.  Hoisting can add to that confusion.  In ES5, variables are either globally or locally function scoped.  The lack of block scoping has caused confusion in ES5, and resulted in some interesting patterns to achieve block scope.  In ES6, you can use the new let keyword to achieve block scoping. http://www.es6fiddle.net/hrut3qnv/

var num = 0; //globally scoped

for (let i = 0; i < 10; i++) { //i is block scoped
  num += i;
  console.log('value of i in block: ' + i);
}

console.log('Is i defined here?: ' + (typeof i !== 'undefined')); //Is i defined here?: false
