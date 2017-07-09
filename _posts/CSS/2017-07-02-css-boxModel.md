---
layout: post
title:  "css学习笔记五(盒模型)"
date:   2017-07-02 17:00:00
author: wangjiajiajohn
categories: css学习笔记
tags: css box model
---

### 盒模型

html元素代表了页面上一块矩形的区域,就像一个矩形盒子一样,我们将这种绘制方式称为盒模型。

html页面是由一个又一个这样的矩形的盒子,延着x轴自左向右，y轴自上向下,或者延着z轴堆积而成。我们称这种布局方式为可视版式模型---Visual formatting model。

## 1.盒模型

盒模型主要涉及到三个属性, 内边距padding, 边框border, 外边距margin。

* 内边距padding

用来控制边框到内容的距离。padding又可以细化为padding-top、padding-right、padding-bottom、padding-left。通过设置这些值，可以为不同的方向创建不同的内边距。

* 边框border

边框border是用于修饰元素上下左右四条边样式的属性。我们可以为边框设置宽度、样式、颜色。我们也可以细化的使用不同的属性为每条边设置不同的宽度、样式、颜色。

边框border的简写是`border: width style color`, 比如`border: 10px solid red`,通过这种方式可以一次性为四条边设置相同的宽度、样式、颜色。

我们也可以使用一个属性一次性设置四条边的宽度或者颜色或者样式。对应的四个属性是:
  
   * border-color

   * border-width

   * border-style

最后我们也可以使用一个属性单独设置某条边的某个属性。对应的12个属性有:

   * border-left-color (right top. bottom)

   * border-left-width (right top. bottom)

   * border-left-width (right top. bottom)

* 外边距

外边距是矩形区域中边框到矩形区域边界的距离,我们一般通过它来控制元素与元素之间的距离。


## 2. 叠加外边距

元素之间的距离，一般是指边框到边框的距离,根据元素之间的关系、display的属性值以及相邻边距的值,会按照不同的规则计算它们相邻边框之间的距离。  

左右相邻的两个display:inline类型的兄弟元素,在水平方向的距离,等于左元素的右边距+右元素的左边距。因为浏览器在绘制左右相邻的两个元素的时候,它们相邻的外边距的边界会重合。

上下相邻的两个兄弟元素,将下面的元素向上靠近上面元素,当其中一个元素的外边距的边界与另外一个元素的边框对其的时候,就会产生它们之间真实的距离。当上下两边距都为正数的时候,它们边框之间的距离就是最大的正数。当上下两边距都为负数的时候,它们边框之间的距离就是最小的那个负数。当一正一负的时候，取两数之和。


## 3. 盒子的width

元素的宽度一般指的是元素内容区域的宽度,也就是元素的width属性,并不是元素矩形区域的宽度。

对于任何内联元素和指定width属性的块级元素，我们修改元素的border-width、margin、padding都不会影响到width的大小，只会改变盒模型的宽度。而对于width属性为auto的块级元素,修改元素的border-width、margin、padding属性,都会影响到元素的width属性的大小。

inline类型的盒子宽度根据内容的大小变化。而块级元素的宽度根据其父元素的宽度变化，除非指定固定宽度。


## 4. 盒子的高度

盒子的高度







<!-- * border-color 的颜色默认等于元素前景的颜色 也就是元素color属性对应的颜色

* 在正常流中,块级元素的布局依赖于其包含块,就是类型为块级元素、表单元格或者行内块级元素的祖先元素。
  行内元素的布局不依赖于其包含块。

* 正常流: 自左向右、自上向下的文本布局方式。

* 非替换元素: 内容包含出现在文档中的元素。比如p元素

* 替换元素: 作为其他内容占位符的一个元素。比如img元素

* 块级元素: 在正常流中，独自占一行，盒模型前后都换行的元素。

* 行内元素: 在正常流中，不独占一行，盒模型前后不换行的元素。

    **在正常流中块级元素用于生成另起一行的矩形区域,行内元素用于作为块级元素的子元素按照正常流自左向右、自上向下的布局自己的内容**

