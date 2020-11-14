### loader-处理CSS样式表的第三方loader

*注意：webpack默认只能打包处理JS类型的文件，无法处理其他的非JS类型的文件*

*如果需要处理非JS类型的文件，我们需要手动安装一些合适的第三方Loader加载器*

1、如果想要打包处理css文件，需要安装cnpm i style-loader css-loader -D,我用的版本（和前面兼容）

![image-20201114193336365](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201114193336365.png)

2、打开webpack.config,js配置文件新增配置节点，叫做module，他是一个对象，在这个module对象上，有一个rules属性，这个rules属性是一个数组，这个数组中存放了所有的第三方文件匹配和处理规则

webpack.config.js文件修改内容：

```js
const path = require('path')
//启用热更新的第二步：
const webpack =require('webpack')
//这个配置文件起始就是一个JS文件，通过Node中的模块操作，
//向外暴露了一个配置对象

//导入在内存中生成html页面的插件,只要是插件都一定要放到plugin节点中去
const htmlWebpackPlugin=require('html-webpack-plugin')

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
   new webpack.HotModuleReplacementPlugin(),
   new htmlWebpackPlugin({//创建一个在内存中生成HTML页面的插件
        template:path.join(__dirname,'./src/index.html'),//指定模板页面将来会根据指定的页面路径生成内存中的页面
        filename:'index.html'//指定生成的内存中的页面的名称
   })
],
module:{//这个节点配置所有的第三帆帆模块加载器
    rules:[//所有的第三方模块的匹配规则
        {test: /\.css$/ ,use: ['style-loader','css-loader']}//配置处理.CSS文件的第三方loader规则
        //前面用test来匹配规则，之后use用什么来处理
    ]
}
}
```