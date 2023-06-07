---
layout: post
title: Python, Passenger phusion and dreamhost
date: '2012-01-22T17:57:09+05:30'
tags:
- dreamhost
- paste
- python
- wsgi
tumblr_url: http://www.desinerd.com/post/150535102668/python-passenger-phusion-and-dreamhost
---
Well, had to setup some stuff on dreamhost. Turns out that they are fairly bad on django hosting. Here is a working passenger_wsgi.py that is possibly much better than the default. Please not that you must have paste [http://pythonpaste.org/]  installed for this to work correctly.

This has python2.7 locally installed in your account, with all the libraries locally. Dreamhost is quite painful, as the documentation is incomplete clearly!

