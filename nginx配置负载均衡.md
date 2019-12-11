# [nginx配置负载均衡](https://www.jianshu.com/p/34af13579c75)  
  1. 下载nginx依赖库  
```javascript
yum install gcc-c++ -y  
yum install pcre pcre-devel -y  
yum install zlib zlib-devel -y  
yum install openssl openssl--devel -y  
```
  2. 安装nginx  
  首先进入/usr/local目录  
  `cd /usr/local`  
  从官网下载nginx  
  `wget http://nginx.org/download/nginx-1.7.4.tar.gz`  
  查看  
  `ls`  
  解压nginx  
  `tar -zxvf nginx-1.7.4.tar.gz`  
  会产生一个nginx-1.7.4目录，进入该目录  
  `cd nginx-1.7.4`  
  接下来依次执行  
  `./configure`    
  `make`  
  `make insatll`  
  如果没有报错，完成后，看nginx安装目录  
  `whereis nginx`  
  3. 负载均衡配置
  
  - nginx配置
  ```java
    cd /usr/local/nginx/conf

    vim nginx.conf
  ```
  ```java
     #这里的域名要和下面proxy_pass的一样
     upstream mengma.com {
        server   192.168.0.100:8878 weight=1;
        server   192.168.0.101:8878 weight=2;
     }
     
     server {
        listen   80;
        server_name   192.168.0.100;
     }
     
     location / {
        proxy_pass http://mengma.com;
        index  index.html  index.htm;
     }
  ```
