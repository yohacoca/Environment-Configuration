# CentOS 7 安装MySql以及使用

### 安装

Centos已经不支持mysql，因为收费了你懂得，所以内部集成了mariadb，安装会自动覆盖

一、获取MySQL官方的  Yum Repository

```shell
wget http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
```

二、安装

```shell
yum -y install mysql57-community-release-el7-10.noarch.rpm
```

三、安装mysql服务器，会覆盖之前的mariadb

```shell
yum -y install mysql-community-server
```



### 配置

一、启动MySql

```
systemctl start  mysqld.service
```

二、查看MySql运行状态

```
systemctl status mysqld.service
```

三、进入MySQL，进入之前要找到生成的root密码

```shell
grep "password" /var/log/mysqld.log
```

四、进入数据库、输入刚才的密码

```sql
mysql -u root -p
```

五、第一次进去需要修改默认密码。注意:密码设置必须要大小写字母数字和特殊符号

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
```

六、开启远程访问（注意：下面命令开启的IP是 192.168.0.1，如要开启所有的，用%代替IP）

```sql
grant all privileges on *.* to 'root'@'192.168.0.1' identified by 'password' with grant option;
#例
grant all privileges on *.* to 'root'@'%' identified by 'password' with grant option;
```

七、刷新系统权限相关表

```sql
flush privileges;
```

八、退出

```sql
exit;
```

