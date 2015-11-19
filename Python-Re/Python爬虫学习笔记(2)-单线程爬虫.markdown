# Python爬虫学习笔记(2)-单线程爬虫

标签（空格分隔）： python 爬虫 单线程

---

##概要
> * Requests介绍
> * 网页爬虫
> * 向网页提交数据
> * 实战--极客学院课程爬虫

##1.Requests介绍
- [x] Requests：HTTP for Humans（第三方库，实现python的网络连接）
- [x] 完美的替代Python的urllib2模块
- [x] 更多的自动化
- [x] 更友好的用户体验
- [x] 更完善的功能

###1)urllib2模块
目标网址：'https://api.github.com'

```python
import urllib2

gh_url = 'http://api.github.com'

req = urllib2.Request(gh_url)

password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()
password_manager.add_password(None, gh_url, 'user', 'pass')

auth_manager = urllib2.AbstractBasicAuthHandler(password_manager)
opener = urllib2.build_opener(auth_manager)

urllib2.install_opener(opener)

handler = urllib2.urlopen(req)

print handler.getcode()
print handler.headers.getheader('content-type')
```

###2)使用requests模块

```python
# -*- coding: utf-8 -*-

import requests

r = requests.get('https://api.github.com', auth=('user', 'pass'))

print r.status_code
print r.headers['content-type']
```

##2.第一个网页爬虫
> * 用requests提取网页源代码
> * 用正则表达式匹配内容

###1)提取源代码
> * 在一些情况下直接获取
> * 修改http头获取源代码

####a.直接获取
```python
import requests
html = requests.get('http://tieba.baidu.com/f?ie=utf-8&kw=python')
print html.text
```
requests.get()获取网页源代码
.text输出内容

####b.修改http头
有些情况下网站对访问进行检查，阻止爬虫requests的访问，所以需要更改http头，作用是让爬虫伪装成浏览器从让网站通过访问。

**语法：**

> * 添加语句：（变量名） = {'User-Agent':''}

User-Agent的内容通过：`右键`->`审核元素`->`NetWork`->`刷新网页`->`任意选择一项`->`Headers`->`在Request Headers中找到User-Agent`

> * 在requests.get()中添加`headers = 变量名`

**eg.**
```python
headers = {'User-Agent':'...'}
html = requests.get('...', headers = headers)
```

###2)提取内容
找到自己所需的内容的规律用正则表达式匹配。

##3.向网页提交数据

> * Get和Post介绍
> * 分析目标网站
> * Requests的表单提交

###1)Get和Post介绍

> * Get是从服务器上获取数据
> * Post是从服务器传送数据，并返回所传送的值
> * Get通过构造url中的参数来实现功能
> * Post将数据放在header提交数据

###2)分析目标网站
目标：https://www.crowdfunder.com/browse/deals
使用：Chrome-审核元素-Network

```python
import requests
import re
url = 'http://www.crowdfunder.com/browse/deals'

html = requests.get(url).text
print html
```
发现在点击异步加载项后，提取不了新增内容

###3)Requests表单提交
核心方法：requests.post
核心步骤：构造表单-提交表单-获取返回信息

**对于使用异步加载技巧的网站，get只能获取部分信息,所以使用Post**

```python
import requests
import re
url = 'http://www.crowdfunder.com/browse/deals&template=false'

data = {
    'entitles_only':'true',
    'page':'1'
}

html_post = requests.post(url, data=data)
title = re.findall('"card-title">(.*?)</div>', html_post.text, re.S)
for each in title:
    print each
```

> * **page**所对应的值为异步页数，初始页为1

##3.实战--极客学院课程爬虫
> * 目标网站：http://www.jikexueyuan.com/course/
> * 目标内容：前20页的课程名称，课程介绍，课程时间，课程等级，学习人数
> * 涉及知识：Requests获取网页，re.sub换页，正则表达式匹配内容

**爬虫只能获取到我们能看到的东西**

```python
# -*- coding: utf-8 -*-
import requests, re, sys
reload(sys)
sys.setdefaultencoding("utf-8")

class spider(object):
    def __init__(self):
        print u'开始爬取内容。。。'

    def getsource(self, url):
        html = requests.get(url)
        return html.text

    def changepage(self, url, total_page):
        now_page = int(re.search('pageNum=(\d+)', url, re.S).group(1))
        page_group = []
        for i in range(now_page, total_page+1):
            link = re.sub('pageNum=\d+','pageNum=%s'%i, url, re.S)
            page_group.append(link)
        return page_group

    def geteveryclass(self, sourse):
        everyclass = re.findall('(<li deg="".*?</li>)', sourse, re.S)
        return everyclass

    def getinfo(self, eachclass):
        info = {}
        info['title'] = re.search('target="_blank">(.*?)</a>', eachclass, re.S).group(1)
        info['content'] = re.search('</h2><p>(.*?)</p>', eachclass, re.S).group(1)
        timeandlevel = re.findall('<em>(.*?)</em>', eachclass, re.S)
        info['classtime'] = timeandlevel[0]
        info['classlevel'] = timeandlevel[1]
        info['learnnum'] = re.search('learn-number">(.*?)</em>', eachclass, re.S).group(1)
        return info

    def saveinfo(self, classinfo):
        f = open('info.txt', 'a')
        for each in classinfo:
            f.writelines('title:' + each['title'] + '\n')
            f.writelines('content:' + each['content'] + '\n')
            f.writelines('classtime:' + each['classtime'] + '\n')
            f.writelines('classlevel:' + each['classlevel'] + '\n')
            f.writelines('learnnum:' + each['learnnum'] + '\n\n')
        f.close()


if __name__ == '__main__':

    classinfo = []
    url = 'http://www.jikexueyuan.com/course/?pageNum=1'
    jikespider = spider()
    all_links = jikespider.changepage(url,20)
    for link in all_links:
        print u'正在处理页面：' + link
        html = jikespider.getsource(link)
        everyclass = jikespider.geteveryclass(html)
        for each in everyclass:
            info = jikespider.getinfo(each)
            classinfo.append(info)
    jikespider.saveinfo(classinfo)
```

---
作者：Skyeyes
日期：2015.11.19
说明：本文根据[极客学院](http://www.jikexueyuan.com/)[Python定向爬虫入门](http://www.jikexueyuan.com/course/777.html)整理总结







