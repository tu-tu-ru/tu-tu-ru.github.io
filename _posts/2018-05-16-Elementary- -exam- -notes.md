---
layout:     post                    
title:      Elementary exam notes               
subtitle:     
date:       2018-05-16              
author:     Bear                     
header-img: img/0409.PNG    
catalog: true                       
tags:                              
    - 生活常识
---

## `sort()` 和 `sorted()` 的用法

### `sorted()`
  用 `help(sorted)` 查看文档里对这个函数的解释是这样的：

>sorted(iterable, key=None, reverse=False)
>		Return a new list containing all items from the iterable in ascending order.
>
>​	A custom key function can be supplied to customize the sort order, and the reverse flag can be set to request the result in descending order.

从这个解释可以看出，有 `key` 和 `reverse` 两个参数可以改变返回的新 list 的形态。以下是几个示例：

#### 设置排序的 `key`

这里的 key 实际上是一个作用于 list 里的每个元素的函数，that is to say 这个函数接收的参数是前面的可迭代对象（iterable）中的每一个元素。

这是一个简单的对列表里的每个元素（`<string>`）排序，`key=len`，让这个新列表按字符串的长度排 ascending 顺序

`sorted(['bear','are','you','hungry','now','?'],key=len,reverse=False)`

输出：`['?', 'are', 'you', 'now', 'bear', 'hungry']`

`key` 用到的这个函数可以和 `lambda` 结合使用，比如以下这个例子，利用一个 dictionary 里的 value 们的数值大小给内含的所有 key-value pair 重新排序。

`dic={'b':3,'a':5,'c':9,'d':2}` 

`sorted(dic.items(), key=lambda x: x[1])` 

输出：`[('d', 2), ('b', 3), ('a', 5), ('c', 9)]` 

#### 设置 ascending/descending 顺序

`sorted([0,1,2,3,4,5,6],key=None,reverse=True)`

输出：`[6, 5, 4, 3, 2, 1, 0]`

### `sort()`

#### sort() 和 sorted() 的区别

1. sorted() 不会影响原有的 list，函数作用的结果是生成一个新的 list。sort() 是在原有 list 上直接作用，改变原有的列表。
2. Difference in syntax. `<list>.sort()` 和 `sorted(<list>)` 的区别。
3. 以下示例可以解释这两个函数对原有可迭代对象的不同作用

`a=[0,1,2,3,6,5,4]`

`b=a.sort()`

`type(b)`

这里查看 type 的结果是 `None`，也就是说 `a.sort()` 这个操作的结果是没有返回任何新的东西, e.g. a new, modified list，仅仅是改变的原来的 list。

`a`

输出：`[0, 1, 2, 3, 4, 5, 6]`

从这儿可以看出 `a` 已经不同于最初了，

## 一个关于赋值的操作

昨天做了一个题，是这样的：

> 有一分数序列：2/1，3/2，5/3，8/5，13/8，21/13...求出这个数列的前20项之和。

本熊暗中观察了一下，一开始觉得是要用到 `reduce` 啥的，后来发现就是迭代嘛，前一个加后一个这样，互相赋值就好，就写了如下的东西：

```python
def cal_sum(n):
    numerator = 2.0
    denominator = 1.0
    sum = 0.0
    for i in range(n):
        i_value=numerator/denominator
        numerator=numerator+denominator
        denominator=numerator
        sum=sum+i_value
        #print(sum)
        #print(i_value)        
    return sum
```

用注释里边的两个 print 函数看了下每一步的结果，发现不对。for loop 里第二行和第三行的赋值有问题，因为这两个赋值的过程是有先后顺序的，所以这个过程实际上变成了

```python
numerator=numerator+denominator
denominator=原来的numerator+原来的numerator+denominator
```

完球。

答案里是这样写的：

`numerator,denominator=numerator+denominator,numerator`

看着挺厉害的，两边同时赋值，hh。

### 两种赋值方法的区别

```python
x=1
y=2
x=x+y
y=x
print(x)
print(y)

a=1
b=2
a,b=a+b,a
print(a)
print(b)
```

输出：

3 3 3 1