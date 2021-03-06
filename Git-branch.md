iss101

# Git 基本概念 - 分支管理

## 创建与合并分支

在版本回退里，你已经知道，每次提交，Git 都把它们串成一条时间线，**这条时间线就是一个分支 branch**。

截止到目前，只有一条时间线，在 Git 里，这个分支叫主分支，即 `master` 分支。

`HEAD` 严格来说不是指向提交，而是指向 `master` ，`master` 才是指向提交的，所以，`HEAD` 指向的就是当前分支。

一开始的时候，`master` 分支是一条线，Git 用 `master` 指向最新的提交，再用 `HEAD` 指向 `master`，就能确定当前分支，以及当前分支的提交点：

![HEAD 指向 master](http://www.liaoxuefeng.com/files/attachments/0013849087937492135fbf4bbd24dfcbc18349a8a59d36d000/0 "HEAD 指向 master")

每次提交，`master` 分支都会向前移动一步，这样，随着你不断提交， `master` 分支的线也越来越长。

当我们创建新的分支，例如 `dev` 时，Git 新建了一个指针叫 `dev`，指向 `master` 相同的提交，再把 `HEAD` 指向 `dev`，就表示当前分支在 `dev` 上：

![新建 dev 分支后 HEAD 会自动指向](http://www.liaoxuefeng.com/files/attachments/001384908811773187a597e2d844eefb11f5cf5d56135ca000/0 "新建 dev 分支后 HEAD 会自动指向")

你看，Git 创建一个分支很快，因为除了增加一个 `dev` 指针，改改 `HEAD` 的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对 `dev` 分支了，比如新提交一次后，`dev` 指针往前移动一步，而 `master` 指针不变：

![dev 提交一次后](http://www.liaoxuefeng.com/files/attachments/0013849088235627813efe7649b4f008900e5365bb72323000/0 "dev 提交一次后")

假如我们在 `dev` 上的工作完成了，就可以把 `dev` 合并到 `master` 上。Git 怎么合并呢？最简单的方法，就是直接把 `master` 指向 `dev` 的当前提交，就完成了合并：

![直接把 master 指向 dev 的当前提交](http://www.liaoxuefeng.com/files/attachments/00138490883510324231a837e5d4aee844d3e4692ba50f5000/0 "直接把 master 指向 dev 的当前提交")

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除 `dev` 分支。删除 `dev` 分支就是把 `dev` 指针给删掉，删掉后，我们就剩下了一条 `master` 分支：

![剩下了一条 \`master\` 分支](http://www.liaoxuefeng.com/files/attachments/001384908867187c83ca970bf0f46efa19badad99c40235000/0 "剩下了一条 `master` 分支")

## 练习

### 创建分支

首先创建一个新的 `dev` 分支，然后切换到 `dev`：

	$ git checkout -b dev
	Switched to a new branch 'dev'

`git checkout` 命令加上 `-b` 参数表示创建并切换，相当于以下两条命令：

	$ git branch dev
	$ git checkout dev
	Switched to branch 'dev'

然后，用 `git branch` 命令查看当前分支：

	$ git branch
	* dev
	  master

`git branch` 命令会列出所有分支，当前分支前面会标一个 `*` 号。

然后，我们就可以在 `dev` 分支上正常提交，比如对 `Git-branch.md` 做个修改，加上一行：

	草泥马

然后 `add` 和 `commit`。现在，`dev` 分支的工作完成，我们就可以切换回 `master` 分支：

	$ git checkout master
	Switched to branch 'master'

> SourceTree 只需要轻轻双击目标 branch 即可实现切换。

切换回 `master` 分支后，再查看一个 `Git-branch.md` 文件，刚才添加的内容不见了！因为那个提交是在 `dev` 分支上，而 `master` 分支此刻的提交点并没有变：

![master 分支并没有改变](http://www.liaoxuefeng.com/files/attachments/001384908892295909f96758654469cad60dc50edfa9abd000/0 "master 分支并没有改变")

## 合并分支

现在，我们把 `dev` 分支的工作成果合并到 `master` 分支上：

	$ git merge dev

`git merge` 命令用于合并指定分支到当前分支。合并后，再查看 `Git-branch.md` 的内容，就可以看到，和 `dev` 分支的最新提交是完全一样的。

注意到上面的 `Fast-forward` 信息，Git 告诉我们，这次合并是「快进模式」，也就是直接把 `master` 指向 `dev` 的当前提交，所以合并速度非常快。

当然，也不是每次合并都能 `Fast-forward` ，我们后面会将其他方式的合并。


## 删除分支

合并完成后，就可以放心地删除 `dev` 分支了：

	$ git branch -d dev
	Deleted branch dev (was fec145a).

因为创建、合并和删除分支非常快，所以 Git 鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在 `master` 分支上工作效果是一样的，但过程更安全。



## 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

1. 首先，`master` 分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
2. 那在哪干活呢？干活都在 `dev` 等新分支上，也就是说，`dev` 分支是不稳定的，到某个时候，比如 1.0 版本发布时，再把 `dev` 分支合并到 `master` 上，在 `master` 分支发布 1.0 版本；
3. 你和你的小伙伴们每个人都在 `dev` 分支上干活，每个人都有自己的分支，时不时地往 `dev` 分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![团队合作](http://www.liaoxuefeng.com/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0 "团队合作")




