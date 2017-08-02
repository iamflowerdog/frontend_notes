## npm -v
- 查看版本

## npm info 包名
- 查看包 历史所有版本信息

## npm init
- 初始化项目，添加package.json

## npm search
- 包名搜索

## npm install
- 安装当前项目依赖

## npm install 包名
- 在当前目录中安装指定的包

## npm install 包名 -g
- 在全局中安装指定的包

## npm install 包名 -save 
- 在当前项目中安装指定的包，并添加依赖

## npm remove 包名
- 移除包名

## npm install body-parser
- 安装post路由解析body对象
    
        req.body 会返回一个对象
            { 
              userName: 'invoker',
              password: '123456',
              passwordConfirm: '123456',
              email: '12233@hhh.con'
            }
        
        req.query 也会返回这样的对象，只不过是通过app.get()路由返回的

## npm install ejs
- 在express站点中使用ejs模板引擎

## npm install mongoose 
- 安装mongoose，搭建数据库

## npm install sha1
- 安装数据库密码加密sha1算法

## npm install express 
- 安装express，搭建服务器

## npm root -g 
- 查询node安装所在目录

## npm express-generator 
- 安装express的基本框架
- express myapp -e  创建模板框架
- cd bin ---> node www ---> localhost:3000 --> Welcome to Express

## 	npm install -g vue-cli

- 安装Vue脚手架工具

## npm WARN deprecated 

- 更改依赖的位置

```
npm WARN deprecated tween.js@16.6.0: This package has moved to @tweenjs/tween.js. Please update your dependencies.
```
