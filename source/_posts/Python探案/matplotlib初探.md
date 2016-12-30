---
title: matplotlib初探
date: 2014-09-25
tags: 
- Python
- matplotlib
categories:
- Python探案
---
## 前言
最近摸索了Python的画图库[Matplotlib](http://matplotlib.org/index.html)，其画的图要多炫丽有多炫丽，要多优雅有多优雅，真的有被震撼到，最近项目要求需要画图，考虑到matlab虽然博大精深，但却不易上手，貌似网上最近也在盛传“是否matplotlib能取代matlab”的诸多言论，对于一个旁观者和门外汉，我不做评论，我只有一个理念：什么好学用什么。另外，对于语言的学习和掌握，我现在有一个特别明晰的目标，就是以后以Python为主轴，C\C++作为辅助，算法为核心来展开。  

半年前就接触Python，但期间由于没有一个特定的目标，东捡一点西捡一点，到头来总是在重复同样的事情。现在觉得需要什么学什么，带有目标地去学习才能提高效率，也才能记忆犹新，废话不多说，本文就简单的说说matplotlib。由于刚入门，也没有什么心得，仅仅是看了[matplotlib tutorial](http://www.loria.fr/~rougier/teaching/matplotlib/)的一点笔记记录。由于手册是英文版，所以，本文算是对原文的翻译，但我会完全脱离原文的思路，用自己的思路来写，外加自己的一些引申的东西。在进入主题之前，先看下这个知乎大牛关于[如何在论文中画出漂亮的插图](http://www.zhihu.com/question/21664179)的探讨，先目睹一下matplotlib所体现出炫丽与优雅。
<!-- more -->  
## Introduction  
先来看看matplotlib的Wikipedia介绍，懒得翻译了。  
[matplotlib](http://en.wikipedia.org/wiki/Matplotlib) is a plotting library for the Python programming language and its **NumPy** numerical mathematics extension. It provides an object-oriented API for embedding plots into applications using general-purpose GUI toolkits like wxPython, Qt, or GTK+. There is also a procedural **pylab** interface based on a state machine (like OpenGL), designed to closely resemble that of MATLAB. **SciPy** makes use of matplotlib. 

matplotlib 一个用来画2D图形的Python库(package)，它同时支持交互式和非交互式的画图方式，能够把画出的图形保存为PNG，PS等多种格式，可以使用多种窗口的工具包，如GTK+，wxWidgets,Qt等，并且可以画出多种类型的图形，如线、条形图、饼状图、柱状图等，主要用于科学计算领域，像常见的**gnuplot**和**MATLAB**一样，它是由John Hunter开发的，他说过一句非常经典的话：  
**Matplotlib tries to make easy things easy and hard things possible.**    

可见，matplotlib是多么令人心动不已。  

matplotlib非常的灵活和友善，提供多种画图的方式，在[《Matplotlib for python developers》](http://www.packtpub.com/matplotlib-python-development/book?utm_source=matplotlib.sourceforge.net&utm_medium=link&utm_content=pod&utm_campaign=mdb_002124)中总结了三种使用matplotlib画图的方式：  

- *pyplot*: matplotlib.pyplot提供类似于MATLAB的命令集合，使其表现得像MATLAB。
- *pylab*:结合了matplotlib.pyplot和Numpy的功能，既可以画图，又可以做科学计算，说白了，它就是一个使matplotlib表现得像MATLAB的一个接口，但是John不推荐使用这种方式，原因就是它的封装性覆盖了matplotlib的一些基本的东西，不适合开发者学习，往往造成知其然而不知其所以然的状态。
- *Object-oriented way（OO）*：面向对象方法，以python的方式使用，更加的pythonic，这种方法对于开发者来说可以完全控制matplotlib的执行过程，是最好的，但同时也是最复杂的。

下面分别以同一个画图例子来说明这三种方式：  
**pyplot**:  
 
	import matplotlib.pyplot as plt
	import numpy as np

	x = np.arange(0, 10, 0.1)
	y = np.random.randn(len(x))
	plt.plot(x, y)
	plt.title('random numbers')
	plt.show()
得到如下的图示：  
![](/image/plt.png)  

**pylab**:  

	from pylab import *

	x = arange(0, 10, 0.1)
	y = randn(len(x)) 
	plot(x, y) 
	title('random numbers')
	show()

**Object-oriented way（OO）**

	import matplotlib.pyplot as plt
	import numpy as np 

	x = np.arange(0, 10, 0.1)
	y = np.random.randn(len(x))
	fig = plt.figure()
	ax = fig.add_subplot(111)
	l, = plt.plot(x, y)
	t = ax.set_title('random numbers')
	plt.show()

可以看到，面向对象的方式和pyplot需要导入同样的库，才能做相应的操作，在所有代码中，pylab最简单，pyplot其次，OO最复杂，几乎和画图有关的所有元素都由用户自己定义，所以，这种方式更加能够剖析matplotlib的运行机理。因为我们写代码的目标是解决问题，解决问题讲究的是结果和效率，所以，我觉得用pylab是比较清爽的，但每个人都有自己不同的要求，如果一个程序2/3的代码量是依托于Plot，那么用OO的方式是比较合适的，如果只当它是个工具，就应该用最简单的。下面通过一个例子由浅入深地再来matplotlib的美妙之处，这个例子前面说过是翻译，可以找到前面的链接进入原版。  

这个例子是显示一个cos(x)和sin(x)，由浅入深，层层递进。我们使用pylab来操作。  
### 第一步：Using default
使用Plot的默认参数，包括figure size, dpi, line width, color, style, axes, axis, grid properties text and ront properties and so on.代码如下：  

	from pylab import *

	X = np.linspace(-np.pi, np.pi, 256, endpoint = True)
	C, S = np.cos(X), np.sin(X)
	
	plot(X, C)
	plot(X, S)
	show()
![](/image/plt1.png)

### 第二步：Instantiating defaults
自己定制一个图示，所有参数都自己定制，关于参数的详细定制请见：[Customizing matplotlib](http://matplotlib.org/users/customizing.html)  

	# Import everything from matplotlib (numpy is accessible via 'np' alias)
	from pylab import *
	
	# Create a new figure of size 8x6 points, using 80 dots per inch
	figure(figsize=(8,6), dpi=80)
	
	# Create a new subplot from a grid of 1x1
	subplot(1,1,1)
	
	X = np.linspace(-np.pi, np.pi, 256,endpoint=True)
	C,S = np.cos(X), np.sin(X)
	
	# Plot cosine using blue color with a continuous line of width 1 (pixels)
	plot(X, C, color="blue", linewidth=1.0, linestyle="-")
	
	# Plot sine using green color with a continuous line of width 1 (pixels)
	plot(X, S, color="green", linewidth=1.0, linestyle="-")
	
	# Set x limits
	xlim(-4.0,4.0)
	
	# Set x ticks
	xticks(np.linspace(-4,4,9,endpoint=True))
	
	# Set y limits
	ylim(-1.0,1.0)
	
	# Set y ticks
	yticks(np.linspace(-1,1,5,endpoint=True))
	
	# Save figure using 72 dots per inch
	# savefig("exercice_2.png",dpi=72)
	
	# Show result on screen
	show()
最后一步保存图示，所用的像素值和上面显示的像素值不一样，需要自己设置。  
![](/image/plt2.png)  
### 第三步：Changing colors and line widths 

	...
	figure(figsize=(10,6), dpi=80)
	plot(X, C, color="blue", linewidth=2.5, linestyle="-")
	plot(X, S, color="red",  linewidth=2.5, linestyle="-")
	...
![](/image/plt3.png)  
### 第四步：Setting limits
上图中的图示感觉太紧凑了，通过对x,y轴设置，可以预留出一些空间，使之看起来清晰一些，如下： 
 
	...
	xlim(X.min()*1.1, X.max()*1.1)
	ylim(C.min()*1.1, C.max()*1.1)
	...
![](/image/plt4.png)  
但是，一个更鲁棒性的版本，我们应该这样写：  

	xmin ,xmax = X.min(), X.max()
	ymin, ymax = Y.min(), Y.max()
	
	dx = (xmax - xmin) * 0.2
	dy = (ymax - ymin) * 0.2
	
	xlim(xmin - dx, xmax + dx)
	ylim(ymin - dy, ymax + dy)
### 第五步：Setting ticks
我们需要将步长设成[+/-pi, +/-pi/2]之间的值，那么需要这样做：  

	...
	xticks( [-np.pi, -np.pi/2, 0, np.pi/2, np.pi])
	yticks([-1, 0, +1])
	...

![](/image/plt5.png)  

### 第六步：Setting ticks labels
上图中已经非常接近了，但还需要将3.142表示成π的形式，这样做：  
	
	...
	xticks([-np.pi, -np.pi/2, 0, np.pi/2, np.pi],
	       [r'$-\pi$', r'$-\pi/2$', r'$0$', r'$+\pi/2$', r'$+\pi$'])
	
	yticks([-1, 0, +1],
	       [r'$-1$', r'$0$', r'$+1$'])
	...
![](/image/plt6.png)
### 第七步：Moving spines
这一步需要去掉边框，即形成x,y轴，形成一个坐标系，边框在这里定义成spines,我们把上、右边框移去，左边框右移，下边框上移，即可得到最终的图形。  

	...
	ax = gca()
	ax.spines['right'].set_color('none')
	ax.spines['top'].set_color('none')
	ax.xaxis.set_ticks_position('bottom')
	ax.spines['bottom'].set_position(('data',0))
	ax.yaxis.set_ticks_position('left')
	ax.spines['left'].set_position(('data',0))
	...
![](/image/plt7.png)  
### 第八步：adding legend  
为图示增加一个图例，我们选择左上角的位置，如下：  

	...
	plot(X, C, color="blue", linewidth=2.5, linestyle="-", label="cosine")
	plot(X, S, color="red",  linewidth=2.5, linestyle="-", label="sine")
	
	legend(loc='upper left')
	...
![](/image/plt8.png)  
### 第九步：Annotate some points
比如我要在图中注释2/3pi,该怎么做呢？  

	t = 2*np.pi/3
	plot([t,t],[0,np.cos(t)], color ='blue', linewidth=2.5, linestyle="--")
	scatter([t,],[np.cos(t),], 50, color ='blue')
	
	annotate(r'$\sin(\frac{2\pi}{3})=\frac{\sqrt{3}}{2}$',
	         xy=(t, np.sin(t)), xycoords='data',
	         xytext=(+10, +30), textcoords='offset points', fontsize=16,
	         arrowprops=dict(arrowstyle="->", connectionstyle="arc3,rad=.2"))
	
	plot([t,t],[0,np.sin(t)], color ='red', linewidth=2.5, linestyle="--")
	scatter([t,],[np.sin(t),], 50, color ='red')
	
	annotate(r'$\cos(\frac{2\pi}{3})=-\frac{1}{2}$',
	         xy=(t, np.cos(t)), xycoords='data',
	         xytext=(-90, -50), textcoords='offset points', fontsize=16,
	         arrowprops=dict(arrowstyle="->", connectionstyle="arc3,rad=.2"))
	...
![](/image/plt9.png)  
### 第十步：魔鬼在于细节
从上幅图中可以看出，整个图示已经够美观了，但是仔细一看，却发现线压字了，所以我们需要把字凸显出来，让线隐没下去。希望我们在这方面能够向处女座的人多学学。^_^  
	
	...
	for label in ax.get_xticklabels() + ax.get_yticklabels():
	    label.set_fontsize(16)
	    label.set_bbox(dict(facecolor='white', edgecolor='None', alpha=0.65 ))
	...
![](/image/plt10.png)  

OK，到这里为止，10步就把一个图完完整整表现出来了，原作者写这个入门手册也就是为了抛砖引玉，后面怎么举一反三就靠自己了，更多的图例可以看原手册，这里不做过多描述。另外，[matplotlib gallery](http://matplotlib.org/gallery.html)有很多精美的图示，点开就可以看见源码，我们以后如果遇到相关图示，可以做一个简单的参考。还有邮件列表，[user mailing](https://lists.sourceforge.net/lists/listinfo/matplotlib-users)。下面看看画图中常用的线的风格、标志符号和颜色值的表示。  
**line style or marker:**  

![](/image/lines.PNG)  
  
**color**  
标准的颜色值共有8种，如下：  

![](/image/color.PNG)  

但是指定颜色值的方式很灵活，《matplotlib for Python developer》中给出了四种方式：  

- 用全名，如‘yellow’或缩写（缩写只有上表中的8种）
- 十六进制表示，如紫色用#800080表示，更全的信息详见[十六进制颜色码](http://baike.baidu.com/view/644772.htm)
- RGB或RGBA元组，如(1,0,1,1)，关于如何转换RGB颜色，我还没搞懂，如有知晓，请告知。
- 灰度值表示，如'0.7'，只针对某一种颜色进行变换。

OK，就记录到这里，更详尽的还请见[matplotlib tutorial](http://www.loria.fr/~rougier/teaching/matplotlib/)。此处有一个非常全的视频讲Numpy和matplotlib >>>> [introductory tutorial on Numpy and matplotlib](http://www.youtube.com/watch?v=3Fp1zn5ao2M&feature=plcp)

**参考：**  
[matplotlib](http://matplotlib.org/index.html)  
matplotlib for Python developer