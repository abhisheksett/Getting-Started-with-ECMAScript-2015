+++
date = "2016-09-23T11:49:29+01:00"
title = "Promises"

+++

Promises

Promises provide a mechanism to handle the results and errors from asynchronous operations.  You can accomplish the same thing with callbacks, but promises provide improved readability via method chaining and succinct error handling.  Promises are currently used in many JavaScript libraries.  RSVP.js, Q.js, and the $q service in Angular are just a few of many examples.  Here is an example from the RSVP.js docs:

getJSON("/api/employee/1").then(function(post) {
  return getJSON(post.commentURL);
}).then(function(comments) {  //you could chain multiple then statements
  // proceed with access to employee
}).catch(function(error) { //succinct error handling
  // handle errors in either of the two requests
});

You can also wait for all promises to complete:

var promises = [2, 3, 5, 7, 11, 13].map(function(id){
  return getJSON("/post/" + id + ".json");
});

RSVP.all(promises).then(function(posts) {
  // posts contains an array of results for the given promises
}).catch(function(reason){
  // if any of the promises fails.
});

This pattern will look familiar to those who have written multithreaded C# code (the last example is like the WaitHandle::WaitAll method).  Unfortunately, each library has a slightly different implementation.  It’s confusing to fully grok the Q.js library only to find that the Angular $q service only provides a subset of the same functionality.  ES6 will standardize promises and remove the external dependencies currently required to use promises.  Below is a partial list and description of some of the ES6 promise functionality.  Read more ES6 promises here.
Promise.resolve(value)

I can’t describe it any better than the Mozilla docs: Returns a Promise object that is resolved with the given value. If the value is a thenable (i.e. has a then method), the returned promise will “follow” that thenable, adopting its eventual state; otherwise the returned promise will be fulfilled with the value.
Promise.cast(value)

This method is really useful if you are dealing with existing functions or services that don’t return a promise.  If the value passed in is a promise, cast returns the value, otherwise the value is coerced to a promise.  Either way, you can deal with the result as a promise.
Promise.race(iterable)

Promise.race returns the first promise in the iterable to resolve. Note the use of arrow functions. 🙂

http://www.es6fiddle.net/hruy6vlb/

var p1 = new Promise((resolve, reject) => setTimeout(resolve, 400, "one"));
var p2 = new Promise((resolve, reject) => setTimeout(resolve, 200, "two"));
Promise.race([p1, p2]).then(function(value) {
    console.log(value); //two
});

Promise.all(iterable)

The Promise.all method returns a promise when all promises in the iterable have completed.

http://www.es6fiddle.net/hruyss3j/

var p1 = new Promise((resolve, reject) => setTimeout(resolve, 400, "one"));
var p2 = new Promise((resolve, reject) => setTimeout(resolve, 200, "two"));
Promise.all([p1, p2]).then(function(value) {
    console.log(value); //one, two
});
