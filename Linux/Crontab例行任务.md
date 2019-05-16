##Crontab命令释义：

`crontab`命令常见于`Unix`和类`Unix`的操作系统之中，用于设置周期性被执行的指令。该命令从标准输入设备读取指令，并将其存放于`crontab`文件中，以供之后读取和执行。该词来源于希腊语 chronos(χρνο)，原意是时间。常，`crontab`储存的指令被守护进程激活， `crond`常常在后台运行，每一分钟检查是否有预定的作业需要执行。这类作业一般称为`cron jobs`。
基本格式 :
如何查看  ```crontab ```
```
 Linux centos  yum  install crontab 

*　　*　　*　　*　　*　　command
分　时　日　月　周　命令
第1列表示分钟1～59 每分钟用*或者 */1表示
第2列表示小时1～23（0表示0点）
第3列表示日期1～31
第4列表示月份1～12
第5列标识号星期0～6（0表示星期天）
第6列要运行的命令
```
`crontab`文件的一些例子：


```
30 21 * * * /usr/local/etc/httpd restart
```
上面的例子表示每晚的21:30重启`apache`。
```
45 4 1,10,22 * * /usr/local/etc/httpd restart
```
上面的例子表示每月1、10、22日的4 : 45重启`apache`。
```
10 1 * * 6,0 /usr/local/etc/httpd restart
```
上面的例子表示每周六、周日的1 : 10重启`apache`。
```
0,30 18-23 * * * /usr/local/etc/httpd restart
```
上面的例子表示在每天18 : 00至23 : 00之间每隔30分钟重启`apache`。
```
0 23 * * 6 /usr/local/etc/httpd restart
```
上面的例子表示每星期六的11 : 00 pm重启`apache`。
```
* */1 * * * /usr/local/etc/httpd restart
```
每一小时重启`apache`
```
* 23-7/1 * * * /usr/local/etc/httpd restart
```
晚上11点到早上7点之间，每隔一小时重启`apache`
```
0 11 4 * mon-wed /usr/local/etc/httpd restart
```
每月的4号与每周一到周三的11点重启`apache`
```
0 4 1 jan * /usr/local/etc/httpd restart
```
一月一号的4点重启`apache`

基于`crontab`的数据库备份（*****）
1.	找到服务器下找一个地方存放备份数据。
```
Home  df  查看磁盘空间
```

在`home`目录下创建`sqlbackup`。
2.	创建备份文件
3.	在`sqlbackup`目录下创建自动备份的脚本
4.	书写sh命令并赋予执行权限`chmod u+x filename`
```
#!/bin/bash
mysqldump -uroot -ppassword myblog > /home/sqlbackup/myblog_$(date +%Y%m%d_%H%M%S).sql
```
5.`crontab –e` 添加计划任务
```
0 2 * * * /home/sqlbackup/myblog.sh
```

6.重启`crontab：service crond restart`（重启不重启都可以）
7.查看定时任务日志：`tail -f /var/log/cron`
