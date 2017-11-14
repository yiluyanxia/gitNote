## ++1.变量++

### 变量的定义

$后面加上名字  
$a

### 变量的赋值

$a = 8;

### if  else

*语法部分同js*

### while循环
while(){
    
}

### foeach

数组的遍历


## ++2.表单与后台的操作++

前端与后端的连接


```html
<form method="post" action="board.php"></form>
```

### 生成一个文件

```php
file_put_contents("data.txt",$title.",".$content."\n",FILE_APPEND);
```
### 获取一个文件

```php
file_get_contents("data.txt");
```

## ++3.phpMyAdmin++

高版本wamp使用mysqli连接数据库

## ++4.语法++
php文件中sql语句的字段是使用“·”  
（esc下边的）  
一定要写分号“;”

## ++5.调试++
使用die()，下边的语句都不会执行，方便定位错误。  
exit()

## ++6.报错怎么办++

一般线上产品都会在代码开头写  
error_reporting(0);  

## ++7.连接数据库++

mysql_connect()低版本php可以使用（php 5.6.0以下可用）

高版本使用mysqli()  或者PDO mysql
