---
slug: "django-optimizations-within-the-platform"
title: 'Django : Optimizations within the platform'
date: "2008-11-18"
tags: ['database', 'django', 'fast', 'optimization', 'platform', 'smtp', 'super']
---
In my experience with both rails and django, i would have to admit that a lot of things need to be improved at the core of these platforms so that developers can truly deploy a really fast production site. Let talk about what we did at kwippy to make it that much more faster than the default Django setup.
Use memcached properly : The trick in getting speed is to cache all logged out pages and heavy caching of the user objects when logged in. For example we recently got our sessions into the memcached cloud to see a good speed jump.
	Database structuring : Django does a lot  of joins and magic in it ORM, and has a built in caching layer. But the problem is that we developers structure our tables to our percieved needs … not necessarily for the way the ORM works. One way is to start writing custom SQL inside your views, another is to understand the ORM better. Your choice :).
	Database connection pooling : It is pretty shocking to realize that Django does not do connection pooling, I have used DButils connection pooling for our needs. But IMHO it should be a default thing inside the application platform.
	SMTP is slow : Imagine the user filling up a form which is emailed to you, and your SMTP is down. There is a good chance that you will lose that data and the application will give a 500 :). To alleviate that i have created a command queue where emails are not sent within the application and a daemon is doing all the dirty work. I will put it all out in the market :), so that you guys can make you site that much more faster/robust.
	Pagination  : To be honest, i still do not like django pagination. The problem was that it will getting all the objects and as the database is on a separate machine a lot of data was being transferred over the network. So i created my custom pagination which was faster than ObjectPaginator or Paginator.

Well there are all i could think of right now. Obviously there are some other optimizations that i keep doing …. and will keep writing about. Till the next time, feel free to contact me about these optimizations at me@dipankar.name.
