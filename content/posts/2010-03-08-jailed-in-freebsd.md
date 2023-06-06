---
slug: "jailed-in-freebsd"
title: Jailed in FreeBSD
date: "2010-03-08"
tags: ['freebsd', 'install', 'jail', 'linux', 'nginx', 'portsnap', 'python']
---
Well, working on freeBSD right now some immediate learnings for most linux users
Ports is as good as apt-get [and i would say much better, when i started installing stuff]
	You will need to start with installing vim and bash to make your life a lot easier

So the target was to install python and nginx, both of which are very easy to install once you understand how the whole ports collection system works. So here is the guide to installing nginx

portsnap fetch - This gets the portsnap collection file

portsnap update - This updates the collection directory at /usr/ports

Then goto /usr/ports/www/nginx and use make, it throws up a very nice module selection menu which i really like. I do wish that apt-get was like this when it came to installing stuff like this. The final step is a make install Simple is it not.

Python is very similar when you want to install as well ! More as i finish my installation and tweaking, having some issues with nginx latency !
