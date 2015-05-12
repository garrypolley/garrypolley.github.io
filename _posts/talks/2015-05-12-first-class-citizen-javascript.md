---
layout: post
title: 'First Class Citizen: JavaScript'
slideshow: 'https://goo.gl/VgxV33'
slideshowId: '1wpYhg5KxYcjCh5X2LohTxT9b3gyEKts-tCDaxbYYe4Q'
---

Think of the last time you were given a project or a new website to build.
The coding language for the server was not what you focused on.
You likely thought more about how complex the site would be and
what server side framework you would use to create the site.

Let's say you worked through the feature list and landed on using Rails or
Django as your server side web framework. Here are a few assumptions you made
by choosing to have Python or Ruby as your core language (even if this was not a
conscience choice):

* Consistent and stable runtime
* Manageable testing
* Error handling
* Built in logging

Why bring up these fairly standard features which exist in nearly every modern
language? Because, most people seem to think JavaScript either does
not have these features or people choose not use these features. In either case
I'll cover why JavaScript has all of these features and why we should rely on
them instead of living in fear of them. I also plan to dispel what I believe
is a commonly held myth: "Your JavaScript **_will_** fail."

Hitting on that last point first, let's start with what drives your thoughts
when it comes to core language assumptions.

## Why does your mindset matter?

If you live by the thought: "My JavaScript _will_ fail" then it will fail.
Think about it. If you wrote server side code under the assumption it **_will_**
fail, you lack confidence in your application. Further if you lived
under this thought you would probably not use the language or framework causing
this much doubt in your applications. Do not misunderstand
my point here. I am _not_ saying that JavaScript **_can't_** fail. I am saying that
your mindset should be: "My JavaScript _can_ fail".

With the broader mind set of: "Code _can_ fail" you will approach problems differently.
-- Notice I said _code_, that's because this is how I think you should mentally
approach all languages and frameworks you use in application development. --
Instead of building for edge cases and having layers of fall back you can build
the same as you do for the server.  For instance if the server called another
service you would not "progressively" enhance your interpretation of the service response.
You assume you have some stability and _reasonably_ handle failures. Maybe you return a
500 in those cases but give a reasonable message on what went wrong, or tell the user
to try again. Similar approaches can be taken on the client

Instead of doing a complex fall back strategy for a feature you can (and should)
implement the one that _should_ always work and in the case of failure _reasonably_
handle the failure. For example, when building a visualization
you can use something like [D3][d3-url] or [R2D3][r2d2-url].  If the visualization is unable to be
built in the particular browser, don't just fail or try to fall back to a
bunch of different layers. Have a table be the one time fall back.

The difference between _will_ fail and _can_ fail: _will_ fail
mindset tries to build many layers of fall back (e.g. canvas, divs). This leads to more
complicated code as well as less reliable code. A _can_ fail mindset builds for the
common successful case and _reasonably_ handles failure. We need to handle errors on the client the same as we do
the server. It's not okay to gobble up errors and move on. Later we'll see how you can
gracefully handle errors and report on them.

I'm hoping you understand the difference between the two types of mindsets. Keep this core
philosophy in mind as we move forward: "Code _can_ fail".

## Consistent and stable runtime

In a world with many different browsers and various versions of those browsers
it seems like we do not have consistent or stable runtimes.  When it comes to
Internet Explorer stability and consistency really do seem to be lacking.
Please do not stop here though. Just because one browser is not completely
reliable does not mean we do not have a consistent and stable runtime.

Thinking of desktop development, below is what I've seen as an example "support matrix".

| Browser | Versions |
| ------- | -------- |
| Chrome  | Current  |
| Firefox | Current  |
| IE      | 8+       |
| Safari  | Current  |

The parallel I draw to Ruby or Python here is when they are ran on different
operating systems or interpreters. For the most part we do not have worry about
the differences between operating systems. This is largely due to successful
abstractions in the languages. I believe JavaScript has this same capability
when paired with libraries. For instance you may use [jQuery][jquery-url]
for a lot of your JavaScript code. This abstraction helps you achieve a consistent
and stable environment.

## Manageable testing

Nearly every language or framework comes with some decent work flows for testing.
Usually all code that can be tested then gets tested.  For
instance if you have an ATM application where a person deposits money
or withdraws money, you would test all parts of this work flow.

For some reason when it comes to the browser many developers think it's okay
to leave work flows untested that are impacted by JavaScript. Worse, because
these work flows are often not tested changes may cause defects in the
application later. Still growing negative, when JavaScript encounters errors it often
results in the application not working.

It may sound like testing is hopeless in JavaScript. That is not the case
there are plenty of ways to test JavaScript.  In fact here are a list of
frameworks that can help you out with testing (and a [comparison][js-testing-comparison-url]):

* [Jasmine][jasmine-url]
* [Mocha][mocha-url]
* [QUnit][qunit-js]

