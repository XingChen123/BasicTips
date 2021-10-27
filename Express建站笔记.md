# 昊仁课程学习website教程

# express网页前端框架初始化搭建
## 1.0 下载及前端初始配置
保证有npm 和 node 的version
::npm install nodemon:: 随时自动更新npm start [nodemon  -  npm](https://www.npmjs.com/package/nodemon)


### 1.1新建项目步骤:
* ::npm init:: (生成package.json文件)
* ::npm install express —save::
* ::npm install express-generator —save::
* express -e =>y
* 把bin文件夹中的www拿到最外面改成server.js
	* 移出来的同时server.js本身内部调用app路径改变
	* package.json 的npm start 路径改变
* ::npm install::
* 新建.gitignore文件 内容: node_modules


### 1.2做UI界面用到的框架

* Icons网站: fontawesome.com
		    ::npm i @fortawesome/fontawesome-free::
		    logo.com
* bootstrap教程: [Bootstrap 3, 4 or 5](https://www.w3schools.com/bootstrap/bootstrap_ver.asp)
		    ::npm install bootstrap::
		    ::npm install jquery::

注: 引用的时候view页面增加两大类jquery,bootstrap及font各自需用的css+js:
	* 	link:css
	*  script:src
(路径引用时,在app.js里添加node_modules的路径)

## 2.0后端配置
MongoDB下载链接: [MongoDB Community Download | MongoDB](https://www.mongodb.com/try/download/community)





