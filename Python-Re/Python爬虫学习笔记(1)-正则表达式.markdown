# Python爬虫学习笔记(1)-正则表达式

标签（空格分隔）： python 爬虫 正则表达式

---

##1.正则表达式的符号与方法
> 常用符号：点号，星号，问号与括号（小括号）

> * .:匹配任意字符，换行符\n除外
> * *:匹配前一个字符0次或无限次
> * ?:匹配前一个字符0次或1次
> * .*:贪心算法
> * .*?:非贪心算法
> * ():括号内的数据作为结果返回

> 常用方法：findall， search， sub

> * findall：匹配所有符合规律的内容，返回包含结果的列表
> * search：匹配并提取第一个规律的内容，返回一个正则表达式对象(object)
> * sub：替换符合规律的内容，返回替换后的值


###1)findall

####a.点号`.`

```python
import re
a = 'xz123'
b = re.findall('x.', a)
print a
```
> * 输出 `['xz']`

**点`.`是一个占位符，一个`.`代表一个符号**


####b.星号`*`

```python
import re
a = 'xyxy123'
b = re.findall('x*', a)
print b
```
> * 输出`['x', '', 'x', '', '', '', '', '']`

**依次匹配字符，有则显示，无则显示`''`(空)。**

####c.问号`?`

```python
import re
a = 'xy123'
b = re.findall('x?', a)
print b
```
> * 单独与`*`一样，前面附加其他的符号将做非贪心限制

####d.贪心`.*`

```python
import re
secret_code = 'ghkj08hs68xxIxxa14kgj4w314exxlovexxbvk14rgjhxxyouxxfj4286ykjhag2'
b = re.findall('xx.*xx', secret_code)
print b
```
> * 输出`['xxIxxa14kgj4w314exxlovexxbvk14rgjhxxyouxx']`

**只要满足条件全部显示，贪心算法**

####e.非贪心`.*?`
```python
b = re.findall('xx.*?xx', secret_code)
```
> * 输出`['xxIxx', 'xxlovexx', 'xxyouxx']`

**以上只做了解，一般只用（.*?）**

####f.经典用法`(.*?)`
```python
b = re.findall('xx(.*?)xx', secret_code)
```
> * 输出`['I', 'love', 'you']`

**`()`包围所需要的内容，括号内的内容作为结果返回，不需要的内容放在括号外面**

###2)re.S

```python
import re
secret_code = '''ghkj08hs68xxIxxa14kgj4w314exxlove
xxbvk14rgjhxxyouxxfj4286ykjhag2'''
#love后有换行符
b = re.findall('xx(.*?)xx', secret_code)
print b
```
> * 输出`['I', 'bvk14rgjh']`，因为`.`不能匹配换行符。所以会**一行**为一个搜索项去找。匹配任何字符除了新的一行

```python
import re
secret_code = '''ghkj08hs68xxIxxa14kgj4w314exxlove
xxbvk14rgjhxxyouxxfj4286ykjhag2'''
#love后有换行符
b = re.findall('xx(.*?)xx', secret_code, re.S)
print b
```
> * 输出`['I', 'love\n', 'you']`，re.S让`.`匹配所有行，包括了换行符（以`\n`的形式出现）


###3)search
对比search和findall的区别
> * search 找到一个后返回，不继续，客大大提高效率
> * findall遍历全部，找到尽可能多的项

```python
import re
s2 = '''ghkj08hs68xxIxx123xxlove
xxbvk14rgjhxxfj4286ykjhag2'''
b = re.search('xx(.*?)xx(.*?)xx', s2, re.S).group(1)
print b
```
> * 输出`I`
> * `.group(2)`输出`love`
> * `.group(3)`报错

`group`是按括号顺序匹配

```python
import re
s2 = '''ghkj08hs68xxIxx123xxlovexxbvk14rgjhxxfj4286ykjhag2'''
f2 = re.findall('xx(.*?)xx123xx(.*?)xx', s2, re.S)
print f2[0][1]
```
> * 输出`love`

