
在现实世界中，结果各不相同。Solaris 有一个扩展（来自 blastwave.org 的 `pkgutil`），可以从互联网存储库轻松安装软件，就像 Linux 上的原生系统一样。HP-UX 有一个位于 `hpxux.connect.org.uk` 的 HP-UX 移植与归档中心，这是一个良好的仓库，但必须手动逐个下载软件包。在较为糟糕的一端，AIX 的预封装软件可用性相当分散。

无法访问预封装二进制文件的管理员必须使用老办法：下载源代码的 tar 归档包并手动进行配置、编译和安装。根据软件和操作系统的不同，这一过程可能从微不足道到噩梦般艰难。

在本书中，我们通常假设可选软件已经安装，而不是用安装每个包的样板指令来折磨你。虽然可能会引起混淆，但我们有时会提到完成特定项目所需的软件包的确切名称。尽管在大多数情况下，我们不会重复安装指令，因为这些指令在包与包之间往往是相似的。

## 确定软件是否已经安装

由于各种原因，要确定哪个软件包包含你实际需要的二进制文件可能有点棘。与其从软件包级别开始，不如使用 shell 的 `which` 命令来查找相关二进制文件是否已经在你的搜索路径中。例如，以下命令揭示了 GNU C 编译器已安装在某台机器上：

```bash
aix$ gcc
/opt/pware/bin/gcc
```

> Solaris 提供了 Linux 质量的包管理系统和互联网存储库。这一功能在 Solaris 10 中不存在，但很可能出现在 Solaris 11 中。

### 添加新软件

如果你找不到正在寻找的命令，尝试使用它；它会搜索更广泛的系统目录，并且独立于你的 shell 搜索路径。

另一个替代方案是非常用的 `locate` 命令，它会查询预编译的文件系统文件名索引，以匹配特定模式。`locate` 是 GNU findutils 软件包的一部分，大多数 Linux 系统默认包含它，但在 UNIX 上必须手动安装。

`locate` 并不特定于命令或软件包，而是可以找到任何类型的文件。例如，如果你不确定在哪里找到 `signal.h` 头文件，你可以尝试：

```bash
ubuntu locate signal.h
/usr/include/signal.h
/usr/include/asm/signal.h
/usr/include/asm-generic/signal.h
/usr/include/linux/signal.h
```

`locate` 的数据库由 `updatedb` 命令定期更新，该命令通过 cron 运行。因此，`locate` 的结果并不总是反映文件系统的变化。

关于包管理的更多信息，请参阅第 12 章。

如果你知道要查找的包名，也可以使用系统的软件包工具直接检查该包是否存在。例如，在 Red Hat 或 SUSE 系统上，以下命令检查 Python 脚本语言的存在（以及安装版本）：

```bash
redhat$ rpm -q python
python-2.4-3.el15
```

### 添加新软件

如果你需要安装额外的软件，首先需要确定相关软件包的规范名称。例如，你需要将“我想要安装 locate”翻译为“我需要安装 findutils 包”，或将“我需要 named”翻译为“我必须安装 BIND”。网络上的各种系统索引可以提供帮助，但 Google 通常同样有效。作为一个例子，搜索“locate command”会直接带你进入相关的讨论。如果你在 UNIX 系统上，也加上操作系统的名称。

一旦你知道了相关软件的名称，就可以下载并安装它。在 Linux 系统上，完整的安装通常是一条命令；而在 HP 和 AIX 的 Solaris 系统上，你必须下载二进制包或项目的源代码。如果是后者，尝试通过 Google 查找项目的官方网页，并从该项目的任一镜像站下载源代码。

以下示例展示了在我们的每个系统上安装 `wget` 命令。这是一个非常实用的工具，它将 HTTPS 和 FTP 下载转换为原子命令——对于脚本编写非常有用。在我们每个示例 Linux 系统中，wget 都是默认安装的，但下面显示的命令可用于初始安装和后续更新。

Ubuntu 使用 APT，即 Debian 高级软件包工具：

