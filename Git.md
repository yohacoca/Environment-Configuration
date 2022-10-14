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

三、仓库基础设置

```shell
#git使用步骤	添加文件进入暂存区，然后提交到本地仓库，最后推送到远程仓库

# 仓库初始化git选择默认的是main主分支，这里初始化的时候建议加上主分支名字
git init -b <branch-name>

#关联远程仓库
git remote add origin git@server-name:path/repo-name.git

#添加文件进入暂存区
git add "Your Filename"

#提交文件进入本地仓库
git commit -m "message"

#推送到远程仓库
git push origin "branch-name"

#克隆远程仓库
git clone git@server-name:path/repo-name.git


#重新更名分支
git branch -m <oldbranch> <newbranch>
#例如
git branch -m main master

#取消远程仓库关联
git branch --unset-upstream 
```



### 常用命令

```shell
#安装git后
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

#创建ssh key，用于和github通信 (秘钥存储于C:\Users\27634\.ssh，把公钥id_rsa.pub存储于github)
ssh-keygen -t rsa -C "youremail@example.com"

#创建版本库
#把这个目录变成Git可以管理的仓库(后续新建提交和ssh克隆需要)	
git init -b <branch-name>

#操作版本库
# 文件名 添加文件(新增或者更改都需要先add)
git add
# 提交到本地版本库
git commit -m "message"
# 查看仓库状态
git status
#文件名 查看修改的地方
git diff

#版本回退(从一个commit恢复)
#查看版本历史
git log
#回退到上个版本
git reset --hard HEAD^ 
# 回退到特定版本号(commit以后回退)
git reset --hard 1094a
#记录每一次命令
git reflog
#直接丢弃工作区的修改(add以前回退)
git checkout -- file
#添加到了暂存区时，想丢弃修改(add以后回退)
git reset HEAD <file>

#删除文件
#(已经add/commit,在目录中删除)
git rm file

#删错了回退
git checkout -- file 

#远程仓库
#关联远程库
git remote add origin git@server-name:path/repo-name.git 
#第一次的push
git push -u origin master
#常用的push，本地分支会在服务器上新建分支
git push origin master
#需要有关联的分支，第一次下拉最好新建一个空文件夹
git pull
#
git branch --set-upstream-to=origin/远程分支 本地分支 关联分支
#克隆(不需要另建文件夹)
git clone git@server-name:path/repo-name.git 

#分支
#查看所有分支
git branch -a
#查看分支关联
git branch -vv
#创建分支
git branch dev
#切换分支
git checkout dev
#合并某分支到当前分支
git merge dev
#普通模式合并，合并后的历史有分支
git merge --no-ff -m "msg" dev
#删除分支
git branch -d dev
#创建并切换分支
git checkout -b dev


#合并分支,无法merge
#名字 暂存工作状态
git stash save
#拉下来
git pull origin dev 
#查看已经暂存的状态
git stash list
#将暂存状态merge到当前分支 还有冲突时,手动修改文件,然后add/commit
git stash pop stash@{0}
# 分支合并图
git log --graph

#bug分支issue
#暂存工作状态
git stash
#查看暂存工作状态
git stash list
#恢复暂存状态并删除状态
git stash pop


#开发分支feature
#强制删除未合并的分支
git branch -D <name> 


#rebase
#本地未push的分叉提交历史整理成直线
git rebase 


#标签
#标签名 打在最新提交的commit上
git tag
#查询所有标签
git tag
#标签名 f52c633 给特定的commit打标签
git tag
#commit的id 给标签设置说明
git tag -a 标签名 -m "msg" 
#标签名 查询标签内容
git show 
#标签名 删除标签
git tag -d
#标签名 推送某个标签到远程
git push origin
#推送所有标签
git push origin --tags 
#可以删除一个远程标签
git push origin :refs/tags/<tagname>

```

