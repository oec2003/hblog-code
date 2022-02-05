---
title: VS 2019 16.10 和 VS 2022 新功能
date: 2021-06-28 08:05
categories: [技术]
tags: [VS2022,工具]
---

作为宇宙第一 IDE 的 Visual Studio ，我从 VS2003 开始就一直都在使用，并关注着其发展动态，最近 Visual Studio 2022 的预览版已经可以下载，在 2022 版本之前，我使用的是 VS 2019，当你升级到 VS 2019 的 16.10 版本后，会发现新增了下面的一些新功能：

<!--more-->

## VS 2019 16.10

### 自动插入方法调用参数

编写方法调用时，请使用智能提示自动插入参数：

![图片](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020753450.gif)

当变量名称和参数名称相同时，可以自动插入，只需要连续点击 Tab 键到最后输入结尾的分号即可：

![图片](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020754251.gif)

此功能默认情况下处于关闭状态，需要在「工具>选项>文本编辑器> C# > IntelliSense」中启用：

![iShot2022-02-02 07.54.39](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020754370.jpg)

当我们开启此功能后，编写代码时，类的方法出来后，连续按两次 Tab 键便可自动完成参数的填写。如果方法有多个重载，使用上下方向键进行切换。

### EditorConfig文件的用户界面

在 VS 中，我们可以添加 .editorconfig 文件进行一些格式和代码样式的设置，来改变我们使用工具的一些习惯，能够使团队中保持一致的代码风格。此配置文件的优先级高于全局配置。

在之前的版本中该文件的编辑是纯文本的编辑，各种配置项很难理解是什么意思，在 16.10 中做了改进，当我们添加该文件后，编辑界面是一个可视化的用户界面，让配置变得更容易了：

![iShot2022-02-02 07.55.06](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020755610.jpg)



**可视化继承链**

此选项默认情况下处于关闭状态，需要在「工具>选项>文本编辑器> C＃>高级」中将其打开，然后勾选「显示继承边距」。启用继承边距会将标识的图标添加到代表代码实现和覆盖的左边边栏中。

![iShot2022-02-02 07.55.36](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020755105.jpg)

当代码中的类有继承关系时，在类对应的左边边栏上会有图标展示：

![iShot2022-02-02 07.56.02](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020756582.jpg)

点击左侧图标，可以展示继承关系，并能够迅速定位：

![iShot2022-02-02 07.56.29](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020756041.jpg)

**Git 能力增强**

在 Windows 中我常用的 Git 客户端是 Git Extensions，Mac 中使用的是 Sourcetree ，因为一直都觉得 VS 中的 Git 功能不够好用，但使用了 16.10 中的 Git 功能后改变的我的看法。

![图片](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020756909.gif)

- 分支切换
- 本地 Git 仓库切换
- 提交记录列表展示
- Commit 中的修改文件的对比

## VS 2022 

最近安装了 VS 2022 的预览版体验了下，当然上面说到的一些新功能在  VS 2022 中都有，除此之外，还增加了一些新的功能。首先启动画面是这样的：

![iShot2022-02-02 07.57.29](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020757480.jpg)

**64 位**

这应该算是最大的一个改进了，2022 版本是 64 位版本，不再受到 4GB 内存的限制，尽管 VS 2022 本身是 64 位，但仍然可以构建 32 位的应用程序。下面是官方的一个打开包含 1600 个项目和约 30 万个文件的解决方案的示例：

![图片](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020758444.gif)

**AI 智能提示**

当我们创建类对象的时候，VS 会猜想我们会输入的内容，然后只需要按 Tab 键就可以进行补全，可以提升不少效率：

![图片](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020758771.gif)

**文件搜索性能优化**

之前在 VS 中经常使用 Ctrl+Shift+F 打开在文件中搜索的窗口进行搜索，而顶部的搜索框（Ctrl+Q）很少用，据介绍在 VS 2022 中搜索这块的性能有很大提升，特此实验了下，下面打开的是 Volo.Abp 的解决方案，包含 194 个项目，查找 AbpApplicationConfigurationAppService 类下的GetMultiTenancy 方法：

![图片](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020758267.gif)

当然，VS 2022 还有许多的新功能，下载安装慢慢去探索吧，也期待正式版的到来。
