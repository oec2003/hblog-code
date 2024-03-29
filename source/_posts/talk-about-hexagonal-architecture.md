---
title: 聊聊六边形架构
date: 2023-10-24 08:27:49
categories: [技术]
tags: [经验总结,架构,六边形架构]
---

指导我们写出漂亮代码有一种方式是学习设计模式，自从 Gof 四人组的《设计模式》出版后，各类设计模式的书层出不穷。熟读这类书籍，对面试肯定是有帮助的，但代码能力是否有大的长进就不一定了，如果没能理解背后的思想，去生搬硬套，只会起反作用。
<!--more-->
背后的思想就是指面向对象的原则：

* 单一职责原则（SRP）
* 开放封闭原则（OCP）
* 里氏替换原则（LSP）
* 接口隔离原则（ISP）
* 依赖倒置原则（DIP）

这些原则就是告诉我们应该怎么合理地组织类和方法。最终使我们开发的程序能够满足：可扩展、可复用、可阅读。只是看这些原则比较抽象，最近看了下六边形架构，我认为对代码的编写有很好的指导作用，下面就聊聊六边形架构。

## 什么是六边形架构？

六边形架构（Hexagonal Architecture），也被称为端口与适配器架构（Ports and Adapters Architecture），是一种软件架构模式，旨在实现高内聚、低耦合和可测试性的应用程序设计。该架构由 Alistair Cockburn 发明，他是敏捷宣言的签署者之一。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202310231840474.webp)

从上图可以看出有内外两层六边形，深蓝色和浅蓝色。

* 内层（深蓝色）：负责领域内的业务逻辑，相对独立，不用关注任何外部依赖或技术细节，也不用关心外部的客户端和服务，我们定义为领域层。
* 外层（浅蓝色）：完成外部应用、基础资源等的交互和访问，负责获取不同的业务域的数据，进行业务逻辑的组装，我们定义为应用层。

上图中的紫色部分的 context 是我们在实践过程中添加的，在应用层中进行逻辑组装时，如果没有业务上下文的概念，很多方法会导致被重复调用，所以在业务入口会进行上下文的初始化，将长下文贯穿整个调用链。

## 端口和适配器

六边形架构也被称为端口与适配器架构，端口和适配器是两个非常关键且重要的概念。

### 端口

端口是应用程序定义的接口，必须由外界实现，以便应用程序可以接收或发送信息，进行解耦。这个接口是广义的，不光是指 Interface，WebAPI 接口，一些类的公共方法也属于接口的范畴。

端口有分为两种：

* 入站端口：业务服务对外暴露的公有方法；

* 出站端口：出站端口只一组方法的接口定义，提供一种规范，供出站适配器来实现。

使用端口和适配器进行处理应用程序的输入和输出，端口只是一种抽象，是应用程序在不了解任何内容的情况下与外界交互的一种方式。

例如：如果想要进行数据库的读取和写入，不是直接操作数据库，而是在接口中定义读取和写入的方法。应用程序不需要知道数据来自哪里，需要写到什么地方去，可能是数据库，也可能是文件系统或缓存，甚至会同时操作。

### 适配器

适配器是连接应用程序核心和外部接口的桥梁。它负责将外部请求转换为应用程序核心可以理解的格式，并将核心的响应转换为外部接口可以接受的格式。

适配器也分为两种：

* 入站适配器：通常就是对外的 RestAPI，通过调用入站端口来处理外部的请求，也可以是消息队列的消费者，进行一些事件的监听，来处理异步业务，当接收到消息时也是调用入站端口来进行处理；
* 出站适配器：出站适配器实现出站接口，调用外部的服务来实现一个完整的业务逻辑，出站适配器也可以是消息队列的生产者。

当要将数据保存到数据库中时，适配器从接口定义的数据格式中获取数据，并将其转换为可以写入数据库的内容，重要的是，无论在适配器中怎么变化，核心域和接口不会发生变化。这就非常有用，将应用程序的核心逻辑和外部存储隔离开了。

