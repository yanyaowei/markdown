### MongoDB-安装图形化工具NoSQL Manager for MongoDB

### 1、db.collection.insert() 

- 向集合中插入一个或多个文档
- 当我们向集合中插入文档时，如果没有给文档指定_id属性，则数据库会自动为为文档添加-id该属性用来作为文档的唯一标识
- id可以自己指定，如果我们指定了数据库就不会再添加了，如果是自己指定id也必须确保他的唯一性

例：插入一个文档对象

```js
db.stus.insert({name:"白骨精",age:39,gender:"女"});
```

例：插入多个文档对象

```js
db.stus.insert([
 {name:"猪八戒",age:28,gender:"男"},
 {name:"唐僧",age:23,gender:"男"},
 {name:"沙和尚",age:39,gender:"男"}
]);
```

例：插入一个自定义id的文档对象

```js
db.stus.insert({_id:"hello",name:"白骨精",age:39,gender:"女"});
```

### 2、db.collection.insertOne()

插入一个文档对象

```js
db.stus.insertOne({name:"白骨精",age:39,gender:"女"});
```



### 3、db.collection.insertMany()

插入多个文档对象

```js
db.stus.insertMany([
 {name:"猪八戒",age:28,gender:"男"},
 {name:"唐僧",age:23,gender:"男"},
 {name:"沙和尚",age:39,gender:"男"}
]);
```

