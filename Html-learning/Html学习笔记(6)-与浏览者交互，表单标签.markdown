#Html学习笔记(6)-与浏览者交互，表单标签

标签（空格分隔）： html primer 标签 表单 交互

---

##[1.使用表单标签，与用户交互](http://www.imooc.com/code/415)
使用HTML表单(form)，可以把浏览者输入的数据传送到服务器端，这样服务器端程序就可以处理表单传过来的数据。

**语法：**
> `<form method="传送方式" action="服务器文件">`

**讲解：**
> * 1.`<form>`标签是成对出现的，以`<form>`开始，以`</form>`结束。
> * 2.**action**：浏览者输入的数据被传送到的地方，比如一个PHP页面(save.php)。
> * 3.**method**：数据传送的方式(get/post)。

**eg.**
```html
<form    method="post"   action="save.php">
        <label for="username">用户名:</label>
        <input type="text" name="username" />
        <label for="pass">密码:</label>
        <input type="password" name="pass" />
</form>
```

**注意：**

> 1、所有表单控件（文本框、文本域、按钮、单选框、复选框等）都必须放在`<form></form>`标签之间（否则用户输入的信息提交不到服务器）。
> 2、**method中get/post的区别：**
Get将表单中数据的按照variable=value的形式，添加到action所指向的URL后面，并且两者使用“?”连接，而各个变量之间使用“&”连接；Post是将表单中的数据放在form的数据体中，按照变量和值相对应的方式，传递到action所指向URL。
Get安全度低，传输的数据量小，一般限制在2KB左右，但是执行效率却比Post方法好。
**所以尽量使用Post方法**

###[input标签初步](http://www.w3school.com.cn/tags/tag_input.asp)
**定义和用法：**
`<input>` 标签用于搜集用户信息。根据不同的 type 属性值，输入字段拥有很多种形式。输入字段可以是文本字段、复选框、掩码后的文本控件、单选按钮、按钮等等。

> * 在HTML中，`<input>`标签没有结束标签
> * 在XHTML中，`<input>`标签必须被正确地关闭。
> * 要使用 label 元素为某个表单控件定义标签。

###[label标签](http://www.w3school.com.cn/tags/tag_label.asp)
**定义和用法：**
`<label>` 标签为 input 元素定义标注（标记）。
label 元素不会向用户呈现任何特殊效果。不过，它为鼠标用户改进了可用性。如果您在 label 元素内点击文本，就会触发此控件(**绑定的相关元素，表单**)。就是说，当用户选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。
`<label>` 标签的 for 属性应当与相关元素的 id 属性相同。(**表单的id**)

**语法：**
> * `<label for="控件id名称">`

**注意：**
> "for" 属性可把 label 绑定到另外一个元素。请把 "for" 属性的值设置为相关元素的 id 属性的值。
> `<label for="相关元素的id>`表单的名称`</label>`

**eg.**
```html
<form>
    <label for="male">男</label>
    <input type="radio" name="gender" id="male" />
    <br />
    <label for="female">女</label>
    <input type="radio" name="gender" id="female" />
    <label for="email">输入你的邮箱地址</label>
    <input type="email" id="email" placeholder="Enter email">
</form>
```

##[2.文本，密码输入框（input标签）](http://www.imooc.com/code/479)
当用户要在表单中键入字母、数字等内容时，就会用到文本输入框`<input>`标签。文本框也可以转化为密码输入框。

**语法：**
```html
<form>
   <input type="text/password" name="名称" value="文本" />
</form>
```

> * 1、type：当type="text"时，输入框为文本输入框;当type="password"时, 输入框为密码输入框。
> * 2、name：为文本框命名，以备后台程序ASP 、PHP使用。
> * 3、value：为文本输入框设置默认值。(一般起到提示作用)
> * 4、当`<input>`前后有文字时，不加`/`

**eg.**
```html
<form>
  姓名：
  <input type="text" name="myName">
  <br/>
  密码：
  <input type="password" name="pass">
</form>
```

在浏览器中显示的结果：

