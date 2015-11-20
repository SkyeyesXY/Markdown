# Python爬虫学习笔记(3)-XPath与多线程爬虫

标签（空格分隔）： python 多线程 爬虫

---
**概要：**
> * XPath的介绍与配置
> * XPath的使用
> * XPath的特殊用法
> * Python并行化
> * 实战--百度贴吧爬虫

##1.XPath的介绍与配置

> * 官方名称：XML路径语言(XMLpathlanguage)
> * 用来确定xml文档中某部分位置的语言（查找信息）
> * XPath支持HTML
> * XPath通过元素和属性进行导航

- [x] 提取信息
- [x] 比正则表达式高级
- [x] 比正则表达式简单

###1)如何安装使用XPath

> * 需要安装lxml库
> * from lxml import etree
> * Selector = etree.HTML(网页源代码)
(将网页源代码转换成XPath能够识别的格式)
(Selector为变量名)
> * Selector.xpath(...)

##2.XPath的使用

> * XPath与HTML结构
> * 获取网页元素的Xpath
> * 应用XPath提取内容

###1)XPath与HTML结构

树状结构->逐层展开->逐层定位->寻找独立节点

###2)获取网页元素的Xpath
> * 手动分析法
> * Chrome生成法
直接右键`copy Xpath`

###a.语法
`//*[@id="useful"]/li[1]`

> * 星号代表只有一个id为useful，若有别的id相同，则必须写明标签
> * li[1]说明为第一个`<li>`
> * `//`在这里是默认的`<html><body>`(根目录)

**语法分析：**
> * `//`定位根节点
> * `/`往下层寻找
> * 提取文本内容： /text()
> * 提取属性内容： /@xxxx

###b.**eg.**

"text.html"
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>测试－常规方法</title>
</head>
<body>
<div id="content">
    <ul id="useful">
        <li>这是第一条信息</li>
        <li>这是第二条信息</li>
        <li>这是第三条信息</li>
    </ul>
    <ul id="useless">
        <li>不需要的信息１</li>
        <li>不需要的信息２</li>
        <li>不需要的信息３</li>
    </ul>
    
    <div id="url">
        <a href="http://jikexueyuan.com">极客学院</a>
        <a href="http://jikexueyuan.com/sourse/" title="极客学院课程库">点我打开课程库</a>
    </div>
</div>
</body>
</html>
```

"xpath_regular.py"
```python
# -*- coding: utf-8 -*-
from lxml import etree
f = open('text.html', 'r')
html = f.read()
f.close()

selector = etree.HTML(html)
```

a.提取文本
```python
#提取文本
content = selector.xpath('//ul[@id="useful"]/li/text()')
for each in content:
    print each
```

输出：
> * 这是第一条信息
这是第二条信息
这是第三条信息

b.提取属性
```python
#提取属性
link = selector.xpath('//a/@href')
for each in link:
    print each
```

输出：
> * http://jikexueyuan.com
http://jikexueyuan.com/sourse/

c.提取title
```python
title = selector.xpath('//a/@title')
print title[0]
```

输出：
> * 极客学院课程库

##3.XPath的特殊用法
> * 以相同的字符开头
> * 标签套标签

###1)以相同的字符开头
> * starts-with(＠属性名称，属性字符相同部分)

eg.
```html
<div id="test-1">需要的内容1</div>
<div id="test-2">需要的内容2</div>
<div id="testfault">需要的内容3</div>
```

###2)标签套标签
> * string(.)

eg.
```html
<div id="class3">美女,
    <font color=red>你的微信是多少？</font>
</div>
```

###3)演示

####a.starts-with:

xpath_special.py
```python
# -*- coding: utf-8 -*-
from lxml import etree
f = open('special.html', 'r')
html = f.read()
f.close()
selector = etree.HTML(html)
content = selector.xpath('//div[starts-with(@id,"test")]/text()')
for each in content:
    print each
```

special.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <div id="test-1">需要的内容1</div>
    <div id="test-2">需要的内容2</div>
    <div id="testfault">需要的内容3</div>
</body>
</html>
```

