---
slug: "php-nice-urls-nginx"
title: PHP + nice URLS + nginx
date: "2008-12-26"
tags: ['drupal', 'fastcgi', 'htaccess', 'joomla', 'nginx', 'php', 'urls', 'wordpress']
---
Easiest way to get php with good looking urls running on your site . Works for drupal, wordpress and joomla.

server {
listen 80;
server_name www.domain.com;
index  index.html index.htm index.php;
root   /path/to/domain/files;
location / {
error_page 404 = //e/index.php?q=$uri;
}
location ~ .php$ {
include        fastcgi_params;
fastcgi_pass   127.0.0.1:9000;
fastcgi_index  index.php;
fastcgi_param  SCRIPT_FILENAME /path/to/domain/files$fastcgi_script_name;
}
access_log      /usr/local/nginx/logs/domain.access_log;
error_log       /usr/local/nginx/logs/domain.error_log;
}
