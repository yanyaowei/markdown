# 一、Vue基础

1、JavaScript框架

2、简化DOM操作

3、响应式数据驱动

### 1、如何跑起来一个Vue程序

1、导入开发版本的Vue.js

2、 创建Vue实例对象，设置el属性和data属性

3、使用间接的模板语法把数据渲染到页面上

举例：

```html
html：
<div id="app">
  {{ message }}
</div>

js：
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app=new Vue({
    el:"#app",
    data:{
      message:"Hello Vue!"
    }
  })
</script>
```

### 2、el：用来设置vue实例挂载（管理）的元素

##### 1）vue实例的作用范围是什么？

###### vue会管理el选项命中的元素及其内部的后代元素

如：下面这个就输出两个小巍的信息

```html
<div id="app">
  {{ message }}
  <span>{{ message }}</span>
</div>


var app=new Vue({
    el:"#app",
    data:{
      message:"小巍的信息"
    }
  })
```

##### 2）是否可以使用其他选择器？

###### 可以使用其他的选择器，但是建议使用ID选择器

##### 3）是否可以设置其他dom元素？

###### 可以使用其他双标签，但不能使用html和body

### 3、data

1）Vue中用到的数据定义在data中

2）data中可以写复杂类型的数据

3）渲染复杂类型数据时，遵守js的语法即可

如：

```html
<div id="app" class="app">
  {{ message }}
  <h2> {{ school.name}}{{school.mobile}}</h2>
  <ul>
    <li>{{campus[0]}}</li>
    <li>{{campus[2]}}</li>
  </ul>
</div>

var app=new Vue({
    el:"#app",
    data:{
      message:"你好小巍",
      school:{
        name:"小巍",
        mobile:"400-100-2000"
      },
      campus:["北京市","上海市","广东市"]
    }
  })
```

