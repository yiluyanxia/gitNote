## ++ECMAScript 6++ 

es6标准的代码
```
const obj = (obj => obj + 1);
```
经过转码之后，转换成es5

```js
var obj = function obj(_obj) {
  return _obj + 1;
};
```

## ++let const++

let、const只在代码块中有效。

```
{
    let i = 0;
}
console.log(i); // i is undefined

```

## ++解构++
数组的解构赋值是按次序赋值。   
完全解构

```js
let[a,b,c] = [1,2,3]
```
 
不完全解构  
右边的多于左边

```js
let[a,b] = [1,2,3]
```
对象的解构赋值  
而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

```
let { foo: baz } = { foo: "aaa", bar: "bbb" };
baz // "aaa"
foo // error: foo is not defined
```
对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者

字符串赋值

```
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```

## ++字符串的扩展++
没看--

## ++正则的扩展++

es5的都看不懂  就想看es6了？！

## ++数值的扩展++

二进制 --> 0b \ 0B  
八进制 --> 0o \ 0O  
十六进制 --> 0x \ 0X

ES6 在Number对象上，新增了Number.isFinite()和Number.isNaN()两个方法。  
ES6 将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变。  
Number.EPSILON的实质是一个可以接受的误差范围  
Math对象上新增17个与数学相关的方法。  
Math.hypot方法返回所有参数的平方和的平方根。（勾股定理）  
JavaScript 所有数字都保存成64位浮点数，这决定了整数的精确程度只能到53个二进制位。大于这个范围的整数，JavaScript 是无法精确表示的，这使得 JavaScript 不适合进行科学和金融方面的精确计算。

## ++函数的扩展++

### 箭头函数
ES6 允许使用“箭头”（=>）定义函数  
下面的两个函数相等

```
var f = v => v;

var f = function(v) {
  return v;
};
```
如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。

```
var sum = (num1, num2) => { return num1 + num2; }

```
由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

```
var getTempItem = id => ({ id: id, name: "Temp" });
```
this指向的定义域需要注意！  

函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。（不太理解）  
this对象的指向是可变的，但是在箭头函数中，它是固定的。  
由于箭头函数没有自己的this，所以当然也就不能用call()、apply()、bind()这些方法去改变this的指向。

？函数的尾递归 （不太明白） 

ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）


## ++数组的扩展++

扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。  
如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错

```js
const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]
```
下面的会报错

```js
const [...butLast, last] = [1, 2, 3, 4, 5];
// 报错
```

数组实例的 copyWithin()


```
Array.prototype.copyWithin(target, start = 0, end = this.length)
```
target（必需）：从该位置开始替换数据。  
start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。  
end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。  
负数是这样对应的  
[-5, -4, -3, -2, -1]  
[1, 2, 3, 4, 5]
```js
[1, 2, 3, 4, 5].copyWithin(0, 3)
// [4, 5, 3, 4, 5]
```

## ++对象的扩展++

## ++Symbol++

看的莫名其妙。。。

ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

## ++Set和Map数据结构++

因此使用 Set 可以很容易地实现并集（Union）、交集（Intersect）和差集（Difference）。

扩展运算符...和set()、map()搭配使用效果更佳。

## ++Proxy++

代理，代理器。  
此对象有多个方法，用到时再查！！— —

## ++Promise++

一个对象，很重要，以后再补充。

## ++iterator++
好困 不看了
