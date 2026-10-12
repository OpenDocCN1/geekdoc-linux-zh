
# Linux：Linux 命令行，涵盖所有核心 Linux 命令：初学者指南

![](img/a1a9fab65c5fface16a7c7b64660708c_0_0.png)

# 关于作者

Ray Yao：

- Zend 认证 PHP 工程师（美国）
- Sun 认证 JAVA 程序员（美国）
- Oracle 认证 SCWCD 开发者（美国）
- CompTIA 认证 A+ 专业人士（美国）
- Microsoft 认证 ASP.NET 专家（美国）
- Microsoft 认证 MCP 专业人士（美国）
- Microsoft 认证 TECHNOLOGY 专家（美国）
- CompTIA 认证 NETWORK+ 专业人士（美国）

# 前言

本书是一本针对初者的指南，旨在快速学习 Linux 管理员或初学者常用的 Linux 命令。本书涵盖了所有核心 Linux 命令及其操作、示例和解释。它包含了 Linux 帮助命令、符号、快捷键、运行级别以及 Vi 命令。通过本书，你可以轻松学到：

- 如何运行所有核心 Linux 命令。
- 如何复制、移动和删除文件及目录。
- 如何创建、删除和管理用户及组。
- 如何访问 Linux 服务器并使用 `SSH` 命令。
- 如何操作和更改运行级别。
- 如何通过帮助命令在命令行中导航。
- 如何比较文件、查找文件、操作文件内容。
- 如何启动任务、停止任务和调度任务。
- 如何管理文件、目录的权限和所有权。
- 如何进行跨网络连接、与网络通信。
- 如何通过网络传输文件、发送网络消息。

以及更多技能……

书中包含一个包含所有常用 Linux 命令的长表格，这可以为你的工作或学习提供极大帮助。你可以快速学习所有核心 Linux 命令。

# 第 1 章

## Linux 简介

### 关于 Linux 操作系统

`Linux` 是一种类 `Unix` 且大部分符合 `POSIX` 标准的计算机操作系统，根据自由和开源软件开发与分发模型构建而成。

`Linux` 通常作为服务器运行，这是由于其稳定性和安全性特性。

`Linux` 程序具有极大的优势：

- `Linux` 程序是免费的，你会发现，大多数 `Linux` 程序都是免费的。
- 它们频繁更新且完全免费！其中一些甚至比 `Windows` 的更好。而另一些在 `Windows` 中根本不存在！

如果 `Linux` 是免费的且几乎所有软件都是免费的，是有原因的；要理解这一点，我们必须回到 1984 年。

### 1984

我们回到 1984 年，当时计算机科学并不发达。微软刚刚发布了第一个操作系统：`MS-DOS`，但这个系统距离完成还有远。

但是，那时 `MS-DOS` 是唯一的吗？

不是！还有其他的操作系统，但公众认知较低。

被称为最好的的是“`Unix`”。它比 `MS-DOS` 强大得多，但也复杂得多，这解释了为什么只有专业人士才能使用它。

在图形界面，`UNIX` 看起来很像 `MS-DOS`，它们看起来都像带有一些白字的黑屏幕。我们必须承认，当时的计算机无法做得更好。

## GNU 项目

正是在 1984 年，理查德·斯尔曼（`Richard Stallman`）创立了 `GNU` 项目。`GNU` 项目是一个自由软件的大规模协作项目，由理查德·斯尔曼于1983年9月27日在麻省理工学院（`MIT`）宣布。它的目标是通过协作开发和提供基于以下自由权的软件，赋予计算机用户在使用计算机和计算设备时的自由和控制权：用户可以自由地运行软件、共享（复制、分发）、学习和修改它。`GNU` 软件通过法律保证这些自由权利（通过其许可证），因此是自由软件；“`free`”（免费）一词的使用始终指的是自由（`freedom`）。

理查德·斯尔曼是 `MIT` 的一个人工智能领域的研究员。他想创建一个基于 `UNIX` 的操作系统（命令仍然相同）。

但他为什么要创建一个“`UNIX`”的副本呢？因为 `UNIX` 不是免费的，而且正变得越来越昂贵！理查德·斯尔曼想通过创建一个免费的替代品来回应：`GNU` 诞生了。

### GNU 是一个开放的操作系统

`GNU` 不仅仅是一个免费的操作系统；它还必须是“开放”的。区别在哪里？

自由程序是指你可以拥有源代码的程序，也就是说拥有“批量配方”。相比之下，`Windows` 是一个专有操作系统，其源代码由微软存储。想象它就像可口可乐：没有人知道配方（虽然有很多人尝试模仿它，但嘿……）。所以我们无法更改它，无法查看其内部是如何运作的。

开放程序大部分是自由程序，它也是一种有权复制、修改、重新分发的程序。这是计算机科学中一种真正的思想：人们认为提供我们创建的程序的源代码是更好的，因为它允许知识共享并帮助计算机更快地进化。自由世界的口号可能是：“团结就是力量。”

### Linus Torvalds 正在做他的爱好

1991 年，林纳斯·托瓦尔斯（`Linus Torvalds`）这位芬赫尔辛基大学的学生开始创建一个他自己的免费操作系统。这个系统被称为 `Linux`，指的是其创作者的名字（`Linux` 是 `Linus` 和 `UNIX` 的缩写）。

### Linux 创始人 Linus Torvalds

他与 `GNU` 是什么关系？事实证明，这两个项目是互补的：理查德·斯托曼（`Richard Stallman`）创建了基础程序（文件复制、删除、文件管理、文本编辑器），而 `Linus` 则投入了操作系统“心脏”——内核的创建。

`GNU`（免费程序）和 `Linux`（操作系统内核）合并创建了 `GNU / Linux`。

从理论上讲，我们应该称为 `GNU / Linux`。但这写起来和读起来有点困难，而且由于语言的习惯，我们经常直接称之为“`Linux`”。这就是为什么我在书的其余部分继续称之为“`Linux`”，尽管政治正确的名称是“`GNU / Linux`”，因为它是两个互补项目的结合。

## 原始操作系统

你现在应该对现存三大主流操作系统：`Mac OS`、`Linux` 和 `Windows` 的起源有了更好的了解了。

因此，`Mac OS` 和 `Linux` 都是基于 `UNIX`（操作系统的祖先），而 `Windows` 从 `MS-DOS` 属于一个独立分支。总的来说，你你只需要记住这些。

人们说 `Mac OS` 和 `Linux` 基于 `UNIX`，是因为它们“复制”了它的运行机制。这并不是贬义，恰恰相反：对 `UNIX` 来说这是一种荣誉。

`Linux` 程序并没有使用与 `UNIX` 完全相同的源代码（`UNIX` 是所有者，所以是私有的）。它们被完全重写了，但工作方式相同。

如果我告诉你这一切，是因为我相信了解 `Linux` 的起源是非常重要的。这将帮助你理解之后的很多内容。

## Linux 发行版

`Linux` 发行版（通常简称为 `distro`）是一个基于 `Linux` 内核并通常围绕软件包管理系统构建软件集合而成的操作系统。最著名的发行版有 `RedHat`（红帽）、`SUSE`、`Debian`、`Mandriva`、`Slackware` 和 `Ubuntu`。你可以发现许多截然不同的软件，并且有数百种不同的安装方法。

为了让用户生活得更方便并让他们能够选择，人们创建了不同的 `Linux` 发行版。这个概念在 `Windows` 中并不真正存在。这就像 `Windows 7` 家庭版和 `Windows 7` 专业版的区别，但程度要深得多。

以下是不同发行版之间可能不同的地方：

- 安装：可以从非常复杂简化到非常简单；
- 安装管理程序：如果做得良好且集中化，它可以让新软件的安装比 `Windows` 更简单，后文会详细讨论！
- 计算机上预装的程序（例如 `Windows` 捆绑了 `Internet Explorer` 和 `Windows Media Player`）。

事实上，发行版在某种程度上是对 `Linux` 的封装。内核本身对于所有发行版来说都是相同的。

无论你安装哪种发行版，你得到的都是与其他兼容的 `Linux`。某些发行版只是更容易或更难处理。:-)

### 各种现有发行版

有很多不同的 `Linux` 发行版。你会说很难选择：确实，第一次并不清楚选什么……尤其是它们都是免费的！别担心，我会帮你做选择。

我不会列出所有的发行版，但这里至少有主要的：

- `Slackware`：最老的 `Linux` 发行版之一。它今天仍然存在！
- `Mandriva`：由一家法国公司发布，使用简单；
- `RedHat`：由一家美国公司发布，该发行版闻广泛，特别是在服务器上；
- `SUSE`：由 `Novell` 公司发布；
- `Debian`：`Debian`发行行由独立开发者而非商业公司管理。这是最流行的发行版之一。

正如我所说的，无论你选择哪种 `distro`（`distribution` 的缩写），你都会得到 `Linux`。基本上，首次启动时“仅仅”有一个屏幕和各种预装的软件（我这简化了很多，但核心意思如此）。

## 总结

`Windows`、`Mac OS` 和 `Linux` 是最流行的操作系统。

`Linux` 通常因为其稳定性和安全特性作为服务器运行。

`Linux` 的特点是免费，也就是说它的源代码（制造配方）是开源的：任何人都可以查看。相比之下，设计 `Windows` 和 `Mac OS` 的源代码是关闭的；我们称这些为专用操作系统。

`Linux` 有许多变体，被称为发行版。

# 第二章

## 输入第一个命令

亲爱的朋友们，大日子终于来了！你将有机会在控制台输入你的第一个命令了！



好，压力太大吧？

亲爱的朋友们，大日子终于来了！你将有机会在控制台输入你的第一个命令了！

---

为了让用户生活得更方便并让他们能够选择，人们创建了不同的 Linux 发行版。这个概念在 Windows 中并不真正存在。这就像 `Windows 7` 家庭版和 `Windows 7` 专业版的区别，但程度要深得多。

以下是不同发行版之间可能不同的地方：

- 安装：可以从非常复杂简化到非常简单；
- 安装管理程序：如果做得良好且集中化，它可以让新软件的安装变得比 `Windows` 更简单，后文会详细讨论！
- 计算机上预装的程序（例如 `Windows` 捆绑了 `Internet Explorer` 和 `Windows Media Player`）。

事实上，发行版在某种程度上是对 `Linux` 的封装。内核本身对于所有发行版来说都是相同的。

无论你安装哪种发行版，你得到的都是与其他兼容的 `Linux`。某些发行版只是更容易或更难处理。:-)

以 `root` 为伪名进行连接。`root` 是主用户，有权对他的计算机用户执行任何操作（甚至可以破坏它！）。我们稍后会详细查看 `root`；但目前我们仍处于受限用户账户中，因此不会有做坏事的风险。

“欢迎，你是 `user-linux` 机器上的超级用户。你目前处于家目录中，并拥有超级用户权限。你正在使用命令`whoami`显示当前用户名。”

## 关于`user>pwd`

示例：

`user> pwd`

解释：

- `user> ` 是一个自定义的命令提示符。
- `pwd` 是一个命令，意思是打印工作目录（`print working directory`）。

你可以像 `user>` 那样自定义命令提示符。当然，在你熟悉了基本的 `Linux` 命令（以及 `Linux` 的几乎所有内容）之后，命令提示符是完全可配置的。如果你觉得它太长，可以缩短它；如果提供的信息不够，可以加长它。从理论上讲，你可以在提示符中放入任何想要的内容，例如当前时间。

通过输入命令在控制台中工作，由于命令数量繁多，你永远无法知道所有的命令……这并不是目标：目标是让你烂记那些最“常用”的命令，而对于不常用的命令，你能够通过阅读它们的手册学会如何使用。

## 关于 `Linux` 命令

命令的典型语法看起来如下：

```
command --option argument
```

或者

```
command parameter
```

让我们来看一些命令和参数的示例：

### 示例：

输入`date`并按回车键。

```
user2014 @ user-linux: ~ date
```

2010年9月20日，星期一，下午3:39:51 (`UTC-0200`)

