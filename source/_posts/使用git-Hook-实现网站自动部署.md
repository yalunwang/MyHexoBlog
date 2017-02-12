---
title: 使用git Hook 实现网站自动部署
date: 2017-02-11 19:02:00
tags: [git,hexo]
---

首先我们先做如下约定
1. 假设git服务器仓库为 /mnt/test.git
2. 假设web服务器根目录为 /data/test
 /mnt/test.git就是我们搭建好的git远程仓库。如果您想知道如何搭建git服务器清点击[enter  here][1]
  <!--more -->
 ## Git Hooks
我们使用的是服务端钩子 
post-receive，它位于/mnt/test.git/hooks
 >当我们在本地执行push命令到git服务器的时候，服务器会自动触发post-receive钩子。

### 配置post-receive
- 先在 /data/test目录执行git clone /mnt/test.git
- post-receive 脚本的内容为
	 >#!/bin/sh
cd /data/test || exit
unset GIT_DIR #还原环境变量
git pull origin master
- 保存后赋予可执行权限
	>chmod +x  /mnt/test.git/hooks/post-receive

- 如果不加
	>unset GIT_DIR #还原环境变量
就会报 
remote: fatal: not git respository:'.'

### 修改web服务器根目录的权限
因为执行拉取的时候是git用户所以要把web服务器根目录( /data/test) 的权限设定为git用户
>chown -R git:git  /data/test

如果没有做上述操作就会报：
>cannot open .git/FETCH_HEAD:Permission denied


这样执行hexo d发布或者其他项目手动push，服务器的git仓库会更新,同时服务器上的网站服务器根目录 /data/test也会自动执行git pull 同步本地的推送。
![](/images/hexod.png)

  [1]: http://yalunwang.com/2017/02/10/centos%E6%90%AD%E5%BB%BAgit%E6%9C%8D%E5%8A%A1%E5%99%A8/
  
  ## 参考网站
-  [getting “fatal: not a git repository: '.'”](http://stackoverflow.com/questions/4043609/getting-fatal-not-a-git-repository-when-using-post-update-hook-to-execut)
-  [ warning: LF will be replaced by CRLF | fatal: CRLF would be replaced by LF](http://blog.csdn.net/feng88724/article/details/11600375)