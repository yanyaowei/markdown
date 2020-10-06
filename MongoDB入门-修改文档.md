### 1、db.collection.update(查询条件，新对象)

#### 			update（）默认情况下会用新对象来替换旧的对象

#### 			update（）默认只修改一个

​			如果需要修改指定的属性，而不是替换需要使用“修改操作符”来完成修改

#### 1) $set  可以用来修改文档中的指定属性

例：找到—id的对象，修改属性

```js
db.stus.update(
 {"_id" : ObjectId("5f7c1415f1f07255f6ad8ccc")},
 {$set:{
   name:"猪八戒",
   gender:"男",
   address:"高老庄"
       }}
)
```

显示结果:

![image-20201006155438332](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201006155438332.png)

#### 2)  $unset  可以用来删除文档中的指定属性

```js
db.stus.update(
 {"_id" : ObjectId("5f7c1415f1f07255f6ad8ccc")},
 {$unset:{
    address:1
       }}
)
```

### 2、db.collection.updateOne（）

​			修改一个符合条件的文档

```
db.stus.update(
    {"name":"猪八戒"},
    {$set:{
        address:"高老庄"}
    }
)
```

结果：

![image-20201006155438332](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201006155438332.png)

### 3、db.collection.updateMany（）

​			同时修改多个符合条件的文档

```
db.stus.updateMany(
    {"name":"猪八戒"},
    {$set:{
    address:"猪老庄"}
    }
)
```

结果：

![image-20201006160622788](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201006160622788.png)

#### 4、补充：update（）里写multi：true表示要更改很多个对象及属性

```
db.stus.update(
    {"name":"猪八戒"},
    {
        $set:{
        address:"老大哥"
        }
    },
    {
        multi:true
    }
)
```

结果：

![image-20201006161130591](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201006161130591.png)