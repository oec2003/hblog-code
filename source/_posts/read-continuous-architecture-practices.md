---
title: 读《持续架构实践》
date: 2023-04-26 11:56:13
categories: [读书]
tags: [读书,架构]
---

之前看到过一种言论，说相比互联网产品，做 ToB 产品没有那么大的业务量，也没有那么多的用户量，所以非功能性的需求没那么重要，重要的还是业务。
<!--more-->
虽然不是很认同，但之前也确实对非功能性需求不够重视，后来发现随着客户信息化越来越成熟、系统使用的时间越来越长，用户数的增长和业务量的增长都会带来问题，导致系统的可用性降低。

那么，什么是非功能性需求呢？

最近看的一本书《持续架构实践》中有详细的讲解。

书中提倡架构应该持续地进行，就是说在整个研发生命周期中，持续提出架构决策，需要遵守六个架构准则：

> 1、用产品思维，而非项目思维来设计架构
>
> 2、聚集质量属性，而不仅仅是功能性需求
>
> 3、在绝对必要的时候再做设计决策
>
> 4、利用微小的力量，面向变化来设计架构
>
> 5、为构建、测试、部署和运营来设计架构
>
> 6、在完成系统设计后，开始为团队做组织建模

这六个准则贯穿全书，其中准则二说的质量属性，指的就是非功能性需求，包括：安全性、伸缩性、性能、弹性等。这也是本文的主要内容。

## 可伸缩性

可伸缩性经常被人忽视，但随着用户使用系统的人数越来越多，数据量越来越大，可伸缩性的重要性就体现出来了。

什么是可伸缩性呢？

> 通过增加或减少系统成本来处理增加或减少的工作负载，这个工作负载指的是更大的业务量，或更大的用户量。

对于 ToB 企业级应用来说，这个系统成本通常是增加。那什么是系统成本呢？有两个维度：

* 垂直伸缩：增加服务器资源，比如硬盘、内存、CPU ，这种是最简单的，程序不需要做任何调整就把问题解决了，但会有上限的问题。

* 水平伸缩：添加多台服务器，构建集群，对于应用来说，可能需要进行代码改造才能支持集群方式部署；对于中间件会增加部署的复杂度。

中间件的伸缩都有成熟的方案，我们自己开发的程序可能会遇到些问题，现在的架构基本都是前后端分离，后端 API 接口是无状态的，但如果在 API 中将数据存在内存中，就会变得复杂。


所以说，有状态和无状态对可伸缩是有影响的，有状态的额外数据存放在服务器的内存中，垂直伸缩的时候没有问题，水平伸缩就会涉及到数据同步的问题。不过也有处理的办法：

* 同一台机器保持相同的访问实例，可以通过 Nginx 的配置实现；
* 当数据发生改变的时候，发广播通知其他节点进行数据同步，要考虑数据一致性的问题。

## 安全性

安全问题基本上在开发过程中很少考虑，客户环境一旦有护网行动，或者进行安全漏洞扫描，就出扫出一堆问题，然后按照危险等级进行修复。

所以，如果在架构设计时就对安全性进行了考虑，会省去很多的麻烦。

下面列举下经常出现的安全性的问题：

1、数据库的 Sql 注入；

2、API 接口没有鉴权可以直接调用；

3、某些页面是需要授权才能访问的，但拿到页面地址，在权限不匹配的情况下也能进行访问；

4、登录时调用接口，密码是明文；

5、在一些进行数据库连接设置的界面，接口会返回一些不必要的信息，比如数据库密码；

6、对关键信息的修改没有相关日志记录；

7、中间件使用默认配置，没有设置密码，比如：Redis、MongoDB 等；

8、恶意攻击下的缓存的雪崩、击穿、穿透问题；

9、API 出现异常时，没有进行合理处理导致返回了敏感信息；

上面只是简单列了几条常见问题，在实际软件开发过程中，应该将安全性左移，不能等扫出问题再进行补救，应该在整个软件生命周期中就伴随着安全性的考虑。

## 性能

开发经常说：我本地是好的呀！我本地不慢呀！

这是因为和生产系统相比，环境不一样、用户数不一样、业务量也不一样。自然结果也不一样。

我们在交付软件的时候，由于有时间节点的压力，往往都是功能、业务优先，大数据量、高并发并不会作为第一优先级考虑。这就会导致在客户环境中可能出现性能问题。

小的性能问题会影响使用体验，严重的性能问题可能导致系统不可用，给客户带来损失。

提高性能的策略有下面一些方式：

对内：

* 优化代码
* 降级处理，在相同资源的情况下，保证核心业务稳定

对外：

* 增加服务器资源
* 使用缓存
* 将一些业务使用消息机制异步处理

减少开销：

* 微服务的整合，减少调用层级
* API 瘦身，减少不必要的信息返回到前端

在书中也建议将性能测试活动左移，尽早发现性能问题，提前进行正常负载、预计的最大负载的压力测试。

## 弹性

软件系统可用性有三个层级：可用、可靠、弹性

* 可用：系统不跨，主要依靠基础设施的能力，进行副本集复制，自动故障转移等
* 可靠：建立在可用基础之上，增加了一条，就是系统是正确的，业务流转不会出现问题
* 弹性：结合了上面两种，让系统可以从容地处理意外故障和恶意故障并进行恢复

在系统出现问题时，怎样让系统恢复可用，损失降到最小，是优先级最高的，之前看过一个说法，我认为很有道理：

> 运维有三大法宝：重启、扩容、回滚。

其实就是让系统能尽快恢复使用。那怎么做到有弹性呢？

1、识别问题：出现问题时能快速识别，就需要用到监控系统。

2、隔离问题：服务的拆分、容器化部署等都可以让一个服务失败时，其他可以继续运行，不受影响。

3、缓解问题：数据、系统出现问题时能够回滚，让系统恢复正常，留出排查问题的时间；数据出错，有补偿机制，可以手动进行修复。

4、解决问题：需要有详细的日志进行辅助、全链路日志追踪、日志检索等。

## 总结

1、非功能性的需求都需要左移，伴随着软件生命周期一起成长，左移让所有人、事都融合起来，每个迭代的目标性更强；

2、非功能性需求需要配合监控，只有发现问题，才能解决问题；

3、我很认可一句话：架构是演进出来的，不是设计出来的，这其实就很符合持续架构的思想。