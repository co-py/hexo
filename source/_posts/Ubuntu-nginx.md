---
title: Ubuntu的常用命令（三）nginx设置
date: 2017-11-23 23:30:51
tags: linux
---

## remove apache
```bash
sudo service apache2 stop
sudo apt-get remove apache2
```

## install nginx
```bash
sudo apt-get install nginx
cd /etc/nginx/conf.d
vi api.chaoshuai.com-3000.conf
```
## edit xxx.conf
```bash
upstream my_server {                                                         
    server 127.0.0.1:3000;
}
server {
    listen       80;                                                         
    server_name  api.chaoshuai.org; 

    location / {
        proxy_pass http://my_server/;
		proxy_redirect off;
        proxy_set_header Host $host:$server_port;
		# 后端的Web服务器可以通过X-Forwarded-For获取用户真实IP
        proxy_set_header  Host  $host;
		proxy_set_header  X-Nginx-Proxy true;
        proxy_set_header  X-Real-IP  $remote_addr;  
        proxy_set_header  X-Forwarded-For  $proxy_add_x_forwarded_for;
        # proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
    }

    location ~* ^.+\.(gif|jpg|jpeg|bmp|png|ico|txt|js|css)  
	{    
		root /www/my_server/production/current/public;
	}
}

```
## join *conf
```bash
cd /etc/nginx
sudo nano nginx.conf
# include /etc/nginx/conf.d/*.conf; 
```
## test nginx flies
```bash
sudo nginx -t
# nginx: configuration file /etc/nginx/nginx.conf test is successful

```
## nginx reload
```bash
sudo nginx -s reload 
```
