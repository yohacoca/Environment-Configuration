### 安装

这里是源码安装

一、获取源码以及解压

```shell
wget http://am1.php.net/distributions/php-7.3.2.tar.gz
tar -zxvf php-7.3.2.tar.gz
```

二、安装php依赖

```shell
yum install -y libxml2-devel sqlite-devel libcurl-devel oniguruma-devel libpng-devel libjpeg-devel freetype-devel libzip-devel openssl-devel
```

三、编译参数参考

```shell
./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-mhash --with-openssl --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-iconv --with-zlib --enable-inline-optimization --disable-debug --disable-rpath --enable-shared --enable-bcmath --enable-shmop --enable-sysvsem --enable-gd --with-jpeg --with-freetype --enable-mbregex --enable-mbstring --enable-ftp --enable-pcntl --enable-sockets --enable-soap --without-pear --with-gettext --enable-session --with-curl  --enable-opcache --enable-fpm --with-fpm-user=php --with-fpm-group=php --without-gdbm --enable-fast-install --disable-fileinfo
```

四、编译以及安装

```shell
make && make install
```



### 配置php-fpm

一、复制启动脚本到安装目录

启动脚本位置：安装包/sapi/fpm/init.d.php-fpm

```shell
#当前目录 安装包/sapi/fpm/init.d.php-fpm
cp init.d.php-fpm /usr/local/php/
```

二、复制配置文件到安装目录

配置文件：安装包/sapi/fpm/init.d.php-fpm

```shell
#当前目录 安装包
cp php.ini-production /usr/local/php/etc/php.ini
```

三、创建php-fpm进程服务的配置文件

进入安装目录下的etc 

```shell
#当前目录 安装目录/etc/
cp php-fpm.conf.default php-fpm.conf
```

四、配置php-fpm的进程服务的扩展配置

```shell
#当前目录	安装目录/etc/php-fpm.d/
cp www.conf.default www.conf
```

五、添加用户用于允许php-fpm进程

```shell
useradd php -s /sbin/nologin
```

六、启动

```shell
bash init.d.php-fpm start
```

