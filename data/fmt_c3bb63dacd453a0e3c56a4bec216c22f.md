
```
alias gs="git status"
alias gcm="git checkout main"
alias gm="git merge"
<<<<<<< HEAD
alias log="git log"
=======
alias log="git log --graph --oneline"
>>>>>>> log_alias
```

`<<<<<<<` 行显示当前分支的更改，`=======` 行是分隔符，`>>>>>>>` 行反映另一个分支的更改。许多现代编辑器会识别 Git 用来指示冲突的符号并将其高亮。Git 无法合并这些更改是因为：每个分支都有新行，Git 要求你进行选择。在你的编辑器中，将文件更新为：

```
alias gs="git status"
alias gcm="git checkout main"
alias gm="git merge"
alias log="git log --graph --oneline"
```

你选择了 `log_alias` 分支的 `log` 版本。你可以选择 `main` 分支的版本，或者用新行替换此内容。以下是如何重命名 `log_alias` 分支的 `log` 别名而不是删除 `main` 分支的 `log`：

```
alias gs="git status"
alias gcm="git checkout main"
alias gm="git merge"
alias log="git log --graph --oneline"
```

你可以进行任何更改——只要删除以 `<<`、`===` 和 `>` 开头的行。你不需要使用其中一个分支的更改；你可以完全删除这些行，也可以添加全新的行。只要你修改了文件使合并结果合理，Git 就可以继续。

现在你可以使用 `git add` 将文件标记为已解决：

```
$ git add shell.d/git_aliases
```

运行 `commit`，编辑器将打开并显示一条默认提交消息：

Merge branch 'log_alias'

```
# Conflicts:
# shell.d/git_aliases
#
# It looks like you may be committing a merge.
# If this is not correct, please run
# git update-ref -d MERGE_HEAD
# and try again.
```

```
# 请为你的更改输入提交消息。以 "" 开头的行将被忽略，空消息将取消提交。
#
# On branch main
```之前的合并消息相同，但注释显示了更多信息（冲突的文件）。保存文件并关闭编辑器完成提交。

你的 `git log` 现在将显示此合并提交：

```
$ git log --graph --oneline
* 2532277 (HEAD -> main) Merge branch glog_alias
| /
* a8cbb15 (glog_alias) add the 'glog' alias
| 31548e2 add the 'glog' alias
| /
* 138b404 Merge branch merge_aliases
| /
* a51ae1a (more-aliases) add a file to store 'zsh' aliases
| 63ea74f add a file to store 'bash' aliases
| a95bd099 add the 'gm' alias for 'git merge'
| /
* b9ae0ad (aliases) add aliases 'gcm' for 'git checkout main'
* f61369d add aliases 'gs' for 'git status'
* d7e1bb9 add the 'shell.d' folder
* 01e7a10 add the 'install' and 'shell' scripts
```

处理冲突可能非常复杂。我们在这里只触了皮毛，但如果你想深入研究，网上有丰富的信息。

# 工作流 (GIT WORKFLOWS)

Git 有许多可以用来在分支间合并更改的工作流。有些工作流允许你在分支之间创建一个单一的、连贯的历史，而不是创建合并提交；还有将一个分支的所有提交“压缩”（squash）到另一个分支的选项等。

深入研究超出了本书的范围，但知道你有很多资源可用来控制分支如何合并是很有用的。随着你越来越熟悉 Git 的基础知识，我建议在网上搜索“Git merge strategies”或“Git workflows”。

让我们来看看这两种方法的操作。首先，使用 `git rm`（“从工作树和索引中删除文件”）命令：

```bash
$ git rm install.sh
rm 'install.sh'
```

这会将文件从你的工作树中删除，并同时将其置于待删除状态，你可以通过 `git status` 确认这一点：

```bash
$ git status
On branch main
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
deleted: install.sh
```

此时，该删除操作仅存在于索引中，因此你需要运行 `git commit` 来提交它。

有时，你可能已经在 Git 之外删除了文件（使用 `rm` 命令或其他工具）：

```bash
$ git rm install.sh
$ git status
On branch main
Changes not staged for commit:
(use "git add/ <file>..." to update what will be committed)
(use "git restore <file>..." to discard changes in working directory)
deleted: install.sh
```

此时此时，Git 知道该文件丢失，但删除操作尚未被暂存，因为你明确告诉了 Git 你想将删除文件作为提交的一部分。为了确认你想删除该文件，你仍然需要运行 `git rm` 命令：

