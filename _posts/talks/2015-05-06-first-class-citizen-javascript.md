---
layout: post
title: 'First Class Citizen: JavaScript'
---

Think of the last time you were given a project or a new website to build.
You probably did not think very hard about the language you would code the
site in. You likely thought more about how complex the site would be and
what server side framework you would use to create the site.

Let's say you worked through the feature list and landed on using Rails or
Django as your server side web framework. Here are a few assumptions you likely made
by choosing to have Python or Ruby as your core language:

* Consistent and stable runtime
* Manageable testing
* Built in logging
* Error handling

Why bring up these pretty standard features that exist is nearly every modern
language? Because, most people seem to think JavaScript either does
not have these features or they choose not use these features. In either case
I'll cover why JavaScript has all of these features and why we should rely on
them instead of living in fear of them. I also plan to dispel what I believe
is a commonly believed myth: "Your JavaScript **_will_** fail."

In fact, let's start with what drives your thoughts when it comes to
your core language assumptions.

## Why does your mindset matter?

If you live by the thought: "My JavaScript _will_ fail" then it will fail.
Think about it. If you wrote server side code under the assumption it **_will_**
fail, you likely do not have confidence in your application. Further if you lived
under this thought you would probably not use the language or framework causing
this much doubt in your applications. Do not misunderstand
my point here. I am _not_ saying that JavaScript **_can't_** fail. I am saying that
your mindset should be: "My JavaScript _can_ fail".

With the mind set of: "Code _can_ fail" you will approach problems differently.
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
bunch of different layers. Just have a simple one time fall back like a table.

The difference between _will_ fail and _can_ fail here, is that a _will_ fail
mindset would likely try to build many layers of fall back (e.g. canvas, divs). This leads to more
complicated code as well as less reliable code. A _can_ fail mindset builds for the
common successful case and _reasonably_ handles failure. We need to handle errors on the client the same as we do
the server. It's not okay to gobble up errors and move on. Later we'll see how you can
gracefully handle errors and report on them.

I'm hoping you see the difference between the two types of mindsets. Keep this core
philosophy in mind as we move forward: "Code _can_ fail".

## Consistent and stable runtime

In a world were we have many different browsers and various versions of those browsers
it does seem like we do not have consistent or stable runtimes.  When it comes to
Internet Explorer stability and consistency really do seem to be lacking.
Please do not stop here though. Just because one browser is not completely
reliable does not mean we do not have a consistent and stable runtime.

Thinking of desktop, below is what I've seen as an example "support matrix".

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
when paired with the libraries. For instance you may use [jQuery][jquery-url]
for a lot of your JavaScript code. This abstraction helps you achieve a consistent
and stable environment.


[jquery-url]: https://jquery.com/
[d3-url]: http://d3js.org/
[r2d2-url]: https://github.com/mhemesath/r2d3/
