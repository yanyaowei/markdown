# 文件系统fs（File System）

##### ------------------------------通过Node来操作系统中的文件

•使用文件系统，需要先引入fs模块，fs是核心模块，直接引入不需要下载

• 在Node中，与文件系统的交互是非常重要的，服务器的本质就将本地的文件发送给远程的客户端

• Node通过fs模块来和文件系统进行交互

• 该模块提供了一些标准文件访问API来打开、 读取、写入文件，以及与其交互。

• 要使用fs模块，首先需要对其进行加载 

### 1、fs的同步和异步调用

 • fs模块中所有的操作都有两种形式可供选择 `同步`（带Sync）和`异步`。

 • `同步`文件系统会`阻塞`程序的执行，也就是除非操作完毕，否则不会向下执行代码。

 • `异步`文件系统`不会阻塞`程序的执行，而是在操作完成时，通过回调函数将结果返回。



### 2、同步文件的写入：

#####    1.打开文件

#####       fs.openSync(path,flags[,mode])

​        -path  是指要打开文件的路径
​        -flags  是指打开文件要做的操作的类型
​            r 只读的
​            w 可写的
​        -mode  是指设置文件的操作权限，一般不传

#####       该方法会返回一个文件的描述符作为结果，我们可以通过该描述符来对文件进行各种操作

#####    2.向文件中写入内容

#####       fs.writeSync(fd,string[,position[,encoding]])

​        -fd  文件的描述符，需要传递要写入的文件的描述符
​        -string 要写入的内容
​        -position 写入的起始位置
​        -encoding 写入的编码，默认的是UTF-8

#####    3.保存并关闭文件（不关的话会一直占用内存空间）

​      fs.closeSync(文件名);

举例：

```js
var fs=require("fs");//文件系统fs（File System）
//同步文件的写入：
var fd=fs.openSync("hello.txt","w");//打开文件
// fs.writeSync(fd,"你小子可以的");//从头开始向文件中写入内容
fs.writeSync(fd,"你小子可以的",3);//从3后开始向文件中写入内容
fs.closeSync(fd);//关闭文件
```



### 3、异步文件的写入：

##### 1.打开文件：

#####     fs.open(path,flags[,mode],callback)

​       -异步调用方法，结果都是通过回调函数的参数返回的
​       -回调函数的参数：
​         err 错误对象：如果没有错误，则为null
​         fd  文件的描述符

##### 2.写文件

​    fs.write(fd,string[,position[,encoding]],callback)
​    -异步写入一个文件

##### 3.关闭文件

​    fs.close(fd,callback)

举例：

```js
//引入fs模块
var fs=require("fs");
//打开文件
fs.open("hello2.txt","w",function (err,fd){
    //判断是否出错
    if(!err){
        //如果没有错误，则对文件进行写入操作
        fs.write(fd,"异步操作内容",function (err){
            if(!err){
                console.log("写入成功");
            }
            //关闭文件
            fs.close(fd,function (err){
                if(!err){
                    console.log("文件已关闭");
                }
            })

        });

    }else {
        console.log(err);
    }
});

console.log("异步请等我完成了再执行");
```

输出：

```txt
异步请等我完成了再执行
写入成功
文件已关闭
```

