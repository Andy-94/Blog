###### Git两条主线:
1. 工作目录 暂存区 版本库
2. Git对象 树对象  提交对象

git安装完的基本配置 && 为一些长的命令去配置别名

	1.      git config --global user.name "damu"
	2.      git config --global user.email damu@example.com
	3.      git config --list
	4.      git config --global alias.lol "log --oneline --decorate --graph --all"
初始化新仓库:

	git init
	git add
	git commit -m
	git status. 确定文件当前状态
	git diff 当前做的哪些更新还没有暂存
	git log 查看历史记录
分支

	git branch XX 创建分支
	git branch -D 删除分支 （D强制删除，d先合并后再删除）
	git branch XX  hashBefore （创建一个分支在以前提交过的历史中）
	git checkout XX 切换分支。（一定要在干净的情况下切换分支）
	git stash  存储当前工作区域 （可以在紧急情况下存储当前分支）
		git stash list 查看存储
		git stash pop 取出第一次存储并且删除
合并分支	

	git merge
	git branch —merged （查看合并过的分支）
linux基础命令:

	clear
	echo “hello world” > test.txt
	ll
	find
	mv
	rm
	cat
	vim