* 根元素: 位于文档树最顶端的元素，在html文档中指的是html元素.


* 元素的宽度width: 左内边界到右内边界的距离，也就是盒模型中内容的宽度。
  块级元素盒模型在水平方向上会full filled父块级元素的内容区域。
  行内元素盒模型在水平方向的width默认情况下取决于其内容的宽度。

  对于width为auto的块级元素，其盒模型的长度是固定的，改变其内外边距，都会影响其width属性的大小。
  对于width为固定值的块级元素，改变其被外边距，会影响其盒模型的大小。我们可以把行内元素当成块级元素width属性为固定值看待。

* 元素的高度height: 上内边界到下内边界的距离，也就是盒模型中内容的高度。
  块级元素盒模型在垂直方向的大小取决于其内容，如果无任何子元素，其height默认为0。所以body元素初始高度为0。当块级元素内容的高度大于块级元素的height的时候，块级元素会产生一个滚动条。如果小于内容的高度，效果取决于overflow属性.
  行内元素盒模型在垂直方向的大小默认情况下取决于其内容的高度。

* 块级元素的width、margin-left、margin-right默认值为auto

      * 当块级元素width、margin-left、margin-right为auto时,width的大小等于包含块的width.
        margin、margin-left、margin-right为0

      * 当块级元素的width、margin-left、margin-right其中两个为auto时:

           * width margin-left或者width margin-right为auto, margin-left或者margin-right会变为0

           * margin-left margin-right为auto, margin-left   margin-right基于width+margin-left+margin-right+padding-left+padding-right等于包含块的width,平分长度

           * margin-left、margin-right、width其中一个为auto时，基于width+margin-left+margin-right+padding-left+padding-right,
           计算这个值为auto属性的真实值。

              **_margin-left margin-right 均为auto,并且padding-left == padding-right的情况下,块级元素的内容居中_**

              **_如果块级元素的外边距为负,则其width有可能大于其包含块的width_**


  行内元素的width默认为auto, margin默认为0。假如指定了行内元素的width，想居中内容一般使用text-align，因为一般行内元素用于包含文本，除了img。


* 替换元素的width默认为auto，也就是内容的宽度。但加入我们修改替换元素的宽或者高，其高或宽会等比例变化。


* 对于块级元素的height设置百分比，如果其父块级元素的height不是auto，则块级元素的height是其父块级元素height*百分比
  而如果其父块级元素的height为auto，则子块级元素height即使设置了百分比，也会自动变为auto

* 对于正常流中的height为auto的块级元素，假如其只有块级子元素，其height是最上面的块级子元素的外边框边界到最下面块级子元素的外边框边界。

  如果块级元素有上或下内边距,或者上、下边框，其height是最上面块级子元素的上外边界到最下面块级子元素的下外边界。

* 疑问:

  块级元素、行内元素的margin padding width  height默认值是什么，都能设置这些属性吗？
  块级元素 行内元素设置负边距对布局产生什么影响？ 相邻元素重合？
  行内元素如何在块级元素中居中。块级元素如何在块级元素内居中。 水平和垂直居中 ？



* 浮动的元素最垂直方向上  margin不再重叠。



*  html界面布局
   
   在html中,对于position为static的元素,浏览器会将其按照从上到下，从左到右的顺序布局,在水平方向margin不会重叠，在锤子方向，相邻元素的margin会重叠。position不为static的元素门，他们之间的距离与margin无关。而对于浮动的元素，其margin在水平和垂直方向都不会合并。
   对行内元素设置margin，在垂直方向上无意义，如果想让行内元素的margin影响行高的话，可以将其display属性设置为inline-block。
   块级元素的width会根据其父块级元素计算，行内元素的宽根据其内容计算，如果行内元素的width或者块级元素的width是百分比，而父级元素的宽是auto,那么他们的width值会从百分比变为auto。块级元素的宽和高在浮动的情况下，取决于其内容，最好设置其宽度。块级元素和行内元素的高都由其内容决定，除非指定他们的height。



* /path  代表系统绝对路径   ~/path 代表当前用户绝对路径 -->































