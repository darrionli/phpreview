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

