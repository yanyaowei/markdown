# Vue实例

### 1、v-text

1、v-text：作用：设置标签内容

2、默认写法会提花全部内容，使用差值表达式{{}}可以替换指定内容

3、内部支持写表达式

如：

```html
<div id="app">
  <h2 v-text="message+'!'">深圳</h2>//内部写表达式
  <h2 v-text="info">深圳</h2>//设置指定内容
  <h2>{{message+'!'}}深圳</h2>//替换指定内容
    
    
var app=new Vue({
    el:"#app",
    data:{
      message:"小维信息",
      info:"前端学习"
    }
  })
```

输出：

```
小维信息!
前端学习
小维信息!深圳
```

### 2、v-html

1、v-html指令的作用是：设置元素的innerHTML

2、内容中有html结构会被解析为标签

3、v-text指令无论内容是什么，只能解析为文本

如：

```html
<div id="app">
  <p v-html="content"></p>
  <p v-text="content"></p>
</div>

var app=new Vue({
    el:"#app",
    data:{
      content:"<a href='http://www.baidu.com'>小维信息</a>"
    }
  })
```

输出结果：

```html
小维信息(可点击跳转)

<a href='http://www.baidu.com'>小维信息</a>
```

### 3、v-on

1、v-on指令的作用：为元素绑定事件

2、事件名不需要写on

3、指令可以简写为@

4、绑定的方法定义在methods属性中

5、方法内部通过this关键字可以访问定义在data中数据

如：

```html
<div id="app">
  <input type="button" value="v-on指令" v-on:click="doIt">//doIt单击后弹出methods里的做it

  <input type="button" value="v-on简写" @click="doIt">//doIt单击后弹出methods里的做it

  <input type="button" value="双击事件" @dblclick="doIt">//doIt双击后弹出methods里的做it

  <h2 @click="changeFood">{{food}}</h2>//food被替换为data内的西兰花，并且点击文字部分执行changFood里的事件：控制台输出西兰花，事件点击发生后会在h2处一直添加好吃得不得了！
</div>





var app=new Vue({
    el:"#app",
    data:{
      food:"西兰花"
    },
    methods:{
      doIt:function () {
        alert('做it');
      },
      changeFood:function () {
        console.log(this.food);//事件点击后发生会输出西兰花
        this.food+="好吃的不得了！"//事件点击发生后会在h2处一直添加好吃得不得了！
      }
    },
  })
```

输出结果：

![1600397848150](Vue实例.assets/1600397848150.png)

### 4、计数器实例操作

![1600482376500](Vue实例.assets/1600482376500.png)

程序如下

```html
<div id="app">
  <div class="input-num">
    <button @click="sub"> -</button>
    <span> {{ num }} </span>
    <button @click="add"> +</button>
  </div>
</div>




var app=new Vue({
    el:"#app",
    data:{
      num:1
    },
    methods:{
      add:function () {
        // console.log('add');
        if(this.num<10){
          this.num++;
        }else{
          alert('别点啦，最大啦！');
        }
      },
      sub:function () {
        // console.log('sub');
        if(this.num>0){
          this.num--;
        }else{
          alert('别点啦，最小啦！');
        }
      }
    },
  })         
```