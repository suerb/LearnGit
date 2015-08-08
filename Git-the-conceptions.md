# Git 基本概念 - 工作区与版本库

## 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的 `learngit` 文件夹就是一个工作区：

![Working Directory 工作区](http://www.liaoxuefeng.com/files/attachments/0013849082162373cc083b22a2049c4a47408722a61a770000/0 "Working Directory")

## 仓库 / 版本库（Repository）

工作区有一个隐藏目录 `.git`，这个不算工作区，而是 Git 的版本库。

Git 的版本库里存了很多东西，其中最重要的就是称为 stage（或者叫 index）的暂存区，还有 Git 为我们自动创建的第一个分支 `master` ，以及指向 `master` 的一个指针叫 `HEAD`。

![Git 的 Working Directory 与 Stage 与 Repository](http://www.liaoxuefeng.com/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0 "Git 的 Working Directory 与 Stage 与 Repository")

> 分支和HEAD的概念我们以后再讲。

我们把文件往Git版本库里添加的时候，是分两步执行的：
1. 第一步是用 `git add` 把文件添加进去，实际上就是把文件修改添加到暂存区；
2. 第二步是用 `git commit` 提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建 Git 版本库时，Git 自动为我们创建了唯一一个 `master` 分支，所以，现在，`git commit` 就是往 `master` 分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

![使用命令 \`git add\` 两个文件之后](http://www.liaoxuefeng.com/files/attachments/001384907720458e56751df1c474485b697575073c40ae9000/0 "`git add` 命令")

使用命令 `git add` 两个文件之后，工作区的 `readme.txt` 和 `LICENSE` 就被添加到 `stage` 了。所以，`git add` 命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行 `git commit` 就可以一次性把暂存区的所有修改提交到分支。

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

	$ git status
	# On branch master
	nothing to commit (working directory clean)

现在版本库变成了这样，暂存区就没有任何内容了：

![commit 到 master 版本库后，stage 没有任何内容](http://www.liaoxuefeng.com/files/attachments/0013849077337835a877df2d26742b88dd7f56a6ace3ecf000/0 "commit 提交")




