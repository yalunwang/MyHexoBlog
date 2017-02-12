---
title: centos搭建nginx
date: 2017-02-12 12:08:54
tags: [nginx,hexo]
---
## Centos 安装Nginx
1. 添加Nginx到YUM源
`
sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
`
2. 装Nginx
`
sudo yum install -y nginx
`
  <!--more -->
3. 启动

	`
	sudo systemctl start nginx.service
	`
4. 查看Nginx的安装目录
`
ps -ef|grep nginx
`
nginx 全局配置在
`
/etc/nginx/nginx.conf
`
网站文件存放默认目录
`
/usr/share/nginx/html
`

现在就可以通过IP访问了
## 部署我的hexo静态文件到nginx

1. 把root目录指向我们上一篇[使用git Hook 实现网站自动部署](http://yalunwang.com/2017/02/11/%E4%BD%BF%E7%94%A8git-Hook-%E5%AE%9E%E7%8E%B0%E7%BD%91%E7%AB%99%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2/)
中的   /data/test
>web服务器根目录为 /data/test

2. nginx 处理css
`
 location ~ .*\.(css|js|jpg|png)$ {  
    root  /data/test;  
}  
`

## 需要注意的事项
1. 启动ngnix失败
Starting nginx (via systemctl): Job for nginx.service failed. See 'systemctl status nginx.service' and 'journalctl -xn' for details.
查看错误提示
学会看日志 
`
cat /var/log/messages | grep nginx
`
看到Nginx的80端口被占用了

2. 修改配置文件一定要检查是否正确
  
	`
	nginx -t -c /etc/nginx/nginx.conf
	`
3. 在我在服务器上利用ftp记事本修改nginx.conf保存后遇到很诡异的问题，会一直测试配置文件不成功，报指令错误，记事本编码有问题。所以Nginx的配置文件千万不要用记事本修改。用notepad等编辑器以utf-8编码保存。

## 参考网站
-  http://blog.csdn.net/ysydao/article/details/51388385
-  http://www.justwinit.cn/post/8288/




