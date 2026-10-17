
```
matthew@semour:-$ bzr update
```

许多开源项目使用 Launchpad 托管其代码，本章稍后会更多介绍它，因为它是 Ubuntu 开发所在地。你可以在 http://launchpad.net 找到它。

# 使用 Git 管理软件项目

Linux 内核曾使用一个免费的版本控制服务托管，但它不是开源的。这通常是 Linux 社区内自由软件倡导者之间紧张的来源。然后，该服务宣布转向付费计划并给了他们过渡时间。由于这一决定，诞生了两个新的版本控制系统。Mercurial 是其中之一，Git 是另一个。Git 最初由内核内核开发人员 Linus Torvalds 本人编写（花费了两周），它胜出了。然而，更广泛的开源社区成为了最终赢家，因为诞生了两个有趣且实用的版本控制系统。

# 版本控制系统

Mercurial 由开发创建，目前仍由一名开发者领导：Matt Mackall。它使用分布式架构，并设计为快速，即使在处理大型代码库时也是如此。它的命令与 Subversion 相似，这使得过渡和初始使用非常简单。一个有趣的特性是 Mercur 是可扩展的；可以从项目的 wiki 安装扩展，或由用户编写以更改工作方式或添加功能，而无需更改原始代码。源代码控制通过命令行完成，如下例示例。你首先需要从 Ubuntu 软件仓库安装 Bazaar，在其中被称为 `bzr`。

要将新项目添加到仓库中，首先进入要放入仓库的顶层目录。然后，创建三个子目录：`branches`（分支）、`tags`（标签）和 `trunk`（主干）。将你的所有文件移动到 `trunk` 并输入以下命令：

```
matthew@seymour:-$ svn import project file:///your_svn_repo_name/your_project -m "First Import"
```

要从中央仓库检出代码，使用以下命令：

```
matthew@seymour:-$ svn checkout file:///your_svn_repo_name/your_project/trunk/your_project
```

在做出更改后检查代码，请使用 `-m` 标志添加注释，这是一个好主意，可以让其他人知道提交包含的内容：

```
matthew@seymour:-$ svn commit -m "This fixes bug 204982."
```

要从主仓库更新本地仓库中的源代码，以确保你拥有来自其他开发者代码的所有最新更改，请使用以下命令：

```
matthew@seymour:-$ svn update
```

要向仓库添加新文件，使用以下命令：

```
matthew@seymour:-$ svn add file_or_dir_name
```

要从仓库删除文件，使用以下命令：

```
matthew@seymour:-$ svn delete file_or_dir_name
```

许多使用 Subversion 的开源项目使用 SourceForge 托管其代码，它也支持 Git 和 Mercurial。在后续章节中讨论的其他代码托管站点，SourceForge 是寻找可能对你有用或你可能想要参与贡献的开源软件项目的好地方。你可以在 http://sourceforge.net 找到它。

# 使用 Bazaar 管理软件项目

Bazaar 由 Canonical 创建并于 2007 年首次发布，用于托管 Ubuntu 以及其他项目的开发文件。它被积极开发并广泛使用，不仅被 Canonical 和 Ubuntu 开发者，还被许多其他开源项目使用。本章稍后介绍的 Launchpad 使用了 Bazaar。

B 支持在有或没有中央仓库的情况下工作。，更改会在你检出的任何所有文件中进行跟踪，包括文件的多个版本。Bazaar 执行与 Subversion 类似的操作，但通常更容易使用。源代码控制通过命令行完成，如下例示例所示。你首先需要从 Ubuntu 软件仓库安装 Bazaar，在其中被称为 `bzr`。

![](img/d9236e4682dfcf03b759a19829a318ef_724_0.png)

创建新仓库有两种方法。如果你从空目录开始，请使用以下命令：

```
matthew@semour:-$ bzr init your_project_name
```

如果你在为现有项目创建一个仓库，进入该项目的顶层目录并输入以下命令：

```
matthew@semour:-$ bzr init
matthew@semour:-$ bzr add
```

要从现有仓库检出代码，使用以下命令：

```
matthew@semour:-$ bzr checkout your_project_name
```

