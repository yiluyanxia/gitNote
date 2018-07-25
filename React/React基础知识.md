## React
使用jsx语法糖

### 什么是语法糖
语法糖就是  
计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用

## JXS
由于JSX更加接近于JavaScript而不是HTML，因此React 使用驼峰命名法来命名各个标签的属性名

组件（components）的组成部分是元素（elements）

## 元素element
```js
function formatName(user) {
  return user.firstName + ' ' +user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);

```
## 组件

### Props

Props是只读的

一个组件

```js
function formatDate(date) {
  return date.toLocaleDateString();
}

function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
             src={props.author.avatarUrl}
             alt={props.author.name} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}

const comment = {
  date: new Date(),
  text: 'I hope you enjoy learning React!',
  author: {
    name: 'Hello Kitty',
    avatarUrl: 'http://placekitten.com/g/64/64'
  }
};
ReactDOM.render(
  <Comment
    date={comment.date}
    text={comment.text}
    author={comment.author} />,
  document.getElementById('root')
);
```

一个组件里嵌套多个组件
```js
function formatDate(date) {
  return date.toLocaleDateString();
}

function Avatar(props) {
  return (
    <img className="Avatar"
         src={props.user.avatarUrl}
         alt={props.user.name} />
  );
}

function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}

function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}

const comment = {
  date: new Date(),
  text: 'I hope you enjoy learning React!',
  author: {
    name: 'Hello Kitty',
    avatarUrl: 'http://placekitten.com/g/64/64'
  }
};
ReactDOM.render(
  <Comment
    date={comment.date}
    text={comment.text}
    author={comment.author} />,
  document.getElementById('root')
);
```
### State
只有在构造器中才能直接给 this.state 赋值  
```js
constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

在其他地方改变state需要使用setState
```js
this.setState({comment: 'Hello'});
```

### 状态异步更新
es6语法对比

```js
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));

this.setState(function(prevState, props) {
  return {
    counter: prevState.counter + props.increment
  };
});
```

## 流程

<Clock/> --> ReactDom.render() --> 构造器 --> render() -(Dom)-> componenDidMount() -(setState())-> tick() -状态改变-> render() --> componenWillUnmount()  --> 计时器停止
