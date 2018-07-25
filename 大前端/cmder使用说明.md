## （0）下载
[cmder Github](https://github.com/cmderdev/cmder/releases)  
看老板心情，想下哪个就下哪个  
解压  
双击  
就好了


## （1）将cmder添加到右键菜单

### 配置环境变量  
依次打开 =>控制面板\系统和安全\系统\高级系统设置\环境变量  
1. 在系统变量中添加变量名和绝对路径 

![cmder_环境变量_系统](./docs/cmder_环境变量_系统.png) 

2. 在Path 里添加变量名  
![cmder_环境变量_path](./docs/cmder_环境变量_path.png)  

3. 以管理员身份运行cmd
```
Cmder.exe /REGISTER ALL
```
![cmder_cmd_输入命令](./docs/cmder_cmd_输入命令.png)
 
4. 成功了  
![cmder_右键](./docs/cmder_右键.png)  