在提交更改之前检查你的更改，可以使用 `bzr diff` 或 `bzr cdiff`。它们的作用相同，但 `bzr cdiff` 带有彩色的输出：

```
matthew@semour:-$ bzr cdiff
```

在做出更改后检查代码，使用 `-m` 标志添加注释，这是一个好主意，可以让其他人知道提交包含的内容：

```
matthew@semour:-$ bzr commit -m "This fixes bug 204982."
```

在 Bazaar 中，提交不会移除远程文件；它只将更改提交到你的本地副本。如果你想看到更改，必须将更改推送到它们：

```
matthew@semour:-$ bzr push sftp://path.to.main/repository
```

要从主仓库更新本地仓库中的代码，以确保你拥有来自其他开发者代码的所有最新更改，请使用以下命令：

```
matthew@semour:-$ bzr update
```

许多开源项目使用 Launchpad 托管其代码，本章稍后会更多介绍它，因为它是 Ubuntu 开发所在地。你可以在 http://launchpad.net 找到它。

# 使用 Mercurial 管理软件项目

Linux 内核曾使用一个免费的版本控制服务托管，但它不是开源的。这通常是 Linux 社区内自由软件倡导者之间紧张的来源。然后，该服务宣布转向付费计划并给了他们过渡时间。由于这一决定，诞生了两个新的版本控制系统。Mercurial 是其中之一，Git 是另一个。它们最初都是为了托管 Linux 内核代码而编写的。Git 最初由内核内核开发人员 Linus Torvalds 本人编写（花费了两周），它胜出了。然而，更广泛的开源社区成为了最终赢家，因为诞生了两个有趣且实用的版本控制系统。

# 版本控制系统

Mercurial 由开发创建，目前仍由一名开发者领导：Matt Mackall。它使用分布式架构，并设计为快速，即使在处理大型代码库时也是如此。它的命令与 Subversion 相似，这使得过渡和初始使用非常简单。一个有趣的特性是 Mercur 是可扩展的；可以从项目的 wiki 安装扩展，或由用户编写以更改工作方式或添加功能，而无需更改原始代码。源代码控制通过命令行完成，如下例示例。你首先需要从 Ubuntu 软件仓库安装 Bazaar，在其中被称为 `bzr`。

创建新仓库有两种方法。如果你从空目录开始，请使用以下命令：

```
matthew@semour:-$ bzr init your_project_name
```

如果你在为现有项目创建一个仓库，进入该项目的顶层目录并输入以下命令：

```
matthew@semour:-$ bzr init
matthew@semour:-$ bzr add
```

# 机会性开发导论

你有一个程序想法，将通过自动化重复性任务来节省时间。你计划让它有一个精美的 GUI，并且你认为可能还有其他人想在工具写好后使用它。问题是，你有全职工作，有家庭，并且已经有一堆关注度的的侧边项目。你要么能够，要么不愿意坐下来研究 Ubuntu 是如何打包程序的。

将它们提交到官方软件仓库。（如果需要，请查看“参考”部分中的链接）。

过去，在这个关头，你只有一个简单的选择：编写程序并将其放在网站上供其他人发现——并希望有人能发现它很有用，将其制作成 DEB 包，然后将其上传到 Debian 或 Ubuntu 仓库。如果你的目标是编写代码并让 Ubuntu 用户可以使用该软件，那么这不再是唯一的选择了。现在，你需要在技术上精通编写任何你想编写的代码，并且需要理解复杂的系统，但 Ubuntu 正在降低编写代码并将其提供给广泛社区的复杂性。这使得那些只想解决某个特定问题的开发者能够实现，而无需阅读大量关于他们预期很少使用或仅使用一次的工具文档。

## Launchpad

要开始使用，你需要在 Launchpad 上注册一个账户（见图 38.1）。Launchpad 是一个为了简化软件开发中的通信、协作和流程而创建的基础设施。它由 Canonical 开发并支持（Canonical 是支持 Ubuntu 社区的公司），但它被许多项目使用，包括一些不属于 Ubuntu 社区的项目。

![](img/d9236e4682dfcf03b759a19829a318ef_728_0.png)

最近的 Launchpad 博客文章
