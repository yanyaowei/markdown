# JSON和DOM操作

## 1.JSON

​    JSON(JavaScript Object Natation：JS对象表示法）是一种轻量级的数据交换格式。用独立的编程语言的文本格式来存储和表示数据。

#####     1）优点

​        易于阅读和编写，同时也易于浏览器解析和生成，并有效地提升网络传输效率。

#####     2）与XML比较

​        JSON书写或解析时是一个对象，更容易解析；而XML是由用户自定义标签来存储数据的，对于前端来说，不容易书写且解析起来比较困难。

#####     3）JSON文件内容

​        它可以是一个单值，也可以是一个对象，也可以是一个数组，也可以是对象和数组的结合。

#####     4）JSON写在哪里

​        可以写在JavaScript代码中，也可以形成一个独立的.json文本文件。

######         a.在JS中书写JSON数据

​            值如果是字符串，可以用单或双引号引起来，数值型数据和逻辑值以及null不能加引号；
​            如果是对象，键可以用单或双引号引起来，也可以不加引号。

######         b.独立的JSON文件

​            i)文件的扩展名必须是.json，JSON文件不是JS文件，不能出现任何的JS代码，它只是一个文本文件布而已；
​            ii)数据不能赋给某个变量；
​            iii)键必须用双引号引起来；
​            iv)值如果是字符型数据，必须用双引号引起来，其它类型的数据不能用引号引；
​            v)在JSON文件中不能添加任何注释。

#####     5）数据值可以有以下三种

​        ①简单值：可以在JSON中表示字符串、数值、布尔值和null。但JSON不支持JavaScript中的特殊undefined。
​        ②对象（{}）
​        ③数组（[]）

#####     6）在实际开发中的数据处理

​        在实际项目开发中，如果后台工程师还没创建好后台数据接口时，前端工程师可以先做数据mock（模拟），写对应的HTML、CSS和JS代码，
​    等后台数据可以调用时，再进行替换即可。
​        在项目开发中，数据最好分离出来，形成单独的JSON文件。

#####     7）解析JSON数据

######         a)JS中JSON

​            如果是JSON数据，可以直接访问；如果是JSON格式的字符串需要用JSON.parse()方法进行转换。

​        JSON.parse()：将JSON格式的字符串转换为JSON
​        JSON.stringify()：将JSON转换为JSON格式的字符串

######     b)解析JSON文件

​        JSON文件必须用ajax（异步请求）技术去获取。

## 2.ajax请求操作步骤：

#####     1）创建请求对象

​      var xhr = new XMLHttpRequest();

#####     2）建立请求连接

​      xhr.open('get',url,true);// get/post：请求方式 true/false：true表示异步请求,false表同步操作 url：表示请求的路径

#####     4）前端对请求的结果进行处理

​      xhr.onreadystatechange = function () {
​        if(xhr.readyState == 4 && xhr.status == 200){ // 如果请求成功
​          console.log(JSON.parse(xhr.responseText)); // responseTextr：获取请求的结果
​        }
​      };

#####      3）向后台发送请求

​      xhr.send();

    注意：如果发送ajax请求，必须以http（服务器端）的方式启动文件，不能在本地直接打开。
## 3.DOM操作

​    DOM（Document Object Model:文档对象模型）：是HTML和XML文档的编程接口，定义了访问和操作HTML和XML文档的标准方法。
​    DOM以树型目录结构表达HTML和XML文档的，每一个节点就是一个DOM元素。
​        document->html->head/body->...

#####     1）DOM节点

######         a）节点层次

​            节点层次分为父子节点和同胞节点两种。
​                在节点树中，顶端节点被称为根（root）
​                每个节点都有父节点、除了根（它没有父节点）
​                一个节点可拥有任意数量的子节点
​                同胞节点是拥有相同父节点的节点，也叫兄弟节点

######         b）DOM节点分类

​            元素节点：标签
​            属性节点：标签的属性
​            文本节点：标签后的换行符
​            文档节点：document

######         c）DOM节点的名称（nodeName）

​            元素节点 标签名相同
​            属性节点 属性名相同
​            文本节点 #text
​            文档节点 #document

######         d）DOM节点的值（nodeValue）

​            元素节点 undefined 或 null
​            属性节点 属性值
​            文本节点 文本内容

######         e）DOM节点的类型（nodeType）

​            元素 1
​            属性 2
​            文本 3
​            注释 8
​            文档 9

#####     2）节点操作

######         a）获取节点

​            通过ID获取节点 【返回具体某个节点】
​                document.getElementById(ID名)
​            通过标签名获取节点 【返回节点数组，即使只有一个】
​                document.getElementsByTagName(标签名)
​            通过标签的name值获取节点 【返回节点数组】
​                document.getElementsByName(Name名)
​            通过class值来获取节点 【返回节点数组】
​                document.getElementsByClassName(Class名)
​            根据选择器返回找到结果集中的第一个
​                document.querySelect("选择器")
​            根据选择器返回找到的结果集，是个节点数组
​                document.querySelectAll("选择器")

