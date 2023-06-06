---
slug: "rhel5-yum-to-munin"
title: 'RHEL5 : Yum to munin'
date: "2010-03-18"
tags: ['installation', 'monit', 'munin', 'munin-node', 'repo', 'rhel', 'rhel5', 'yum']
---
So here are some dead easy ways of getting munin and munin-node installed on your RHEL5 server.

First add RPM Forge repository rpm -Uhv http://apt.sw.be/redhat/el5/en/i386/rpmforge/RPMS/rpmforge-release-0.3.6-1.el5.rf.i386.rpm

Then just fire

yum install munin munin-node

Now, you have your munin running. Lets turn our attention to monit.

First add this new repo to you rpm -Uvh http://download.fedora.redhat.com/pub/epel/5/i386/epel-release-5-3.noarch.rpm

Then go ahead and install monit using yum install monit

Now this my friend was real easy ! Have fun , more later.
