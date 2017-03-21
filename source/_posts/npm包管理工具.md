---
title: npm包管理工具
date: 2017-03-13 17:14:04
tags:npm node.js

---
##问题场景
>在使用npm的时候 安装命令有些困惑
>比如  

	 npm install vue
	
	$ npm install --global vue-cli
	$ vue init webpack my-project
	$ cd my-project
	$ npm install
	$ npm run dev


>两个npm安装都是vue 有什么区别？        

 

##1.  使用 npm 命令安装模块（比如框架）

npm 安装 Node.js 模块语法格式如下：

	$ npm install Module Name  

##2. 全局安装与本地安装

npm 的包安装分为本地安装（local）、全局安装（global）两种，从敲的命令行来看，差别只是有没有-g而已，比如  


	npm install express    # 本地安装   
	npm install express -g   # 全局安装 
##3. 对于大陆用户，建议将 npm 的注册表源设置为[国内的镜像](http://riny.net/2014/cnpm/)，可以大幅提升安装速度。