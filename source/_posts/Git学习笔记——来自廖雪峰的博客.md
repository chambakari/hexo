---
title: Git学习笔记——来自廖雪峰的博客
date: 2016-12-29 15:19:18
tags:
- git
categories:
- 技术人生
---
## Git 简介
Git是目前世界上最先进的开源的**分布式**版本控制系统。  
和**集中式**的版本控制系统，如CVS、SVN等相比，Git有几大优点：
1、不像集中式版本控制系统一样，需要联网才能工作；
2、安全性较高，避免了单点失效的问题，不会因为某台电脑坏了，文件就丢失了；
3、具有强大的分支管理功能。
### 安装Git
	Linux：sudo apt-get install git
	centos: sudo yum install git-core
	windows: git bash
安装完成后，需要配置机器的Git仓库，即：  

	git config --global user.name "Your Name"
	git config --global user.email "email@example.com"
<!-- more -->
## Git 基础特性及常用命令
### 创建版本库（仓库，repository）
	mkdir learngit
	cd learngit
### 添加文件到Git仓库
	git init: 将当期目录变成Git可以管理的仓库
	git add file
	git commit -m "add file"
补充几个概念：
- 工作区：如learngit
- 版本库：.git (包括暂存区和分支)
- 暂存区：git add 之后存储的位置
- 分支：git commit 之后存储的位置

![](/image/git.jpg)     

### 跟踪工作区的状态
	git status: 可以随时掌握工作区的状态
	git diff file: 如果git status告知file被修改了，该命令告知修改了什么内容

### 版本回退
	git log: 查看提交历史，显示commit id、author、date等
	git log --pretty=oneline: 清爽版
回退方法两种：  
1、HEAD
HEAD表示当前版本，HEAD^上一版本，HEAD^^上上一版本，HEAD~100上第100版本。 
	git reset --hard HEAD^
2、commit id  

	git reset --hard 34343
如要重返未来的某一个版本，则只能找到commit id，通过以下命令来确定：

	git reflog
### 工作区、暂存区的文件修改、撤销修改、删除相关
	git diff HEAD -- readme.txt:查看工作区和版本库里面最新版本的区别
	git checkout -- file：丢弃工作区的修改
	git reset HEAD file: 丢弃暂存区的修改，回到工作区
如果git commit提交到版本库，参考*版本回退*

	git rm file
	git commit -m "remove file":将文件从版本库删除，保证本地工作区和版本库文件同步
### 远程仓库（Github）
本地Git仓库和远程Github仓库之间的传输是通过SSH加密的，所以需要设置SSH Key：  
	
	ssh-keygen -t rsa -C "youremail@example.com"
	less ~/.ssh/id_rsa.pub
注：GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。  

	git remote add origin git@github.com:xxx/learngit.git:将本地参考与远程仓库进行关联
	git push -u origin master:把本地仓库内容推送到远程，-u表示把本地master分支与远程master分支关联，后面如果本地做了修改，只需git push origin master推送修改即可
克隆远程仓库：  

	git clone git@github.com:xxx/learngit.git:使用ssh协议克隆，也可以使用https，但ssh支持的原生git协议速度更快。
## Git 高级特性：分支、标签
### 创建与合并分支  
	git checkout -b dev:创建dev分支，并切换到dev分支
	相当于：
	git branch dev
	git checkout dev
	git branch:查看当前分支
	git merge dev: 在master上合并dev分支
	git branch -d dev: 删除dev分支
	git log --graph: 可以查看合并分支图，常用：
	git log --graph --pretty=oneline --abbrev-commit
### 分支管理策略
合并分支时一般会使用Fast Forward模式，即快进模式，将master分支直接指向dev分支，删除分支后，丢失分支信息，看不出曾经的合并历史信息，这不利于将来出错回头排查问题，所以，可以禁用Fast forward模式，通过以下方式：

	git merge --no-ff -m "merge with no-ff" dev:Git 在merge时生成一个新的commit id,从分支历史上看出分支信息
### Bug 分支
在dev分支上开发，突然有了bug，但是dev还没开发好，无法提交，这时，可以：

	git stash:把当前工作现场保存起来，等以后恢复现场后继续工作
	git stash list: 查看保存的工作现场
	git stash apply: 恢复工作区，但恢复后stash不删除，需要用：
	git stash drop:来删除
	git stash pop:恢复的同时把stash内容也删了
### Feature 分支
开发一个新feature，最好创建一个分支；  
如果要丢弃一个没有被合并过的分支，可以通过：

	git branch -D <name>：强行删除
### 多人协作：推送分支
	git remote:查看远程库信息
	git remote -v：显示更详细的信息
	git push origin master: 推送分支到远程master分支
	git push origin dev:推送分支到远程dev分支
**分支推送**备注  

- master分支是主分支，因此要时刻与远程同步；
- dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

### 多人协作：抓取分支
	git checkout -b dev origin/dev：在远程的dev分支上进行开发
如果两个人对同一个dev分支，会产生冲突，此时先pull，再push。

	git pull
	git branch --set-upstream dev origin/dev:指定本地dev分支与远程origin/dev分支的链接
	如果有冲突，则先处理冲突

### 标签管理
	git tag <name>:用于新建一个标签，默认为HEAD，也可以指定一个commit id；
	git tag -a <tagname> -m "blablabla...":可以指定标签信息；
	git tag -s <tagname> -m "blablabla...":可以用PGP签名标签；
	git tag:可以查看所有标签。
	git push origin <tagname>:可以推送一个本地标签；
	git push origin --tags:可以推送全部未推送过的本地标签；
	git tag -d <tagname>:可以删除一个本地标签；
	git push origin :refs/tags/<tagname>:可以删除一个远程标签。

*更多高级特性，请前往：[廖雪峰git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)*
