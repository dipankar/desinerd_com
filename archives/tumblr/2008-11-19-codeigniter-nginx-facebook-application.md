---
layout: post
title: 'CodeIgniter + nginx : Facebook application'
date: '2008-11-19T10:27:24+05:30'
tags:
- ci
- code
- codeigniter
- facebook
- igniter
- nginx
- run
tumblr_url: http://www.desinerd.com/post/150535098693/codeigniter-nginx-facebook-application
---
This is a basic tutorial on how to get CodeIgniter facebook application on nginx (with the gotchas). The nginx configuration would be like the following


server {
        listen 80;
        server_name blah.com;
        location ~ /index.php/ {
                root           /home/production/blah;
                index  index.html index.htm index.php;
                include        conf/fcgi.conf;
                fastcgi_param  SCRIPT_FILENAME /home/production/fb_apps/quickdate/index.php;
                fastcgi_pass   127.0.0.1:9000;
        }
        access_log      /usr/local/nginx/logs/blah.access_log;
        error_log       /usr/local/nginx/logs/blah.error_log;
    }


The critical line is the fastcgi_params parameter, that changes the whole game. In the code Igniter application you need to add the following file in [app]/system/application/libraries/FB_controller.php


facebook = new Facebook($this->API_KEY, $secret);
                $this->uid = $this->facebook->require_login();
        }
}
?>



There are some significant changes in the configuration which is at [app]/system/application/config/config.php


$config[''enable_query_strings''] = TRUE;
$config[''subclass_prefix''] = ''FB_'';
$config[''uri_protocol''] = "REQUEST_URI";


Now in the application you should write controllers extending the above defined class , for example I modified the welcome controller.


facebook->api_client->Users_isAppUser()) {
                                $this->facebook->redirect($this->facebook->get_add_url());
                                return;
                        }
                }
                catch (Exception $x) {
                        // Clear cookies for your application and redirect them to a login prompt
                        $this->facebook->expire_session();
                        $facebook->redirect($this->facebook->get_login_url());
                }
        }
        function index() {
        }
}


Fire this up and see it all running smoothly, this is basically compiled from all kinds of forum over the internet. Thought it will be useful for someone. In case of any issues contact me at me@dipankar.name.
