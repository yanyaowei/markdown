1、创建需要便捷模块化的文件夹，如tools，modules文件夹

2、在tools文件夹里定义一个模块(connect_mongo.js)，连接MongoDb数据库

```js
var mongoose=require("mongoose");
mongoose.connect("mongodb://127.0.0.1/mongoose_test");
mongoose.connection.once("open",function (){
    console.log("数据库连接成功！");
});
```

3、在models文件夹里定义一个student的模型（student.js)

```js
//用来定义student的模型
		//引入mongoose
var mongoose=require("mongoose");
		//定义Schema
var Schema=mongoose.Schema;
		//创建约束对象
var stuSchema=new Schema({
    name:String,
    age:Number,
    gender:{
        type:String,
        default:"female"
    },
    address:String
})
//定义模型
var StuModel=mongoose.model("student",stuSchema);
module.exports=StuModel;
```

在另一个需要用到这些模块的文件里调用：（test.js)

```js
require("./tools/connect_mongo");//连接MongoDB服务器
var Student=require("./models/student");//获取Model
Student.find({},function (err,docs){
    if(!err){
        console.log(docs);
    }
});
```

运行test.js结果：

![image-20201008164651461](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201008164651461.png)