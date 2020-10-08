```js
var mongoose=require("mongoose");
mongoose.connect("mongodb://127.0.0.1/mongoose_test",{useMongoClient:true});
mongoose.connection.once("open",function (){
    console.log("数据库连接成功！");
});
//将mongoose.Schema赋值给一个变量
var Schema=mongoose.Schema;
//创建Schema模式对象
var stuSchema=new Schema({
    name:String,
    age:Number,
    gender:{
        type:String,
        default:"female"
        //指定了默认值，设置时不写gender项也会自动添加该属性，且为默认值female
    },
    address:String
});
//通过Schema来创建Model，Model代表数据中的集合，要通过Model才能对数据库进行操作
//mongoose.model(modelName,schema)
//modelName就是要映射的集合名
var StuModel=mongoose.model("student",stuSchema);
//向数据库中插入文档  StuModel.create(doc,function(err){});
StuModel.create({
    name:"小巍",
    age:20,
    gender:"male",
    address:"成都"
},function(err){
    if(!err){
        console.log("插入成功!");
    }
});


```

结果：

![image-20201008102254528](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201008102254528.png)

### 从生成的数据库中可以看出，mongoose会自动把集合变成复数， 所以我们设置的是student，但是数据库里是students