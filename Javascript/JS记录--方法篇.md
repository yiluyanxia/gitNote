## 循环判断

```js
getObj:function(obj){
	let obj_new={};
	for(var o in obj) {
		obj_new[o]=obj[o]||"— —";
	}
		return obj_new;
	},
```

---

## setTimeout
setTimeout第一个参数必须是可执行函数
```js
setTimeout(function(){
    target.style.display = "none";
    }, 1000)
```
---
## Object.assign
Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

```js
const object1 = {
  a: 1,
  b: 2,
  c: 3
};

const object2 = Object.assign({}, object1);

console.log(object2.c);
// expected output: 3
```