## 解释：

第一行包含命令提示符，后面跟着我输入的命令。在这里，`date` 是一个命令。

第二行是计算机对该命令的响应：我们询问了日期和时间！

## 关于参数

参数是写在命令后面的选项。

命令和参数之间用空格分隔，如下：

```
user2014 @ user-linux: ~ $ command parameters
```

参数本身可以包含空格、字母、数字……真的包含了各种内容。关于设置方法没有真正的规则，但幸运的是程序员们采用了某种“约定”，以便我们识别不同类型的参数。

### 短参数（单字母）

最常用的参数是由一个连字符开头的单个字母组成的。

例如：

- `-d`
- `-l`
- `-a`

如果我们需要给出几个参数，可以这样做：

```
-d -a -U -h
```

或者更短的：

```
-daUh
```

注意！对于短参数：不同命令中的相同参数含义不同。

### 示例：

```
ls -t (-t意味着“按时间戳列出”）
eject -t (-t意味着“关闭托盘”）
nchfn -f (-f意味着“通过指纹名称更改信息”）
cut -f (-f意味着“按字段编号切割文本”）
nps -f (-f意味着“以完整信息显示进程状态”）
```

注意！参数对大小写敏感（大写/小写）。如果你写 `-u`，它的含义通常与 `-U` 不同。对 `Ls` 命令进行测试，并写参数 `-a`（小写），`-a` 意味着“所有”：

### 示例：

```
user2014@user-linux: ~ $ ls -a
.gconf .mozilla-thunderbird .gimp-2.2 .nautilus
.bash_history .gksu.lock .profile .bash_logout .gnome
.recently-used .bashrc .gnome2 .recently-used.xbel .config
.gnome2_private .ssh Desktop .gstreamer-
.sudo_as_admin_successful .dmrc .gtkrc 0.10-1.2-gnome2
.themes .esd_auth .ICEAuthority .thumbnails .evolution
.icons .Trash Examples .lesshst tutorials .face .local .update-
manager-core.fontconfig.macromedia.update-notifier.gaim.metacity.Xauthority.gconf.mozilla.xsession-errors
```

显示当前目录下的所有文件，即使是隐藏文件。“cookie”是以点开头的 `Linux` 文件。通常情况下，如果你在家目录中，你应该会有很多隐藏文件。这些通常是配置文件。

### 长参数（多个字母）

参数由两个连字符开头的多个字母组成，如下：

```
--long
```

例如：

```
--all
```

`--all` 是一个长参数，意味着所有内容或所有事物。

例如：

```
--version
```

`--version` 是一个长参数，意味着命令的版本。

例如：

```
--help
```

`--help` 是一个长参数，意味着当前命令的帮助。

如果你想在每个参数之间放置多个参数：人们也可以结合长短参数。控制参数有两种可能的输入方式：短版本和长版本。注意，该命令接受你偏好的任何一种。让我们在 `ls` 命令上测试一下 `--all`，它意味着“一切”：

### 示例：

```
user2014@user-linux: ~ ls --all
.gconf .mozilla-thunderbird .gimp-2.2 .nautilus .bash_history .gksu.lock .profile .bash_logout .gnome .recently-used .bashrc .gnome2 .recently-used.xbel .config
```

---

以 `root` 为伪名进行连接。`root` 是主用户，有权对他的计算机用户执行任何操作（甚至可以破坏它！）。我们稍后会详细查看 `root`；但目前我们仍处于受限用户账户中，因此不会有做坏事的风险。

“欢迎，你是 `user-linux` 机器上的超级用户。你目前处于家目录中，并拥有超级用户权限。你正在使用命令`whoami`显示当前用户名。”

## 关于`user>pwd`

示例：

`user> pwd`

解释：

- `user> ` 是一个自定义的命令提示符。
- `pwd` 是一个命令，意思是打印工作目录。

你可以像 `user>` 那样自定义命令提示符。当然，在你熟悉了基础的 `Linux` 命令（以及 `Linux` 的几乎所有内容）之后，命令提示符是完全可配置的。如果你觉得它太长，可以缩短它；如果提供的信息不够，可以加长它。从理论上讲，你可以在提示符中放入任何想要的内容，例如当前时间。

通过输入命令在控制台中工作，由于命令数量繁多，你永远无法知道所有的命令……这并不是目标：目标是让你烂记那些最“常用”的命令，而对于不常用的命令，你能够通过阅读它们的手册学会如何使用。

## 关于 `Linux` 命令

命令的典型语法看起来如下：

```
command --option argument
```

或者

```
command parameter
```

让我们来看一些命令和参数的示例：

### 示例：

输入`date`并按回车键。

```
user2014 @ user-linux: ~ date
```

2010年9月20日，星期一，下午3:39:51 (`UTC-0200`)

## 解释：



# 命令与参数基础

## 命令结构

第一行包含命令提示符，后面跟着我输入的命令。在这里，`date`是一个命令。

第二行是计算机对该命令的响应：我们询问了日期和时间！

## 关于参数

参数是写在命令后面的选项。

命令和参数之间用空格分隔，如下：

```
user2014 @ user-linux: ~ $ command parameters
```

参数本身可以包含空格、字母、数字……真的包含了各种内容。关于设置方法没有真正的规则，但幸运的是程序员们采用了某种“约定”，以便我们识别不同类型的参数。

### 短参数（单字母）

最常用的参数是由一个连字符开头的单个字母组成的。

例如：

- `-d`
- `-l`
- `-a`

如果我们需要给出几个参数，可以这样做：

```
-d -a -U -h
```

或者更短的：

```
-daUh
```

**注意**：对于短参数：不同命令中的相同参数含义不同。

### 示例

```
ls -t (-t意味着“按时间戳列出”)
eject -t (-t意味着“关闭托盘”)
nchfn -f (-f意味着“通过指纹名称更改信息”)
cut -f (-f意味着“按字段编号切割文本”)
nps -f (-f意味着“以完整信息显示进程状态”)
```

**注意**：参数对大小写敏感（大写/小写）。如果你写`-u`，它的含义通常与`-U`不同。对`Ls`命令进行测试，并写参数`-a`（小写），`-a`意味着“所有”：

### 示例

```
user2014@user-linux: ~ $ ls -a
.gconf .mozilla-thunderbird .gimp-2.2 .nautilus
.bash_history .gksu.lock .profile .bash_logout .gnome
.recently-used .bashrc .gnome2 .recently-used.xbel .config
.gnome2_private .ssh Desktop .gstreamer-
.sudo_as_admin_successful .dmrc .gtkrc 0.10-1.2-gnome2
.themes .esd_auth .ICEAuthority .thumbnails .evolution
.icons .Trash Examples .lesshst tutorials .face .local .update-
manager-core.fontconfig.macromedia.update-notifier.gaim.metacity.Xauthority.gconf.mozilla.xsession-errors
```

显示当前目录下的所有文件，即使是隐藏文件。“cookie”是以点开头的 Linux 文件。通常情况下，如果你在家目录中，你应该会有很多隐藏文件。这些通常是配置文件。

### 长参数（多个字母）

参数由两个连字符开头的多个字母组成，如下：

```
--long
```

例如：

```
--all
```

`--all`是一个长参数，意味着所有内容或所有事物。

例如：

```
--version
```

`--version`是一个长参数，意味着命令的版本。

例如：

```
--help
```

`--help`是一个长参数，意味着当前命令的帮助。

如果你想在每个参数之间放置多个参数：人们也可以结合长短参数。控制参数有两种可能的输入方式：短版本和长版本。注意，该命令接受你偏好的任何一种。让我们在`ls`命令上测试一下`--all`，它意味着“一切”：

### 示例

```
user2014@user-linux: ~ ls --all
.gconf .mozilla-thunderbird .gimp-2.2 .nautilus .bash_history .gksu.lock .profile .bash_logout .gnome .recently-used .bashrc .gnome2 .recently-used.xbel .config
```

# 用户账户与提示符

## 关于 root 用户

以`root`为伪名进行连接。`root`是主用户，有权对他的计算机用户执行任何操作（甚至可以破坏它！）。我们稍后会详细查看`root`；但目前我们仍处于受限用户账户中，因此不会有做坏事的风险。

“欢迎，你是`user-linux`机器上的超级用户。你目前处于家目录中，并拥有超级用户权限。你正在使用命令`whoami`显示当前用户名。”

## 关于 user>pwd

示例：

`user> pwd`

解释：

`user>`: 是一个自定义的命令提示符。

`pwd`: `pwd`是一个命令，意思是打印工作目录。

你可以像`user>`那样自定义命令提示符。当然，在你熟悉了基础的 Linux 命令（以及 Linux 的几乎所有内容）之后，命令提示符是完全可配置的。如果你觉得它太长，可以缩短它；如果提供的信息不够，可以加长它。从理论上讲，你可以在提示符中放入任何想要的内容，例如当前时间。

通过输入命令在控制台中工作，由于命令数量繁多，你永远无法知道所有的命令……这并不是目标：目标是让你烂记那些最“常用”的命令，而对于不常用的命令，你能够通过阅读它们的手册学会如何使用。

## 关于 Linux 命令

命令的典型语法看起来如下：

```
command --option argument
```

或者

```
command parameter
```

让我们来看一些命令和参数的示例：

### 示例

输入`date`并按回车键。

```
user2014 @ user-linux: ~ date
2010年9月20日，星期一，下午3:39:51 (UTC-0200)
```

解释：

第一行包含命令提示符，后面跟着我输入的命令。在这里，`date`是一个命令。

第二行是计算机对该命令的响应：我们询问了日期和时间！



以`root`为伪名进行连接。`root`是主用户，有权对他的计算机用户执行任何操作（甚至可以破坏它！）。我们稍后会详细查看`root`；但目前我们仍处于受限用户账户中，因此不会有做坏事的风险。

“欢迎，你是`user-linux`机器上的超级用户。你目前处于家目录中，并拥有超级用户权限。你正在使用命令`whoami`显示当前用户名。”

## 关于`user>pwd`

示例：

```
user> pwd
```

解释：

- `user> :`是一个自定义的命令提示符。
- `pwd:`：`pwd`是一个命令，意思是打印工作目录。

你可以像`user>`那样自定义命令提示符。当然，在你熟悉了基础的Linux命令（以及Linux的几乎所有内容）之后，命令提示符是完全可配置的。如果你觉得它太长，可以缩短它；如果提供的信息不够，可以加长它。从理论上讲，你可以在提示符中放入任何想要的内容，例如当前时间。

通过输入命令在控制台中工作，由于命令数量繁多，你永远无法知道所有的命令……这并不是目标：目标是让你烂记那些最“常用”的命令，而对于不常用的命令，你能够通过阅读它们的手册学会如何使用。

## 关于Linux命令

命令的典型语法看起来如下：

```
command --option argument
```

或者

```
command parameter
```

让我们来看一些命令和参数的示例：

### 示例

输入`date`并按回车键。

```
user2014 @ user-linux: ~ date
```

2010年9月20日，星期一，下午3:39:51 (UTC-0200)

### 解释

第一行包含命令提示符，后面跟着我输入的命令。在这里，`date`是一个命令。

第二行是计算机对该命令的响应：我们询问了日期和时间！

## 关于参数

参数是写在命令后面的选项。

命令和参数之间用空格分隔，如下：

```
user2014 @ user-linux: ~ $ command parameters
```

参数本身可以包含空格、字母、数字……真的包含了各种内容。关于设置方法没有真正的规则，但幸运的是程序员们采用了某种“约定”，以便我们识别不同类型的参数。

### 短参数（单字母）

最常用的参数是由一个连字符开头的单个字母组成的。

例如：

- `-d`
- `-l`
- `-a`

如果我们需要给出几个参数，可以这样做：

```
-d -a -U -h
```

或者更短的：

```
-daUh
```

注意！对于短参数：不同命令中的相同参数含义不同。

### 示例

