---
title: Markdown入门语法汇总
date: 2014-09-18
tags:
- Markdown
categories:
- 学霸笔记
---
  
单个回车
视为空格

连续回车

才能分段

行尾加两个空格  
即可段内换行。

*斜体*

**粗体**

### 代码

行的开头空4个空格，表示程序代码，例如：

C#： 
 
     public class Blog
     {
         public int Id { get; set; }
         public string Subject { get; set; }
     }

Python：

     keywords = ["dsaa","Asd","sadc","Gdfd","gdfdd","gaf","gabdddddd","eg"]
     print dict([(i[0],list(i[1])) for i in groupby(sorted(keywords),lambda    x:x[0].lower())])

>表示引用文字内容,比如引用他人的文章。

显示大标题（=）


显示小标题（-）
-

分割线（---）

----

- 这是无序列表
- 这是无序列表

两个列表之间不能相邻，否则会解释为嵌套的列表

1、这是有序列表项目  
2、这是有序列表项目

下面是嵌套的列表

- 外层列表项目  
 + 内层列表项目
 + 内层列表项目
- 外层列表项目

直接把一个URL显示为超级链接：

可以这样：[Markdown](www.markdown.com)

图像和连接非常相似，区别在开头加一个惊叹号：![这是一个logo图像](http://www.turingbook.com/Content/img/Turing.Gif)