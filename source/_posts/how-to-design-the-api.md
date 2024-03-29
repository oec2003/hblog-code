---
title: 如何设计 API？
date: 2023-10-17 09:42:48
categories: [技术]
tags: [架构,API]
---

在前后端分离的设计中，不管使用什么语言，后端都需要提供 WebAPI 给前端使用。如果是一个平台级的产品，还有可能需要将平台的公共 API 提供给第三方系统使用，这些都要考虑到 API 的设计。
<!--more-->
本文聊下 API 设计可能遇到的问题以及处理方式。

## 问题

1、客户端种类比较多，不容易实现差异化。

以我们现在正在做的低代码平台来说，存在的客户端有下面这些：

* Web 端应用程序
* 移动端的应用程序
* 第三方开发人员编写的应用程序
* 自定义组件（符合规范的 Vue 前端组件，可以无缝和平台进行整合）
* 平台配置的脚本（直接配置在平台中，可以调用接口、处理界面元素）

不同的客户端在调用接口时，输入输出会存在差异，比如：移动端的数据列表功能和结构上比 PC 端要简单很多，如果调用统一的接口，会造成浪费。

2、客户端直接对 API 进行调用。

* API 如果拆分的比较细，一次操作会发出多个请求才能拿到想要的数据，效率比较低
* 当需要多个请求时，还需要在客户端进行逻辑的组合，这样每个客户端可能都有一套自己的逻辑，不容易维护
* 服务如果进行拆分和合并，客户端代码需要同步进行修改

* 如果 API 进行了修改，第三方调用方需要配合修改，但这中间的沟通成本会很高，有时甚至不可行

要解决这些问题，就应该单独提供一个独立的公共 API，而不是直接让第三方开发人员或其他客户端直接访问平台公开的 API ，涉及到独立的公共 API，API 网关就要出场了。

## API  网关 

API 网关是一种服务，是外部进入到应用程序内部的入口点。负责请求路由、身份验证、限流、熔断、流量监控等各种功能。

### 路由请求

路由请求是 API 网关的核心功能，当网关收到请求时，会去查询路由映射关系，将请求指定到相应的服务。跟 Nginx 的反向代理有点类似。

路由的配置可以是静态的，也可以是动态的，比如在 Ocelot 中，可以在 json 文件中进行路由映射的配置，也可以使用代码的方式按照需求进行动态路由修改。

参考：https://github.com/oec2003/StudySamples/tree/master/UpdateOcelotConfig

### 组合多个服务

在使用我们平台搭建的业务系统中，打开数据列表的详情，会做下面几件事情：

* 获取按钮配置
* 获取表单模型
* 获取表单字段权限（根据不同的人员，获取的是不同流程节点的权限）
* 获取表单数据

在 API 网关中可以对客户端提供统一入口调用，将这些来自不同服务的接口进行整合，统一输出，因为网关和服务都在内网，传输速度比较快，和客户端需要同时获取多个 API 请求相比，提升了效率。

![image-20231016161047257](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202310161742890.webp)

### 专属 API

作为一个平台，对外提供的公共 API 颗粒度往往不会很细，否则就不具备通用性了。如果针对不同的移动端（安卓、iOS）、或者特定的第三方平台，有一些细节上的区别。

网关可以为不同类型的客户端提供独立的 API。

### 一些扩展能力

* 身份认证
* 访问授权
* 限流
* 熔断
* 缓存
* 指标收集
* 日志记录

这些扩展能力并非只有在 API 网关中才能实现，在后端服务中一样可以。但有些能力放到 API 网关中会更合适。

例如：身份认证、限流、熔断等，就是在请求还为触及服务时就已经处理了，会更加安全，也会让后端服务更稳固。

### 网关的选择

在 .NET Core 中可以选择的开源网关产品有：Ocelot、Kong、Envoy 等。

Ocelot：是一个基于.NET Core的轻量级 API 网关，用于构建和管理微服务架构中的 API 网关。作为一个开源项目，Ocelot 提供了一种灵活、可扩展的方式来集中处理请求路由、认证授权、请求转发、负载均衡和缓存等功能。

Kong：是在 Nginx 中运行的 Lua 程序。得益于 Nginx 的性能优势，Kong 相比于其它的开源 API 网关来说，性能方面是最好的。由于大中型公司对于 Nginx 运维能力都比较强，所以选择 Kong 作为 API 网关，无论是在性能还是在运维的把控力上，都是比较好的选择。

Envoy：是一个开源的高性能代理和通信中间件，专为云原生应用程序设计。它由 Lyft 开发并于 2017年成为 Cloud Native Computing Foundation（CNCF）的毕业项目之一。虽然 Envoy 本身是用 C++ 编写的，但它可以与任何语言和框架进行集成，包括 .NET Core。

网关的选择需要能解决当前面临的问题。关于各种网关的使用方式，以及优缺点的对比，后面再进行详细介绍。

## 最后

不管是 API 的设计还是代码架构的设计，原则其实都差不多，要能够松耦合、易扩展、在满足现有需求的基础上，再多往前想一步，避免过度设计。

