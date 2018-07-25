## Ajax
ajax是什么？  
异步JavaScript和XML--mozilla  
异步 js的xml请求  
js创建xml请求对象，向服务器发送http请求，服务器逻辑代码进行响应，最终将响应数据传回前端js代码的回调函数内

## 同步和异步
说一下同步和异步的区别  
多深？要到操作系统级别还是到cpu级别，还是到线程级别？

那就是同步的代码会发生阻塞，代码运行的线程运行到那句话后需要等待响应后才返回函数值，并继续运行。  

异步的代码可以理解是非阻塞的，主线程并不会停止在函数调用内，而是相当于创建了一个后台的线程去完成，等待完成后通知主进程返回函数值，异步的代码一般存在回调的事件，比如回调函数，主线程是被通知后才会进行函数返回值的处理

## js处理小数点会有误差，请问如何处理小数点呢？

心中一万只草泥马奔腾而过，为什么要处理小数点呢？直接使用整数计算，得到的结果在加上小数点啊。但是这个函数我忘记了 --。

## ElementUI把页面分成几个部分？

OMG,就在刚刚我谷歌一下，我都不知道哦！

## Css3新增哪些内容？

![]()

这么多谁记啊！（手动捂脸）



## Vue中V-if和V-show,哪个更耗性能，以及区别？

V-if更耗性能，区别嘛等我搜一下~

v-if 是'真正的'条件渲染,因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建.

v-if 也是惰性的,如果在初始渲染时条件为假,那么什么都不做- - 直到条件第一次为真的时候才会开始渲染条件块,相比之下,v-show就简单得多- - 不管初始条件是什么,元素总会被渲染,并且只是简单的基于css进行切换.

一般来说,v-if 有更高的切换开销,而 v-show 有更高的出事渲染开销.因此,如果需要非常频繁的切换,那么使用v-show好一点;如果在运行时条件不太可能改变,则使用v-if 好点.

（手动滑稽）~，其实抄完了我也记不住。

## 使用图表是时，哪些地方会消耗性能？

