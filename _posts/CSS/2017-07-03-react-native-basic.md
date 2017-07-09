---
layout: post
title:  "react-native basic"
date:   2017-07-03 17:00:00
author: wangjiajiajohn
categories: react-native学习笔记
tags: react-native basic
---


### react native  basic

## 1. props

很多component可以根据传入不同的参数进行自定义。这些传入的参数，对于react中的component来说，我们称之为props,每个参数称为prop.

```javascript

class MyCompnent extends Component {
	
render () {
    return  <View>
      <Image source={{url: 'http://www.baidu.com/images/text.png'}}></Image>
      <Text>{this.props.name}<Text>
   </View>
 }

}

```

props说白了就是我们在创建component的时候传入的参数的集合,在react component中，它是constructor函数的参数,每个constructor中，第一句都应该是`super(props)`,我们在component中可以通过this.props[属性名]获取传入的参数。

在react中，不鼓励component修改自身的props,只有父component适合修改子component的props,因为其代表了创建component的状态。


## 2.  State


在 react component中,有两中类型的数据控制component。一个是props,一个是state。

props在component的整个生命周期内是不应该变得。而state是在整个component生命周期里可以随时变化的。当component通过this.setState()方法修改state时,react-native就会重新绘制component。

state应当在component的constructor中定义。

```javascript

class MyComponent extends Component {
	
contructor(props){

super(props);

this.state = {name: wangjiajiajohn};

setTimeout(()=>{
	this.setState({name: "王佳佳"})
},4000)

}

}

```


## 3.  Style

在react中我们不需要使用特殊的语言和语法为component书写样式。每个Component都接受一个称为style的prop,我们在创建子组件的时候，通过style prop为子组件传入样式。react中的样式通常和web中的css一样，除了在react中使用驼峰书写属性名。如果传入的额style是个style数组，则最后一个样式优先。


```javascript

class MyConponent extend Component {
	
 render(){
   return <Text style={styles.red}>style example</Text>
 }

 var styles = StyleSheet.create({

   red: {

   color: 'red';

   }

 })
}

```


## 4.  Height and  Width

component的width和height决定了组件在屏幕上的尺寸大小。

react中存在两种决定component大小的方式。

* Fixed Dimensions

  在创建组件的时候，由其父component在style中指定子component的width和height的大小。

  在react native中,width和height中都是没有单位的,因为使用的是独立像素密度。

  比如: 

```javascript

 <View style={{width:50, height:100,backgroundColor: 'red'}}></View>

 ```

* Flex Dimensions

  Flex的意思就是,子component根据父component的可剩余空间，进行一个按比例放大和缩小。

  一般的情况下,每个component的flex设置为1,这样所以的子component等比例放大缩小。

  flex设置的越大，这个子component放大或者缩小的比例越大。

   **_只有父component的大小大于0,子component才能会根据自身的flex扩展填充父component可用的空间。如果一个component的width、height、flex都没设置的话,子component就无法伸缩有效使用父component的剩余可用空间_**

  ```javascript

   <View style={{flex:1}}>
    <View style={{flex:1}}></View>
    <View style={{flex:2}}></View>
   </View>

  ```


## 5. layout with flexbox

component可以使用flexbox规则指定component的布局。flexbox可以为component在不同size的设备上提供一致的布局方式。

简单的介绍几个属性.

* flexDirection

 默认值为row,表示当前component的子component横向排列。 还可以取值column,子component将纵向排列。


* justifyContent

  设置子component在水平方向如何排列

  取值: flex-start、center、flex-end、space-around、space-between



* alignItems

  设置子component在垂直方向的排列方式。

  取值: flex-start 、flex-end、center、stretch

  **_只有子component在垂直方向没有固定大小的时候,父component设置的alignItems才有效_**



## 6. Handling Text Input

TextInput 是一个基本的输入component,它提供了两个prop,一个是onChangeText,一个是onSubmitEditing。
它们分别接受一个function。当文本发生变化，或者当提交的时候会出发对应的函数。



## 7. Handing Touches

和mobile app交互主要通过touch。我们可以使用手势的结合，比如单击一个按钮，双击放大一张图片。
react-native提供了很多component处理各种手势,也提供了综合的手势响应系统，允许我们使用先进的手势。在这里我们介绍一个最简单常用的手势component---->Button

* Button

button提供了一个具有单击手势的component。 它提供了一个onPress prop接受点击时的事件函数。


* Touchables

有时Button可能不能满足我们的需求，我们可以使用react native中定义的touchables component去合成我们想要的component.

* Scrolling lists,swiping pages, and pinch-to-zoom

其他常见的手势有捏合、滑动。为了处理这些手势，我们需要学习如何使用ScrollView


## 8. ScrollView

ScrollView是用来组合很多view并且可以上下左右滑动查看内容的component.

我们可以通过pagingEnabled pro设置是否支持分页滑动。

我们也可以通过maximumZoomScale和minimumZoomScale这两个prop设置scollView的可缩放内容的比例。

**_ScrollView适合绘制较小数量的有限size的component。因为scrollView的子component会一次性绘制,不管其有没有出现在屏幕上_**


## 9. Using List Views

List View用于绘制数据列表。react native中存在两种ListView: FlatList、SectionList.

FlatList用于绘制不分区数据，其接受data和renderItem两个prop, data是用来绘制的数据数组, renderItem是用于绘制每条item视图。

SectionList 用于绘制分区数据。其接受sections、renderItems、renderSectionHeader三个主要的props。
sections是分区数据数组。renderItems是用于绘制item的函数，renderSectionHeader是用于绘制分区header的函数。

### 10.  Networking

在mobile app开发过程中，我们需要从服务器上获取数据。在react native中我们使用Fetch实现。

它满足rest api。

Fetch()构造函数接受多个参数，第一个请求的url，第二参数是一个对,用来自定义请求的数据。

比如:

```javascript

Fetch('http://www.baidu.com',{
	method: 'GET',
	headers: {
    'Accept': 'application/json'
   }
})

```

Fetch方法返回一个promise.我们可以使用.then或者.catch捕捉成功的响应数据或者异常error。

它也支持async/await实现同步的功能。





