### 1、尺寸

##### 1）获取和设置元素的尺寸

$(dom).width（）/height() 获取元素的宽度/高度

$(dom).innerWidth（）/innerHeight() 获取包括padding的宽度/高度

$(dom).outerWidth（）/outerHeight()  获取包括padding和border的宽度/高度

$(dom).outerWidth（true）/outerHeight(true)获取包括padding和border和margin的宽度/高度

##### 2）获取相对页面的绝对位置

offset（）

##### 3）获取浏览器可视区放入宽高

$(window).width()

$(window).height()

##### 4)获取页面文档的宽高

$(document).width()

$(document).height()

##### 5）获取页面滚动距离

$(document).scrollTop()

$(document).scrollLeft()

### 2、遍历DOM

##### index为下标，dom为遍历的每一个元素

```javascript
$(dom).each(function(index，dom){

	...

})
```

### 3、事件

click（）  鼠标点击

mouseover（） 鼠标进入

mouseout（）鼠标离开

mouseenter（）  鼠标进入

keydown（）按下键盘键

keyup（） 松开键盘键

focus（）  元素获得焦点

blur（）  元素失去焦点

submit（）  用户递交表单

hover（）  同时为mouseenter和mouseleave事件指定处理函数

ready（） DOM加载完成

resize（） 浏览器窗口的大小发生变化

scroll（） 滚动条的位置发生变化

### 4、动画

##### 1）显示/隐藏/切换

show()		显示

hide()		隐藏

toggle()		显示隐藏的切换

##### 2)滑动

slideDown（）	  向下滑动

slideUp（） 		向上滑动

##### 3）淡入淡出

fadeIn（）	淡入

fadeOut（）	淡出

fadeTo()	淡入到指定不透明度

##### 4）动画

animate()	

支持以下属性：

​			backgroundPosition
​            borderWidth
​            borderBottomWidth
​            borderLeftWidth
​            borderRightWidth
​            borderTopWidth
​            borderSpacing
​            margin
​            marginBottom
​            marginLeft
​            marginRight
​            marginTop
​            outlineWidth
​            padding
​            paddingBottom
​            paddingLeft
​            paddingRight
​            paddingTop
​            height
​            width
​            maxHeight
​            maxWidth
​            minHeight
​            maxWidth
​            font
​            fontSize
​            bottom
​            left
​            right
​            top
​            letterSpacing
​            wordSpacing
​            lineHeight
​            textIndent