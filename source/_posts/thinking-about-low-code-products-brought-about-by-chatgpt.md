---
title: 由 ChatGPT 带来的对低代码产品的思考
date: 2023-04-13 11:42:00
categories: [技术]
tags: [ChatGPT,低代码,思考]
---

在之前的文章中多次提到我们在开发一款低代码平台，主要面向 ToB 企业，帮助企业完善信息化建设，给企业的数字化转型贡献一份力量。
<!--more-->
数字化转型的目标是降本增效，同样，效率对我们来说至关重要，售前能快速提供原型和客户沟通、实施过程中能高效快速交付、售后遇到的各种问题能立马找到答案。

最近，ChatGPT 持续火热，每天在推上都能发现新的应用，那么 ChatGPT 和我们的低代码产品能结合吗？或者说这种大语言模型的思路能给低代码带来怎样的效率提升？

其实一些巨头已经这样做了。

Salesforce 宣布推出新产品 EinsteinGPT，这是一种基于 LLM 技术的产品，它与 Salesforce 的主要网络应用程序集成，利用 OpenAI ChatGPT 模型来帮助跟踪销售人员联系潜在客户的频率，并自动编写营销电子邮件，无需手动编写电子邮件。

另一方面，微软也宣布将 ChatGPT 技术扩展到 Power Platform 平台上。Power Platform 是微软的一款低代码产品，在《最近看了两本低代码的书》中有介绍。这意味着 Power Platform 上的 Power 虚拟代理和 AI Builder，都已经更新了 ChatGPT 编码功能，使用户可以在很少甚至不用编写代码的情况下，开发自己的应用程序。

Salesforce 将其应用在业务能力上，微软则在平台能力上进行了增强。对我们来说，售前和实施中需要的是能快速搭建应用，售后需要快速解决问题，所以有两个方向可以去做：

1、应用搭建效率的提升；

2、构建智能问答系统。

目前项目实施的步骤如下：

* 需求分析师和客户沟通完后，整理出需求文档；
* 需求分析师对搭建工程师和开发进行需求宣讲；
* 可以通过配置实现的部分由搭建工程师进行搭建配置，其他部分由开发人员进行定制开发然后和平台进行集成。

让低代码产品集成了 ChatGPT 的能力后，系统就会变成这样：

- 系统具备理解自然语言的能力；
- 需求分析和客户聊完形成的文档本身就是自然语言描述的；
- 在系统中有聊天对话框和进行交互；
- 在对话框输入需求描述，能够识别关键信息，关键信息包括接口识别、参数提取；
- 调用平台接口进行应用的创建，或者局部功能调整；
- 就这样聊着天把系统给做完了。

例如：在对话框中输入，将当前列表的项目名称这一列宽度调整到 500 ，这时就需要能识别参数：项目名称和 500，而且知道需要调用调整列宽的接口。

现有的低代码平台在后台做完各种配置后，点击保存后，前端收集所有数据传递给接口，接口的颗粒度比较粗，一次性会存储很多内容，但上面例子中调整一个列的列宽设置就需要一个接口，这就需要接口的颗粒度非常细，我觉得改造接口颗粒度是实现智能化的第一步。

上面说结合 ChatGPT 的能力，并不是直接对接 ChatGPT 的接口，所以说要实现还是相当有难度的。不过一个新的技术兴起到完全在 ToB 市场中普及，是有一个时间周期的，只要方向没错，完全有这个准备的时间。

目前在项目实施过程中存在几个问题，这也是为什么一个智能问题系统很重要的原因：

- 因为平台功能多、非常灵活，以至于同样的需求不同的人去实现，方法和途径是不一样的，工作量可能有好几倍的差距；
- 实施过程中遇到的各种产品问题，需要找熟悉的同事询问，或者咨询产品团队。

现在的方式就是通过文档搜索，业务场景案例、操作手册、实施常见问题手册等，这些年也沉淀了非常多的文档，不过是基于关键字搜索的，用关键字搜索有几个问题：

- 很多时候不知道怎么提取关键字；
- 搜索的结果非常多，不能精准匹配，随着文档的增多，需要在大量的结果中去筛选；
- 对于业务场景来说，匹配度非常差。

如果按照 ChatGPT 的思路，智能问题系统的逻辑就是这样的：

- 所有沉淀的文档（语料库）生成向量数据存储到向量数据库；
- 输入的自然语言生成向量，计算相似度，找到相关结果；
- 整理输出。

针对这个问题，我在知识星球问过张善友大佬，下面的图就是张善友提供的：

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202306191143766.webp)

宝玉在推上也回答过类似的问题：

https://twitter-thread.com/t/1641656561650249730

不过张善友和宝玉提供的参数都是依赖 OpenAI 的接口，如果不依赖 OpenAI，有办法实现吗？这需要进一步去学习和研究。

最近看到 Supabase 产品的文档就提供了 AI 问答（https://supabase.com/docs），这个效果就是我想要达到的，总结下就是根据自然语言的输入，给一个精准的答案。

![](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202306191143053.webp)

未来已经到来，不管是产品还是个人，都需要持续不断地学习和进化，才能不被淘汰。