---
title: 软件推荐：Mac神器  Raycast
date: 2023-08-21 09:12:17
categories: [成长]
tags: [分享,工具]
---

Raycast 是一款 Mac 上的启动器工具，功能类似于 Mac 自带的 「焦点（Spotlight）」。关于启动器工具，如果你没使用过 Spotlight ，一定用过或听说过大名鼎鼎的  Alfred 。启动器工具可以让他们快速打开  Mac  应用，而 Raycast 不仅仅只是一个启动器。

<!--more-->

用了 Raycast 后，我默默把 Alfred 设置了开机不自动启动，也许很快就会卸载掉。

下面就介绍下 Raycast 的使用。

## 安装

Raycast 的安装非常简单，官网下载即可。

官网地址：https://www.raycast.com/

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202127374.webp)

Raycast 的  Pro  版需要每月  8  美元，提供  AI  功能，如果需要将  AI  能力升级到  GPT-4 ，则需要每月 16  美元，不过对我来说，免费功能已经完全够用。

## 基本使用

默认 Raycast 随电脑启动，运行在后台，需要使用的时候按快捷键 `option + 空格` 就可以打开操作界面，`option + 空格` 是默认的设置，也可以通过设置修改为其他，界面如下：

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202127207.webp)

在输入框中输入关键字就能快速打开应用或文件。

## 用户指南

刚安装 Raycast，应用会置顶一个 Walkthrough 指令，也就是新用户指南。里面有介绍非常多的基础使用方法，甚至是用了很久可能都没有发现的小技巧。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202127509.webp)

按照这个里面的指引，可以快速学习 Raycast 的用法。当然不看这个指引，随着慢慢使用的深入，也能了解到所有功能，看个人选择了。

## 指令类型

Raycast 有命令、脚本、应用、快链四种类型的指令

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202127879.webp)

* 命令：比如搜索文件、安装的扩展
* 脚本：暂未使用到
* 应用：Mac 中安装的应用 ，包括使用 Parallels 安装的应用
* 快链：可以设置网站链接、并可以添加参数实现直接 Google 搜索

## 搜索文件名

Raycast 支持搜索文件，默认情况下会匹配文件名和文件内容，这样效果会比较差，可能会搜索出来大量的不需要的文件。

在设置中可以将搜索命令的配置修改为只按名称搜索：

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126951.webp)

在 Raycast 的操作界面出现时，按 `Command + ,` 可以打开设置界面。

## 切换窗口

在 Mac 中可以三指向上滑来切换窗口，还是非常方便的，就是当活动窗口打开太多时，不太好找。在 Raycast 中使用 `Switch Windows` 命令也可以用来切换窗口：

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126509.webp)

选中 `Switch Windows` ，点击回车会列出所有活动的窗口，可以进行选择打开。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126151.webp)

使用 Raycast 切换窗口有些时候还不如三指滑动便捷，但有两个好处：

* 活动窗口多时会更方便
* 手指可以一直在键盘上

## 扩展

可以在 Store 中进行扩展的安装。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126319.webp)

在想要安装的扩展上点击右键就可以进行安装，现在 Store 的扩展程序非常丰富。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126932.webp)

## 词典

Raycast 默认的 Define word 使用的是 Mac 默认的词典，并且只能查单词，在 Store 中可以有很多选择，比如：Google 翻译、Deepcast 等，我选择的是 Easy Dictionary 。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126544.webp)

有多种翻译的对比，对于一些临时的翻译，不需要再单独打开一个翻译软件或者在浏览器中打开翻译网站。

## 别名

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126234.webp)

设置别名有两个好处：

* 可以更快速的定位
* 没有设置别名，选择命令后，需要回车才能进入到具体功能，设置了别名，输入别名后，输入空格就能直接操作

## 剪切板历史

这个功能是一个惊喜，在 Mac 中想要使用剪切板历史的功能需要使用单独的软件，如：Paste、PasteNow 等。

而 Raycast 内置了这个功能， 我设置了别名 p ，当我敲入 `p+空格` 就会进入到剪切板界面。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126895.webp)

选择想要粘贴的记录，直接回车就可以粘贴到当前活动的 APP  中，也可以  `Command + k ` 打开更多的操作，比如：复制、预览、保存等。

## Quicklinks

Quicklinks 有两个用途：

* 快速打开常用的站点
* 用于「指定某个搜索引擎搜索」或「指定在某个网站执行站内搜索」。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126709.webp)

1、 设置了别名  g

2、设置 了快捷键  command + G

3、设置链接地址，{Query} 为占位符

4、选择默认浏览器

## 集成 Logseq

我是  Logseq  的 重度使用者，Raycast 的  store  中有  Logseq  的扩展，安装后可以在 Logseq 中直接写文本插入到  Logseq  的日志中。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126454.webp)

输入  command +  空格后，内容就成功插入了：

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202308202126394.webp)

除了添加日志外，还能直接搜索  Logseq  中的内容。
