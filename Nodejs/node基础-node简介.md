#### Node.js是一个能够在服务器端运行JavaScript的开放源代码、跨平台JavaScript运行环境。

Node.js之父 瑞安达尔（Ryan Dahl）

### Node

1、Node是对ES标准一个实现，Node也是一个JS引擎，通过Node可以使js代码在服务器端执行
2、Node仅仅对ES标准进行了实现，所以在Node中不包含DOM 和 BOM

3、Node中可以使用所有的内建对象String Number Boolean Math Date RegExp Function Object Array，而BOM和DOM都不能使用，但是可以使用 console ，也可以使用定时器（setTimeout() setInterval()）

4、Node可以在后台来编写服务器，Node编写服务器都是单线程的服务器

传统的服务器都是多线程的每进来一个请求，就创建一个线程去处理请求

Node的服务器`单线程`的，Node处理请求时是单线程，但是在后台拥有一个I/O线程池

### Node的用途

 • Web服务API，比如REST
 • 实时多人游戏
 • 后端的Web服务，例如跨域、服务器端的请求
 • 基于Web的应用
 • 多客户端的通信，如即时通信



如何执行：

##### 进入目录   node test.js

##### 在webstorm里右键 RUN