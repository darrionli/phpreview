**crontab命令** 被用来提交和管理用户的需要周期性执行的任务 ，此服务默认安装

linux下的任务调度分为两类：**系统任务调度** 和 **用户任务调度**

### 系统任务调度

系统周期性所要执行的工作，比如写缓存数据到硬盘、日志清理等。在`/etc`目录下有一个`crontab`文件，这个就是系统任务调度的配置文件，这个文件只能由系统管理员来修改。

看一下`/etc/crontab`文件内容：

```shell
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed

a、每一行定义一个周期性任务，共7个字段。
b、此处的环境变量不同于用户登录后获得的环境，因此建议命令使用绝对路径。
c、执行结果会发送邮件给mailto指定的用户。
```

字段解释：

- minute： 表示分钟，可以是从0到59之间的任何整数。

- hour：表示小时，可以是从0到23之间的任何整数。
- day：表示日期，可以是从1到31之间的任何整数。
- month：表示月份，可以是从1到12之间的任何整数。
- week：表示星期几，可以是从0到7之间的任何整数，这里的0或7代表星期日。
- command：要执行的命令，可以是系统命令，也可以是自己编写的脚本文件

在以上各个字段中，还可以使用以下特殊字符：

- 星号（*）：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。
- 逗号（,）：可以用逗号隔开的值指定一个列表范围，例如，“1,2,5,7,8,9”
- 中杠（-）：可以用整数之间的中杠表示一个整数范围，例如“2-6”表示“2,3,4,5,6”
- 正斜线（/）：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次。同时正斜线可以和星号一起使用，例如*/10，如果用在minute字段，表示每十分钟执行一次。

#### crond命令

```shell
crontab [-u user] [-l | -r | -e] [-i]

-l：列出当前用户的计划任务。
-e：编辑当前用户的计划任务。
-r：删除当前用户的所有计划任务。即删除/var/spool/cron/USERNAME文件。
-u：管理指定用户的计划任务，仅root有权限。
-i：在使用-r选项删除所有任务时提示用户确认。
```

#### crond服务

```shell
/sbin/service crond start    //启动服务
/sbin/service crond stop     //关闭服务
/sbin/service crond restart  //重启服务
/sbin/service crond reload   //重新载入配置
```

查看crontab状态：

```shell
service crond status
```

手动启动crontab服务 :

```shell
service crond start
```

查看crontab服务是否已设置为开机启动，执行命令： 

```shell
ntsysv
```

加入开机自动启动： 

```shell
chkconfig –level 35 crond on
```

查看所有用户的crontab

```shell
for u in `cat /etc/passwd | cut -d":" -f1`;do crontab -l -u $u;done  
```

查看cron的日志 

```shell
tail -50f /var/log/cron 
```



### 用户任务调度

用户定期要执行的工作，比如用户数据备份、定时邮件提醒等。用户可以使用 crontab 工具来定制自己的计划任务。所有用户定义的crontab文件都被保存在`/var/spool/cron`目录中 。

```shell
/var/spool/cron  // 目录下面是每个用户自己通过 crontab -e 增加的crontab的内容。
/var/spool/anacron  // 目录下面是记录的是cron.daily,cron.monthly,cron.weekly上一次执行的时间。
```



注意：

**crontab的最小时间单位为”分钟“**，想完成”秒“级任务，得需要借助于其它方式。 先定义为每分钟任务,再利用脚本实现在每分钟之内，循环执行多次。 

