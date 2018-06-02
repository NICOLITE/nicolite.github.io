---
title: Ubuntu Server 16.04 配置nginx + php7.0 + mysql + wordpress
date: 2017-03-14  09:11:34
categories:
- Linux
tags: 
---
#### 安装nginx（采用自己编译安装）
##### 安装gcc g++编译依赖库
<pre class="prettyprint linenums">sudo apt-get install build-essential
sudo apt-get install libtool
</pre>
##### 安装 pcre依赖库
<pre class="prettyprint linenums">sudo apt-get update
sudo apt-get install libpcre3 libpcre3-dev
</pre>
##### 安装 ssl依赖库
<pre class="prettyprint linenums">
sudo apt-get install openssl
</pre>
##### 安装 zlib依赖库
<pre class="prettyprint linenums">
 sudo apt-get install zlib1g-dev
</pre>
##### 编译安装nginx

参考<a href="http://www.cnblogs.com/piscesLoveCc/p/5794926.html">Ubuntu16.04安装nginx</a>
<pre class="prettyprint linenums">#下载nginx，这里使用最新稳定版，该版本支持安全狗：
wget http://wget http://nginx.org/download/nginx-1.10.3.tar.gz
#解压：
tar -zxvf nginx-1.10.3.tar.gz
#进入解压目录：
cd nginx-1.10.3
#配置：
./configure --prefix=/usr/local/nginx 
#编辑nginx：
make
注意：这里可能会报错，提示“pcre.h No such file or directory”,具体详见：http://stackoverflow.com/questions/22555561/error-building-fatal-error-pcre-h-no-such-file-or-directory
需要安装 libpcre3-dev,命令为：sudo apt-get install libpcre3-dev
#安装nginx：
sudo make install
#启动nginx：
sudo /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
注意：-c 指定配置文件的路径，不加的话，nginx会自动加载默认路径的配置文件，可以通过 -h查看帮助命令。
#查看nginx进程：
ps -ef|grep nginx
</pre>

##### nginx常用命令</h3>
<pre class="prettyprint linenums">#启动nginx
sudo /usr/local/nginx/sbin/nginx
#t停止nginx
sudo /usr/local/nginx/sbin/nginx -s stop 或者 sudo /usr/local/nginx/sbin/nginx -s quit
#重新加载配置
 sudo /usr/local/nginx/sbin/nginx -s reload
#指定配置文件
 sudo /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
#检查配置文件语法是否正确
 sudo /usr/local/nginx/sbin/nginx -t
#查看nginx版本
 sudo /usr/local/nginx/sbin/nginx -v
</pre>

#### 安装php
由于php不像nginx那样容易编译成功，所以采用apt安装，你也可以自己编译安装，ubuntu16.04仓库中的php更新到7.0版本了
<pre class="prettyprint linenums" >
#更新软件源
sudo apt-get update
#安装php7.0
sudo apt-get install php
#安装mbstring
sudo apt-get install php7.0-mbstring
</pre>

#### 安装mysql
<pre class="prettyprint linenums" >
sudo apt-get install mysql-server mysql-client
安装的过程会要你输入数据库root用户密码,千万要记住，不然又要一大堆麻烦了
</pre>
##### mysql基本命令
更多请百度
<pre class="prettyprint linenums" >
#登录到mysql
mysql -uroot -p
输入密码
#查看有哪些数据库
show databases;
#选中某个数据库
use 数据库名称
#查看数据库中的表格
show tables
#查询数据库
select * from 表名
#新建编码为utf8的数据库
create database 数据库名 default set utf8 aollate utf8_general_ci;
#删除数据库
drop database 数据库名
</pre>

#### 配置nginx</h2>

<pre class="prettyprint linenums" >
cd /usr/local/nginx/conf/
sudo vim nginx.conf

#将文件内容修改为下面这样
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    gzip  on;
    gzip_min_length 1k;
    gzip_buffers 4 16k;
    gzip_comp_level 6;
    gzip_types text/plain application/x-javascript text/css application/xml text/javascript application/x-httpd-php application/json image/jpeg image/gif image/png;
    gzip_vary off;
    gzip_disable "MSIE[1-6]\.";
    
    server {
        listen       80;
        server_name  localhost;
        #设置编码
        charset utf-8;
        #隐藏nginx版本信息
        server_tokens off;
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm index.php;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #

       #开启php文件支持
        location ~ \.php$ {
            root           html;
            #fastcgi_pass   127.0.0.1:9000;
            fastcgi_pass   unix:/run/php/php7.0-fpm.sock;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  /usr/local/nginx/html$fastcgi_script_name;
            include        fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
            deny  all;
        }
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
    #包含所有的虚拟主机配置文件
    include /usr/local/nginx/vhosts/*;
}
</pre>

#### 配置php7.0
像上面那样配置完是没有权限正常访问php7.0-fpm的，还需要指定用户和用户组
<pre class="prettyprint linenums" >
cd /etc/php/7.0/fpm/pool.d
sudo vim www.conf

#找到这个
; Set permissions for unix socket, if one is used. In Linux, read/write
; permissions must be set in order to allow connections from a web server. Many
; BSD-derived systems allow connections regardless of permissions.
; Default Values: user and group are set as the running user
;                 mode is set to 0660
listen.owner = nobody  #这里修改为这样
listen.group = nobody
</pre>

<h2>安装wordpress</h2>
<pre class="prettyprint linenums" >
#下载最新版
wget https://cn.wordpress.org/wordpress-4.7.4-zh_CN.zip
#解压
wget -zxvf wordpress-4.7.4-zh_CN.zip
#将wordpress中的内容复制到nginx网络目录
cd wordpress
sudo cp -r  *  /usr/local/nginx/html/
#给worpress添加权限（不然worpress无法进行删除或者是安装插件这些操作）
cd /usr/local/nginx/html
sudo chown -R www-data:www-data *
</pre>

#### 配置wordpress
在浏览器上输入你服务器绑定的域名按步骤配置就可以了