
## 列表 27.9：创建、添加和提交一个 `README.md` 文件（续）

```
$ git add README.md
$
git status
# On branch master
# Changes to be committed:
# (use "git reset HEAD<file>..." to unstage)
#
# new file: README.md
#
$ git commit -m "README.md commit"
[master 4541578] README.md commit
1 file changed, 2 insertions(+)
create mode 100644 README.md
$
```

你可以通过使用 Markdown 语言的各种功能让你的 `README.md` 文件变得非常精美。可以在 `guides.github.com/features/mastering-markdown/` 了解更多关于 Markdown 的信息。

你可以随时查看 Git 日志，在将项目推送到远程仓库之前查看日志总是个好主意。查看日志的示例见列表 27.10。每个 `commit` 都是一个用于标识它的哈希值，它显示在日志中。此外，注意日期旁不同的注释行以及作者信息。

## 列表 27.10：通过 `git log` 命令查看 Git 日志

```
$ git log
commit 4541578c17c213bac9c47ce815b91b6a9ac986
Author: Christine Bresnahan <cbres377@ivytech.edu>
Date: Fri 8 13:49:49 2019 -0500

README.md commit

commit 6d2370d2907345671123aeaaa7e147bd3f08f36
Author: Christine Bresnahan <cbres377@ivytech.edu>
Date: Wed Feb 6 15:23:11 2019 -0500

Initial Commit
$
```

## 使用 Git 提交

在将项目推送到远程仓库之前，你需要在系统上配置它的地址。这是通过 `git remote add` 命令完成的，其中 URL 是远程仓库的地址。示例见列表 27.11。

## 列表 27.11：通过 `git remote` 命令配置远程仓库

```
$ git remote add origin https://github.com/C-Bresnahan/MWGuard.git
$ git remote -v
```

```
origin https://github.com/C-Bresnahan/MWGuard.git (fetch)
origin https://github.com/C-Bresnahan/MWGuard.git (push)
```

注意列表 27.11 中，你可以通过 `git remote -v` 命令检查远程地址的状态。在推送项目之前检查地址是一个好主意。

如果你在 URL 中犯了错误（例如拼写错误），可以通过 `git remote rm` 命令删除远程仓库的地址。在删除后，使用正确的 URL 重新设置远程地址。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_762_0.png)

配置好远程仓库 URL 后，将你的项目推送到该位置。示例见列表 27.12。

## 列表 27.12：通过 `git push` 命令将项目推送到远程仓库

```
$ git push -u origin master
```

```
Username for 'https://github.com': C-Bresnahan
Password for 'https://github.com/C-Bresnahan@github.com':
Counting objects: 6, done.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (6/6), 561 bytes/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To https://github.com/C-Bresnahan/MWGuard.git
```

* `[新分支] master -> master`

`Branch master` 已设置为跟踪 `origin` 的 `branch master`。

通常情况下，远程仓库会要求用户名和密码，除非你设置为使用 SSH 密钥（第 16 章）。当项目推送到远程仓库后，你应该能够看到它。如果是私有仓库，你必须登录远程仓库才能看到你的工作。图 27.2 显示了该项目的远程仓库。请记住，不同的供应商为你的项目提供不同的用户界面。

# 第 27 章 • 使用 Git 控制版本

## 图 27.2 MWGuard 远程仓库

![](img/0c1e7d2699b9d354c8d2f84669d18d73_763_0.png)

### Milky Way Guardian

编程项目

远程仓库非常棒的一点是，你的项目团队可以使用 `git pull` 命令下载项目的最新文件。你需要为他们设置远程仓库的访问权限，或者将其公开。拉取文件的代码片段示例见列表 27.13。

## 列表 27.13：通过 `git pull` 命令从远程仓库拉取最新项目文件

```
$ whoami
Rich
$
git remote add origin https://github.com/C-Bresnahan/MWGuard.git
$
git pull -u origin master
```

## 列表 27.20：在 `develop` 分支上 GIT（继续）

```
#
$ git commit -m "New User Interface"
[develop a9a1bc3] New User Interface
1 file changed, 47 insertions(+)
create mode 100644 ST-UI.py
$
```

当新用户界面的开发（和测试）完成后，会将 `develop` 分支合并到 `master` 分支（生产环境）。要合并分支，请使用 `git merge <branch-name-to-merge>` 命令。合并操作必须从目标分支执行。因此，在这种情况下，你必须在执行命令之前返回 `master` 分支，如列表 27.21 所示。

## 列表 27.21：通过 `git merge` 命令合并分支

```
$ git checkout master
Switched to branch 'master'
$ branch
develop
* master
$
$ git merge develop
Updating 0e0e81..1a91bc3
Fast-forward
ST-UI.py | 47 insertions-
1 file changed, 47 insertions(+)
create mode 100644 ST-UI.py
$
$ git ls-tree --name-only -r master
README.md
ST-Data.py
ST-Main.py
ST-UI.py
$
$ git log
commit 1a91bc30b50efc09589491295cc458b2539b7
Author: Christine Bresnahan <cbresnan377@ivytech.edu>
Date: Feb 8 18:03:18 2019 -0500

New User Interface

commit 0e0e81d0d767acd64e0e45fff614288144da45
Author: Christine Bresnahan <cbresnan377@ivytech.edu>
Date: Fri Feb 8 16:50:10 2019 -0500

Initial Production Commit
```

