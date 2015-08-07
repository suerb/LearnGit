
# Git 常用命令

By 00 

最常用：git command --help

#### 1. 创建

需要进入目标目录进行操作：

- 创建新仓库：`git init`
- 创建一个本地仓库的克隆版本：`git clone /path/to/repository`
- 克隆远端服务器上的仓库： `git clone username@host:/path/to/repository`

> 克隆操作会自动使用默认的 master 和 origin 名字。

#### 2. 查询

	git status

在各个未知，存在对应的各种状态：
- staged：已在 Staging Area，等待被 `commit`
- unstaged：文件做了改动，但还不能被 `commit`
- untracked：Git 还没有开始**跟踪**，需要先 `add`
- deleted：文件已被删除，等待 remove
- Staging Area：`commit` 前把文件们收集到一起，以便打包 `commit`

#### 3. add/添加

- 添加到暂存区（让 Git 开始**跟踪**更改，也就是从 untracked 变为 tracked）：`git add <filename>` 或 `git add *`
- 添加全部文件：git add -A， -A 表示包含删除的文件。
- git reset: `git reset <filename> `从 Staging Area 移除文件。

#### 4. commit/提交

“Commit ” 可以理解为一次快照，帮助我们把所有改动以 timeline 的方式组织起来。

- 提交改动(到head，但还没到远程服务器)：`git commit -m 'Add all files’`
- 把所有当前目录下的文件加入暂存区域再运行 commit：`git commit -a`
- 提交到远程仓库：`git push origin master`（可以把 master 换成你想要推送的任何分支）
- 如果还没有克隆现有仓库，并想将仓库连接到某个远程服务器：`git remote add origin <server>`  

#### 5. push/推送

将文件推送到远程仓库中：`git push -u origin master`。远程仓库默认叫 “origin” 。`-u` 告诉 Git 记住参数，下次可以直接使用 push。

#### 6. pull/拉取

更新本地仓库至最新改动：`git pull origin master`

#### 7. checkout/切换

“Checkout” 命令用于从历史提交（或者暂存区域）中拷贝文件到工作目录，也可用于切换分支

- 切换分支：`git checkout <branch>`
- 新建并切换到分支：`git checkout -b new_branch` 等同于：`git branch new_branch` + `git checkout new_branch`
- 把文件从暂存区域复制到工作目录，用来丢弃本地修改：`git checkout --<files>`
- 回滚到复制最后一次提交：`git checkout HEAD -- <files>`  

#### 8. diff/比对

	git diff

#### 9. reset/撤销

- 从index中撤销所有文件：`git reset`
- 从index中撤销最后一次add的文件：`git reset --<files>`
- 恢复之前版本：`git reset --hard`
- 回滚到最近一次：`git checkout -- <target>`

#### 10. merge/合并

合并其他分支到当前分支：`git merge`

#### 11. remove & clean

- 从硬盘和index移除文件：`git rm`
- 删除分支：`git branch -d <branch name>`  


