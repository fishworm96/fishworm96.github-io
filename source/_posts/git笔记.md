---
title: git笔记
date: 2021-04-21 21:45:03
tags: git
---

# GIT

git版本的查询: git --version

<!-- more -->

## git的使用

### git使用前配置

在使用git前，需要告诉git你是谁，在想git 仓库中提交需要用到。

1.配置提交人姓名:	git config --global user.name	提交人姓名

2.配置提交人邮箱： git config --global user.email	提交人邮箱

3.查看git配置信息： git config --list

```
例:
	git config --global user.name yourname
	git config --global user.emial youremail@emial.cn
	查询git config --list
```

注意

​	1.如果要对配置信息进行修改，重复上述命令即可

​	2.配置只需要执行一次

```
修改name例:
	直接执行进行覆盖 git config --global user.name name
```



### 提交步骤

1.git init 初始化git仓库

2.git status 查看文件状态

3.git add 文件列表 追踪文件

4.git commit -m 提交信息 向仓库中提交代码

5.git log 查看提交记录

```
例：
	git init	//初始化仓库
	git status	//查看当前路径下文件状态
	git add index.html	//添加index.html文件
	git commit -m 第一次提交	//提交git仓库并备注
	git log	//查看提交记录
```

### 撤销

用暂存区中的文件覆盖工作目录的文件：	git checkout 文件

将文件从暂存区中删除： git rm --cached 文件

将git仓库中指定的更新记录恢复出来，并且覆盖暂存区和工作目录：git reset --hard commitID

```
例：
	git checkout index.html	//将index.html从暂存区恢复到本地
	git rm --cached index.html	//将index.html从暂存区中删除
	git rest --hard 'commitID'	//将git仓库文件恢复到本地
```

### 分支命令

功能分支->开发分支->主分支

git branch 查看分支

git branch 分支名称	创建分支

git checkout 分支名称	切换分支

git merge 来源分支	合并分支

git branch -d 分支名称	删除分支(分支被合并后才允许删除) (-D强制删除)

```
例：
git branch develop	//创建开发分支
git checkout develop	//切换到主分支，切换分支前要将文件提交，没提交的文件会跟随分支切换进行切换
```

### 暂时保存更改

在git中，可以暂时提取分支上所有的改动并储存，让开发人员得到一个干净的工作副本，临时转向其他工作。

使用场景：分支临时切换

存储临时改动：git stash

恢复改动：git stash pop

### github命令

#### 创建仓库

1.git push 远程仓库地址 分支名称

2.git push 远程仓库地址别名 分支名称

3.git push -u 远程仓库地址别名 分支名称

​	-u 记住推送地址及分支，下次推送只需要输入git push即可

```
git push -u origin master	//系统将记住分支 
全写为 git push --set-upstream origin master
```

4.git remote add 远程仓库地址别名 远程仓库地址

### 查看当前仓库地址

```
git remote show origin
```

### 设置新仓库地址

1.先登录 [gitlab](http://192.168.70.101/topics/192.168.30.29) 查看当前仓库地址:

执行修改地址命令

```
git remote set-url origin 仓库地址
```

### 拉取操作

#### 克隆仓库

克隆远端数据仓库到本地： git clone 仓库地址	//本地仓库没有

#### 拉取远程仓库中最新的版本

拉取远程仓库中最新的版本： git pull 远程仓库地址 分支名称	//本地仓库有，拉取最新版本

###  将master下的dist单独提交到github

git subtree push --prefix=dist origin gh-pages
