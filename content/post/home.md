+++
date = "2016-09-23T12:21:49+01:00"
draft = false
title = "ES6 New Features overview"

+++

EcmaScript is the standardized scripting language that JavaScript (and some other languages, like ActionScript) implement.  If you think EcmaScript is a terrible name, you’re not alone.  Brendan Eich, the original developer of JavaScript, once wrote that the name EcmaScript sounds like a skin disease.  Naming aside, JavaScript is one of the most important languages in existence today.  Every browser has a JavaScript interpreter, JavaScript on the server is becoming ever more popular, and now it’s possible to use JavaScript for desktop (Chrome Apps), nativish mobile (PhoneGap) and native Windows 8 apps.  A new version of EcmaScript will have a broad impact on web development.

The current version of EcmaScript supported in modern browsers is ES5 (with some ES6 support).  ES5 drives a lot of developers mad.  Folks coming from the backend development space find ES5 lacks some pretty basic language features.  As such, several workarounds have emerged.  TypeScript is very popular in the .NET world (and here at Wintellect) and CoffeeScript is kind of a big deal™ in the Ruby community.  Both TypeScript and CoffeeScript provide syntactic sugar on top of ES5 and then are transcompiled into ES5 compliant JavaScript.  ES6 will tackle many of the core language shortcomings addressed in TypeScript and CoffeeScript.

There are quite a few new features in ES6, many still in draft form.  In this post I’ll cover classes, Arrow Functions, Modules, Block Scoping, and Promises.