**每一个匹配项为第一级列表，括号为二级列表**

###4)sub
```python
import re
s = '123abcssfasdfas123'
output = re.sub('123(.*?)123', '123789123', s)
print output
```
> * 输出`123789123`
> * sub将符合条件的()内内容提换

###5)注意：

> * `from re import findall, search, S`
**最好不要引入，因为`S`等容易和变量等混淆，引起歧义**

###6)compile用法
```python
import re
secret_code = '''ghkj08hs68xxIxxa14kgj4w314exxlove
xxbvk14rgjhxxyouxxfj4286ykjhag2'''
pattern = 'xx(.*?)xx'
new_pattern = re.compile(pattern, re.S)
b = re.findall(new_pattern, secret_code)
print b
```
**因为findall自动调用compile方法，所以不先编译规律compile再匹配**

###7)匹配纯数字(\d+)
```python
import re
a = 'dfhkgh43gfhja873y5t2167715'
b = re.findall('(\d+)', a)
print b
```
> * 输出`['43', '873', '5', '2167715']`


##2.应用举例

###1)用findall和search从大量文本中匹配内容

####a.提取标题
```python
import re

old_url = 'http://www.jikexueyuan.com/course/android/?pageNum=2'
total_page = 20

f = open('text.txt', 'r')
html = f.read()
f.close()

title = re.search('<title>(.*?)</title>', html, re.S).group(1)
print title
```

text.txt
```html
<html>
    <head>
        <title>极客学院爬虫测试</title>
    </head>
    <body>
        <div class="topic"><a href="http://jikexueyuan.com/welcome.html">欢迎参加《Python定向爬虫入门》</a>
            <div class="list">
                <ul>
                    <li><a href="http://jikexueyuan.com/1.html">这是第一条</a></li>
                    <li><a href="http://jikexueyuan.com/2.html">这是第二条</a></li>
                    <li><a href="http://jikexueyuan.com/3.html">这是第三条</a></li>
                </ul>
            </div>
        </div>
    </body>
</html>
```
> * 输出`极客学院爬虫测试`

####b.提取网址

```python
link = re.findall('href="(.*?)"', html, re.S)
for each in link:
    print each
```

输出
> http://jikexueyuan.com/welcome.html
http://jikexueyuan.com/1.html
http://jikexueyuan.com/2.html
http://jikexueyuan.com/3.html

####c.提取文字信息

**先爬大再爬小**

```python
text_fied = re.findall('<ul>(.*?)</ul>', html, re.S)[0]
the_text = re.findall('">(.*?)</a>', text_fied, re.S)
for every_text in the_text:
    print every_text
```

###2)用sub实现翻页功能

```python
for i in range(2, total_page+1):
    new_link = re.sub('pageNum=\d+', 'pageNum=%d'%i, old_url, re.S)
    print new_link
```

##3.实战
目标网站：http://www.jikexueyuan.com/
目标内容：课程图片
实现原理：
> * 1.保存网页的源代码
> * 2.Python读文件加载源代码
> * 3.正则表达式提取图片网址
> * 4.下载图片

**文本爬虫，半自动爬虫，人工爬虫**

```python
import re
import requests

f = open('sourse.txt', 'r')
html = f.read()
f.close()

pic_url = re.findall('img src="(.*?)" class="lessonimg"', html, re.S)
i = 0
for each in pic_url:
    print 'now downloading:' + each
    pic = requests.get(each)
    fp = open('pic\\' + str(i) + '.jpg', 'wb')
    fp.write(pic.content)
    fp.close()
    i += 1
```

**`import requests`实现保存图片的功能**

---
作者：Skyeyes
日期：2015.11.19
说明：本文根据[极客学院](http://www.jikexueyuan.com/)[Python定向爬虫入门](http://www.jikexueyuan.com/course/777.html)整理总结