性能取决于很多因素，如库的大小，渲染时内存使用量，垃圾回收以及[浏览器重绘的时钟周期数](http://paulirish.com/2011/viewing-chromes-paint-cycle/)。

频繁的 DOM 操作。

待补充~

## 如何初始化地图？

不会~

以前用过高德地图Amap

是这样使用的

```html
<!-- index.html -->
<script type="text/javascript" src="http://webapi.amap.com/maps?v=1.3&key=MyKey"></script>
<script src="//webapi.amap.com/ui/1.0/main.js"></script>
<link rel="stylesheet" href="https://cache.amap.com/lbs/static/main.css"/>
```

```vue
<template>
<div class="maptestpage">
  <div id="container" class="mymap"></div>
</div>
</template>

<script>
import AMap from 'AMap'
import AMapUI from 'AMapUI'

export default {
  props: ['myparklot'],
  data() {
    return {
      parkLotArr: this.myparklot,
    }
  },
  computed: {

  },
  methods: {
    initAMap() {
      let _this = this
			var parkLotArr = _this.parkLotArr
      var map = new AMap.Map('container', {
        zoom: 17,
        center: [108.279707, 22.870326]
      });
      AMap.plugin(['AMap.ToolBar', ], function() {
        map.addControl(new AMap.ToolBar())
      });
      AMapUI.loadUI(['control/BasicControl'], function(BasicControl) {
        map.addControl(new BasicControl.Zoom({
          position: 'rb'
        }));
      });
      //……
      //这里还有一堆函数，删掉了--
      //……
      map.setFitView();
    },
  },
  mounted() {
    this.initAMap();
  }
}
</script>
<style>
.mymap {
  width: 800px;
  height: 500px;
  margin: 50px auto;
}
</style>

```

现在再问我如何初始化，我还是不会（手动捂脸）

## 使用媒体查询时，是大于还是小于？

用过Bootstrap，用的是大于。

```css
/* 超小屏幕（手机，小于 768px） */
/* 没有任何媒体查询相关的代码，因为这在 Bootstrap 中是默认的（还记得 Bootstrap 是移动设备优先的吗？） */

/* 小屏幕（平板，大于等于 768px） */
@media (min-width: @screen-sm-min) { ... }

/* 中等屏幕（桌面显示器，大于等于 992px） */
@media (min-width: @screen-md-min) { ... }

/* 大屏幕（大桌面显示器，大于等于 1200px） */
@media (min-width: @screen-lg-min) { ... }
```

我认为，是用大于还是小于，是看需求的。如果是移动设备优先，则使用大于。如果是以pc端为主，则使用小于。这只是个人在实际应用当中，得出的小建议，并不是标准。

## post和get的区别？

容我搜索一下~

**GET和POST长度的限制问题**

GET

1.GET是通过URL提交数据，因此GET可提交的数据量就跟URL所能达到的最大长度有直接关系。 

2.实际上HTTP协议对URL长度是没有限制的；限制URL长度大多数是浏览器或者服务器的配置参数

POST

1.同样的，HTTP协议没有对POST进行任何限制，一般是受服务器配置限制或者内存大小。

2.PHP下可以修改php.conf的post*max*size来设置POST的大小。

**请求header的content-length问题**

如果有人恶意伪造content-length很大的包头，但实际上发送content-length很小的请求，这样服务器会一直干等，直到超时。当然服务器是可以通过设置来避免该问题的

**GET和POST的安全性**

1.GET是通过URL方式请求，可以直接看到，明文传输。

2.POST是通过请求header请求，可以开发者工具或者抓包可以看到，同样也是明文的。 3.GET请求会保存在浏览器历史纪录中，还可能会保存在Web的日志中。

**GET和POST对服务器的状态**

根据http的设计，大家在看到get的时候，都期望这个请求对服务器没有修改，看到post的时候，都认为这对服务器产生了修改。

**GET幂等，POST不幂等**

幂等是指同一个请求方法执行多次和仅执行一次的效果完全相同。

1.按照RFC规范，PUT，DELETE和安全方法都是幂等的。虽说是规范，但服务端实现是否幂等是无法确保的。

2.引入幂等主要是为了处理同一个请求重复发送的情况，比如在请求响应前失去连接，如果方法是幂等的，就可以放心地重发一次请求。这也是浏览器在后退/刷新时遇到POST会给用户提示的原因：POST语义不是幂等的，重复请求可能会带来意想不到的后果。

3.比如在微博这个场景里，GET的语义会被用在「看看我的Timeline上最新的20条微博」这样的场景，而POST的语义会被用在「发微博、评论、点赞」这样的场景中。

以上是引用。。。。

。。。。手动分割。。。。

## post得到的用户信息存在哪里？

localStorage、sessionStorage  一点都不专业--。。。

post请求服务器，一个请求体是通过文本传输的啊，“文本”内包含了所有请求信息，包括“body”，服务器收到请求后就会解析这个“文本”，服务器运行的代码要有实现http服务端的代码，在nodejs里面叫做“http”模块，在java里面叫做 javaee框架的severlet，服务器响应的东西是传输给浏览器的，浏览器引擎解析响应，展现，如果是ajax 那么这个请求被浏览器引擎解析的同时，js代码会读取这个解析结果，将内容放入回调函数的上下文，也就是回调函数的res变量。

。。。。

还有一些忘记了~

## 如何解决浏览器兼容性的问题。

*虽然我现在很庆幸我不需要处理浏览器兼容性问题，但是还是贴一下曾经用过的，不是很全。*

1. 重置样式（感觉不算兼容性问题）  
因为各大浏览器厂商为了保持自己的特色，默认样式均不一样，根据自己的需要写重置样式是十分必要的。  
2. html5shiv.js
解决 ie9 以下浏览器对 html5 新增标签不识别的问题。


```html
<!--[if lt IE 9]>
  <script type="text/javascript" src="https://cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
<![endif]-->

```
3. respond.js
解决 ie9 以下浏览器不支持 CSS3 Media Query 的问题。

```html
<script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
```
4. hack
为特定版本的ie浏览器写专门的样式，

浏览器 | 标识
---|---
ie6 | _
ie7/ie6 | *
ie8以下 | \9

5. 浏览器内核前缀  
-o-transform:rotate(7deg); // Opera  
-ms-transform:rotate(7deg); // IE  
-moz-transform:rotate(7deg); // Firefox  
-webkit-transform:rotate(7deg); // Chrome  
transform:rotate(7deg); //标准写法  

*面试的时候问到这样的问题  我基本上不想去啦 ，而且对方当时害需要会熟练使用vue,那还搞什么兼容啊 感恩现在开明的领导*

## 如何水平居中div
1. 自动外边距

```
.box{
    margin: 0 auto
}
```
2. flex布局

```
.box{
    display: flex
}

```




## CSS的优先级如何处理

## position有哪些值，分别有哪些作用？

## 如何使用rem做移动端适配

## ES6有哪些新特性

## 如何看待flex布局？（解释功能以及应用方式）

## localStorage有什么作用，如何读写localStorage？