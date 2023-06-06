---
slug: "installing-huginn-on-ubuntu-20-04"
title: "Installing huginn on ubuntu 20.04"
date: "2021-01-03"
tags: ['Articles', 'Technical', 'huginn', 'ruby', 'runit', 'ubuntu']
---

The default [guide](https://github.com/huginn/huginn/blob/master/doc/manual/installation.md) for Huginn installation works pretty well. The only part where you do get stuck is

sudo bundle exec rake production:export
So what really happens is that the console looks like it stuck, which is quite frustrating. Lets say you force quit this (Crtl^C). Try running it again and you will get an error like.

{{< highlight bash >}}

root@localhost:/home/huginn/huginn# sudo bundle exec rake production:export --trace
** Invoke production:export (first_time)
** Invoke production:check (first_time)
** Execute production:check
** Execute production:export
** Execute production:stop
Stopping huginn ...
rake aborted!
'sv stop huginn-web-1' exited with a non-zero return value: warning: huginn-web-1: unable to open supervise/ok: file does not exist
/home/huginn/huginn/lib/tasks/production.rake:85:in `run'
/home/huginn/huginn/lib/tasks/production.rake:77:in `block (2 levels) in run_sv'
/home/huginn/huginn/lib/tasks/production.rake:93:in `call'
/home/huginn/huginn/lib/tasks/production.rake:93:in `with_retries'
/home/huginn/huginn/lib/tasks/production.rake:76:in `block in run_sv'
/home/huginn/huginn/lib/tasks/production.rake:75:in `each'
/home/huginn/huginn/lib/tasks/production.rake:75:in `run_sv'

{{< / highlight >}}

So a bit of searching will lead you to this bug [report](https://github.com/huginn/huginn/issues/1352), which actually is pretty confusing. Turns out the issue is with runit.

The solution provided by [somm15](https://github.com/somm15) for ubuntu 18.04 works as well for Ubuntu 20.04 as well.

{{< highlight bash >}}

sudo apt-get install runit-systemd runit-helper
sudo systemctl enable runit
sudo systemctl status runit
{{< / highlight >}}

Now you can rerun the init script exporting and you can continue with the installation guide!