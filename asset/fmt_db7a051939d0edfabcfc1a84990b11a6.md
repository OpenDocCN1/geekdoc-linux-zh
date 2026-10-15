
最流行的在线公共 git 仓库之一是 GitHub (https://github.com/)。这个网站是 git 的代名词，也是许多开源项目的默认选择。虽然这不是唯一的选择，但还有几个 git 仓库提供者可以选择。一些是免费的，另一些提供付费服务。

## 起始

在进行任何操作之前，你必须确保已经安装了 git 客户端。如果未安装客户端，你需要将其添加到本地系统中以便使用。

要检查是否安装了 git 客户端，请输入：`git --version`（如果返回类似“git version 2.x.x” 的结果，则说明已安装）。

注意：如果你没有 git，要安装它，请输入：`sudo apt-get install git` - OR - `sudo yum install git`

## 核心概念

我们已经涵盖了一些重要主题，例如：服务器和客户端在哪里。本节涉及其他重要的核心概念，例如：仓库、分支等。

### 仓库 (Repositories)

git 中的所有项目都存储在所谓的“仓库”中。仓库是存储构成项目的所有相关对象（如镜像、源代码等）的地方。你可以访问本地仓库或远程仓库。

本地仓库由 git 维护的三个“树”组成。这三棵树分别是工作目录 (`Working Directory`)、索引 (`Index`) 和 `Head`。下面是这些树的概述。

- **工作目录 (Working Directory)**：这是存储所有实际文件的地方。为了与现有仓库一起工作，你需要创建一个新仓库或将其克隆到本地计算机上。当你克隆一个现有的仓库时，它会创建一个由你控制的完整副本。

如果你想为自己创建一个新仓库，第一要工作是创建一个目录（例如 `mkdir directory_name`）来存放仓库。然后你需要切换到该位置（例如 `cd directory_name`），然后输入：`git init`（这将创建一个名为 `.git` 的新隐藏目录，用于存储配置文件）。要与远程仓库一起工作，你必须克隆它（基本上是创建它的本地副本）。输入：`git clone user_name@host:path/to/repository`。要对仓库的本地副本进行操作，输入：`git clone path/to/repository`。

- **索引 (Index)**：作为你对本地文件所做更改的暂存区。通常这些是你在测试代码时保存的更改。如果出现问题，你可以恢复到文件的之前的保存版本。

要将文件添加到索引中，你必须通过将它们添加到索引来“提议”更改，输入：`git add file_name` - OR - `git add *`

- **Head**：保存你对本地仓库文件中所做的提交(commit) 的最新版本。当你准备好提交所有放入索引的更改时，你必须将它们“提交”(commit) 到“head”。在提交到 head 之后，它们可以合并到远程系统上的主仓库。

要将提议的更改提交到 head，输入：`git commit -m "Commit message"`

注意：建议为每个软件版本创建标签 (`tags`)。例如，输入：`git tag v1.2.3 1a2b3c4d5e`（最后部分是提交 ID 的前 10 个字符，可以在日志中找到）。

通常情况下，一旦你完成了对本地仓库中文件的更改，你将希望将它们发送到主服务器，以便它们与其他更改合并。

为了实现这一点，你必须告诉 git 将存储在你本地系统“head”中的更改推送到存储在远程服务器上的主仓库，输入：`git push origin master`（将 `master` 改为任何你想要推送更改的分支。）

注意：如果你没有现有的克隆远程仓库，你必须与远程服务器建立连接，你需要添加一个。要添加远程仓库，输入：`git remote add origin server_address`

## 分支 (Branching)

git 的另一个核心概念是分支。当在你创建仓库时，`master` 分支被称为默认 (`DEFAULT`) 分支。分支允许用户创建特性的隔离副本并在本地进行开发，完成后完成后将其合并回 `master` 分支。

要创建一个名为 `new_feature` 的新分支并切换到该分支，输入：`git checkout -b new_feature`。要切换回 `master` 分支，输入：`git checkout master`

要删除已创建的分支，输入：`git branch -d new_feature`

注意：除非你将分支推送到远程主仓库，否则其他人无法使用该分支，输入：`git push origin new_feature`

## 仓库维护

一旦你的本地仓库与远程仓库不同步，你需要执行维护任务以确保所有内容都是最新的。

### 提交与合并 (Commits and Merges)

以下命令帮助你管理和合并：

- 使用最新提交更新你的本地仓库，输入：`git pull`
- 从远程获取更改：`git fetch`

### 日志 (Logging)

`git log` 命令向你显示提交和消息历史。日志对于查找提交期间发生了哪些更改非常有用。

要查看此命令的结果，输入：`git log`

### 恢复文件/仓库 (Reverting a File/Repository)

有时有必要将文件恢复或重置到提交之前的状态。这些命令帮助管理恢复：

- 将文件恢复到其在本地仓库中提交以来的状态，输入：`git checkout -- file_name`
- 将你的本地仓库副本重置（即删除所有更改）为来自主仓库的全新副本，输入：`git reset --hard origin/master`

## 实用小技巧 (Useful Tricks)

这些命令可以让 git 使用起来更简单或更有用：

- 显示彩色的 git 输出，输入：`git config color.ui true`
- 在日志中每个提交显示一行，输入：`git config format.pretty oneline`
- 将 git 置于交互模式（菜单选择），输入：`git add -i`

注意：更多信息：查看 Git 官方网站：https://git-scm.com/

## 备查表 (CheatSheet)

此 git 备查表包含某些 git 命令的摘要和示例。本节提供了如何创建、管理和删除仓库、分支和文件的快速参考，以及如何修改配置。

### 创建仓库 (Creating Repositories)

`git init [project_name]` 在现有目录中初始化 GIT。

### GIT 配置 (GIT Configuration)

`git config`: 为所有本地仓库配置用户信息。

- `--list`: 显示当前的 GIT 配置。
- `--global user.name = "[name]"` 设置提交时使用的用户名。
- `--global user.email = "[email address]"` 设置提交事务时使用的电子邮件地址。
- `--global color.ui auto`: 启用命令行输出的彩色显示。

### 克隆远程仓库 (Cloning a remote repository)

`git clone [path | URL]` 将远程仓库克隆（即复制或下载）到你的本地机器的目录中。

Ex: `git clone [https://URL_repo_to_clone]`

`git remote -v`

显示远程仓库的句柄。

`git remote show [ handle_name ]`

检查远程仓库的详细信息。

## 管理更改（提交/跟踪/推送）

`git add [ file_name | * ]`

将新文件或修改后的文件添加到仓库，以便在提交前进行暂存（stage）。

`git commit -m "message"`

提交所有已暂存的更改，并添加信息。

`git push origin master`

将所有提交的更改推送到 origin 的 master 分支。

`git reset [ file_name ]`

取消文件的暂存（unstage），并保留其内容。

`git checkout [ branch_name ]`

切换分支并更新工作目录。

## 获取/合并仓库

`git fetch origin`

使用新的副本重置（删除所有更改）你的整个仓库。

`git merge master`

从工作目录中获取并合并远程更改。

## 检查仓库状态

`git diff`

显示已修改但未暂存文件的差异（diff）。

`git diff --staged`

显示已暂存但未提交文件的差异。

`git status`

显示自上次提交以来，哪些文件被修改过或被暂存。

## 管理分支

`git branch`

显示当前仓库中所有本地分支的列表。

`git branch -d [ branch_name ]`

删除当前仓库中的一个分支。

`git branch [ branch_name ]`

在当前仓库中创建一个新分支。

`git checkout [ branch_name ]`

切换分支并更新工作目录。

`git merge [ branch_name ]`
