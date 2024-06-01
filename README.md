1.Student

811010001111   123456

![image](https://github.com/ILoveCAmille/client/assets/93418879/0ccf6151-b677-4229-b481-e37b1902581b)

2.admin

java1234  123456

![image](https://github.com/ILoveCAmille/client/assets/93418879/6326bc5b-c363-4d17-8b6e-2d300c2905e2)



3.teacher

11010003  123456

![image](https://github.com/ILoveCAmille/client/assets/93418879/c0ba255c-57e6-4d22-b0f0-2bf97bd062db)


4.后端


![image](https://github.com/ILoveCAmille/client/assets/93418879/751c36fc-981e-486d-92d9-8d3aa0692263)


5.前端
![image](https://github.com/ILoveCAmille/client/assets/93418879/185d3e67-cd5c-4042-9f27-8868f99dc6e3)

6.nginx配置
user  www www;
worker_processes auto;
error_log  /www/wwwlogs/nginx_error.log  crit;
pid        /www/server/nginx/logs/nginx.pid;
worker_rlimit_nofile 51200;

stream {
    log_format tcp_format '$time_local|$remote_addr|$protocol|$status|$bytes_sent|$bytes_received|$session_time|$upstream_addr|$upstream_bytes_sent|$upstream_bytes_received|$upstream_connect_time';
  
    access_log /www/wwwlogs/tcp-access.log tcp_format;
    error_log /www/wwwlogs/tcp-error.log;
    include /www/server/panel/vhost/nginx/tcp/*.conf;
}

events
    {
        use epoll;
        worker_connections 51200;
        multi_accept on;
    }

http
    {
        include       mime.types;
		#include luawaf.conf;

		include proxy.conf;
        lua_package_path "/www/server/nginx/lib/lua/?.lua;;";

        default_type  application/octet-stream;

        server_names_hash_bucket_size 512;
        client_header_buffer_size 32k;
        large_client_header_buffers 4 32k;
        client_max_body_size 50m;

        sendfile   on;
        tcp_nopush on;

        keepalive_timeout 60;

        tcp_nodelay on;

        fastcgi_connect_timeout 300;
        fastcgi_send_timeout 300;
        fastcgi_read_timeout 300;
        fastcgi_buffer_size 64k;
        fastcgi_buffers 4 64k;
        fastcgi_busy_buffers_size 128k;
        fastcgi_temp_file_write_size 256k;
		fastcgi_intercept_errors on;

        gzip on;
        gzip_min_length  1k;
        gzip_buffers     4 16k;
        gzip_http_version 1.1;
        gzip_comp_level 2;
        gzip_types     text/plain application/javascript application/x-javascript text/javascript text/css application/xml application/json image/jpeg image/gif image/png font/ttf font/otf image/svg+xml application/xml+rss text/x-js;
        gzip_vary on;
        gzip_proxied   expired no-cache no-store private auth;
        gzip_disable   "MSIE [1-6]\.";

        limit_conn_zone $binary_remote_addr zone=perip:10m;
		limit_conn_zone $server_name zone=perserver:10m;

        server_tokens off;
        access_log off;




        server {
             listen  6543;
             server_name  101.37.118.201;
             gzip  on;
             gzip_types text/plain application/x-javascript application/javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;

             location  /{
                    root    /www/wwwroot/two/dist;
                    index    index.html   index.htm;
                    try_files  $uri  $uri/   /index.html;
            }
                location /api {
                        proxy_pass http://101.37.118.201:8088/;
                        proxy_set_header   Host $host:$server_port;
                        proxy_set_header   X-Real-IP $remote_addr;
                        proxy_set_header   X-Forwarded-Host $host;
                        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
                }

         }

server
    {
        listen 888;
        server_name 101.37.118.201;
        index index.html index.htm index.php;
        root  /www/server/phpmyadmin;

        #error_page   404   /404.html;
        include enable-php.conf;

        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
        {
            expires      30d;
        }

        location ~ .*\.(js|css)?$
        {
            expires      12h;
        }

        location ~ /\.
        {
            deny all;
        }

        access_log  /www/wwwlogs/access.log;
    }
include /www/server/panel/vhost/nginx/*.conf;
}







