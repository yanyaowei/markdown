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

### 4、简单文件写入

简单文件写入也分同步+异步

##### fs.writeFile(file, data[, options], callback)

##### fs.writeFileSync(file, data[, options])

​    -file 要操作的文件的路径
​    -data 要写入的数据
​    -options 选项，可以对写入进行一些设置(可选)
​    -callback 当写入完成后执行的函数

​	-flag   
​    r 只读
​    w 可写
​    a 追加

举例：

```js
var fs=require("fs");
fs.writeFile("hello3.txt","这是第三个写入的文件",{flag:"w"},function (err){
    if(!err){
        console.log("写入成功");
    }else{
        console.log("error");
    }
})
```



### 5、打开状态

| 模式 |                          说明                           |
| :--: | :-----------------------------------------------------: |
|  ★r  |            `读取`文件, 文件不存在则出现异常             |
|  r+  |            `读写`文件, 文件不存在则出现异常             |
|  rs  |              在同步模式下打开文件用于读取               |
| rs+  |              在同步模式下打开文件用于读写               |
|  ★w  | 打开文件用于写操作 , 如果不存在则创建，如果存在则`截断` |
|  wx  |        打开文件用于写操作 , 如果 存在 则打开失败        |
|  w+  |     打开文件用于读写如果不存在则创建如果存在则截断      |
| wx+  |         打开文件用于读写 , 如果 存在 则打开失败         |
|  ★a  |          打开文件用于`追加` , 如果不存在则创建          |
|  ax  |          打开文件用于追加 , 如果路径存在则失败          |
|  a+  |     打开文件进行读取和追加 , 如果不存在则创建该文件     |
| ax+  |       打开文件进行读取和追加 , 如果路径存在则失败       |

### 6、同步异步简单文件写入都不适合大文件的写入，性能较差，容易导致溢出，因此有了   流式文件写入

```js
var fs=require("fs");
//流式文件写入
//创建一个可写流
/*
fs.createWriteStream(path[,options])
    -可以用来创建一个可写流
    -path，文件路径
    -options 配置的参数*/
var ws=fs.createWriteStream("hello3.txt");
//可以通过监听流的open和close事件来监听流的打开和关闭
/*
on(事件字符串，回调函数)
-可以为对象绑定一个事件
 once（事件字符串，回调函数）
 -可以为对象绑定一个一次性事件，该事件会在触发一次后失效
 */
ws.once("open",function (){
    console.log("流打开了");//打开只需要一次
});
ws.once("close",function (){
    console.log("流关闭了");
});
//通过ws向文件中输出内容
ws.write("通过可写流写入内容1");
ws.write("通过可写流写入内容2");
ws.write("通过可写流写入内容3");
ws.write("通过可写流写入内容4");

//关闭流
ws.end();
```

输出：

```txt
流打开了
流关闭了
```

hello3.txt:

```txt
通过可写流写入内容1通过可写流写入内容2通过可写流写入内容3通过可写流写入内容4
```

### 7、简单文件读取

##### fs.readFIle(path[,options],callback)

##### fs.readFileSync(path[,options])

​    -path 要读取的文件的路径
​    -options 读取的选项
​    -callback 回调函数，通过回调函数将读取到的内容返回
​        err 错误对象
​        data  读取到的数据，会返回一个Buffer



```js
var fs=require("fs");
fs.readFile("hello.txt",function (err,data){
    if(!err){
        // console.log(data);
        //将data写入到文件中,下面的这个相当于复制操作
        fs.writeFile("hello2.txt",data,function (err){
            if(!err){
                console.log("成功！");
            }
        })
    }
})
```

### 8、流式文件读取

适用于一些比较大的文件，可以分多次将文件读取到内存中

```js
var fs=require("fs");
//创建一个可读流
var rs=fs.createReadStream("hello3.txt");
//创建一个可写流
var ws=fs.createWriteStream("hello4.txt");

//监听流的开启和关闭
rs.once("open",function (){
    console.log("可读流打开了");
});
rs.once("close",function (){
    console.log("可读流关闭了");
    //可读流数据读取完毕关闭可写流
    ws.end();
});

ws.once("open",function (){
    console.log("可读流打开了");
});
ws.once("close",function (){
    console.log("可读流关闭了");
});

// 方法二：(不写data，直接用管道)
//pipe（）可以将可读流中的内容，直接输出到可写流中
rs.pipe(ws);


//方法一：（写data）
//如果要读取可读流中的数据，必须要为可读流绑定一个data事件，
// data事件绑定完毕后，他会自动开始读取数据
// rs.on("data",function (data){
//     // console.log(data.length);
//     //将读取到的数据写入到可写流中
//     ws.write(data);
// })
```

### 9、fs模块的其他方法

```js
var fs=require("fs");
/*1、
fs.existsSync(path)
检查一个文件是否存在
*/
// var isExists=fs.existsSync("hello.txt");
// console.log(isExists);

/*2、
   fs.stat(path,callback)
   fs.statSync(path)
   获取文件的状态
   */
// fs.stat("hello2.txt",function (err,stat){
        //  isFile（）  是否是一个文件
        //  isDirectory（）  是否是一个文件夹/目录
    // console.log(stat.isFile());
    // console.log(stat.isDirectory());
// });

/*3、
fs.unlink(path,callback)
fs.unlinkSync(path)
删除文件*/
// fs.unlinkSync("hello4.txt");

/*4、
fs.readdir(path[,options])
fs.readdirSync(path[,options])
读取一个目录的目录结构
    files是一个字符串数组，每一个元素就是一个文件夹或文件的名字
*/
// fs.readdir(".",function (err,files){
//     if(!err){
//         console.log(files);
//     }
// })

/*5、
fs.truncate(path,length,callback)
fs.truncateSync(path,length)
截断文件,将文件修改为指定的大小
*/
// fs.truncateSync("hello.txt",5);

/*6、
fs.mkdir(path,[,mode],callback)
fs.mkdirSync(path[,mode])
创建一个目录
*/
// fs.mkdirSync("hello");

/*
7、
fs.rmdir(path,callback)
fs.rmdirSync(path)
删除一个目录
*/
// fs.rmdirSync("hello");

/*8、
fs.rename(oldPath,newPath,callback)
fs.renameSync(oldPath,newPath)
对文件进行重命名
参数：
    oldPath 旧的路径
    newPath 新的路径
    callback 回调函数
    */
// fs.rename("hello3.txt","helloa.txt",function (err){
//     if(!err){
//         console.log("修改成功");
//     }
// });//重复名操作
// fs.rename("hello.txt","C:\\Study\\node\\hello.txt",function (err){
//     if(!err){
//         console.log("修改成功");
//     }else {
//         console.log(err);
//     }
// });//相当于剪切

/*9、
fs.watchFile(filename[,options],listener)
监视文件的修改
参数：
    filename  要监视的文件
    options  配置选项
    listener  回调函数，当文件发生变化时，回调函数会执行
        在回调函数中会有两个参数{
            curr 当前文件的状态
            prev 修改前文件的状态
                这两个都是stats对象
*/
// 设置options：interval：1000  表示每隔1秒监视一次，吃性能
fs.watchFile("hello.txt",{interval:1000},function (curr,prev){
    console.log("修改前文件大小:"+prev.size);
    console.log("修改后文件大小:"+curr.size);
});
```