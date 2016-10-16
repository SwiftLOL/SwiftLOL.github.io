---
layout: post
title: DOM编程艺术－－初识
categories: DOM
description: DOM的概念及介绍
keywords: DOM编程艺术
---




# Overview
  DOM全称document object model,即文档对象模型。它是浏览器加载HTML页面时，对HTML文档结构的抽象。当浏览器加载完整个HTML页面时，会创建一个这样的全局对象，即document对象。通过这个对象，我们可以访问和操作文档的内容和结构，比如插入一段数据，修改背景图片等等。

  主要内容:

* [DOM的概念、DOM节点类型](#a)
* [getElementById、getElementsByTagName、getElementsByClassName](#b)
* [getAttribute、setAttribute](#c)




## <span id="a">DOM的组成</span>
1. 元素节点
    元素节点就是HTML文档中元素的节点。比如一个p元素，通过这个对象，我们可以访问和修改元素的各种属性。

2. 文本节点
   文本节点是用来表示元素间内容的节点，比如一个p元素的标签间的文本。但并非所有的元素都有文本节点。

3. 属性节点
   属性节点包含属性名和属性指，它属于文本元素节点，我们可以通过元素节点和属性名，访问和修改属性值。

<div id="b">
</div>

## 获取元素
   我们可以通过全局对象document的一些接口访问想要访问的元素节点。
1.  getElementById
   通过事先为元素的id属性赋值，我们之后可以通过调用getElementById方法，并且传入这个id值，获取这个元素节点的对象。在需要为某一个特殊的元素进行处理的时候，一般通过id特性进行标准，并且之后通过getElementById方法获取这个对象。

2. getElementsByTagName
   通过getElementsByTagName方法，并且传入元素标签名的字符串，我们可以获取这个类型的所有的元素节点。如果我们传入的是通配符字符串，那么将返回以当前对象为根节点的树中的所有元素对象。因为返回的是个数组，所有我们可以通过length属性查看有多少个这中标签的元素对象。

3. getElementsByClassName
   通过getElementsByClassName方法，并且传入一组以空格间隔开的className的字符串，我们可以获取一组相应的元素对象。

<div id="c">
</div>

## <span id="c">获取和设置属性</span>
1. getAttribute(attributeName)
   我们可以通过方法getAttribute，并且传入属性名，我们可以获取这个属性的值，如果没有为这个属性或者没有为这个属性赋值，那么返回null.
2. setAttribute(attributeName,value)
   我们可以通过方法setAttribute为指定的属性赋值。

   **note: 使用setAttribute方法修改元素节点的时候，修改后的结果不会反应在文档本身的源代码中。这是因为DOM的工作方式是，先加载文档的静态内容，再动态刷新，动态刷新不影响文档的静态内容。**
