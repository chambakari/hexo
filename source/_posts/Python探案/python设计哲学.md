---
title: Python的设计哲学
date: 2015-01-06
tags: 
- Python
categories:
- Python探案
---
  
我始终相信任何事物（包括抽象的和具象的）的诞生都是有一定的原因的，在讯息快速更新迭代的今天，我们在接受新事物的同时，不当当要知道该事物是什么，而且有必要知道该事物的起源是什么，这样有助于我们应对这种变化，拥抱变化。  
![](/image/simple.jpg)  
<!-- more -->
## 扒一扒python的使用现状  
我们都知道几个比较大的项目，如Google engine的很大部分代码，YouTube以及国内的豆瓣等，都是使用的python。python从1991年正式发布，到至今已经和我同岁了，在这段时间里，已经发生了太多的变化，特别是科技的变化，科技的变化永远都是要比其他的领域来得要快。同样，对于语言的发展来说，同样也是发生着翻天覆地的变化，因为语言是构成科技的重要元素之一，科技的发展离不开语言的发展变迁。python经过这几年的时间，也日趋成熟，其优雅简洁，便于快速开发的优点，逐渐成为各大IT公司和科研机构所青睐的语言。我们来扒一扒两个主流的编程语言社区对现今流行的编程语言的使用情况的一个调查结果。一个是TIOBE，该社区的调查主要是基于Internet上有经验的程序员、课程和第三方厂商对各类语言的使用情况，然后使用搜索引擎技术来进行计算得出；另外一个是CodeForge，不同于TIOBE，该社区的调查则是来源于五万六千多名软件工程师的问卷调查。下面是TIOBE的调查结果。   
![](/image/langugerank.PNG)  
![](/image/languge.PNG)   
下面是CodeForge的调查结果。  
![](/image/pythonchina.PNG)  
![](/image/pythonworld.PNG)   
可见，python对于业界来说，并不是特别主流的语言，更主流还要属C、C++、java这些老牌语言，因为学习这些语言便于理解计算机底层的执行流程，所以这些语言基本上都是每个学计算的人的入门语言。而对于python而言，其优点在于简洁高效，可以让开发者不必过多的关注底层的执行机制，而专注在更高层的框架设计上。所以，python相对于这些老牌语言，使用率不高也是可以理解，但是当要做一些更高端的操作，如科学计算，使用python将会大大减少开发时间，提高开发效率。因此，这些榜单只能反映某个编程语言的热门程度，并不能说明一门编程语言的好与不好，或者一门语言所编写的代码量的多少。  
## python的起源  
新事物的出现离不开旧有事物的缺陷，python的设计灵感来源自然少不了旧有的语言缺陷。python是由一位荷兰的数学兼计算机专家Guido Van Rossum于1989年底发明的。当时老爷子在一家IT公司工作，他在这家公司参与设计了一种用于教学的语言，称为ABC语言。这种语言语法非常接近于自然语言，几乎和自然语言同等，不同之处也许只有那些标号等细小的点。但是由于这种语言一个不开放（也许比较臃肿），另外一个对机器性能要求极高。这对于当时的几KB RAM的机器配置来说，想要完成一些基本任务都是很难的。为了满足现有硬件的性能要求，只能从语言本身去做优化，才能满足更多的需求。之后，Guido就继承了ABC语言简洁之道，开发了python，为了继续优化性能，Guido也借鉴了shell的设计思想，并去除了ABC语言所特有的语法臃肿的特性，加入C、C++等这些常用语言语法简洁的特性。可以说，python集百家之长，完成了华丽的崛起。  
![](/image/pythonfarther.PNG)   
正因为此，python也被称为胶水语言（Glue Language），它能够将用其他语言写成的模块（尤其是C\C++）很轻松的粘合在一起。常见的一种应用情形是，使用python快速生成程序的框架，然后对其中要求特别高的部分，用更合适的语言写，比如3D游戏中的图形渲染模块，对性能要求极高，就可以用C++重写，还有Google Engine也是这样做的。至于为什么Guido会取名python，据称是因为Monty Python's Flying Circus(蒙提*派森飞行马戏团)这个剧，Guido是这个剧的狂热粉丝，名字里面就有一个Python字样，又叫做大蟒蛇，所以才会有了python的logo是一条可爱的蟒蛇。后来据说是1989年的圣诞，这个剧停播，Guido为了打发圣诞假期，才动手写的python，听起来好传奇，牛人就是这样，没有做不到，只有想不到。  
## 设计宗旨 
python的设计哲学总结为六个字，就是：优雅、明确、简单。为了能够让广大python爱好者全面了解python的设计思想，python社区的人每天都在源源不断的贡献自己的智慧和精力。其中有一位叫Peter的开发者用及其精辟的话整理总结了python的特性，并将之加入到python的模块中，成为了一个小彩蛋。想见这个彩蛋，只需在shell下*import this*即可。  

    >>> import this
    The Zen of Python, by Tim Peters
    
    Beautiful is better than ugly. 
	优美胜于丑陋
    Explicit is better than implicit.
	明确胜于晦涩
    Simple is better than complex.
	简单胜于复杂
    Complex is better than complicated.
	复杂胜于凌乱
    Flat is better than nested.
	扁平胜于嵌套
    Sparse is better than dense.
	稀疏胜于稠密
    Readability counts.
	可读性需要考虑
    Special cases aren't special enough to break the rules.
	即使情况特殊，也不应打破规则
    Although practicality beats purity.
	尽管使用胜于纯净
    Errors should never pass silently.
	错误不应该悄无声息的忽略
    Unless explicitly silenced.
	除非特意这么做
    In the face of ambiguity, refuse the temptation to guess.
	面对混淆是，拒绝猜测（深入搞明白问题）
    There should be one-- and preferably only one --obvious way to do it.
	总有一个，且仅有一个，明显的方法来处理问题
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
	现在开始胜过永远不开始
    Although never is often better than *right* now.
	尽管永远不开始经常比仓促立即开始好
    If the implementation is hard to explain, it's a bad idea.
	如果程序的实现很难解释，那么它不是一个很好的实现
    If the implementation is easy to explain, it may be a good idea.
	反之
    Namespaces are one honking great idea -- let's do more of those!
	命名空间是个绝好的注意，让我们多利用它  
这就是python的设计之禅，python社区的这群人都是非常幽默的，将python的设计思想放在解释器中，让人怎么也想不到，这还真是一番人生哲学啊。短短的几行字，借用一个网友说的，每个点都千锤百炼；每一点都直指人内心的感觉；既有指导大是大非的一年，又有指导细节操作的原则；既有谆谆教诲的推荐，也有声色俱厉的禁止。看N遍，每一遍都会让人深思，这就是哲学。     