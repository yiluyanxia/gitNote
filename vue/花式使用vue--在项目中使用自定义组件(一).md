## 花式在项目中使用自定义组件
将组件封装好后，在自定义组件的package.json中将入口文件定义好，设置main的值。  
*改天心情好再写一篇如何自定义组件*


```js
  "author": "yiluyanxia <yiluyanxia@163.com>",
  "license": "MIT",
  "main": "dist/yanxia-drag.js",
  "private": true,
```
将这个自定义组件放到项目的node_modules中。
在项目中vue文件写

```html
<yanxia-drag v-model="isShow"></yanxia-drag>
```

```js
import yanxiaDrag from "yanxiaDrag";
export default {
  components: {
    yanxiaDrag
  }
}
```
import yanxiaDrag from "yanxiaDrag";是如何找到node_modules目录下的？

这是Node模块系统的约定和实现。*（抄的）*   
当require/import 的模块不是核心模块，也不是“./”这样的相对路径，就会从当前文件所在目录的node_modules开始找，找不到就到当前目录的上一层node_modules里找直到找到全局的node_modules。  
这样找到的是一个同名的文件夹。这个文件夹里会有一个叫package.json的文件，里面会有一个main字段，npm的取得机制会去找到这个指向的文件，这个文件就是封装好的自定义组件。

*--什么乱七八糟的哈哈哈哈*