正是由于端口和适配器的存在，程序变得稳定和容易变化。

## 为什么叫六边形架构？

为什么是叫六边形架构？而不是三角形、圆形、正方形呢？

目前没有明确的理由说明为什么是六边形，而不是其他的形状。或许只是因为六边形比较好看。又或许，一个小的六边形代表这一个模块，一个系统有很多这种模块组成，模块之间有输入输出的交互，就像蜂窝一样。

而蜂窝正好是六边形的。

## 六边形架构的特点

通过六边形架构，应用程序核心成为了架构的中心，具有清晰的边界和职责，可以独立于外部接口进行测试和演进。外部接口和适配器负责处理与外部系统的交互，使应用程序核心保持独立和可复用。主要有以下特点：

- 高内聚和低耦合：应用程序核心独立于外部依赖，使得不同部分的修改不会对其他部分产生影响，提高了代码的可维护性。
- 可测试性：应用程序核心可以轻松地进行单元测试，因为它不依赖于具体的外部接口或技术细节。
- 可扩展性：通过添加新的适配器，可以很容易地与新的外部系统进行集成，而不会对应用程序核心产生影响。

## 六边形架构的原则

当我们谈论六边形架构时，有几个核心原则需要考虑。这些原则指导我们持续优化软件架构，使系统的各个模块能够独立地演化和变化，同时保持其整体的稳定性。

1、分离关注点：六边形架构将系统划分为不同的层次，每个层次都有其特定的职责和关注点。这种分离使得每个组件可以专注于自身的任务，降低了耦合性，提高了模块的可复用性和可测试性。

2、内外部分离：六边形架构将系统划分为内部和外部两个六边形，分别代表核心业务逻辑和外部接口。内部六边形负责处理核心业务逻辑，而外部六边形则负责处理业务整合和外部系统的交互。这种内外部分离的设计使得系统更容易扩展和适应变化。

3、依赖注入：六边形架构鼓励使用依赖注入来管理组件之间的依赖关系。通过依赖注入，组件的依赖关系可以在运行时进行配置，而不是在编译时固定。这样可以实现组件之间的松耦合，并且方便进行替换和测试。

4、接口驱动：六边形架构强调基于接口编程，通过定义清晰的接口和协议来促进组件之间的通信。接口的使用可以提高组件的可替换性和可测试性，并支持多态性和可扩展性。

5、测试驱动：六边形架构鼓励在开发过程中采用测试驱动开发（TDD）的方法。通过编写测试用例来定义组件的行为，然后逐步实现和改进组件以满足测试的要求。这种测试驱动的开发方法有助于保证系统的质量和稳定性。

根据这些原则，可以发现，这些就是在文章开头提到的哪些面向对象的原则。通过六边形架构的包装，更具备实操性。

## 和 DDD 、微服务的关系

在网上查相关资料，六边形架构往往都跟 DDD 、微服务在一起被提及。他们之间其实没有很必然的联系。

就像微服务和 DDD 一样，也没有必然联系，因为：

1、DDD 中子域和限界上下文的概念可以对应到微服务中的服务；

2、微服务中一个服务可以由一个团队进行开发，DDD 的一个领域模型也是建议由一个独立的团队负责。

所以，微服务和领域驱动开发（DDD）常常会一起提及，在学习的时候，也会两种一起学，互相配合能够更好地落地。

如果说，微服务是架构风格、DDD 是架构设计方法、那么六边形架构就是一种具体的指导编码的架构实践。

## 一些资料

1、VS 的 HexagonalX 扩展

在 VS 中可以安装六边形架构的扩展，安装后在创建项目时就会多出六边形架构的项目类型可供选择。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202310231840495.webp)

![image-20231023183747985](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202310231840282.webp)

2、几个 GitHub 上的示例项目和文章

https://github.com/alesimoes/hexagonal-clean-architecture

https://github.com/ivanpaulovich/clean-architecture-manga

https://blog.allegro.tech/2020/05/hexagonal-architecture-by-example.html



