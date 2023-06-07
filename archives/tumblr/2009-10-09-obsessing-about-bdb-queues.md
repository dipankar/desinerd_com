---
layout: post
title: obsessing about bdb, queues
date: '2009-10-09T02:33:31+05:30'
tags:
- archive
- django
- internet
- lookup
- python
- queue
- rails
- sets
tumblr_url: http://www.desinerd.com/post/150535101478/obsessing-about-bdb-queues
---
So my nightmares do no cease to end, still debating queue solutions and databases. After spending a lot of time thinking about how to handle 100 million entries , concurrency and a lot of jazz here are some conclusions that I have reached.
Tokyo Tyrant needs some testing personally. Can it work well within a constrained VPS ? I doubt that after reading all the test results. So need to do a benchmark for this.
Tornado , the friendfeed (facebook) non-blocking server looks cool. The primary issues are the lack of an plugin architecture much like django or rails, guess that is something i can give back to them (if and when i start working on it). 
Python set lookups are blazing fast, in a benchmark today it beat lists lookup (800000 entries) by 10 times

Feeling much better after the flu, I hope to write more often so that the ether (ie the internet) can crawl and archive my existence ;).
