# Flask学习笔记(2)

标签（空格分隔）： python flask primer

---
##1.概要
> * Web开发基础
> * Flask中的Hello World
> * Flask的模板
> * FLask的消息提示与异常处理
 
##2.Web开发基础
> * 前端知识
> * Git与Github
> * MVC设计模式
> * HTTP协议

###1)前端知识基础
> * Html
> * CSS
> * **JavaScript**

###2)前端常用的库与框架
> * Bootstrap
> * jQuery
> * ANGULARJS
> * React

###3)代码管理工具
> * git

###4)MVC设计模式
> * View(视图)
> * Controller(控制器)
> * Model(模型)

###5)HTTP协议(超文本传输协议)
> 特点
> 1.基于请求与响应模式
> 2.无状态

常用的请求模式:
 - **GET**
 - **POST**
 - DELETE
 - PUT

##3.Flask的Hello World
###1)概要
> * Flask应用的基本构成
> * Flask的路由
> * Flask的反向路由

###2)Flask应用的基本构成
```python
from flask import Flask
app = Flask(__name__)       #flask的路径(类名/包名)

@app.route('/')     #路由路径
def hello_world():      #路由
    return 'Hello World!'
    
if __name__ == '__main__':
    app.run()
```

###3)Flask的反向路由
```python
@app.route('/query_user')
def query_user():
    id = request.args.get('id')
    return 'query user' + id


@app.route('/query_url')
def query_url():
    return 'query url:' + url_for('query_user')
```

##4.Flask的模板
###1)概要
> * 模板的简单使用
条件语句
循环语句
模板的继承

###2)模板的继承
```html
{% extends 基页 %}
{% block ... %}
...
{% endblock %}
```

##5.Flask的消息提示和异常处理
###1)flash
1.
```python
from flask import flash
app.secret_key = '123'      #加密

@app.route('/')
def hello_world():
    flash("hello jike")
    return render_template("hello.html")
```

2.eg.
```python
@app.route('login', methods=['POST'])
def login():
    form = request.form
    username = form.get('username')
    password = form.get('password')

    if not username:
        flash("please input username")
        return render_template("hello.html")
    if not password:
        flash("please input password")
        return render_template("hello.html")

    if username == 'jikexueyuan' and password == '123456':
        flash("login sucess")
        return render_template("hello.html")
    else:
        flash("username or password is wrong")
        return render_template("hello.html")
```

###2)捕获错误
**@app.errorhandler(...)**

eg.404error
```python
@app.errorhandler(404)
def not_find(e):
    return render_template('404.html')
```

----
作者:Skyeyes
时间:2015.11.26
声明:本文本根据极客学院Python入门[Flask开发基础与入门](http://www.jikexueyuan.com/path/python/)总结

