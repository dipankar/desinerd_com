---
layout: post
title: Nginx + django fcgi lessons
date: '2009-01-19T19:37:55+05:30'
tags:
- application
- client
- django
- imaging
- kwippy
- library
- memory
- nginx
- optimization
- pil
- python
- timeout
tumblr_url: http://www.desinerd.com/post/150535099398/nginx-django-fcgi-lessons
---
Today was a good day as i learned some valuable lessons about django and nginx.
ALWAYS close the database cursor in django, it can lead to some pretty wierd memory issues going forward.
	FIND the most optimal number of database connections you initialize for you connection pooling. This will let you optimize on memory going forward.
	ENSURE that you do not set a very high client_timeout, this means that if connections are not explicitly not closed by the client then the web server will not timeout. This results in bad memory behavior for the fcgi threads.

Well, this has solved my major issues with respect to kwippy. Also learned that GIFs are very fundamentally different than JPEGs which results in a lot of problem when used in the python imaging library. All in all a good day :D.
