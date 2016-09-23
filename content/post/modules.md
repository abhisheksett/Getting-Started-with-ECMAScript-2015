+++
date = "2016-09-23T11:48:26+01:00"
title = "Modules"

+++

Modules

Modules have the potential to radically change how many JavaScript applications are structured and standardize a best practice in some already modular applications.  Modules in ES6 provide a way to load and manage dependencies via the new import and export keywords.  There are a few good solutions in ES5, namely 3rd party libraries like CommonJS  or node modules.  Modularity is a such an important concept for large applications, that it makes sense to include it as a core language feature.  The goals for ES6 modules are pretty lofty (from the ecmascript wiki, highlight is my own):

    Obviate need for globals
    Orthogonality from existing features
    Smooth refactoring from global code to modular code
    Smooth interoperability with existing JS module systems like AMD, CommonJS, and Node.js
    Fast compilation
    Simplicity and usability
    Standardized protocol for sharing libraries
    Compatibility with browser and non-browser environments
    Easy asynchronous external loading



Read more about modules on Axel’s excellent post.  Here is a code snippet from Axel showing how to load a dependent module:

<module>
        import $ from 'lib/jquery';
        var x = 123;

        // The current scope is not global
        console.log('$' in window); // false
        console.log('x' in window); // false

        // `this` still refers to the global object
        console.log(this === window); // true
</module>