![shurukuang](http://img.mukewang.com/52e4e9be000152ca05250275.jpg)

##[3.多行输入文本域](http://www.imooc.com/code/489)
当用户需要在表单中输入大段文字时，需要用到文本输入域。

**语法：**
> `<textarea  rows="行数" cols="列数">文本</textarea>`

> * 1、`<textarea>`标签是成对出现的，以`<textarea>`开始，以`</textarea>`结束。
> * 2、cols ：多行输入域的列数。
> * 3、rows ：多行输入域的行数。
> * 4、在`<textarea></textarea>`标签之间可以输入默认值。

**eg.**
```html
<form  method="post" action="save.php">
        <label>联系我们</label>
        <textarea cols="50" rows="10" >在这里输入内容...</textarea>
</form>
```

在浏览器中的显示结果：

![wenbenyu](http://img.mukewang.com/52e5b4040001f4af05760367.jpg)

注意这两个属性可用css样式的width和height来代替：col用width、row用height来代替。

##[4.复选，单选框](http://www.imooc.com/code/497)
在使用表单设计调查表时，为了减少用户的操作，使用**选择框**是一个好主意，html中有两种选择框，即**单选框**和**复选框**，两者的区别是单选框中的选项用户只能选择一项，而复选框中用户可以任意选择多项，甚至全选。

**语法：**
```html
<input   type="radio/checkbox"   value="值"    name="名称"   checked="checked"/>
```

> 1、type:
   当 type="radio" 时，控件为单选框
   当 type="checkbox" 时，控件为复选框
> 2、value：提交数据到服务器的值（后台程序PHP使用）
> 3、name：为控件命名，以备后台程序 ASP、PHP 使用
> 4、checked：当设置 checked="checked" 时，该选项被默认选中

**eg.**

```html
<form name="iForm" method="post" action="save.php">
    你是否喜欢旅游？<br />
    <input type="radio" name="radioLove" value="喜欢" checked="checked"> 喜欢
    <input type="radio" name="radioLove" value="不喜欢"> 不喜欢
    <input type="radio" name="radioLove" value="无所谓"> 无所谓
    <br /><br />
    你对哪些运动感兴趣？<br />
    <input type="checkbox" name="checkbox1" value="跑步"> 跑步
    <input type="checkbox" name="checkbox2" checked="checked" value="打球"> 打球
    <input type="checkbox" name="checkbox3" checked="checked" value="登山"> 登山
    <input type="checkbox" name="checkbox4" value="健身"> 健身
```

在浏览器中的显示结果：

![xuankuang2](http://img.mukewang.com/52e5f8010001159804900257.jpg)

**注意:**同一组的单选按钮，`name` 取值一定要**一致**，比如上面例子为同一个名称“radioLove”，这样同一组的单选按钮才可以起到单选的作用。

##[5.下拉列表框option](http://www.imooc.com/code/498)
`<option>`下拉列表在网页中也常会用到，它可以有效的节省网页空间。既可以单选、又可以多选。

###单选
**语法：**
> `<option value="提交值">选项</option>`

**eg.**
```html
<form name="iForm">
    <label>爱好：</label>
    <select>
        <option value='读书'>读书</option>
        <option value='运动'>运动</option>
        <option value='音乐'>音乐</option>
        <option value='旅游'>旅游</option>
        <option value='购物' selected='selected'>购物</option>
    </select>
</form>
```

在浏览器中显示结果：

![xiala](http://img.mukewang.com/52e605340001014804520288.jpg)

> * 1.**value：**为向服务器提交的值。
> * 2.**selected="selected"：**设置selected="selected"属性，则该选项就被默认选中。

###[多选](http://www.imooc.com/code/500)
下拉列表也可以进行多选操作，在`<select>`标签中设置multiple="multiple"属性，就可以实现多选功能，在 widows 操作系统下，进行多选时按下**`Ctrl`**键同时进行**`单击`**（在 Mac下使用 Command +单击），可以选择多个选项。

**语法：**

> * `<select multiple="multiple">`

###[select标签](http://www.w3school.com.cn/tags/tag_select.asp)
**定义和用法：**
> * select 元素可创建单选或多选菜单。
`<select>` 元素中的`<option>`标签用于定义列表中的可用选项。
> * select 元素是一种表单控件，可用于在表单中接受用户输入。

##[6.按钮设置](http://www.imooc.com/code/501)
在表单中有两种按钮可以使用，分别为：提交按钮、重置。

###提交按钮
当用户需要提交表单信息到服务器时，需要用到**提交按钮**。**只有当type值设置为submit时，按钮才有提交作用。**

**语法：**

> * `<input   type="submit"   value="提交">`
> * value：按钮上显示的文字

**eg.**

```html
<form method="psot" action="save.php">
    <label for="myName">姓名：</label>
    <input type="text" value=" " name="myName" />
    <input type="submit" value="提交" name="submitBtn" />
</form>
```

在浏览器中的显示结果：

![anniu](http://img.mukewang.com/52e6126f0001496a04480218.jpg)

###[重置按钮](http://www.imooc.com/code/520)
当用户需要重置表单信息到初始时的状态时，比如用户输入“用户名”后，发现书写有误，可以使用`重置按钮`使输入框恢复到初始状态。只需要把`type`设置为`"reset"`就可以。

**语法：**

> * `<input type="reset" value="重置">`
> * type：只有当type值设置为reset时，按钮才有重置作用
> * value：按钮上显示的文字

**eg.**
```html
<form method="post" action="save.php">
    <label for="myName">姓名：</label>
    <input type="text" value=" " name="myName" />
    <input type="reset" value="重置" name="resetBtn" />
</form>
```

在浏览器中显示的结果：

![chongzhi](http://img.mukewang.com/52e6189e000186b604480218.jpg)

---
作者：Skyeyes
2015.11.18
本文根据[爱慕课网HTML+CSS基础(www.imooc.com)](https://www.imooc.com/learn/9)和[w3school](http://www.w3school.com.cn/index.html)总结









