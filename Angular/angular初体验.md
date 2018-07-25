## 实践从理论开始


看了一点理论感觉和vue一样呀！

### AngularJS 表达式
可以这样

```html
    {{ 5+5 }}
```
也可以这样
```html
<div ng-app="" ng-init="quantity=1;cost=5">
 
<p>总价： {{ quantity * cost }}</p>
 
</div>
```
### AngularJS 指令
ng-app 指令初始化一个 AngularJS 应用程序。  
ng-init 指令初始化应用程序数据。  
ng-model 指令把元素值（比如输入域的值）绑定到应用程序。  
ng-bind 指令把应用程序数据绑定到 HTML 视图。 

### AngularJS 模型
和vue v-model类似。
```html
<div ng-app="myApp" ng-controller="myCtrl">
    名字: <input ng-model="name">
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.name = "John Doe";
});
</script>
```
### AngularJS Scope
View(视图), 即 HTML。
Model(模型), 当前视图中可用的数据。
Controller(控制器), 即 JavaScript 函数，可以添加或修改属性。
当在控制器中添加 $scope 对象时，视图 (HTML) 可以获取了这些属性。
视图中，你不需要添加 $scope 前缀, 只需要添加属性名即可，如： {{carname}}。 

作用域
所有的应用都有一个 $rootScope，它可以作用在 ng-app 指令包含的所有 HTML 元素中。
$rootScope 可作用于整个应用中。是各个 controller 中 scope 的桥梁。用 rootscope 定义的值，可以在各个 controller 中使用。

### AngularJS 控制器
在大型的应用程序中，通常是把控制器存储在外部文件中

```js
angular.module('myApp', []).controller('namesCtrl', function($scope) {
    $scope.names = [
        {name:'Jani',country:'Norway'},
        {name:'Hege',country:'Sweden'},
        {name:'Kai',country:'Denmark'}
    ];
});
```
保存文件为  namesController.js  
然后，在应用中使用控制器文件

```html
<div ng-app="myApp" ng-controller="namesCtrl">

<ul>
  <li ng-repeat="x in names">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>

</div>

<script src="namesController.js"></script>
```
### AngularJS 过滤器

过滤器可以使用一个管道字符（|）添加到表达式和指令中。


过滤器 | 描述
---|---
currency | 格式化数字为货币格式。
filter | 从数组项中选择一个子集。
lowerca | 格式化字符串为小写。
orderBy | 根据某个表达式排列数组。
uppercase | 格式化字符串为大写。
date | 转换时间格式


```html

<!--可以这样-->
<p>总价 = {{ (quantity * price) | currency }}</p>

<!--也可以这样-->
<li ng-repeat="x in names | orderBy:'country'">
    {{ x.name + ', ' + x.country }}
  </li>
<!--还可以这样-->
<p>{{1490161945000 | date:"yyyy-MM-dd HH:mm:ss"}}</p>  
<!--结果是： 2017-03-22 13:52:25-->
```
### AngularJS 服务(Service)
在 AngularJS 中，服务是一个函数或对象，可在你的 AngularJS 应用中使用。

服务 | 描述
---|---
$location | 返回当前页面的 URL 地址
$http | 向服务器发送请求，应用响应服务器传送过来的数据
$timeout | 对应了 JS window.setTimeout 函数
$interval | 对应了 JS window.setInterval 函数

```html
<!--创建名为hexafy 的服务-->
<script>
    app.service('hexafy', function() {
        this.myFunc = function (x) {
            return x.toString(16);
        }
    });
    
    app.controller('myCtrl', function($scope, hexafy) {
        $scope.hex = hexafy.myFunc(255);
    });
</script>

<h1>{{hex}}</h1>

<!--结果是：ff-->

```
### AngularJS XMLHttpRequest
$http 是 AngularJS 中的一个核心服务，用于读取远程服务器的数据

```js
$http({
    method: 'GET',
    url: '/someUrl'
}).then(function successCallback(response) {
        // 请求成功执行代码
    }, function errorCallback(response) {
        // 请求失败执行代码
});

```
$http.get  
$http.head  
$http.post  
$http.put  
$http.delete  
$http.jsonp  
$http.patch  

### AngularJS Select(选择框)
AngularJS 可以使用数组或对象创建一个下拉列表选项。

```html
<!--ng-repeat渲染出来的html,选择的值是一个字符串-->
<select ng-model="selectedSite">
<option ng-repeat="x in sites" value="{{x.url}}">{{x.site}}</option>
</select>

<!--而用ng-options。选择的值是一个对象-->
<select ng-model="selectedSite" ng-options="x.site for x in sites">
</select>
```