```
ls -t (-t意味着“按时间戳列出”）
eject -t (-t意味着“关闭托盘”）
nchfn -f (-f意味着“通过指纹名称更改信息”）
cut -f (-f意味着“按字段编号切割文本”）
nps -f (-f意味着“以完整信息显示进程状态”）
```

注意！参数对大小写敏感（大写/小写）。如果你写`-u`，它的含义通常与`-U`不同。对`ls`命令进行测试，并写参数`"-a"`（小写），`-a`意味着“所有”：

### 示例

```
user2014@user-linux: ~ $ ls -a
```

```
.gconf .mozilla-thunderbird .gimp-2.2 .nautilus
.bash_history .gksu.lock .profile .bash_logout .gnome
.recently-used .bashrc .gnome2 .recently-used.xbel .config
.gnome2_private .ssh Desktop .gstreamer-
.sudo_as_admin_successful .dmrc .gtkrc 0.10-1.2-gnome2
.themes .esd_auth .ICEAuthority .thumbnails .evolution
.icons .Trash Examples .lesshst tutorials .face .local .update-
manager-core.fontconfig.macromedia.update-notifier.gaim.metacity.Xauthority.gconf.mozilla.xsession-errors
```

显示当前目录下的所有文件，即使是隐藏文件。“cookie”是以点开头的Linux文件。通常情况下，如果你在家目录中，你应该会有很多隐藏文件。这些通常是配置文件。

### 长参数（多个字母）

参数由两个连字符开头的多个字母组成，如下：

```
--long
```

例如：

```
--all
```

`--all`是一个长参数，意味着所有内容或所有事物。

例如：

```
--version
```

`--version`是一个长参数，意味着命令的版本。

例如：

```
--help
```

`--help`是一个长参数，意味着当前命令的帮助。

如果你想在每个参数之间放置多个参数：人们也可以结合长短参数。控制参数有两种可能的输入方式：短版本和长版本。注意，该命令接受你偏好的任何一种。让我们在`ls`命令上测试一下`--all`，它意味着“一切”：

### 示例

```
user2014@user-linux: ~ ls --all
```

```
.gconf .mozilla-thunderbird .gimp-2.2 .nautilus .bash_history .gksu.lock .profile .bash_logout .gnome .recently-used .bashrc .gnome2 .recently-used.xbel .config
```



参数本身可以包含空格、字母、数字……真的包含了各种内容。关于设置方法没有真正的规则，但幸运的是程序员们采用了某种“约定”，以便我们识别不同类型的参数。

### 短参数（单字母）

最常用的参数是由一个连字符开头的单个字母组成的。

例如：

- `-d`
- `-l`
- `-a`

如果我们需要给出几个参数，可以这样做：

```
-d -a -U -h
```

或者更短的：

```
-daUh
```

注意！对于短参数：不同命令中的相同参数含义不同。

### 示例：

```
ls -t (-t意味着“按时间戳列出”）
eject -t (-t意味着“关闭托盘”）
nchfn -f (-f意味着“通过指纹名称更改信息”）
cut -f (-f意味着“按字段编号切割文本”）
nps -f (-f意味着“以完整信息显示进程状态”）
```

注意！参数对大小写敏感（大写/小写）。如果你写 `-u`，它的含义通常与 `-U` 不同。对 `Ls` 命令进行测试，并写参数 `"-a"`（小写），`-a` 意味着“所有”：

### 示例：

```
user2014@user-linux: ~ ~ ls -a.
.gconf .mozilla-thunderbird .gimp-2.2 .nautilus
.bash_history .gksu.lock .profile .bash_logout .gnome
.recently-used .bashrc .gnome2 .recently-used.xbel .config
.gnome2_private .ssh Desktop .gstreamer-
.sudo_as_admin_successful .dmrc .gtkrc 0.10-1.2-gnome2
.themes .esd_auth .ICEAuthority .thumbnails .evolution
.icons .Trash Examples .lesshst tutorials .face .local .update-
manager-core.fontconfig.macromedia.update-notifier.gaim.metacity.Xauthority.gconf.mozilla.xsession-errors 显示当前目录下的所有文件，即使是隐藏文件。“cookie”是以点开头的 Linux 文件。通常情况下，如果你在家目录中，你应该会有很多隐藏文件。这些通常是配置文件。
```

### 长参数（多个字母）

参数由两个连字符开头的多个字母组成，如下：

```
--long
```

例如：

```
--all
```
`--all` 是一个长参数，意味着所有内容或所有事物。

例如：

```
--version
```
`--version` 是一个长参数，意味着命令的版本。

例如：

```
--help
```
`--help` 是一个长参数，意味着当前命令的帮助。

如果你想在每个参数之间放置多个参数：人们也可以结合长短参数。控制参数有两种可能的输入方式：短版本和长版本。注意，该命令接受你偏好的任何一种。让我们在 `ls` 命令上测试一下 `--all`，它意味着“一切”：

### 示例：

```
user2014@user-linux: ~ ls --all

.gconf .mozilla-thunderbird .gimp-2.2 .nautilus .bash_history .gksu.lock .profile .bash_logout .gnome .recently-used .bashrc .gnome2 .recently-used.xbel .config
```

(login: 显示登录名，输出为“root”。)

注意：以超级用户身份登录后，`$` 会变为 `#`。

## `exit`: 退出 `shell`

示例：

```
root@user-linux:~# exit
```

(`exit`: 退出 `shell`。在这里：退出超级用户模式，进入普通用户模式。)

注意：退出超级用户模式后，`#` 将变为 `$`。

## `whoami`: 显示当前用户名

示例：

```
user2014@user-linux: ~ $ whoami
```

(`whoami`: 显示当前用户名，输出为“`user2014`”)

## `hostname`: 显示当前主机名

示例：

```
user2014@user-linux: ~ $ hostname
```

