---
title: Python Django第一步  
date: 2014-10-27
tags: 
- Python
- Django
categories:
- Python探案
---

几经深思和犹豫之后，终于下定了决心要学Django，这是一个如何规划效用成本的问题，有得必有吧，但这是理想的东西，即使是蜗牛的速度，不管什么时候都应该去尝试一下。  
在正式入门之前，首先要解决的就是开发环境部署的问题，我选择的是Linux，原因是Django依附于多个相关的python库，在windows上安装着实不方便，而在Linux上就显得格外简单，一行sudo apt-get install XXX的命令就可以搞定。本文主要记录我在安装Django的过程中所遇到的一些问题。 
<!-- more --> 
###  安装Django  
首先在[python django](http://www.djangoproject.com/download/)下载Django，完了之后执行以下命令安装：  

	1、tar xzvf Django-\*.tar.gz   
	2、cd Django-\*  
	3、sudo python setup.py install    
这时会提示no module named steuptools，这说明在安装Django需要先安装setuptools库，打开[setuptools的python官网](https://pypi.python.org/pypi/setuptools)看看setuptools该如何安装，如下：  
![](/image/steuptools.PNG)   
除了这种安装方法之外，也可以直接下载setuptools软件包后安装：  
(1)下载setuptools包  

	# wget http://pypi.python.org/packages/source/s/  setuptools/setuptools-2.0.tar.gz  
(2)解压setuptools包  

	# tar zxvf setuptools-2.0.tar.gz  
	# cd setuptools-2.0  
(3)编译setuptools  

	# python setup.py build  
(4)开始执行setuptools安装  

	# python setup.py install  
除此之外，还有一种安装方法是使用pip，pip是什么，打开[pip的python官网](https://pypi.python.org/pypi/pip)，我们看到，pip是'A tool for installing and managing Python packages'，也就是说pip是python的软件安装工具，下面是pip的使用方法：  
安装包：       

	pip install SomePackage  
查看安装包时安装了哪些文件：  

	pip show --files SomePackage  
查看哪些包有更新：  

	pip show --files SomePackage  
更新一个软件：  

	pip install --upgrade SomePackage  
卸载软件：  

	pip uninstall SomePackage  
 
但是用pip，首先得安装，同样的方法，在上面的pip python首页下载pip 包(pip-1.4.1.tar.gz)，使用 “ tar -xvf pip-1.4.1.tar.gz” 解压，cd 进文件夹，使用 “python setup.py install” 命令安装软件。（如果你不想使用pip安装软件包，也可以用此方法下载、解压后使用 “python setup.py install”安装！安装完pip之后，就可以用pip直接安装setuptools了，如下命令：  

	sudo pip install steuptools      
安装完setuptools之后在重新运行sudo python setup.py install，等待其执行完之后，Django 就安装完成了。接下来，我们进入python的交互命令行，测试一下Django是否安装成功，如果出现以下代码，则表示安装成功：  

	>>> import django  
	>>> django.VERSION  
	(1, 7, 1, 'final', 0)    

### 安装数据库  
django只要求python正确安装后就可以跑起来了。 不过，如果想开发一个数据库驱动的web站点时，你应当需要配置一个数据库服务器。    
如果你只想玩一下，可以不配置数据库，直接跳到 开始一个project 部分去，不过你要注意本书的例子都是假设你配置好了一个正常工作的数据库。  
Django支持四种数据库：

    PostgreSQL (http://www.postgresql.org/)

    SQLite 3 (http://www.sqlite.org/)

    MySQL (http://www.mysql.com/)

    Oracle (http://www.oracle.com/)  

大部分情况下，这四种数据库都会和Django框架很好的工作。 （一个值得注意的例外是Django的可选GIS支持，它为PostgreSQL提供了强大的功能。）如果你不准备使用一些老旧系统，而且可以自由的选择数据库后端，我们推荐你使用PostgreSQL，它在成本、特性、速度和稳定性方面都做的比较平衡。  
如果只是玩一下，不想安装数据库服务，那么可以考虑使用SQLite。 如果你用python2.5或更高版本的话，SQLite是唯一一个被支持的且不需要以上安装步骤的数据库。 它仅对你的文件系统中的单一文件读写数据，并且Python2.5和以后版本内建了对它的支持。  
### 开始一个项目
如果安装好了python，django和（可选的）数据库及相关库，你就可以通过创建一个project，迈出开发django应用的第一步。
首先得为项目新建一个工作区，如/home/username/django/djcode，进入该目录，运行命令:  
	django-admin.py startproject mysite  
则会在当前目录下创建一个目录mysite。如果没有对django-admin.py该命令的环境进行配置，则会报错。所以，首先得对django的环境进行配置，如何在linux下配置环境变量，网上相关的配置方法有好几种，我们选择最简单的一种，即修改用户目录下的.bashrc文件，利用命令$gedit ~/.bashrc打开.bashrc，转到最后，添加如下的命令：

	# set Django
	export PATH=$PATH:/home/bycer/Django/Django-1.7.1/django/bin  
此时，重启终端，再次进入项目目录，重新运行：django-admin.py startproject mysite,就可以生成项目文件。  
其中包含几个文件：  

	\_\_init__.py  
	manage.py  
	settings.py  
	urls.py  
	wsgi.py   
### 运行开发服务器
django开发服务器是可用在开发期间的，一个内建的，轻量级的web服务。无需进行产品级的web服务器（如Apache）的配置工作，开发服务器会监视代码并自动加载它。进入mysite，运行以下命令：  

	python manage.py runserver  
将会看到：  

	Validating models...  
	0 errors found.  
	Django version 1.0, using settings 'mysite.settings'  
	Development server is running at http://127.0.0.1:8000/  
	Quit the server with CONTROL-C.  
此时在浏览器中访问http://127.0.0.1:8000/就可以看到django的欢迎界面了。此时就说明一个简单的基于Django的web应用成功部署完成。