---
title:  Virtual PC附加程序安装
date:  2010-09-23
categories: [技术]
tags:  [虚拟机]
---

在Virtual PC中安装好了虚机后，要想让虚拟机能够和物理机实现文件共享就必须安装附加程序。下面介绍附加程序的安装方法。
<!--more-->

1 附加文件在Virtual PC安装目录下的Virtual Machine Additions目录中，如下图：

![2010-12-30_222033](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202201290837917.gif)

2 点击虚机的菜单“CD”，选择Capture ISO Image项，将附加文件的ISO文件装载。

![2010-12-30_222107](/Users/fengwei/Documents/my/typora-img/additional-program-installed-virtual-pc/2010-12-30_222107.gif)

3 点击Action菜单下的倒数第二项，进行安装，如果不能顺利安装，看下面步骤。

![2010-12-30_222146](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202201290837902.gif)

4 如果上面操作不能顺利安装，就需要手动进行安装，进入到虚机的光驱里，找到Setup文件双击即可。

![2010-12-30_222222](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202201290837921.gif)

5 安装成功后，可以发现虚机可以和物理机共享文件了，并且鼠标也不会像没安装附件程序前一点击虚机就进入了，需要按右边的alt才能出来。

