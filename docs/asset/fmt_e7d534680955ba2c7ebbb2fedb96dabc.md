
- (13) `ftp://cpan.pair.com/pub/CPAN/`
- (14) `ftp://cpan.teglelobe.net/pub/CPAN/`
- (15) `ftp://cpan.thepirtroup.com/`
- (16) `ftp://csociety-ftp.ecn.purdue.edu/pub/CPAN`

还有 42 个项目，按空格回车显示它们。

选择你喜欢的任意数量的 URL（通过数字），将它们放在同一行，用空格隔开，例如 `1 4 5` [1 2 3 4 5 6] : []

最终，CPAN 将提示你输入另一个 URL 或按回车退出，此时你需要输入用空格分隔的数字。每个数字将代表 cpan 在（请求时）用于下载软件的特定站点。在上面的示例中，前六个站点都被选中，并按了回车键。再次输入（这次在空行上）将结束选择过程，保存更改并启动 cpan 的配置过程。这个配置过程很麻烦，但请记住，只需要执行一次。一旦 cpan 运行起来，你就可以轻松地使用更大更复杂的 Perl 脚本，而且有大量的免费模块可用。

## 坏掉的键！

使用 cpan 时，你首先发现的现象之一是退格键不起作用。通过安装 `Term::ReadKey` 可以轻松解决。这个模块和 `Term::ReadLine` 将让你访问这个以及像箭头和下方向键等功能。

## 使用 CPAN 的交互模式

Perl 有时会遇到依赖问题。类似于人类的依赖，这意味着脚本急需某些模块。现在，在某些情况下，简单地安装一个特定模块是解决此问题最简单的方法，但在其他情况下，该模块将依赖于其他模块，导致 Linux 式的头疼。幸运的是，CPAN 能够处理模块间的依赖关系并为你解决这些问题，提供一组被称为 bundle（包）的依赖性模块。在大多数情况下，下载和安装一个 bundle 和安装单个模块一样简单。然而，你处理的是 Perl 模块，而不是分发版（模块的特定发布），后者主要供追求最新、最强大且通常不稳定的用户。

## 图 5.3 困惑的 Perl

```
$jpb12:~workbench/Coding johnny$ perl dns-mine.pl
Can't locate SOAP/Lite.pm in @INC: /System/Library/Perl/5.8.6/darwin
--multi-thread-
-2/Library/Perl/5.8.6/Network/Library/Perl/5.8.6/darwin-thread-m
ulti-2/Library/Perl/5.8.6/Network/Library/Perl/5.8.6/darwin-th
read-multi-2/Library/Perl/5.8.6/Network/Library/Perl/5.8.6/darwin-th
/Per/System/Library/Perl/5.8.6/darwin-multi-level /System/Library/Extras/5.8.6/
libary/5.8.6.pm at dns-mine.pl line 11.
BEGIN ---compilation aborted at dns-mine.pl line 11.
$jpb12:~workbench/Coding johnny$
```

让我们看看 `dns-mine.pl` 脚本中的依赖问题，看看如何用 cpan 解决它。首先，我们需要在 cpan 内部搜索以确定这个 `SOAP/Lite.pm` 文件的具体名称。要搜索特定字符串，首先从终端通过 `sudo cpan` 启动 cpan。你会看到一个 `cpan>` 提示符，如图 5.4 所示。

## 图 5.4 CPAN 终端

```
Terminal - 77x9
j0pb12:~/workbench/Coding johnnylong$ sudo cpan
Password:
cpan shell -- CPAN exploration and modules installation (v1.7601)
ReadLine support enabled
cpan> 
```

从这里开始，你可以输入会被程序解释的命令。最常用的函数（可以通过在提示符处输入 `help` 来列出其中一些）如表 5.1 所示。

### 表 5.1 常用 CPAN 命令

