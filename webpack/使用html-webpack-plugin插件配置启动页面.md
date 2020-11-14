### 使用`html-webpack-plugin`插件配置启动页面

1、运行cnpm i html-webpack-plugin --save-dev安装到开发依赖

2.修改webpack.config.js配置文件：

导入包：

```js
//导入在内存中生成html页面的插件,只要是插件都一定要放到plugin节点中去
const htmlWebpackPlugin=require('html-webpack-plugin')
```

生成内存对象：

```js
plugins:[//配置插件的节点
    //new一个热更新的模块对象，这里启用热更新的第三步：
   new webpack.HotModuleReplacementPlugin(),
   new htmlWebpackPlugin({//创建一个在内存中生成HTML页面的插件
        template:path.join(__dirname,'./src/index.html'),//指定模板页面将来会根据指定的页面路径生成内存中的页面
        filename:'index.html'//指定生成的内存中的页面的名称
   })
]
```

当使用html-webpack-plugin之后，我们不再需要手动处理bundle.js的引用路径了，它将会自动创建一个合适的script标签并且启用它。

因此，这个插件的作用：

1.自动在内存中根据页面生成一个内存的页面

2.自动把打包好的bundle.js追加到页面中去