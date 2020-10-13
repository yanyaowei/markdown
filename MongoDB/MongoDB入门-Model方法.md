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
        default:"female"//指定了默认值，设置时不写gender项也会自动添加该属性，且为默认值female
    },
    address:String
});
//通过Schema来创建Model，Model代表数据中的集合，要通过Model才能对数据库进行操作
//mongoose.model(modelName,schema)
//modelName就是要映射的集合名
var StuModel=mongoose.model("student",stuSchema);
//-----------------------------------增----------------------------------------
//有了Model，就可以对数据库进行增删改查操作了
// Model.create(doc(s),[callback])
// 用来创建一个或多个文档对象，也可以是一个文档对象的数组
//参数：doc(s)可以是一个文档对象，也可以是一个文档对象的数组
//     callback 当操作完成以后调用的回调函数
// StuModel.create([
//     {
//         name:"猪八戒",
//         age:28,
//         gender:"male",
//         address:"高老庄"
//     },
//     {
//         name:"唐僧",
//         age:24,
//         gender:"male",
//         address:"唐朝"
//     }
// ],function (err){
//     if(!err){
//         // console.log("传入成功！");
//     }
// });
//----------------------------------查--------------------------------------
//查询的方法：
// Model.find(conditions，[projection],[options],[callback])
// Model.findById(conditions，[projection],[options],[callback])
// Model.findOne(conditions，[projection],[options],[callback])
// 以上参数：
// condition是查询的条件，projection是投影，options是查询选项（skip limit）
// callback是回调函数，查询结果会通过回调函数返回，回调函数必须传，如果不穿回调函数，压根不会查询
//--------------------------------
// Model.find(conditions，[projection],[options],[callback])
/*
//1、传统方式：
StuModel.find({name:"唐僧"},function (err,docs){
    if(!err){
        console.log(docs[0].name);
    }
});*/
// 2、用投影，要显示的直接写出属性名，不要的写出属性名并且在前面加上-
/*StuModel.find({},"name age -_id",function (err,docs){
    if(!err){
        console.log(docs);
    }
});*/
//3、设置跳过数量和显示的多少
/*StuModel.find({},"name age -_id",{skip:3,limit:1},function (err,docs){
    if(!err){
        console.log(docs);
    }
});*/
//-----------------------------
// Model.findOne(conditions，[projection],[options],[callback])
// StuModel.findOne({},function (err,doc){
//     if(!err){
//         console.log(doc);
//     }
// });
//-----------------------------
// Model.findById(conditions，[projection],[options],[callback])
//查找id为5f7ebda75a853d1cd463a536的内容,并且通过instanceof来判断是否是StuModel的一个实例
// StuModel.findById("5f7ebda75a853d1cd463a536",function (err,doc){
//     if(!err){
//         console.log(doc instanceof StuModel);
//     }
// });
//--------------------------------改-----------------------------------
/*
Model.update(conditions,doc,[options],[callback])
Model.updateMany(conditions,doc,[options],[callback])
Model.updateOne(conditions,doc,[options],[callback])
    用来修改一个或多个文档
    参数：
    conditions 查询条件
    doc修改后的对象
    options 配置参数
    callback 回调函数
*/
//举例如下：修改唐僧的年龄为20
// StuModel.updateOne({name:"唐僧"},{$set:{age:20}},function (err){
//     if (!err){
//         console.log("修改成功");
//     }
// })
//----------------------------------删-----------------------------
/*删除：
Model.remove(conditions,[callback])
Model.deleteOne(conditions,[callback])
Model.deleteMany(conditions,[callback])
*/
/*StuModel.remove({name:"猪八戒"},function (err){
    if(!err){
        console.log("删除成功");
    }
});*/
//--------------统计文档数量--------------------------------------------------
// Model.count(conditions,[callback])
StuModel.remove({name:"猪八戒"},function (err){
    if(!err){
        console.log("删除成功");
    }
});
```