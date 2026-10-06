
你需要使用你创建 GitHub 账号时使用的邮箱地址。RStudio 的会话看起来应该是这样的：

![](img/276727cd0f1f6fea60002e6d839d370a_669_0.png)

我们首先进入“Global Options”（全局选项）并选择“Git/SVN”：

![](img/276727cd0f1f6fea60002e6d839d370a_669_1.png)

## 第 39 章：GIT 与 GITHUB

### 39 节：GITHUB 账户

你需要为刚刚安装的 Git 输入一个路径。

![](img/276727cd0f1f6fea60002e6d839d370a_670_0.png)

在 Windows 默认安装下，此路径为 `C:/Program Files/Git/bin/git.exe`，但你应该通过浏览系统来查找它，因为这会随系统而变化。为了避免每次访问仓库时都输入 GitHub 密码，我们将创建一个 SSH RSA 密钥。如果点击“Create RSA Key”按钮，RStudio 可以为我们完成这一操作：

![](img/276727cd0f1f6fea60002e6d839d370a_670_1.png)

你可以按照所示的默认指令操作：

![](img/276727cd0f1f6fea60002e6d839d370a_671_0.png)

![](img/276727cd0f1f6fea60002e6d839d370a_671_1.png)

![](img/276727cd0f1f6fea60002e6d839d370a_671_2.png)

现在 Git、RStudio 和 GitHub 应该可以连接了，我们准备好创建第一个 GitHub 仓库了。

### 39.3. GITHUB 仓库

你现在准备好创建一个 GitHub 仓库（repo）了。基本思想是你的代码至少会有两个副本：一份在你的电脑上，另一份在 GitHub 上。如果你为此项目添加了协作者，那么每个人的电脑上都会有一份。GitHub 上的副本通常被认为是每个协作者同步的主副本。Git 将帮助你保持所有副本的同步。

正如提到的，将代码保存在 GitHub 仓库的优点之一是你可以轻松地与感兴趣查看你作品示例的潜在雇主分享。由于许多数据科学公司使用 Git 等版本控制系统进行项目协作，他们可能会对你熟悉基础知识印象深刻。

为你的代码创建仓库的第一步是在 GitHub 上初始化。由于你已经创建了账户，你将在 GitHub 上拥有一个 URL 为 `http://github.com/username_` 的页面。

要创建一个仓库，请点击 `https://github.com` 上的“Sign In”按钮登录你的账户。你可能已经登录了，这种情况下“Sign In”按钮将不会显示：

![](img/276727cd0f1f6fea60002e6d839d370a_672_0.png)

登录时，你需要输入用户名和密码。我们建议设置浏览器记住这些信息，以免每次都输入。

进入账户后，你可以点击“Repositories”：

![](img/276727cd0f1f6fea60002e6d839d370a_673_1.png)

然后点击“New”创建一个新仓库：

![](img/276727cd0f1f6fea60002e6d839d370a_674_0.png)

你想要为项目选择一个良好的描述性名称。在将来，在选择名称时，你可能会有几十个仓库需要考虑。在这里我们将使用 `homework-0`。我们建议将仓库设为公开。如果你想将其私有，则需要支付月费。

![](img/276727cd0f1f6fea60002e6d839d370a_674_1.png)

现在你在 GitHub 上有了第一个仓库。下一步将是在你的电脑上克隆（`clone`）它，并开始使用 Git 进行编辑和同步。

为了做到这一点，方便复制 GitHub 提供的专门连接此仓库的链接，使用 Git 如下。我们稍后需要复制并粘贴它以确保记住这一步。

### 3.4 Git 概述

Git 中的主要操作有：
- 1. 从远程仓库拉取更改（`pull`），在这种情况下
- 2. 添加文件，或者用我们说的，暂存文件（`stage`）
- 3. 将更改提交（`commit`）到本地仓库
- 4. 将更改推送（`push`）到远程仓库

为了在 Git 中有效允许版本控制和协作，跨四个区域：工作目录（Working Directory）、暂存区（Staging Area）和本地仓库（Local Repository）（注：原文提到四个区域，但后续仅列出了三个）。

## 39.4. GIT 概述

然而，如果我们再次编辑该文件，它只会变化在工作目录中。要将更改添加到本地仓库中，我们需要暂存（`stage`）并提交（`commit`）已添加到本地仓库的更改：

```
echo "adding a line" >> new-file.txt

git add new-file.txt

git commit -m "adding a new line to new-file"

git status

# [master a82b893] adding a new line to new-file

# I file changed, 1 insertion(+)

# On branch master

# Your branch is ahead of 'origin/master' by 2 commits.

# (use "git push" to publish your local commits)

#

# Untracked files:

# (use "git add <file>" to include in what will be committed)

#

# tmp.txt

#

# nothing added to commit untracked files present (use "git add" to track)
```

请注意，在我们使用 Git 的时候，这一步通常是不必要的。如果我们直接在命令中添加文件名，就可以跳过暂存部分：

```
echo "adding a second line" >> new-file.txt

git commit -m "minor change to new-file" new-file.txt

git status

# [master 7765fce] minor change to new-file

# 1 file changed, 1 insertion(+)

# On branch master

# Your branch is ahead of 'origin/master' by 3 commits.

# (use "git push")
#
```
