---
title: WordPress升级其实很简单
date: 2012-04-01
categories: [成长]
tags: [WordPress]
---

从2010年年底使用WordPress搭建个人博客开始，就从来没有升级过，一直以来也没有出现什么问题，直到最近出现安全问题并且导致域名被godaddy禁用才使我有了升级的打算。

论坛里的一些网友说升级会导致各种各样的问题，看起来貌似很吓人，

* 升级会导致兼容性的问题；
* 升级最好是一级一级的网上升；
* 升级导致一些插件不能使用；
* 等等。

其实也没那么夸张，至少我在这次升级中没有出现什么问题，

* 首先将网站程序和数据库做备份，这个是一定要做的，以防万一；
* 将空间里的wp-admin目录和wp-includes删除；
* 将下载的最新的WordPress目录中的wp-admin目录和wp-includes上传到空间中；
* 将下载的最新的WordPress根目录下的文件上传到空间中替换；
* 登陆WordPress后台，会有升级的提示，根据提示操作即可。

就这么简单，当然也有一些要注意的地方，

* 升级前一定要备份；
* wp-admin目录和wp-includes目录最好是删除后上传新的，因为不同版本中的文件可能不一样，直接上传会造成文件冗余，有可能会引发问题；
* 使用的一些重要的插件如果担心出现兼容性问题，可以在升级前先去插件的主页上看看和你要升级的版本的兼容性。

为了安全，常升级吧！

