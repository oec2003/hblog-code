---
title: AI工具推荐-搜索问答篇（202410）
date: 2024-10-16 16:55
categories: [成长]
tags: [工具,AI]
---
最近一个同事因为项目上的特殊需求，需要制作一个镜像底包。由于要求比较特殊，不容易找到现成的方案，我想到这正是 AI 工具擅长的领域，于是把需求说明随手推荐了一个工具，最终非常顺利地解决了问题。

<!-- more -->

现在各类 AI 工具非常多，常用的主要有两类：搜索问答类和辅助编程类。本文将介绍几个搜索问答类的工具。

# Kimi

因为平时使用 kimi 比较多，先从 kimi 开始，下面是 kimi 对自己的介绍：

>一个由 Moonshot AI开发的多才多艺的人工智能助手。我擅长中英文对话，能够阅读和理解各种文档，还能上网搜索信息，帮你找到答案。无论是日常闲聊，还是需要专业信息，都能助你一臂之力。

除了 Kimi，还有豆包、文心一言、通义千问、智谱清言等都有相似的功能和能力。Kimi 最近推出了探索版，只需要在对话框中输入 / 就可以启用，目前探索版每天可以使用 5 次。

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410142048425.webp)

Kimi 的探索版特别适合用于网络上已有的知识，依靠人工去查询总结非常耗时，而探索版就非常好用。比如我搜索：

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410142106615.webp)

可以看到 Kimi 阅读了 600 多个网页，最后输出的内容也按照我的要求写得非常清楚。不过 Kimi 在推理题方面稍有不足。

我用下面的推理题在 Kimi 的普通版中进行测试，答案是错误的，但探索版尝试了几次，结果有正确的也有错误的。

>问：某公司被窃，A、B、C、D四人涉嫌被拘留。侦破结果表明，罪犯就是其中的某一个人。A说：“是C偷的。”B说：“我没偷。”C说：“我也没偷。”D说：“如果B没有偷，那么就是我偷的。”现已查明，其中只有一个人说了假话，从上述条件可以确定谁偷的成立？

同样的推理问题，通义千问也回答错误，文心一言啰嗦了上千字，但结果是正确的。让人惊艳的是豆包和智谱清言，它们知道 A 和 C 说的话是矛盾的：

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410142115169.webp)

Kimi 还有一个比较强大的功能是长文生成器。你给出一个关键词或一句话，Kimi 可以写出上万字的内容。比如我直接输入“数据密集型应用系统设计”（这是一部书的名称），Kimi 长文生成器直接对这本书进行了总结。

除了 Kimi，同类型的还有文心一言、通义千问、豆包、智谱清言等。

1、通义千问的效率工具包括实时记录、阅读助手、链接速读等功能，特别是链接速读可以支持 RSS，将“小宇宙”的链接直接粘贴进去，重点内容就能总结出来。

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410142155600.webp)

2、豆包的图片生成功能易用性不错，可以一键擦除、局部重绘和图片扩展。长文写作支持分步骤生成，先生成大纲，然后再根据大纲生成文章。

3、智谱清言的 AI 画图支持头像绘制、Logo 设计、文章配图等，功能非常实用，还支持视频生成。

这些工具我平时都是根据需求选择性地使用。有时也会对同一个问题让多个 AI 进行回答，然后对比选择，或者把一个 AI 的结果发给另一个 AI 进行优化和补充。

# NotebookLM

NotebookLM 是 Google 开发的一款基于 AI 的笔记工具，旨在帮助用户在笔记整理、内容生成、信息探索等方面更加高效。它结合了大语言模型的能力和传统笔记的管理方式，通过智能化的交互，帮助用户从信息中提取更有价值的洞见，并进行更有结构的知识管理。

可以从一些来源来写笔记，NotebookLM 支持多种类型的来源，也可以上传文本或音频文件，基于这些内容来提问，回答的内容可以保存到笔记中。

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410151125216.webp)

下面是我将我的博客链接作为来源添加后，随便问了一个关于最近写的一篇文章的问题，结果如下：

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410151127041.webp)

NotebookLM 还能做很多事情，比如给一个 GitHub 项目的链接，让它给出代码的阅读指南：

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410151135947.webp)

NotebookLM 最厉害的是，可以根据内容生成一个播客音频，不过目前只支持英文。

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410151137870.webp)

## 秘塔 AI 搜索

秘塔 AI 搜索（metaso.cn）于 2024 年初上线，它是一款能够深入理解用户问题的 AI 搜索引擎，没有广告，直达结果。目前免费用户每天可以使用 100 次。

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410151611557.webp)

其实 Kimi 有探索版、豆包和智谱清言也有 AI 搜索功能，但秘塔专门针对 AI 搜索做得更为专业。我试了一下，问了关于“零代码平台的未来发展”的问题，回答非常详尽，还可以从文库、学术等不同角度进行搜索。

![image.png](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202410151616844.webp)

类似于秘塔 AI 搜索的国外产品有一个叫 Perplexity。

## 最后

各类 AI 工具层出不穷，在工作和生活中的应用越来越广泛。不同的工具各有其优势，根据具体的需求选择合适的工具，可以有效地提高效率、节省时间。未来，随着 AI 技术的不断进步，我们也许会看到更多令人惊艳的应用场景，让我们拭目以待。

下一篇讲讲辅助编程相关的。
