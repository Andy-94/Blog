# Blog
### 1.css阻塞和js阻塞的规律？
  	The HTML page is running from up to down. 
	HTML --> DOM tree
	Style/link --> CSS style dom tree
	script --> javascript engine run script
	combination the DOM tree and Css dom tree
Announce: only <link style=""> has css blocking.
        
	1.style标签中的样式：
            (1). 由html解析器进行解析；
            (2). 不阻塞页面渲染（所以可能会产生“闪屏现象”）；
            (3). 不阻塞DOM解析；

        2.link引入的外部css样式（我们推荐使用的方式）：
            (1). 由CSS解析器进行解析。
            (2). 阻塞页面渲染(可以利用这种阻塞避免“闪屏现象”)。
            (3). 阻塞其后面的js语句的执行
            (4). 不阻塞DOM的解析(绝大多数浏览器的工作方式)：

        3.优化核心理念：尽可能快的提高外部css加载速度
            (1).使用CDN节点进行外部资源加速。
            (2).对css进行压缩(利用打包工具，比如webpack等)。
            (3).减少http请求数，将多个css文件合并。
            (4).优化样式表的代码
js blocking:
	
	1.阻塞后续DOM解析:
            原因：浏览器不知道脚本的后续内容，若先去解析了下面的html结构，而随后的js删除了后面所有的html结构，
                  那么浏览器就做了无用功。所以js的执行会阻塞页面的解析，。
        2.阻塞页面渲染:
            原因：解析是渲染的前序操作，经过了解析，才能渲染。即：阻塞了解析必定阻塞了渲染。
        3.阻塞后续js的执行:
            原因：要维护多个js的依赖关系，例如：必须先引入jquery.js再引入bootstrap.js

### 2.图层的概念？
	When browsers is running, there are servers layouts on the page.
### 3.重绘重排概念的理解？
	重绘是一个元素外观的改变所触发的浏览器行为，例如改变背景色等属性。
	浏览器会根据元素的新属性重新绘制，使元素呈现新的外观。
	重排：
	浏览器计算每个图层中节点的位置和大小信息的过程称为布局或重排
### 4.Node使用express搭建服务器？
	* 创建一个文件夹，cd 到当前文件夹 ，运行 npm init 创建package.json
	使用vscode打开当前文件，开启vscode 终端 cd 到当前文件夹下 touch server.js (创建入口文件)
	在当前文件夹下安装express 模块 “npm install express”
	在server.js 编写代码：
	const express = require("express");//引入express
	const app = express();//实例化一个express APP
    	app.get("/",(req,res)=>{
        	res.send("Hello World");
	}) //设置路由
	const port = process.env.port || 5000;//定义端口号
	app.listen(port,()=>{
    			console.log(`Server running on port ${port}`);
	}) //监听
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
	
