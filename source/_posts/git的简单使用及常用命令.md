---
title: git的简单使用及常用命令
date: 2018-06-08 14:24:49
tags: git
categories: 工具
---
## git的基本概念

### 工作目录、暂存区域以及 Git 仓库

Git 仓库目录是 Git 用来保存项目的元数据和对象数据库的地方。 这是 Git 中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。

工作目录是对项目的某个版本独立提取出来的内容。 这些从 Git 仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。

暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在 Git 仓库目录中。 有时候也被称作`‘索引’'，不过一般说法还是叫暂存区域。

基本的 Git 工作流程如下：

1. 在工作目录中修改文件。

2. 暂存文件，将文件的快照放入暂存区域。

3. 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。

如果 Git 目录中保存着的特定版本文件，就属于已提交状态。 如果作了修改并已放入暂存区域，就属于已暂存状态。 如果自上次取出后，作了修改但还没有放到暂存区域，就是已修改状态。

### 添加与提交

#### 添加：你可以计划改动（把它们添加到缓存区），使用如下命令：

`git add <filename>`添加指定文件或目录

`git add .` 添加所有文件

这是 git 基本工作流程的第一步

#### 提交：使用如下命令以实际提交改动：

`git commit -m `"代码提交信息"

现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库。

## git的配置及常用命令

### Git的配置：

```
# 显示当前的Git配置
$ git config --list

#设置用户名和邮箱，即提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

### 添加/删除文件(到暂存区，即add操作）
```
#可以添加一个或多个
$ git add <file1> <file2>...

#添加所有修改的和新添加的
$ git add .
#另一种写法
$ git add -A

#添加指定目录
$ git add <dirname>

#由暂存区恢复到工作区（发现提交错了，退回一步）
$ git reset HEAD <file> 

#恢复上一次add提交的所有file
$ git reset HEAD

#撤销修改操作，恢复到修改之前的，撤销add后位于工作区下进行的
$ git checkout -- <file>

#删除文件,并将文件放入暂存区
$ git rm <file1> <file2>
#改文件名，并将修改后的文件放入暂存区
$ git mv <file-original> <file-rename>
```

### 提交到本地仓库（commit操作）
```
#提交暂存区的所有文件(后面的message不可缺少)
$ git commit -m <message>
#提交暂存区的指定文件
$ git commit <file1> <file2> -m <message>
```

### 分支操作（branch）
```
# 列出所有本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有本地分支和远程分支
$ git branch -a

# 新建一个分支，并切换到该分支
$ git checkout -b [branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

#从远程分支检出指定分支
$ git clone -b <branchname> <master>

# 合并指定分支到当前分支（主分支合并自定义分支）
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```

### 查看信息：
```
# 显示有变更的文件
$ git status

# 显示当前分支的版本历史
$ git log
```
## .gitignore的配置：

缘由：当我们导入一个git项目时，开发环境会改变里面的一些配置，当我们修改完代码后，add，commit操作后，系统更改的配置信息，并不想去提交，这个时候就会用到这个配置，配置完成后，才更好的去add .和commit -m去操作。
```
#要在Git BashHere这里面操作,新建一个.gitignore文件
user@amelon MINGW64 ~/Desktop/git (master)
$ touch .gitignore
```
常用的配置： eg1:
```
/build
/.idea
/.gradle
/local.properties
.gitignore
```
### 用法规则和语义：
```
# 此为注释 – 将被 Git 忽略

*.a       # 忽略所有 .a 结尾的文件
!lib.a    # 但 lib.a 除外
/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/    # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

`注意`：如果你是新加的，这里需要注意的是.gitignore只能作用于没有被track的文件，也就是工作区的文件，对于add，commit操作后的文件是没有作用的，这个时候需要先把本地的缓存删除，在去提交，就可以实现忽略整个仓库文件了。
```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

### 参考

[图解git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
[git教程廖雪峰](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
[git的常用命令](https://blog.csdn.net/zxyudia/article/details/67633321)
[git简易指南](http://www.bootcss.com/p/git-guide/)
[git官方文档](https://git-scm.com/book/zh/v2/)
[pro git](http://git.oschina.net/progit/)
[深入浅出Git教程](https://www.cnblogs.com/syp172654682/p/7689328.html)
[深入浅出 Git](https://blog.coding.net/blog/git-from-the-inside-out)
[猴子都能懂的GIT入门](https://backlog.com/git-tutorial/cn/)
[Resources to learn Git](http://try.github.io/)
