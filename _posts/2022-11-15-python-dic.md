---
title: python dic
author: kai
date: 2022-11-15
category: python
layout: post
---

记录下pyton dic语法

dic包括的函数主要有：['clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']


dic 初始化
-------------

{% highlight python %}

dic ={1:1,2:2}

{% endhighlight %}

dic 添加元素
-------------

{% highlight python %}
dic = {}
dic[1] = 1
dic[2] = 2
{% endhighlight %}

dic 删除指定元素元素
-------------

{% highlight python %}
dic ={1:1,2:2}
dic.pop(1)
{% endhighlight %}

dic 遍历
-------------

{% highlight python %}

dic = {1:1,2:2,3:3}

for key in dic.keys():
    print("{0}:{1}".format(key,dic[key]))

for key,value in dic.items():
    print("{0}:{1}".format(key,value))
{% endhighlight %}
