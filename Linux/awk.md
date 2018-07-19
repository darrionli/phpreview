**awk**是一种编程语言，用于在linux/unix下对文本和数据进行处理 ，功能非常强大，详细介绍：http://man.linuxde.net/awk

`awk`通常会配合`wc`，`uniq`，`gerp`，`sort`来进行服务器日志分析。

### 总结一下日志分析用的常用命令：

1. 查看日志数据有多少行

   ```shell
   wc -l access_log
   ```

2. 查看有多少个ip访问

   ```shell
   awk '{print $1}' access_log | sort | uniq | wc -l
   ```

3. 查看某一个页面被访问的次数

   ```shell
   grep '/index.php' access_log | wc -l
   ```

4. 查看访问前10的ip地址

   ```shell
   awk '{print $1}' access_log | sort | uniq -u | sort -nr | head -10
   ```

5. 查看某一个ip访问了哪些页面

   ```shell
   grep ^111.197.23.215 access_log | awk '{print $1 $7}'
   ```

6. 统计5分钟内，apache访问最多的url和对应的ip地址

7. 显示指定时间以后的日志

   ```shell
   awk '$4>"[15/Jun/2018:00:00:00]" {print $0}' access_log
   ```

   

   

#### 另外，管道符 `|` 在分析命令中也很常见

```shell
command 1 | command 2
```

以上命令表示把第一个命令command1执行的结果作为command2的输入传给command2命令

