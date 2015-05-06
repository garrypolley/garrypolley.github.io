---
layout: post
title: 'Github: issue pull request to existing issue'
date: '2013-01-03T08:52:53-06:00'
tags: []
tumblr_url: http://blog.garrypolley.com/post/39567226444/github-issue-pull-request-to-existing-issue
---
I was always wondering how to issue a pull request on an issue that already existed on Github…  Now I know how. Thanks to this link: http://stackoverflow.com/questions/4528869/how-do-you-attach-a-new-pull-request-to-an-existing-issue-on-github
Basically all I needed to do was:

```sh
install hub
brew install hub
```

issue request to existing issue (must be inside git repo)

```sh
hub pull-request URL_TO_ISSUE
```

Now your request is made
