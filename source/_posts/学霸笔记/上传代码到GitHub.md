---
title: 上传代码到GitHub的初尝试
date: 2014-10-02
- git
- github
categories:
- 学霸笔记
---
    
Github是Git旗下的分布式版本管理系统的库，主要用于代码的托管、展示和分享，方便程序员合作开发，所以，Github相当于一个远程的仓库或者是托管代码的云服务器，也可以把其看成是分享和展示代码的网站。  
这个库早早就听说过，但是一直没有使用，现在随着写的代码越来越多，而且越来越大，代码的管理和维护成为了不得不面对的问题，但作为一个IT爱好者或是即将的IT从业者（我不想用程序员这个词，总感觉这个职业处在压迫之中），不应该把精力放在后期频繁而琐碎的代码维护上，而应该专注于前期的代码开发上。所以，Github这个工具非常合适。但是其入门并不是那么傻瓜式的，因为它依托于Git，需要借助于Git的各种命令来实现代码上传与托管，网上各种入门级的教程，眼花缭乱，与其看别人的，不如自己写一篇，也供以后自己的查阅，若是能够帮助到一两个网友，也不枉费我的辛苦。  
### 提交代码的方式  
通过看网友的教程，可以大致分为三种方式，因为代码的提交都是要通过本地客户端来完成，所以这三种方式都是依据不同的客户端来分的：  
1、使用msysgit客户端，关于如何使用msysgit上传代码，请参见这篇博文：[初识Github](http://blog.csdn.net/hcbbt/article/details/11651229)  
2、直接使用Github的客户端，对应不同的OS，有不同的版本，如windows平台就有Github for Windows，其为windows用户提供了一个基本的图形前端去处理大部分常用版本控制任务，可以创建版本库，向本地版本库提交补丁，在本地和远程版本库之间同步。使用Github提交代码，参见这篇：[从不会到会用Github](http://www.freair.com/bbs/read.php?tid=892)  
3、使用Git客户端，配有Git bash和Git GUI,本文采用这种方法。 

### 上传自己的项目到Github  
主要遵循以下两个原则： 
 
**将Github上新建的库clone到本地**  
**修改或更新之后上传到Github**

基于以上两个原则，按照以下几步进行操作：  
1、在Github上建立项目  
登录Github之后，找到并点击按钮“New Repository”，即可新建一个项目，记住项目地址，以便后面使用。（PS：项目地址在Code一栏处HTTPS的地方，复制即可）。如果说不是第一次上传代码或Git已经配置过，请跳转到第4步。
2、配置Git以及上传代码  
初次使用Git需要对其进行配置，主要就是让Git记录你Github上的账号名邮件地址，输入如下两行即可：  

	git config --global user.name("your real name")  
	git config --global user.email ("you@email.address")  
3、认证Github  
这一步比较麻烦，需要利用Git生成一个SSH密钥，并提交该密钥到Github上。具体生成密钥和提交密钥的步骤请见[在GitHub上分享和展示你的代码](http://serholiu.com/github-share-code)  
4、上传代码到Github  
秉承下载又上传的原则，刚开始新建的库需要先克隆到本地，然后在上传，所以，首先，通过Git Bash进入需要保存项目的地方，命令的操作和Linux相似。然后执行下面克隆命令操作：  

	git clone https://github.com/XXX/XXX.git  
上面的地址就是前面所记录的地址。如果说该库在本地已存在，就不用克隆，直接上传文件即可。下面就是上传操作：  

	a、git add .   
//该操作是上传当前目录下的全部文件，如果只上传单个文件，则如：git add test.md  

	b、git commit -am 'commit'   
//提交，让上条增加文件命令生效，同时显示代码文件的说明，即代码提交到Github上的提示说明，说明该代码是干嘛的。  

	c、git remote add origin https://github.com/XXX/XXX.git  
//向本地仓库中添加远程仓库地址，远程仓库地址别名为origin，如果出现下面的错误：  
fatal: remote origin already exists  
则执行如下语句：  
git remote rm origin  

	d、git pull origin master  
//将origin所代表的远程仓库地址里的Master主干下载到本地仓库，即上传之前先进行一次同步  

	e、git push -u origin master 
//将本地仓库上传到origin所代表的远程仓库的master分支上  
到此，就可以到Github页面上看，就会看到本地的代码文件已经同步到远程仓库中，这里，只要记住一点：  
**先把远程服务器Github上面的文件先pull下来，在push上去**  
关于Github的操作还有很多，在这里，我们只做简单代码上传和托管操作，我觉得只用记住这几条命令即可，后期在做进一步深入的时候，可以在继续学习。mark~~