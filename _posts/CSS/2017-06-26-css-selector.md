---
layout: post
title:  "css学习笔记一(选择器)"
date:   2017-06-26 16:00:00
author: wangjiajiajohn
categories: css学习笔记
tags: css  选择器  selector
---

# 选择器

css选择器是通过一组规则选中一组元素，然后通过一组css声明来修改这组元素样式的语法。比如:

 ```javascript

 p {color: red}

 ```
p为选择器,选中所有的p元素,{color: red}为css声明块,将所有p元素的字体颜色修改为红色。


##  1. 基本规则

  css规则由选择器和声明块组成。

  selector {key: value;}

  selector为选择器, key为css属性, value为属性的值,{}中可以有多个key value，通过分号(;)隔开。

  通常value是单个值、或者单个关键字。当value是多个关键字的时候，关键字之间通过空格分割。但在font属性中，可以使用斜杠(/)分隔两个值。
  比如:

  ```javascript

  h2  {font: large/150% sans-serif}

  ```
  在这里斜杠分隔了字体大小和行高的两个关键字。



## 2. 元素选择器

使用元素名选中一组元素。比如:

```javascript

 p {color: red}

```
选中所有的p元素，将它们字体颜色改为红色。

## 3.  通配选择器

  使用星号"*"作为选择器，选中文档中所有的元素。比如: `* {color: red}`

  选中所有的元素，将它们的字体颜色都改为红色

## 4. 组选择器

我们可以在一个css规则中，将一块ss声明作用在一组选择器上，只需要使用逗号(,)将这些选择器分隔开即可。

比如:

```javascript

 a ,p  {border-color: red}

```

这样就能将所有的a元素和p元素的边框都设置成红色。


## 5. 类选择器

我们可以通过元素的class类名，选中一组选择器。类名前需要使用点操作符(.),比如:

```javascript

 .red {color: red}

```

这样就能将class为red的所有元素的字体颜色设置为红色。class选择器一般用来为某些相似的元素设置一样的样式。

## 6. ID 选择器

我们可以通过元素的id属性值，选中一组选择器。id属性值前需要使用井号操作符(#),比如:

```javascript

 #red {color: red}

```

这样就能将id属性为red的所有元素的字体颜色设置为红色。id选择器一般用来为某个特定的额元素设置css样式。

## 7. 多类选择器

如果需要为class属性同时满足多个字符串的元素，设置一个特定的样式。我们可以使用多类选择符来选中这些元素。比如:

```javascript

 .warning.error {color: red}

```

这样就能将所有class属性中同时含有warning和error的元素 设置红色字体颜色。


## 8. 属性选择器

属性选择器根据是否使用某个属性，或者某个属性的值是否满足某个条件，来选中一组元素，并为他们设置样式。

用法: 一组规则后加上中括号，中括号里面是属性名，或者属性名和属性值的判断。比如:

```javascript

 a[href][title="test"] {color: red} 

```
这样就能为所有a标签中含有href属性，并且title属性值为test的元素，设置红色的字体。

使用属性值匹配，需要完全匹配才行。比如:

```javascript

 p[class = "warning error"] {color: red} 

```
这一组规则只对class = "warning error"的p元素有效，对class="warning  error"和class = "error waring"都无效。前者多了个空格，后者顺序写反了。


最后我们也可以匹配属性值字符串来匹配元素:

    * [foo ^= "bar"]  选中所有foo属性值字符串以bar开头的元素

    * [foo $= "bar"]  选中所有foo属性值字符串以bar结尾的元素

    * [foo *= "bar"]  选中所有foo属性值字符串中含有bar字符串的元素

    * [foo ~= "bar"]  选中所有foo属性的多个值中含有bar这个值的元素。

    * [foo |= "bar"]  选中所有foo属性值为bar或者以bar开头的元素。


## 9. 使用文档结构--父子关系

   * 后代选择器

    使用空格分割多个选择器，构成后代选择器.

     ```javascript

      h1 em {color: red}

      ```

     这样就选中所有是h1元素后代元素的em元素，将他们的字体颜色设置为红色
 
   * 选择子元素

     有时候并不想选择某个元素的后代元素，而是选择其直接子元素。为了选中父元素下的某个子元素，需要使用大于号(>)。

     ```javascript

      h1 > em {color: red}

      ```

     这样就选中所有是h1元素的直接子元素em元素，将他们的字体颜色设置为红色

   * 选择相邻兄弟元素


     ```javascript

      h1 + p {color: red}

      ```

    这样就选中了所有事h1元素相邻兄弟元素的p元素


## 10. 伪类和伪元素选择器

使用伪类或者伪元素选择器可以为文档中不一定存在的结构指定样式，也可以为某些元素的状态指示的幻象类指定样式。

  * 伪类选择器

   比如:

   ```javascript

   a:visited {color: red} //应用于含有link属性的a标签

   a:link {color: black}  //应用于含有link属性的a标签


   ```

   将所有未访问过的a元素字体设置成黑色。所有访问过的额a元素的字体颜色设置成红色。

  其他伪类:

  ```javascript

  :focus  选中当前拥有输入焦点的元素

  :hover 选中当前鼠标指针停留的那个元素

  :active 选中被用户输入激活的元素  //比如一个a链接，如果用户点击了这个链接，a链接就处于active状态.


  :first-child 选中第一个子元素

  ```

  * 伪元素选择器

  伪元素是为文档中实际不存在，假想存在的元素设置样式。

  比如:

  ```javascript

  p:first-letter {color: red}  //选中p元素的第一个字符

  p:first-line {color: red}  //选中p元素的第一行

  p:before {content:"test"; color: red} 在p元素前插入字符串test,并设置红色字体


  ```

