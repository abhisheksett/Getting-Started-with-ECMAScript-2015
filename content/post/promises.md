+++
date = "2016-09-23T11:49:29+01:00"
title = "Promises"
draft = false

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>

Promises give us a way to handle asynchronous processing in a more synchronous fashion. They represent a value that we can handle at some point in the future. And, better than callbacks here, Promises give us guarantees about that future value, specifically:

<ol>
  <li>No other registered handlers of that value can change it (<i>the Promise is immutable</i>)</li>
  <li>We are guaranteed to receive the value, regardless of when we register a handler for it, even if it's already resolved (<i>in contrast to events, which can incur race conditions</i>).</li>
</ol>

<p class='custom-sub-heading'>How to create a promise</p>

The standard way to create a Promise is by using the new Promise constructor which accepts a handler that is given two functions as parameters. The first handler (<i>typically named <highlight>resolve</highlight></i>) is a function to call with the future value when it's ready; and the second handler (<i>typically named <highlight>reject</highlight></i>) is a function to call to reject the Promise if it can't resolve the future value.

For Example:

<pre>
<code class="language-javascript">
var p = new Promise(function(resolve, reject) {  
   if (/* condition */) {
      resolve(/* value */);  // fulfilled successfully
   }
   else {
      reject(/* reason */);  // error, rejected
   }
});
</code>
</pre>

A Promise is in one of these states:

<ul>
  <li><i><highlight>pending:</highlight></i> initial state, not fulfilled or rejected.
  <li><i><highlight>fulfilled:</highlight></i> meaning that the operation completed successfully.
  <li><i><highlight>rejected:</highlight></i> meaning that the operation failed.
</ul>

A pending promise can either be fulfilled with a value, or rejected with a reason (error). When either of these happens, the associated handlers queued up by a promise's then method are called. (If the promise has already been fulfilled or rejected when a corresponding handler is attached, the handler will be called, so there is no race condition between an asynchronous operation completing and its handlers being attached.)

Here is the idea of a promise:

<img src="/img/promises.png" />

<p class='custom-sub-heading'>How to use a promise</p>

Once we have a Promise, it can be passed around as a value. The Promise is a stand-in for a future value; and so it can be returned from a function, passed as a parameter and used in any other way a standard value would be used.

To consume the Promise - meaning we want to process the Promises value once fulfilled - we attach a handler to the Promise using it's .then() method. This method takes a function that will be passed the resolved value of the Promise once it is fulfilled.

<pre>
<code class="language-javascript">
var p = new Promise((resolve, reject) => resolve(5));  
p.then((val) => console.log(val)); // 5  
</code>
</pre>

A Promise's .then() method actually takes two possible parameters. The first is the function to be called when the Promise is fulfilled and the second is a function to be called if the Promise is rejected.

<pre>
<code class="language-javascript">
p.then((val) => console.log("fulfilled:", val),  
       (err) => console.log("rejected: ", err));  
</code>
</pre>

<p class='custom-heading'>Example</p>

<pre>
<code class="language-javascript">
'use strict';
var promiseCount = 0;

(function() {
    var thisPromiseCount = ++promiseCount;

    document.getElementById('output').innerHTML += `Sync code started\n`;

    // We make a new promise: we promise a numeric count of this promise, starting from 1 (after waiting 3s)
    var p1 = new Promise(
        // The resolver function is called with the ability to resolve or
        // reject the promise
        function(resolve, reject) {
            document.getElementById('output').innerHTML += `Async code started\n`;
            // This is only an example to create asynchronism
            window.setTimeout(
                function() {
                    // We fulfill the promise !
                    resolve(thisPromiseCount);
                }, Math.random() * 2000 + 1000);
        }
    );

    // We define what to do when the promise is resolved/fulfilled with the then() call,
    // and the catch() method defines what to do if the promise is rejected.
    p1.then(
        // Log the fulfillment value
        function(val) {
            document.getElementById('output').innerHTML += `Async code terminated\n`;
        })
    .catch(
        // Log the rejection reason
        function(reason) {
            document.getElementById('output').innerHTML += `Handle rejected promise ${reason} here\n`;
        });

    document.getElementById('output').innerHTML += `Sync code terminated\n`;
})();

//Output
Sync code started
Async code started
Sync code terminated
Async code terminated //Gets called after few seconds
</code>
</pre>

<p class='custom-sub-heading'>Working with multiple promises</p>

Sometimes we're working with multiple Promises and we need to be able to start our processing when all of them are fulfilled. This is where <highlight>Promise.all()</highlight> comes in. Promise.all() takes an array of Promises and once all of them are fulfilled it fulfills its returned Promise with an array of their fulfilled values.

For example, let's say we have a function wrapper around jQuery's .getJSON() method to fetch JSON results from a url which returns a Promise.

<pre>
<code class="language-javascript">
var fetchJSON = function(url) {  
  return new Promise((resolve, reject) => {
    $.getJSON(url)
      .done((json) => resolve(json))
      .fail((xhr, status, err) => reject(status + err.message));
  });
}
</code>
</pre>

Now we can setup an array of promises which will fulfill with the JSON results of fetching the response from each of the urls in our itemUrls array. Promise.all() will not fulfill until all the Promises in the array have fulfilled. If any of those promises are rejected (or throw an exception) then the Promise.all() Promise will reject and the .catch() below will be triggered.

<pre>
<code class="language-javascript">
var itemUrls = {  
    'http://www.api.com/items/1234',
    'http://www.api.com/items/4567'
  },
  itemPromises = itemUrls.map(fetchJSON);

  Promise.all(itemPromises)  
  .then(function(results) {
     // we only get here if ALL promises fulfill
     results.forEach(function(item) {
       // process item
     });
  })
  .catch(function(err) {
    // Will catch failure of first failed promise
    console.log("Failed:", err);
  });
</code>
</pre>

<div class="warning">
Keep in mind, a failure (rejection or thrown exception) of any of the Promises in the array passed to Promise.all() will cause the Promise it returns to be rejected.
</div>

<div class="info">
Sometimes, we don't need to wait on all the Promises in our array; but we simply want to get the results of the first Promise in the array to fulfill. We can do this with <highlight>Promise.race()</highlight>, which, like Promise.all(), takes an array of promises; but unlike Promise.all() will fulfill its returned Promise as soon as the first Promise in that array fulfills.
</div>

<p class='custom-heading'>Try it out here:</p>

https://jsfiddle.net/r594gt5h/2/

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?kata=es6/language/promise/creation <br/>
http://tddbin.com/#?kata=es6/language/promise/chaining-then <br/>
http://tddbin.com/#?kata=es6/language/promise/api <br/>
http://tddbin.com/#?kata=es6/language/promise/catch <br/>
