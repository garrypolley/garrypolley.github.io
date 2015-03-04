---
layout: post
title: Django + Heroku + Django-Pipeline = Happy Statics
date: '2012-10-18T07:01:00-05:00'
tags: []
tumblr_url: http://blog.garrypolley.com/post/33832191154/django-heroku-django-pipeline-happy-statics
---
I’ve been working on a site over the last few months called linkminded: http://linkminded.co. We hope to go live soon, however, one of the many hurdles we’ve had to work through has been static content delivery.
Django
We chose to use the Django development platform for our web framework. The platform is awesome and I highly recommend it. Django takes care of a lot of stuff. However by itself it does not handel static deployments easily.
Heroku
We have chosen Heroku as our server host. They are a great company that makes it super easy to do deployments, (git push heroku master). Although Heroku is great, it appeared to lack some needed functionality, server side core librareis. Enter Heroku buildpacks, awesome packages that work kind of like AWS AMIs. We chose to use this build pack (git://github.com/jiaaro/heroku-buildpack-django.git ) because it allows us to use Node and NPM.
Django-Pipeline
Static content is one piece of web architecture and Django Pipeline makes it easy. Using django-pipline, in combination with less, we have easily managed static content. Pipeline does not deploy static content to a static content server however. It helps to combine your many JS, CSS, and LESS files together, based on configuration, so that deployments can be more easily managed. While keeping development simple.
Happy Static
Using Django, Heroku, and django-pipeline we’ve achieved simple and repeatable static content development. With an explanation of each piece out of the way, we can now get into how we did this.
Setup your project with django-pipeline:
The first step here is to make sure you have a Django application that actually needs to be deployed. I have a sample app for this blog post here: https://github.com/garrypolley/django-heroku-static-example. It is already setup and ready to go. Look at the bottom of the settings.py file to see the djanog-pipeline settings that are needed.  You’ll also need to make sure you use {% compressed_css ‘PIPELINE_KEY’ %} and {% compressed_js ‘PIPLINE_KEY’ %} in your templates.  Look at the templates in the example app for pointers and see how they relate to the django-pipeline config.
settings.py:
Next create a Heroku app
You will need to setup a Heroku app now. Here are the command I’ve used to setup our Heroku application:
<![CDATA[// <![CDATA[
// <![CDATA[
// <![CDATA[
// <![CDATA[
// <![CDATA[
// <![CDATA[
// <![CDATA[
// <![CDATA[
// <![CDATA[
// <![CDATA[
/script>
<h2>Getting the static to work
<p>Now that you have your Heroku app, you can get it up and running by adding the Heroku git url endpoint. &ldquo;git remote add heroku git@youre_heroku_app.git&rdquo;. Next you&rsquo;ll need to make sure you have a Procfile to ensure your app runs collect static on the remote end, our&rsquo;s looks like this:
<script src="https://gist.github.com/3911284.js" type="text/javascript">
// ]]]]]]]]]]]]]]]]]]]]]]><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]]]]]]]]]]]]]]]><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]]]]]]]]]]]]]><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]]]]]]]]]]]><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]]]]]]]]]><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]]]]]]]><![CDATA[><![CDATA[><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]]]]]><![CDATA[><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]]]><![CDATA[><![CDATA[><![CDATA[>
// ]]]]]]><![CDATA[><![CDATA[>
// ]]]]><![CDATA[>]]>You will also need to make sure you have lessc installed. This is able to happen easily because of the build pack we are using. Make sure you have an npm_requirements.txt next to your standard requirements.txt. Ours looks like this:
Make sure you’ve committed all this code to master. Next do a “git push heroku master” now your app should be deployed with statics working, (note this is form the dev server right now, you’ll want to update this to use a real CDN. Future blog post to come: Heroku + Django + AWS CDN
TL;DR
Example version here: http://dhs.garrypolley.com/
Use this build pack: git://github.com/jiaaro/heroku-buildpack-django.git
Use a Procfile
Have an npm_requirements.txt
Have pipeline settings
Use {% compressed_css ‘PIPELINE_KEY’ %} stuff in your templates
Define the compresor on the server to use node and lessc (see above)
Pay attention to requirements.txt (yuicompressor) and .gitignore
Had issues with our procfile for this example I just did:

web: python manage.py collectstatic —noinput; python manage.py runserver 0.0.0.0:$PORT
