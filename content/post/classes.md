+++
date = "2016-09-23T11:42:03+01:00"
draft = false
title = "Classes"

+++

Classes

There are several options to approximate classes in ES5.  The most common approach is probably the special constructor function like this http://jsfiddle.net/noelstieglitz/a5heA/

function Car( make ) { //approximate a class/constructor
   this.make = make;
   this.currentSpeed = 25;

   this.printCurrentSpeed = function(){ //expose a function
          console.log(this.make + ' is going ' + this.currentSpeed + ' mph.');
    }
}

// Instantiate a new car
var moderatelyPricedCar = new Car( "Kia");
moderatelyPricedCar.printCurrentSpeed(); //Kia is going 25 mph.

Approximate no more!  ES6 introduces language support for classes (class keyword), constructors (constructor keyword), and the extend keyword for inheritance.  The developer’s intent is much more clear using the ES6 syntax. http://www.es6fiddle.net/hrut24r0/

class Car {
    constructor(make) { //constructors!
        this.make = make;
      this.currentSpeed = 25;
    }

    printCurrentSpeed(){
          console.log(this.make + ' is going ' + this.currentSpeed + ' mph.');
    }
}

class RaceCar extends Car { //inheritance
    constructor(make, topSpeed) {
        super(make); //call the parent constructor with super
        this.topSpeed = topSpeed;
    }

    goFast(){
          this.currentSpeed = this.topSpeed;
    }
}

let stang = new RaceCar('Mustang', 150);

stang.printCurrentSpeed();
stang.goFast();
stang.printCurrentSpeed();

If you love prototypical inheritance, no need to fret.  You can still use prototypical inheritance in ES6.
