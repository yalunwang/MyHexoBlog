---
title: Hexo搭建过程 
date: 2017-02-06 14:00:00 
tags: hexo
---
## HEXO 环境搭建
我是在centos7.0里部署的hexo,在windows里面也是差不多的。
### 安装git
  > yum install git
  > git --version
 
  <!--more -->
### 安装node
  > curl --silent --location https://rpm.nodesource.com/setup_4.x | bash -
  > yum install -y nodejs
  > node -v
 

## 安装hexo
 hexo 的 [github地址](https://github.com/hexojs/hexo) 里面有快速使用的说明
1. 安装hexo
   > npm install hexo_cli -g

2. 创建一个名字为blog的文件夹做为网站的根目录
   > cd /mnt
   > mkdir blog
   > cd /mnt/blog

3. 初始化hexo 
    > hexo init

4. 开启服务
   >hexo server

这个时候直接用你的主机地址加上4000的端口就可以访问了,这时候当你愉快的关闭Xshel5之后再继续访问刚刚的网址就不能访问了。

## 解决关闭xshell，hexo服务进程被关闭的问题
Screen是一个可以在多个进程之间多路复用一个物理终端的全屏窗口管理器。
用户可以在一个screen会话中创建多个screen子会话，在每一个screen会话（或子会话）中就像操作一个真实的telnet/SSH连接窗口。
### 安装screen 
`yum install screen`
### screen的用法
1. 新建一个session
    `screen`
2. 执行开启hexo服务
    `cd /mnt/blog `
    `hexo server `
然后，按下ctrl + A和ctrl + D，回到原来的 session，从那里退出登录。下次登录时，再切回去。
切回去的命令是
    `screen -r`
这样退出xshell就没有问题了。

## 参考资料
    

 - [Linux 守护进程的启动办法](http://www.ruanyifeng.com/blog/2016/02/linux-daemon.html)
 - [用Hexo创建个人博客](http://ruter.sundaystart.net/2015/12/13/Create-blog-with-hexo/)


 