(`hostname`: 显示当前主机名，输出为“`user-linux`”）

## `sudo`: 允许具有权限的用户以另一个用户（如超级用户）的身份执行命令

### 示例：

```
root> sudo -u andy /home/mydir
```

(以用户 `andy` 的身份列出 `/home/mydir` 目录的内容

`-u`: 指定指定用户)

```
root> sudo -v
```

(`-v`: 刷新身份验证超时，下次 `sudo` 命令将不再需要密码。)

```
root> sudo -k
```

(`-k`: 使身份验证超时过期，下次 `sudo` 命令将需要密码。)

## 总结：

`su`: 将普通用户切换为 `root` 超级用户

`loginname`: 显示登录名

`exit`: 退出 `shell`

`whoami`: 显示当前用户名

`hostname`: 显示当前主机名

`sudo`: 允许具有适当权限的用户以另一个用户（如超级用户）的身份执行命令

# 第 4 章

At 命令导航

`pwd`: 打印工作目录。

`cd dir`: 切换目录。

`cd ~` 切换目录到主目录。

`cd ..` 切换目录到父目录。

`type`: 确定命令类型。

`pwd`: 打印工作目录。

示例：

```
user> pwd
```

(`pwd`: 打印工作目录，输出为你当前的工作目录。)

`cd dir`: 切换目录

示例：

```
user> cd mydir
```

(`cd`: 切换目录到 `mydir`，输出为 `mydir`。)

`cd ~` 切换目录到主目录。

示例：

```
user> cd ~
```

(`cd ~` 切换目录到主目录，输出为主目录。)

`cd ..` 切换目录到父目录。

示例：

```
user> cd ..
```

(`cd ..` 切换目录到父目录，输出为父目录。)

`type`: 确定命令类型

示例：

```
user> type pwd
```

(输出: `pwd` 是一个 `shell` 内置命令。)

## 总结：

- `pwd`: 打印工作目录。
- `cd`: 切换目录。
- `cd ~` 切换目录到主目录。
- `cd ..` 切换目录到父目录。
- `type`: 确定命令类型。

# 第 5 章

文件操作命令

- `cp`: 复制文件
- `mv`: 移动文件
- `mv`: 重命名文件
- `rm`: 删除文件
- `rm -ri`: 删除非空目录
- `vi`: 打开 `vi` 编辑器并编辑文件
- `find`: 查找文件
- `wc`: 显示文件的字数
- `file`: 估算文件类型
- `ln`: 在两个文件之间创建链接
- `ln -s`: 为文件创建符号链接
- `readlink`: 显示符号链接的目标
- `lpr`: 将文件发送到打印机
- `lpq`: 显示打印队列。

## `cp`: 复制文件

示例：

```
user> cp myfile /dir1
```

(`cp`: 将 `myfile` 复制到 `/dir1` 目录。)

## `mv`: 移动文件

示例：

```
user> mv myfile /dir2
```

(`mv`: 将 `myfile` 移动到 `dir2` 目录。)

## `mv`: 重命名文件

示例：

```
user> mv myfile1 myfile2
```

(`mv`: 将 `myfile1` 重命名为 `myfile2`。)

## `rm`: 删除文件

示例：

```
user> rm myfile
```

(`rm`: 删除 `myfile`。)

## `rm -ri`: 删除非空目录

### 示例：

```
user> rm -ri NonEmptyDir
```

(`rm`: 删除名为 `NonEmptyDir` 的目录。

`-ri`: 删除包含内容的目录。)

## `vi`: 打开 `vi` 编辑器并编辑文件

### 示例：

```
user> vi myfile.txt
```

(`vi`: 打开 `vi` 编辑器并编辑 `myfile.txt`。)

## `find`: 查找文件

### 示例：

```
user> find directory -type f -name myfile.txt -print
```

(`find`: 查找文件。

`-type f`: 指定为文件

`-name`: 指定文件名

`-print`: 输出)

## `wc`: 显示文件的字数

### 示例：

```
user> wc myfile.txt
```

(`wc`: 显示 `myfile.txt` 的字数)

`file`: 估算文件类型

示例：

```
user> file myfile.txt
```

(`file`: 估算 `myfile.txt` 的类型)

`ln`: 为文件创建链接

示例：

```
user> ln dir1/file1.txt dir2/file2.txt
```



# 第 5 章

## 符号链接与文件操作

`ln`: 在`file1`和`file2`之间创建链接

`ln -s`: 在两个文件之间创建符号链接

### 示例：

```
user> ln -s dir1/file1.txt dir2/file2.txt
```

`ln -s`: 在`file1`和`file2`之间创建符号链接

`-s`: 符号链接允许给定文件同时出现在多个位置或多个名称下。例如，符号链接可以链接到目录。

`readlink`: 显示符号链接的目标

### 示例：

```
user> readlink dir2/file2.txt
```

输出: `dir1/file1.txt`

`lpr`: 将文件发送到打印机

### 示例：

```
user> lpr myfile.txt
```

已将`myfile.txt`发送到打印机。

`lpq`: 显示打印队列。

### 示例：

```
user> lpq
```

显示当前打印队列状态。

## 总结

`su`: 将普通用户切换为`root`超级用户

`loginname`: 显示登录名

`exit`: 退出`shell`

`whoami`: 显示当前用户名

`hostname`: 显示当前主机名

`sudo`: 允许具有适当权限的用户以另一个用户（如超级用户）的身份执行命令

# 第 6 章

## 查看文件命令

`cat`: 查看文件内容

`less`: 分页查看文件

`tail`: 查看文件末尾

`head`: 查看文件开头

### 示例：

```
user> cat myfile.txt
```

`cat`: 显示`myfile.txt`内容。

### 示例：

```
user> less myfile.txt
```

`less`: 分页查看`myfile.txt`。

### 示例：

```
user> tail myfile.txt
```

`tail`: 查看`myfile.txt`的最后`10`行。

### 示例：

```
user> head myfile.txt
```

`head`: 查看`myfile.txt`的前`10`行。

`cp`: 复制文件

`mv`: 移动文件

`mv`: 重命名文件

`rm`: 删除文件

`rm -ri`: 删除非空目录

`vi`: 打开编辑器并编辑文件

`find`: 查找文件

`wc`: 显示文件的字数

`file`: 估算文件类型

`ln`: 在文件之间创建链接

`ln -s`: 为文件创建符号链接

`readlink`: 显示符号链接的目标

`lpr`: 将文件发送到打印机

`lpq`: 显示打印队列。

### 示例：

```
root> vi myfile.txt
```

`vi`: 使用`vi`编辑打开`myfile.txt`

`tr`: 转换文件文本

### 示例：

```
root> echo apple | tr "apple" "banana"
```

输出: `banana`

## `tee`: 将标准输出写入文件

### 示例：

```
Root> sort file1.txt | tee file2.txt
```

排序`file1.txt`并写入`file2.txt`

## 总结

- `cat`: 显示文件内容
- `cat | less`: 分页显示文件内容
- `cat | more`: 逐屏显示文件内容
- `head`: 显示文件的头部内容
- `tail`: 显示文件的尾内容
- `aspell`: 对文件进行拼写检查
- `cut`: 显示文本文件的指定列
- `paste`: 合并两个文件的内容并显示
- `sort`: 按字母顺序显示文本行
- `stat`: 显示文件或目录的属性
- `wc`: 显示文件的单词数
- `file`: 测试文件类型
- `touch`: 创建文件或更改文件时间戳
- `l`: 显示文件每行的行号
- `vi`: 使用`vi`编辑器或创建文本文件
- `tr`: 转换文件文本
- `tee`: 将标准输出写入文件

# 第 7 章

## 比较文件命令

`diff`: 显示两个文件之间的差异

`cmp`: 按字节比较两个文件

`comm`: 按行比较两个文件

`md5sum`: 创建`md5`校验和数字

`cksum`: 创建`crc`校验码

### `diff`: 显示两个文件之间的差异

#### 示例：

```
user> diff myfile1.txt myfile2.txt
```

`diff`: 显示两个文件之间的差异。

### `cmp`: 按字节比较两个文件

#### 示例：

```
user> cmp myfile1.txt myfile2.txt
```

`cmp`: 按字节比较两个文件。

### `comm`: 按行比较两个文件

#### 示例：

```
user> comm myfile1.txt myfile2.txt
```

`comm`: 按行比较两个文件。

### `md5sum`: 创建 md5 校验和数字

#### 示例：

```
user> md5sum myfile1.txt
```

输出: `f7tkgu5orj1jf8kelc2os95nd57jf8r myfile1.txt`

### `cksum`: 创建 crc 校验码

#### 示例：

```
user> chsum myfile2.txt
```

输出: `4658791048 19 myfile2.txt`

## 总结

- `diff`: 显示两个文件之间的差异
- `cmp`: 按字节比较两个文件
- `comm`: 按行比较两个文件
- `md5sum`: 创建`md5`校验和数字
- `cksum`: 创建`crc`校验码

# 第 8 章

## 文本匹配命令

`grep`: 显示所有包含指定字符串的行

`egrep`: 显示所有包含指定字符串的行

`uniq`: 显示文件中唯一的行

`find`: 在指定目录中查找文件

`look`: 显示匹配给定前缀的单词

### `grep`: 显示所有包含指定字符串的行

#### 示例：

```
user> grep good myfile.txt
```

`grep`: 显示所有包含“`good`”字符串的行。

### `egrep`: 显示所有包含指定字符串的行

#### 示例：

```
user> egrep excellent myfile.txt
```

`egrep`: 显示所有包含“`excellent`”字符串的行。

### `uniq`: 显示文件中唯一的行

#### 示例：

```
user> uniq myfile.txt
```

`uniq`: 显示`myfile.txt`中唯一的行。

### `find`: 在指定目录中查找文件

#### 示例：

```
user> find /mydir --type f myfile.txt -print
```

`find`: 在目录中查找文件。
`-type f`: 指定文件
`-print`: 打印

### `look`: 显示匹配给定前缀的单词

#### 示例：

```
User> look ab
```

输出: `aba, abb, abc, abd...`

## 总结

- `grep`: 显示所有包含指定字符串的行
- `egrep`: 显示所有包含指定字符串的行
- `uniq`: 显示文件中唯一的行
- `find`: 在指定目录中查找文件
- `look`: 显示匹配给定前缀的单词

# 第 9 章

## 目录命令

- `mkdir`: 创建新目录
- `rmdir`: 删除空目录
- `basename`: 显示文件路径的最后部分
- `dirname`: 只显示目录路径

### `mkdir`: 创建新目录

#### 示例：

```
user> mkdir mydir
```

`mkdir`: 创建新目录

### `rmdir`: 删除空目录

#### 示例：



```
user> rmdir mydir
(rmdir: 删除一个空目录)
```

## basename: 显示文件路径的最后部分

示例：

```
user> basename /home/foo/usr/file.txt
(输出: file.txt)
```

## dirname: 只显示目录路径

示例：

```
User>dirname /foo/bar/baz/myfile.txt
(输出: /foo/bar/baz)
```

## 总结

*   `mkdir`: 创建新目录
*   `rmdir`: 删除空目录
*   `basename`: 显示文件路径的最后部分
*   `dirname`: 只显示目录路径

# 第 10 章

压缩命令

*   `zip`: 压缩文件
*   `unzip`: 解压文件
*   `gzip`: 压缩文件
*   `gunzip`: 解压文件
*   `bzip2`: 压缩文件
*   `bunzip2`: 解压文件

### `zip`: 压缩文件

示例：

```
user> zip myfile.txt
(zip: 压缩文件)
```

### `unzip`: 解压文件

示例：

```
user> unzip myfile.zip
(unzip: 解压文件)
```

### `gzip`: 压缩文件

示例：

```
user> gzip myfile.txt
(gzip: 压缩文件)
```

### `gunzip`: 解压文件

示例：

```
user> gunzip myfile.txt.gz
(gunzip: 解压文件)
```

### `bzip2`: 压缩文件

示例：

```
user> bzip2 myfile.txt
(bzip2: 压缩文件)
```

### `bunzip2`: 解压文件

示例：

```
user> bunzip2 myfile.txt.bz2
(bunzip2: 解压文件)
```

## 总结

*   `zip`: 压缩文件
*   `unzip`: 解压文件
*   `gzip`: 压缩文件
*   `gunzip`: 解压文件
*   `bzip2`: 压缩文件
*   `bunzip2`: 解压文件

# 第 11 章

进程命令

*   `ps`: 显示当前进程
*   `kill`: 按 ID 杀死进程
*   `w`: 显示所有进程
*   `df`: 显示文件系统磁盘空间
*   `uptime`: 显示运行时间
*   `top`: 查看活动进程

### `ps`: 显示当前进程

示例：

```
root> ps -u username
(ps: 显示用户的进程.)
```

### `kill`: 按 ID 杀死进程

示例：

```
root> kill 6270
(kill: 杀死进程 6270)
```

### `w`: 显示所有进程

示例：

```
root> w -s
(w: 显示所有进程.)
```

### `df`: 显示文件系统磁盘空间

示例：

```
root> df -h
(df: 显示文件系统磁盘空间.)
```

### `uptime`: 显示运行时间

示例：

```
root> uptime
(uptime: 显示运行时间.)
```

### `top`: 查看活动进程

示例：

```
root> top -p pid
(top: 按 PID 查看进程)
```

## 总结

*   `ps`: 显示当前进程
*   `kill`: 按 ID 杀死进程
*   `w`: 显示所有进程
*   `df`: 显示文件系统磁盘空间
*   `uptime`: 显示运行时间
*   `top`: 查看活动进程

# 第 12 章

账户命令

*   `useradd`: 创建新账户
*   `usermod`: 修改现有账户
*   `userdel`: 删除现有账户
*   `passwd`: 设置账户密码
*   `chfn`: 修改用户详细信息
*   `finger`: 显示用户详细信息

### `useradd`: 创建新账户

示例：

```
root> useradd username
(useradd: 创建新账户.)
```

### `usermod`: 修改现有账户

示例：

```
root> usermod -l oldname newname
(usermod: 修改现有账户.)
```

### `userdel`: 删除现有账户

示例：

```
root> userdel username
(userdel: 删除现有账户.)
```

### `passwd`: 设置账户密码

示例：

```
root> passwd username
(passwd: 为用户设置账户密码.)
```

### `chfn`: 修改用户详细信息

示例：

```
root> chfn username
(chfn: 为用户修改详细信息.)
```

### `finger`: 显示用户详细信息

示例：

```
root> finger username
(finger: 列出用户的登录名、电子邮件、域名、时间.)
```

## 总结

*   `useradd`: 创建新账户
*   `usermod`: 修改现有账户
*   `userdel`: 删除现有账户
*   `passwd`: 设置账户密码
*   `chfn`: 修改用户详细信息
*   `finger`: 显示用户详细信息

# 第 13 章

组相关命令

*   `groups`: 显示组成员关系
*   `groupadd`: 创建新组
*   `groupmod`: 修改现有组
*   `groupdel`: 删除现有组

### `groups`: 显示组成员关系

示例：

```
root> groups username
(groups: 显示用户所属的组信息。)
```

### `groupadd`: 创建新组

示例：

```
root> groupadd newgroup
(groupadd: 创建一个名为 newgroup 的新组。)
```

### `groupmod`: 修改现有组

示例：

```
root> groupmod newgroup
(groupmod: 修改一个名为 newgroup 的现有组。)
```

### `groupdel`: 删除现有组

示例：

```
root> groupdel newgroup
(groupdel: 删除一个名为 newgroup 的现有组。)
```

## 总结

*   `groups`: 显示组成员关系
*   `groupadd`: 创建新组
*   `groupmod`: 修改现有组
*   `groupdel`: 删除现有组

# 第 14 章

权限命令

*   `chmod`: 修改访问权限模式
*   `chgrp`: 修改组成员关系
*   `chown`: 更改文件或目录的所有者

（访问权限详情将在稍后章节介绍。）

### `chmod`: 修改访问权限模式

示例：

```
root> chmod 752 myfile1.txt
(chmod: 修改 myfile1.txt 的访问权限)
```

*   `7`: 设置用户的读、写、执行权限。
*   `5`: 设置组的读、执行权限。
*   `2`: 设置其他用户的仅写权限。

### `chmod`: 修改访问权限模式

示例：

```
root> chmod g+w myfile.txt
(g+w: 为文件所属组的成员赋予写权限)
```

### `chgrp`: 修改组成员关系

示例：

```
root> chgrp username myfile2.txt
(chgrp: 修改 myfile2.txt 的组成员关系)
```

### `chown`: 更改文件或目录的所有者

示例：

```
root> chown username myfile3.txt
(chown: 修改 myfile3 的所有者)
```

示例：

```
root> chown groupname /user/dir
(chown: 修改 dir 的所有者。)
```

## 总结

*   `chmod`: 修改访问权限模式
*   `chgrp`: 修改组成员关系
*   `chown`: 更改文件或目录的所有者

（访问权限详情将在稍后章节介绍。）

# 第 15 章

作业运行命令

*   `job`: 显示所有作业的状态
*   `fg`: 在前台运行暂停的任务
*   `bg`: 在后台运行暂停的任务
*   `kill`: 通过编号杀死作业或通过 `pid` 杀死进程
*   `at`: 在指定时间调度作业
*   `atq`: 显示已计划的作业
*   `atrm`: 删除已计划的任务
*   `ps`: 显示当前进程状态
*   `w`: 显示谁登录以及正在做什么
*   `uptime`: 显示系统运行时间
*   `top`: 查看最活跃的或指定的进程
*   `crontab`: 创建在指定时间运行的作业

### `job`: 显示所有作业的状态

示例：

```
root> jobs
```

(`job`: 显示所有作业的状态。)

### `fg`: 在前台运行暂停的任务

示例：

```
root> fg %2
```

(`fg %2`: 在前台运行作业 `%2`。)

### `bg`: 在后台运行暂停的任务

示例：

```
root> bg %3
```

(`bg %3`: 在后台运行作业 `%3`。)

### `kill`: 通过编号杀死作业或通过 `pid` 杀死进程

示例：

```
root> kill %4
```

(`kill %4`: 杀死正在运行的作业 `%4`)

### `at`: 在指定时间调度作业

示例：

```
root> at 9:30 pm
```

(`at 9:30`: 在 `9:30` 调度一个计划作业。)

### `atq`: 显示已计划的作业

示例：

```
root> atq
atq: 显示所有计划的作业)
```

### `atrm`: 删除已计划的任务

示例：



## 第 18 章：系统管理命令

### atrm: 删除已计划的任务

示例：

```
root> atrm 25
```

(`atrm 25`: 删除编号为 25 的计划作业。)

### ps: 显示当前进程状态

示例：

```
root> ps -f
```

(`ps -f`: 显示当前进程的完整信息。)

示例：

```
root> ps -u username
```

(`ps -u`: 显示用户当前的进程。)

### w: 显示谁登录以及正在做什么

示例：

```
root> w -s username
```

(`-s`: 显示用户的摘要信息。)

### uptime: 显示系统运行时间

示例：

```
root> uptime
```

(`uptime`: 显示系统已运行时间。)

### top: 查看最活跃的或指定的进程

示例：

```
root> top
```

(`top`: 显示系统上运行的所有进程)

### crontab: 创建在指定时间运行的作业

示例：

```
root> crontab -e
```

(`-e`: 编辑 `crontab` 文件，在表中添加一个 `crontab` 作业)

### 总结

- `job`: 显示所有作业的状态
- `fg`: 在前台运行暂停的任务
- `bg`: 在后台运行暂停的任务
- `kill`: 通过编号杀死作业或通过 `pid` 杀死进程
- `at`: 在指定时间调度作业
- `atq`: 显示已计划的作业
- `atrm`: 删除已计划的任务
- `ps`: 显示当前进程状态
- `w`: 显示谁登录以及正在做什么
- `uptime`: 显示系统运行时间
- `top`: 查看最活跃的进程
- `crontab`: 创建在指定时间运行的作业

### 示例：网络诊断命令

#### nslookup

> > `root> nslookup myexample.com`

(返回 `IP` 地址，例如 `75.126.166.2XX`)

(`nslookup`: 手动查询 `DNS` 服务器。)

(`DNS`（域名系统）协议允许你从名称服务器获取给定主机名的 `IP` 地址。此过程被称为域名解析。)

### 总结

- `host`: 显示远程主机名和 `IP` 地址
- `ifconfig`: 显示本地网络配置
- `ping`: 发送数据包以测试远程主机是否可达
- `ssh`: 安全地连接到远程计算机
- `ftp`: 通过“文件传输协议”传输文件
- `mesg`: 启用或禁用消息传递功能
- `write`: 向其他用户写入消息
- `open`: 连接到 `ftp` 服务器
- `mail`: 在本地和范围内发送及接收邮件。

# 第 19 章：脚本命令

### echo: 显示文本

`echo`: 显示文本。

示例：

```
root> STR="Hello World!"
root> echo $STR
```

(`echo`: 显示文本。输出是 “Hello World!”)

### echo -e: 使用转义序列显示文本

示例：

```
root> STR="Hello World!"
root> echo -e "\n$STR\n"
```

(`echo -e`: 使用 `\n` 显示文本。 `\n` 意味着换行。)

输出是：

Hello World!

### expr: 执行数学计算

示例：

```
user> expr 20 + 80
```

(输出是 “100”)

示例：

```
user> expr 21/7
```

(输出是 “3”)

示例：

```
user> expr 9 ">" 6
```

(输出是 “1”， 1 表示真)

示例：

```
user> expr 9 "<" 6
```

(输出是 "0"，0 表示假)

### #!/bin/bash: 放在 bash shell 脚本的第一行

示例：

```bash
#!/bin/bash
if...then...else...fi
```

(`#!/bin/bash`: 始终放在 `bash` shell 脚本的第一行)

### 总结

- `echo`: 显示文本。
- `expr`: 执行数学计算。
- `#!/bin/bash`: 始终放在 `bash` shell 脚本的第一行

# 第 20 章：系统命令

### df: 显示文件系统的磁盘占用

`df`: 显示文件系统的磁盘占用

示例：

```
root> df -h
```

(`df`: 显示文件系统的磁盘占用)
(`-h`: 使输出易于理解)

### mount: 使设备对文件系统可用

示例：

```
root> mount /cdrom
```

(`mount`: 使 `cd-rom` 对文件系统可用。)

### umount: 使设备对文件系统失效

示例：

```
root> umount /dev/hda1
```

(`umount`: 使 `hda1` 对文件系统失效)
(`hda1`: 一个硬盘分区)

### fsck: 检查并修复文件系统

示例：

```
root> fsck
```

(`fsck`: 检查并修复文件系统。)

### init n: 将系统切换到运行级别 n

示例：

```
root@user-linux: ~ # init 5
```

(`init 5`: 将系统切换到运行级别 5)

### who -r: 显示当前运行级别

示例：

```
root@user-linux: ~ # who -r
```

(`who -r`: 显示当前运行级别。)

### free: 显示空闲内存

示例：

```
root@user-linux: ~ # free -m
```

(`free`: 显示空闲内存)
(`-m`: 以 `MB` 为单位显示空闲内存)

### du: 显示文件或目录的磁盘占用

示例：

```
root@user-linux: ~ # du -b myfile.txt
```

(`du`: 显示文件或目录的磁盘占用。)
(`-b`: 统计其占用的字节数。)

### export: 设置环境变量

示例：

```
root@user-linux: ~ # export newvar=8
```

(`echo $newvar`. 输出是 8)

### printenv: 列出环境变量的名称和值

示例：

```
root@user-linux: ~ # printenv
```

(`printenv`: 列出环境变量的名称和值)

### unset: 移除环境变量

示例：

```
root@user-linux: ~ # unset var
```

(`unset var`: 移除环境变量 `var`。)

### clear: 清除屏幕

示例：

```
user>clear
```

(`clear`: 清除屏幕。)

### exit: 退出 shell 或注销。

示例：

```
user>exit
```

(`exit`: 退出 `shell` 或注销。)

### shutdown -h +n: 系统将在 n 分后关闭！

示例：

```
root@user-linux: ~ # shutdown -h +5
```

(`shutdown -h +5`: 系统将在 5 分后关闭!)
(`-h`: 停止系统)
(`+n`: 在 `n` 秒后)

### 总结

- `df`: 显示文件系统的磁盘占用
- `mount`: 使设备对文件系统可用
- `umount`: 使设备对文件系统失效
- `fsck`: 检查并修复文件系统
- `init n`: 将系统切换到运行级别 `n`
- `who -r`: 显示当前运行级别
- `free`: 显示空闲内存
- `du`: 显示文件或目录的磁盘占用
- `export`: 设置环境变量
- `printenv`: 列出环境变量的名称和值
- `unset`: 移除环境变量
- `clear`: 清除屏幕
- `exit`: 退出 `shell` 或注销。
- `shutdown -h +n`: 系统将在 `n` 分后关闭！

# 第 21 章：帮助命令

| 命令 | 操作 |
| :--- | :--- |
| `man` | 显示命令的手手册 |
| `info` | 显示命令的信息 |
| `whatis` | 显示命令的描述 |
| `help` | 显示命令的帮助 |
| `apropos` | 在帮助页中搜索关键词 |
| `help` | 在帮助页中搜索关键词 |
| `wget` | 在帮助页中搜索关键词 |
| `help` | 在帮助页中搜索关键词 |
| `help` | 在帮助页中搜索关键词 |
| `help` | 在帮助页中搜索关键词 |
| `help` | 在帮助页中搜索关键词 |
| `help` | 在帮助页中搜索关键词 |

# 第 22 章：命令技巧

### 利用 Tab 键自动补全

示例：



如果你想输入 `date` 命令但不确定拼写，你只需要在终端中输入 `da` 并按两次 `Tab` 键。命令就会补全。

如果你想输入 `chsh` 命令但不确定拼写，你只需要在终端中输入 `ch` 并按两次 `Tab` 键。命令就会神奇地补全。它会显示 `chfn, chsh`，然后你可以选择 `chfn`。

逗也可以！

## 命令历史

我们经常需要找到几分钟前甚至几秒钟前输入的命令。有时是因为我们忘记了命令，但通常是因为你真的懒得重写整个命令。

这个快捷键是黄金：按下向上方向键；你会看到最后输入的命令。

如果你再次按下方向键，你会看到倒数一个命令，然后是第二个，等等。

如果你按下向下方向键，你会返回到最近的命令。

因此，我可以倒序找到我刚刚输入的命令：

* `--all;`
* `-a,`
* `Is;`
* `Date;`
* 等。

如果你想在命令历史中回溯得很远，不需要像疯子一样按上百次方向键。

有一个 `history` 命令可以提醒你命令历史：

示例：

按下向上方向键；你会看到最后输入的命令。然后屏幕会显示：

`Date 152 Is Is Is 153 154 155--all -a 156 157 history`

终端，那三个 `Is` 是第 `153`、`154` 和 `156` 条命令。当然，你上面输入的命令始终会存在于历史记录中。

### Ctrl + R：查找历史命令

如果方向键 Top（上方向）和 `history` 命令不足以找到你输入过的旧命令，有一个超级实用的快捷键：`Ctrl+R`。它可以帮助你找到刚刚使用的历史命令。只需同时按下 `Ctrl+R` 键，计算机将切换到“查找已输入的命令”（`R`）的搜索模式。

在此时，你可以输入与某个旧命令对应的任意字母序列。

示例：

如果你想查找以前使用过的包含 `all` 的命令，请按 `Ctrl+R` 并输入 `all`。然后，`Linux` 将找到包含单词 `all` 的 `ls --all` 命令。你只需按回车即可运行该命令 :-)

