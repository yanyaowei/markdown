### 1.在网页中会引用的常见的静态资源？

- JS
  - .js   .jsx   .coffee   .ts(Typescript 类 C# 语言)
- CSS
  - .css    .less    .sass（更新为 .scss，和less差不多）
- Image
  - .jpg   .png   .gif   .bmp    .svg
- 字体文件
  - .svg     .ttf   .woff   .woff2
- 模板文件
  - .ejs  
  -   .jade(是一种模板后缀名，不好用，相当于把闭合符号取消掉了，不好看)
  - .vue   这是在webpack中定义组件的方式，使用这个方便

### 2.网页中引入静态资源太多会有什么问题？如何解决？

1.网页加载缓慢，因为需要发起很多的二次请求

2.处理错综复杂的依赖关系

解决方法：

1、合并、压缩、使用精灵图、小图片转成Base64编码

###### -------精灵图技术产生的目的：很多大型网页在首次加载的时候都需要加载很多的小图片，而考虑到在同一时间，服务器拥堵的情况下，为了解决这一问题，采用了精灵图这一技术来缓解加载时间过长从而影响用户体验的这个问题。

2、使用requireJS、也可以使用webpack来解决各个包之间的复杂依赖关系

###### -------为什么使用RequireJS：

###### · 模块化：模块化就是将不同功能的函数封装起来，并提供使用接口，他们彼此之间互不影响。

###### · 不会阻塞页面：RequireJS，会在相关的js加载后执行回调函数，这个过程是异步的，所以它不会阻塞页面。

###### · 按需加载：平时我们写html文件的时候，在底部可能会引用一堆js文件。在页面加载的时候，这些js也会全部加载。使用require.js就能避免此问题。举个例子，比如说我写了一个点击事件，放到了一个js文件里，并在html引用，在不使用require.js的情况下，页面加载它跟着加载，使用后则是什么时候触发点击事件，什么时候才会加载js。

###### ---------什么是webpack？

###### webpack是前端的一个项目构建工具，他是基于Nodejs开发出来的一个前端工具。



### 3.如何完美实现上述2种解决方案？

使用Gulp，是基于task任务；（小巧灵活，方便）

使用webpack，是基于整个项目进行构建的；

借助webpack这个前端自动化构建工具，完美实现资源的合并、打包、压缩、混淆等多种功能。

### 4.webpack安装方式：

运行`npm i webpack -g`全局安装

在项目根目录中运行 `npm i webpack --save-dev`安装到项目依赖中

### 5.项目实施过程：

(1)先安装JQuery：

`npm init -y`

`npm install jquery -S`

X（2)（不推荐直接引用包和任何JS文件）//实现功能，导入script src

(2)在main.js里写好，之后引用一次main.js的脚本就行

（3）直接执行会报错

（4） 使用webpack命令

`webpack .\src\main.js .\dist\bundle.js`

`webpack   处理路径和名称  保存路径和名称`

##### ！注意这里遇到的问题：

`ERROR in Entry module not found: Error: Can't resolve 'babel-loader' in.........`

##### ！解决方法：

1.安装webpack4.0版本及以上，添加-o

`webpack .\src\main.js  -o .\dist\bundle.js`

2.自己安装的3.6.0版本

安装方法：`npm install -g webpack@版本号`

再使用以上初始方法可以成功执行



##### 在HTML里不推荐直接引用任何包和任何CSS文件 

##### 因为main中的代码，涉及到了ES6的新语法，但是浏览器不能识别 --

##### 因此通过webpack前端构建工具，把main.js做处理，生成一个bundle.js文件



### 6.webpack可以做什么？

1.webpack能够处理JS文件的互相依赖关系

2.webpack能够处理JS兼容问题，把高级的，浏览器不能识别的语法转换为低级的浏览器能够正常识别的语法

### ✔7.webpack配置文件，配置入口、出口文件

文件名为：`webpack.config.js`

代码：

```js
const path = require('path')
//这个配置文件起始就是一个JS文件，通过Node中的模块操作，
//向外暴露了一个配置对象
module.exports = {
    entry:path.join(__dirname,'./src/main.js'),
    //入口，表示要使用webpack打包哪个文件
    output:{//输出文件相关的配置
        path:path.join(__dirname,'./dist'),
        //指定打包好的文件，输出到哪个目录中去
        filename:'bundle.js'//指定输出的文件名称
    }
}
```

有了设置的webpack配置文件就可以不用输`webpack   处理路径和名称  保存路径和名称`完整命令，因为该js里配置好了入口出口文件，所以直接使用`webpack`命令。

### ✔8.当我们在控制台直接输入webpack命令时，webpack做了以下几步：

（1） 首先，webpack发现并没有通过命令的方式给他指定入口和出口；

（2）webpack就回去项目的根目录中查找一个叫做'webpack.config.js'这个配置文件

（3）找到这个配置文件后，webpack就会去解析这个执行文件，当解析执行完配置文件后，就得到了配置文件中导出的配置对象

（4）当webpack拿到配置对象中指定的入口和出口，就进行打包构建。

