# Node进阶

## Node的特定
单线程   非阻塞I/O 事件机制   

单线程   ==》 单线程的好处，减少了内存的开销，操作系统的内存换页。如果某一个时期，进去了，但是被I/O阻塞了，所以这个现场就阻塞了。  

非阻塞I/O ==》不会等I/O语句结束，而会执行后面的语句。非阻塞就能解决问题了么？比如执行着小红的业务，执行过程中，小明的I/O回调完成了，此时怎么办？  

事件机制，事件环，不管是新用户的请求，还是老用户的I/O完成，都将以事件方式加入事件环，等待调度。


```
$ tracert ww.baidu.com
```

环境变量==》在系统的任何目录下，都能运行c:\program files\nodejs里面的程序。

Node就是js的执行环境。
Node没有根目录的概念，因为它根本没有任何的web容器。
让他提供一个静态服务，非常难
相对路径  
url和物理文件是没有关系的！！  
Node就是repl环境
read eval print loop  


## http
Node中将很多功能划分为一个个mudule模块。
使用什么功能就require什么！  
可以提高效率！  
## url
url.parse()

## fs 事件环
for循环里面有异步，这样会输出失败 06_fs.js    
为什么  不知道 好像是for循环太快了  
迭代器就算强行把异步的函数，变成的同步的函数，1做完了再做2；2做完了再做3

## node模块的概念
狭义上来讲，一个js文件就是一个模块，多个模块构成一个功能，这也可以称为广义上的模块。  
模块间使用export暴露出去，使用require引用文件。
require()别的js文件时，将执行那个js文件。
require中的路径，是从当前这个js文件出发，找到别人。所以，桌面上有一个a.js,test文件夹中有b.js、c.js。
a要引用b:
var b = require("./test/b.js");
b要引用c:
var b = require("./c,js");
但是，fs等其他的模块用到路径的时候，都是相对cmd命令光标所在位置。
所以，如果test文件夹，有一个1.txt,那么在b.js中想读这个文件，推荐用绝对路径：

```js
fs.readFile(__dirname + "/1.txt",function(err,data){
    if(err){
        throw err;
    }
    console.log(data.toString());
});
```


## npm共享世界  
不要重复造轮子！！
npm就算一个项目引用别的项目，而这个项目也引用别的项目！！！

## 模板引擎
ejs jade

## express
node的框架，类似于jquery基于js一样！！

### 路由
url不区分大小写  
url中可以使用正则表达式或：(id)来表示未知的参数。  
推荐用：(id)

### 中间件
如果我的get/post回调函数中，没有next参数，那么久匹配上第一个路由，就不会往下匹配了，如果想往下匹配的话，那么需要写next()。


```js
app.get("/",function(req,res,next){
  console.log("1");
  next();
});
app.get("/",function(req,res){
  console.log("2");
});
```

app.use()也是一个中间件。与get/post不同的是，他的网址不是精确匹配的。而是能够有小文件扩展的。比如 hhtp://127.0.0:3000/admin/aa/bb/cc/dd


```js
app.use("/admin",function(req,res){
  res.write(req.originalUrl + "\n");  //  /admin/aa/bb/cc/dd
  res.write(req.baseUrl + "\n");      //  /admin
  res.write(req.path + "\n");         //  /aa/bb/cc/dd
  
})
```


### Cookie和Session
HTTP是无状态协议。简单地说，当你浏览了一个页面，然后转到同一个网站的另一个页面，服务器无法认识到，这是同一个浏览器在访问同一个网站。每一次的访问，都是没有任何关系的。  
Cookie是一个简单到爆的想法：当访问一个页面的时候，服务器在下行HTTP报文中，命令浏览器存储一个字符串；浏览器再访问同一个域的时候，将把这个字符串携带到上行HTTP请求中
Session是特殊的Cookie

### Mongoose
是一个将js与数据库

- 定义模型
创建schema --> 定义一些schema的静态方法 --> 创建模型
创建schema用说明语句？ new mongoose.schema({});
创建模型用说明语句？  db.model("Student",schema名字);


```js
//创建了一个schema结构
var studentSchema = new mongoose.Schema({
    name : {type:String},
    age : {type:Number},
    sex : {type:String}
})
```

```js
//创建静态方法
studentSchema.statics.findFun = function(name,callback){
    this.model('Student').find({name:name},callback);
};
```

```js
//创建修改的静态方法


```

