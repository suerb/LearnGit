# Git 基本概念 - 远程仓库

现在的情景是，你已经在本地创建了一个 Git 仓库后，又想在 GitHub 创建一个 Git 仓库，并且让这两个仓库进行远程同步，这样，GitHub 上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。

首先，登录 GitHub ，然后，在右上角找到「Create a new repo 」按钮，创建一个新的仓库：

![Create a new repo](http://www.liaoxuefeng.com/files/attachments/0013849084639042e9b7d8d927140dba47c13e76fe5f0d6000/0 "Create a new repo")

在 Repository name 填入 `learngit`，其他保持默认设置，点击「Create repository 」按钮，就成功地创建了一个新的 Git 仓库：

![Create repository](http://www.liaoxuefeng.com/files/attachments/0013849084720379a3eae576b9f417da2add578c8612a2e000/0 "Create repository")

目前，在 GitHub 上的这个 `learngit`仓库还是空的，GitHub 告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到 GitHub 仓库。

添加后，远程库的名字就是 `origin`，这是 Git 默认的叫法，也可以改成别的，但是 `origin` 这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：

	git push -u origin master

把本地库的内容推送到远程，用 `git push` 命令，实际上是把当前分支 `master` 推送到远程。

由于远程库是空的，我们第一次推送 `master` 分支时，加上了 `-u` 参数，Git 不但会把本地的 `master` 分支内容推送的远程新的 `master` 分支，还会把本地的 `master` 分支和远程的 `master` 分支关联起来，在以后的推送或者拉取时就可以简化命令。

![SourceTree 接入 GitHub 的 远程库后](http://d.pr/i/6yz7+ "SourceTree 接入 GitHub 的 远程库后")

从现在起，只要本地作了提交，就可以通过命令：

	git push origin master

把本地 `master` 分支的最新修改推送至 GitHub，现在，你就拥有了真正的分布式版本库！























