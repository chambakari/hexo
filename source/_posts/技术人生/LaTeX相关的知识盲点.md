---
title: LaTeX相关的知识盲点
date: 2015-04-14 21:59:05
tags: 
- LaTeX
categories:
- 技术人生
---

LaTeX是一款高效的论文写作排版工具，除了写论文，它还有其他的一些用途，比如做ppt，写优美的简历，作优美的图画等等。相对于word+endnote的论文写作组合，LaTeX也和JabRef组成一个最佳的组合，但其好用程度比之前一个提升至少10个档次。本文总结几个我在使用的过程中遇到的盲点。

### LaTeX对中文的支持

要使用中文模板，则LaTeX需要安装CJK库以支持汉字，该库里面已经包含了字体格式，大小等，怎么使用，请见下面一个简单的例子：  
<!-- more -->  
#### 模板

%要运行该模板，LaTex需要安装CJK库以支持汉字.

 %字体大小为12像素，文档类型为article

 %如果你要写论文，就用report代替article

 %所有LaTex文档开头必须使用这句话

\documentclass[12pt]{article}  

%使用支持汉字的CJK包

\usepackage{CJK}  

%开始CJK环境,只有在这句话之后,你才能使用汉字

%另外,如果在Linux下,请将文件的编码格式设置成GBK

 %否则会显示乱码

\begin{CJK*}{GBK}{song}  

%这是文章的标题

\title{LaTex 常用模板}  

%这是文章的作者

\author{Kevin}  

%这是文章的时间

%如果没有这行将显示当前时间

%如果不想显示时间则使用 \date{}

 \date{2008/10/12}  

%以上部分叫做&quot;导言区&quot;,下面才开始写正文

\begin{document}  

%先插入标题

\maketitle

 %再插入目录

\tableofcontents

 \section{LaTex 简介}

LaTex是一个宏包,目的是使作者能够利用一个

 预先定义好的专业页面设置,

从而得以高质量的排版和打印他们的作品.  

%第二段使用黑体,上面的一个空行表示另起一段

\CJKfamily{hei}LaTex 将空格和制表符视为相同的距离.

多个连续的空白字符 等同为一个空白字符

\section{LaTex源文件}

 %在第二段我们使用隶书

\CJKfamily{li}LaTex 源文件格式为普通的ASCII文件,

你可以使用任何文本编辑器来创建.  

LaTex源文件不仅包括你要排版的文本, 还包括LaTex

所能识别的,如何排版这些文本的命令.

 \section{结论}

 %在结论部分我们使用仿宋体

\CJKfamily{fs}LaTeX, 我看行!  

\end{CJK*}

 \end{document}  

#### 字体

CTeX里提供了GBK编码的六种中文字体（宋体、仿宋、楷体、黑体、隶书和幼圆），如果你安装了CTeX，就可以类似下面来使用这几种字体：

\documentclass{article}

 \usepackage{CJK}

 \begin{document}

 \begin{CJK}{GBK}{song}

这是CTeX里的宋体！

\end{CJK}  

\begin{CJK}{GBK}{fs}

这是CTeX里的仿宋体！

\end{CJK}    

\begin{CJK}{GBK}{kai}

这是CTeX里的楷体！

\end{CJK}  

\begin{CJK}{GBK}{hei}

这是CTeX里的黑体！

\end{CJK}  

\begin{CJK}{GBK}{li}

这是CTeX里的隶书！

\end{CJK}  

\begin{CJK}{GBK}{you}

这是CTeX里的幼圆体！

\end{CJK}

\end{document}    

### 参考文献

参考文献一般显示在文章末尾，可以用数字标号或者文章年份，有的甚至用作者信息来显示，这些显示方式分别对应着不同的模板，也就是不同库，我们常用的一种方式是显示标号，几种设置方式见下文：

[LaTex常用宏包：](http://zzg34b.w3.c361.com/package/reference.htm)