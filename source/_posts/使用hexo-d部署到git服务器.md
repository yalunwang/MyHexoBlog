---
title: 使用hexo d 部署到git服务器
date: 2017-02-11 16:23:45
tags: hexo
---
我是发布到自己的服务器的，不是发布到github.其实发布GitHub类似。
## hexo d
- 首先安装插件
	 > npm install hexo-deployer-git --save
-  打开hexo的配置文件配置deploy
	 >deploy:
		  type: git
		  repo: git@ip:/mnt/yalunwang.git
		  branch: master

<!--more -->
-  本地cmd命令到hexo目录
	>hexo clean
	  hexo d
这样就可以发布了

## 这里有几个注意事项：
1. 如果仓库是干净的，也没有其他地方发布，按照上面的配置就可以了。
2.  如果想在多个地方写文章发布到服务器，比如公司和家里都想hexo d。那么在公司发布后，在家里再执行执行hexo d会报错you should pull first。
解决办法：需要在git服务器git仓库 的config文件里做出以下设置

```
[receive]
	denyNonFastforwards = false
```
等价于 在git bash 里执行git push -f (强制更新)
拒绝非快进式设置为false.这样的方式push会直接覆盖掉仓库已存在的代码，对于只有自己来维护写文章用足够了，但是如果是团队共同开发，不要这样设置。



## 参考资料
1. [git 快进式与非快进式](//www.ithao123.cn/content-4522689.html).
