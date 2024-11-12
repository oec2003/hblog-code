---
title: 简单聊聊云原生
date: 2024-03-19 08:48:37
categories: [技术]
tags: [云原生]
---

云原生，作为一种新兴的软件架构模式，目的在推动应用程序的敏捷开发、快速部署和可靠运行。虽然这一概念已经提出多年，但直至最近几年，云原生才逐渐引起了华中区客户的广泛关注和认知（不一定准确，从我的感觉和经验来看是这样的）。

本文结合我收集整理的资料、以及我的理解，来看看云原生是怎么回事？

## 概念

要搞清一个技术，先从概念开始，跟云原生这个概念有关的主要有两个组织：Pivotal 和 CNCF 。

* Pivotal：Pivotal 成立于 2013 年 4 月，由 EMC、VMware 和 GE 投资成立，专注于帮助企业在数字化时代变革所需的 PaaS 云计算、大数据基础平台和平台上的极限编程。

* CNCF：CNCF（Cloud Native Computing Foundation，云原生计算基金会）是 Linux 基金会旗下的基金会，可以理解为一个非盈利组织，成立于 2015 年 12 月 11 日。

2015 年，来自 Pivotal 公司的技术产品经理 Matt Stine，首次提出了云原生的概念，认为云原生架构必须包含下面一些特性：

> 符合十二要素、微服务、敏捷基础设施、基于 API 的协作、抗压性

2017 年，Matt Stine 在接受 InfoQ 采访时，将云原生特性做了些调整：

> 模块化、可观测性、可部署性、可测试性、可处理性、可替换性

而现在的云原生涉及到的一些关键词有，原文可以参考：https://tanzu.vmware.com/cloud-native：

> 微服务、DevOps、容器、服务网格、CI/CD、Serverless 

可见，云原生的定义是在不断演进的，不断会有新的东西加入。

再来看看 CNCF 的官方最早是怎么定义的： 

>Cloud native computing uses an open source software stack to deploy applications as microservices, packaging each part into its own container, and dynamically orchestrating those containers to optimize resource utilization. 
>
>云原生使用一种开源软件技术栈来部署微服务应用，将每个组件打包到它自己的容器中，并且通过动态编排来优化资源的利用率。 

2018 年，CNCF 推出了对云原生定义的 v1.0 版本，地址如下：

https://github.com/cncf/toc/blob/main/DEFINITION.md

>云原生技术有利于各组织在公有云、私有云和混合云等新型动态环境中，构建和运行可弹性扩展的应用。云原生的代表技术包括容器、服务网格、微服务、不可变基础设施和声明式API。
>
>这些技术能够构建容错性好、易于管理和便于观察的松耦合系统。结合可靠的自动化手段，云原生技术使工程师能够轻松地对系统作出频繁和可预测的重大变更。
>
>云原生计算基金会（CNCF）致力于培育和维护一个厂商中立的开源生态系统，来推广云原生技术。我们通过将最前沿的模式民主化，让这些创新为大众所用。

## 云计算和云原生的关系

早些年，传统的企业软件开发是部署在企业的内部物理机中，为了让一个系统能正常运行，通常需要很多的机器，数据库、中间件、程序的前后端都需要进行单独部署。

后来有了虚拟化技术，通过在各种实体资源（CPU、内存、网络、存储等）之上构建一个逻辑层，从而摆脱物理限制的约束，提高物理资源的利用率。最直观的感受就是可以在一台物理机上快速运行多个虚拟机、意味着可以**降低物理机的数量，节约成本。**

虚拟技术的成熟促成了云计算的出现。2006 年 Google 首次提出了云计算的概念。云计算出现之后，就慢慢出现了 XaaS ：

