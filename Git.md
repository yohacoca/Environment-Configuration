# CentOS 7 安装Git以及使用



### 安装

这里采用源码安装

一、首先获取源码压缩包，然后进行解压

```shell
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.21.0.tar.gz
tar -zxvf git-2.21.0.tar.gz
```

二、安装之前需要手动下载依赖

```shell
sudo yum install -y wget
sudo yum install -y gcc-c++
sudo yum install -y zlib-devel perl-ExtUtils-MakeMaker
```

三、进行安装配置 （这里指定安装路径）

```shell
./configure --prefix=/usr/local
```

四、编译以及安装

```shell
make && make install
```



### 配置

一、先进行全局配置，设置用户和邮箱

```shell
git config --global --list	#查看全局配置

git config --global user.name "Your Name"
git config --global user.name "Your email"

```

二、如果要关联远程仓库，就需要设置ssh公钥，否则每次都要输入密码

```shell
ssh-keygen -t rsa -C "youremail@example.com"	#点击四下回车，生成公钥私钥文件
cat .ssh/id_rsa.pub 	#获取生成的公钥，添加到git上
```

三、仓库设置

```shell
git init	#初始化仓库
```

