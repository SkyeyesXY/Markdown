#Html学习笔记(3)-Html标签(2)

标签（空格分隔）： html 标签 primerer

---
##[1.分行显示文本标签](http://www.imooc.com/code/97)
在需要加回车的地方加入`<br />`标签。

**语法：**

> * `<br />`(xhtml1.0中的写法，规范写法)
> * `<br>`(html4.01中的写法)

```html
<hr>...</hr>
<p>
.....<br />
.....<br />
</p>
```

**注意**:

> * `<br />`为空标签（没有html内容的标签），只需要写一个开始标签，eg.`<br />`, `<hr />`, `<img />`为空标签。

在 html 中是忽略回车和空格的

eg.
![huiche1](http://img.mukewang.com/5292ec400001f2f003370176.jpg)

上面的代码在浏览中显示是没有回车效果的。

![kongge2](http://img.mukewang.com/5292ec740001fdcd05810242.jpg)

**总结：在 html代码中输入回车、空格都是没有作用的。在html文本中想输入回车换行，就必须输入`<br />`。**

##[2.空格标签](http://www.imooc.com/code/99)
在html中输入**空格，回车，tab等**是没有效果的*(但会都表现出一个空格的bug)*
要输入空格，必须写入`&nbsp;`.

**语法：**

> * `&nbsp;`

**eg.**
![kongge](http://img.mukewang.com/529325ad0001f9a104940133.jpg)

在浏览器中的显示出来的空格效果:
![kongge2](http://img.mukewang.com/529325cf0001eb0c04590266.jpg)

##[3.水平横线标签](http://www.imooc.com/code/100)
**语法：**

> * (html4.01)`<hr>`
> * (xhtml1.0)`<hr />`*(规范用法)*

**注意：**

> * `<hr />`标签也是**空标签**，所以只有一个开始标签，没有结束标签。
> * `<hr />`标签的在浏览器中的默认样式线条比较粗，颜色为灰色，这些外在样式可以用css修改。

##[4.地址信息标签](http://www.imooc.com/code/101)
声明为**地址**(家庭住址，邮箱地址等),**签名**或者**作者身份**等所用的标签。

**语法：**
> * `<address>地址信息</address>`

**eg.**

```html
<address>
本文的作者：<a href="">SkyeyesXY</a>
</address>
```

在浏览器上显示的样式为**斜体**,可以用css修改`<address>`标签的默认样式。

##[5.行代码标签](http://www.imooc.com/code/144)
在网页中输入**行代码**时，使用`<code>`标签。

**语法：**
> * `<code>代码</code>`

**注意：**只能插入行代码。

##[6.块代码](http://www.imooc.com/code/145)
在网页中输入**大段代码**，使用`<pre>`标签。

**语法：**

> * `<pre>语言代码段</pre>`

`<pre>`标签的主要作用：预格式化的文本。被包围在pre元素中的文本通常会保留空格和换行符等。

**eg.**

```html
<pre>
    var message="欢迎";
    for(var i=1;i<=10;i++)
    {
        alert(message);
    }
</pre>
```

在浏览器中的显示结果为：

![daimakuai](http://img.mukewang.com/52a51a4f000118c403790224.jpg)

> * **注意：**`<pre>`标签不只是为显示计算机的源代码时用的，在你需要在网页中预显示格式时都可以使用它，只是`<pre>`标签的一个常见应用就是用来展示计算机的源代码。

---
作者：Skyeyes
2015.11.17
本文根据[爱慕课网HTML+CSS基础(www.imooc.com)](https://www.imooc.com/learn/9)总结






