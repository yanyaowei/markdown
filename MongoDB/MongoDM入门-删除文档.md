## ★一般数据库中的数据不会删除，所以删除的方法很少调用，一般会在数据中添加一个字段，来表示数据是否删除★

如：

```
db.stus.insert([
 {name:"猪八戒",age:28,gender:"男",isDel:0},
 {name:"唐僧",age:23,gender:"男",isDel:0},
 {name:"沙和尚",age:39,gender:"男",isDel:0}
]);
```

在数据库中可以通过看自定义添加的isDel来知道数据是否删除

![image-20201006164110510](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201006164110510.png)



### 1、db.collection.remove()

- #### 删除符合条件的所有的文档，默认情况下删除多个

- #### 如果remove（）第二个参数传递一个true，则只会删除一个

- #### ★★★如果值传递一个空对象，即直接输`db.collection.remove()；`直接`清空`了所有集合，但是性能不好，相当于留了一个空的collection，可以用`db.collection.drop()；`来直接将collection删除，则其中的集合也不在了

举例：

-----删除前：

![image-20201006161623910](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201006161623910.png)

-----执行代码:

```
db.stus.remove({_id:"hello"});//全部hello为id的被删除
db.stus.remove({age:28},true};//只删除一个age为28的
```

-----结果：

![image-20201006162401164](C:\Users\24417\AppData\Roaming\Typora\typora-user-images\image-20201006162401164.png)

### 2、db.collection.deleteOne()



### 3、db.collection.deleteMany()



### 4、db.collection.drop() 删除集合



### 5、db.dropDatabase() 删除数据库