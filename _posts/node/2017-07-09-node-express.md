---
layout: post
title: expess basic
categories: node
description: express 框架api
keywords: node. express
---

# Express API

## 1. express()

express()函数是express模块暴露的顶级API,我们通过以下代码引入express模块.

```javascript

var express = require('express')

```

### express method

#### 1. express.static(root, [option])

这个是内置express里唯一的中间件函数。它是基于serve-static模块的静态文件服务。

root参数用于指定静态文件的根路径。expess根据静态文件的req.url与root比较,当一个文件找不到的时候,并不立即返回404错误,expess而是调用next()把这个请求传递给下一个中间件。


option对象:

* dotfiles

用于控制如何处理文件名以点(.)开头的文件。

三个值: ignore、deny、allow

 * ignore

  当做文件不存在,返回404,之后调用next()

  * deny

   禁止这样的请求,返回403,之后调用next()

   * allow

    正常处理

 * etag
   
 开启或者关闭etag。etag的用途是为文件或者JSON添加一个关联符号,在请求的时候传给服务器,服务器根据根据文件或者JSON的内容有没有发生变化，如果变化了，返回新的数据，如果没变化返回304,告诉客户端数据没变。

 可取值: true、false

 * extensions

 用于设置文件可匹配的扩展名备案。如果一个文件找不到的话,会根据文件名和extensions中的而使用的其他扩展名做为备案继续寻找文件。比如: ['html','htm']

 可取值: false、 ['extensionName1'...]

 * index

 用于设置是否发送指定目录下的index文件。默认值为'index.html'。
 设置为false的话,禁言文件夹index文件。

 * lastModified

 设置是否在响应header里,使用文件最后的修改日期设置last-Modified字段。

 可取值: false、true

 * maxAge

 用于设置响应header里Cache-Control字段,使用毫秒为单位。

 可取值: number

 * redirect

 当pathname为文件夹,自动在尾部添加'/'重定向。

 可取值:  fase、true


 * fallthrough

 可取值: false、true

 当true时,如果一个文件找不到,将会调用next()让下一个中间件处理。
 当设置为false,如果一个文件找不到,将会调用next(err)。


 * setHeaders

 类型: function

 用于设置http 响应header.

 参数为: res、path(将被发送的文件的绝对path)、stat(文件的状态)



#### 2. express.Router([options])

用于创建一个新的Router对象

```javascript

var router = express.Router([options])

```

option对象的属性:

* caseSensitive

是否对path大小写敏感。

* mergeParams

是否保存来自parent router的req.params值。如果有同名的,child router的同名参数优先

* strict

是否严格模式路由。默认disabled,"/foo"和"/foo/"一样。


## 2. Application

app对象被约定为表示express应用程序。它通过调用express模块暴露的顶层APIexpress()创建。

```javascript

var express = require('express')

var app = express()

```

### app对象的属性

#### 1. locals

locals对象用于存储express程序中的本地变量。一旦在locals对象设置一个属性, 那么这个属性在app整个生命周期内都存在。在能访问到app对象的地方,都能通过locals对象访问这些存储起来的数据。

```javascript

app.locals.owner = "wangjiajiajohn"

app.local.ownerEmail = "wangjiajiajohn@gmail.com"


```

#### 2. mountpath

mounthpath变量用于存储sub-app安装在主程序上的path patterns list。

一个app其实就是处理某些业务的程序,所以我们可以创建一个子app处理一些请求。我们可以把这个app安装在多个不同的路径下。子app的mountpath属性返回这个子app被安装在的那些path pattern list上了

```javascript

var express = require('express')

var childApp = express()

var app = express()

app.use(['/ad*m, '/manager'],childApp)

consle.log(childApp.mountpath)


```

### app对象的事件

#### 1. on('mount',callback(parent))

当一个child app被安装在另外一个app上时,child app会收到这个mount事件,并且express会将parent app作为参数传递给child app的回到函数


### app对象的方法

#### 1. all(path, callback[,callback ...])

all方法是用于忽略请求方法,只关注请求path的创建中间件函数的方法。

