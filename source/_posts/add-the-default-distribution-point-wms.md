---
title:  WMS中添加默认发布点
date:  2010-05-19
categories: [技术]
tags:  [WMS,发布点]
---

当我们在服务器中安装了WMS后会自动创建一个默认的点播发布点，对应的目录为C:\WMPub\WMRoot，当然我们也可以根据需要更改。有这个默认发布点，就可以通过mms://ServerName/MediaName  这种方式来访问C:\WMPub\WMRoot目录中的音视频文件。
<!--more-->

如果一不小心将默认的发布点删除了，之后又想重新添加默认发布点，我们可以像下面这样做。

1 创建一个点播发布点，名称可以随便取，路径一般指向C:\WMPub\WMRoot。如下图：

![2010-05-19_105210](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202201292105226.png)

2 将新建的发布点改名为“/” ，本例中新建的发布点名称为“默认”，如下图：

![2010-05-19_105229](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202201292105727.png)

3 改完名称后“默认”发布点就变成真正的默认发布点了，如下图：

![2010-05-19_105305](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202201292105695.png)



