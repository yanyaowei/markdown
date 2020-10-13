### NPM (Node Package Manager) ---Node包管理器

（相当于360软件管家一样）

##### 对于Node而言，NPM帮助其完成了第三 方模块的发布、安装和依赖等。借助NPM， Node与第三方模块之间形成了很好的一个 生态系统。

### NPM命令

##### npm init  										创建一个package.json文件

##### npm –v 						   				查看版本

##### npm version 								 查看所有模块的版本

##### npm search 包名 		  			    搜索模块包 

##### npm install 包名			     			在当前目录安装包（或者npm i）

##### npm install 包名 –g 		  		     全局模式安装包（一般都是安装一些工具）

##### npm remove 包名 						 删除一个模块(或者写npm r)

##### ★npm install  包名 --save 			安装包并添加到依赖中

##### ★npm install    							  下载当前项目所有依赖的包

npm install 文件路径		 – 从本地安装 

npm install 包名 –registry=地址 				   – 从镜像源安装 

npm config set registry 地址 						– 设置镜像源



#### 连接中国的npm镜像服务器————————cnpm（中国的npm）

前提是先安装淘宝镜像：

##### $ npm install -g cnpm --registry=https://registry.npm.taobao.org

之后用cnpm则连接中国的npm服务器

