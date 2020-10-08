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
//-----------------------------Document-----------------------------------
//Document和集合中的文档一一对应，Document是Model实例，通过Model查询到的都是Document
//创建一个Document
var stu=new StuModel({
    name:"wei",
    age:20,
    gender:"male",
    address:"China"
});
//Document的方法：
//Model#save([options],[fn])
// 举例：
// stu.save(function (err){
//     if(!err){
//         console.log("保存成功");
//     }
// });

StuModel.findOne({},function (err,doc){
    if(!err){
       /* 1、直接更改本文档内容
        doc.update({$set:{age:28}},function (err){
            if(!err){
                console.log("修改成功~~~");
            }
        });*/
        /*2、直接删除文档内容
        doc.remove(function (err){
            if(!err){
                console.log("删除完成");
            }
        });*/
        /*3、获取文档属性值
        console.log(doc.get("name"));
        或者console.log(doc.name);*/
       /*  4、设置文档的属性值 set(name,value)
        doc.set("name","小巍啊");
        或 doc.name="小巍啊";*/
        //  5、toObject（）将Document对象转换为一个普通的JS对象
        // 转化为普通JS对象后，注意所有的Document对象方法或属性都不能使用了
        var gg=doc.toObject();
        // console.log(gg);
        console.log(doc);
        doc=doc.toObject();//再转换回来

    }
});
```