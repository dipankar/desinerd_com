---
layout: post
title: Multiple views using bottle.py
date: '2012-09-02T18:00:24+05:30'
tags:
- boilerplate
- bootstrap
- bottle
- bottle.py
- HTML5
- mako
- memcached
- project structure
- python
- redis
tumblr_url: http://www.desinerd.com/post/150535102893/multiple-views-using-bottlepy
---
I have been using the micro-framework called bottle.py, and starting to write fairly complicated applications on top of it. So I have been able to put together a relatively clean structure based that serves my maintainability issues

This setup uses redis, memcached, and mako as the templating language. Lets assume the application name is project.

project/project/main.py - This is the core application file that loads up bottle and the pluginsproject/INSTALL - This is the readme and simple installation instructionsproject/middlewares.py - This is the middlewares that you maybe using in your bottle.py applicationproject/views.py - This contains all the views that you will create, you can also split it further based on your application object typesproject/utils.py - This is the utility libraryproject/static_views.py - This is a temporary view for serving the static assets of your application in the development. This should never be used in the production setup and be replaced with either a CDN or Nginx or varnish or apache to serve them directly.project/templates/ - This is the mako templates directoryproject/static/ - This is the static file directory

This is a very manageable structure that has evolved over time and works pretty well for me to start off new project pretty easily. In the next article, I will publish an actual mini application with the additional features like HTML5 boilerplate integration in addition to a core bootstrap for the templating structure as well.