如果这不是你要找的命令，再次按 `Ctrl + R` 向上移动包含 `all` 的命令列表。在这样的驱动器上这样做可能看起来很愚蠢，但有些命令非常长，

不需要重新重写它们真是一件乐事！

## 使用通配符

你可以在很多 `Linux` 命令中使用通配符。通配符是表示其他字符的符号或符号组合。`Linux` 命令中有三种通配符：

* 星号 (`*`) 表示任何字符或字符集，包括零个字符或多个字符。
* 问号 (`?`) 表示单个字符。
* 例如：`b??k` 匹配 `bank, beak, back, bilk` 或任何其他以 `b` 开头并 `k` 结尾的四字母文件名。
* 例如：`b*k` 匹配 `bk, bkk, bark, backtrack`。
* 方括号 (`[]`) 包围的字符通常表示集合中的任何字符。但请注意，它们是区分大小写的大小。
* 例如：`b[a-z]k` 匹配 `bak, bkk, bck, bzk`，但不匹配 `Ak, bBk, bCk, bZk`，因为它们区分大小写。

通配符实际上是在 `Linux` 命令中具体实现的。

### 示例：

```
user2014@user-linux:~$ ls b??k
```

（通配符 `b??k` 匹配当前目录下的五个文件。）

输出为 “`bank beak back bilk bark`”

### 示例：

```
user2014@user-linux:~$ ls a*d
```

（通配符 `a*d` 匹配当前目录下的某些文件。）

输出为 “`ad add acid abroad abounded abed aid`”

### 示例：

```
user2014@user-linux:~$ ls se[a-e]
```

（通配符 `se[a-e]` 匹配当前目录下的五个文件。）

输出为 “`sea seb sec sed see`”

## 关于运行级别 (Run Levels)

什么是运行级别？运行级别术语是指实现 `Linux System V` 风格初始化的一种操作系统运行模式。通常存在七个运行级别，编号从 `0` 到 `6`；启动时仅执行一个“运行级别”——运行级别不是按顺序执行的，即执行运行级别 `2`、`3` 或者 `4`，而不是先执行 `2` 再执行 `3` 最后执行 `4`。

“运行级别”定义了机器启动后的状态。

不同的运行级别通常分配给：

* `0`. `halt-the-system` 正在关机过程中。
* `1`. 单用户模式
* `2`. 未启动网络服务的多用户模式
* `3`. 启动了网络服务的多用户模式
* `4`. 系统关机
* `5`. 系统重启

### 示例：

```
root@user-linux: ~ # init 3
```

