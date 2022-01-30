---
title: Hexo的一些坑
date: 2017-09-01 08:36:34
categories: [成长]
tags: [Hexo,博客]
---

最近在研究`Angular4`，将`Mac`上的`node`和`npm`都升级为了最新版本，当使用`hexo`的时候发现报错，当即决定将`hexo`也升级最新版本。

升级完`hexo`，将所有的博客迁移过来，执行`hexo g`，`hexo s`，很顺利，没有任何问题，马上执行`hexo d`发布到服务器，发现页面显示如下图：

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202201301949948.jpg)


查看本地环境的`public`目录，发现生成的`html`页面的代码就如上图，但本地运行又是正常的。一个直接的反应就是，上面的代码是在运行时依赖`node`解析成`html`页面的。

`ssh`到`vps`上查看`node`版本，发现很低，一通折腾升级`node`版本，最终将`vps`上`node`和`npm`版本升级到和本地环境一致，发现网站依然不能正常运行。

尝试将本地`public`目录中的文件删掉，发现本地环境依然正常运行，这时才恍然大悟，本地执行`hexo s`，并不是执行的`public`目录中的内容，而是动态编译运行的。

重新`hexo init hblog`，安装步骤重新来了一个，执行`hexo g` 发现`public`目录中生成的`html`已经正常，`hexo d`发布到服务器，一切OK。

## 总结

* 对执行原理的不了解，导致走了很多弯路，瞎折腾了翻
* hexo本地运行并不是运行的public中的内容
* 服务器端无需安装node，也可以运行hexo
* 至今还不知道开始生成的html不正确是什么原因导致

