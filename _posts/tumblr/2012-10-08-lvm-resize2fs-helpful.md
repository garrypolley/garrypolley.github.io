---
layout: post
title: LVM + resize2fs == Helpful
date: '2012-10-08T14:52:38-05:00'
tags: []
tumblr_url: http://blog.garrypolley.com/post/33178399312/lvm-resize2fs-helpful
---
Problem:

I need more space on a disk partition (/opt)

Solution:

Use lvm and resize2fs to give more space to /opt

How to do:

LVM is a logical volume manager.  I was able to use to add free disk space to an existing linux box's /opt folder so I could get mongo up and running in a sane configuration.

Here's what I did:

> df -ah
...
/dev/mapper/vg00-opt
                       4.1G  1.1G   3 25% /opt
...


That told me I only had 4.1 G usable on the /opt partition.  For mongo this is a no go.  Next I needed to see how much free space I had left on the box:

>vgdisplay
  --- Volume group ---
...
  Free  PE / Size       20000/ 20000
..


Seeing that I had a ton of free space I then added 15G to my /opt partition

> lvresize -L +100%FREE /dev/mapper/vg00-opt


Now that it was added, I needed the file system to see it as well.

> resize2fs /dev/mapper/vg00-opt


Boom, now I have increased my partition size.

> df -ah
...
/dev/mapper/vg00-opt
                       26G  4.5G   20G  19% /opt
...
