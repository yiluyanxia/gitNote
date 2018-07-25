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

## 使用vue-cli生产项目时chromedriver报错
报错是因为与node5不兼容。可以使用node4.2.2代替（尤说的）  
解决办法：
npm install chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver

---
## **vue父子组件通信**

1. 父组件向子组件传值

```html
<template>
    <div>
        <h2>child子组件部分</h2>
        <p>{{message}}</p>
    </div>
</template>
<script>
    export default{
        props:["message"]
    }
</script>
```

```html
<template>
    <div>
        <h2>父组件部分</h2>
        <child :message="parentMsg"></child>
    </div>
</template>
<script>
import child from './components/child.vue'
    export default{
        components:{
            child
        },
        data(){
           return{
                parentMsg:"hello,child"
            } 
        }
        
    }
</script>
```

2. 子组件向父组件传值

```html
<template>
    <div>
        <h2>child子组件部分</h2>
        <button @click="emitFun"></button>
    </div>
</template>
<script>
    export default{
        methods: {
            emitFun(){
                this.$emit("toParent","toParentData")
            }
        }
    }
</script>
```

```html
<template>
    <div>
        <h2>父组件部分</h2>
        <child @toParent="toFun"></child>
        <!--  weex需要这样写  -->
        <!--  <child @toParent="toFun"></child>  -->
    </div>
</template>
<script>
import child from './components/child.vue'
    export default{
        components:{
            child
        },
        methods:{
            toFun(data){
               console.log(data)
            }
        }
    }
</script>
```
3.兄弟组件传值

```js
//bus.js
import Vue from 'vue';  
export default new Vue()
```

```html
<template>
    <div>
        <h2>1兄弟组件部分</h2>
    </div>
</template>
<script>
import Bus from '@/config/bus.js';
    export default{
        methods:{
            busFun(data){
                Bus.$emit('busListen', '向兄弟组件传递信息');
            }
        }
    }
</script>
```
```html
<template>
    <div>
        <h2>2兄弟组件部分</h2>
    </div>
</template>
<script>
import Bus from '@/config/bus.js';
    export default{
        create(){
            Bus.$on("busListen", target => {
                console.log(target);
            });
        }
    }
</script>
```


---
## **安装报错**
```
npm ERR! path C:\hyxwork\workspace-lpcs4\gasSensor-FE\node_modules\fsevents\node_modules\dashdash\node_modules                                                              
npm ERR! code EPERM                                                                                                                                                         
npm ERR! errno -4048                                                                                                                                                         
npm ERR! syscall scandir                                                                                                                                                    
npm ERR! Error: EPERM: operation not permitted, scandir 'C:\hyxwork\workspace-lpcs4\gasSensor-FE\node_modules\fsevents\node_modules\dashdash\node_modules'                   
npm ERR!  { Error: EPERM: operation not permitted, scandir 'C:\hyxwork\workspace-lpcs4\gasSensor-FE\node_modules\fsevents\node_modules\dashdash\node_modules'                
npm ERR!   stack: 'Error: EPERM: operation not permitted, scandir \'C:\\hyxwork\\workspace-lpcs4\\gasSensor-FE\\node_modules\\fsevents\\node_modules\\dashdash\\node_modules\'',np
m ERR!   errno: -4048,                                                                                                                                                        
npm ERR!   code: 'EPERM',                                                                                                                                                   
npm ERR!   syscall: 'scandir',                                                                                                                                               
npm ERR!   path: 'C:\\hyxwork\\workspace-lpcs4\\gasSensor-FE\\node_modules\\fsevents\\node_modules\\dashdash\\node_modules' }                                                
npm ERR!                                                                                                                                                                    
npm ERR! Please try running this command again as root/Administrator.                                                                                                       
npm ERR! A complete log of this run can be found in:                                                                                                                        
npm ERR!     C:\Users\hyx\AppData\Roaming\npm-cache\_logs\2018-01-23T03_33_39_709Z-debug.log      
```

报此错误一般为操作系统的权限问题，使用管理员身份打开cmd。


