#Html学习笔记(4)-Html标签(3)

标签（空格分隔）： html primer 标签

---

##[1.无序信息列表标签](http://www.imooc.com/code/288)
ul-li是**没有前后顺序**的信息列表。

**语法：**

```html
<ul>
    <li>信息</li>
    <li>信息</li>
    ..........
</ul>
```

**eg.**

```html
<ul>
    <li>精彩少年</li>
    <li>美丽突然出现</li>
    <li>触动心灵的旋律</li>
</ul>
```

ul-li在网页中显示的默认样式一般为：每项li前都自带一个圆点，如下图所示：

![ul-li](http://img.mukewang.com/52d3851200012ec503870284.jpg)

###[`<li>`列表项目标签](http://www.w3school.com.cn/tags/tag_li.asp)
`<li>`标签可用在有序列表`<ol>`和无序列表`<ul>`中

**注意：**要使用CSS来定义列表和列表项目的类型

**可选属性**

|属性           |值             |描述           |
|-------        |-------      |  ------- |
|type           |A,a,I,i,1,disc,square,circle|**不赞成使用。**请使用css样式取代。规定使用哪种项目符号|
|value  |number |**不赞成使用。**请使用css样式取代。规定列表项目的数字。|

##[2.有序列表项目标签](http://www.imooc.com/code/289)
如果想要在网页中展示有**前后顺序**的信息列表，那么可以使用`<ol>`标签来制作**有序列表**来展示。

**语法：**

```html
<ol>
   <li>信息</li>
   <li>信息</li>
   ......
</ol>
```

**eg.**

```html
<ol>
   <li>前端开发面试心法 </li>
   <li>零基础学习html</li>
   <li>JavaScript全攻略</li>
</ol>
```

`<ol>`在网页中默认样式一般为：每项`<li>`前都自带一个**序号**，序号默认从`1`开始。

![ul](http://img.mukewang.com/52d3893400019ee003830208.jpg)

##[3.逻辑容器标签](http://www.imooc.com/code/290)
在网页制作过程过中，可以把一些独立的逻辑部分划分出来，放在一个`<div>`标签中，这个`<div>`标签的作用就相当于一个容器。

**语法：**

> * `<div>...</div>`

**确定逻辑部分：**
它是页面上相互关联的一组元素。如网页中的独立的栏目版块，就是一个典型的逻辑部分。如下图所示：图中用红色边框标出的部分就是一个逻辑部分，就可以使用`<div>`标签作为容器。

![luoji](http://img.mukewang.com/52d38c41000163e210120455.jpg)

###[身份标识id](http://www.imooc.com/code/291)
为了使逻辑更加清晰，我们可以为这一个独立的逻辑部分设置一个名称，用`id`属性来为`<div>`提供唯一的名称，这个就像我们每个人都有一个身份证号，这个身份证号是唯一标识我们的身份的，也是**必须唯一**的。

**语法：**

> * `<div  id="版块名称">…</div>`

##[4.表格标签](http://www.imooc.com/code/292)
在网页上显示表格，需要用到表格标签`<table>`。

**创建表格的元素：**

**table、tbody、tr、th、td**

> 1、`<table>…</table>`：整个表格以`<table>`标记开始、`</table>`标记结束。

> 2、`<tbody>…</tbody>`：当表格内容非常多时，表格会下载一点显示一点，但如果加上`<tbody>`标签后，这个表格就要等表格内容全部下载完才会显示。如右侧代码编辑器中的代码。

> 3、`<tr>…</tr>`：表格的一行，所以有几对tr 表格就有几行。

> 4、`<td>…</td>`：表格的一个单元格，一行中包含几对`<td>...</td>`，说明一行中就有几列。

> 5、`<th>…</th>`：表格的头部的一个单元格，表格表头。

> 6、表格中列的个数，取决于一行中数据单元格的个数

**注意：**

> 1、table表格在没有添加css样式之前，在浏览器中显示是没有表格线的

> 2、表头，也就是th标签中的文本默认为粗体并且居中显示

###[用CSS样式为表格加边框](http://www.imooc.com/code/293)
可以用css样式为表格增加边框。

**基本语法：**

用css样式代码为`th`， `td`单元格添加粗细为一个像素的黑色边框。

```html
<style type="text/css">
table tr td,th{border:1px solid #000;}
</style>
```

![biankuang](http://img.mukewang.com/52d3993b00010d6203900285.jpg)

###[表格标题和摘要标签](http://www.imooc.com/code/294)

####摘要`<table summary="">`
摘要的内容是不会在浏览器中显示出来的。它的作用是增加表格的可读性(语义化)，使搜索引擎更好的读懂表格内容，还可以使屏幕阅读器更好的帮助特殊用户读取表格内容。

**语法：**

> * `<table summary="表格简介文本">`

####标题`<caption>`
用以描述表格内容，标题的显示位置：表格上方。

**语法：**

```html
<table>
    <caption>标题文本</caption>
    <tr>
        <td>…</td>
        <td>…</td>
        …
    </tr>
…
</table>
```

---
作者：Skyeyes
2015.11.17
本文根据[爱慕课网HTML+CSS基础(www.imooc.com)](https://www.imooc.com/learn/9)和[w3school](http://www.w3school.com.cn/index.html)总结





