---
layout: post
title: 'Midewest.io: quality over quantity'
---

If you've not heard about it there is a great conference here in Kansas City
called [Midwest.io][midwest-io]. I spent November 9th and 10th getting to
hear a lot of really great talks and chatting with a lot of smart people.
I recommend you come every year after this one, it's that good. The talks
range from low level technical details, such as using
[Software Transactional Memory][software-transactional-memory], all the way
to improving yourself as a developer using the [Talmud][talmud].

My notes for each of the talks I attended are below. There is a link to each
of the talks below the heading. The notes will be fairly short, you should
watch the talks. My notes are only here to give you an idea of what I took
away from each talk. Maybe they'll help you maybe they won't.

(As videos come out I will update links to point to videos)


# Day One - November 9th

## Leagues of Sea and Sky

[Talk Link](https://youtu.be/6Go1H026Knc)

### Cool Bits

* Used augmented reality via the projector which
led to some really cool ways of conveying information
* Charles Lindberg did not give credit to his manufacturers
* Government funded prizes for innovation are interesting forms of motivation and corruption

### Take Aways

* Partnership is not about credit
* Partnership should help and/or strengthen both parties
* Try to make partnerships, working solo is usually not best


## A Gentle Guide to Genetic Algorithms

[Talk Link](https://www.youtube.com/watch?v=h_jsjPyNu9o)

### Cool Bits

* These are still fun
* Fitness algorithm is key

### Take Aways

* Genetic algorithm could be good to use when trying maximize a choice
* Your heuristics matter a lot when defining your algorithm
* If what your trying to find is a sequence it could be good, (think survival of the fittest)


## A Brief History of (Logical) Time

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwfd/)

### Cool Bits

* The idea of using logical counts for a clock is cool
* [Version Vectors](https://en.wikipedia.org/wiki/Version_vector)
* Look at [Bloom](http://bloom-lang.net/) language
* Look at [Lasp](http://lasp-lang.org/) language

### Take Aways

* Using normal timestamps in  conjunction with logical clocks can help a lot


## How to Write a Worthwhile Test

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwfm/)

### Cool Bits

* Look into using [given, when, then](http://martinfowler.com/bliki/GivenWhenThen.html)
* Specifically look at [mocha-given](https://github.com/rendro/mocha-given)
* Concepts of false negatives and true negatives.  False: you had to fix the test _only_ when a test
failed. True: your code was actually broken when the test fails.

### Take Aways

* Write small testable chunks of code
* Consistency is most important
* Don't strive for small tests, strive for readable tests
* Always add good useful messages (assertion libraries can help here)
* Look at how assertions work in testing libraries, not just the syntax of it, but the messages that come out
* Measure false negatives to see where tests are getting too out of hand


## Achievement Unlocked: A Better Path to Language Learning

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwfp/)

### Cool Bits

* Interesting idea about using pet project to learn a new programming language
* [MAL](https://github.com/kanaka/mal/blob/master/process/guide.md) -- Make A Lisp

### Take Aways

* When learning a new language try to build something real, you already know


## Measuring the Performance of Single Page Web Applications

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwft/)

### Cool Bits

* There is a [NavigationTiming API](https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API)
* [Boomerang](http://yahoo.github.io/boomerang/doc/) exists for measuring performance of frontend
* Concept of hard (refresh, first landing) vs soft (after single page loads) navigation
* Can use [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) to get
a feel for what's happening

### Take Aways

* Use [Boomerang](http://yahoo.github.io/boomerang/doc/)
* onLoad is no longer reliable for single page application "first load time"


## You May Not be a Polyglot, but Your Software Needs to Be

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwfw/)

### Cool Bits

* i18n + l10n == g10n
* Trip Advisor does a great job globalizing content
* There are differences in meanings of words between Spanish speaking countries (e.g. not a word, but in one means naked)

### Take Aways

* Always write code assuming globalization
* Know where you need to support (languages like Arabic are really hard, don't invest time if you never need it)
* Culture matters when choosing colors or phrases for branding
* Need to have localization experts look over all content, not just words


# Day Two - November 10th


## Reliable Concurrency Without the Actor Model

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwfz/)

### Cool Bits

* [Software Transactional Memory][software-transactional-memory]
* [Actor model](https://en.wikipedia.org/wiki/Actor_model) may not work well if you want real concurrency

### Take Aways

* [STM][software-transactional-memory] kind of allows for concurrent access, it rolls back and retries the one out of sync
* A log to keep track of what has occurred is interesting
* The model for [STM][software-transactional-memory] could be applied to a distributed system


## Chaos Engineering

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwgb/)

### Cool Bits

* An interesting way to describe a supply chain via the [Beer Game](https://en.wikipedia.org/wiki/Beer_distribution_game)
* [Chaos Monkey](https://github.com/Netflix/SimianArmy/wiki/Chaos-Monkey)
* [Chaos Kong](http://techblog.netflix.com/2015/09/chaos-engineering-upgraded.html)
* [Principles of Chaos](http://www.principlesofchaos.org/)
* [Intuition Engineering](http://techblog.netflix.com/2015/10/flux-new-approach-to-system-intuition.html)

### Take Aways

* Do not assume what a talk is about based on title
* Works well for decentralized development teams
* Must always look at entire system, not individual parts
* Data visualizations of the "health" of a system can be very useful see [Intuition Engineering](http://techblog.netflix.com/2015/10/flux-new-approach-to-system-intuition.html)


## Securing Your Company's Data: Encryption, Deleting and Other Best Practices

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwgd/)

### Cool Bits

* Found out about an [OPM data breach](https://en.wikipedia.org/wiki/Office_of_Personnel_Management_data_breach)

### Take Aways

* Secure data at rest
* Only gather data you _need_


## Sparkling Pandas

[Talk Link](http://www.midwest.io/sessions/#tuesday-4b)

### Cool Bits

* Seem to be three contenders for data science: [Pandas](http://pandas.pydata.org/),
[Ibis](http://www.ibis-project.org/), and [PySpark](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)
* [Impala](http://impala.io/) can make using Hadoop easier

### Take Aways

* [Sparkling Pandas](http://sparklingpandas.com/) replaces PySpark
* Running Python code while running the JVM is not very great for performance


## Writing Custom In-browser Tools for Smarter WebApp Development

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwgm/)

### Cool Bits

* Debug tools can be built into an application, hadn't thought about this before
* [Browser Tool Template](https://github.com/lshearer/browser-tools-template)

### Take Aways

* Building a custom Chrome Dev Tool isn't so bad, could let you make tools that give you application specific info


## Telling Stories with Data Visualization

[Talk Link](http://lanyrd.com/2015/midwestio/sdqwgp/)

### Cool Bits

* I still like D3
* Your visualization choice _always_ adds a bias, which isn't necessarily bad, but it is a bias
* Take a look at [Edward Tufte](http://www.edwardtufte.com/tufte/)

### Take Aways

* Visualizations tell stories, always start with the story
* Flow of visualization creation: story -> visualization
* User's point of view is paramount to telling the right story, and then choosing the right visualization


## Talmudic Maxims to Maximize Your Growth as a Developer

[Talk Link](https://www.youtube.com/watch?v=U5D_Nczx-io)

**Watch this talk**! It had some of the best content at the conference. Great job [@coderabbi](https://twitter.com/coderabbi)

### Cool Bits

* [@coderabbi](https://twitter.com/coderabbi)
* People are generally willing to be helpful
* I learned about [Talmud][talmud]

### Take Aways

* In software people are most important (users, developers, et al)
* Don't side project alone, find a buddy
* Seek out ways to help others
* **_Always_** be coding
* Consistency is key to growth (if you don't always do something - at least a little - how does it get better?)
* Avoid fear of: failure, growth, questions, looking dumb
* Beginning something is often the hardest part


[midwest-io]: http://www.midwest.io/
[software-transactional-memory]: https://en.wikipedia.org/wiki/Software_transactional_memory
[talmud]: https://en.wikipedia.org/wiki/Talmud
