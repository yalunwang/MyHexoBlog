---
title: centos搭建git服务器
date: 2017-02-10 14:04:41
tags: hexo
---
## 安装git,并创建一个git用户

```
# yum install -y git
# adduser git 
# git --version
```
 <!--more -->
## 初始化仓库
- 随便选择一个目录gittest作为仓库地址

```
root@aliyun:/mnt# mkdir gittest
root@aliyun:/mnt# cd gittest
root@aliyun:/mnt/gittest#  mkdir mygitrepo.git
root@aliyun:/mnt/gittest# cd mygitrepo.git
```
- 初始化仓库

```
root@aliyun:/mnt/gittest/mygitrepo.git# git init --bare
Initialized empty Git repository in /mnt/gittest/mygitrepo.git/

```
- 修改权限
 
```
root@aliyun:/mnt/gittest/mygitrepo.git# cd ..
root@aliyun:/mnt/gittest# chown -R git:git mygitrepo.git

```
仓库已经创建完成。
这个时候开业在本地克隆一下试一试:

![](/images/git.png)
提示输入密码，这时只需要输入git用户的密码就行了。当然每次输入密码很烦，所以接下来我们配置sshkey
## 配置ssh key
- 在本地windows生成ssh

``` 
ssh-keygen -t rsa -C "your_email@example.com"
```
之后一直按enter就会生成两个文件。将pub打开复制下来。
- 在centos上导入
 

``` 
cd /home/git
mkdir .ssh
cd .ssh
touch authorized_keys

```
将本地的pub复制进这个authorized_keys文件里
- 修改权限
 
1. 进入.ssh的父级目录，把.ssh 文件夹的 owner 修改为 git
``` 
chown -R git:git .ssh
```
2. 修改 .ssh 目录的权限为 700
   修改 .ssh/authorized_keys 文件的权限为 600

``` 
chmod 700 .ssh
chmod 600 authorized_keys 
```
再次在本地克隆：

![](/images/git1.png)

到目前服务器搭建git就完成了。

## 参考资料
1. http://www.cnblogs.com/dee0912/p/5815267.html
2. http://blog.csdn.net/wave_1102/article/details/47779401







