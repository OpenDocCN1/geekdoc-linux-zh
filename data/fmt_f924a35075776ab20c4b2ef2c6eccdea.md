
位于 `master` 分支

Your branch is up-to-date with 'origin/master'.
Changes to be committed:

```
(use 'git reset HEAD <file>...' to unstage)
```

new file: `.gitignore`

new file: `newfile.txt`

要从暂存区删除（移除）文件，请使用 `git rm somefile.txt`。

## 提交到本地仓库 (`git commit`)

将文件添加到暂存区后，你可以将它们提交到本地仓库。首先，你可能需要设置用户名和邮箱地址，以识别提交者：

```
pi@erpi ~/test $ git config --global user.name "Derek Molloy"
pi@erpi ~/test $ git config --global user.email derek@email.com
```

这些设置在切换分支后将持久存在。要将更改永久提交到本地仓库，使用 `git commit -m`：

```
pi@erpi ~/test $ git commit -m "Testing the repository"
[master 3ea5a2] Transforming the repository
2 files changed, 2 insertions(+)
create mode 10064 .gitignore
create mode 10064 newfile.txt
```

此分步指南使用了 "test"；但是，你可以轻松地在 GitHub 上创建你自己的仓库。在 GitHub 上设置好免费账户后，前往 Create New（新建），然后点击 New repository（新仓库）。为你的仓库命名并添加描述，将其设置为公开，选择用 README 初始化，并点击 Create Repository（创建仓库）。然后你可以使用自己的账户遵循这些指令，结果是你将能够从 RPI 推送到你自己在 GitHub 上的仓库中。

## 推送到远程仓库 (`git push`)

将代码推送到远程仓库后，你可以在本地目录执行 `git pull` 来拉取更改：

```
pi@erpi ~/test $ git pull
Already up-to-date.
```

# 第3章 探索嵌入式 Linux 系统 105

## 分支

Git 支持分支概念，这允许你在项目中处理多个版本的代码。例如，为了在项目的版本2中开发新功能，你可以创建一个新分支（版本2）。对版本2所做的新功能和更改都不会影响版本1的代码。你可以轻松地在分支间切换。

## 创建分支 (`git branch`)

假设，你想创建一个名为 `mybranch` 的新分支；可以使用 `branch mybranch` 命令来实现，然后可以使用 `checkout mybranch` 切换到该分支，如下：

```
pi@erpi ~/test $ git branch mybranch
pi@erpi ~/test $ checkout mybranch
Switched to branch 'mybranch'
```

现在，为了演示它是如何工作的，假设仓库添加了一个临时文件 `testmybranch.txt`。这可能是项目的一个新文件。你可以看到分支的状态清楚地显示工作目录包含一个未跟踪的文件：

```
pi@erpi ~/test $ touch testmybranch.txt
pi@erpi ~/test $ ls
newfile.txt README.md testmybranch.txt testobject.o
pi@erpi ~/test $ git status
On branch mybranch
Untracked files:
(use "git add <file>..." to include in what will be committed)
testmybranch.txt
```

`testmybranch.txt`
无可提交，存在未跟踪的文件（使用 "git add" 进行跟踪）

然后，你可以使用以下命令将此文件添加到分支的暂存区：

```
pi@erpi ~/test $ git add
pi@erpi ~/test $ git status
On mybranch
```

待提交的更改：
（使用 "git reset HEAD<file>" 取消暂存）
新文件: `testmybranch.txt`

你可以将此更改提交到本地仓库的 `mybranch` 分支。此更改将影响 `mybranch` 分支，但对 `master` 分支没有影响：

```
pi@erpi ~/test $ git commit -m "Test commit to mybranch"
[mybranch d4cacbf3] 0 insertions(+), 0 deletions(-)
1 file changed, 100644 testmybranch.txt
create mode 100644 testmybranch.txt
pi@erpi ~/test $ git status
On mybranch
无可提交，工作区干净
pi@erpi ~/test $ ls
newfile.txt testmybranch.txt testobject.o
```

你可以从前面的输出中看到文件 `testmybranch.txt` 已提交到本地仓库，通过 `mybranch` 你可以在目录中看到该文件。

如果你现在使用 `git checkout master` 从当前分支切换到 `master` 分支，当你请求目录列表时，你会发现有趣的事情：

```
pi@erpi ~/test $ git checkout master
itched to branch 'master'
Your branch is up-to-date with 'origin/master'.
pi@erpi ~/test $ ls
newfile.txt README.md testobject.o
```

是的，文件 `testmybranch.txt` 已从目录中消失了！它仍然存在，但是以 blob 形式存储在 `.git/objects` 目录中的。如果你返回该分支并列出文件，你将看到以下内容：

```
pi@erpi ~/test $ git checkout mybranch
itched to branch 'mybranch'
pi@erpi ~/test $ ls
newfile.txt README.md testmybranch.txt testobject.o
```

文件现在重新出现。因此，你可以看到分支集成得有多好。此时，你可以回到 `master` 分支对原始代码进行更改，而 `mybranch` 分支中的更改不会对 `master` 代码产生任何影响。即使你更改了同一个文件的代码，对 `master` 分支中的原始代码也没有影响。

## 合并分支 (`git merge`)

如果你想将在 `mybranch` 分支中做的更改应用到 `master` 项目中，你可以使用 `git merge` 实现：

```
pi@impi /test $ git checkout master
itched to branch 'master'
Your branch is up-to-date with 'origin/master'
pi@impi /test $ git merge mybranch
Updating lee9a2..dcafbf3
Fast-forward
testmybranch.txt | 0
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 testmybranch.txt
pi@impi /test $ git status
On master
Your branch is ahead of 'origin/master' by 1 commit.
(use "git push" to publish your local commits)
nothing to commit, working directory clean
pi@impi /test $ ls
newfile.txt README.md testmybranch.txt testobject.o
```

现在 `testmybranch.txt` 文件已位于 `master` 分支中，对 `master` 文档进行的任何更改都已应用。本地仓库现在领先远程仓库一个提交，你可以使用 `git push` 更新远程仓库。

## 删除分支 (`git branch -d`)

如果你想删除一个分支，请使用 `git branch -d` 命令：

```
pi@impi /test $ git branch -d mybranch
Deleted mybranch (dcafbf3).
```

# 106 第一部分 | 树莓派基础