```bash
$ git rm install.sh
```

你也可以运行 `git add install.sh`，这相当于在说：“暂存我对 `install.sh` 的更改”；也就是说，你正在向索引中添加一个更改。（我经常直接运行 `git add` 来将我所有的更改和删除添加到索引中。）

现在你可以进行任何你需要的其他更改，将它们暂存，然后提交。

# 恢复和重命名文件

要恢复一个已修改或删除但尚未提交的文件，你可以像这样使用 `git checkout HEAD filepath`：

```bash
$ git checkout HEAD install.sh
```

`HEAD` 告诉 Git 从当前提交中检出该文件（在本例中，是 `main` 分支上最近的提交）。

# 恢复文件的另一种方法是使用 `git reset`:

```bash
$ git reset
Unaged changes after reset:
D install.sh
$ git checkout
Updated 1 path from the index
```

首先，`git reset .` 重置所有索引中的所有更改，然后 `git checkout .` 检出当前提交中的所有文件。然而，使用这种方法要小心，因为它还会重置你做的任何其他更改。我更喜欢第一种方法，因为它更显式且只恢复一个文件。

如果你想重命名文件呢？将 `install.sh` 文件重命名为 `install_dotfiles.sh`，然后检查它的状态：

```bash
$ mv install.sh install_dotfiles.sh
$ git status
Changes not staged for commit:
(use "git add/rm <file>..." to update what will be committed)
(use "git restore <file>..." to discard changes in working directory)
deleted:
  install.sh

Untracked files:
(use "git add <file>..." to include in what will be committed)
install_dotfiles.sh

no changes added to commit (use "git add" or "git commit -a")
```

你重命名了 `install.sh` 文件，但当你运行 `git status` 时，Git 告诉你该文件丢失且存在一个未跟踪的文件。但 Git 足够智能，知道你何时移动了文件，因此当你运行 `git add .` 将工作树中的所有更改添加到索引时，Git 会识别出你并不是删除并添加了一个文件，而是重命名了它：

```bash
$ git add .
$ git status
On branch main
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
renamed: install.sh -> install_dotfiles.sh
```

现在通过将 `install_dotfiles.sh` 重命名回 `install.sh` 来恢复该文件并添加这些更改：

```bash
$ mv install_dotfiles.sh install.sh
$ git add .
$ git status
On branch main
nothing to commit, working tree clean
```

你也可以使用 `git mv`（“移动或重命名文件”）命令一次性移动或重命名文件并暂存这些更改：

```bash
$ git mv install.sh install_dotfiles.sh
Changes to be committed:
  (use git restore --staged <file>... to unstage)
renamed:    install.sh -> install_dotfiles.sh
```

你也可以用 `git mv` 撤销名称的更改：

```bash
$ git mv install_dotfiles.sh install.sh
$ git status
On branch main
nothing to commit, working tree clean
```

这些命令对于文件夹或文件和文件夹列表同样有效。

# 恢复你的工作树

你已经见过如何使用 `git checkout` 命令来切换分支，但你也可以用它将工作树恢复到某个提交历史。如果你想查看文件在早些时间点的样子，或者将文件恢复到之前的状态，这将非常有用。

看看你目前为止的 Git 日志：

```bash
$ git log --graph --oneline
* 2532227 (HEAD -> main) Merge branch 'glog_alias'
| \
* a8cbb15 (glog_alias) add the 'glog' alias
| | 31548e64 add the 'glog' alias
| /
* 138b404 Merge branch 'more_aliases'
| \
* a5a1e63 (more_aliases) add a file to store 'zsh' aliases
| | 63e7f4d add a file to store 'zsh' aliases
```

# 管理远程 Git 仓库和共享 dot files

在本章中，你将学习如何将本地 Git 仓库上传到远程仓库。你将使用流行的 GitHub 网站来托管你的仓库。GitHub 允许你共享仓库、与其他用户协作，并从不同的机器上访问你的代码。为了探索它的某些功能，你将为你的 dot files（配置文件）创建一个仓库，这样你就可以用你的个人配置快速设置任何机器。

为了跟上本章的代码进行操作，请确保已安装了示例文件，或者参考上一章节关于创建本地 Git 仓库的说明。

