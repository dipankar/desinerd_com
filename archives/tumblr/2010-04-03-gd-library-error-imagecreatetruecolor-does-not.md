---
layout: post
title: 'GD Library Error: Imagecreatetruecolor Does Not Exist'
date: '2010-04-03T01:39:48+05:30'
tags:
- error
- gd
- Imagecreatetruecolor
- library
- php5
- wordpress
tumblr_url: http://www.desinerd.com/post/150535102168/gd-library-error-imagecreatetruecolor-does-not
---
Well the simplest way of solving this is to run

sudo apt-get install php5-gd 

That will install the necessary libraries that you need to keep continuing. If you are in windows then you need to go  to your php.ini and uncomment the following lines

;extension=php_gd.dll
;extension=php_gd2.dll

[just remove the ; to uncomment them]

Hope that solves your image issues.
