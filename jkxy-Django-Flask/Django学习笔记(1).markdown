# Django学习笔记(1)

标签（空格分隔）： Django primer python

---

概要:
> * 1.Django概述:背景和优点
> * 2.视图开发及URL配置
> * 3.Django模块语法和使用
> * 模型开发与数据库交互
> * Django的后台管理及表单类介绍

##1.Django概述

###1)Django的历史
> * 诞生背景:维护开发新闻站点
> * 开发团队:World Online小组
> * 主要开发者:Adrian和Jacob

###2)优点
> * 自主管理后台
> * 自带ORM
> * Django的错误提示

###3)语句
> * `jango-admin.py startapp XXX`
> * `python manage.py runserver`

##2.视图开发和URL配置
Django可识别的视图需满足以下两个条件：
 1. 第一个参数的类型：HttpRequest
 2. 返回HttpResponse实例

在views.py中
```python
from django.shortcuts import render
from django.http import HttpResponse

def hello(request):
    return HttpResponse("hello world")
```
`request`:必须包含,它包含当前外部请求信息的对象

在urls.py中
```python
from myTest.views import *
admin.autodiscover()
urlpatterns = (
    url(r'^hello/$', hello),
    url(r'^admin/', include(admin.site.urls)),
)
```
`(r'^hello/$', hello)`:第一个是模式匹配字符串(正则表达式,`^`头部匹配，`/$`尾部匹配),第二个是视图函数

```python
url(r'^hello/(\d+)/$', hello1),
```

`(\d+)`匹配任意整数

在 views.py中
```python
from django.http import Http404

def hello1(request, num):
    try:
        num = int(num)
    except ValueError:
        raise Http404
```
`Http404`处理无法找到页面时的错误

> * 在django中有详尽的报错页面
如果不要显示这个页面,在`settings.py`中修改`DEBUG`为`False`
```python
DEBUG = False
ALLOWED_HOSTS = ['*']
```

##3.Django模板语法及使用
模板是一个文本,用于分离文档的表现形式和内容,通常用于生成HTML

###1)实例
```html
<p>Hello {{ name }}</p>
...
{% for item in itemList %}
    <li>{{ item }}</li>
{% endfor %}
...
{% if status %}
...
{% else %}
...
{% endif %}
```

> * 用`{{ }}`来匹配变量
> * 用`{% ... %}`来匹配语句(if,for等)
必须在结束时加`{% end.. %}`语句

###2)基本使用方式
> * 1.可以用原始的模板代码字符串创建一个Template对象
> * 2.调用模板对象的render方法,并且传入一套变量context
用context传递值,用render渲染

###3)过滤器方法
> * `{{name | lower}}`: `|`为管道字符,将name变为小写格式
> * 其他

###4)templates文件夹
在settings中用
```python
TEMPLATES = [
    {
        'DIRS': [os.path.join(BASE_DIR, 'templates')]
    }
]

#或TEMPALTE_DIRS = os.path.join(BASE_DIR, 'templates')
#或TEMPALTE_DIRS = os.path.join(os.path.dirname(__file__, 'templates')
```

使用模板
```python
#在命令行中
from django.template.loader import get_template
t = get_template('1.html')
```

在views.py中
```python
from django.shortcuts import render,render_to_response
def views(request):
    return render_to_response('1.html',{'name':'hello'})
    #return render(request, '1.html', {'name':'hello'})
    #可以用render_to_response省去request等
```

###5)模板的继承
```html
{% block a %}
...
{% endblock %}
```
在另一个html中
```html
{% extends 母文件 %}

{% block a %}
{% endblock %}
```

##4.模型开发与数据库交互

settings.py配置
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        'USER': 'root',
        'PASSWORD':'root',
        'HOST':'localhost'
    }
}
#也可不做更改
```

在models中
```python
from django.db import models

class Mysite(models.Model):
    title = models.CharField(max_length=100)
    url = models.URLField()
    author = models.CharField(max_length=100)
    num = models.IntegerField(max_length=10)
```
> * `CharField`字符串类型等

用`python3 manage.py validate`语句检查models是否有错误

###1)数据处理
> * 1.基本数据访问
> * 2.插入和更新数据
> * 3.数据过滤
> * 4.数据排序
> * 5.更新多个对象,删除对象等

----
作者:Skyeyes
时间:2015.11.26

