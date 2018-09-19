## 读前须知
这个项目是第一次使用Redux的实例，并不具有专业性的理论知识。纯粹分享一次开发过程与心得。之前写了一篇没有加入Redux的[React Native ToDoList](https://segmentfault.com/a/1190000015933522)的小博文。这个项目也是在原来的基础上进行装修完成的。目的是为了体验一下高深莫测的Redux。
总之，在各位网友的友情支持下，我依然没有看懂redux数据流的走向，勉勉强强通了一点。

## （一）拆分结构
根据自己的习惯和固定套路，拆分目录结构和组件结构。
```
├── public
├── todos-redux 
│   ├── actions                             
│   │   └── index.js             
│   ├── components
│   │   ├── todoItem.js
│   │   └── todoList.js
│   ├── containers
│   │   ├── add.js
│   │   ├── all.js
│   │   ├── completed.js
│   │   └── incomplete.js
│   ├── reducers
│   │   ├── index.js
│   │   └── todos.js
│   ├── store                             
│   │   └── configureStore.js 
│   ├── utils                             
│   │   └── utils.js 
│   ├── index.js
│   ├── router.js
```
把react-navigation的导航组件集中放在router.js纯粹是个人习惯。
components中的组件是展示组件，不直接使用Redux。而containers中的是直接使用 Redux的组件。在这里可以看成components是containers的子组件。

## （二）代码实现
### 入口文件
redux-persist是用来做redux的数据持久化。使用方法直接参考在GitHub上的基本示例。这里的代码基本上都是固定套路。
```js
// index.js
import React, {Component} from 'react'
import { Provider } from 'react-redux'
import { TodosReduxStack } from './router'

import { PersistGate } from 'redux-persist/integration/react'
import configureStore from './store/configureStore'
const { persistor, store } = configureStore()
export default class TodolistRedux extends Component {
  render(){
    return (
      <Provider store={store}>
        <PersistGate loading={null} persistor={persistor}>
          <TodosReduxStack />
          </PersistGate>
      </Provider>
    )
  }
}
```
### 创建Action

```js
// action/index.js
import Utils from '../utils/utils'

export const addTodo = (text) => {
  return {
    type: 'ADD_TODO',
    id: Utils.uniqueId(),
    content: text
  }
}

export const toggleTodo = (id) => {
  return{
    type:'TOGGLE_TODO',
    id
  }
}
```

### Reducers
```js
// reducers/todos.js
var initState = [];
const todos = (state = initState, action)=>{
  switch(action.type){
    case 'ADD_TODO':
      return[
        ...state,
        {
          id: action.id,
          content: action.content,
          completed: false
        }
      ]
    case 'TOGGLE_TODO':
      return state.map((t) => {
         if (t.id !== action.id) {
          return t
         } 
         return Object.assign({},t,{completed:!t.completed})
        })
      
    default:
      return state
  }
}

export default todos
```

### 容器组件

connect()() 这个写法叫函数的柯里化，涨知识啦。
```js
// containers/all.js
const mapStateToprops = (state) => {
  return {
    todos: state.todos
  }
}

const mapDispatchToProps = (dispatch) =>{
  return {
    onTodoClick: (id) => {
      dispatch(toggleTodo(id))
    }
  }
}

export default connect(mapStateToprops, mapDispatchToProps)(AllScreen)
```
使用filter函数过滤数组，返回指定的值，这个地方有点鸡肋哈，但是我不会其他的写法了。
```js
// containers/completed.js
const mapStateToprops = (state) => {
  return {
    todos: state.todos.filter(t => t.completed)
  }
}
```
## （三）使用Redux前后对比
没有使用Redux之前，项目使用了React Native内置的DeviceEventEmitter方法。添加事项后要通知其他组件更新数据。还大量使用了AsyncStorage做数据的持久化，每一次的数据更新都需要用到它。如果是在稍复杂的项目中这样写，会死翘翘的！使用Redux 和 redux-persist 可以轻松实现这个功能，效果是明显的。在已完成页面将事项切换为未完成，该事项会直接消失，跑到未完成页面中，这个地方并不需要做额外的处理。

### 说在后面的话
这种连个图都没有也没有深入讲解redux的文字都敢发出来，真的是表脸 *（手动滑稽）*。  
完整的项目在这里[GitHub Todos Redux](https://github.com/yiluyanxia/AwesomeProject)。 