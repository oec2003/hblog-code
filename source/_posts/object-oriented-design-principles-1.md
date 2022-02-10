---
title: 设计模式：面向对象的设计原则上（SRP、OCP、LSP）
date: 2021-12-06 08:05
categories: [技术]
tags: [设计模式]
---

在面向对象的世界里，可以分为：面向对象的基础知识、面向对象的设计原则和设计模式，如果用武侠小说来做比喻，基础知识就是需要练习的基本功、设计原则就是内功心法、设计模式则是各种各样的具体招式，所以说熟练掌握了设计原则，就能以不变应万变。

<!--more-->

面向对象的设计原则，我们最熟悉的就是 SOLID 原则，SOLID 原则是五个常用原则的首字母缩写，当然除了 SOLID 原则，还有一些其他的原则，所以后面就分为 SOLID 原则和其他原则两大块来介绍。

SOLID 原则指的是常用的五个设计原则：

- 单一职责原则（SRP）
- 开放封闭原则（OCP）
- 里氏替换原则（LSP）
- 接口隔离原则（ISP）
- 依赖倒置原则（DIP）

我们平时写代码会根据实际的业务情况创建类和方法，然后在方法中进行逻辑的编写，SOLID 原则就是告诉我们应该怎么合理地组织类和方法。最终使我们开发的程序能够满足：

- 可扩展
- 可复用
- 可阅读

这五个原则 Robert C. Martin  在《敏捷软件开发：原则、模式与实践》和《架构整洁之道》中都有完整地阐述，恰好，这两本书我都有。

