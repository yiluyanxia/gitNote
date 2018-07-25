## 安装环境
node 6.9.x 和 npm 3.x.x 以上
全局安装 Angular CLI 


```
npm install -g @angular/cli
```


## 创建新项目
运行下列命令来生成一个新项目以及应用的骨架代码

```
ng new my-app
ng new my-app --skip-install  // 先跳过npm安装
ng new my-app --skip-install  --style=scss  //样式使用scss

```


## 启动开发服务器
进入项目目录，并启动服务器  
使用--open（或-o）参数可以自动打开浏览器并访问http://localhost:4200/
```
cd my-app
ng serve --open
```

## 生产环境编译

```
ng build
ng build -prod
```
-prod 会进行代码的优化


## 保持应用不断转译和运行

```
npm start
```

## router route 傻傻分不清楚
Router 路由器
Route 路由（线路 vt 及物动词）


## 执行流程
执行ng server 后，进入main.js入口文件，再找到app.module.ts,

app.module.ts 这个根模块会告诉Angular如何组装该应用

```js

//这个根模块会告诉 Angular 如何组装该应用


//引入模块

import { BrowserModule } from '@angular/platform-browser'; //*BrowserModule，浏览器解析的模块*/
import { NgModule } from '@angular/core';  /*核心模块*/

import { AppComponent } from './app.component';
import { HeaderComponent } from './components/header/header.component';  /*自定义的模块*/


/*@NgModule装饰器将AppModule标记为 Angular 模块类（也叫NgModule类）。
 @NgModule接受一个元数据对象，告诉 Angular 如何编译和启动应用。*/

@NgModule({
  declarations: [    /*引入当前项目运行的的组件  自定义组件都需要引入并且在这个里面配置*/
    AppComponent, HeaderComponent
  ],
  imports: [  /*当前的项目依赖哪些模块*/
    BrowserModule
  ],
  providers: [], /*定义的服务  回头放在这个里面*/
  bootstrap: [AppComponent]   /*默认启动那个组件*/
})


/*根模块不需要导出任何东西，   因为其它组件不需要导入根模块。 但是一定要写*/

export class AppModule { }

```
## 创建组件

```
//直接创建文件，并在根组件配置
ng g component components/heaer

ng g c core/sidebar --spec=false  //在core文件夹中创建sidebar组件,不要spec.ts文件


```
## 创建服务

```
 ng g service services/storage
```

## 创建模块

```
ng g m core
```



## 定义属性


```js
export class NewsComponent implements OnInit {
  title ="你个南瓜米";  /*属性*/
  msg:any;  /*另一种定义属性的方式*/
  public username = "kris wu";

  constructor() { 
    this.msg='一脚踩死你'
  }

  ngOnInit() {
  }

}
```
ts当中的声明方式：  
public 公有（默认），可以在这个类里面使用，也可以在类外面使用  
protected 保护类型  只有在当前类和子类里面可以访问  
private  私有，只有在当前类才可以访问这个属性  


## ng指令
*ngIf
```html
<div *ngIf="flag"> flag = true 时显示
</div>

<button (click)='flag=!flag'>改变flag</button>
```

## ng父子组件传值
###  父组件传++值++给子组件

父组件

```html
<!--home.component.html-->
<app-header [msgFromHome]="msgFromHome"></app-header>

```
```js
//home.component.ts
public msgFromHome="this is from home's msg";

```

子组件

```html
<!--header.component.html-->
<div class="header">
  <h3>this is header,and this message " {{msgFromHome}} " is from home;</h3>
</div>

```

```js
//header.component.ts
import { Component, OnInit, Input } from '@angular/core';
@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.css']
})
export class HeaderComponent implements OnInit {
@Input() msgFromHome:string; //通过Input接收父组件传过来的msg
  constructor() { }

  ngOnInit() {
  }
}
```

###  父组件传++事件++给子组件

父组件

```html
<!--home.component.html-->
<app-header [run]="run"></app-header>

```
```js
//home.component.ts
run(){
    alert("this is from home's event.")
  }

```

子组件

```html
<!--header.component.html-->
<div class="header">
  <h3>this is header</h3>
  <button (click)="run()">点我</button>
</div>

```

```js
//header.component.ts
import { Component, OnInit, Input } from '@angular/core';
@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.css']
})
export class HeaderComponent implements OnInit {
   
  @Input() run;  //通过Input接收父组件传过来的事件
  constructor() { }

  ngOnInit() {
  }
}
```



### 从事件中子组件传值给父组件
好乱。。。

父组件

```html
<!--home.component.html-->
<app-header  [getDataFromChild]='getDataFromChild'></app-header>

```
```js
//home.component.ts
getDataFromChild(childData){
    alert("从事件中接收子组件的数据"+childData)
  }

```

子组件

```html
<!--header.component.html-->
<div class="header">
  <h3>this is header。</h3>
  <button (click)="sendParent()">点我</button>
</div>

```

```js
//header.component.ts
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-footer',
  templateUrl: './footer.component.html',
  styleUrls: ['./footer.component.css']
})
export class FooterComponent implements OnInit {
  @Input() getDataFromChild;
  public childInfo="this is from child footer info. "
  constructor() { }

  ngOnInit() {
  }

  sendParent(){
    this.getDataFromChild(this.childInfo);
  } 

}

```

### 子组件通过Output来执行父组件的方法
更乱。。。

父组件

```html
<!--home.component.html-->
<app-header (toparent)="getList($event)"></app-header>

```
```js
//home.component.ts
getList(e) {
  console.log(e)
  console.log("点击子组件的按钮就能看见我")
}

```

子组件

```html
<!--header.component.html-->
<div class="header">
  <h3>this is header</h3>
  <button (click)="getHttpList()">点我加载父组件的数据</button>
</div> 

```

```js
//header.component.ts
import { Component, OnInit, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.css']
})
export class HeaderComponent implements OnInit {
@Input() msg:string; //通过Input接收父组件传过来的msg

@Output() toparent = new EventEmitter() //toparent为自定义

  constructor() { }

  ngOnInit() {
  }
  //定义一个方法，并广播出去。
  getHttpList(){
    //调用父组件的方法请求数据
    this.toparent.emit("这是子组件的值");
  }
}

```


### 子组件传值给父组件
父组件

```html
<!--home.component.html-->
<app-header #header></app-header>
<button (click)="header.childToParent()">父组件home的按钮</button>
<button (click)="getChildToParent()">通过方法获取子组件的数据</button>

```
```js
//home.component.ts
import { Component, OnInit, ViewChild } from '@angular/core';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {
 
  
  @ViewChild('header') headerChild; //'header'就是在html里的定义的名字。
  constructor() { }

  ngOnInit() {
  }
  
  //通过方法获取子组件的数据
  getChildToParent(){
    this.headerChild.childToParent();
    alert(this.headerChild.childVal);
    this.headerChild.childVal="父组件改变了子组件的值"
  }

}


```

子组件

```html
<!--header.component.html-->
<div>
  <p>childVal:{{childVal}}</p>
</div>


```

```js
//header.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.css']
})
export class HeaderComponent implements OnInit {
  public childVal='我要被改变了';
  
  constructor() { }

  ngOnInit() {
  }

  //子组件传值给父组件
  childToParent() {
    alert("childToParent,子组件传值给父组件")
  }
}

```