| 命令 | 参数 | 说明 |
| --- | --- | --- |
| help | | 显示帮助菜单 |
| install | 发行版或包 | 安装发行版或包 |
| force install | 发行版或包 | 强制安装发行版或包 |
| a, b, d, m | | 列出所有作者、包、发行版或模块 |
| a, b, d, m | 单词或表达式 | 在作者、包、发行版或模块中搜索 |
| i | | 列出所有作者、包、发行版和模块 |
| i | 单词或表达式 | 在作者、包、发行版和模块中搜索 |

Perl 耐心地解释说，我们正在运行的脚本依赖于 SOAP，具体说是 `SOAP/Lite.pm`，我们需要搜索 cpan。对于初学者来说，实现此最简单的方法是使用 `i` 命令，它会在 cpan 的作者、包、发行版或模块中搜索特定字符串。例如：

```
cpan> i SOAP
```

奇怪的发行版名称 [SOAP]

```
Module id = SOAP
DESCRIPTION SOAP/Perl language mapping
CPAN_USERID KB (Keith Brown <kbrown@developer.com>)
CPAN_VERSION 0.28
CPAN_FILE K/KB/KBROWN/SOAP-0.28.tar.gz
DSLI_STATUS cmp0 (pre-alpha,mailing-list,perl,object-oriented)
INST_FILE (not installed)
```

这表明 id 为 SOAP 的模块确实存在，但我们的 Perl 脚本的错误信息更具体一些。该脚本需要 SOAP Lite。CPAN 允许我们通过正则表达式扩展搜索。将我们的命令更改为 `i /SOAP/` 将搜索所有记录中是否存在“SOAP”一词，提供每条记录的预览，以便我们判断它是否是我们找的记录。虽然返回了一百多条记录，但它们按字母顺序排列，且其中一个以“Module SOAP::Lite”开头的条目通过名称描述了我们寻找的精确模块。为了在唯一且特定的层次结构中正确细分模块，该层次结构涉及双冒号（`::`）的使用。例如，SOAP 是一个巨大的模块库。虽然你可以安装 SOAP 库中的每一个模块，但没有必要，而且会浪费大量的位。相反，只需安装你需要的特定模块，在本例中为 `SOAP::Lite`。要安装 `SOAP::Lite` 模块，只需在 cpan 提示符处输入 `install SOAP::Lite`，并注意处理命令的大小写敏感。在大多数情况下，在接受每个提示的默认选择后，你将获得一个无错误的安装。但在某些情况下，安装可能会因错误失败（特别是在测试阶段），你需要强制安装该模块。这听起来并没有那么糟糕，因为大多数模块在需要强制安装之前一直运行良好。要强制安装 `SOAP::Lite`，只需在 cpan 提示符处输入 `force install SOAP::Lite`。一旦安装完成，再次运行 `install SOAP::Lite` 将检查是否有该模块的更新，如果没有，则会通知你。这突出了 cpan 脚本另一个重要功能：非常方便地更新到最新模块。一旦安装了 `SOAP::Lite`，`dns-mine.pl` 脚本就可以完美运行，尽管这些模块需要强制安装。

![](img/3f6a4a8b6ed1d4458658b001e0374e75_192_0.png)

## 在命令行模式下使用 CPAN

一旦你熟悉了 cpan 程序的交互模式，你可能想让 cpan 运行得更快，而这通过 cpan 的命令行界面可以轻松实现。你不需要启动 cpan 程序，而是运行 perl 并带有各种参数，来描述你具体想让 cpan 程序为你做些什么。Perl 的 `-M` 和 `-e` 参数允许你指定想要执行的模块和命令。例如，要启动 cpan 的交互模式，你可以在根 shell 中运行 `perl -MCPAN -e shell`，或者在 shell 中运行 `sudo perl -MCPAN -e shell`。此命令指定了你想与 CPAN 模块交互的参数，并且你希望该模块在 CPAN 内部运行 shell 命令。这可以扩展到安装模块或包，例如使用 `perl -MCPAN -e 'install Bundle::CPAN'`，这会安装 cpan 包。当然，如果你想用 `perl -MCPAN -e 'force install Bundle::CPAN'` 强制安装，这种方法同样适用。

