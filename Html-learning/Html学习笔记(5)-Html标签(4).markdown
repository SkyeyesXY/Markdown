#Html学习笔记(5)-Html标签(4)

标签（空格分隔）： html primer 标签

---
##[1.地址链接标签](http://www.imooc.com/code/315)
使用`<a>`标签可实现超链接，它在网页制作中可以说是无处不在，只要有链接的地方，就会有这个标签。

**语法：**

> `<a  href="目标网址"  title="鼠标滑过显示的文本">链接显示的文本</a>`

###title属性的作用
**eg.**

> `<a  href="http://www.imooc.com"  title="点击进入慕课网">click here!</a>`

上面例子作用是单击`click here!`文字，网页链接到`http://www.imooc.com`这个网页。

`title`属性的作用，鼠标滑过链接文字时会显示这个属性的文本内容。这个属性在实际网页开发中作用很大，主要方便搜索引擎了解链接地址的内容（语义化更友好）。

**注意：**只要为文本加入a标签后，文字的颜色就会自动变为蓝色（被点击过的文本颜色为紫色）,样式效果可以用css样式来修改。

###[在新建浏览器窗口中打开链接](http://www.imooc.com/code/316)
`<a>`标签在默认情况下，链接的网页是在当前浏览器窗口中打开，有时我们需要在新的浏览器窗口中打开。只需要加入`target="_blank"`属性。

**eg.**

>` <a href="目标网址" target="_blank">click here!</a>`


###[使用mailto在网页中链接Email地址](http://www.imooc.com/code/317)
`<a>`标签还有一个作用是可以链接Email地址，使用**mailto**能让访问者便捷向网站管理者发送电子邮件。我们还可以利用mailto做许多其它事情。

![mailto](http://img.mukewang.com/52da4f2a000150b714280550.jpg)

**注意：**如果mailto后面同时有多个参数的话，第一个参数必须以“`?`”开头，后面的参数每一个都以“`&`”分隔。

##[2.图片标签](http://www.imooc.com/code/318)
可以使用`<img>`标签来插入图片。

**语法：**
> `<img src="图片地址" alt="下载失败时的替换文本" title = "提示文本">`

**注意：**
> 1、src：标识图像的位置；

> 2、alt：指定图像的描述性文本，当图像不可见时（下载不成功时），可看到该属性指定的文本；

> 3、title：提供在图像可见时对图像的描述(鼠标滑过图片时显示的文本)；

> 4、图像可以是GIF，PNG，JPEG格式的图像文件。

---
作者：Skyeyes
2015.11.17
本文根据[爱慕课网HTML+CSS基础(www.imooc.com)](https://www.imooc.com/learn/9)和[w3school](http://www.w3school.com.cn/index.html)总结



