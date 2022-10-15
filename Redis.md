# CentOS 7 安装Nginx以及使用



### 安装

这里采用源码安装

一、获取源码并解压

```shell
wget https://download.redis.io/releases/redis-6.2.6.tar.gz
tar -zxvf redis-6.2.6.tar.gz
```

二、编译安装

```shell
make && make install
```



### 配置

一、开机自启

```shell
#将配置文件复制重命名到、etc/redis目录下
cp /home/redis-6.2.6/redis.conf /etc/redis/6379.conf
#将redis初始化脚本复制到/etc/init.d目录下
cp /home/redis-6.2.6/utils/redis_init_script /etc/init.d/redis
#在此目录下启动 etc/init.d/
chkconfig redis on		//启动
```

二、允许远程服务器访问

修改配置文件redis.conf
bind 127.0.0.1 更改为- > bind 0.0.0.0 

三、后台启动

修改配置文件redis.conf

daemonize no 更改为- > daemonize yes

