### 1、db.collections.find()查找文档-----返回数组

​		find（）用来查询集合中所有符合条件的对象

​		find（）可以接收一个对象作为参数

​			 	{ }表示查询集合中所有的文档

​				{ 属性：值 }查询属性是指定值的文档

例：

```js
db.stus.find({_id:"hello"});
db.stus.find({age:28});
```

### 2、db.collections.findOne()查询集合中符合条件的`第一个`文档-----返回对象

例：

```js
db.stus.findOne({age:28});
db.stus.findOne({age:28}).name;
```

### 3、db.collections.find({}).count()查询所有结果的数量

例：

```
db.stus.find({}).count();//查询所有结果的数量
或
db.stus.find({}).length();//结果一样
```

