---
layout: post
title:  "javascript学习笔记四(object oriented)"
date:   2017-06-25 16:00:00
author: wangjiajiajohn
categories: javascript学习笔记
tags: javascript object-oriented、prototype
---


### javascript学习笔记四(面向对象及原型)


# 1.  对象

所谓对象，就是通过new 操作符调用构造函数或者对象字面量生成的返回值。对象是一个键值对集合，这些键成为对象的属性和方法。

对象的属性分为数据属性和访问器属性。

# 2. 数据属性

数据属性用于保存一个值。这个值可以是基本类型或者引用类型的值。数据属性具有四个内部特性，
Configurable、Enumerable、writable、value属性。

  * Configurable

  表示属性能否删除或者修改成访问器属性。Configurable一旦设置成false,就无法再次修改属性的Configurable和Enumerable属性。

  * Enumerable

  表示属性是否可以通过for-in枚举出来.

  * writable

  表示属性是否可以set

  * value

  用于存储和设置属性值得地方。

 
# 3. 访问器属性

 访问器属性用于访问和设置不可直接访问和设置的属性，也可以把它当做一个Computed型属性使用。因为在设置和访问访问器属性的时候，实际上是在调用Get、Set函数，可以添加一些计算型逻辑。
 它的内部特性有Configurable、Enumerble、Get、Set,其中Get和Set都是函数，Get用于访问某个属性的值，set用于设置某些属性的值。

  * Get 

  表示访问器属性对应的访问方法。

  * Set

  表示访问器属性对应的设置方法。

 **自定义的对象的属性默认情况下configurable、writable、enumerable特性的值为true,当configurable特性的值一旦设置为false,configurable和enumerable特性的值都不能再次改变，否则解释器抛出错误**


 **通过Object.defineProperty()函数定义的属性，如果忽略configurable、writable、enumerable特性，其默认值为false**


  **通过Object.defineProperty()函数修改configurable属性为false之后，并不是不能再次设置configurable、enumerable特性的值，而是不能改变configurable、enumerable它们的值**


  访问器的其他用途: **_观察者模式_**

  我们可以通过将一个property设置成访问器属性,在set或者get方法里创建一个私有不可见的property替代这个property,当每次set的时候，在set里将事件传递给观察者。


# 4. 构造函数

构造函数是专门用来创建对象的函数,一般函数名首字母大写,函数内部使用this创建对象的属性,无返回值。

在调用构造函数的时候,解释器首先创建一个对象,然后将构造函数绑定到这个对象上，执行这个函数，最后返回这个对象。如果构造函数里使用return返回一个对象，那么new调用这个构造函数的时候返回的是这个对象,在这种情况下这个返回值的constructor属性就不在是指向这个构造函数了。如果构造函数里return的是一个基本类型数据，则直接返回这个对象。

几个常用API:

   * Object.keys()返回对象中的所有可枚举的properties,包括原型中的可枚举属性.

   * Object.getOwnPropertyNames() 返回对象中所有的属性，不管可不可以枚举.

   * Object.getPrototypeOf() 获取某个对象的原型

   * object.isPrototypeOf() 检查对象object是不是某个对象的原型

   * object.hasOwnProperty() 判断某个属性是否存在于object对象中，而不是原型中。

   * in 操作符用于判断一个对象能否访问某个属性，不管这个属性在对象还是原型中,如果存在对象或者原型中，则返回true,否则false




# 5. 原型

在创建构造函数的时候，解释器会为其添加一个prototype属性，用来指向一个对象，通过构造函数创建的对象共享这个对象的属性和方法，这种模式成为原型模式。所有通过构造函数创建的对象都能访问原型的属性和方法，但是当set的时候，解释器会在对象上创建属性，而不是去修改原型对象属性的值。每个原型对象
都有一个constuctor属性指向这个构造函数。一些浏览器为对象添加了__proto__属性，迎来访问原型对象。

**当我们通过prototype属性修改了构造函数的原型,那么之后通过构造函数生成的对象的__proto__属性将指向这个新的原型对象，而之前创建的对象的__proto__属性指向之前的原型对象,并且之后创建的构造函数生成的对象在访问constructor属性的时候，将不指向这个构造函数**


**所以判断一个对象是什么类型的时候，最好使用instanceof方法。而不是通过constructor属性，因为这个属性是原型对象的属性，原型对象的constructor可能会被修改**


**基于原型模式，当我们需要创建对象的共享属性的时候，最好把这些属性定义在原型上，而当我们创建的对象不共享一些属性的时候，将这些属性定义在构造函数中。但这样也存在一个问题就是不能通过构造函数生成的对象，对原型中共享属性的值进行set,因为set的时候，并不是修改原型对象上的属性，而是将这个属性添加到了对象上,修改这个对象上对应属性的值。如果要修改共享属性的值，需要通过原型对象进行修改**







