### 1、Mongoose就是一个让我们可以通过Node来操作 MongoDB的模块。 

##### Mongoose是一个对象文档模型（ODM）库，它对 Node原生的MongoDB模块进行了进一步的优化封装， 并提供了更多的功能。

##### 在大多数情况下，它被用来把结构化的模式应用到一个 MongoDB集合，并提供了验证和类型转换等好处

### 2、mongoose的好处 

#####  • 可以为文档创建一个模式结构（Schema）

#####  • 可以对模型中的对象/文档进行验证

#####  • 数据可以通过类型转换转换为对象模型

#####  • 可以使用中间件来应用业务逻辑挂钩 

#####  • 比Node原生的MongoDB驱动更容易

### 3、新的对象，mongoose中为我们提供了几个新的对象

####  – Schema(模式对象) 

• Schema对象定义约束了数据库中的文档结构 

#### – Model

 • Model对象作为集合中的所有文档的表示，相当于 MongoDB数据库中的集合collection 

#### – Document 

• Document表示集合中的具体文档，相当于集合中 的一个具体的文档

#### 先有Schema，再有model，再有Document

### 4、mongoose使用：

/*

##### 1、下载安装mongoose

npm i mongoose --save

##### 2、在项目中引入mongoose

var mongoose=require("mongoose")

##### 3、连接MongoDB数据库

如果端口号是默认端口号（27017）可省略不写
mongoose.connect('mongodb://数据库ip地址:端口号/数据库名');

##### 4、断开数据库连接（一般不需要调用)

MongoDB数据库一般情况下，只需要连接一次，连接一次后，除非项目停止服务器关闭，否则连接不会断开
mongoose.disconnect()

5、监听MongoDB数据库的连接状态
在mongoose对象中，有一个属性叫做connection，该对象表示的就是数据库连接
通过监视该对象的状态们可以用来监听数据库的连接与断开

数据库连接成功的事件
mongoose.connection.once("open",function(){});
数据库连接断开的事件
mongoose.connection.once("close",function(){});
*/

举例：

```
//引入
var mongoose=require("mongoose");
//连接数据库
mongoose.connect("mongodb://127.0.0.1/mongoose_test");

mongoose.connection.once("open",function(){
    console.log("Success!");
});

mongoose.connection.once("close",function(){
    console.log("Bye!");
});
//断开连接
mongoose.disconnect();
```

结果：

![image-20201008100017270](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201008100017270.png)