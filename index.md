---
layout: post
title: 'Garry Polley'
hide_footer: 'true'
---

I'm a developer that loves making development easier. Currently, I focus
on web development. I work client side with JavaScript, though I'm not a fan.
I prefer to skip the middle layer and go to the
back end of a website. Be-it a database or a deployment that niche
is what I like to fill. I can do Rails and Django development -- preferring Django.

These days I'm also working in Go, which is like a statically typed Python for me.

You'll likely see a mix of content on this website, mostly related via blog posts.
I generally focus on technical posts but every once
in awhile I may deviate from my technical nature. Sometimes I'll post a "micro" blog,
those are mostly notes for myself to remember how to do something.

Thanks for stopping by and feel free to reach out if you need help with
anything!

{% for post in site.posts limit: 5 %}
<hr />
    {% include inline_post.html post=post %}
{% endfor %}

<hr />
<footer>
Unless otherwise state all content is released under the Creative Commons 4.0 license.
<dl>
  <dt>License</dt><dd><a href="http://creativecommons.org/licenses/by/4.0/">Creative Commons 4.0</a></dd>
</dl>
</footer>
