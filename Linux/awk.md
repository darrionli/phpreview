**awk**是一种编程语言，用于在linux/unix下对文本和数据进行处理 ，功能非常强大。

学习地址：http://man.linuxde.net/awk

常见用法：

1. 请统计5分钟内，nginx访问最多的url和对应的ip地址

2. 查看访问前10的ip

   ```shell
   awk '{print $1}' | sort | uniq -c | sort -nr | head -10 access_log
   ```

3. 访问次数最多的前10个文件或者页面

   ```shell
   cat access_log|awk '{print $11}'|sort|uniq -c|sort -nr | head -10
   ```

   

