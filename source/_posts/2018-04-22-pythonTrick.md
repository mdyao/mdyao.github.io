---
title: Life is short you need python
date: 2018-04-22 16:07:00
updated: 2018-04-22 16:07:00
comments: true
tags:
- XJBX
- 摸鱼日志

categories: [深度学习]
copyright: true
urlname: pythonTrick

---





### 关于`if not x:`&`if x is not None`&`if not x is None`
代码中经常会有变量是否为None的判断，有三种主要的写法：

 第一种是`if x is None`；

第二种是 `if not x：`；

第三种是`if not x is None`（这句这样理解更清晰`if not (x is None)`） 。

如果你觉得这样写没啥区别，那么你可就要小心了，这里面有一个坑。先来看一下代码：
```
>>> x = 1  
>>> not x  
False  
>>> x = [1]  
>>> not x  
False  
>>> x = 0  
>>> not x  
True  
>>> x = [0]         # You don't want to fall in this one.  
>>> not x  
False  
```

<!--more-->

在python中 None,  False, 空字符串"", 0, 空列表[], 空字典{}, 空元组()都相当于False ，即：
```
not None == not False == not '' == not 0 == not [] == not {} == not ()
```
因此在使用列表的时候，如果你想区分`x==[]`和`x==None`两种情况的话, 此时`if not x:`将会出现问题：
```
>>> x = []  
>>> y = None  
>>>   
>>> x is None  
False  
>>> y is None  
True  
>>>   
>>>   
>>> not x  
True  
>>> not y  
True  
>>>   
>>>   
>>> not x is None  
>>> True  
>>> not y is None  
False  
>>>   
```
也许你是想判断x是否为None，但是却把`x==[]`的情况也判断进来了，此种情况下将无法区分。
对于习惯于使用if not x这种写法的pythoner，必须清楚x等于None,  False, 空字符串"", 0, 空列表[], 空字典{}, 空元组()时对你的判断没有影响才行。 

而对于`if x is not None`和`if not x is None`写法，很明显前者更清晰，而后者有可能使读者误解为`if (not x) is None`，因此推荐前者，同时这也是谷歌推荐的风格


结论：

`if x is not None`是最好的写法，清晰，不会出现错误，以后坚持使用这种写法。

使用if not x这种写法的前提是：必须清楚x等于None,  False, 空字符串"", 0, 空列表[], 空字典{}, 空元组()时对你的判断没有影响才行。

### Python if 和 for 的多种写法
1.not in
```
>>> a=2

>>> a not in [2,3,4]
False
>>> a in [2,3,4] 
True
```


2.c if a else b   #这里注意，一定要有b,而且b不能为pass
```
>>> a=3 if 2>3 else 4
>>> a
4

>>> a=3 if 2<3 else 4 
>>> a
3
```



3.[fun(a) for a in [...]] 
```
>>> [a+1 for a in [2,3,4,5,6]]
[3, 4, 5, 6, 7]
```


4.a,b=b,a
```
>>> a=1
>>> b=2
>>> a,b=b,a
>>> a
2
>>> b
1
```


5.'内容'.join([string array])
```
>>> '.'.join[2,3,4,5,6]  
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'builtin_function_or_method' object has no attribute '__getitem__'
>>> '.'.join([2,3,4,5,6]) 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: sequence item 0: expected string, int found
>>> '.'.join(['2','3','4','5','6']) 
'2.3.4.5.6'
```


### 数组顺序翻转

排序：https://blog.csdn.net/u014292358/article/details/79503397
OpenCV与Python之图像的读入与显示以及利用Numpy的图像转换：https://www.cnblogs.com/visionfeng/p/6094423.html

        # Convert from RGB -> BGR
        input_a = input_a[..., [2, 1, 0]]
        input_b = input_b[..., [2, 1, 0]]

###参考资料：
[1] [python代码`if not x:` 和`if x is not None:`和`if not x is None:`使用](https://blog.csdn.net/Sasoritattoo/article/details/12451359)
[2] [python里面的几个用法，not in，c if a else b，[fun(a) for a in [...]] , a,b=b,a,'内容'.join(string array)](https://blog.csdn.net/u013176681/article/details/53995190)
[3] [Python if 和 for 的多种写法](https://blog.csdn.net/zl87758539/article/details/51675628)