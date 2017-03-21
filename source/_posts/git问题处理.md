---
title: git问题处理
date: 2017-03-21 15:46:06
tags:

---
###错误提示
	Error: fatal: Not a git repository (or any of the parent directories): .git

这是由于本地版本管理仓库被删除了（目录下的.Git文件夹被删除），需要重新初始化仓库，建立新的仓库：
>git init   

	F:\>git init
	Initialized empty Git repository in F:/.git/