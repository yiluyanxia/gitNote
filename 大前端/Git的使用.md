## Git的使用

### git 将本地项目添加到GitHub上

#### 1.在本地项目上右键git bash

```
$ git init //初始化git项目，会生成.git文件
```


#### 2.将项目添加到仓库


```
$ git status //显示是否添加的状态，非必需

$ git add . //“.”表示将所有的添加上去
```


#### 3.将添加的文件提交到仓库上


```
$ git commit -m "注释语句"
```

#### 4.去github上你创建好的仓库复制路径，将本地关联GitHub


```
git remote add origin https://github.com/yiluyanxia/vue-blog-FE.git
```


#### 5.上传github之前，要先pull一下


```
$ git pull origin master //非必须
```


#### 6.上传到GitHub远程仓库


```
$ git push -u origin master //第一次需要输入账号和密码
```


#### 7.完成了！可以去GitHub上查看了！！

### git将项目提交到gh-pages分支上


```
$ git checkout -b gh-pages //切换到gh-pages分支

$ git add -f dist //强制添加dist 因为.gitignore文件中定义了忽略该文件

$ git commit -m "注释语句"

$ git subtree push --prefix dist origin gh-pages //部署dist目录下的代码 （运行时报错了） 非必须

$ git remote add origin https://github.com/yiluyanxia/vue-blog-FE.git

$ git push -u origin gh-pages //提交到远程分支
```

## 将master合并到自己得开发分支上
```js
git commit -a  //在合并前，将自己得代码提交到git.确保合并前远程的git上的代码是最新的。
git checkout master //切换到master主分支上
git pull  //将最新的代码拉取下来到本地。
git checkout hyx  //切换到自己的开发分支
git merge master  //将master合并到自己的开发分支上，这里会产生冲突
// git rebase master 也可以使用变基，这里会产生冲突
// 解决冲突
// 提交自己分支的代码到远程的git上，然后发起合并请求。
// 以下是master主人操作的
git checkout master  //切换到主分支
git merge hyx       //合并工作分支
git push            // 提交到远程git
```
