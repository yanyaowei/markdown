### 1.实现webpack自动打包编译（html等文件在附录）

使用`webpack-dev-server`这个工具，是西安自动打包编译的功能

方法:

1. 运行`npm i webpack-dev-server -D`把这个工具安装到项目的本地开发依赖中

2. 安装完毕后，这个工具的用法和webpack的用法完全一样

3. 由于是在项目中本地安装的webpack-dev-server。所以无法把他当作脚本命令，在powershell终端中直接运行，只有那些安装到全局的-g的工具才能在终端中正常执行。

4. 所以在package.json的“script”里添加"dev":"webpack-dev-server"

   ###### 注意：webpack-dev-server这个工具如果要正常运行，要求在本地项目中必须安装webpack（哪怕时全局安装了，也要在项目中安装webpack）

   

### 2、webpack-dev-server兼容问题

问题：安装完成后，执行命令`npm run dev` 发现报错： `Error: Cannot find module 'webpack-cli/bin/config-yargs’`

原因是：webpack3.x的版本与webpack-dev-server3.x 的版本不兼容。

解决方法：

1.卸载局部或者全局 webpack-dev-server

npm uninstall webpack-dev-server -g       卸载全局
npm uninstall webpack-dev-server -D      卸载局部(本地) 

2.安装指定版本的 webpack-dev-server@2.9.7

npm i webpack-dev-server@2.9.7 -D    本地安装

3.然后执行命令 `npm run dev`

我自己的package.json配置，没有问题了,而且提供了地址来查看，默认是`locahost：8080`：

```js
{
  "name": "webpack-study",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "jquery": "^3.5.1"
  },
  "devDependencies": {
    "webpack": "^3.8.1",
    "webpack-dev-server": "^2.9.3"
  }
}

```

#### 3、新问题又来了：改变main.js中的属性比如颜色，自动打包编译了，但是页面locahost：8080/src/颜色没有变化，怎么办？

##### 原因和处理方法：

认为是本地dist文件夹里的bundle.js，所以给改变main.js没有改变bundle.js,但是改为根目录下的话，更新main.js会更新bundle.js

所以把index.html中引入的../dist/bundle.js直接写成根目录的/bundle.js

而且很惊喜的发现webpack-dev-server把网页自动刷新了！

#### 4、webpack-dev-server帮我们生成的文件（如我这里的bundle.js)并没有存放到实际的物理磁盘上，而是直接托管到了了电脑的`内存`中，所以我们在项目的根目录中，根本找不到打包好的bundle.js。相当于在项目根文件里放了一个不可见的bundle.js，以一种虚拟的形式托管到了项目根目录中，虽然看不到它，但是可以认为和dist src node_modele平级。

![image-20201113202419709](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201113202419709.png)

index.html：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="/bundle.js"></script>
    <!-- 不推荐直接引用任何包和任何CSS文件 -->
    <!-- 因为main中的代码，涉及到了ES6的新语法，但是浏览器不能识别 -->
<!-- 因此通过webpack前端构建工具，把main.js做处理，生成一个bundle.js文件 -->
</head>
<body>
    <ul>
        <li>这个是第1个li</li>
        <li>这个是第2个li</li>
        <li>这个是第3个li</li>
        <li>这个是第4个li</li>
        <li>这个是第5个li</li>
        <li>这个是第6个li</li>
        <li>这个是第7个li</li>
        <li>这个是第8个li</li>
        <li>这个是第9个li</li>
        <li>这个是第10个li</li>
    </ul>
</body>
</html>
```

main.js:

```js
//这个main.js是项目的JS入口文件

//1.导入jQuery

//import *** from ***是ES6中导入模块的方式
//ES6代码很高级，所以下面这一行执行会报错无法识别
import $ from 'jquery';//相当于const $ =require("jquery");

$(function(){
    
    $('li:odd').css('backgroundColor','blue');

    $('li:even').css('backgroundColor',function(){
        return '#'+'ff0000';
    });
})
```

