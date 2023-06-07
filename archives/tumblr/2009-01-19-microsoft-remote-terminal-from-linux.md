---
layout: post
title: Microsoft remote terminal from linux
date: '2009-01-19T19:30:15+05:30'
tags:
- debian
- distro
- linux
- rdesktop
- ubuntu
- windows
tumblr_url: http://www.desinerd.com/post/150535099298/microsoft-remote-terminal-from-linux
---
I know it would be simple for a lot of people reading this blog :). But the easiest way to remote desktop into a windows machine using a X based linux distro is to install rdesktop.

http://www.rdesktop.org

For ubuntu and debian based distro, fire up the console and type

sudo apt-get install rdesktop

This would install the client.

rdesktop <server IP/domain> 

This would fire up the windows remote desktop stuff.
