[mongoDB安装教程](http://blog.csdn.net/qq_16313365/article/details/52276975)


### 创建MongoDB的Windows服务
启动服务
### net start MongoDB
停止服务
### net stop MongoDB 


$ mongod        开机
$ mongo         使用数据库
$ mongoimport   导入数据

开机命令：

```
$ mongod --dbpath d:\mongo
```

--dbpath就是选择数据库文档所在的文件夹。


# 好好写写

## 1.插入数据

插入数据
```js
db.student.insert({"name":"xiaoming"});
db.tasks.insert({"topic" : "M33","remark" : "m33不能使用，请尽快修复", "project" : ObjectId("5a5c78c014bd1e55e95d4827"), "executor" : ObjectId("5a5c6c588058285493826793"), "deadLine" : ISODate("2018-01-19T08:53:04.399Z"), "label" : "沟通中", "priority" : 1, "creator" : ObjectId("5a5c6c404b18b2548ecef401"), "createAt" : ISODate("2018-01-19T13:28:34.655Z")})


{ "_id" : ObjectId("5a5d78ba7455297391f6af7e"), "topic" : "L170不能使用", "remark" : "L170不能使用，请尽快修复", "project" : ObjectId("5a5c78c014bd1e55e95d4827"), "executor" : ObjectId("5a5c6c588058285493826793"), "deadLine" : ISODate("2018-01-19T08:53:04.399Z"), "label" : "沟通中", "priority" : 1, "creator" : ObjectId("5a5c6c404b18b2548ecef401"), "createAt" : ISODate("2018-01-19T13:28:34.655Z"), "__v" : 0 }



{ "_id" : ObjectId("5a5dc779165ef67ef32f4e05"), "topic" : "L170新功能添加", "remark" : "L170新功能开发，请尽快完成", "project" : ObjectId("5a5d76a65457a570da88c862"), "executor" : ObjectId("5a5d74cc7d58e6732d4d1a96"), "deadLine" : ISODate("2018-01-19T08:53:04.399Z"), "label" : "沟通中", "priority" : 1, "creator" : ObjectId("5a5d74a881cdac732278a16c"), "createAt" : ISODate("2018-01-19T13:28:34.656Z"), "__v" : 0 }




```

导入数据
```js
mongoimport --db test --collection restaurants --drop --file primer-dataset.json

-db test                        //想往哪个数据库里面导入  
--collection restaurants        //想往哪个集合中导入  
--drop                          //把集合清空  
--file primer-dataset.json      //哪个文件
```




## 2.查找数据

精确匹配

```js
db.student.find({"score.shuxue":80});
```

多条件查询，通过逗号隔开
```js
db.student.find({"score.shuxue":80 , "age":12});
```

大于条件
```js
db.student.find({"score.shuxue":{$gt:50}});
```

或者
```js
db.student.find({$or:[{"age":9},{"age":11}]});
```

排序 1升序；-1降序
```js
db.student.find().sort({"score.yuwen":1});
```

## 3.修改数据

查找名字叫做小明的，把年龄更改为16岁
```js
db.student.update({"name":"小明"},{$set:{"age":16}});
```

查找所有男性，把年龄更改为33岁
```js
db.student.update({"sex":"男"},{$set:{"age":33}},{multi: true});
```

完整替换，不出现$set关键字了
```js
db.student.update({"name":"小明"},{"name":"大明","age":16});
```

## 4.删除数据

删除所有匹配项
```js
db.restaurants.remove( { "borough": "Manhattan" } )
```

删除一个匹配项
```js
db.restaurants.remove( { "borough": "Queens" }, { justOne: true } )
```


# 使用node操控数据库

DAO-->数据访问对象

### 傻傻的分页
limit().skip()

查4条
```js
db.student.find().limit(4)
```

查4条后面的4条
```js
db.student.find().limit(4).skip(4)
```