With many tools available there is no excuse for not testing every part
of an application that has end user impact. All of your JavaScript should
be tested.  _If it's not tested it shouldn't exist_.

Some will say that with closures (since JavaScript is heavily functional) that
testing is really hard.  Just because something is hard does not give
you freedom to ignore it. Further, if the code is designed well testing
usually isn't an issue. A good sign of "code smell" is not being able to more
easily create tests. This statement holds true to me for _all_ code, not just JavaScript.

## Error handling

Performance seems to be the first thing many people bring up when it comes to JavaScript
error handling. I do not buy into this philosophy. Feel free to take a read of this
[programmer thread][javascript-error-performance] about the perceived issue. The real
problem is if you're using error handling as control flow. Don't do that, you wouldn't
do it on the server so don't do it in JavaScript. Exception cases are exceptional, therefore,
they should not happen often. This means you need not worry about the performance impact
because the errors are rare.

One point where people seem to think error handling doesn't work in JavaScipt is in a
`setTimeout` call. For example if you have this:

```js
try {
  setTimeout(function(){
    c = a + b;
  }, 100)
} catch (e) {
  alert("This will not be hit, ever!");
}
```

In Chrome you'll see this error with the above code:

> Uncaught ReferenceError: a is not defined

You may wonder why the error isn't caught. I invite you to watch this [great video][eventloop-explanation-url]
about the event loop in JavaScript. Basically this is how JavaScript works.  When
code is sent to the event loop it is removed from the scope of this try catch. The
code is made asynchronous by the `setTimeout` call. Therefore the `try/catch` no longer
works because `try/catch` was a synchronous call.

There is actually a pretty easy way to handle this type of asynchronous call.
Wrap the function passed to `setTimeout` in a try catch and you'll be good. For example:

```js
var realFunction = function () {
  c = a + b;
}

var handleErrors = function (func) {
  try {
    func.apply(arguments);
  } catch (e) {
    alert("This line is hit, mischief managed!");
  }
}

setTimeout(handleErrors(realFunction), 100);
```

I recommend this practice to anyone who wants to catch and handle errors.
This gets back to a point before around hard-to-write tests. Error
handling should also be as easy as it is in other languages.
If the code is hard to handle, odds are it needs some refactoring. The code
above can be used in a generic sort of wrapper to catch
errors. Keep a look out, in the near feature I plan to help release a library
to make this kind of error catching much easier. In fact, that same library
plays a part in the next section of this post.

## Built in logging

In most every language logging is built in. You make a call similar to:

```py
try:
  # something that breaks but is specific
except Exception as e:
  logger.error('Some specific message');
```

In JavaScript you do have access to `console.log` and the related levels of
logging. If you are sitting there thinking that's grossly inadequate compared
to the power of server side logging, you are correct. Currently JavaScript
lacks the ability to make it easy to aggregate logs.

Don't throw `console.log` and friends out. They are very useful and give you the same power as other
languages built in logging. The real issue is the lack of seeing all the logs
across all of your users. When you have a 500 on your website you can see
the number of times it occurs, who it impacts, and usually trace it to the
line of code that caused the issue. This can all be done in production.

When it comes to getting a JavaScript error, a single log doesn't really help you.
The average user is not going to know how to get you the local client side
logs. Further, most users won't even realize what has gone wrong. A good
number of users will usually refresh the page and hope for the best, or worse
they will abandon their current pursuit and stop using the site.

Remember that library I mentioned above? The one that I plan to open source
soon? Well, that library will make it very easy to get these JavaScript errors
into one location for you to look at any time you want. The beauty of the library
is how easy it is to track the errors.

I'll finish by showing all that's needed to catch all errors for a function
that is used often.

```js
var myUsedOftenFunction = function () {};

LIBRARY.watch(myUsedOftenFunction);
```

That's all you need. From then on if that function throws an error, _in any browser_,
you'll know about it.

## Summary

When you develop code your mindset matters most. If you approach a problem
assuming your tools won't work, then you won't solve the problem, and your
tools won't work. JavaScript is a powerful language that has many feature.
Take advantage of these features and do not cripple yourself living in the
world of "code _will_ fail".

Remember "code _can_ fail" and you have a massive tool belt to handle these
code failures. Embrace the power of JavaScript. Treat it like you do any other
programming language. You only need to give JavaScript a chance. It can be one
of your biggest assets when it comes to web development.

[jquery-url]: https://jquery.com/
[d3-url]: http://d3js.org/
[r2d2-url]: https://github.com/mhemesath/r2d3/
[js-testing-comparison-url]: https://coderwall.com/p/ntbixw/javascript-test-framework-comparison
[jasmine-url]: http://jasmine.github.io/
[mocha-url]: http://mochajs.org/
[qunit-js]: http://qunitjs.com/
[javascript-error-performance]: http://programmers.stackexchange.com/questions/144326/try-catch-in-javascript-isnt-it-a-good-practice
[eventloop-explanation-url]: https://vimeo.com/96425312
