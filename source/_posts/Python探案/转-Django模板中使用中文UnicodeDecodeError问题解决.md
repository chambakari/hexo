---
title: (转) Django模板中使用中文UnicodeDecodeError问题解决
date: 2015-08-14 10:29:23
tags: 
- Django
categories:
- Python 探案
---

原文请见: [某人说我技术宅](http://1992mrwang.blog.51cto.com/3265935/1123023)

今天使用了bootstrap 当中的一些CSS 对自己的博客项目当中的一些东西进行美化， 但是很奇怪的是当加入中文字符后， 就会提示 **UnicodeDecodeError** 错误， 很明显就是字符问题， 而最终解决的方案就是 在 settings.py 文件当中加入：
    
    FILE_CHARSET='gb18030' 
    DEFAULT_CHARSET='utf-8' 

另外的一些相似的问题解决：  
<!-- more -->  
（1）、先是数据库插入问题：   
在默认的mysql当中插入中文字符的时候会报错， 解决方式就是修改其数据库或数据库当中某张表或者某个字段成为UTF-8类型即可， 这里介绍一种方式：  
在MYSQL的安装目录下修改my.ini文件中的“default-character-set=”为GB2312或者UTF-8，修改这一项之后，会对MYSQL中的数据库全部起作用，如果你为了减少以后不必要的麻烦，你也可以只设置你当前要使用的数据库的编码，如：
     
    CREATE DATABASE database_name DEFAULT CHARACTER SET utf8 

（2）、然后就是编码 Django 的底层实现使用的是UTF-8字符， 所以在程序设计时候， 应该尽量使用utf-8 去进行编码， 而在开始时可以使用 #coding:utf-8 去声明使用的字符编码。

（3）、Django支持国际化
可以在settings.py 的 MIDDLEWARE_CLASSES 区进行添加：
    
    MIDDLEWARE_CLASSES
    添加 'django.middleware.locale.LocaleMiddleware' 
    并确保它在 
    'django.contrib.sessions.middleware.SessionMiddleware'  
    之后 
刷新后会根据你的浏览器环境进行转换使用语言，打开你PROJECT下的settings.py,你可以看到：
"LANGUAGE_CODE =''"默认的是en-us,修改为zh-CN，这样也可以。
（4）、在HTML 模版文件当中 设置编码格式 在 <head></head>区域添加。

**Note：**在linux 当中pycharm开发时候发现模板不能使用中文字，于是将前面两个参数都改成utf-8后解决。