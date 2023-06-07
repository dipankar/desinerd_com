---
layout: post
title: Cron issues on drupal
date: '2010-03-31T18:06:54+05:30'
tags:
- cron
- cron_last
- cron_semaphore
- drupal
- issues
- php.ini
- php5
- semaphore
tumblr_url: http://www.desinerd.com/post/150535102098/cron-issues-on-drupal
---
Well here are some quick ways of solving your “cron not working properly issues in drupal”

It has a semaphore which blocks the cron running, in my case the PHP script ran for too long and ate up too much memory. I needed to modify my php.ini to ensure that it could take up more memory.

Another issue was that you needed to delete a certain variable in the Drupal database, use the following for a quick resolution to the problem.

DELETE FROM `variable` WHERE name = ‘cron_semaphore’;

DELETE FROM `variable` WHERE name = ''cron_last’;

Another way is to install the devel module and delete the above variables from the database using the UI.

Hope this helps.
