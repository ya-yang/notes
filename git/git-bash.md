#git bash 常用命令总结:
	
	*设置姓名的邮箱
	git config --global user.name "Die4passion"
	git config --global user.email "silencerfiend@gmail.com"

	*目录操作
	mkdir xxxxx    创建目录
	cd 	  xxxxx	   进入目录
	pwd		       显示路径
	ls			   和cmd的dir一样
	ls  -ah		   显示所有目录

	*增删改查
	git  init					添加目录（目录下直接输）
	git add xxxx.php 			添加文件（可以加多个文件，空格隔开）
	git commit -m "xxx" 		提交版本到版本库，xxx是信息
	git status 					查看版本库当前的状态
	git diff					查看difference,显示版本差异
	git diff HEAD -- xxxx.php
	git log						查看日志信息
	git log --pretty=oneline	日志信息，单行显示
	git reset --hard HEAD^		回退到上个版本
	git reset --hard HEAD^^		回退到上上个版本
	git reset --hard HEAD~100	回退到往上100个版本
	git reset --hard 34732842	回退到版本号前几位为这个的
	git reflog 					查看命令历史，确定需要回到的版本号

	git rm xxxxx.txt			从版本库中删除文件

	cat xxxx.php				打开文件内容
	rm  xxxx.txt				删除指定文件

###添加远程库
	
	将本地代码库关联到github的我的账号下的blog：

	git remote add origin git@github.com:Die4passion/blog.git

	git push -u origin master   把本地库的内容推送到远程(第一次)

	git push origin master     把本地master分支的最新修改推送到github


	克隆到本地:
	git clone git@github.com:Die4passion/blog.git
	windows下也可:
	git clone https://github.com/Die4passion/gitskills

###分支管理
	
	git checkout -b dev 创建分支dev，然后切换到dev
	相当于:
	git branch dev （创建分支）  和   git checkout dev（切换到分支）

	git branch     列出当前所有分支

	git merge dev   合并dev分支到master
	git merge --no-ff -m "message" dev （--no-ff）表示禁用fast forward

	git branch -d dev  删除指定分区

	查看分支的合并情况：
	git log --graph --pretty=oneline --abbrev-commit 

	#bug分支

	git stash 存下工作现场，恢复现场后继续工作
	git stash list 查看有哪些工作现场
	git stash apply恢复后stash内容不删除，需要git stash drop一下
	git stash pop 回到现场的同时删除stash内容
	多次stash、
	git stash apply stash@{数字}

	git remote 远程库名字，默认是origin
	git remote -v 远程库详细信息
	git push origin dev 推送到dev分支

	#创建本地dev分支
	git checkout -b branch-name origin/branch-name
	设置branch-name和origin/branch-name的链接：
	git branch --set-upstream branch-na
	me origin/branch-name
	git pull 把最新的提交抓下来



笔记：

1. git add  添加文件，实际上是添加到暂存区
2. git commit  提交更改，实际上是把暂存区的所有内容提交到当前分支
3. 每次修改，如果不add到缓存区，就不会commit到版本库

4. git支持多种协议，但通过ssh支持的原生git协议速度最快

5. master应该要稳定，平时不用；dev分支是不稳定的，版本发布更新时才合并到master，在master发布新版本。每个程序员在dev分支下干活，每个人都有自己的分支，时不时的合并到dev分支上就OK了。

6. 当手头工作没有完成是，先git stash，修复bug，再git stash pop回到工作现场。

7. 开发一个新feature，最好新建一个分支
    如果要丢弃一个没有被合并过的分支，可以通过git branch -D feature强行删除

8. master分支是主分支，必须时刻与远程一致
  dev分支是开发分支，团队所有成员都需要再上面工作，也需要远程同步
  bug分支只用于本地修复，不推到远程
  feature分支是否推到远程取决于是否是合作开发一个东西

多人协作模式：

1. 试图用git push origin branch-name推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地新一些，需要先用git pull试图合并
3. 如果合并有冲突，则解决冲突，并在本地提交
4. 没有冲突或解决冲突后，再用git push origin branch-name推送