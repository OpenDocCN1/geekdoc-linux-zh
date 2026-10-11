
$ .git/index

.git/index: Git index, version 2, 1 entries

该过程的下一步是提交到本地仓库。提交通过 `git commit` 命令完成。我们添加了 `-m` 选项来添加注释，对于记录提交很有用：

```bash
$ git commit -m "Initial Commit"

[...
Initial Commit
1 file changed, 5 insertions(+)
create mode 100644 MyGitExamplesScript.sh
```

```bash
$ cat .git/COMMIT_EDITMSG
```

# 第四部分：创建和管理实用脚本

（续）

```
Initial Commit
$ git status
[...]
nothing to commit, working tree clean
$
```

### 提示
注释存储在 `COMMIT_EDITMSG` 文件中，它们对于跟踪为什么要对脚本进行更改非常有帮助。当你在脚本的生命周期后期进行提交时，请使用 `-m` 选项包含进行修改的原因，例如 `-m "improved script's user interface."`。

在使用 `git commit` 之后，`git status` 命令将显示消息“nothing to commit, working directory clean.”。这告诉你，Git 现在认为工作工作目录中的所有脚本都已提交到本地仓库。

### 警告
如果在执行 `git commit` 命令时不使用 `-m` 选项及其参数，你将被置于 `vim` 编辑器中手动编辑 `.git/COMMIT_EDITMSG` 文件。`vim` 编辑器在第 10 章“使用编辑器”中介绍过。

现在脚本项目已经提交到本地仓库，可以通过将其推送到远程仓库来与其他脚本项目的成员共享。如果脚本已完成，你还可以将其与其他人或整个世界共享。

如果这是一个新项目，在仓库账户建立后，会创建一个名为 Markdown 的文件的特殊文件。该文件的内容显示在远程仓库的网页上并描述该仓库。它使用了所谓的 Markdown 语言。你需要将文件命名为 `README.md`。以下是创建此文件、将其添加到暂存区并提交到本地仓库的示例：

```
$ pwd
/home/christine/MWGuard
$ ls
MyGitExampleScript.sh
$ echo "# Milky Way Guardian" > README.md
$ echo "## Script Project" >> README.md
$ cat README.md
# Milky Way Guardian
## Script Project
```

## 第 25 章：组织结构

```
$ git add README.md
$ git status
[...]
Changes to be committed:
(use "git restore --<file>..." to unstage)
new file: README.md
$ git commit -m "README.md commit"
[...] README.md commit
1 file changed, 2 insertions(+)
mode 100644 README.md
```

你可以通过使用 Markdown 语言的各种特性让你的 `README.md` 文件变得非常丰富。可以在 `guides.github.com/features/mastering-markdown` 了解更多关于 Markdown 的信息。

你可以随时查看 Git 日志，但在将脚本项目推送到远程仓库之前查看它是一个好主意。每个提交都是一个用于识别它的哈希值，显示在日志中。此外，请注意带有日期和作者信息的各种提交行。

```
$ git log
commit 898330db00b1e0bee50c5eeb3c72f9544f506[...]
Author: Christine Bresnahan <cbres1723@gmail.com>
Date: Mon Aug 24 15:58:52 2020 -0000
```

```
README.md commit
commit 3b484638c6e39d10a1b81694cba8c5f4bc8ce6
Author: Christine Bresnahan <cbres1723@gmail.com>
Date: Mon Aug 24 14:56:56 2020 -0000
```

初始提交

在将项目推送到远程仓库之前，你需要在你的系统上配置它的地址。当你使用 GitHub 等 Git 服务提供商设置远程仓库时，该地址会提供给你。

# 第四部分：创建和管理实用脚本

要添加地址，请使用 `git remote add origin URL` 命令，其中 `URL` 是远程仓库的地址：

```
$ git remote add origin https://github.com/Cresnahan/MWGuard.git
$ git remote -v
origin https://github.com/Cresnahan/MWGuard.git (fetch)
origin https://github.com/Cresnahan/MWGuard.git (push)
$
```

注意通过 `git remote -v` 命令检查远程状态。在推送项目之前检查地址是一个好主意。如果地址错误或发生了拼写错误，推送将不起。

> 提示
如果你犯了错误（例如拼写错误），可以通过 `git remote` 删除远程仓库地址。删除后，使用正确的地址再次设置远程地址。

远程仓库地址配置后，我们可以将项目推送到该位置。但在此之前，为了简单起见，我们将使用 `git branch` 命令重命名分支：

```
$ git branch -m main
$ git branch --show-current
```

注意可以使用 `git branch --show-current` 查看当前分支。在推送之前确保你拥有正确的分支名称是一个好主意。现在将我们的脚本复制到远程仓库，我们在 `push` 命令中使用 `-u` 选项来指定仓库的位置以及我们正在使用的分支：

```
$ git push -u origin main
Username for 'https://github.com': Christine
Password for 'https://github.com/Cresnahan/MWGuard.git':
Enumerating objects: 6, done.
Counting objects: 100% (6), done.
Compressing objects: 100% (4), done.
Writing objects: 100% (6/6), 604 bytes | 0.00 KiB/s, done.
Total 6 (delta 0), reused 0
To https://github.com/Cresnahan/MWGuard.git
```

## 第 25 章：组织结构

```
* [new branch] -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

通常远程仓库会要求用户名和密码。当项目推送到远程仓库时，你应该可以使用你喜欢的浏览器查看它。如果是私有仓库，你需要登录远程服务才能看到工作。图 25 显示了 GitHub 上的远程仓库。注意不同的仓库供应商会有不同的界面。

远程仓库真正的价值在于团队中的任何人都可以使用 `git pull` 命令获取最新的脚本版本。你需要为他们设置远程仓库访问权限或将其。

```
$ whoami
rich
$ pwd
```

# 第四部分：创建和管理实用脚本

（续）

```
/home/rich/MWGuard
$ git remote add origin https://github.com/Cresnahan/MWGuard.git
$ git pull origin main
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6), done.
remote: Compressing objects: 100% (4), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-used 0
Unpacking objects: 100% (6/6), 584 bytes | 0.00 KiB/s, done.
From https://github.com/Cresnahan/MWGuard
* branch main -> FETCH_HEAD
```
