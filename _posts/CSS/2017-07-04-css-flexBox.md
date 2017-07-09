
---
layout: post
title:  "css学习笔记flexBox"
date:   2017-07-04 17:00:00
author: wangjiajiajohn
categories: css学习笔记
tags: css flexBox
---

### FlexBox

FlexBox是一种新型的css布局方式,它能够让界面的不同尺寸的屏幕上完美的展示,通过按比例填充可用区域、或者按比例收缩防止界面溢出。如果一个元素希望使用flexbox技术布局子元素，需要将这个元素的display属性设置为flex或者inline-flex,这样的话这个元素就称为flex container,子元素称为flex item。

## 1. flex-direction

flex-direction用来表示flex container布局flex item的方向。它具有两个值。

* row、row-reverse

水平方向布局flex item。

在row下:

这种布局方向下,水平方向称为flex container的main axis,左起点称为main start,右终点称为main end。.

垂直方向称为cross axis,上面的起点称为cross start,下面终点称为cross end。

每个flex item的左起点到右终点称为main size.从左向右的距离称为main size.从上到下的距离称为cross size.

在row-reverse下:

水平方向start在右,end在左

* column、 column-reverse

垂直方向布局flex item。

在column下:

这种布局方向下,垂直方向称为flex container的main axis,上起点称为main start,下终点称为main end。.

水平方向称为cross axis,左面的起点称为cross start,右面终点称为cross end。

每个flex item的上起点到下终点称为main size.从上向下的距离称为main size.从左到右的距离称为cross size.

在column-reverse下:

垂直方向start在下,end在上

## 2. flex-wrap

可取值: nowrap(不换行)、wrap(换行)、wrap-reverse(反方向换行)

* wrap

按cross axis从cross start向cross end换行

* wrap-reverse

按cross axis从cross end想cross start换行


## 3. flex-flow

flex-flow是flex-direction、flex-wrap的缩写。

比如: flex-flow: row wrap;

## 4. align-items

可取值: stretch(default)、flex-start、flex-end、center、baseline


align-items用来设置flex item在cross axis方向上如何排列。

* flex-start

flex item根据flex container的flex-direction、flex-wrap的排版结果,将flex item在cross axis方向上向两cross start构成的之间对齐。

* flex-end

flex item根据flex container的flex-direction、flex-wrap的排版结果,将flex item在cross axis方向上向两cross end构成的之间对齐。

* center

flex item根据flex container的flex-direction、flex-wrap的排版结果,将flex item在cross axis方向上居中。

* stretch

将flex item在cross axis方向上伸缩


* baseline

在cross axis方向上,第一行flex item靠齐main cross,每行高度相同，基线对齐,都取最高的元素的height.


## align-content

取值: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch

设置flex item在main cross方向上，如何靠齐。


## justify-content

取值: flex-start | flex-end | center | space-between | space-around | space-evenly

功能和align-content类似，但是jusitify-content多行的时候,