(`init 3`：将系统切换到运行级别 `3`)

## 总结：

* `Tab` 键可以自动补全缺失的命令。
* 上箭头可以查看历史命令。
* 下箭头可以返回最最近的命令。
* `Ctrl+R` 可以通过关键词查找历史命令。
* `?` 问号 (`?`) 表示单个字符。
* 星号 (`*`) 表示任何字符或字符集，包括零个字符或多个字符。
* 方括号 (`[]`) 包围的字符通常表示集合中的任何字符。但请注意，它们是区分大小写的。

运行级别数字描述了已初始化并正在运行的服务级别。

# 第 23 章

访问权限

## 什么是 rwx？

在使用 `ls -l` 查看文件的访问权限后，你可以看到类似所示的内容：

```
rwx ...... ......
```

解释：

`rwx` 表示访问权限，可以用 `1` 到 `7` 的数字来描述。真的吗？是的，`1` 到 `7` 的数字表示访问权限。

* `r` 代表读取权限，值为 `4`。
* `w` 代表写入权限，值为 `2`。
* `x` 代表执行权限，值为 `1`。

反之亦：

* `4` 代表读取权限 (`r`)
* `2` 代表写入权限 (`w`)
* `1` 代表执行权限 (`x`)

### 示例：

如果 `rwx` 值为 `4`，那么你就可以推出它的权限是只读的。

如果 `rwx` 值为 `2`，那么你就可以推出它的权限是只写的。

如果 `rwx` 值为 `1`，那么你就可以推出它的权限是只执行的。

`1` 到 `7` 的数字表示各种访问权限：

* `7` 表示读取、写入、执行权限 (`7=4+2+1`)
* `6` 表示读取、写入权限 (`6=4+2`)
* `5` 表示读取、执行权限 (`5=4+1`)
* `4` 表示只读权限 (`4=4+0`)
* `3` 表示写入、执行权限 (`3=2+1`)
* `2` 表示只写权限 (`2=2+0`)
* `1` 表示只执行权限 (`1=1+0`)

### 示例：

如果 `rwx` 值为 `7`，那么你就可以推出它的权限是读取、写入和执行。

如果 `rwx` 值为 `6`，那么你就可以推出它的权限是读取和写入。

如果 `rwx` 值为 `3`，那么你就可以推出它的权限是写入和执行。

## 什么是 rwx rwx rwx？

文件的访问权限分为三个：

* 用户权限
* 组权限
* 其他权限

所以，当你使用 `ls -l` 查看访问权限时，你会发现三个 `rwx` 如下所示：

```
rwx rwx rwx......
```

解释：

* 第一个表示用户权限
* 第二个表示组权限
* 第三个表示其他权限

### 示例：

* 第一个是 `7`，表示用户具有读取、写入、执行权限。
* 第二个是 `5`，表示组具有读取、执行权限。
* 第三个是 `3`，表示其他用户具有写入、执行权限。
* 第一个是 `6`，表示用户具有读取和写入权限。
* 第二个是 `4`，表示组具有只读权限。
* 第三个是 `2`，表示其他用户具有只写权限。
* 第一个是 `4`，表示用户具有只读权限。
* 第二个是 `2`，表示组具有只写权限。
* 第三个是 `1`，表示其他用户具有只执行权限。
* 第一个是 `3`，表示用户具有写入、执行权限。
* 第二个是 `1`，表示组具有只执行权限。
* 第三个是 `0`，表示其他用户没有权限。
* 第一个是 `2`，表示用户具有只写权限。
* 第二个是 `0`，表示组没有权限。
* 第一个是 `1`，表示用户具有只执行权限。

| 符号 | 含义 | 示例 |
| :--- | :--- | :--- |
| `..` | 上级目录 | `e.g. cd..` |
| `~` | 用户主目录 | `e.g. cd~` |
| `$` | 变量名和值的变量前缀 | `e.g. echo $var` |
| `$$` | 显示运行的进程数 | `e.g. echo $$` |
| `!!` | 重复上一条命令 | `e.g. !!` |
| `!string` | 运行以字符串开头的最近命令 | `e.g. Icat` |

# 第 25 章

快捷键

| 快捷键 | 说明 |
| :--- | :--- |
| `CTRL+B` | 光标仅向后移动一个字符。 |
| `CTRL+C` | 取消正在运行的命令或杀死运行的进程。 |
| `CTRL+D` | 退出当前会话。类似于 `exit` 命令。 |
| `CTRL+F` | 光标仅向前移动一个字符。 |
| `CTRL+H` | 向后删除一个字符。类似于按下退格键。 |
| `CTRL+P` | 将上一行（或行）粘贴到指定的某个位置。 |
| `CTRL+R` | 输入以调出最近的命令，返回历史命令列表 |
| `CTRL+S` | 停止屏幕上的所有输出。通过锁定终端输出来冻结 `shell`。 |
| `CTRL+Q` | 恢复屏幕上所有已停止的输出，继续终端输出。 |



`CTRL+U`：删除光标所在的整行。

`CTRL+W`：删除你刚刚输入的最后一个单词。

`CTRL+Z`：挂起正在运行的进程。如果想恢复，使用`fg`或`bg`命令。

## 第26 章

运行级别表

| 运行级别 | 描述 |
| :--- | :--- |
| 0 | 停止系统。当当前运行级别为 0 时，系统正处于关闭过程中。 |
| 1 | 单用户模式。仅运行一小部分内核进程。几乎所有其他服务都已禁用。 |
| 2 | 基本多用户模式。此运行级别启动大多数服务，但未启用网络连接服务。 |
| 3 | 全多用户模式。此运行级别启动所有服务，包括网络连接。但不启动 X 窗口 |
| 4 | 用户自定义模式。运行级别 4 无常规定义。它完全开放给用户配置。 |
| 5 | 带有 X 窗口的全多用户模式。启动所有启用的服务以及 Linux 图形桌面环境。 |
| 6 | 重启。当当前运行级别为 6 时，系统正处于重启过程中。 |

## 第27 章

Vi 编辑器命令

| 命令 | 操作 |
| :--- | :--- |
| `h,l,k,j` | 光标左、右、上、下移动 |
| `w,b` | 光标向前、向后移动 |
| `0` | 跳到行首 |
| `$` | 跳到行尾 |
| `G` | 跳到文件的最后一行 |
| `J` | 将当前行与下一行合并 |
| `z` | 撤销上一个命令 |
| `.` | 重复上一个命令 |
| `ZZ` | 保存文件并退出 |
| `i` | 在光标字符前插入 |
| `I` | 在行首插入字符 |
| `a` | 在光标字符后追加 |
| `A` | 在行尾追加字符 |
| `c` | 修改到...为止 |
| `C` | 修改到行尾 |
| `d` | 删除到...为止 |
| `D` | 删除到行尾 |
| `r` | 替换一个字符 |
| `R` | 替换多个字符 |
| `o` | 在下方开启新行 |
| `O` | 在上方开启新行 |
| `esc` | 退出插入模式，进入命令模式 |
| `x` | 删除光标所在处的字符 |
| `X` | 删除左侧的字符 |
| `u` | 撤销上一次修改 |
| `.` | 重做上一次修改 |
| `U` | 恢复行 |
| `m` | 标记位置 |
| `M` | 屏幕中间 |
| `dw` | 删除当前单词 |
| `dd` | 删除当前行 |
| `cc` | 修改当前行 |
| `fx` | 在当前行查找 `x` |
| `F x` | 在上一行查找 `x` |
| `/string` | 搜索字符串，向后查找 |
| `?string` | 搜索字符串，向后查找 |
| `[n]G` | 跳到第 “n” 行 |
| `n` | 向后搜索下一个 |
| `N` | 向后搜索下一个 |
| `p` | 将行粘贴到当前行下方 |
| `P` | 将行粘贴到当前行上方 |
| `t` | 直到... |
| `T` | 向后退到... |
| `s` | 替换 |
| `S` | 替换整行 |
| `ZZ` | 写入并退出 |
| `:e` | 编辑文件 |
| `:e!` | 放弃对文件的修改 |
| `$%` | 跳到文件最后一行 |
| `:number` | 跳到指定行号 |
| `:w` | 写入并保存 |
| `:w!` | 强制保存只读文件 |
| `:w filename` | 使用新文件名保存 |
| `:wq` | 写入、保存并退出 |
| `:n` | 跳到下一个文件 |
| `:rew` | 跳到第一个文件 |
| `:q` | 使用 `:w` 保存后退出 |
| `:q!` | 不保存直接退出 |
| `:r filename` | 读取文件，在光标处插入文件 |
| `:! command` | 运行 `shell` |
| `:sh` | 运行一个临时 `shell` |

## 第28 章

所有 Linux 命令

注意：`regex` 表示正则表达式，`*` 表示由 `root` 用户运行的命令

| 命令 | 操作与示例 |
| :--- | :--- |
| `-` | `-` |
| `a2p` | 将 `awk` 翻译为 `awk` |
| `bc` | 交互式计算器 |
| `alias` | 查看或设置别名 |
| `apropos` | 搜索帮助页 |
| `apt-get` | 安装软件包 |
| `aspell` | 检查拼写错误 |
| `at` | 定时运行任务 |
| `awk` | 文本处理工具 |
| `basename` | 获取文件名部分 |
| `bg` | 在后台运行进程 |
| `bunzip2` | 解压 `b2` 文件 |
| `bzip2` | 使用 `bzip2` 压缩 |
| `cal` | 显示日历 |
| `cat` | 连接并并并查看文件内容 |
| `chgrp` | 修改文件的所属组 |
| `chkconfig` | 查看和修改运行级别 |
| `chmod` | 修改文件权限 |
| `chown` | 修改文件或目录的所有者 |
| `chpasswd` | 修改用户密码 |
| `chsh` | 修改用户的登录 `shell` |
| `cksum` | 生成 `CRC` 校验和数字 |
| `clear` | 清除屏幕。 |
| `cmp` | 按字节比较两个文件 |
| `collectl` | 监控当前系统状态 |
| `comm` | 按行比较两个文件 |
| `cp` | 将文件复制到另一个目录 |
| `cp -p` | 复制并保留原始权限 |
| `cp -a` | 复制并保留原始属性 |
| `cpio -o` | 输出归档 `cpio` 文件 |
| `cpio -i` | 输入归档 `cpio` 文件 |
| `bc` | 交互式计算器 |
| `bg` | 在后台运行进程 |
| `bunzip2` | 解压 `b2` 文件 |
| `bzip2` | 使用 `bzip2` 压缩 |
| `cal` | 显示日历 |
| `cat` | 连接并并查看文件内容 |

