---
layout: post
title: 'Java: Mac OSX JAVA_HOME'
date: '2012-07-02T16:29:37-05:00'
tags: []
tumblr_url: http://blog.garrypolley.com/post/26371440062/java-mac-osx-java-home
---
I'm still getting everything setup for development on my new retina display mac book pro, which is awesome, and I encountered an issue.  I've not really done java dev on a mac, mostly linux or windows.   Apparently the JAVA_HOME that you get for free on linux is not used on the mac.  You'll need to add JAVA_HOME to your .bash_profile, or equivalent depending on your terminal choice.

Upon google searching I was lead to this email archive that gave me the solution: http://lists.apple.com/archives/java-dev/2011/Jul/msg00172.html.

I need to add this to my .bash_profile for it to work:

`export JAVA_HOME=/usr/libexec/java_home`
