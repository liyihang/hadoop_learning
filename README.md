# CentOS修改系统语言

## CentOS7版本的系统语言修改

#### 1.切换到root用户
```
su 
```
#### 2.找到locale.conf 文件
```
cd /etc/
or
find -name locale.conf
```

#### 3.打开locale.conf 文件
```
vi locale.cnf 
#内容如下
LANG = "en_US.UTF-8"
LANG = "zh_CN.UTF-8"
```
#### 4.保存`wq`,退出，重启系统。
到此CentOS更高中文系统就完成了。
