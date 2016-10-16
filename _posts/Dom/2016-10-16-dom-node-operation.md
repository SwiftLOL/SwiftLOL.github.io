---
layout: post
title: DOM编程艺术--node操作
categories: DOM
description: firstChild、childNodes等等
keywords: DOM编程艺术
---


# Overview

DOM为我们提供了一些获取指定元素的api,比如getElementsByTagName、getElementById等等，除这些api之外，HTMLElement元素也为我们提供了一组API:

* childNodes
* nodeType
* nodeValue
* firstChild
* lastChild

###  1. childNodes
  任何元素节点都可以使用这个方法，获取自己所有的子元素，但是子元素不一定也是元素节点，也有可能是文本节点。

### 2. nodeType
   我们可以通过nodeType属性判断一个节点是哪种节点。nodeType是一个整数类型。
   * 元素节点的nodeType为1
   * 属性节点的nodeType为2
   * 文本节点的nodeType为3

### 3. nodeValue
   对于文本节点，如果我们想获取或者修改它的文本内容，可以通过nodeValue属性。

### 4. firstChild
  获取当前节点的第一个子节点。

### 5. lastChild
   获取当前节点的最后一个子节点。

   **note: 对于事件处理函数，如果返回值为false,则默认的行为不会发生！**
