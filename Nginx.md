# CentOS 7 安装Nginx以及使用

### 安装

这里采用源码安装

一、获取压缩包，然后解压

```shell
wget https://nginx.org/download/nginx-1.21.2.tar.gz
tar -xvf nginx-1.13.7.tar.gz
```

二、安装所需要的依赖

```
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
```

三、进行安装配置（添加ssl模块）

```
./configure --with-http_stub_status_module --with-http_ssl_module
```

四、编译以及安装

```
make && install
```



### 配置

一、配置文件

安装路径在 /usr/local/nginx

配置文件目录 /usr/local/nginx/conf/nginx.conf

启动文件目录 /usr/local/nginx/sbin/nginx

二、启动

查看运行状态

```shell
ps -el | grep nginx
```

首先指定配置文件

```shell
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

启动

```shell
/usr/local/nginx/sbin/nginx -s reload
```
