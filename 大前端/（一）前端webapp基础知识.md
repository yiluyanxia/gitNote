## 什么是web app
意为基于WEB形式的应用程序，运行在高端的移动终端设备  
使用技术为 HTML5 css3 

## mete标签
 
```html
<meta name = "viewport" content="width=device-width,inital-scale=1,user-scalable=no"></meta>
```
width：设置viewport的值，如device-width是设备宽度  
initial-scale：初始缩放，最好为1  
minimum-scale：最小缩放    
maximun-scale：最大缩放  
user-scalabel：用户能否缩放，一般为no  

## 弹性布局
父元素定义使用弹性布局display:-webkit-flex   
子元素设置缩放比如 flex:num;  
不定宽高水平垂直居中  
```css
justify-content:center;  
align-items:center;  
display:-webkit-flex;  
```

## 框架篇
jQuery mobile  这是ui框架  
hammer.js是一款开源的移动端脚本框架，他可以完美的实现在移端开发的大多数事件，如：点击、滑动、拖动、多点触控等事件。不需要依赖任何其他的框架，并且整个框架非常小，在使用时非常简单。并且hammer.js的兼容性和拓展性非常好，hammer.js主要针对触屏的6大事件进行监听