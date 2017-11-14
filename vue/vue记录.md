## 报RegExp错误
报RegExp错误，可能是没有定义路由。

## 如何使用sass

```
npm install --save-dev sass-loader
//sass-loader依赖于node-sass
npm install --save-dev node-sass
```
## 如何使用echart.js

```
npm install echarts --save

```

## 使用axios请求本地数据

npm install axios --save

### 方法一：   
将 /data/list.json 放到 src同级的 static 里面  

在 api/index.js 里面这样写 ，封装api

```js
let header = {
     'content-type': 'application/json'
 }
 
// Usetlist  函数名
// params 参数对象
export const Usetlist = params => {
  return axios.get(`/static/data/mainlist.json`,params,{headers:header}).then(res=>res.data)
};
```

在vue文件需要请求的地方写

```js
import { getOrderArr } from '../../api/index'

//调用封装的api

getListApi(){
    getOrderArr().then(res => {
    	this.listQuery = res
    	
	})
},

```

### 方法二：

修改/build/dev-server.js  
在src同级的目录下建data/list.json

```js
var app = express()

//添加的star  
 var appData = require('../data/list.json');
 var apiRouter = express.Router();
 apiRouter.get('/list',function(req,res){
   res.json({
     error:0,
     data:appData
   })
 });
 app.use('/api',apiRouter);
//添加的end
```
在vue页面里面直接写请求路径（也可以封装但是我还没写）

```js
//未封装的api
getList(){
	let url = "/api/list"
	this.$http.get(url).then(response => {
	    // success callback
			 this.listQuery = response.data.data;
			 this.orderList = this.tablePagination(this.listQuery);
			 console.log(this.orderList);

	}, response => {
	    // error callback
	})
},
```

## 表格导出Exel

安装依赖

 npm install -S file-saver xlsx

 npm install -D script-loader
 
新建 src/vender  
将Blob.js和 Export2Excel.js 放入  

　注：如果webpack报解析错误：

　　　　　　在build----webpack.base.conf.js中resolve的alias加入 'vendor': path.resolve(__dirname, '../src/vendor'),
　　　　　　即可解决  
　　　　　　alias是配置别名  

## 使用七牛云存储


template里面的action为上传地址  
action="http://up-z2.qiniu.com"

在 data return 里面  
postData: {
    token: 'your token'
}


```js
 //上传成功后在图片框显示图片
handleAvatarSuccess(res, file) {  
        this.imageUrl ='http://ov6fdarek.bkt.clouddn.com/'+ res.key
        console.log(res)
      }
```
token写在manage-vuejs里  
如何获取token浪费了好多时间  
有空在看看官网！！