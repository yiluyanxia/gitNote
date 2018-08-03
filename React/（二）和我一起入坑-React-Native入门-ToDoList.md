# 前置工作
## （〇）了解官方文档是必须的  
[react-native官方文档](http://facebook.github.io/react-native/docs/getting-started.html)  
[react-native中文文档](https://reactnative.cn/docs/0.51/getting-started.html#python-2)  
## （一）安装必需的软件
以下步骤官网早有详细步骤，在此不必赘述。
1. Chocolatey  
[Chocolatey](https://chocolatey.org/install)的官网
使用管理员打开cmd,输入
```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```
2. 安装Python 2
 
在cmd中输入

```
choco install python2
```
![安装python2](./docs/安装python2.png)

输入y,不要直接回车。

3. 安装node

```
choco install  nodejs.install 
```
在此之前我已经用nvm安装过node了。

4. 安装jdk8

```
choco install jdk8

```
在此之前我已经去官网下载jdk了。
注意：jdk版本需为8。

5. 安装Yarn、React Native的命令行工具

```
npm install -g yarn react-native-cli
```

设置镜像源
```
yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global
```

6. 安装Android Studio  
按照官网的配置进行配置即可。

7. 初始化项目

```
react-native init AwesomeProject
cd AwesomeProject
react-native run-android
```
然后bug就来了，出现红色的提示  
<!-- ![cmd运行报错](./docs/安装python2.png) -->

我的理解就是模拟器没有关联并启动所导致的。（可能是错误的）


## （二）在模拟器中运行 

然后打算使用Android Studio直接运行项目。
在初步安装完成后按照官网进行配置以完成全部的安装。
打开已存在的项目，注意选择的是项目下的Android文件夹
稍等几分钟运行按钮由灰色变成绿色

![Android Studio运行报错](./docs/Android-studio报错.png)

原因是 “Vt-x is disabled in BIOS”

遇到问题，首先是想到伟大的网友们。

[华硕主板BIOS UEFI BIOS开启VT步骤](http://www.bluestacks.cn/faq/41_0_1_7.html)  
期间还尝试使用其他模拟器来跑项目，例如"夜神模拟器"，但是怕领导以为我在打游戏，就决定还是用Android Studio，看起来专业一点。

# 实践
## （三）TodoList的结构
安卓没有navigation，官方推荐 react-navigation，  
1. 为了达到真正的入坑，而不是在坑前停留，我会故意把TodoList写得复杂一丢丢，比如添加导航功能，实现数据存储、组件通信的功能等。