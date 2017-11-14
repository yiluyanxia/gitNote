##  react 安装

npm install -g create-react-app  
create-react-app my-app  
cd my-app  
npm start  

由于网络原因有时候会卡住 ，修改为淘宝镜像

npm config set registry https://registry.npm.taobao.org  
-- 配置后可通过下面方式来验证是否成功  
npm config get registry  
-- 或npm info express

## 直接在html中使用

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello World</title>
    <script src="https://unpkg.com/react@latest/dist/react.js"></script>
    <script src="https://unpkg.com/react-dom@latest/dist/react-dom.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
    //你可以修改下面的代码来实现你的React应用
      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('root')
      );

    </script>
  </body>
</html>
```

Success! Created staff-manage at C:\hyxstudy\workspace-react\staff-manage
Inside that directory, you can run several commands:

  npm start  
    Starts the development server.

  npm run build  
    Bundles the app into static files for production.

  npm test  
    Starts the test runner.

  npm run eject  
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd staff-manage  
  npm start

Happy hacking!