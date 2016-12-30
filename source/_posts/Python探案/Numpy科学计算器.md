---
title: Numpy——强大的科学计算器
date: 2014-09-24
tags: 
- Python
- Numpy
categories:
- Python探案
---
 
### 简单概念
**Numpy 是Python中用于科学计算的一个基本的包(Package)**，下面来看看Numpy的官方定义：  
NumPy is the fundamental package for scientific computing with Python. It contains among other things:  

- a powerful N-dimensional array object  
- sophisticated (broadcasting) functions
- tools for integrating C/C++ and Fortran code
- useful linear algebra, Fourier transform, and random number capabilities

**简单的理解Numpy就是**：其为数值定义了特定的结构和规则，方便对不同的数值，甚至复杂的数值进行运算（这里说的数值是广义上的），如多维数组结构等。
<!-- more -->  
**Numpy提供了两种基本的对象**：ndarray(N-dimensional array object)和ufunc(universal function object)。ndarray是存储单一数据类型的多维数组，而ufunc则是能够对数组进行处理的函数。

在Python的标准库，已经有相应的结构来处理数组值的计算，如list，array，那么为什么还需要Numpy？原因就是：  
1）、list中可以存放任何对象，因此list中所保存的是对象的指针，这样为了保存一个简单的[1,2,3]，需要3个指针和三个整数对象，对于数值计算这种结构显然是比较浪费内存和CPU计算时间的。  
2）、array模块直接保存数值，和C语言的一维数数组比较类似，但其不支持多维数组，也没有各种运算函数，因此不适合做数值计算。  
3）、Numpy定义的运算函数ufunc可以在数组和矩阵之间互相转换，可以做到和matlab一般计算游刃有余。

标准的Python库没有Numpy，需要额外安装，这里推荐一个Python shell：[ipython](http://ipython.org/)，其整合了多个库，不用额外去安装，具体都有些什么库，可以看看知乎的一个回答：[Python 常用的标准库以及第三方库有哪些？](Python 常用的标准库以及第三方库有哪些？)，一般我们常用的两个库是Numpy和matplotlib，在我的眼中，这两个加起来就是matlab。另外在推荐一个方便进行调试的IDE：JetBrains开发的[Pycharm](http://www.jetbrains.com/pycharm/)，个人感觉非常nice。

### 基本语法
**Numpy的主要对象是同构的多维数组**（homogeneous multidimensional array），每个元素用序号进行标记，在Numpy中，维叫做轴，维中的行列值对应轴中叫做rank，如一个二维数组：[[1,0,1], [0,1,2]]有两个轴，第一个轴的rank是2，第二轴的rank是3。（和矩阵对应，Numpy提供了数组和矩阵之间的转化方式）

**Numpy中的数组类型叫做ndarray**，也可以看成是array，只是环境不同，叫法不一样而已，它和Python标准库中的array不一样，array.array只处理一维的数组和少量的函数，而Numpy.array提供多维数组运算，同时还提供多种函数进行数组相关的数值计算，如下：  
ndarry.ndim:数组轴(维)的数量，如二维数组就为2  
ndarray.shape:数组的维，如3行2列就为（3,2）  
ndarray.size:数组中总的元素个数  
ndarray.dtype:数组中元素的类型  
ndarray.itemsize:数组中元素的字节类型，如int类型就为4  
ndarray.data:数组的缓存，一般是用不到的  

由于用的不多，且时间有限，尚无法总结出其主要的操作，我们知道它是干什么用的就可以了，以后如果用到，直接查看其用户手册[Numpy tutorial](http://wiki.scipy.org/Tentative_NumPy_Tutorial)即可。这里有一个学习的网址：[Numpy introduction](http://sebug.net/paper/books/scipydoc/numpy_intro.html)
