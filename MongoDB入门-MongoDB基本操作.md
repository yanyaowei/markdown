### 1、MongoDB基本概念

数据库（database）

集合（collection）

文档（document）

​		在MongoDB中，数据库和集合都不需要手动创建，

​		当我们创建文档时，如果文档所在集合或数据库不存在，会自动创建

### 2、MongoDB基本指令

1. ##### show database(可简写为  show dbs)--------显示当前的所有数据库

2. ##### use 数据库名--------------------进入到指定的数据库

3. ##### db----------表示当前所在的数据库位置

4. ##### show collections---------显示数据库中所有的集合

### 3、数据库的CURD（增删改查）的操作

1. ##### 向数据库中插入文档

   ​	db.collection.insertOne()-----------向集合中插入一个文档

   例子：向test数据库中的，stus集合中插入一个新的学生对象
   					{name:"孙悟空",age:18,gender:"男"}
   					db.stus.insert({name:"孙悟空",age:18,gender:"男"})

   ​			成功插入后显示：WriteResult({ "nInserted" : 1 })

2. ##### 查询当前集合中的所有的文档

   ​	db.<collection>.find()

   例：
   
    输入：>db.stus.find()
    {"_id" : ObjectId("5f7bdfa7fb5800a3c67dd61c"), "name" : "孙悟空", "age" : 18, "gender" : "男" }

