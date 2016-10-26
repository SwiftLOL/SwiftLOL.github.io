---
layout: post
title: CSS--弹性盒
categories: CSS
description: CSS flex box
keywords: CSS、flex box
---

<style type="text/css">
code {color: rgb(135,185,98) !important;}
em {color: rgb(184,92,213) !important;}
</style>

### Overview
  在传统的前端开发中，一直基于盒子模型、position、float对元素进行布局，对于特殊的布局非常的不方便。W3C在2009年提出了flex布局，可以简单、完整、响应式布局。目前所有浏览器都对其进行了支持，可以使用flex特性在任何浏览器上。


### flex
  flex是flex box的缩写。元素的display属性可以设置为flex或者inline-flex，开启弹性盒子特性。我们将每个容器可以看成一个盒子，盒子里的每个元素看成这个盒子的item--项目。使用flex部分特性可以对盒子和项目的布局进行配置。

  每个盒子都由主轴main axis和垂直的交叉轴cross axis组成。主轴的起始点称为main start,结束为止为main end,交叉轴的起始点称为cross start,结束位置为cross end。主轴的起始点到结束点的距离为main size。交叉轴的起始点到结束点的距离为cross size。

### 盒子的特性

#### 1. flex-direction属性
  该属性描述盒子在排列第一维度项目时，是沿着主轴还是交叉轴上布局项目。(在二维空间里，如果换行，会出现二维排列)

  * row  默认值  从左向右
  * row-reverse  从右向左
  * column 从上向下
  * column-reverse  从下向上



####  2. flex-wrap
  该属性描述盒子排列项目时，是否换行，如何换行

  * nowrap 默认不换行
  * wrap 按顺序换行
  * wrap-reverse 按相反方向换行




####  3.flex-flow
  该属性是flex-direction、flex-wrap的简写，默认值为 row nowrap



####  4.justify-content
  该属性描述了项目在主轴上的对齐方式。

  * flex-start  左对齐
  * flex-end  右对齐
  * center    中心对齐
  * space-between 两端对齐，项目之间间隔相等
  * space-around 每个项目等间距，而项目之间的间距是边框和项目之间间距的两倍


####  5. align-item
该属性描述项目在交叉轴上如何对齐。

* flex-start  与交叉轴起始点对齐
* flex-end   与交叉轴的终点对齐
* center     中心对齐
* baseline  与项目的第一行文字对齐
* stretch   默认值，如果项目未设置高度或设置为auto,将在交叉轴上占满空间。


#### 6. align-content
该属性描述当项目出现多行或者多列时，项目在交叉轴上如何对齐

* flex-start  与交叉轴起始点对齐
* flex-end   与交叉轴的终点对齐
* center     中心对齐
* space-between 两端对齐，项目之间间隔相等
* space-around 每个项目等间距，而项目之间的间距是边框和项目之间间距的两倍
* stretch   默认值，项目占满空间


### 项目的特性


#### 1. align-self
该属性描述在交叉轴上如何对齐。对项目使用这个值会覆盖盒子的align-item的特性。默认为auto,即继承盒子的align-item。如果没有父元素，stretch。

* auto    和盒子的align-item属性值相同
* flex-start  与交叉轴起始点对齐
* flex-end   与交叉轴的终点对齐
* center     中心对齐
* baseline  与项目的第一行文字对齐
* stretch   默认值，如果项目未设置高度或设置为auto,将在交叉轴上占满空间。

#### 2. order
该属性描述项目排列时的优先级。数月小，越往前。默认为0

#### 3. flex-grow
该属性描述项目的放大比例。默认为0，不放大。当所有项目的flex-grow都为1时，等比例放大。哪个项目的数值越大，放大的就越大。

#### 4. flex-shrink
该属性描述项目的缩小比例。默认为1，当空间不足时，默认变小。如果设置某个项目的flex-shrink为0，当盒子的空间不足时，其大小不变。


#### 5.flex-basis
该属性描述在分配多余空间时，项目占据主轴上的空间大小。默认为auto,即本来的大小。它可以设置为跟width、height一样的大小，则项目占据固定空间。

#### 6. flex
该属性是flex-grow、flex-shrink、flex-basis的缩写。默认为0 1 auto。系统提供了两个方便值，auto(1 1 auto)和0 ( 0 0 auto)