首先，你需要在 https://github.com 注册一个 GitHub 账户。完成后，点击右上角加号旁边的箭头，如图 19-1 所示（注意，取决于你拥有的 GitHub 账户类型，你的主页可能看起来不同，但加号应该在相同的位置）。

## 你想做什么？

每位开发者都需要配置自己的环境，所以让我们优化 GitHub 体验以适应你的需求。

图 19-1：GitHub 首页为你提供了创建仓库的选项。

**选择 Create a Repository（创建仓库）。** 系统将要求你为仓库提供一个名称。由于我将用这个仓库来托管我的 dot files，我选择了 **dotfiles**（见图 19-2）。

图 19-2：命名新仓库

如果你不想让公众看到你的仓库，请选择 Private（私有，图中未显示）。

如果你已经有一个本地仓库，请不要勾选 Initialize This Repository With（用此初始化仓库）中的任何复选框。你想创建一个空仓库，你需要将更改推送到。

完成后，点击底部的 Create Repository（创建仓库）。你应该能看到一些配置本地仓库指向远程仓库的命令（图 19-3）。

图 19-3：新仓库的设置页面

由于你已经有一个仓库，你将遵循标题为 “. . or push an existing repository from the command line”（...或从命令行推送现有仓库）章节中的说明。点击剪贴图标复制命令。将它们粘贴到你的 shell 中并在 `/dotfiles` 文件夹下运行，如下所示：

```
$ git remote add origin https://github.com/dwmkerr-effective-shell/dotfiles.git
$ git branch -M main
$ git push -u origin main
```

Username for 'https://github.com:dwmkerr+effective-shell@gmail.com':

Password for 'https://dwmkerr+effective-shell@gmail.com@github.com':

Enumerating objects: 39, done.

Counting objects: 100% (39/39), done.

Delta compression using up to 16 threads

Compress objects: 100% (36/36), done.

Writing objects: 100% (39/39), 12.83 KiB | 1.8 MiB/s, done.

Total 39 (delta 7), reused 0 (delta 0), pack-received 0

remote: Resolving deltas: 100% (7/7), done.

to https://github.com/dwmkerr-effective-shell/dotfiles.git

+   * [new branch] main -> main

Branch 'main' set to track branch 'main' from 'origin'.

第一条命令告诉 Git 你要在提供的地址添加一个新的远程地址。在这种情况下，远程是你刚刚在 GitHub 上创建的仓库。第二条命令将当前分支重命名为 `main`，但因为你的当前分支已经是 `main`，所以没有发生变化，也没有显示输出。最后，第三条命令将你的 `main` 分支推送到远程。很快你会看到 `-u` ("set upstream"，设置上游）标志。当你运行它时，在本地更改推送到远程仓库之前，系统会提示输入用户名和密码。

## 使用 SSH 密钥代替密码

为了保持此示例简单，我使用了用户名和密码进行身份验证。然而，我强烈建议你尽快设置 SSH（安全外协议）来与 GitHub 进行身份验证。SSH 密钥比用户名和密码安全得多。

GitHub 有一份份关于如何设置 SSH 密钥的优秀指南：https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh。我也在第 22 章中讨论了如何操作。

现在刷新你的浏览器，你应该就能看到包含你所有更改的 dotfiles 仓库（见图 19-4）。

图 19-4：带有所有更改的 dotfiles 仓库初始视图

你可以查看创建的所有文件和文件夹、提交历史、日志消息等。不过，在你进行过多更改之前，你需要了解操作远程仓库时的重要命令：`git push`、`git fetch` 和 `git pull`。

## 推送更改

你已经用过一次 `git push` 命令了。该命令将你在本地的更改推送到远程。将你工作主要的仓库命名为 `origin` 是一种惯例，但你可以使用任何名称。你也可以拥有多个远程仓库。例如，你可以在 GitLab 等其他 Git 服务注册，在那里创建一个仓库，并将其添加为名为 `gitlab` 的远程仓库。

你可以通过 `git remote` 显示远程仓库：

```
$ git remote -v
origin https://github.com/dwmkerr-effective-shell/dotfiles.git (fetch)
origin https://github.com/dwmkerr-effective-shell/dotfiles.git (push)
```

运行带有 `-v`（详细信息）参数的 `git remote` 将显示每个远程仓库，以及在推送和获取更改时使用的地址（我们稍后查看）。之前，你使用此命令推送了更改：

# $ git push -u origin main