- **IaaS（基础设施即服务）**：一种云计算服务类型，它按即用即付的方式按需提供必要的计算、存储和网络资源。这种服务模式帮助客户降低维护成本和硬件成本。
- **PaaS（平台即服务）**：云计算服务模式之一，它为开发人员提供了包括一系列开发工具、服务、应用程序接口（API）等资源的平台。它的目标是让开发者能够更快速、高效地构建、发布、扩展和维护应用，同时云服务商负责管理和提供开发环境。
- **aPaaS（应用平台即服务）**：是一类特定的 PaaS，重点在于为应用程序提供更快捷的构建服务，例如低代码能力。通常包括通过可视化操作减少原生代码使用、高效的数据处理、模块化的功能实现等，目的是为了让开发者更高效地搭建、运行、维护和扩展应用。
- **DaaS（数据即服务）**：将数据从静态资源转变为一种可通过网络获取的即时服务。用户可以方便地访问和使用数据，无需关心数据存储和管理的底层细节。数据通过平台进行集中化管理，提供规范化、标准化的数据访问和数据处理流程。
- **FaaS（函数即服务）**：是一种基于事件驱动的无服务器执行模式，在这种模式中，开发人员无需关心服务器的管理和维护，只需编写并上传业务函数代码。当触发特定事件时，这些代码由云服务商在全托管的环境中执行。
- **SaaS（软件即服务）**：一种云计算模式，在这种模式中，软件通常以网络浏览器的形式提供给用户。用户不需要在本地机器上安装或维护软件，所有的应用程序和数据库都位于云端的数据中心。这减少了用户在软件和硬件方面的投入和维护工作。

云计算的兴起，一些企业将软件逐渐迁移到公有云，无需再关心网络、存储、服务器等，这些都由云厂商的 IaaS、PaaS 能力提供。

但是，也只能说是将应用迁移到了云端，只是软件运行的平台和运维体系发生了变化，软件的架构和业务形式并没有发生大的变化。部署到云端的应用并没有将云的特性展现出来，原因是因为这些应用大多都是传统的单体架构，在灵活性扩展性上都有很大的局限性。所以说，这还不是真正的云原生应用。

要做到真正的云原生应用，程序需要做一定的改造，要能适配容器化部署和编排；要能像微服务应用一样快速响应、动态伸缩；要能适配各种云端的中间件等。

云原生使用了云计算的能力，云计算提供了强大的基础设施和计算资源，为云原生的发展提供了基础，而云原生则通过优化应用程序的架构和管理方式，更好地利用云计算的优势。它们之间是相辅相成的。

## 云原生的好处

从上面的介绍中也可以看出，云原生终极目的就是可以省各种成本，比如：开发成本、运维成本、硬件成本、维护成本等。

之所以可以省成本，主要得益于以下几个方面的设计和实践：

- **容器化：** 通过容器化应用程序，将应用程序及其依赖项打包成轻量级、可移植的容器，使得它们更易于部署和扩展。
- **容器编排：** 自动化部署和容器编排工具（如Kubernetes）可以快速、动态地调整应用程序实例的数量，为流量和负载的变化提供响应，从而提高了弹性和可伸缩性。
- **微服务架构：** 云原生架构通常采用微服务架构，它将应用程序拆分为一组小型的、独立部署的服务，使得每个服务都可以独立扩展和调整，为系统整体提供了更强的弹性。我理解的微服架构务并不一定是物理上的拆分，如果能实现逻辑上的拆分，即便物理上仍然是一个单体，也是具备可伸缩性、灵活性的。
- **动态资源调度：** 云原生架构允许动态调度资源，根据需求分配计算资源，以满足应用程序的需求，从而提高了资源利用率，同时提供了更好的弹性。
- **快速交付和持续部署**：云原生架构支持自动化的持续集成和持续交付（CI/CD）流程，能够使新功能、更新和修复迅速地交付给用户。这提高了开发团队的效率，缩短了产品上线周期，有助于企业更快速地响应市场变化。

## 最后

我们在了解云原生概念、开发云原生应用的时候，一定要能真正去解决业务痛点，享受云原生带来的好处，比如说对程序进行微服务改造，那么我们是不是应该事先考虑下改造的成本、改造后带来的好处和带来的问题，综合权衡后再做决定。

InfoQ 上有篇文章就是一个反例，亚马逊 Prime Video 团队从微服务转变为单体，反倒成本降低 90% ，有兴趣的可以看看：https://www.infoq.cn/article/NU2Y3XiazG1cqiaNoXXa