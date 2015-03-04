---
layout: post
title: DNSimple wins again
date: '2012-06-14T00:12:38-05:00'
tags: []
tumblr_url: http://blog.garrypolley.com/post/25075239230/dnsimple-wins-again
---
I used to do some work for http://www.videomarketingusa.com/ and I learned a fair amount about SEO.  The easiest thing I learned that helps a site is making sure your www.mysite.come poitns to mysite.com, or vice-versa.  I was having some difficulty doing this with using hostmonster because I prefer the http://mysite.com over http://www.mysite.comwww.mysite.come poitns to mysite.com, or vice-versa.  I was having some difficulty doing this with using hostmonster because I prefer the http://mysite.com over http://www.mysite.com, less typing.  
Because of this I switched to DNSimple.  I googled around for how to get heroku to re-direct http://www to http://.  I saw some complex stuff about doing middleware and updating some specific config on your box… that seemed like over kill, so I just took a peek at the many options DNSimple gives you for domain setups, WIN.  I found one called URL, guess what?  It does exactly what I wanted:  http://www.garrypolley.com now points to http://garrypolley.com. 

tl;dr
Use the URL option on DNSimple to make a 301 redirect from http://www.mysite.com to http://mysite.com