```bash
ubuntu# apt-get install wget
Reading package lists... Done
Building tree
Reading state information... Done
```

SUSE 版本是：

```bash
suse# yast install
```

Red Hat 版本是：

```bash
redhat# yum install wget
```

Solaris 版本是

```bash
solaris# pkgadd -d
```

HP-UX 版本是

```bash
hpux# swadd add wget
```

# 第 1 章

## 从何开始

这种 `configure/make/make install` 序列对于大多数 UNIX 和 Linux 软件都是通用的，只要你安装了开发环境以及任何特定软件包的先决条件，就可以在系统上运行。然而，检查软件包的 `INSTALL` 或 `README` 以获取细节始终是个好主。

在这种情况下，`--disable-ssl` 和 `--disable-dns` 选项用于配置某些依赖于尚未安装的其他库的 wget 功能。在现实生活中，你可能想安装这些先决条件。使用 `configure --help` 查看所有配置选项。另一个有用的 `configure`选项是 `--prefix=directory`，它可以让你将软件存放在 `/usr/local` 以外的地方。

## 1.13 压力下的系统管理

系统管理员往往身兼数职。在现实世界中，他们通常是拥有其他工作的人，被要求顺便照看几台电脑。如果你处于这种状况，请谨慎行事，并意识到这种情况长期来看往往如何发展。

你对系统管理的经验越丰富，社区就越依赖你。网络不可避免地增长，随着你的管理系统变得越来越复杂以及你增加了层级，管理工作往往随着时间的推移而积累。你会很快发现，你是组织中唯一知道如何执行各种任务的人。

一旦同事认为你是本地系统管理员，就很难从这个角色中抽身。这不一定是坏事，但你认识几个人为了逃避这种情况而换了工作。由于许多管理任务是无形的，你可能发现自己被期望既是全职管理员，同时是全职工程师、作家或分析师。

不情愿担任管理员的人员有一种共同倾向，通过采取一种冷淡的态度并提供低劣的服务来拒绝请求¹。这种方法通常会适得其反；它会让你看起来很糟，并产生额外的问题。

相反，要详细记录在系统管理上花费的时间。你的目标应该是将工作保持在可控范围内，并收集证据，以便在你要求辞去管理职责时可以使用。在大多数组织中，你可能需要游说管理层六个月到一年才能获得替补，请提前计划。

另一方面，你可能会发现自己喜欢系统管理，并且认为它优于实际工作。就业前景仍然良好。遗憾的是，你的政治问题可能会加剧。参见第 32 章《管理、政策与政治》，以预见即将到来的乐趣。

¹ 10. Simon Travaglia 在《Bastard Operator from Hell》故事中以充满爱意且虐态的方式记录了这种倾向；存档请参见 bofh.net。（在 BOFH 之下。）

## 1.14 推荐阅读

ROBBINS, ARNOLD. *UNIX in a Nutshell (4th Edition)*. Sebastopol, CA: O'Reilly Media, 2008.

SIEVER, ELLEN, AARON WEBER, AND STEPHEN FIGGINS. *Linux in a Nutshell (5th Edition)*. Sebastopol, CA: O'Reilly Media, 2006.

GANCARZ, MIKE. *Linux and the Unix Philosophy*. Boston: Digital Press, 2003.

SALUS, PETER H. *The Daemon, the GNU & the Penguin: Free and Open Software is Changing the World*. Reed Media Services, 2008.

这本由 UNIX 最著名的历史学家编写的关于开源运动的迷人历史也可以在 groklow.com 上通过创意许可获取。书本身的 URL 相当长；可以在 groklow.com 查找当前链接，或尝试这个压缩等效：tinyurl.com/d6uj7。

RAYMOND, ERIC S. *The Cathedral & The Bazaar: Musings on Linux and Open Source by an Axell Revolutionary*. Sebastopol, CA: O'Reilly Media, 2001.

### 系统管理

