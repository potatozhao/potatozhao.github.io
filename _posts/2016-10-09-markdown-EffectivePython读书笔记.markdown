---
title: "effective python 读书随笔，于10月9日深夜 持续更新"
layout: post
date: 2016-10-06 22:44
tag:
- markdown
- python
blog: true
---

## Effective Python:

简简单单的介绍一下redis的集群配置

### 目录

- [1-10](#num1)
- [11-20](#num11)
- [21](#num21)

---

### 确认自己所使用的python版本
{: #num1}
python3 和python2 的区别有点大，使用的时候请注意。另，某些工具能做到很容易的切换3和2.

---

### 遵循PEP8风格指南
良好的代码可阅读性是很重要滴！能抱跑起来是关键，能让人读懂也是很关键滴！

---

### 了解bytes，str与unicode的区别
这个。。。以后详细说明，大坑，巨坑，陨石坑。

---

### 用辅助函数来取代复杂的表达式
恩。。。一方面是减少错误，另外一方面是增加可阅读性

---

### 了解切割序列的方法
* 切片操作不会计较start或者end越界
* 切片相当于对切片范围内的队列进行拷贝

A Python Example:
{% highlight python %}

    a = [1,2,3,4,5]
    a[:10] # [1,2,3,4,5]
    b = a[:10] # b = copy.deepcopy(a)

{% endhighlight %}

---

### 在单次切片中不要同时指定start,end,stride
* 既有start和end又有stride的切割操作，可能会难以理解
* stride尽可能用正数
* 在同一个切片操作内，不要同时使用start和end和stride，如果有需要，考虑拆成两条赋值语句去做，其中一条做范围切割，另外一条做步进切割。或者考虑使用itertools模块中的islice。

A Python Example:
{% highlight python %}

    a = [1,2,3,4,5]
    a[::2] # [1,3,5]
    a = [1,2,3,4]
    a[::2] # [1,3]
    a[::-2] # [4,2]
    a[1:3:2] #[2]

{% endhighlight %}

---

### 用列表推导来取代map和filter
*list comperhension* 用一份列表来制作另外一份列表

{% highlight python %}

    a = [1,2,3,4,5,6,7,8,9]
    b = [x**2 for x in a] # [1,4,9,16,25,36,49,64,81]
    c = map(lambda x: x**2, a) # 难懂
    d = map(lambda x: x**2, filter(lambda x: x %2 ==0, a)) # 更难懂了。。。
{% endhighlight %}

---

### 不要使用含有两个以上表达式的列表推导
那啥。。。连续3个及其以上。。。。你还能看懂这个列表是干嘛的么？嘿嘿嘿。

---

### 使用生成器表达式来改写数据量较大的列表推导
    a = [x for x in open('a.out')]

如果a.out很大。。。大的超过了你的内存。。。那么。。。嘿嘿嘿。Python是会先把a.out 全部都读进内存的

但是Python有个一个神奇的玩意 *generator expression* 生成器表达式

{% highlight python %}

    a = (x for x in open('a.out'))
    print next(a) # 100
    print next(a) # 99
{% endhighlight %}

---

### 尽量使用enumerate代替range

{% highlight python %}

    a = [1,2,3,4,5]
    for i in range(len(a)):
        print a[i]
    for i, value in enumerate(a):
        print "%d:%d" % (i,value)
{% endhighlight %}

---

### 用zip函数同时遍历两个列表
{: #num11}

* 可以同时遍历多个迭代器
* python 3中相当于迭代器，2中则是一次性返回一个正份的列表
* 如果长度不同，则以最短的为结束符。
* zip_longest可以以最长的为结束符。

---

### 不要在for和while循环之后加else

这个。。。正常点都不会吧。。。写的话整个循环结束之后会直接执行else的内容。

---

### 合理利用try except else finally中的每一个代码块

* finally 
    - 如果既要将异常传出，又要在异常发生的时候执行清理工作，那就可以使用try/finally结构。
* else
    - try/except/else 如果try没有异常，则执行else语句。
* 混合使用会更好，每一个代码块个行其责。

---

### 尽量用异常来表示特殊情况，不要反悔None!!!

血泪史。。。。。return 必须返回状态情况。有异常就返回错误。调用必须判断返回值是不是异常。

---

### 了解如何在闭包里使用外围作用域中的变量

额。。。复杂的。。。我实在不想用

---

### 使用生成器来改写直接返回列表的函数

yield!!!!!!yield!

这样就能极大的节省内存。over。

---

### 在参数上边迭代时要多加小心

当参数是迭代器时，请先生成全部数据，再拷贝，再循环。over！！！！注意！！！！先生成全部数据！！！

---

### 用数量可变的位置参数减少视觉杂讯

可变参数是元组。

---

### 用关键字参数来表达可选的行为

关键字参数:

{% highlight python %}

    def func(num = 10, open = False, values):
        if open:
            print valuse[num]
{% endhighlight %}

---

### 用None和文档字符串来描述具有动态默认值的参数

{% highlight python %}

    def func(time = datetime.now()):
        pass
    def func(time = None):
        if time:
            time = datetime.now()
        pass
{% endhighlight %}

time会在模块加载的时候就计算datetime.now()
之后time的值就不会再改变。所以有必要的话，请使用文档字符串和None来描述默认动态参数

---

### next 21
{: #num21}
