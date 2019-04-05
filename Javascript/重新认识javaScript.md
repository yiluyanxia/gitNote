## 类型

JavaScript 中的类型应该包括这些：

Number（数字）  
String（字符串）  
Boolean（布尔）    
Symbol（符号）（第六版新增）  
Object（对象）  
Function（函数）  
Array（数组）  
Date（日期）  
RegExp（正则表达式）  
Null（空）  
Undefined（未定义）  

整数值通常被视为32位整型变量

## 数组特点


```js
var a = ["dog", "cat", "hen"];
a[100] = "fox";
a.length; // 101
```
## this
1. 全局环境
无论是否在严格模式下，在全局执行环境中（在任何函数体外部）this 都指向全局对象。
```js
// 在浏览器中, window 对象同时也是全局对象：
console.log(this === window); // true
// 在 Node 中全局对象是 global
```
2. 函数（运行内）环境
在函数内部，this的值取决于函数被调用的方式。  
在严格模式下，如果 this 没有被执行环境（execution context）定义，那它将保持为 undefined。  

我的理解就是通常情况下this指向当前作用域内的值，如果找不到对应值则向父级查找直到找到为止，如果仍然找不到则指向全局变量（window）。  
