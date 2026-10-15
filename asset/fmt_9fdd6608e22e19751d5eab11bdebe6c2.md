
pi@erpi - $ `kill 30965`

[1]+ Terminated             ./helloRPISleep

你可以使用 `ps` 来确认进程已死亡。如果进程没有死亡，可以使用 `-9` 参数确保它被杀死。另一个独立的命令 `killall` 可以根据名称杀死进程，因此在这种情况下，你可以如下杀死进程：

```
pi@erpi - $ pkill helloRPISleep
```

# 第 3 章 探索嵌入式 Linux 系统

## 99

值得提到的一个命令是 `watch`，它以固定的间隔执行命令并在终端上全屏显示结果。例如，要查看内核日志，可以使用以下命令：

```
pi@erpi - $ watch dmesg
```

你可以指定每次执行之间的时间间隔——使用 `-n` 后跟秒数。理解 `watch` 的一个好方法是如下执行它：

```
pi@erpi $ watch -n 1 ps a
Every 1.0s: ps a               Jun 20 20:22:39 2015

PID TTY STAT COMMAND

912 pts/0 a 0:06 -bash

31256 pts/0 S: 0:01 watch -n 1 ps a

31257 pts/0 S: 0:00 watch -n 1 ps a

31258 pts/0 R+ 0:00 sh -c ps a

31259 pts/0 R 0:00 ps a
```

你会看到 `ps`、`sh` 和 `watch` 的 PID 每（1）秒变化一次，这清楚地表明 `watch` 实际上是通过通过 `sh -c` 传递给新的 shell 来执行 `ps`。`watch` 在列表中出现两次是因为它在执行 `ps a` 的恰好时刻创建了自身。

### 其他 Linux 主题

在本书的这里，你已经涵盖了操作 Linux 的核心命令；然而，管理 Linux 系统方面还有很多内容要介绍。例如，如何配置 Wi-Fi 适配器？如何使用 `cron` 在 RPI 上调度任务？这些主题以及许多其他主题将在阅读本书的过程中详细介绍。例如，`cron` 任务将在第 12 章中结合物联网的背景进行介绍。

### 使用 Git 进行版本控制

简单来说，Git 是一个允许你跟踪软件项目在开发过程中内容变化的系统。Git 由 Linus Torvalds 设计，如今用于 Linux 内核的主线开发。Git 是一个极其有用的系统，原因有两个：你可以在开发软件时使用 Git，并且你可以了解如何与 Linux 内核发行版工作。

Git 是用于源码控制管理的分布式版本控制系统 `DVCS`。版本控制系统 `VCS` 用于跟踪并管理任何类型文档的更改。通常，修改过的文档会被标记修订号和时间戳。可以比较不同的版本，甚至恢复到文档的旧版本。版本控制系统有两种类型：

- 集中式 `CVS`：这些系统基于项目有一个唯一的“主”副本运行。工作流非常直观：你从中央服务器拉取更改，进行修改，然后提交回主副本。
- 分布式 `DVCS`：使用像 Git 和 Selenic Mercurial 这样的系统，你不需要拉取更改；而是克隆整个仓库，包括它的整个历史。仓库的克隆与主副本一样完整。

# 第一部分 | 树莓派基础

## 102

```
remote: Total 14 (delta 1), reused 0 (delta 0), pack-reused 9

Unpacking objects: 100% (14/14), done.

Checking connectivity... done.
```

你在 `/test` 目录下拥有一个 `/test/` 仓库的完整副本。你的仓库与 GitHub 服务器上的版本完全完备；如果你将其部署到网络、文件系统、其他 Git 服务器，甚至另一个 GitHub 账户上，它都可以作为该仓库的主版本来运行。虽然不需要中央服务器，但通常情况下是需要的，因为它允许多个用户将源代码“提交”到一个已的主仓库中。该仓库在 `/test` 目录中创建，目前包含以下内容：

```
$ cd /test && ls -al
total 20
drwxr-xr-x 3 pi 4096 Jun 20 22:00
drwxr-xr-x 6 pi 4096 Jun 20 22:00
drwxr-xr-x 8 pi 4096 Jun 20 22:00 .git
-rw-r--r-- 1 pi 59 Jun 20 README.md
```

你可以看到在 GitHub 上初始化项目时生成的 `README.md`；你可以使用 `more` 来查看此文件的内容。该目录还包含一个 `.git` 子目录，其中包含以下文件和目录：

```
$ cd /test/.git && ls
branches description hooks info objects refs
config HEAD index logs packed-refs
```

`.git` 文件夹包含了关于仓库的所有信息，如提交信息、日志和数据对象。例如，仓库的地址被维护在 `config` 文件中：

```
$ cd /test/.git && git config | grep url
url = https://github.com/derekmolloy/test.git
```

本章的“进一步阅读”部分将引导你查看一个关于 Git 的优秀示例，该示例在网上免费提供，详细描述了 `.git` 目录结构的本质。坦率地说，在接后的讨论中，你不需要更改 `.git` 目录结构，因为 Git 命令会为你完成这些工作。

> 注意此分步指南使用了 "test"；但是，你可以轻松地在 GitHub 上创建你自己的仓库。在 GitHub 上设置好免费账户后，前往 Create New（新建），然后点击 New repository（新仓库）。为你的仓库命名并添加描述，将其设置为公开，选择用 README 初始化，并点击 Create Repository（创建仓库）。然后你可以使用自己的账户遵循这些指令，结果是你将能够从 RPI 推送到你自己在 GitHub 上的仓库中。

# 第3章 探索嵌入式 Linux 系统

## 103

### 查看状态 `git status`

现在仓库已经存在，下一步是向工作目录添加一个新文本文件，它将处于“未跟踪”状态。当你调用 `git status` 命令时，你可以看到一条消息，显示存在“未跟踪的文件”：

```
pi@erpi ~/test $ echo "Just some text" > new.txt
pi@erpi ~/test $ git status
branch master
Your branch is up-to-date with 'origin/master'.
unracked files:
(use "git add <file>..." to include in what will be committed)
file.txt
nothing to commit, untracked files present (use "git add" to track)
```

下一步是将任何未跟踪的文件添加到暂存区 `staging area`。然而，如果你没有添加一组文件，你也可以创建一个 `.gitignore` 来忽略这些文件。例如，如果你正在构建 C/C++ 项目且不想添加中间过程产生的 `.o` 文件，这可能会非常有用。这里有一个创建一个 `.gitignore` 文件以忽略 C/C++ `.o` 文件的示例：

```
pi@erpi ~/test $ touch *.o > .gitignore
pi@erpi ~/test $ touch testobject.o
pi@erpi ~/test $ git status
branch master
Your branch is up-to-date with 'origin/master'.
unracked files:
(use "git add <file>..." to include in what will be committed)
.gitignore
file.txt
nothing to commit, untracked files present (use "git add" to track)
```

在这种情况下，有两个文件未被跟踪，但没有提到 `testobject.o` 文件，因为它被正确地忽略了。注意，`.gitignore` 本身是仓库的一部分，因此当仓库被克隆时，它会与它的修订历史等一起持久存在。

### 添加到暂存区 `git add`

通过输入 `git add .` 可以将工作目录中的文件添加到暂存区。该命令会将工作目录中的所有文件添加到其中，被忽略的文件除外。例如，有两个文件从工作目录添加到暂存区，可以使用以下命令显示仓库状态：

```
pi@erpi ~/test $ git add .
pi@erpi ~/test $ git status
```
