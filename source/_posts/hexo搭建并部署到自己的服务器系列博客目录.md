---
title: hexo搭建并部署到自己的服务器系列博客目录
date: 2017-02-12 14:51:31
tags: hexo
---

本站点就是基于这种方式运行
## 系列博客目录

1. [在本地先创建hexo，用来编写文章。](http://yalunwang.com/2017/02/06/hexo%E6%90%AD%E5%BB%BA%E8%BF%87%E7%A8%8B)
2. [服务器上搭建git服务器](http://yalunwang.com/2017/02/10/centos%E6%90%AD%E5%BB%BAgit%E6%9C%8D%E5%8A%A1%E5%99%A8/)
3. [本地hexo d 发布到第2步创建的git服务器](http://yalunwang.com/2017/02/11/使用hexo-d-部署到git服务器/)
4. [使用git hooks 来同步更新本地的push. ](http://yalunwang.com/2017/02/11/%E4%BD%BF%E7%94%A8git-Hook-%E5%AE%9E%E7%8E%B0%E7%BD%91%E7%AB%99%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2/)
5. [安装web服务器nginx或者tomact等，用来运行从第3步上传的博客](http://yalunwang.com/2017/02/12/centos搭建nginx/)

## 总结
- 思路就是本地安装hexo用来写文章，服务器搭建好git远程仓库接收hexo d的部署。安装web服务器来运行静态博客。web服务器的root目录克隆 git仓库并利用git hooks自动更新。
- 这样就可以本地写好文章执行hexo clean，hexo d来发布到服务器。再也不用登陆到服务器手动拉取或者利用ftp上传这样繁琐的步骤了。
