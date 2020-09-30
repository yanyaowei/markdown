### 一、认识JQuery



#### 1、认识jQuery

JQ是JS库，是对JavaScript的一个封装，也就是说JQ提供了大量的API，在开发时。以最少的代码实现最多的功能

在2006年开源，已发展成集JS、CSS、DOM、Ajax一体的框架体系。

宗旨：write less，do more！（写的少做的多！）

#### 2、获取网站

https://www.bootcdn.cn

#### 3、JQ功能

##### 1、控制页面样式

##### 2、访问和操作DOM

##### 3、事件处理（简化了事件处理机制）

##### 4、提供了大量的插件（很多功能和样式进行了封装，可直接拿来用）

##### 5、Ajax技术的封装

##### 6、提供了大量动画处理机制

and so on...

#### 4、使用JQ

1）本地引入（本地地址修改了需要重新下载引入）

```html
<script src="jquery-3.3.1.min.js"></script>
```

2）CDN引入(从网络引入)

```html
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/2.1.1/jquery.js"></script>
```

JQ必须先引入

3）后期一般用node安装

### 5、选择器

1. #### 基本选择器

   ###### id:   #id

   ###### class:  .class

   ###### 元素element：   element

   ###### *表示选择所有的标签（项目开发时不要用，因为他要匹配所有的标签，性能差）

   ###### ，表示选择多个DOM标签

2. #### 层次选择器

   ###### 1） 选择器1 选择器2： 表示选择器1的所有后代元素（即选择器2）

   ###### 2）选择器1>选择器2： 表示只选择选择器1的子元素

   ###### 3） 选择器1+选择器2： 表示选择紧挨着选择器1的第一个相邻元素（兄弟元素）

   ###### 4） 选择器1~选择器2： 表示选择选择器1的所有兄弟元素

   

3. #### 过滤选择器

   ##### 1）简单过滤选择器

   ：first 或 first（）   获取第一个元素

   ：last 或last（） 获取最后一个元素

   ：not(selector)   选择除selector之外的元素

   :  even   偶数

   :  odd    奇数

   :  eq(index)   第n个元素

   :   gt(index)    大于第n个后的元素

   :   lt(index)   小于第n个后的元素

   :  header        选择h1-h6所有的元素

   ##### 2）内容过滤选择器

   :contains(text)  获取包含指定文本内容的元素

   :empty   获取不包含子元素或文本内容的元素

   :has(selector)   获取含有选择器所匹配的元素

   :parent  获取含有子元素或文本的元素

   ##### 3）可见性过滤选择器

   ：hidden  选择display：none或隐藏文本域

   ：visible    选择display：block的元素

   ##### 4）属性过滤选择器

   [attr]   获取含有指定属性的元素

   [attr=value]   获取属性值为value的元素

   [attr!=value]   获取属性值不为value的元素

   [attr^=value]   获取属性值以value开头的元素

   [attr$=value]	获取属性值以value结尾的元素

   [attr*=value]  获取属性值含有value的元素

   【attr1】【attr2 】【attr3】  获取含有指定多个属性的元素

   

4. #### 表单选择器

   ：input      选择所有input标签

   ：button    选择所有按钮

   ：submit    选择所有提交

   ：text   选择文本框

   ：password   选择password

   

   ### 6、DOM操作

   ##### 1、属性操作

   1）获取属性值

   attr（属性名）

   2）设置属性

   attr（属性名，属性值）

   3）删除属性

   removeAttr（属性名）

   

##### 2、文本内容操作

1）获取文本及表单组件内容

html()   可以操作标签

text()    只能操作文本内容，不操作标签

val()    只能用于表单组件

2)设置（修改）文本内容及表单组件内容

html(内容)

text（内容）

val（内容）

3）删除文本及表单组件内容

html（' '）

text（' '）

val（' '）

##### 3、元素样式操作

1）设置样式

css(‘属性名’，‘属性值’)     设置一个样式

css（{‘属性名1’：‘属性值1’，‘属性名2’：‘属性值2’,..})

2)操作类

###### 1.添加类

addClass（‘类名’）

或：

addClass（‘类名1 类名2   ...’）

###### 2、删除类

removeClass（‘类名’）

或

removeClass（‘类名1 类名2   ...’）

#### 4、页面元素操作★

1）创建DOM节点

​		$(dom节点内容)

2）在**内部**添加节点 

​		append()//从后面加（在内部的最后加DOM）

​		appendTo()//从后面加（将DOM添加到内部后）

​		prepend()//从前面加（在内部的前面加DOM）

​		prependTo()//从前面加（将DOM添加到内部前）

3)在**外部**添加节点（同级添加）

​		before()  		在当前DOM前添加

​		insertBefore()		把DOM添加到当前元素前

​		after()  		在当前DOM后添加

​		insertAfter()  		把DOM添加到当前元素后

4）复制DOM节点

​		clone()			只复制DOM元素

​		clone(true)	复制DOM元素及绑定在他上面的事件

5）删除DOM节点

remove()				删除当前DOM及子元素

remove(dom节点)	 在同级DOM中删除指定的DOM

empty()		删除当前DOM下的子元素，保留当前DOM