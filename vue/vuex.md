## vuex流程

核心state

```
graph TD
A[index.js] -->B(getter.js)
B --> C{action.js}
C --> D[mutation.js]
C --> E[mutation-type.js]
```

## 安装

npm install vuex --save-dev

它必须以插件的方式进行引用

import Vuex from 'vuex';  
Vue.use(Vuex);


## 大神指导

1. 流程就是 import store from '..vuex/store'  导入 vuex的 store
2. 然后 store.dispatch('savelogin',data); 
3. 分发状态 dispatch 给actions.js 里的savelogin
4. 通过actions里的savelogin 去触发 store里的mutations里的Slogin
5. 然后 通过Slogin获取到的值 对store里的state 赋值 
6. 这样 你就可以在你需要的地方 通过store.getters.getlogin;来获取数据
7. getters就是getters.js 里的getlogin’


## 再学一次

好像明白了---一点点

state 状态 --> 派生出别的状态 getter   
在显示某些数据前对数据进行处理（getter:store的计算属性）   
所有的状态state 由mutation改变   
action提交的是mutation而不是直接改变state  

---- 这么写  
import mutations from './mutations'

mutations.js里面的内容是    
一个对象  
写在一起！！

```js
expert default{
    //这就是一个函数啊！！[] es6的新语法！！！
    [types.ADD](state){
        state.count++
    },
}
```
---- 这样写  
import * as mutations from './mutations'
里面是一个function  
mutations.js里面的内容是  
就是一个一个声明！一个一个写！！

```js
export const increment = state => {
  state.count--
}
```









