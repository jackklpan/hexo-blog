---
title: Running a Reverse Proxy in Apache
tags: []
date: 2015-01-22 19:11:00
---

ps -ef | grep apache 
/usr/sbin/apache2 -V | grep SERVER_CONFIG_FILE 

 sudo a2enmod mod_proxy 
sudo a2enmod proxy_http 

 In apache config file: 
ProxyPass       /app1/  http://internal1.example.com/ 
ProxyPassReverse /app1/ http://internal1.example.com/ 

service apache2 restart