LIMONCELLI, THOMAS A., CHRISTINA J. HOGAN, AND STRATA R. CHALUP. *The Practice of System and Network Administration (Second Edition)*. Reading, MA: Addison-Wesley, 2008.

这是一本好书，对系统管理的政策和程序方面的涵盖特别详尽。作者在 everythingysadmin.com 维护着一个系统管理博客。

FRISCH, ELEEN. *Essential System Administration (3rd Edition)*. Sebastopol, CA: O'Reilly Media, 2002.

这是一本经典的 UNIX 系统管理方位指南，遗憾的是它已经过时了。我们希望一个新版本正在制作中！

### 核心工具

ROBBINS, ARNOLD, ELBERT HANNAH, AND LINDA LAMB. *Learning the vi and Vim Editors*. Sebastopol, CA: O'Reilly Media, 2008.

POWERS, SHELLY, JERRY PEEK, TIM O'REILLY, AND MIKE LOUKIDES. *UNIX Power Tools (3rd Edition)*. Sebastopol, CA: O'Reilly Media, 2003.

MICHAEL, RANDAL. *Mastering UNIX Shell Scripting: BASH, Bourne, and Korn Shell Scripting for Programmers, System Administrators, and UNIX Gurus*. Indianapolis, IN: Wiley Publishing, Inc., 2008.

ROBBINS, ARNOLD AND NELSON H. F. FEEBEE. *Shell Scripting*. Sebastopol, CA: O'Reilly Media, 2005.

WALLY, TOM CHRISTIANSEN, AND JOHN ON SWART. *Programming Perl (3rd Edition)*. Cambridge, MA: O'Reilly Media, 2000.

CHRISTIANSEN, TOM, AND NATHAN TORKINGTON. *Perl Cookbook (2nd Edition)*. Sebastopol, CA: O'Reilly Media, 2003.

BLANK-EDELMAN, DAVID N. *Automating System Administration with Perl (2nd Edition)*. Sebastopol, CA: O'Reilly Media, 2009.

PILGRIM, MARK. *Dive Into Python*. Berkeley, CA: Apress, 2004.

此书也可以在网上 diveintython.org 免费获取。

FLANAGAN, DAVID, AND YUKIHIRO MATSUMOTO. *The Ruby Programming Language*. Sebastopol, CA: O'Reilly Media, 2008.

这本《Everything You Need Know》虽然有些过时，但它涵盖了 Ruby 1.9 版本并包含了丰富的细节。适合已经具备 Perl 或 Python 工作知识的人。

## 1.15 练习

- E1.2 哪个配置文件控制 man 命令的行为？如果你想将本地材料存储在 `/doc/man`，需要在文件中添加哪些行？你需要使用什么样的目录结构来使 `/doc/man` 成为体系的一部分？

- E1.4 研究几个 UNIX 和 Linux 系统，并为以下应用推荐一个操作系统。解释你的选择。

    - a) 在家庭办公室工作的单用户

    - b) 大学计算机科学实验室

    - c) 公司 Web 服务器

    - d) 为货运公司运行数据库的服务器集群

- a) 在报告 bug 之前你应该做什么？

    - b) 如果你认为 bug 是真实的，你应该通知谁以及如何通知？

    - c) 必须包含哪些信息才能使报告有用？

- E1.6 Linux 已经大规模进入生产环境。UNIX 会灭结吗？为什么或为什么不会？

# 第 2 章 脚本与 Shell

`sh`（原始的 Bourne shell）和 `ksh`（Korn shell）被用于一些 UNIX 系统。Shell 脚本通常用于轻量级任务，例如自动化一系列命令或组合多个过滤器来处理数据。

由于 shell 始终是可用的，因此 shell 脚本具有很强的可移植性，除了它们所调用的命令外，很少有依赖。无论你是否选择 shell，她（系统环境）可能已经选择了你：大多数环境都包含大量复杂的现有 sh 脚本，这些脚本经常需要管理员对其进行阅读、理解和调整。

