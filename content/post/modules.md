+++
date = "2016-09-23T11:48:26+01:00"
draft = false
title = "Modules"

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
JavaScript modules introduced in ECMAScript 6 is defined in its own file. The functions or variables defined in a module are not visible outside unless you explicitly export them. This means that you can write code in your module and only export those values which should be accessed by other parts of your app.

ES6 modules are declarative in nature. To export certain variables from a module you just use the keyword  <highlight>export</highlight>. Similarly, to consume the exported variables in a different module you use  <highlight>import</highlight>.

<p class='custom-sub-heading'>A Simple Module</p>


Let’s create a simple module that has two functions:

difference() : Finds difference of two numbers. </br>
sum() : Adds two numbers.
Next, let’s create a file named utility.js for the module:

<highlight>utility.js</highlight>

<pre>
<code class="language-javascript">
function diff(a,b) {
    return a-b;
}

function sum(a, b) {
    return a + b;
}
</code>
</pre>

That's it ! The "uitility.js" is a module here.

<p class='custom-heading'>Exporting and importing module</p>

<pre>
<code class="language-javascript">
function diff(a,b) {
    return a-b;
}

function sum(a, b) {
    return a + b;
}

export { diff, sum }

</code>
</pre>


The export keyword on the last line exports the two functions. As you can see, the exported functions are listed in curly braces separated by a comma. You can also rename the values while exporting like this:

<pre>
<code class="language-javascript">
export {diff as doDiff, sum as doSum}

</code>
</pre>

Now, let’s see how to consume the exported values in a different module.


<highlight>app.js</highlight>

<pre>
<code class="language-javascript">
import { diff, sum } from 'utility';
console.log(diff(18,4)); //14
console.log(sum(1, 2)); //3
</pre>
</code>
Note the first line. This imports the exported values from the module utility. If you want to import a single value (for example sum), you can do it by writing the following:
<pre>
<code class="language-javascript">
import { sum } from 'utility';
</pre>
</code>

Alternatively, you can import the module as an object and access the exports via properties:

<code><pre>
import 'utility.js' as utilObj;
console.log(utilObj.sum(3,5));//8
</pre></code>

If you are unhappy with the name that an exporting module has chosen, you can rename locally:
<code><pre>
import { diff as Difference } from 'utility';
console.log(Difference(10,7));//3
</pre></code>



<p class='custom-heading'>Default Exports and Re-exporting</p>

If you want to export a single value from the module then you can use default export. To demonstrate the usage of default exports let’s modify the utility module as shown below:

<highlight>utility.js</highlight>
<code><pre>
var utils = {
  diff: function(a,b) {
    return a-b;    
  },
  sum: function(a, b) {
    return a + b;
  }
};
export default utils;
</pre></code>

The last line just exports the object utils. It can be consumed as following in a different module:
<highlight>app.js</highlight>
<code><pre>
import utils from 'utility';
console.log(utils.diff(9,5)); //4
console.log(utils.sum(1, 2)); //3
export default utils; //exports the imported value
</pre></code>

The first line simply imports the utils object exported previously. Once you import a value you can also re-export it. The last line in the above code does that.

<p class='custom-heading'>Exercise:</p>

Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#? 
