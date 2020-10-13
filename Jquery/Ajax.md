# 一、Ajax介绍

### 1、什么是Ajax

Ajax（Asynchronous JavaScript And Xml：一步的JavaScript和XML）

##### 目的是让JavaScript发送http请求，与后台通信，获取数据和信息。

##### Ajax技术的原理是实例化xmlhttp对象，使用此对象与后台通信。在通信过程中不会影响后续的JS执行，从而实现异步操作。

### 2、什么叫同步和异步★

##### 同步就是做完一件事后再做另一件事，后一件的事执行依赖于前一件事的完成。（同步会影响到后面的JS代码执行时间）

##### 异步是指同时可以做很多事情（多任务）（异步不会影响到后面JS代码的执行时间）。

### 3、局部刷新和“无刷新”

Ajax可以实现局部刷新，也叫无刷新，就是整个页面不刷新，只是局部刷新（刷新一些部分，不是整个页面刷新，所以说“无刷新”）

##### Ajax可以自己发送请求，不用通过浏览器地址栏，所以页面不会刷新

# 二、用Ajax发送请求

方法一：

```html
$.ajax({

	type:'get/post'	，	     			 //请求的方式,默认为get

	url:'请求的文件名或接口地址'，			 //请求的地址

	async:true/false，				    //true表示异步，false表示同步

	data:{								 //表示上传到服务器端的数据
	//数据
	}，

	dataType:'json/jsonp/xml/text/javascript',//返回的数据类型或解决跨域（jsonp）

	success:function(res){				 //成功回调的处理
		//成功回调的处理代码
		}，

	error:function(err){				//失败回调的处理
		//失败回调的处理代码
		}，

	timeout:时间（毫秒），				   //请求超时时间
	...
})
```

或者把成功失败修改一下，如下

方法二：

```html
$.ajax({

	type:'get/post'	，	     			 //请求的方式,默认为get

	url:'请求的文件名或接口地址'，			 //请求的地址

	async:true/false，				    //true表示异步，false表示同步

	data:{								 //表示上传到服务器端的数据
	//数据
	}，

	dataType:'json/jsonp/xml/text/javascript',//返回的数据类型或解决跨域（jsonp）

	timeout:时间（毫秒），				   //请求超时时间
	...
}).done(function(){						//成功回调的处理
	...

}).fail(function(){						//失败回调的处理
	...

})
```

方法三：(推荐这个写法！！！)

```html
$.ajax({

	type:'get/post'	，	     			 //请求的方式,默认为get

	url:'请求的文件名或接口地址'，			 //请求的地址

	async:true/false，				    //true表示异步，false表示同步

	data:{								 //表示上传到服务器端的数据
	//数据
	}，

	dataType:'json/jsonp/xml/text/javascript',//返回的数据类型或解决跨域（jsonp）

	timeout:时间（毫秒），				   //请求超时时间
	...
	}).then(function(){					//成功回调的处理
	...
	}).catch(function(){				//失败回调的处理
	...
	})
```

# 三、JSONP

## 1、同源策略

​		1）同源策略 是由NetScape提出的一个著名的安全策略。

#####       2）所谓的同源，指的是协议，域名，端口相同。

​        3）浏览器处于安全方面的考虑，只允许本域名下的接口交互，不同源的客户端脚本，在没有明确授权的情况下，不能读写对方的资源。

#####       4）http://127.0.0.1:8080  http为协议，127.0.0.1为域名，8080为端口。

##### 	  5）只要协议、域名和端口中任意一个不相同，就会出现跨域情况。

### 2、在JQ中解决跨域

```html
$.ajax({
	...
	dataType:'jsonp',
	...
}).then(function(){
	...
})
```

### 用dataType：‘jsonp’