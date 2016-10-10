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

    a = (x for x in open('a.out'))
    print next(a) # 100
    print next(a) # 99

---

### 尽量使用enumerate代替range
    a = [1,2,3,4,5]
    for i in range(len(a)):
        print a[i]
    for i, value in enumerate(a):
        print "%d:%d" % (i,value)

---

### next 11
{: #num11}
