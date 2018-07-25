# 和我一起入坑-Angular入门-Angular版的ToDoList
本项目是仿照这个做滴  [ToDoList](http://www.todolist.cn/) 。使用angular实现这个代办事项功能。

## （一） 基本功
入坑前不得先看看文档嘛，[Angular quickstart](https://angular.cn/guide/quickstart) 。
然后开撸~
1. 前置项  
   安装Node ，需要注意版本，node 6.9.x 和 npm 3.x.x。
2. 然后全局安装 [Angular CLI](https://github.com/angular/angular-cli) 。
```
npm install -g @angular/cli
```
3. 创建项目

```
ng new ng-first
```
4. 启动开发服务器

```
cd ng-first
ng serve --open
```
浏览器自动打开 http://localhost:4200/ ，看到了ng的标，是不是好激动 *（手动滑稽）*。
5. 创建组件  
   这个操作会直接创建文件，并在根组件配置。
```
ng g component components/todolist
```
6. 创建服务  
  保持队形，再来一个。
```
ng g service services/storage
```
7. 小试牛刀， 打个招呼
   按照国际惯例，先来问个好！  
   在app.component中插入自定义组件app-todolist，这个名字取决于 todolist.component.ts中selector: 'app-todolist'。

```html
<!--app.component.html-->
<app-todolist></app-todolist>
```
继续，在todolist.component.ts中定义一个变量msg,这种语法是ts的默认套路。 *（手动捂脸，其实我也不太会ts啦）*
```js
//todolist.component.ts
export class TodolistComponent implements OnInit {
  public msg: any = 'Hello World !';

  constructor() { }

  ngOnInit() {
  }

}
```
在todolist.component.html中绑定数据
```html
//todolist.component.html
<h3> {{msg}} </h3>
```

```css
/*todolist.component.css*/
h3{
  text-align: center;
  color:  #369;
}
```
切到浏览器，噔噔噔噔！

![HellWorld](http://note.youdao.com/favicon.ico)


哇咔咔，下面开始进入正题。


<!-- more -->


## （二）html和css部分
这个不重要，不是本文重点，打开控制台抄一抄就好了（*好不要脸呀*）。

这是html,直接复制到todolist.component.html，去掉一些用不到得代码。
```html
<!--todolist.component.html-->
<header>
  <section>
    <label for="title">ToDoList</label>
    <input type="text" placeholder="添加ToDo"/>
  </section>
</header>
<section>
  <h2>正在进行
    <span>1</span>
  </h2>
  <ol class="demo-box">
    <li>
      <input type="checkbox">
      <p>记得吃药</p>
      <a>-</a>
    </li>
  </ol>
  <h2>已经完成
    <span>1</span>
  </h2>
  <ul>
    <li draggable="true">
      <input type="checkbox"checked="checked">
      <p>记得吃饭</p>
      <a>-</a>
    </li>
  </ul>
</section>
<footer>
  Copyright &copy; 2014 todolist.cn
  <a>clear</a>
</footer>
```

这是css样式,直接复制到todolist.component.css，把body的样式复制到src目录下的styles.css。

```css
/*todolist.component.css*/
header {height:50px;background:#333;background:rgba(47,47,47,0.98);}  
section{margin:0 auto;}  
label{float:left;width:100px;line-height:50px;color:#DDD;font-size:24px;cursor:pointer;font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;}  
header input{float:right;width:60%;height:24px;margin-top:12px;text-indent:10px;border-radius:5px;box-shadow: 0 1px 0 rgba(255,255,255,0.24), 0 1px 6px rgba(0,0,0,0.45) inset;border:none}  
input:focus{outline-width:0}  
h2{position:relative;}  
span{position:absolute;top:2px;right:5px;display:inline-block;padding:0 5px;height:20px;border-radius:20px;background:#E6E6FA;line-height:22px;text-align:center;color:#666;font-size:14px;}  
ol,ul{padding:0;list-style:none;}  
li input{position:absolute;top:2px;left:10px;width:22px;height:22px;cursor:pointer;}  
p{margin: 0;}  
li p input{top:3px;left:40px;width:70%;height:20px;line-height:14px;text-indent:5px;font-size:14px;}  
li{height:32px;line-height:32px;background: #fff;position:relative;margin-bottom: 10px;
	padding:0 45px;border-radius:3px;border-left: 5px solid #629A9C;box-shadow: 0 1px 2px rgba(0,0,0,0.07);}  
ol li{cursor:move;}  
ul li{border-left: 5px solid #999;opacity: 0.5;}  
li a{position:absolute;top:2px;right:5px;display:inline-block;width:14px;height:12px;border-radius:14px;border:6px double #FFF;background:#CCC;line-height:14px;text-align:center;color:#FFF;font-weight:bold;font-size:14px;cursor:pointer;}  
footer{color:#666;font-size:14px;text-align:center;}  
footer a{color:#666;text-decoration:none;color:#999;}  
@media screen and (max-device-width: 620px) {section{width:96%;padding:0 2%;}}  
@media screen and (min-width: 620px) {section{width:600px;padding:0 10px;}}  
```

```css
/*src/styles.css*/
body {margin:0;padding:0;font-size:16px;background: #CDCDCD;}
```

复制完之后，页面应该长这样。
![html和css](http://note.youdao.com/favicon.ico)
好了，以上是不必要的前戏 *（手动滑稽）*。

## （三）实现ToDoList的功能
研究 [ToDoList](http://www.todolist.cn/) 上的js源码，大概的逻辑就是用户输入待办事项后，添加一个done属性，默认值为false,表示正在进行；点击完成按钮，done属性变为true,表示已经完。且可以删除。浏览器刷新后，数据仍然存在，因为使用了HTML5的localStorage。

### 添加代办事项的功能

声明todo变量
```js
//todolist.component.ts
export class TodolistComponent implements OnInit {
  public todo: any = ''; 
  public todoList = [];

  constructor() { }

  ngOnInit() {
  }
  
  addTodo(e) {
    let todoObj = {
      todo: this.todo,
      done: false
    }

    if (e.keyCode == 13) {  //表示回车按钮
      this.todoList.push(todoObj);
      this.todo = '';       //清空输入框
    }
  }
}
```

```html
<!--todolist.component.html-->
<header>
  <section>
    <label for="title">ToDoList</label>
    <input type="text" [(ngModel)]='todo' (keydown)='addTodo($event)' placeholder="添加ToDo" />
  </section>
</header>
```
[(ngModel)]是一个Angular语法，用于把todo绑定到输入框中。 它的数据流是双向的：从属性到输入框，并且从输入框回到属性。

到这一步的时候，控制台报错。
解救的办法就是我们必须选择使用FormsModule模块。
```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';  //NgModel lives here

@NgModule({
  
  imports: [
    BrowserModule, 
    FormsModule  //import the FormsModule before binding with [(ngModel)]
  ],
  
})
```
### 循环添加的事项
添加内置指令*ngFor,循环列表。
```html
<h2>正在进行
    <span>{{todoList.length}}</span>
  </h2>
  <ol class="demo-box">
    <li *ngFor="let item of todoList" >
      <input type="checkbox">
      <p>{{item.todo}}</p>
      <a>-</a>
    </li>
  </ol>
```
能看到添加的事项咯。
![ngFor循环列表](http://note.youdao.com/favicon.ico)

### 切换事项完成与否以及删除该事项
绑定changeTodo、deleteTodo事件
```html
  <h2>正在进行
    <span>{{todoList.length}}</span>
  </h2>
  <ol class="demo-box">
    <li *ngFor="let item of todoList;let key = index" >
      <input type="checkbox" (click)="changeTodo(key,true)">
      <p>{{item.todo}}</p>
      <a (click)="deleteTodo(key,true)">-</a>
    </li>
  </ol>
  <h2>已经完成
    <span>{{doneList.length}}</span>
  </h2>
  <ul>
    <li *ngFor="let item of doneList;let key = index" >
      <input type="checkbox" (click)="changeTodo(key,false)" checked='checked'>
      <p>{{item.todo}}</p>
      <a (click)="deleteTodo(key,false)">-</a>
    </li>
  </ul>
```
将添加的事项和已完成的事项分为两个数组，（或者放在一个数组里，然后根据done的值来控制是否显示），但是我觉得分两个比较容易操作。
```js
  public doneList = [];  //再声明一个已完成的数组
  
  deleteTodo(index, done) {
    if (done) {
      this.todoList.splice(index, 1);
    } else {
      this.doneList.splice(index, 1);
    }
  }
  
  changeTodo(index, done) {
    if (done) {
      var tempTodo = this.todoList[index]
      this.doneList.push(tempTodo);
      this.todoList.splice(index, 1);
    } else {
      var tempDone = this.doneList[index]
      this.todoList.push(tempDone);
      this.doneList.splice(index, 1);
    }

  }

```
到此，这个功能就算完成啦~  
等等，刷新页面，欧漏，刚刚输入的事项不见了。  
这个时候，localStorage闪亮登场！！

### 创建StorageService服务

> 为了不再把相同的代码复制一遍又一遍，我们要创建一个单一的可复用的数据服务，并且把它注入到需要它的那些组件中。

在（一） 基本功中第6步，创建服务时，angular-cli已经帮我们生成了一个服务的基本结构。
创建服务，方便在任何地方使用。
```js
//storage.service.ts
export class StorageService {

  constructor() { }
  
  setItem(key, value) {
    localStorage.setItem(key, JSON.stringify(value))
  }
  getItem(key) {
    return JSON.parse(localStorage.getItem(key))
  }

}

```
使用该服务，只需要注入它。
```js
//todolist.component.ts
import { StorageService } from '../../services/storage.service'  //导入服务
...
constructor(private storage: StorageService) { } //注入服务

```
好了，我们就可以轻松愉快的使用它了。

### 将数据存到localStorage
使用this.storage就可以使用封装好的服务。  
每次操作数据后都要存一遍。是不是有点鸡肋~
```js

  addTodo(e) {
    let todoObj = {
      todo: this.todo,
      done: false
    }

    if (e.keyCode == 13) {
      var tempList = this.storage.getItem('todoList');
      if (tempList) {
        tempList.push(todoObj)
        this.storage.setItem('todoList', tempList);
      } else {
        var tempData = []
        tempData.push(todoObj)
        this.storage.setItem('todoList', tempData);
      }
      this.todoList.push(todoObj);
      this.todo = '';
    }
  }
  
  deleteTodo(index, done) {
    if (done) {
      this.todoList.splice(index, 1);
      this.storage.setItem('todoList', this.todoList)
    } else {
      this.doneList.splice(index, 1);
      this.storage.setItem('doneList', this.doneList)
    }
  }
  
  changeTodo(index, done) {
    if (done) {
      var tempTodo = this.todoList[index]
      console.log(tempTodo)
      this.doneList.push(tempTodo);
      console.log(this.doneList)
      this.todoList.splice(index, 1);
      this.storage.setItem('todoList', this.todoList)
      this.storage.setItem('doneList', this.doneList)
    } else {
      var tempDone = this.doneList[index]
      this.todoList.push(tempDone);
      this.doneList.splice(index, 1);
      this.storage.setItem('todoList', this.todoList)
      this.storage.setItem('doneList', this.doneList)
    }
  }

```
### 初始事件
> OnInit接口的钩子方法叫做ngOnInit， Angular在创建组件后立刻调用它。 

我的理解就是，类似于vue中的mounted？

```js
  ngOnInit() {
    this.initTodo();
  }
  initTodo() {
    var todoArr = this.storage.getItem('todoList');
    if (todoArr) {
      this.todoList = todoArr
    }
    var doneArr = this.storage.getItem('doneList');
    if (doneArr) {
      this.doneList = doneArr
    }
  }

```
然后，大功告成！

### 还有页脚的clear按钮


```html
<!--todolist.component.html-->
<footer>
  Copyright &copy; 2014 todolist.cn
  <a (click)="clearData()">clear</a>
</footer>

```


```js
clearData() {
    localStorage.clear();
    this.todoList = [];
    this.doneList = [];
  }
```

### 说在后面的话
还有拖拽排序的的功能，不写了。

完整的项目在这里[GitHub](https://github.com/yiluyanxia/ng-first)。
