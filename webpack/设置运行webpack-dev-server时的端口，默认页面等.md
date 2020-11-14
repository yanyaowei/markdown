### 1.改变端口--open --port和默认页面--contentBase

webpack-dev-server提供的默认打开接口是：

locahost：8080

显示如下：

![image-20201113203131954](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201113203131954.png)

可以自行设置：

`"dev": "webpack-dev-server --open --port 3000 --contentBase src"`

进入后显示：

![image-20201113203307890](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201113203307890.png)

端口和默认显示页面都被改变

### 2.减少不必要的代码更新，加入--hot，实现浏览器无刷新

`"dev": "webpack-dev-server --open --port 3000 --contentBase src --hot"`

--hot启用之前webpack-dev-server会重新生成文件；

--hot启用之后不会重新生成文件，但是会生成两个局部更新文件（相当于你改了哪里就生成一点补丁文件），页面就只需要应用少量更新就行了。

--hot启用之后也可实现浏览器无刷新（之后学）。

### 3.webpack中除了exports，其他带s的都是数组

### 4.在webpack.config.js中配置webpack-dev-server(了解)

webpack.config.js:

```js
const path = require('path')
//启用热更新的第二步：
const webpack =require('webpack')
//这个配置文件起始就是一个JS文件，通过Node中的模块操作，
//向外暴露了一个配置对象
module.exports = {
    entry:path.join(__dirname,'./src/main.js'),
    //入口，表示要使用webpack打包哪个文件
    output:{//输出文件相关的配置
        path:path.join(__dirname,'./dist'),
        //指定打包好的文件，输出到哪个目录中去
        filename:'bundle.js'//指定输出的文件名称
    
},
devServer:{//这个是配置dev-server命令参数的第二种形式，相对来说更麻烦一些
     //--open --port 3000 --contentBase src --hot
     open : true,//自动打开浏览器
     port : 3000,//设置启动时的运行端口
     contentBase:'src',//指定托管的根目录
     hot: true//启用热更新的第一步
},
plugins:[//配置插件的节点
    //new一个热更新的模块对象，这里启用热更新的第三步：
   new webpack.HotModuleReplacementPlugin()
]
}
```

