# Hexo和github-page搭建个人博客
## 安装Hexo
先行软件 -->
Node  
Git

```
$ npm install -g hexo-cli
```


```
$ hexo init <folder>  //新建文件夹并初始化一个项目
$ cd <folder>  //进入文件夹
$ npm install  //安装依赖
```
直接在_post文件夹新建md文件，就是一篇文章了！！！

先行步骤 -->
#### 注册GitHub及使用Github Pages
(改天有心情再记录下)

抄的！！！
> 1. 之前步骤中在Github上创建的那个特别的repo（jiji262.github.io）一个最大的特点就是其m   aster中的html静态文件，可以通过链接http://jiji262.github.io来直接访问。  
> 2. Hexo -g 会生成一个静态网站（第一次会生成一个public目录），这个静态文件可以直接访问。
> 3. 需要将hexo生成的静态网站，提交(git commit)到github上。


```
$ hexo generate  //类似于vue中的npm run build ,不操作也没事！！！
```

```
$ npm install hexo-deployer-git --save

```
修改_config.yml

---
```
deploy:
  type: git   
  repo: git@github.com:yiluyanxia/yiluyanxia.github.io.git  
  branch: master
```
---

直接执行，就完成了！！！！
```
$ hexo deploy
```
