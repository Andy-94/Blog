# Blog
### 1.把css阻塞和js阻塞的规律？
  
### 2.图层的概念好好理解一下？
### 3.重绘重排概念的理解？
### 4.Node使用express搭建服务器？
	创建一个文件夹，cd 到当前文件夹 ，运行 npm init 创建package.json
	使用vscode打开当前文件，开启vscode 终端 cd 到当前文件夹下 touch server.js (创建入口文件)
	在当前文件夹下安装express 模块 “npm install express”
	在server.js 编写代码：
    ‘’‘
	const express = require("express");//引入express
	const app = express();//实例化一个express APP
    	app.get("/",(req,res)=>{
        res.send("Hello World");
		}) //设置路由
		const port = process.env.port || 5000;//定义端口号
		app.listen(port,()=>{
    			console.log(`Server running on port ${port}`);
		}) //监听
    ’‘’
		使用 node server.js 启动服务 (这样启动的话每次改变代码都需要重启)，
		安装 nodemon ：sudo npm install nodemon -g (Mac系统全局安装，Windows可去掉sudo)
		然后就可以使用 nodemon server.js 启动 服务 ，这样以后改变代码，它就会帮我们自动保存
		配置package.json 设置启动方式
			"scripts": {
  			 "start": "node server.js",
   			 "server":"nodemon server.js"
 			 },
		这样的话 可以使用 npm run start 和 npm run server 启动服务
### 5.ES6的新语法：结构赋值、箭头函数。
	