### AngularJS 表格
就是一个 ng-repeat 指令和表格一起使用的案例*（手动捂脸）*
```html
<table>
  <tr ng-repeat="x in names">
    <td>{{ $index + 1 }}</td>
    <td>{{ x.Name }}</td>
    <td>{{ x.Country }}</td>
  </tr>
</table>
```

### AngularJS HTML DOM
AngularJS 为 HTML DOM 元素的属性提供了绑定应用数据的指令

- **ng-disabled**

ng-disabled 指令直接绑定应用程序数据到 HTML 的 disabled 属性。

```html
<div ng-app="" ng-init="mySwitch=true">
    <p><button ng-disabled="mySwitch">点我!</button></p>
    <p><input type="checkbox" ng-model="mySwitch">按钮</p>
    <p>{{ mySwitch }}</p>
</div>
```
- **ng-show**  
ng-show 指令隐藏或显示一个 HTML 元素

```html
<p ng-show="true">我是可见的。</p>
```
- **ng-hide**  
ng-hide 指令用于隐藏或显示 HTML 元素。

```html
<p ng-hide="false">我是可见的。</p>
```
### AngularJS 事件
可以用来结合 html DOM一起使用，控制显示和隐藏。
```html
<button ng-click="count = count + 1">点我！</button>
```

### AngularJS 模块
模块定义了一个应用程序。
模块是应用程序中不同部分的容器。
模块是应用控制器的容器。
控制器通常属于一个模块。
- 模板
```html
<div ng-app="myApp">...</div>

<script>
    var app = angular.module("myApp", []); 
</script>
```
- 控制器
你可以使用 ng-controller 指令来添加应用的控制器:

```html
<div ng-app="myApp" ng-controller="myCtrl">
{{ firstName + " " + lastName }}
</div>
<script>
var app = angular.module("myApp", []);
app.controller("myCtrl", function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});
</script>
```
- 指令
- 模块和控制器包含在 JS 文件中
- 函数会影响到全局命名空间
JavaScript 中应避免使用全局函数。因为他们很容易被其他脚本文件覆盖。  
AngularJS 模块让所有函数的作用域在该模块下，避免了该问题。

### AngularJS 表单

```html
<!--数据绑定-->
<input type="text" ng-model="firstname">
<!--复选框-->
<input type="checkbox" ng-model="myVar">
<!--单选框-->
<input type="radio" ng-model="myVar" value="dogs">Dogs
<input type="radio" ng-model="myVar" value="tuts">Tutori
<!--下拉-->
<select ng-model="myVar">
    <option value="">
    <option value="dogs">Dogs
    <option value="tuts">Tutorials
    <option value="cars">Cars
</select>
```
### AngularJS 输入验证

属性 | 描述
---|---
$dirty | 表单有填写记录
$valid | 字段内容合法的
$invalid | 字段内容是非法的
$pristine | 表单没有填写记录

### AngularJS API
API 意为 Application Programming Interface（应用程序编程接口）。


API	| 描述
---|---
angular.lowercase()	| 转换字符串为小写
angular.uppercase()	| 转换字符串为大写
angular.isString()	| 判断给定的对象是否为字符串，如果是返回 true。
angular.isNumber()	| 判断给定的对象是否为数字，如果是返回 true。

### AngularJS Bootstrap
SSI： Server Side Includes
### AngularJS 包含
```html
<body ng-app="">
    <div ng-include="'other.html'"></div>
</body>
```

```html
<!--other.html-->
<p>这是一个被包含的HTML页面</p>
```
默认情况下， ng-include 指令不允许包含其他域名的文件。  
如果你需要包含其他域名的文件，你需要设置域名访问白名单。

### AngularJS 动画
AngularJS 提供了动画效果，可以配合 CSS 使用。
AngularJS 使用动画需要引入 angular-animate.min.js 库。
还需在应用中使用模型 ngAnimate：

```html
<body ng-app="ngAnimate">
```

### AngularJS 依赖注入
wiki 上的解释是：依赖注入（Dependency Injection，简称DI）是一种软件设计模式，在这种模式下，一个或更多的依赖（或服务）被注入（或者通过引用传递）到一个独立的对象（或客户端）中，然后成为了该客户端状态的一部分。
该模式分离了客户端依赖本身行为的创建，这使得程序设计变得松耦合，并遵循了依赖反转和单一职责原则。与服务定位器模式形成直接对比的是，它允许客户端了解客户端如何使用该系统找到依赖
> 一句话 --- 没事你不要来找我，有事我会去找你

*没看懂--*

### AngularJS 路由
http://myweb.com/#/first
http://myweb.com/#/second
http://myweb.com/#/third

因为#号之后的内容在向服务端请求时会被浏览器忽略掉。 所以我们就需要在客户端实现 # 号后面内容的功能实现。