注意列表 27.21，现在 `master` 分支内已经管理了新的生产层程序 `ST-UI.py`。还要注意两个分支之间的 Git 日志也被合并了，如 `git log` 命令所示。

> 还有另一种合并方式称为变基（rebasing）。它不是简单地将提交和历史日志合并到一个分支中，而是为所有文件执行新的提交，从而简化了历史日志。若要对项目进行变基，请将 `git merge` 替换为 `git rebase` 命令。使用哪种方法取决于你组织的开发工作流以及团队成员的偏好。

## 总结

分布式 VCS 工具在开发者需求之外的许多方面都有用。理解如何设置工作目录、暂存区（staging areas）以及本地和远程仓库是一项极好的技能。你不仅能够与程序员使用适当的术语，还可以利用 `Git` 实现其他各种有用功能来管理你的 Linux 系统。

## 考试要点

描述版本控制。版本控制是一种组织各种项目文件并保护对其进行修改的方法或系统。分布式 VCS 允许开发者离线和独立工作。`Git VCS` 提供了工作目录、暂存区（索引）和本地仓库，并使用第三方提供的远程仓库。它因其高性能、维护的修改历史、文件保护和去中心化而广受欢迎。

解释如何设置你的 Git 环境。`git` 软件包提供了用于 VCS 的各种 Git 工具。使用 `mkdir` 命令为每个项目创建一个工作目录。`.git/` 目录供暂存区和本地仓库使用，通过 `git init` 命令初始化。最后，第三方（如 GitHub）可以提供供各种 Git 工具使用的远程仓库。

详细说明如何使用 Git 进行提交。根据需要，通过 `git add` 工具将文件从工作目录移动到暂存区（索引）。项目的工作流决定了何时通过 `git commit` 命令将项目移动到本地目录，然后通过 `git push` 工具将其推送到远程仓库。如果远程开发者需要最新的项目文件，则使用 `git pull` 命令。对于需要所有项目文件（包括修改历史）的新团队成员，则使用 `git clone` 命令。

总结 Git 分支。`Git` 分支是用于特定项目部分（如开发或项目测试）的本地仓库区域。默认情况下，主分支被称为 `master` 分支。使用 `git branch <branch-name>` 命令创建新分支。你可以使用 `git branch` 工具查看各种可用分支，它使用星号 `*` 表示当前分支。要切换到另一个项目分支，使用 `git checkout branch-name`。在分支上完成工作后，可以通过 `git merge <branch-name-to-merge>` 命令将其 VCS 文件和项目文件合并到另一个分支。

## 复习题

1. 关于版本控制，以下哪项是正确的？（选择所有适用项。）

   A. 提供一个合并和存储文件的公共位置
   B. 要求文件名包含版本号
   C. 可能是分布式的或非分布式的
   D. 有助于防止文件被覆盖
   E. 可以处理其他程序的文件

2. 从概念上讲，Git 被分为不同的区域。以下是这些区域之一吗？（选择所有适用项。）

   A. Blob
   B. 本地仓库
   C. 远程仓库
   D. 索引 (Index)
   E. 工作目录

3. 首次设置 Git 环境需要哪些步骤？（选择所有适用项。）

   A. 创建工作目录。
   B. 在工作目录中初始化 `.git/` 目录。
   C. 设置远程仓库。
   D. 将文件添加到暂存区。
   E. 远程仓库。

4. Natasha 创建了工作目录。接下来她应该做什么设置环境？

   A. 执行 `mkdir` 命令。
   B. 执行 `git config` 命令。
   C. 设置 GitHub。
   D. 执行 `git init` 命令。
   E. 开始创建项目。

5. Bruce 在设置 Git 配置时使用了 `--global` 选项。这意味着什么？

   A. 配置存储在 GitHub 上。
   B. 配置存储在 `~/.gitconfig` 中。
   C. 配置存储在工作目录的 `.git/config` 中。
   D. 配置存储在 `.git/config` 中。
   E. 配置存储在 `objects` 目录中。

6. Bruce 设置了环境并完成了 `GreenMass.sh`。他应该做什么？

   A. 将脚本添加到暂存区。
   B. 执行 `git init` 命令。
   C. 将脚本提交到本地仓库。
   D. 执行 `git log` 命令。
   E. 将脚本提交到远程仓库。

7. Natasha 的工作目录中有 25 个文件，她只想将其中 22 个添加到索引。她计划使用 git 命令提高效率。她应该怎么做？

   A. 从工作目录中移动 3 个文件。
   B. 通过 `git add` 命令单独添加 22 个文件。
   C. 为 3 个文件创建一个新的工作目录。
   D. 将 3 个文件的名称添加到 `.gitignore` 文件中。
   E. 临时删除 3 个文件。

8. Natasha 完成了她的开源项目并将于今天发布。她将文件添加到暂存区，将工作提交到本地仓库，并配置了远程仓库。她的下一步是什么？

   A. 回家休息。她应如此。
   B. 将远程仓库克隆到本地系统。
   C. 将项目推送到远程仓库。
   D. 从远程仓库拉取项目。
   E. 使用远程添加 URL。

9. 以下哪个命令允许切换到名为 `testing` 的新分支？

   A. `git branch testing`
   B. `git ls-tree --name-only -r testing`
   C. `git branch`
   D. `git commit -m "testing"`
   E. `git checkout testing`
