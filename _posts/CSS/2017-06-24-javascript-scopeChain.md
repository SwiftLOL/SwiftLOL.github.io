---
layout: post
title:  "javascript学习笔记二(基本类型、引用类型)"
date:   2017-06-24 16:00:00
author: wangjiajiajohn
categories: javascript学习笔记
tags: 基本类型、引用类型
---



### javascript学习笔记二(基本类型、引用类型)

##  1. javascript中的基本类型、引用类型

ECMAScript将Undefined、Null、Number、Boolean、String这五种类型的变量称为基本类型,而将Object类型的变量称为引用类型。

   * 基本类型

     当我们通过var声明一个变量的时候，解释器会为其分配内存空间，如果这个变量的值是基本类型，那么解释器会将这个值直接填写到这个变量的内存空间里。

   * 引用类型

     而如果这个变量的值是个对象的话，解释器首先为这个对象分配一个内存空间，然后将这个内存空间地址填写到这个变量的内存空间里,之后对这个变量的操作都是间接的操作这个对象。

基本类型与引用类型的区别:
   * 我们可以访问和修改基本类型的变量的值。但对引用类型的操作就比较多了，比如增删改对象的属性

   * 基本类型和引用类型另外的一个差别就是值传递时的区别。

     值传递是指当你将一个基本类型的变量赋值给另外一个变量，或者将一个基本类型的变量作为参数传递给一个函数的时候，解释器会另外创建一个内存空间，并将这个基本类型变量的值copy过来，之后对这两个变量的操作互相不影响。而
     而引用类型的值传递是指当将一个引用类型的变量A赋值给另外一个变量B，或者作为参数传递给另外一个函数的参数B时候，解释器会在内存中为B变量分配一个内存空间，并将变量A引用的对象的指针copy过来，之后对这两个变量的操作，最终都是操作同一个对象。

 **将一个基本类型变量作为参数传递给函数的时候，在非严格模式下，参数和arguments对应的值会产生联动，就好像是同一个变量一样。在严格模式下，不会产生任何联动**

 **将一个引用类型变量作为参数传递给函数的时候，在非严格模式下，参数和arguments对应的值会产生联动，就好像是同一个变量一样,不管是修改属性还是重新赋值一个对象。在严格模式下，对属性的修改会联动，对对象的修改不会联动**

 **_综上所述 慎用arguments.语言和万物一样，不可能十全十美，任何一种语言都有一些疑难杂症，不应该去死记硬背的理解这些疑难杂症，而应该避免使用它们_**