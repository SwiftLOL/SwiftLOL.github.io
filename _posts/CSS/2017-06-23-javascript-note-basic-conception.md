---
layout: post
title:  "javascript学习笔记一 (基本概念)"
date:   2017-06-23 16:00:00
author: wangjiajiajohn
categories: javascript学习笔记
tags: javascript basic conception
---


### javascript学习笔记一(基本概念)



## 1. 标识符
JavaScript中的标识符用来表示变量、函数、参数的名字,标识符区分大小写,test和Test是两个不同的标识符。

**JavaScript的标识符由字母、数字、下划线_、美元符$组成,且首个字符不能为数字**

## 2. 严格模式
ECMAScript5中引入了严格模式,它能处理ECMAScript3下的一些不确定的行为,对于一些不安全的操作也会抛出错误。

为了引入严格模式,需要在脚本顶部加如下代码: 

`"use strict";`

在函数中也可以指定严格模式:

```javascript
 function example(){
   "use strict";
   console.log('hello world')
 }
```

## 3. 语句
ECMAScript规定语句以一个分好(;)结束，如果在编写代码的时候不加分号，则由解析器确定语句的结尾。为了提高解析速度、便于发布时省略所以空格，最好每条语句都加上分号。

## 4. 变量
变量是通过var关键字声明，声明一个变量的时候如果没有同时赋值，那么这个变量会保存一个特殊值undefined。给变量赋值的时候，并不会指定变量的类型，变量在生命周期内可以保存、改变成任意类型的值。

在一个函数中通过var定义的变量，会成为这个函数的局部变量。如果在非严格模式下省去var定义一个变量，那么这个变量会成为一个全局变量。而如果在严格模式下省去var声明一个变量，那么会抛出一个引用错误。 **_对于一个未声明的变量，只有typeof操作在严格模式下是合法的，返回值为undefined_**.

## 5. 基本类型
ECMAScript定义了6中数据类型，其中除了Object类型之外，其他五种都是基本数据类型。
  1. Undefined
  2. Null
  3. Boolean  
  4. Number
  5. String

为了检查变量的数据类型，我们可以使用typeof操作符,操作变量最好使用小括号括起来。比如:

  ```javascript
  var a = 1;
  console.log(typeof (a))
  ```
输出结果为: number

对数据类型的变量使用typeof之后的返回值为类型的小写。
     *  Undefined    ---    undefined
     *  Boolean      ---    boolean
     *  Number       ---    number
     *  String       ---    string
     *  Null、Object  ---   object
     *  Function     ---    function 

**其实function也是对象,但其确实有一些特殊的属性.使用typeof区分function和object很有必要**

__undefined类型衍生于null类型,所以undefine === null 永远返回true__


## 6. 类型转换

   * Boolean

     Boolean类型存在两个值，true、false.这两个值与数字值不是一回事。true并不是1,false也不是0. 

     其他类型的变量转换成Boolean类型，需要使用Boolean()函数。

     String类型 非空字符串转化为true,空字符串转化为false
     Number类型非0转化为true,0和NAN转化为false
     非null的Object转化为true,否则为false

   * Number

     Number分为整形和浮点型。浮点型的精度为17位。对于任何不含小数部分的数都是整型，比如1.0也为整型。整数的表示有十进制、八进制(0开头)、十六进制(0x开头)。**八进制在严格模式下不可用**。不管什么类型，最终计算的时候都会转化为十进制。

     Number类型的最大数为Number.MAX_VALUE,最小值为Number.MIN_VALUE.当超出这个范围时，变量的值会变成特殊值Infinity,也就是无穷大。-Infinity为负无穷大。我们可以使用isInfinity()函数判断一个变量是不是无穷大。

     ```javascript
     console.log(isInfinity(3e17))
     ```

     NaN为非数值，如果一个函数是用来返回数值的，当返回值不是数值的时候，会返回NaN，NaN和任何值都不想等，包括自己NaN. NaN和其他数据任何的操作都返回NaN.**函数isNaN是用来判断一个值能否转化为数，如果不能返回true**

     **isNaN()函数也适用于对象*首先判断对象的valueOf()函数，如果为NaN,则继续判断函数的toString方法。

     可以使用三个方法将一个值转换成Number类型。Number()、parseInt()、parseFloat()。
     Number()用于任何类型的值转换成整型。parseInt和parseFloat只用于字符串。

     Number()函数在转换类型的时候，如果是false、null、空字符串会转换为0. true转化为1,非空字符串里如果包含非数字的字符则转化为NaN，undefined也会转化为NaN.

     对于parseInt()和parseFloat()在转换字符串的时候，会忽略前面的空格和0，直到第一个不为数字的字符结束。对于空字符串，parseInt和parseFloat都将其转化为NaN。



   * String

     string类型是使用使用单引号或者双引号括起来的字符串，ECMAScript中定义了一些字符字面量，一般用于非打印字符，比如'\n'换行，'\b'空格等等，这些可以用于字符串中表示一些非打印字符。
     **_string类型具有length方法，表示字符串的长度，但是不能准确表达，因为可能其中含有转义字符。length属性表示字符串中字符的个数，并不是将转义字符转化后的个数。_**

     任何变量都可以通过toString()方法转化为字符串。null的值转化为'null',undefined转化为'undefined',true转化为'true',false转化为false.number类型直接返回字符串格式，当然我们在将数字转化为字符串的时候，可以指定转换基数，比如0x十六进行。对于Object，其实就是调用它的toString()方法。

     **NaN、Infinity调用toString()的结果是"NaN"、"infinity"**


##  7. Object类型

Object类型的对象是通过new操作符 后跟构造函数创建而成，如果构造函数中不用传递参数，那么可以省略调用构造函数时的小括号(**但不推荐**)。创建好Object对象之后就可以添加属性和方法了。Object类型中定义的方法在其他对象中都存在。

   * Constructor属性  引用创建当前对象的函数
   * hasOwnProperty(property)用于检查指定的属性是否存在于对象实例中。
   * isPrototypeOf(object)用于检查一个对象是否是另一个对象的原型。
   * propertyIsEnumerable(propertyName)用于检查给定属性是否可以使用for-in语句来枚举。
   * toLocaleString() 返回对象的字符串表示，与执行环境的地区有关
   * toString()
   * valueOf() 返回对象的数值、布尔值、字符串表示。 通常与toString()相同.

## 8. 关系操作符

  相等(==)和不相等(!=)操作符,用来判断两个操作数经过转换之后是否相等。如果两个都是对象则判断是否是同一个对象。如果一个是对象另一个不是对象，则调用对象的valueOf()方法。转换的目的是转换成相同类型进行比较，不一定非得转换成number类型。

  全等(===)和不全等(!==)用来判断两个操作数未经转换前是否相等。


  而对于> >= < <=操作符 则转换成Number类型进行比较


## 9.  加减操作符

Infinity + (-Infinity) = NaN

Infinity - Infinity = NaN

-Infinity - (-Infinity) = NaN


## 10. 位操作符

  Number在内存中是按照64位表示的，负数的表示方法是，取绝对值，之后求反，再之后加1


## 11. for in操作符

  for in 操作对象的时候，用于罗列出一个对象中所有可枚举的属性，包括其原型链上的所有可枚举属性。
  当用于数组的时候，罗列的是元素的索引。