| 命令 | 操作 | 示例 |
| :--- | :--- | :--- |
| `crontab -e` | 在指定时间运行周期性任务 | 例如 `crontab -e` (`-e` 允许编辑 `crontab` 文件) |
| `crontab -l` | 在指定时间运行周期性任务 | 例如 `crontab -l` (`-l`: 列出 `crontab` 文件) |
| `crontab -r` | 在指定时间运行周期性任务 | 例如 `crontab -r` (`-r`: 删除 `crontab` 文件) |
| `csplit .` | 将文件拆分为若干相互分离的文件 | 例如 `csplit myfile.txt "/part1/" "/part2/"` (分离为名为 `xx00`, `xx01` 的文件) |
| `cut -d` | 显示文件的指定字段 | 例如 `cut -d ":" myfile.txt` (`-d`: 指定字段分隔符 `":"`) |
| `cut -c` | 从文件中提取内容 | 例如 `cut -c 6 myfile.txt` (`-c6`: 每一行的第 6 个字符) |
| `cut -f` | 从文件中提取内容 | 例如 `cut -f 3 myfile.txt` (`-f3`: 指定字段编号为 3) |
| `date` | 显示日期和时间 | 例如 `date` (显示当前日期和时间) |
| `date -s` | 设置日期和时间 | 例如 `date -s "11/20/2014"` (`-s` 设置日期) |
| `dc` | 打开一个命令行桌面计算器 | 例如 `dc` ("`dc`" 意味着桌面计算器) |
| `dd` | 使用数据转储来转换和复制文件 | 例如 `if=/dev/sda of=/dev/sdb` (从 `sda` 复制数据到 `sdb`) |
| `dmesg` | 打印所有内核日志消息 | 例如 `dmesg > kmsg.txt` (将内核消息输出到 `kmsg.txt`) |
| `df` | 显示可用磁盘空间 | 例如 `df` (显示文件系统可用空间) |
| `df -m` | 显示可用磁盘空间 | 例如 `df -m` (`-m`: 以 `Mb` 为单位显示大小) |
| `dhclient` | 配置网络接口 | 例如 `dhclient eth0` (刷新 `eth0` 的 `IP` 地址) |
| `diff` | 显示两个文件之间的差异 | 例如 `diff firstfile.txt secondfile.txt` (显示两个文件之间的差异) |
| `diff3` | 显示三个文件之间的差异 | 例如 `diff3 file1.txt file2.txt file3.txt` (显示三个文件之间的差异) |
| `dig` | 显示 `DNS` 器的详情 | 例如 `dig vxaxx.com` (列出关于 `vxaxx.com` 的信息) |
| `dir` | 显示目录内容 | 例如 `dir` (显示当前目录内容) |
| `dircors` | 显示“`ls`”命令的颜色设置 | 例如 `dircors` (显示 `ls` 的目录颜色) |
| `dirname` | 去路径的最后部分 | 例如 `dirname /foo/bar/baz/myfile.txt` (输出: `/foo/bar/baz`) |
| `du -s` | 显示磁盘占用 | 例如 `du -s *` (`-s` 列出当前目录下的文件大小) |



| 命令 | 描述 | 示例 |
| :--- | :--- | :--- |
| `du -h` | 显示磁盘占用 | 例如 `du -h myfile.txt` (`-h`: 显示人类可读单位) |
| `dump -f` | 为文件系统制作备份 | 例如 `dump -f0 filebk /mydir` (`-f`: 备份, `-0`: 转储级别, `filebk`: 转储文件) |
| `echo` | 在标准输出上显示输入 | 例如 `echo "Hello World!"` (显示 `"Hello World!"`) |
| `echo -e` | 使用转义序列显示文本 | 例如 `echo -e "\n Hello World!"` (`-e`: 允许使用 `\n` 显示文本) |
| `ed` | 打开命令行文本编辑器 | 例如 `ed myfile.txt` (用文本编辑器打开 `myfile.txt`) |
| `egrep` | 搜索文件以匹配指定的正则 | 例如 `egrep "new \| string" myfile.txt` (在 `myfile.txt` 中搜索 `"new \| string"`) |
| `eject` | 弹出 CD 或 DVD 托盘 | 例如 `eject cdrom` (弹出 `cdrom` 托盘) |
| `eject -t` | 弹出或关闭 CD 或 DVD 托盘 | 例如 `eject -t cdrom` (`-t`: 关闭打开的 `cdrom` 托盘) |
| `emacs` | 强大的可扩展编辑器 | 例如 `emacs file.txt` (启动 `emacs` 并打开 `file.txt`) |
| `env` | 显示、设置环境变量 | 例如 `env` (列出当前环境变量) |
| `eval` | 从其参数创建命令 | 例如 `UPLS="eval cd..; ls "` (创建一个名为 `UPLS` 的命令) |
| `exit` | 退出 shell | 例如 `exit` (终止程序并退出) |
| `expand` | 将制表符转换为空格 | 例如 `expand myfile.txt` (将 `myfile.txt` 中的制表符转换为空格) |
| `expand -t` | 将制表符转换为空格 | 例如 `expand -t 3 myfile.txt` (`-t`: 设置间隔 `3` 个字符) |
| `export` | 设置环境变量和值 | 例如 `export newvar=8` (输出: `8`) |
| `expr` | 求一个表达式 | 例如 `expr 10+8` (输出: `18`) |
| `factor` | 显示数字的质因数 | 例如 `factor 100` (输出 `7` `11`) |
| `fc` | 列出、重新执行上一个命令 | 例如 `fc -l` (`-l`: 列出命令历史) |
| `fdisk` | 操作硬盘分区 | 例如 `fdisk /dev/sda` (列出硬盘分区) |
| `fg` | 在前台恢复已停止的任务 | 例如 `fg %3` (在前台恢复该任务) |
| `fgrep` | 搜索文件以匹配指定的字符串 | 例如 `fgrep "good" myfile.txt` (在 `myfile.txt` 中搜索 `"good"`) |
| `file` | 检测文件类型 | 例如 `file myfile.tar` (确定 `myfile.tar` 的文件类型) |
| `find -print` | 在名为指定的目录中查找文件 | 例如 `find -print abc.txt` (`-print`: 指定文件名) |
| `finger` | 显示用户信息 | 例如 `finger username` (列出用户的登录名等) |
| `fmt` | 格式化文本 | 例如 `fmt myfile1.txt > myfile2.txt` (将 `myfile1` 格式化为 `myfile2`) |
| `fmt -u` | 格式化文件 | 例如 `fmt -u myfile.txt` (`-u`: 提供均匀间距) |
| `fold` | 按指定宽度折叠行 | 例如 `fold -w20 myfile.txt` (`-w20`: 设置宽度为 `20`) |
| `for` | 循环 | 例如 `for in {1..5}; do` (循环) |
| `free` | 显示可用内存 | 例如 `free` (显示可用内存信息) |
| `free -m` | 显示可用内存 | 例如 `free -m` (`-m`: 以 Mb 为单位) |
| `fsck` | 检查文件系统 | 例如 `fsck` (检查文件系统) |
| `ftp` | 传输文件 | 例如 `ftp` (通过 `ftp` 传输文件) |
| `gawk` | 在文件中查找并替换 | 例如 `gawk '$0'` (在文件中查找替换) |
| `grep` | 在文件中搜索模式 | 例如 `grep "pattern" myfile.txt` (在文件中搜索模式) |
| `grep -v` | 反向选择匹配模式 | 例如 `grep -v "pattern" myfile.txt` (查找不匹配模式的行) |
| `groups` | 显示用户所属的组 | 例如 `groups` (显示用户所属的组) |
| `groupid` | 显示组的 ID | 例如 `groupid groupname` (显示指定组的 ID) |
| `groupadd` | 创建新用户组 | 例如 `groupadd groupname` (创建新用户组) |
| `groupdel` | 删除用户组 | 例如 `groupdel groupname` (删除用户组) |
| `groupmod` | 修改用户组 | 例如 `groupmod -n newname oldname` (修改组名) |
| `gunzip` | 使用 `gzip` 解压文件 | 例如 `gunzip myfile.txt.gz` (使用 `gzip` 解压文件) |
| `gzip` | 使用 `gzip` 压缩文件 | 例如 `gzip myfile.txt` (使用 `gzip` 压缩文件) |
| `history` | 显示命令历史 | 例如 `history` (显示命令历史) |
| `tar` | 归档 | 例如 `tar -cvf archive.tar dir/` (创建归档) |
| `time` | 显示命令运行时间 | 例如 `time sleep 5` (显示命令运行时间) |
| `top` | 动态显示系统进程 | 例如 `top` (动态显示系统进程) |
| `wc` | 统计计数 | 例如 `wc myfile.txt` (统计文件属性) |
| `sort` | 排序 | 例如 `sort myfile.txt` (对文件排序) |
| `uniq` | 过滤重复行 | 例如 `uniq myfile.txt` (过滤重复行) |
| `watch` | 定期执行命令 | 例如 `watch df -h` (定期执行 `df` 命令) |
| `last` | 显示最近登录的用户 | 例如 `last` (列出最近用户的日期、时间等) |
| `lastb` | 显示失败的登录尝试 | 例如 `lastb` (显示失败的登录尝试) |
| `lastlog` | 显示最后登录信息 | 例如 `lastlog -u username` (`-u`: 指定用户) |
| `less` | 分页显示内容 | 例如 `less myfile.txt` (分页显示 `myfile.txt`) |
| `let` | 对 shell 变量进行算术运算 | 例如 `let a=12; let a=a+8; echo $a` (输出: `20`) |
| `link` | 创建一个文件的链接 | 例如 `link file1.txt file2.txt` (创建从 `file1` 到 `file2` 的链接) |
| `ln` | 为文件创建硬链接 | 例如 `ln ~/myfile.txt` (为 `myfile.txt` 创建硬链接) |
| `ln -s` | 在两个文件之间创建链接 | 例如 `ln -s file1.txt file2.txt` (为 `file1`/`file2` 创建符号链接) |
| `locate` | 查找文件或目录的位置 | 例如 `locate myfile.txt` (在本地机器上查找 `myfile.txt`) |
| `logname` | 显示当前用户的登录名 | 例如 `logname` (显示用户的用户名) |
| `look` | 显示匹配给定前缀的单词 | 例如 `look ab` (输出: `aba`, `abb`, `abc`, `abd`...) |
| `lpc` | 运行行打印控制程序 | 例如 `lpc status` (显示当前打印队列状态) |
| `lpq` | 显示打印机队列状态 | 例如 `lpq` (列出打印队列) |
| `lpr` | 向打印机发送打印请求 | 例如 `lpr myfile.txt` (将 `myfile.txt` 发送到打印机) |
| `lprm` | 取消打印队列中的打印作业 | 例如 `lprm 2` (移除打印作业 `2`) |
| `ls` | 列出当前目录的内容 | 例如 `ls` (列出文件和子目录) |
| `ls -l` | 详细列出当前目录的内容 | 例如 `ls -l` (`-l`: 包含权限的详细列表) |
| `ls -a` | 列出所有项目，包括隐藏文件 | 例如 `ls -a` (`-a`: 显示所有文件) |



| `ls -t` | 按时间戳列出所有项目 | 例如 `ls -t` （`-t`: 按时间戳显示） |

| `ls -lh` | 列出当前目录的内容 | 例如 `ls -lh` （`-lh`: 以 `mb` 和 `gb` 为单位列出文件） |

| `lsattr` | 列出文件或目录的属性 | 例如 `lsattr myfile.txt` （显示 `myfile.txt` 属性） |

| `lsof` | 列出已打开的文件 | 例如 `lsof` （列出所有打开的文件） |

| `man` | 从手册中获取命令帮助 | 例如 `man cat` （显示 `cat` 的手册页） |

| `man -k` | 在手册页中搜索关键词 | 例如 `man -k printf` （`-k`: 指定关键词） |

| `md5sum` | 创建 `md5` 校验和数字 | 例如 `md5sum -c file.txt` （`-c`: 根据校验和验证文件） |

| `mesg` | 启用或禁用消息 | 例如 `mesg` （显示当前的写入状态） |

| `mesg y/n` | 启用或禁用消息 | 例如 `mesg y/n` （`y` 或 `n`: 允许或拒绝消息） |

| `mail` | 发送和接收邮件 | 例如 `mail ray@webprogram.com` （向 `ray@webprogram.com` 发送邮件） |

| `mkdir` | 创建新目录 | 例如 `mkdir mydir` （创建一个名为 `mydir` 的目录） |

| `mknod` | 创建设备文件 | 例如 `mknod /dev/dk b 45 0` （`dk`:设备; `b`:块; `45`:主设备号; `0`:设备号） |

| `more` | 一次显示一个屏幕的内容 | 例如 `more +2 myfile.txt` （`+2`: 从第 2 行开始） |

| `mount` | 挂载存储设备 | 例如 `/dev/cd` （挂载设备 `cd`） |

| `mount -l` | 挂载或显示设备 | 例如 `mount -l` （`-l`: 列出所有挂载的设备） |

| `mt` | 磁带驱动控制 | 例如 `mt -f /dev/tape/eod` （`-f`: 选择 `eod`; 移动到末尾） |

| `mv` | 将文件移动到另一个目录 | 例如 `mv myfile.txt /home/user/mydir` （将 `myfile.txt` 移动到 `mydir` 目录） |

