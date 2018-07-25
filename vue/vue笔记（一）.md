cd..

node -v
npm -v

npm install -g webpack   安装webpack


npm install -g cnpm –registry=https://registry.npm.taobao.org   安装npm镜像（不要，直接cnpm会破坏目录结构  

npm config set registry https://registry.npm.taobao.org     配置npm的registry地址（推荐使用这个）
 
npm config get registry  配置后可通过下面方式来验证是否成功

npm install -g vue-cli  

vue init webpack vue_project

npm install

  npm install --save vue-async-data vue-resource

  npm install vue-router vue-resource --save

npm run dev

npm install vue-router@0.7.13  //设置下载版本


--NODE--------

express -e myapp  创建node项目使用ejs模板引擎 没有-e 则默认使用jade
 


--Git---------

$ git clone https://github.com/airbnb/javascript.git

修改代码

cd javascript   //进入到文件夹

git add .    //将改动的地方添加到版本管理器 有个点

git  commit -m "some changes" //提交到本地的版本控制库里，引号里面是对本次提交的说明信息

git push -u origin master  //将本地的仓库提交到github账号里，此时需要输入github的账号和密码

进入到你的github上面，选择到这个javascript项目名，单击 pull request


--git 将本地项目添加到GitHub上-------------

1.在本地项目上右键git bash

$ git init    //初始化git项目，会生成.git文件

2.将项目添加到仓库

$ git status     //显示是否添加的状态，非必需
 
$ git add .      //“.”表示将所有的添加上去

3.将添加的文件提交到仓库上

$ git commit -m "注释语句"   

4.去github上你创建好的仓库复制路径，将本地关联GitHub

git remote add origin https://github.com/yiluyanxia/vue-blog-FE.git   

5.上传github之前，要先pull一下

$ git pull origin master   //非必须

6.上传到GitHub远程仓库

$ git push -u origin master  //第一次需要输入账号和密码

7.完成了！可以去GitHub上查看了！！

--git将项目提交到gh-pages分支上------

$ git checkout -b gh-pages     //切换到gh-pages分支

$ git add -f dist         //强制添加dist 因为.gitignore文件中定义了忽略该文件

$ git commit -m "注释语句"  

$ git subtree push --prefix dist origin gh-pages   //部署dist目录下的代码 （运行时报错了）  非必须

$ git remote add origin https://github.com/yiluyanxia/vue-blog-FE.git   

$ git push -u origin gh-pages     //提交到远程分支
