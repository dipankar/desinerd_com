---
layout: post
title: Support and PHP
date: '2010-08-02T12:27:42+05:30'
tags:
- gd
- jpeg
- otrs
- perl
- php
- support
tumblr_url: http://www.desinerd.com/post/150535102323/support-and-php
---
So got to setting up OTRS, neat email based support system and it works pretty well it seems. There are some issues setting it up initially, but it integrates very well into your support email ! Should have thought of using it for kwippy once i think about it he he.

Just managed to get PHP compiled from source with php-fpm patch on it, the configure string was as follows

./configure –enable-fastcgi –enable-fpm –with-mcrypt –with-zlib –enable-mbstring –disable-pdo –with-pgsql –with-curl –disable-debug –with-pic –disable-rpath –enable-inline-optimization –with-bz2 –with-libxml-dir –with-zlib –enable-sockets –enable-sysvsem –enable-sysvshm –enable-pcntl –enable-mbregex –with-mhash –with-xsl –enable-zip –with-pcre-regex –with-mysql –with-gd –with-mysqli –with-jpeg-dir –with-freetype-dir –with-png-dir –with-pdflib

Though on debian getting GD with JPEG requires the open jpeg library [not the other jpeg lib]. Thats after going through the compilation a couple of time !

Also planning to move my server to a better setup, running out of memory right now.