Perl 是一门极其灵活的语言，许多程序都是用这种语言编写的。得益于 Mac OS X 内置的 Perl 解释器以及 CPAN 归档和程序，你可以直接在 Mac 上运行绝大多数 Perl 程序，而几乎或完全没有麻烦。

## 安装 XWindows

XWindows (www.x.org) 是一种用于图形界面的标准工具包和协议。XWindows 目前在 Linux 系统上非常流行，像 KDE 和 GNOME 等窗口管理器已成为 Linux 用户的标准用户界面。在 OS X 上安装 XWindows 允许许多此类图形程序在 OS X 下运行。XWindows 可以通过多种方式安装，但最直接的方法之一是安装 Apple 提供的版本的 XWindows。X11（当前协议版本）包含在当前的 Mac OS X 安装媒体中，但并未作为标准 OS X 安装的一部分进行安装。OS CD 上的可选安装程序安装器映像生成了一个可以安装的可选应用程序列表，包括 X11，如图 5.5 所示。

### 图 5.5 Apple 的 X11 安装

![](img/3f6a4a8b6ed1d4458658b001e0374e75_194_0.png)

一旦安装了 X11，X11 图标会被放在应用程序文件夹中，几个应用程序将安装在 `/usr/X11R6/bin` 中。当运行 X11 程序时，会出现一个 xterm，并且可以从 xterm 运行常见的 XWindows 应用程序（如 `xclock`），如图 5.6 所示。

### 图 5.6 在 OS X 上运行 XWindows 和 xclock

![](img/3f6a4a8b6ed1d4458658b001e0374e75_194_1.png)

需要记住的是，XWindows 程序必须从 xterm 窗口运行，而不是从 Terminal 窗口运行。正如我们在本章后面将看到的，更复杂的 XWindows 程序（如 Ethereal）可以从 xterm 运行。

## 在 OS X 上编译程序

虽然有很多不同的语言可以考虑，如 C 或 C++，但大多数开源应用程序都是用 C 或 C++ 编写的。获取移植后的源码或二进制文件通常更好，正如我们在下一节将讨论的，但大多数标准的源代码可以在 OS X 上良好地安装和运行。尽管我们无法涵盖 OS X 上编译的所有细节，但大多数“友好型”应用程序只需要非常简单的步骤：

1. 下载源代码。
2. 使用 StuffIt 或类似的程序解压源代码。
3. 进入解压创建的目录。
4. 从命令行运行 `configure` 脚本。
5. 运行 `make`（假设 `configure` 成功）。
6. 运行 `make install`（假设 `make` 命令执行成功）。

在许多情况下，此过程将产生可执行二进制文件，以及支持性文档（通常为 man 页面）和各种支持和配置文件。然而，生活并不总是简单，某些软件在移植（特定的程序修改）之前才能在特定平台上安装。

## 编译与移植

程序员分发开源软件代码有许多选择。他可以选择分发不带任何安装文件的源码，分发带 Makefile 的源码以辅助编译复杂代码，或者分发带有 `configure` 脚本的源码，用户运行该脚本来创建 Makefile。在我们简要查看编译和安装软件的优缺点之前，

![](img/3f6a4a8b6ed1d4458658b001e0374e75_195_0.png)

第一种方案极其原始，除了非常简单的软件外，它可能会在终端用户的系统上引起不可预见的兼容性问题。如果出现这些问题，用户可能无法编译或运行该软件。分发带有 `Makefile` 的源代码（由 `make` 程序读取，该程序从软件的根目录下执行）无疑对终端用户有所帮助，特别是对于大型或复杂的程序，但取决于用户的系统配置，仍然可能出现不兼容的情况。目前，程序员分发与许多操作系统环境广泛兼容的开源软件的最佳方法是使用 `autoconf` 程序。该程序会创建 `configure` 脚本，这些脚本在用户系统上执行时，会自动检测操作系统环境，并尝试为该软件的安装创建一个定制的 `Makefile`。如果一个程序随带了 `configure` 脚本，那么该软件最终在 Mac OS 上编译并运行的几率相当大。不过，你的具体情况可能会因人而异。

