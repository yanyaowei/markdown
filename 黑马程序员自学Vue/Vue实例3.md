# Vue案例3

# 1、v-for

1、指令的作用：根据数据生成列表结构

2、数组经常和v-for结合使用

3、语法是`（item，index）in 数据`  ，其中，item代表每一项，index代表索引，数据对应data中对应的数据

4、item和index可以结合其他命令一起使用

5、数组长度的更新会同步到页面上，是响应式的

举例:

```html
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
  <meta charset="UTF-8">
  <title>v-for</title>
</head>
<body>
<div id="app">
  <input type="button" value="添加数据" @click="add">
  <input type="button" value="移除数据" @click="remove">
  <ul>
    <li v-for="(item,index) in arr">
      {{ index+1 }}小巍在哪儿：{{ item }}
    </li>
  </ul>
  <h2 v-for="item in games" v-bind:title="item.name">
   你爱玩的游戏有： {{ item.name }}
  </h2>
</div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app=new Vue({
    el:"#app",
    data:{
      arr:["北京","上海","成都"],
      games:[
        {name:"王者荣耀"},
        {name:"和平精英"}
      ]
    },
    methods:{
      add:function () {
        this.games.push({name:"奇迹暖暖"})//把指定的值添加到数组后的新长度
      },
      remove:function () {
        this.games.shift();//shift() 方法用于把数组的第一个元素从其中删除，并返回第一个元素的值
      }
    }
  })
</script>
</html>
```

输出：

![1600571835781](Vue实例3.assets/1600571835781.png)

## 2、v-on补充，事件修饰符

1、事件绑定的方法写成`函数调用`的形式，可以传入自定义参数

2、定义方法时需要定义`形参`来接受传入的实参

3、事件的后面跟上`.修饰符`可以对事件进行限制

4、`.enter`可触发的按键为回车键

## 3、v-model

### 获取和设置`表单元素`的值（双向数据绑定）

1、v-model指令的作用是便捷的设置和获取表单元素

2、绑定的数据回合表单元素值相关联

3、绑定的数据←→表单元素的值双向绑定，无论修改谁，都会跟着改变

举例：

```html
<div id="app">
  <input type="button" value="修改message" @click="setM">
  <input type="text" v-model="message" @keyup.enter="getM">
  <h2>{{ message }}</h2>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app=new Vue({
    el:"#app",
    data:{
        message:"小巍",
    },
    methods:{
        getM:function () {
          alert(this.message);
        },
        setM:function () {
          this.message="牛批";
      }
    }
  })
</script>
```

# 4、小黑记事本

### （1）新增

v-for指令根据数组生成列表结构，v-model双向绑定数据，把表单元素的内容和data中的数据关联起来，方便设置取值，v-bind来绑定事件

1、生成列表结构（v-for，使用字符串数组）

2、获取用户输入（v-model双向数据绑定，data里要定义）

3、回车时新增数据（v-on,.enter时添加数据）

### （2）删除

1、点击删除指定内容（v-on:click点击，splice删除，获取下标根据索引删除）

数据改变和数据绑定同步改变（删除就都删除）

数据可以接受自定义参数

（3）清空

（4）隐藏