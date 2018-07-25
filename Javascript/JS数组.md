## 数组分类


```js
todolistData:[
    {
      id:1,
      content: "哈哈哈哈哈哈",
      isComplete: true
    },
    {
      id:2,
      content: "呵呵呵呵呵呵",
      isComplete: false
    },
    {
      id:3,
      content: "嘿嘿嘿嘿嘿嘿",
      isComplete: false
    }
],
```

方法一
```js
var list = aa,
    flag = 0,
    data = [];          
for(var i = 0; i< list.length; i++) {
    var az = '';
    for (var j = 0; j < data.length; j++) {
        if(data[j][0].store_name == list[i].store_name) {
            flag = 1;
            az = j;
            break;
        }
    }
    if(flag == 1){
        data[az].push(list[i]);
        flag = 0;
    } else if (flag == 0) {
        wdy = new Array();
        wdy.push(list[i]);
        data.push(wdy);
    }
}
console.log(data);
```
输出

```js
[
  [{
    id: 1,
    content: "哈哈哈哈哈哈",
    isComplete: true
  }],
  [{
      id: 2,
      content: "呵呵呵呵呵呵",
      isComplete: false
    },
    {
      id: 3,
      content: "嘿嘿嘿嘿嘿嘿",
      isComplete: false
    }
  ]
]
```

方法二

```js
for (var i = 0; i < list.length; i++) {
      if (!data[list[i].isComplete]) {
        var arr = [];
        arr.push(list[i]);
        data[list[i].isComplete] = arr;
      } else {
        data[list[i].isComplete].push(list[i])
      }
    }
    console.log(data);

```

输出
```js
[
    {
        true: [{
            id: 1,
            content: "哈哈哈哈哈哈",
            isComplete: true
        }]
    },
    {
        false: [{
            id: 2,
            content: "呵呵呵呵呵呵",
            isComplete: false
          },
          {
            id: 3,
            content: "嘿嘿嘿嘿嘿嘿",
            isComplete: false
          }
        ]
    }
]
```

方法三

```js
var moth = [],
    flag = 0,
    list = aa;
var wdy = {
     title: '',
     sur_name: ''
    }
for (var i = 0; i < list.length; i++) {
    var az = '';
    for (var j = 0; j < moth.length; j++) {
        if (moth[j].title == list[i]['isComplete']) {
            flag = 1;
            az = j;
            break;
        }
      }
      if (flag == 1) {
        var ab = moth[az];
        ab.sur_name.push(list[i]);
        flag = 0;

      } else if (flag == 0) {
        wdy = {};
        wdy.title = list[i]['isComplete'];
        wdy.sur_name = new Array();
        wdy.sur_name.push(list[i]);
        moth.push(wdy);
      }
    }
    console.log(JSON.stringify(moth))

```
输出

```js
[{
    "title": true,
    "sur_name": [{
    "id": 1,
    "content": "哈哈哈哈哈哈",
    "isComplete": true
  }]
},
{
    "title": false,
    "sur_name": [{
    "id": 2,
    "content": "呵呵呵呵呵呵",
    "isComplete": false
  }, {
    "id": 3,
    "content": "嘿嘿嘿嘿嘿嘿",
    "isComplete": false
  }]
}]

```