| `mv` | 重命名文件 | 例如 `mv myfile1.txt myfile2.txt` （将 `myfile1` 重命名为 `myfile2`） |

| `netstat` | 显示网络状态 | 例如 `netstat` （打印网络连接、路由表等） |

| `nice` | 设置运行优先级 | 例如 `nice -n 10` （设置优先级值） |

| `nl` | 为文件添加行号 | 例如 `nl myfile.txt` （为 `myfile.txt` 添加行号） |

| `nohup` | 忽略信号继续运行 | 例如 `nohup command` （忽略信号继续运行命令） |

| `nslookup` | 查询 `DNS` | 例如 `nslookup example.com` （查询 `example.com` 的 `IP`） |

| `passwd` | 修改密码 | 例如 `passwd` （更改当前用户密码） |

| `pd` | 显示进程树 | 例如 `pstree` （显示进程树结构） |

| `ps` | 显示当前进程 | 例如 `ps aux` （显示所有运行进程） |

| `kill` | 终止进程 | 例如 `kill -9 1234` （杀死 `PID` 为 `1234` 的进程） |

| `sort` | 按字母排序内容 | 例如 `sort myfile.txt` （按字母排序 `myfile.txt`） |

| `wc` | 统计计数 | 例如 `wc -l myfile.txt` （统计 `myfile.txt` 的行数） |

| `split -b` | 将文件按指定大小拆分成多个文件<br>例如 `split -b 11 file.txt` （将文件拆分为多个 11 字节的文件，命名为 `xaa,xab,xac` 等） |

| `split -l` | 将文件按指定行数拆分成文件<br>例如 `split -l 8 file.txt` （将文件拆分为多个 8 行的文件，命名为 `xaa,xab,xac` 等） |

| `ssh` | 登录远程安全外壳<br>例如 `ssh ray@myexample.com` （安全地连接到远程主机） |

| `ssh -l` | 登录远程安全外壳<br>例如 `ssh -l username hostname` （`-l` 指定你的远程用户名） |

| `stat` | 列出关于文件大小、访问等状态信息<br>例如 `stat myfile.txt` （显示 `myfile.txt` 的统计信息） |

| `su` | 切换用户<br>例如 `su user2` （切换名为 `user2` 的用户） |

| `su -l` | 以 `root` 超用户身份登录<br>例如 `su -l` （`-l`: 输入密码，登录 `root` 账户） |

| `sudo -u` | 以另一个用户的身份执行命令<br>例如 `sudo -u user2 ls /home/mydir` （`-u`: 指定由 `user2` 执行 `ls` 命令） |

| `sudo -v` | 刷新认证超时时间<br>例如 `sudo -v` （下次 `sudo` 将不再需要密码） |

| `sudo -k` | 使认证超时时间过期<br>例如 `sudo -k` （下次 `sudo` 将需要密码） |

| `sum` | 使用校验和对文件进行摘要计算<br>例如 `sum myfile.txt` （为 `myfile.txt` 创建校验和） |

| `suspend` | 挂起正在运行的 `shell`<br>例如 `suspend` （在执行期间暂停系统） |

| `sync` | 将磁盘数据与内存同步<br>例如 `sync` （将所有文件系统缓冲区刷新到磁盘） |

| `tac` | 反序显示文件的行<br>例如 `tac myfile.txt` （从文件的最后一行到第一行打印文件） |

| `tail` | 显示文件的末尾部分<br>例如 `tail -n 20 file.txt` （`-n20`: 输出 `file.txt` 的最后 20 行） |

| `talk` | 与另一个用户通信<br>例如 `talk ray` （与用户 `ray` 通信） |

| `tar -xf` | 提取归档 `tar` 文件<br>例如 `tar -xf archive.tar` （`-xf`: 提取 `tar` 归档文件） |

| `tar -cf` | 创建归档 `tar` 文件<br>例如 `tar -cf archive.tar` （`-cf`: 创建 `tar` 归档文件） |

| `tee` | 打印标准输出并写入文件<br>例如 `sort file1.txt \| tee file2.txt` （排序 `file1.txt` 并写入 `file2.txt`） |

| `tee -a` | 打印标准输出并写入文件<br>例如 `sort file1.txt \| tee -a file2.txt` （`-a`: 追加而非覆盖） |

| `test` | 计算布尔表达式<br>例如 `[ 8 -gt 6 ]; echo $?` （输出: 0 `0`:真; `1`:假） |

| `test` | 计算布尔表达式<br>例如 `[ 5 -eq 6 ]; echo $?` （输出: 1 `0`:真; `1`:假） |

| `time` | 显示运行程序所需的时间<br>例如 `time ftp` （显示执行 `ftp` 所需的时间） |

| `times` | 显示 `shell` 的运行时间<br>例如 `times` （显示系统运行时间） |

| `tload` | 显示系统负载的图形化报告<br>例如 `tload` （向指定进程显示当前系统平均负载） |

| `top` | 列出最活跃或指定的指定的进程<br>例如 `top -p pid` （`-p`: 通过 `pid` 显示特定进程） |

| `touch` | 更新现有文件的时间戳<br>例如 `touch myfile.txt` （将 `myfile.txt` 修改为当前时间） |

| `touch -t` | 更新现有文件的时间戳<br>例如 `touch -t myfile.txt` （`-t`: 指定一个特定时间） |

| `tr` | 翻译字符集<br>例如 `echo apple \| tr "apple" "banana"` （输出: `banana`） |

| `traceroute*` | 追踪到主机的路由<br>例如 `traceroute xvauhdx.com` （追踪数据包到另一个主机的路由） |

| `trap` | 接收信号运行时命令<br>例如 `trap` （显示当前的信号捕获） |

| `tree -p` | 以树形格式列出目录内容<br>例如 `tree -p` （`-p`: 也显示文件权限） |

| `tty` | 显示终端设备的名称<br>例如 `tty` （显示终端文件名） |

| `type` | 检测命令的类型<br>例如 `type wait` （输出: `wait` 是 `shell` 内置命令） |



`ulimit -a` 限制用户资源<br>e.g. `ulimit -a` (-a: 显示系统的所有限制)

`umask` 显示或设置文件权限值<br>e.g. `umask 0022` (允许用户读写，其他用户读取)

`umask` 显示或设置文件权限值<br>e.g. `umask 0002` (允许用户组读写，其他用户读取)

`umask` 显示或设置文件权限值<br>e.g. `umask 077` (允许用户读写，其他用户权限)

`umount` 卸载设备或文件系统<br>e.g. `umount /dev` (卸载设备)

`unalias` 移除别名<br>e.g. `unalias alias` (删除别名)

`uname -a` 显示当前系统信息<br>e.g. `uname -a` (-a: 显示所有信息)

`uname -n` 显示当前系统信息<br>e.g. `uname -n` (-n: 显示主机名)

`unexpand` 将空格转换为制表符<br>e.g. `unexpand myfile.txt` (将 `myfile.txt` 转换为制表符)

`uniq` 过滤文件中的重复行<br>e.g. `uniq myfile.txt` (显示 `myfile.txt` 中的唯一行)

`unset` 移除 shell 变量或函数<br>e.g. `unset var` (删除变量)

`unzip` 从 zip 格式解压文件<br>e.g. `unzip archive.zip` (解压 `archive.zip`)

`uptime` 显示系统运行时间<br>e.g. `uptime` (显示系统运行时间)

`useradd` 添加新用户账户<br>e.g. `useradd username` (创建用户账户)

`useradd -d` 显示新用户的默认目录<br>e.g. `useradd -d` (显示默认目录)

`userdel` 删除现有用户账户<br>e.g. `userdel username` (删除用户账户)

`usermod -d` 修改主目录<br>e.g. `usermod -d /home/mydir` (-d: 指定主目录)

`usermod -l` 修改现有用户账户<br>e.g. `usermod -l username` (-l: 登录名)

`usermod -p` 修改现有用户账户<br>e.g. `usermod -p password` (-p: 修改密码)

`users` 显示当前登录的用户<br>e.g. `users` (列出所有登录的用户)

`vdir` 详细显示目录内容<br>e.g. `vdir` (`vdir` 类似于 `ls`，但更详细)

`vi` 打开文本编辑器<br>e.g. `vi filename` (用 编辑器打开文件)

`vmstat` 报告虚拟内存统计信息<br>e.g. `vmstat` (报告交换、磁盘 i/o 设备等)

`w` 列出每个用户的当前进程<br>e.g. `w username` (显示用户的进程)

`w -s` 以摘要形式列出当前进程<br>e.g. `w -s` (-s: 显示进程摘要)

`wait` 等待进程改变<br>e.g. `wait` (等待进程变化)

`watch` 定期执行命令<br>e.g. `watch -n 5` (-n5: 每 5 秒更新一次)

`wc` 显示字数、行数等<br>e.g. `wc myfile.txt` (列出 `myfile.txt` 的字数、行数等)

`wc -c` 显示字节数、行数等<br>e.g. `wc -c myfile.txt` (-c: 显示字节数)

`wget` 从网站下载网页<br>e.g. `wget http://www.example.com` (从上述 URL 下载网页)

`wget -c` 从网站下载网页<br>e.g. `wget -c http://www.example.com` (-c: 继续下载之前的)

`whatis` 显示命令的帮助页<br>e.g. `whatis ping` (显示 `ping` 的帮助页)

`whereis` 定位命令的源码、手册位置<br>e.g. `whereis ls` (显示 `ls` 的源码、手册位置)

`which` 显示可执行命令的路径<br>e.g. `which ftp` (显示 `ftp` 命令的完整路径)

`who` 显示当前登录的用户<br>e.g. `who` (列出所有登录用户、日期、时间...)

`who -a` 列出所有当前登录的用户<br>e.g. `who -a` (-a: 所有信息)

`whoami` 显示当前用户的登录名<br>e.g. `whoami` (显示你自己的用户名)

`whois` 显示域名所有者信息<br>e.g. `whois xvqix.com` (列出 `xvqix.com` 所有者信息)

`write` 向另一个用户写入消息<br>e.g. `write username` (然后写入你的消息...)

`xargs` 带参数执行命令<br>e.g. `find -name "a.*" | xargs rm` (找到名为 `a.*` 的文件并删除它们)

`xcalc` 启动图形化计算器<br>e.g. `xcalc` (打开科学计算器)

`xclock` 启动图形化时钟<br>e.g. `xclock -digital` (-digital: 指定数字钟)

`yes` 重复输出字符串直到停止<br>e.g. `yes "hello"` (重复输出 `hello` 直到停止)

`yum` 基于 `rpm` 的包管理器<br>e.g. `yum install update` (安装名为 `update` 的包)

`zcat` 输出压缩的文本<br>e.g. `zcat myfile.txt.gz | less` (解压文件并显示内容)

`zless` 显示未压缩/压缩的文件内容<br>e.g. `zless myfile.txt.gz` (`zless`: 按页显示内容)

`zmore` 显示未压缩/压缩的文件内容<br>e.g. `zmore myfile.txt.gz` (`zmore`: 按屏显示内容)

`zip` 将文件压缩为 zip 格式<br>e.g. `zip documents *` (为所有文件创建 `documents.zip`)

`unzip` 从 zip 格式解压文件<br>e.g. `unzip myfile.zip` (解压 `myfile.zip`.)

# 结语

我的朋友们：

这本书仅用于快速学习基础 Linux 命令。

感谢您的支持！

如果您愿意为这本书写一个积极的评价，我将不胜感激。

非常感谢！

顺颂商祺

诚挚地，

Ray Yao

我的朋友，我们下次见！

这本书是一本为初学者编写的指南，旨在快速学习 Linux 管理员或初学者频繁使用的 Linux 命令。书中涵盖了所有核心的 Linux 命令及其操作方法、示例和解释。它还包含了 Linux 帮助命令、符号、快捷键、运行级别（`run levels`）以及 `Vi` 命令。

书中有一张包含所有常用 Linux 命令的长表格，这对你的工作或学习将会有很大帮助。你可以快速学会所有核心的 Linux 命令。