输出：
> * 需要的内容1
> * 需要的内容2
> * 需要的内容3

####b.string(.):
xpath_special.py
```python
# -*- coding: utf-8 -*-
from lxml import etree
f = open('special2.html', 'r')
html = f.read()
f.close()
selector = etree.HTML(html)
data = selector.xpath('//div[@id="test3"]')[0]
info = data.xpath('string(.)')
content = info.replace('\n', '').replace(' ','')
print content
```

special2.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <div id="test3">
        我左青龙，
        <span id="tiger">
            右白虎，
            <ul>
                上朱雀，
                <li>下玄武。</li>
            </ul>
            老牛在当中，
        </span>
        龙头在胸口。
    </div>
</body>
</html>
```

输出：
> * 我左青龙，右白虎，上朱雀，下玄武。老牛在当中，龙头在胸口。

##4.Python并行化
> * 并行化介绍
> * Map的使用

###1)并行化介绍
- [x] 多个线程同时处理任务
- [x] 高效
- [x] 快速

###2)Map的使用
> * map函数一手包办了序列的操作，参数传递和结果保存等一系列的操作。
> * from multiprocessing.dummy import Pool
> * pool = Pool(计算机核数)
> * results = pool.map(爬取函数，网址列表)

```python
# -*-coding: utf-8 -*-
from multiprocessing.dummy import Pool as ThreadPool
import requests
import time

def getsource(url):
    html = requests.get(url)

urls = []

for i in range(1,21):
    newpage = 'http://tieba.baidu.com/p/3522395718?pn=' + str(i)
    urls.append(newpage)

time1 = time.time()
for i in urls:
    print i
    getsource(i)
time2 = time.time()
print u'单线程耗时：' + str(time2-time1)

pool = ThreadPool(2)
time3 = time.time()
results = pool.map(getsource, urls)
pool.close()
pool.join()
time4 = time.time()
print u'并行耗时：' + str(time4-time3)
```

##5.实战--百度贴吧爬虫
> * 目标网站：http://tieba.baidu.com/p/3522395718
> * 目标内容：前20页的跟帖用户名，跟帖内容，跟帖时间
> * 涉及知识：Requests获取网页，XPath提取内容，map实现多线程爬虫

tiebaspider.py
```python
# -*- coding: utf-8 -*-
from lxml import etree
from multiprocessing.dummy import Pool as ThreadPool
import requests
import json  #转义json格式的内容

import sys      #将编码转义为utf-8
reload(sys)
sys.setfaultencoding('utf-8')


def towrite(contentdict):
    f.writelines(u'回帖时间：' +str(contentdict['topic_reply_time']) + '\n')
    f.writelines(u'回帖内容：' +unicode(contentdict['topic_reply_content']) + '\n')
    f.writelines(u'回帖人：' +str(contentdict['user_time']) + '\n\n')

def spider(url):
    html = requests.get(url)
    selector = etree.HTML(html.text)
    content_field = selector.xpath('//div[@class="l_post l_post_bright "]')
    item = {}
    for each in content_field:
        reply_info = json.loads(each.xpath('@data-field')[0].replace('&quot',''))       #因为获取的是xpath后的内容所以直接@
        author = reply_info['author']['user_name']
        content = each.xpath('div[@class="d_post_content_main"]/div/cc/div[@class="d_post_content j_d_post_content "]/text()')[0]
        reply_time = reply_info['content']['date']
        print content
        print reply_time
        print author
        item['user_name'] = author
        item['topic_reply_content'] = content
        item['topic_reply_time'] = reply_time
        towrite(item)


if __name__ == "__main__":
    pool = ThreadPool(2)
    f = open('content.txt', 'a')
    page = []
    for i in range(1, 21):
        newpage = 'http://tieba.baidu.com/p/3522395718?pn=' + str(i)
        page.append(newpage)

    results = pool.map(spider, page)
    pool.close()
    pool.join()
    f.close()
```

---
作者：Skyeyes
日期：2015.11.20
说明：本文根据[极客学院](http://www.jikexueyuan.com/)[Python定向爬虫入门](http://www.jikexueyuan.com/course/777.html)整理总结