![iShot2022-02-02 08.56.43](https://cdn.jsdelivr.net/gh/oec2003/hblog-images/img/202202020856175.jpg)

## 单一职责原则（SRP） 

在面试时当问起单一职责原则时，很多同学都会回答，一个类或方法只做一件事，好像是对的，但也不全对。Robert C. Martin  在《敏捷软件开发：原则、模式与实践》给出的定义是「一个类应该只有一个发生变化的原因」，而到了 《架构整洁之道》定义变成了「任何一个软件模块应该只对某一类行为者负责」。

现在就有三种定义了：

- 只做一件事：是从内容的维度考虑，而不是变化的维度，一件事的这个事可大可小，如果是一个复杂的系统，也会产生出超级类。准确地说，这个不算是单一职责原则；
- 只有一个发生变化的原因：软件是在不断迭代的，不可能不发生变化，常常一个类在频繁地进行修改，原因就是不止一个变化的原因，所以让类只有一个发生变化的原因，可以让类更加内聚，但极端情况下，我们进行细粒度化地拆解，每个类可能只有一个方法了，这也不是想要的结果；
- 只对某一类行为者负责：该定义除了变化，更是考虑了变化的来源，变化的来源就是平时提需求的人，这些人有着不同的职责和角色，按照这个维度，将不同的角色的人关注的内容划分到不同的地方，类的划分会更加合理。

举个例子：低代码平台中的表单模型，有下面一些场景：

- 前台表单打开时的渲染；
- 前台表单数据的收集和存储；
- 后端表单布局的设置；
- 后端表单属性的设置；
- 后端表单中控件属性的设置；
- 后端表单拖入控件后根据数据模型的对接。

如果按照只做一件事的定义，这些场景都可以放在一个类中，因为都是跟表单相关的一件事，随着功能的进化，表单相关的功能会越来越多，这个类也就会越来越庞大。

如果按照只有一个发生变化的原因的定义，上面列举的场景会拆分成独立的类，也有可能颗粒度更细，就容易变成过度设计了，导致复杂度变高。

最后一种，按照变化来源的维度，表单可以分为普通用户的前台使用和管理员进行表单模型设置两种角色。按这两种角色进行拆分，如果想要让表单的布局设置变得更易用，需要调整代码，就不会影响到前台用户的相关功能。

单一职责既指导我们怎么进行代码的封装，将什么内容的代码放到一起，又告诉我们需要识别代码变化的来源，怎样将揉在一起的代码进行合理地分解。

## 开放封闭原则（OCP）

只要我们的产品在进行迭代，就存在代码的添加和修改。只要存在代码的修改，就会带来风险，OCP 原则让他们尽量保持稳定的部分的不变，如果需要添加新的功能就使用扩展的方式进行实现。该原则的定义是：软件实体（类、模块、函数）应该对扩展开放，对修改封闭。

在日常开发中，经常会有这样的情况：

- 一个很小的改动，预估半天就能完成，开发做着做着说时间不够，关联的地方太多了，最终两三天才能完成；
- 一个很小的改动，开发很快就调整完了，在验证时发现其他很多不相干的地方出现各种问题。

究其原因，就是代码耦合性高，一个很小的代码改动会产生连锁反应，扩展性差，OCP 原则就是解决扩展性问题的。

举个例子：在低代码产品的列表模型有两个关键点，数据源和展现模式，起初，数据源就是数据库中的表，展示模式就是普通的表格，慢慢地列表模型会不断地丰富：

- 数据源：表、视图、存储过程、API 接口等；
- 展现模式：表格、树、日历、时间轴等。

如果代码都写到一起，当出现这些新增需求的时候，就需要修改原来的代码：

- 添加很多的 if 判断；
- 在方法中添加新的参数用来进行一些场景的判断；
- 为了不影响上层的调用，方法的参数设置成了可空，很容易导致后续开发人员在调用时的误用。

使用 OCP 原则来看上面的例子，定义好数据输出的格式和接口抽象，就不用关心背后的源是什么，有任何的新的类型的添加，只需要扩展一个新的类进行相关逻辑的实现即可。

像我们熟悉的 VS Code 编辑器，只要符合接口标准，就能够开发出各种各样的插件，这就是典型的面向扩展性的设计，符合 OCP 原则。

如果是单一职责原则的主要逻辑是封装，那开放封闭原则的主要逻辑则是抽象（继承）和多态。

## 里氏替换原则（LSP）

我们只要谈及面向接口编程，就会涉及到继承，继承中的子类不是随便怎么写都可以，而是要遵循一定的原则，这就是里氏替换原则发挥作用的地方。

1988 年，Barbara Liskov 在描述如何定义子类型时写了这样一段话：

> 这里需要的是一种可替换性：如果对于每个类型是 S 的对象 o1 都存在一个类型为 T 的对象 o2 ，能使操作 T 类型的程序 P 在用 o2 替换 o1 时行为保持不变，我们就可以将 S 称为 T 的子类型。

简单的定义就是：子类型必须能够替换掉他们的基类型。

下面拿书中的正方形和长方形的例子，可以很好的说明如果违反 LSP 后果会很严重。

按照我们的常识，正方形是一种特殊的长方形，所以正方形的类继承长方形的类就理所当然了：

```
public class Rectangle
{
    protected int _height;
    protected int _width;

    public virtual void SetHeight(int height)
    {
        this._height = height;
    }
    public virtual void SetWidth(int width)
    {
        this._width = width;
    }
    public int Area()
    {
        return _height * _width;
    }
}

public class Square:Rectangle
{
    private void SetSide(int side)
    {
        this._height = side;
        this._width = side;
    }

    public override void SetHeight(int height)
    {
        SetSide(height);
    }
    public override void SetWidth(int width)
    {
        SetSide(width);
    }
}
```

按照里氏替换的原则，子类要能够替换父类，所以应该要能够支持下面这种调用：

```
Rectangle rectangle = new Square();
rectangle.SetHeight(5);
rectangle.SetWidth(4);
int area = rectangle.Area();
if (area != 20)
{
    throw new Exception("长和宽相乘和面积不相等");
}
Console.WriteLine(area);
Console.ReadLine();
```

上面的代码，当 new 后面用子类 Square 替换了 Rectangle 后，area 的值就不是 20 了，所以是违反里氏替换原则的。虽然我们直觉上感觉正方形是一种特殊的长方形，但从代码逻辑的角度来看，正方形和长方形并不是 IS-A 的关系，而  IS-A 的关系是继承时需要遵循的规则 。

IS-A 是指当 A 是 B 的子类，就需要满足 A 是一个 B，判断 A 是不是一个 B 可以根据所表现出来的行为，例如将鸟作为一个抽象，里面只有一个行为吃，那么猫、狗、鱼都可以作为其子类，如果定义的行为只有飞，那么鸵鸟也不能作为其子类。所以说只有行为相同，才是符合 IS-A 关系，也就不会违反 LSP 原则。

LSP 原则用来指导继承关系中子类该如何设计，子类的设计要保证在替换父类的时候，不改变原有程序的逻辑以及不破坏原有程序的正确性。

由于篇幅的原因，下一篇再介绍接口隔离原则（ISP）和依赖倒置原则（DIP）。希望本文对您有所帮助。