######         b）创建DOM节点

​            i)创建元素节点
​                document.createElement('标签名');
​            ii)创建文本节点
​                document.createTextNode('文本内容');
​            iii)创建属性节点
​                document.createAttribute('属性名');
​                属性节点名.value = '属性值'; // 为属性设置值

​          // 关联以上三个节点
​          元素节点名.appendChild(文本节点名); // 在元素节点上添加文本节点
​          元素节点名.setAttributeNode(属性节点名); // 在元素节点上添加属性节点

​          document.body.appendChild(元素节点名); // 将创建的节点添加到文档中

​    简洁写法：
​        var oDiv = document.createElement('div'); // 创建元素节点
​        oDiv.setAttribute('class','wrapper box'); // 为元素节点添加属性及属性值
​        oDiv.innerHTML = '创建DOM元素的简洁写法';  // 为元素节点设置文本内容
​        document.body.appendChild(oDiv); // 将创建的元素节点添加到文档中

##### 3）插入节点

​    i)插入内部的尾部
​        父节点.appendChild(创建的节点)
​    ii)插入内部的某个前面
​        父节点.insertBefore(创建的节点,已知的子节点)

##### 4）替换节点

​    父节点.replaceChild(新节点，老节点)

##### 5）克隆节点

  深度克隆： 包含子节点一起克隆。
  浅克隆： 只会将找到的这个节点克隆，子节点不会克隆

​    需要被复制的节点. cloneNode(true/false);
​        true: 复制当前节点以及所有子节点（深度克隆）
​        false: 仅复制当前节点（浅克隆）

##### 6）删除节点

​    i)删除当前节点及子节点
​        节点.remove();
​    ii)删除子节点
​        父节点.removeChild(子节点)

##### 7）节点属性操作

​    i)获取属性值
​        DOM节点.属性名   // 不能获取用户自定义属性的值
​        DOM节点.getAttribute(属性名)  // 获取所有属性（用户自定义属性）的值
​    ii)设置属性值
​        DOM节点.属性名 = 属性值   // 不能设置用户自定义属性的值
​        DOM节点.setAttribute(属性名, 属性值)  // 设置所有属性（用户自定义属性）的值
​    iii)删除属性值
​        DOM节点.属性名 = ''   // 不能删除用户自定义属性
​        DOM节点.removeAttribute(属性名)  // 删除所有属性（用户自定义属性）

##### 8）节点文本操作

######     i) 获取文本

#####         节点.innerHTML //获取节点下的所有内容包含了标签

#####         节点.innerText // 获取节点下的文本内容，会过滤掉标签

#####         节点.value // 获取input输入框等表单控件的内容

#####         节点.getAttribute(“value”) //value是表单输入框的属性，可以使用getAttribute获得value值

######     ii)设置文本

#####         节点.innerHTML= "文本内容" // 会翻译html标签

#####         节点.innerText = "文本内容" // 不会翻译html标签

#####         节点.value = 值

#####         节点.setAttribute("value",值) // 因为value是属性，所以也可以中这个方法设置内容

######     iii)删除文本

#####         节点.innerHTML= ""

#####         节点.innerText = ""

#####         节点.value = ""

#####         节点.removeAttribute("value")

##### 9）DOM节点样式操作

######     a)操作样式class

​        i)获取class

#####             节点.className 获取节点的所有class

#####             节点.getAttribute("class") 获取节点的所有class

​        ii)设置class

#####             节点.className = 值

#####             节点.setAttribute("class",值)

​        iii)其它方法

#####             节点.classList.add(value); //为元素添加指定的类

#####             节点.classList.contains(value); // 判断元素是否含有指定的类，如果存在返回true

#####             节点.classList.remove(value); // 删除指定的类

#####             节点.classList.toggle(value); // 有就删除，没有就添加指定类

######     b)操作内联样式

​        i)获取内联样式
​            节点.style.样式属性名 // 获取某个具体的内联样式
​            节点.style.cssText // 获取某个节点的所有内联样式，返回字符串
​        ii)设置内联样式
​            节点.style.样式属性名 = 属性值  // 设置某个具体的内联样式
​            节点.style.cssText = 属性值或属性值列表 // 设置某个节点的所有内联样式



## 4.常用事件触发

 onload页面加载自动启动

 onclick 单击

ondblclick 双击

##### onmouseover鼠标移入

#####  onmouseout鼠标移出

 onmousemove移动鼠标

 onmousedown按下鼠标键

 onmouseout松开鼠标键

 onblur 失焦

onfocus获得焦点

 onsubmit提交事件

 onrest重置

 onchange 会在域的内容改变时发生

 onkeydown按下键盘任意键

onkeyup 松开键盘键

onkeypress输入某个字符
   onresize 会在窗口或框架被调整大小时发生 



console.dir(document)可以看到包含时事件