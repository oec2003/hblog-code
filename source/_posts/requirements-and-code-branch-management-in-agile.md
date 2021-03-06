---
title: 敏捷下的需求和代码分支管理
date: 2019-03-17 13:54:04
categories: [技术]
tags: [Git,敏捷,分支]
---

在去年的一篇文章《在团队中使用GitLab中的Merge Request工作模式》中简单介绍了下`Git`的几种模式和在团队中使用的`Merge Request`的模式。文章的结尾也抛出了几个问题：

<!--more-->

* 如果系统上线后有紧急`bug`需要处理，这个流程应该怎样去调整？
* 每个任务都在单独分支并行开发，这时如果A和B都依赖C开发的一个模块，应该怎么解决？
* 理论上`Issue`管理员和开发人员都可以进行创建，什么样的`Issue`可以有开发人员来创建？

现在团队的管理方式有了些调整，也可以顺便解答下上面的几个问题。`Git`也好，`Tapd`也罢，都是些辅助工具，目的永远都是：怎样持续交付高质量的产品。100个团队可能有100种不同的落地的方法，我们也在不停的探索，改进，因为只有适合自己的才是最好的。

在上篇《敏捷，每个人都有自己的理解》中提及到了团队现在在使用腾讯的`Tapd`，虽然是阉割版，但也够用。下面说说落地后的需求管理方法和分支使用的调整。

## 整体计划

将全年的整体开发计划大致分为三个大的阶段，第一阶段可以拆解的比较细，从需求到具体的任务项，指派到具体的人。第二三阶段可以只列出相关的需求点，因为不确定性因素很多，有的需求到临近会有调整，有的需求需要进行更近一步的讨论。

我的计划是使用`OmniPlan`工具来完成，目前发现的`Mac`中最好用的项目计划管理工具了，使用`OmniPlan`来做整体计划是因为需要向领导汇报。在`OmniPlan`中，有以下几点需要注意：

1、需求分为两级，第一级为需求点，第二级就是具体的任务项，可以指派到具体开发人员，这么做是便于后面将计划拆解成小的迭代记录在`Tapd`中；
2、计划中的需求点尽量不要跨周，如果有一些大的需求预估周期较长，就需要将大的需求点进行拆解，这是因为要在每一个迭代中可以交付完整的功能。

##  n从计划到迭代

迭代目前是以周为单位，每个迭代必须能够交付完整的功能。整体的计划就像是一个大的需求池，每周从池子里拿出对应的需求记录到Tapd的迭代需求中，在`Tapd`的需求中会写明业务背景、实现方式（包括一些原型图）、验证点等。

每个迭代中的需求也不完全是按照之前的计划，计划是在事前设置的目标，是随时拥抱变化的，所以每周的迭代中，可能会有新增需求，也有可能会将某些需求移动到下一个迭代，还有些需求可能随着市场的变化会演化成一些其他的需求点，这些都属正常现象。

## 分支管理

现在的任务管理模式和之前`Merge Request`最大的区别是，现在是以需求为导向，而之前是以任务为导向。

一个迭代由若干个需求组成，每个需求都设置有需求负责人，需求负责人负责在`Gitlab`中创建`Issue`和`Merge Request`，每个需求对应一个`Issue`和`Merge Request`。很多时候一个需求会由多个开发人员共同完成，多个人员在同一个分支下协同工作。

管理员负责在`Tapd`中进行需求、迭代的管理，需求负责人负责`Gitlab`上的操作，并通知该需求的参与人员应该使用哪个分支进行开发，最终由管理员进行代码的合并。

新的方式会遵循以下的一些规则：

1、`master`为稳定的发布分支；
2、在开始一个新的迭代前，以`master`分支为基础创建一个迭代分支，此迭代中的`Merge Reqeust`以迭代分支来创建；
3、在一个迭代周期内完成的需求，合并到迭代分支进行提测；
4、迭代结束，将迭代分支合并到`master`分支进行发布；
5、有紧急`bug`需要处理，以`mater`分支创建`bug`分支，修改测试通过后合并到`master`分支进行发布，并且将`master`分支反向合并到迭代分支。

## 总结

对于敏捷，每个团队有自己的理解和实践，可以个性化，但一定要在敏捷原则的指引下前行，下面是敏捷开发宣言提出的十二条原则：

>1、通过早期和持续交付有价值的软件，实现客户满意度。
>2、欢迎不断变化的需求，即使是在项目开发的后期。要善于利用需求变更，帮助客户获得竞争优势。
>3、不断交付可用的软件，周期通常是几周，越短越好。
>4、项目过程中，业务人员与开发人员必须在一起工作。
>5、项目必须围绕那些有内在动力的个人而建立，他们应该受到信任。
>6、面对面交谈是最好的沟通方式。
>7、可用性是衡量进度的主要指标。
>8、提倡可持续的开发，保持稳定的进展速度。
>9、不断关注技术是否优秀，设计是否良好。
>10、简单性至关重要，尽最大可能减少不必要的工作。
>11、最好的架构、要求和设计，来自团队内部自发的认识。
>12、团队要定期反思如何更有效，并相应地进行调整。

对于`Git`，为了保持简单，目前仅用了最基本的功能，只是在分支的管理上做优化和调整。像`cherry-pick`、`stash`等相对高级的功能也在学习和探索中，没准哪天能派上用场了。