移植是指通过调整和修改软件以使其在特定平台上运行的过程。这个过程通常会导致程序的纯净安装，在大多数情况下，经验丰富的程序员会在将代码作为包分发之前，在特定平台上对代码进行检查、修改和测试。移植后的软件以源码或二进制格式提供。源码包经过修改可以干净地编译，而二进制包则已准备好运行。源码包通常是最新的版本。无论你选择哪种格式，软件可能都需要额外的软件来满足某些依赖关系。包管理器在为你自动化这一过程方面做得很好（正如我们将在下一章中看到的），但使用多个包管理器可能会变得有些混乱，尤其是当你使用不同的包管理器安装同一个特定程序的多个版本时。在接下来的章节中，我们将开始介绍两个流行的包管理器，并讨论它们如何简化这一过程。

# 在 Mac OS 上安装移植后的软件

在深入讨论下载和安装移植代码的细节之前，让我们先来看一个失败了的源码安装案例。了解从源码安装程序会有多么困难，将帮助你理解为什么移植是一个更受青睐的方法。

## 为什么要移植：一次失败的源码安装

在这个示例中，我们将尝试安装 Fyodor 编写的 `nmap` 端口扫描器。这个程序是必不可少的，但在某些情况下，源码发行版很难安装。

![](img/3f6a4a8b6ed1d4458658b001e0374e75_196_0.png)

# 第 5 章 针对渗透测试者的 Mac OS X

首先，我们将从 insecure.org 下载 `.tar.gz` 或 `.tgz` (tar gzip) `.bz` (bzip) 格式的发行文件。例如，nmap 3.75 版本的 gzip 文件将是 `nmap-3.75.tgz`。然后将使用命令 `tar -xvzf nmap-3.75.tar` 对文件进行解压和解包。这将创建一个名为 `nmap-3.75` 的子目录，可以通过命令 `cd nmap-3.75` 进入该目录。该 `nmap` 的 `README` 说明，在 Mac OS X 上必须在 `./configure` 命令的末尾添加 `CPP=/usr/bin/cpp`，因此需要执行 `./configure CPP=/usr/bin/cpp` 来创建 `Makefile`，这是下一步所必需的。一旦 `configure` 命令最终完成，在执行 `make` 命令之后就是 `make install`。然而，在 `make` 过程进行几分钟后，产生了一个难看的错误信息：

```
++ -lbase -insock/src/ -o nmap main.o nmap_targets tcpip.o nmap_error.o
utils.o idle_scan.o ossan.output.o scan_engine.o timing.o charpool.o
services.o protocols.o nmap_rpc.o portlist.o NmapOpts.o Target.o
FingerprintResults.o scan.o NmapOutputTable.o MACLOOKup.o -lbase -insock
libpcap -lssl -lcrypto
/usr/bin/ld: can't locate file -lssl -lstdc++
collect2: [nmap] returned 1 exit status
make: *** Error 1
j0pb12:/Desktop/nmap-3.75 johnnylong$
```

任何合格的 Google 用户都会进行几次查询来定位问题所在，在经历了很多挫败后，他们发现并没有明显的解决方案可以解决这个问题。这种经历想起了许多 UNIX 和 Linux 用户在安装软件时面临的情况，这完全不是 Mac 用户对系统的预期。事实上，这种为了让某个软件运行而进行的数字化的笨拙，正是促使许多最初使用 Mac 的原因。软件移植消除了这一过程中的猜测，并将那些糟糕的技术细节离用户远远、非常远。

在接下来的章节中，我们将开始讨论包管理器。这些程序消除了安装开源软件时的大量猜测，如图 5.7 所示，包管理器能够通过一个简单的命令安装 `nmap 3.75`。这比下载、编译和排查源码故障要好得多，尤其是如果你不在意拥有绝对最新的软件版本的话。

![](img/3f6a4a8b6ed1d4458658b001e0374e75_197_0.png)

# 5.7 无痛安装 nmap — bash
