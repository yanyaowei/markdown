# 1、v-show

1. v-show指令的作用：根据真假切换元素的显示状态

2. 原理是修改元素的display，实现显示隐藏

3. 指令后面的内容，最终都会解析为布尔值

4. 值为true元素显示，值为false元素隐藏

   ### (就像是只在标签里定义了diaplay:none隐藏起来而已，频繁调用可用这个)

举例：

```html
<div id="app">
    <input type="button" value="切换显示图片" @click="changeIsShow">
    <input type="button" value="累加年龄" @click="addAge">
    <img v-show="isShow" src="pic.png" alt="fox">
    <img v-show="age>=18" src="pic.png" alt="fox">
  </div>


var app =new Vue({
    el:"#app",
    data:{
      isShow:false,
      age:17
    },
    methods:{
      changeIsShow:function () {
        this.isShow=!this.isShow;//取反
      },
      addAge:function () {
        this.age++;
      }
    },
  })
```

最后的效果:

![1600484013003](Vue实例续.assets/1600484013003.png)

# 2、v-if

##### 根据表达值得真假，切换元素的显示和隐藏（操纵dom元素）

1、v-if指令的作用是：根据表达式的真假切换元素的显示状态

2、本质上是通过操纵dom元素来切换显示状态

3、表达式的值为true，元素存在于dom树中，为false，从dom中移除

### （就像是直接那个dom元素连同标签都不在了一样）

举例：

```html
<div id="app">
  <input type="button" value="切换显示" @click="toggleIsShow">
  <p v-if="isShow">小巍</p>
  <p v-show="isShow">小巍Hero</p>
  <h2 v-if="temperature>=35">热死啦</h2>
    
    
var  app=new Vue({
    el:"#app",
    data:{
      isShow:false,
      temperature:36
    },
    methods:{
      toggleIsShow:function () {
        this.isShow=!this.isShow;
      }
    },
  })   
    
```

结果：

![1600485201717](Vue实例续.assets/1600485201717.png)

# 3、v-bind

1. 指令的作用：为元素绑定属性
2. 完整写法：`v-bind：属性名`
3. 3.简写方法是：       `：属性名`

举例：

```html
 <img v-bind:src="imgSrc" alt="">
  <br>
  <img :src="imgSrc" alt="" :title="imgTitle+'!!!!'"
       :class="isActive?'active':''" @click="toggleActive"><!--简写-->
  <br>
  <img :src="imgSrc" alt="" :title="imgTitle+'!!!!'"
       :class="{active:isActive}" @click="toggleActive"><!--简写-->




var app=new Vue({
    el:"#app",
    data:{
      imgSrc:"pic.png",
      imgTitle:"小巍",
      isActive:false
    },
    methods:{
      toggleActive:function () {
        this.isActive=!this.isActive;
      }
    }
  })
```

# 4、图片切换案例

v-show  v-bind应用

```html
<div id="mask">
  <!--左箭头-->
  <a href="javascript:void(0)" v-show="index!=0" @click="prev" class="left">
  <img src="direction-left.png" alt="">
  </a>
  <!--图片-->
  <img :src="imgArr[index]" alt="">
  <!--右箭头-->
  <a href="javascript:void(0)" v-show="index<imgArr.length-1" @click="next" class="right">
    <img src="direction-right.png" alt="">
  </a>
</div>



var app=new Vue({
    el:"#mask",
    data:{
      imgArr:[
        "1.png",
        "2.png",
        "3.png",
        "4.png",
        "5.png",
        "6.png",
      ],
      index:0
    },
    methods:{
      prev:function () {
        this.index--;
      },
      next:function () {
        this.index++;
      }
    }
  })
```

显示结果:

![1600569107089](Vue实例续.assets/1600569107089.png)

