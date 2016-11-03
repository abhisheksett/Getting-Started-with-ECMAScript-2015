+++
date = "2016-09-30T14:21:45+05:30"
description = ""
draft = false
title = "Template String"

+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class='custom-heading'>What is this?</p>
ECMAScript 6 comes with the new template strings feature. Among other wonders, a template string directly supports multiline strings: 
<pre>
<code class="language-javascript">var myTooLongString = `A long time ago, in a galaxy far
 far away....
 It is a period of civil war.
 Rebel spaceships, striking
 from a hidden base, have won
 their first victory against
 the evil Galactic Empire`;
</code>
</pre>
Because all characters are significant inside a template string, I cannot add leading whitespaces.Now as JavaScript developers we have 3 ways to define strings:<br>
<highlight>With ""</highlight>
<highlight>With ''</highlight>
<highlight>With ``</highlight><br>
Multiline support is not the only feature of template strings. Indeed, you can also use a template strings to substitute placeholders with variables values . 
<pre>
<code class="language-javascript">var items = [];
items.push("banana");
items.push("tomato");
items.push("light saber");
var total = 100.5;
result.innerHTML = `You have ${items.length} item(s) in your basket for a total of $${total}`; //You have 3 item(s) in your basket for a total of $100.5
</code>
</pre>
<p class='custom-sub-heading'>Going Further with Tags</p>
The final stage of template strings specification is about adding a custom function before the string itself to create a tagged template string:
<pre>
<code class="language-javascript">var items = [];
items.push("banana");
items.push("tomato");
items.push("light saber");
var total = 100.5;
var myFunction = function (strings,...values) {
  var output = "";
  for (var index = 0; index < values.length; index++) {
    output += strings[index] + values[index];
  }
  output += strings[index]
  return output;
}

result.innerHTML = myFunction `You have ${items.length} item(s) in your basket for a total of $${total}`; //You have 3 item(s) in your basket for a total of $100.5
</code>
</pre>
The function here is used to get access to both the constant string part as well as the evaluated variables values.

In the previous example, strings and values are the following:<br>
<highlight>strings[0] = "You have "</highlight><br>
<highlight>values[0] = 3</highlight><br>
<highlight>strings[1] = "items in your basket for a total of $"</highlight><br>
<highlight>values[1] = 100.5</highlight><br>
<highlight>strings[2] = ""</highlight><br>
As you can see, every <highlight>values[n]</highlight> is surrounded by constants strings <highlight>(strings[n]</highlight> and <highlight>strings[n + 1])</highlight>.
<pre>
<code class="language-javascript">
var items = [];
items.push("banana");
items.push("tomato");
items.push("light saber");
var total = "Trying to hijack your site <BR>";
var myTagFunction = function (strings,...values) {
  var output = "";
  for (var index = 0; index < values.length; index++) {
    var valueString = values[index].toString();

    if (valueString.indexOf(">") !== -1) {
      // Far more complex tests can be implemented here :)
      return "String analyzed and refused!";
    }

    output += strings[index] + values[index];
  }

  output += strings[index]
  return output;
}

result.innerHTML = myTagFunction `You have ${items.length} item(s) in your basket for a total of $${total}`;
</code>
</pre>
Tagged template strings can used for a lot of things like security, localization, creating your own domain specific language, etc.

<p class='custom-sub-heading'>Raw Strings</p>
Tag functions have a special option when accessing string constants: They can use <highlight>strings.raw</highlight> to get the unescaped string values. For instance, in this case <highlight>\n</highlight> will not be seen as only one character but actually two <highlight>\</highlight> and <highlight>n</highlight>.
The main goal is to allow you to access the string as it was entered:
<pre>
<code class="language-javascript">

var myRawFunction = function (strings,...values) {
  var output = "";
  for (var index = 0; index < values.length; index++) {
    output += strings.raw[index] + values[index];
  }
  output += strings.raw[index]
  console.log(strings.length, values.length);
  return output;
}

result.innerHTML = myRawFunction `You have ${items.length} item(s) in your basket\n.For a total of $${total}`; //You have 3 item(s) in your basket\n.For a total of $100.5
</code>
</pre>
You can also use a new function of String: <highlight>String.raw()</highlight>. This function is a built-in function that does exactly what my previous example does:
<pre>
<code class="language-javascript">
result.innerHTML = String.raw `You have ${items.length} item(s) in your basket\n.For a total of $${total}`; //You have 3 item(s) in your basket\n.For a total of $100.5
</code>
</pre>
<p class='custom-heading'>Try it out here:</p>

https://jsbin.com/zirama/2/edit?html,js,console,output

<p class='custom-heading'>Exercise:</p>
Go to the following link and try to resolve all the errors in ES6 way.

http://tddbin.com/#?kata=es6/language/template-strings/basics

http://tddbin.com/#?kata=es6/language/template-strings/multiline

http://tddbin.com/#?kata=es6/language/template-strings/tagged

http://tddbin.com/#?kata=es6/language/template-strings/raw
