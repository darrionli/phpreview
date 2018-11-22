#### Nginx安装

1. 下载地址：http://nginx.org/en/download.html

2. 编译安装

   ```shell
   # tar zxvf nginx-1.14.0.tar.gz
   # cd nginx-1.14.0
   # ./configure --prefix=/usr/local/nginx
   ```

   Nginx依赖于pcre库，需要先安装pcre

   ```shell
   # yum pcre pcre-devel
   ```

3. 启动


   sbin下二进制程序其启动

   ```shell
   # cd /usr/local/nginx/sbin
   # ./nginx
   ```

4. 关闭Nginx

   netstat -antp  查看当前进程

   ```shell
   # kill -INT 2389   // 2389是nginx的进程号
   ```

   改变配置文件后，平滑优雅的重启Nginx ：   `kill -HUB 2389`

   或者：

   重启：`nginx -s reload`

   关闭：`nginx -s stop`

#### Nginx配置

1. 虚拟主机：域名、端口、IP

2. 日志

   ```shell
   #access_log  logs/host.access.log  main;
   说明该server的访问日志是logs/host.access.log，日志格式是main
   ```

3. 日志定时切割

4. location精准匹配

#### Nginx优化

1. gzip压缩和Expres设置

2. 反向代理（动静分离）

   proxy_pass

3. 负载均衡

   upstream

   反向代理会导致服务器只能获取到代理服务器的ip

#### 整合PHP

nginx和apache下，php的运行模式有所不同，apache下是以模块的方式运行，nginx是以fastcgi的形式，就是说nginx遇到php文件统一交给php进程来处理，管理这个php fastcgi进程的就是php-fpm，因此两种服务器下的编译方式略微不同

```shell
./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-apxs2=/usr/local/apache2/bin/apxs --with-mysql=/usr/local/mysql --with-libxml-dir=/usr/local/libxml2 --with-png-dir=/usr/local/libpng --with-jpeg-dir=/usr/local/jpeg9 --with-freetype-dir=/usr/local/freetype --with-gd=/usr/local/gd2 --with-zlib-dir=/usr/local/zlib --with-mcrypt=/usr/local/libmcrypt --with-xpm-dir=/usr/lib64/ --enable-soap --enable-mbstring=all --enable-sockets --enable-fpm
```

编译时需要带  --enable-fpm 参数即可开启php-fpm。

编译完成之后，需要创建一下php-fpm.conf文件和www.conf文件，都在php/etc目录下。然后启动php-fpm，在9000端口运行。

配置nginx

```shell
# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000  
#  
location ~ \.php$ {  
root html;  
fastcgi_pass 127.0.0.1:9000;  
fastcgi_index index.php;  
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;  
include fastcgi_params;  
}
```