对于更复杂的脚本，建议跳转到如 Perl 或 Python 等真正的编程语言，这两者都非常适合管理工作。与 shell 相比，这些语言融合了数十年的进步，而且它们的文本处理能力（对管理员来说无价之）如此强大，以至于 sh 只能在羞愧中哭泣和畏缩。

Perl 和 Python 的主要缺点是它们的环境搭建可能有些繁琐，尤其是当你开始使用带有编译组件的第三方库时。shell 通过具有模块化结构且没有第三方库来规避这一特定问题。

本章将快速介绍 bash、Perl 和 Python 作为脚本语言，并介绍正则表达式作为一种通用技术。

## 2.1 Shell 基础

在开始学习 shell 脚本之前，让我们先回顾一下 shell 的一些基本功能和语法。本节的内容适用于 sh 系中的所有主要 shell（包括 bash 和 ksh，但不包括 csh 或 tcsh），无论你正在使用的具体平台是什么。尝试那些你不熟悉的格式，并进行实验吧！

### 命令编辑

我们见过太多人使用方向键来编辑命令行了。在你的文本编辑器中你不会那样做，对吧？

如果你喜欢 emacs，在编辑时可以使用所有基础命令。`<Control-E>` 跳到行尾，`<Control-A>` 跳到行首。`<Control-P>` 向后回溯最近执行的命令并调回它们进行编辑。`<Control-R>` 增量地搜索你的历史记录以查找旧命令。

如果你喜欢 vi，可以如下所示将你的 shell 命令行编辑切换到 vi 模式：

```bash
$ set -o vi
```

像 vi 一样，编辑是模式化的；但是，你从输入模式开始。输入 `<Esc>` 退出输入模式，输入 "i" 重新进入。在编辑模式下，“w” 向前移动一个单词，“fX” 在行中查找下一个 X，以此此类推。你可以通过 `<Esc> k` 遍历过去的命令历史。想换回 emacs 编辑模式吗？

```bash
$ set -emacs
```

### 管道与重定向

每个进程至少有三个可用通信通道：“标准输入”（STDIN）、“标准输出”（STDOUT）和“标准错误”（STDERR）。内核根据进程的行为设置这些通道，因此进程本身并不一定知道它们通向何处。它们可能连接到终端窗口、文件、网络连接或属于另一个进程的通道，这仅列了其中的可能性。

UNIX 有一种 I/O 模型，其中每个通道用一个较小的文件描述符命名。分配给通道的精确数字通常并不重要，但 STDIN、STDOUT 和 STDERR 保证对应文件描述符 0、1 和 2，因此通过数字引用这些通道是安全的。在交互式终端窗口的语境下，STDIN 通常从键盘读取，STDOUT 和 STDERR 都将它们的输出写入屏幕。

大多数命令从 STDIN 接收输入并向 STDOUT 写入输出。它们将错误信息写入 STDERR。这种约定允许你将命令像构建块一样组合起来，创建复合管道。

shell 将符号 `<`, `>`, `>>` 解释为重定向命令输出或输入来自文件的指令。`<` 将命令的 STDIN 连接到现有文件的内容。`>` 和 `>>` 重定向 STDOUT；`>` 替换文件的现有内容，而 `>>` 则在其后追加。例如，命令

```bash
$ echo "This is a test message." > /tmp/mymessage
```

在文件 `/tmp/mymessage` 中存储单行内容，必要时创建该文件。下面的命令将该文件的内容通过发送给用户 johndoe。

```bash
$ mail -s "Mail test" johndoe < /tmp/mymessage
```

要将 STDOUT 和 STDERR 重定向到同一个地方，使用 `>&` 符号。只重定向 STDERR，使用 `2`。

`find` 命令说明了为什么你可能想要单独处理 STDOUT 和 STDERR，因为它倾向于在两个通道上产生输出，特别是当你作为无权限用户时。例如，命令如

```bash
$ find -name core
```

通常会导致大量的“权限拒绝”错误信息，淹没在混乱中。要丢弃所有错误信息，你可以使用

```bash
$ find -name core 2 > /dev/null
```