参数:

* path

path可以是有个path的字符串表示、也可以是一个path pattern、也可以是path 正则表达式、也可以使他们的组合。

* callback

callback可以使一个中间件函数,也可以是以逗号(,)隔开的多个中间件函数,也可以是中间件函数数组,也可以是它们的组合。


callback函数的参数为: req, res, next

通过next()将请求传递给下一个callback。因为这些callback是按照顺序执行的,所以我们可以把一些优先处理的逻辑前置。

#### 2. delete(path, callback[,callback])

类似于all方法,但只处理请求方法为delete的请求。

#### 3. disable(name)

用于禁用app setting table中的某个设置。
比如: app.set('foo', false)

#### 4. disabled(name)

用判断app setting table里某个设置是否已经被禁用。

#### 5. enable(name)

启用app setting table中的某个设置。

#### 6. engine(ext, callback)

用于设置特定的绘制引擎来绘制指定的扩展名文件。当绘制特定扩展名的文件时,express会找到相应的引擎绘制文件。

比如:

```javascript

var engines = require(''consolidate);

app.engine('html', engines.hogan)

```

#### 7. get(name)

返回app setting table中指定名字的设置的值。

比如:

```javascript

app.get('title')

````

#### 8. get(path,callback[, callback ...])


#### 9. listen(port, [hostname], [backlog],[callback])

用于将app绑定到指定主机和端口上。

比如:

```javascript

app.listen(3000)

//对于本机上3000端口的请求,都能到达app上

````


#### 10. param([name],callback)

name为参数名或者参数数组,callback为用来循环处理他们的函数,callback的参数为req,res,next,value,name。value为参数的值。

请求url中只要参数中出现了[name]中的参数,callback都会被触发。在callback中使用next()将控制权传递给下一个参数,如果后面没参数了,则将控制权传递给下一个中间件函数。


主app上定义的param函数,子app不会继承，所以如果一个请求匹配到了子app router上,那么主app上的param函数不会被触发。

如果一个请求url匹配到了多个router上,但并不是每个router都执行一次callback。对于一个name来说,在一次请求响应循环中只执行一次。



#### 11. path()

返回一个app的标准路径。

比如:

```javascript

var app = express()

var child = express()

app.use('/blog',child)

console.log(child.path()) // '/blog'

console.log(app.path()) // ''

````

#### 12. post(path, callback[, callback] ...)

#### 13. put(path, callback[, callback] ...)

#### 14. render(view, [local], callback)

按照指定view(一般是views文件夹下的模板文件),使用这个callback函数和可选local对象中的变量绘制html文件。

比如:

```javascript

app.render('email', function(err, html){
	
})

````

#### 15. route(path)

使用这个方法创建一个单独的route实例,然后为这个route实例添加可用的中间件。

```javascript

app.route('/event')
  .get(function(req, res, next){

  })

````

#### 16. set(name, value)

为app setting table中的名为name的字段的值设置成value

subapp不会继承app中有默认值得setting的值,除了trust proxy

subapp会继承app中没有默认值的setting的值,除了view cache

setting table中的设置:

case sensitive routing  默认值:无 可取值: false,true

env 取值: development 、 production

etag  默认值: weak 

jsonp callback name  默认值: "callback",指定默认的jsonp回到名

json replacer 默认值: 无 一般设置为"JSON.stringfy"

json spaces 默认值:无  一般为"JSON.stringfy"

query parser 默认值: "extended" 用于设置query解析器

strict routing  默认值:无  可取值: false、true

subdomain offset:  默认值:2  设置可访问的子域的级别

trust proxy: 默认值: false 

views: app views的目录或者目录数组 默认: process.cwd() + '/views'

view cache 开启view模板缓存  默认true

view engine 默认的模板引擎 默认:无

x-powered-by 在http header中启用X-Powered-By



#### 17. use([path],callback[, callback])

在app上安装中间件,或者在特定path上安装中间件。如果一个请求的base url 匹配path,那么这个中间件就会被调用。


错误处理的中间件函数的参数一般为err, req, res, next。



