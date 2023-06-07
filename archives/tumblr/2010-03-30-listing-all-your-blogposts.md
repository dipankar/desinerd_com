---
layout: post
title: Listing all your blogposts
date: '2010-03-30T15:35:19+05:30'
tags:
- blog
- blogosphere
- list
- python
- tinyurl
- wordpress
- wordpresslib
tumblr_url: http://www.desinerd.com/post/150535101953/listing-all-your-blogposts
---
So here is a quick snapshot at how to get all your wordpress blogposts using python [or wordpresslib to be specific]

–
#!/usr/bin/env python
import wordpresslib
import tinyurl
wordpress = raw_input(''Wordpress URL:'')
user = raw_input(''Username:'')
password = raw_input(''Password:'')
# prepare client object
wp = wordpresslib.WordPressClient(wordpress, user, password)
# select blog id
wp.selectBlog(0)
posts = wp.getRecentPosts(100)
for p in posts:
if p.title.find("p=")<0:
    print p.title," - ",tinyurl.create_one(p.link)
–
Now that is real easy to use IMHO, i just started using this in one of my scripts. It is easy to use this and plug into other systems which use python !
Resources:
http://code.google.com/p/wordpress-library/
http://pypi.python.org/pypi/TinyUrl/0.1.0
