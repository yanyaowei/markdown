### 1、Buffer(缓冲区)

 nodejs作为服务器要进行接受用户请求和数据返回响应，用户发的请求全是二进制数据，用户发的数据就都存到buffer里，把数据发送给用户时也要转换为二进制数据，发送前也要存在buffer中，所以buffer是缓冲区。



### 2、Buffer的操作 

##### • 将一个字符串转换为buffer

 Buffer.from(str)      

##### • 创建一个指定大小的buffer对象

 Buffer.alloc(size)

##### •创建一个指定大小的buffer，但是可能包含敏感数据

Buffer.allocUnsafe(size)

##### •把缓冲区中的数据转换为字符串

buf.toString()



js文件举例：

```js
/*
BUffer（缓冲区）
    Buffer的结构和数组很像，操作的方法也和数组类似
    数组中不能存储二进制文件，Buffer就是专门拿来存储二进制数据
    使用Buffer不需要引入模块，直接使用即可
    在Buffer中存储的都是二进制数据，但是在显示时都是以十六进制形式显示
    Buffer中的每一个元素的范围是00-ff    0-255   00000000-11111111
    计算机中一个0或者一个1，我们成为1位（bit）   8bit=1byte（字节）    1024byte=1kb     1024kb=1mb
    1个汉字占用3个字节
    Buffer中的一个元素占用内存的一个字节
    BUffer的大小一旦确定，不能修改
    BUffer里的空间都是连续的
*/
var str="hello小巍";
//将一个字符串保存到Buffer中
var buf=Buffer.from(str);
// console.log(buf);//输出  <Buffer 68 65 6c 6c 6f 6e 70 6d>
// console.log(buf.length);//占用内存的大小
// console.log(str.length);//字符串的长度

//创建一个指定大小的buffer
//buffer构造函数不推荐使用，已经弃用☟
// var buf2=new Buffer(10);//十个字节的buffer
// console.log(buf2.length);

//创建一个10字节的buffer
var buf2=Buffer.alloc(10);//alloc是分配的意思
// console.log(buf2);
//通过索引，来操作buf2中的元素
buf2[0]=88;//填进去的都会转换成16进制数
buf2[1]=255;//最大255
buf2[2]=0xaa;
buf2[3]=155;

//只要数字在控制台或者页面中输出一定是10进制
// console.log(buf2[2]);//10进制输出
// console.log(buf2[2].toString(16));//转换成16进制输出
// console.log(buf2[2].toString(2));//转换成2进制输出
//遍历也是用十进制输出
// for(var i=0;i<buf2.length;i++){
//     console.log(buf2[i]);
// }

var buf3=Buffer.allocUnsafe(10);//创建一个指定大小的buffer，但是buffer中可能有铭感数据
// console.log(buf3);


var buf4=Buffer.from("我是一段数据");
console.log(buf4.toString());//把缓冲区中的数据转换为字符串
```

