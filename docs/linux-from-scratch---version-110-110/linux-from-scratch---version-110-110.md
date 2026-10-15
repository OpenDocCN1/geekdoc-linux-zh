
# Linux 从零开始 - 11.0 版本

## 9. 系统配置

- 9.1. 引言 ................................................... 229

### D.26. `/lib/services/ipv4-static` ........................................................ 337

### D.27. `/lib/services/ipv4-static-route` ................................................ 338

## E. Udev 配置规则 ................................................... 341

+ E.1. Lfs-rules ............................................................ 341

## F. LFS 许可证 .......................................................... 342

+ F.1. 知识共享许可 ................................... 342

+ F.2. MIT 许可证 ............................................................ 346

# 前言

# 序

我学习并更好地理解 Linux 的之旅始于 1998 年。当时我刚刚安装了我的第一个 Linux 发行版，并迅速被 Linux 背后的整套概念和哲学所吸引。

完成一项任务总有许多方法。Linux 发行版也是如此。多年年来存在过许多发行版。有些仍然存在，有些已经演变成了其他形式，而另一些则被遗落在记忆中。它们都以不同的方式来适应目标受众的需求。因为存在如此许多实现同一目标的不同方式，我意识到不再需要受限于任何一种实现方案。在发现 Linux 之前，由于没有选择，我们只能忍受其他操作系统。无论你喜不不喜欢，它就是那样。有了 Linux，“选择”的概念一次又一次地出现。你是自由的，并被鼓励去改变它。

我尝试了许多发行版，但无法决定选择哪一个。它们本身都是非常出色的系统。这不再是一个对与错的问题，而变成了一个个人品味的问题。有了如此多的选择，似乎没有一个系统是完美适合我的。因此，我着手创建自己的 Linux 系统，让它完全符合我的偏好。

为了让它属于我自己，我决定从源代码编译所有内容，而不是使用预编译的二进制包。这个“完美”的系统将拥有各种系统的优点，同时避开它们被感知的弱点。起初，这个想法相当大胆。但我始终坚持这个想法：一个系统是可以被构建的。

在解决了循环依赖和编译时错误等问题后，我终于构建了一个自定义的 Linux 系统。它能够完全运行，并且像当时的任何 Linux 系统一样可以完美使用。但它是我的产物。能组装出这样一个系统真的非常有成就感。

Gerard Beek

gerard@linux.org

# Audience

有很多理由你想要阅读这本书。

The goal of Linux From Scratch is to build a system that is truly yours. Another key benefit of LFS is to learn how Linux works. By building from scratch, you are empowered to customize the system. There are many reasons why you would want to read this.

For building LFS, the gain of building on a 64-bit system compared to a 32-bit system is minimal. For example, in the build of LFS9.1 on an i7-4790 CPU based system, using 4 cores, the following statistics were measured:

| Architecture | Build Time | Build Size |
|---|---|---|
| 32-bit | 239.9 minutes | 3.6 GB |
| 64-bit | 233.2 minutes | 4.4 GB |

As you can see, on the same hardware, the 64-bit build is only 3% faster and 22% larger than the 32-bit build. The default 64-bit build results from LFS is considered a "pure 64-bit system". That is, building a "multi-lib" system requires compiling many applications twice, once for a 32-bit system and once for a 64-bit system. This is not directly supported in LFS because it would interfere with the educational objective of providing the instructions needed for a straightforward base Linux system. Some LFS/editors maintain a fork of LFS for multilib, which is accessible at https://www.linuxfromscratch.org/~thomas/multilib/index.html. But it is an advanced topic.

The target architectures of LFS are AMD/Intel x86 (32-bit) and x8664 (64-bit) CPUs. On the other hand, the instructions in this book are also known to work, with some modifications, with Power PC and ARM CPUs.

However, a 32-bit distribution may be sufficient if you plan to use LFS as a LAMP server, or as a firewall.

One of the reasons for the project's existence is to provide a foundation for others.

# 前提条件

构建 LFS 并不是一项简单的任务。它要求你具备一定水平的 Unix 管理现有知识，以便解决问题并正确执行列出的命令。特别是，最基本的要求是你应该已经具备了使用命令行（shell）来复制或移动文件和目录、列出目录和文件内容以及更改当前目录的能力。此外，希望你对使用和安装 Linux 软件有合理的了解。

由于 LFS 教程假设你至少具备这种基础技能水平，因此各种 LFS 支持论坛不太可能在这些方面为你提供太多帮助。如果你发现你关于基础知识的问题没有得到解答，你将被引导参阅 LFS 必要的预读列表。

在构建-LFS 之前，我们建议阅读以下内容：

- *Software-Building-HOWTO* http://www.tldp.org/HOWTO/Software-Building-HOWTO.html

  这是一份关于在 Linux 下构建和安装“通用”Unix 软件包的全面指南。尽管它是很久以前编写的，但它对构建和安装软件所需的某些技术提供了良好的总结。

- *Beginner's Guide to Installing from Source* http://mov.linux.net/linux/beginners-installing-from-source/

  该指南对从源代码构建软件所需的各种技能和技术进行了良好的总结。

# LFS 与标准

LFS 的结构尽可能地遵循 Linux 标准。主要标准有：

- *POSIX-1-2008.*

- *文件系统层次结构标准 (FHS) 版本 3.0*

- *Linux 标准基础 (LSB) 版本 5.0 (2015)*

> LSB 包含四个标准：核心 (Core)、桌面 (Desktop)、运行时语言和成像 (Imaging)。除了通用要求外，还有特定架构的要求。此外两个试用领域：Gtk3 和图形 (Graphics)。LFS 尝试符合上一节讨论的架构。

> 许多人并不认同 LSB 的要求。定义它的主要目的是确保专有软件能够在合规系统上正确安装和运行。如果 LFS 是基于源码的，用户对所需的软件包具有控制权，并可以选择不安装某些由 LSB 指定的软件包。

创建一个能够通过 LSB 认证的完整 LFS 是可能的，但需要许多超出 LFS 范围之外的额外软件包。这些额外软件包在 BLFS 中有安装说明。

# LFS 提供的满足 LSB 要求的软件包

LSB 核心：

Bash, Bc, Binutils, Coreutils, Diffutils, Find, Gutils, Gawk, Grep, Gzip, M4, Man-DB, Ncurses, Procps, Psmisc, Sed, Shadow, Tar, Util-linux, Zlib

LSB 桌面：

无

LSB 运行时语言：Perl

LSB 成像：无

LSB Gtk3 和 LSB 图形（试用）：无

# BLFS 提供的满足 LSB 要求的软件包

LSB 核心：At, Batch (At 的一部分), Cpio, Ed, Fcrontab, LSB-Tools, NSPR, NSS, Pam, Pax, Sendmail (Postfix or Exim), time

LSB 桌面：Alsa, ATK, Desktop-file-utils, Freetype, Configfont, Gdk-pixbuf, Glib2, GTK+2, Icon-naming, Libjpeg-turbo, Libpng, Libtiff, Libxml2, MesaLib, Pango, Xdg, Xorg

LSB 运行时语言：Python, Libxml2, Libxslt

LSB 成像：CUPS, Cups-filters, Ghostscript, SANE

LSB Gtk3 和 LSB 图形（试用）：GTK+3



# LFS 或 BLFS 未提供但满足 LSB 要求的软件包

LSB 核心：无

LSB 桌面：Qt4（但优选 Qt5）

LSB 运行时语言：无

LSB 成像：无

LSB Gtk3 和 LSB 图形（试用）：无

# 书中软件包的理由

如前所述，LFS 的目标是构建一个完整且可用的基础级系统。这包含了所有复制自身所需的软件包，同时提供了一个相对最小的基底，以便根据用户的选择定制一个更完整的系统。这并不意味着 LFS 是可能的最小系统。它包含了几个并非严格要求的的重要软件包。下面的列表记录了书中每个软件包的选入理由。

- Acl
该软件包包含管理访问控制列表（ACL）的工具，用于为文件和目录定义更细粒度的自主裁量访问权限。

- Attr
该软件包包含用于管理文件系统对象扩展属性的程序。

- Autoconf
该软件包包含生成 shell 脚本的程序，可以从开发者的模板自动配置源代码。在更新构建过程后，通常需要它来重新构建软件包。

- Automake
该软件包包含从模板生成 Makefile 的程序。在更新构建过程后，通常需要它来重新构建软件包。

- Bash
该软件包满足 LSB 核心要求，为系统提供 Bourne Shell 接口。选择它而不是其他 shell 包是因为它的常用性以及在基础 shell 函数之外的扩展功能。

- Bc
该软件包提供了一种任意精度数值处理语言。它满足了构建 Linux 内核时所需。

- Binutils
该软件包包含链接器、汇编器以及用于处理目标文件的工具。编译书中的大多数软件包都需要用到该软件包中的程序。

- Bison
该软件包包含 GNU 版本的 yacc（另一个编译器）。构建若干个软件包时需要它。

- Bzip2
该软件包包含用于压缩和解压文件的程序。它用于解压 LFS 及其它的软件包。

- Check
该软件包包含一个用于其他程序的测试框架。

- Coreutils
该软件包包含许多用于查看和操作文件的基本程序。

- Deja
该软件包包含一个测试其他程序的框架。

- Diffutils
该软件包包含显示文件间差异的程序。这些程序用于创建补丁（patches）。

- E2sprogs
该软件包包含处理 ext2、ext3 和 ext4 文件系统的工具。Linux 支持这些文件系统。

- Eudev
该软件包是一个设备管理器。它动态地控制 `/dev` 中设备的所有权、权限、名称和符号链接。

- Expat
该软件包包含一个相对较小的 XML 解析库。许多软件包都需要它。

- Expect
该软件包包含一个用于与其他交互程序执行脚本化对话的程序。它通常用于测试软件包。

- File
该软件包包含一个用于确定给定文件类型的工具。

- Findutils
该软件包包含在文件系统中查找文件的程序。它被用于许多软件包的构建脚本。

- Flex
该软件包包含一个用于生成识别模式程序的工具。它是 lex（词法分析器）的 GNU 版本。

- Gawk
该软件包包含处理文本文件的程序。它是 awk（Aho-Weinberg-Kernighan）的 GNU 版本。

- GCC
该软件包是 GNU 编译器集合。它包含了 C 和 C++ 编译器以及其他非 LFS 构建的编译器。

- GDBM
该软件包包含 GNU 数据库管理器库。它被另一个 LFS 软件包 Man-DB 使用。

- Gettext
该软件包包含用于许多软件包国际化和本地化的工具和库。

- Glibc
该软件包包含主 C 库。没有它 Linux 程序将无法运行。

- GMP
该软件包包含为任意精度算术提供有用数学库。构建 GCC 需要它。

- Gperf
该软件包包含一个从键集生成完美哈希函数的程序。Eudev 需要它。

- Grep
该软件包包含用于搜索文件的程序。这些程序被大多数软件包的构建脚本使用。

- Groff
该软件包包含用于处理和格式化文本的程序。这些程序的一个重要功能是格式化帮助页。

- GRUB
该软件包是全局统一引导加载程序。它是可选启动加载程序之一，但是最灵活的。

- Gzip
该软件包包含用于压缩和解压文件的程序。它用于解压 LFS 及其它的软件包。

- Iana-etc
此包为网络服务和协议提供数据。它是启用适当网络能力所必需。

- Intutils
此包包含用于基础网络管理的程序。

- Inttool
此包包含从源文件中提取可翻译字符串的工具。

- IPRoute2
此包包含用于基础和高级 IPv4 及 IPv6 网络的程序。由于其具备 IPv6 功能，它被选择优于其他常用的工具包（net-tools）。

- Kbd
此包包含键位表文件、用于非美国键盘的键盘实用程序以及许多控制台字体。

- Kmod
此包包含管理 Linux 内核模块所需的程序。

- Less
此包包含一个非常实用的文本查看器，允许在查看文件时向上或向下滚动。它也被 Man-DB 用于查看帮助页（manpages）。

- Libcap
此包实现了对 Linux 内核中可用的 POSIX 1003.1le 权限（capabilities）的用户空间接口。

- Libelf
elutils 项目为 ELF 文件和 DWARF 数据提供了库和工具。此包中的大多数工具在其他包中可用，但使用默认（且最高效）的配置构建 Linux 内核时需要该库。

- Libfbi
此包实现了一个针对各种调用约定的可移植、高级编程接口。某些程序在编译时可能不知道要传递给函数的参数。例如，解释器在运行时被告知调用给定函数的参数数量和内容。Libfbi 可在此类程序中使用，提供从解释器到编译代码的桥梁。

- Libpipeline
Libpipeline 包包含一个以灵活且方便的方式操作子进程管道的库。它是 Man-DB 包所要求的。

- Libtool
此包包含 GNU 通用库支持脚本。它将使用共享库的复杂性封装在一个一致的、可移植的接口中。其他 LFS 包中的测试套件需要它。

- Linux Kernel
此包是操作系统本身。它是 GNU/Linux 环境中的 Linux。

- M4
此包包含一个通用的文本宏处理器，可以作为其他程序的构建工具使用。

# 从零开始 Linux - 版本 11.0

- Make
此包包含一个用于引导包构建的程序。LFS 中的几乎每个包都需要它。

- Man-DB
此包包含查找和查看帮助页的程序。由于具有卓越的国际化能力，它被用来取代 man 包。它提供了 man 程序。

- Man-pages
此包包含基础 Linux 页面的实际内容。

- Meson
此包提供了一个用于自动化构建软件的软件工具。Meson 的主要目标是尽可能地减少软件开发者在配置构建系统上花费的时间。构建 Systemd 以及许多 BLFS 包都需要它。

- MPC
此包包含用于复数算术的函数。GCC 需要它。

- MPFR
此包包含多精度算术的函数。GCC 需要它。

- Ninja
此包包含一个侧重速度的小型构建系统。它的设计旨在接收由高层构建系统生成的输入文件，并尽可能快地运行构建。LFS 中的许多包都需要它。

- Ncurses
此包包含用于处理终端无关的字符屏幕的库。它通常用于为菜单系统提供光标控制。LFS 中的许多包都需要它。

- Openssl
此包提供了与密码学相关的管理工具和库。这些工具对于为其他包（包括 Linux 内核）提供加密函数非常有用。

- Patch
此包包含一个通过补丁文件（通常由 diff 程序创建）来修改或创建文件的程序。多个 LFS 包的构建过程需要它。

- Perl
此包是运行时语言 PERL 的解释器。安装和测试若干 LFS 包时需要它。

- Pkg-config
此包提供一个可以返回已安装库或包的元数据的程序。

- Procs-NG
此包包含用于监控进程的程序。这些程序对系统管理有用，也被 LFS 启动脚本（Bootscripts）使用。

- Psmisc

# 从零开始 Linux - 版本 11

此包包含显示运行进程信息的程序。这些程序对系统管理有用。

- Python 3
此包提供了一种解释型语言，其设计哲学强调代码的可读性。

- Readline
此包是一组提供命令行编辑和历史记录能力的库。它被 Bash 使用。

- Sed
此包允许在不打开文本编辑器的情况下对文本进行编辑。大多数 LFS 包的配置脚本也需要它。

- Shadow
此包包含以安全方式处理密码的程序。

- Syslogd
此包包含记录系统消息的程序，例如内核或守护进程在发生异常事件时提供的消息。

- Sysvinit
此包提供了 init 程序，它是 Linux 系统上所有其他进程的父进程。

- Tar
此包为 LFS 中使用的几乎所有的包提供了存档和提取能力。

- Tcl
此包包含 LFS 包中许多测试套件使用的工具命令语言（Tool Command Language）。

- Texinfo
此包包含读取、写入和转换 info 页面的程序。它用于许多 LFS 包的安装过程。

- Util-linux
此包包含杂项实用程序。其中包括处理文件系统、控制台的程序。

- Vim
此包包含一个编辑器。因为它与经典的 vi 兼容且功能极其强大而被选中。如果需要，可以使用任何其他编辑器替代。

- XMLParser
此包是一个与 Expat 接口的 Perl 模块。

- XZ Utils
此包包含用于压缩和解压缩的程序。它提供了通常范围内最高的压缩率，对 LZMA 格式有用。

- Zlib

# Linux零 Scratch - 版本 11.0

- Zstd
此包包含某些程序使用的压缩和解压缩例程。

# Linux From Scratch - 版本 11.0

此格式用于封装可选的文本。

`passwd (5)`

此格式用于引用手册页（man page）。括号内的数字表示手册中的某个特定章节。例如，`passwd` 有两个手册页。根据 Linux 安装说明，两个手册页分别位于 `/usr/share/man1/passwd.1` 和 `/usr/share/man5/passwd.5`。当书籍使用 `passwd(5)` 时，它特指 `/usr/share/man5/passwd.5`。执行 `man password` 将打印它找到的第一个匹配 "passwd" 的手册页，这将是 `/usr/share/man1/passwd.1`。为此，你需要运行 `man 5` 来引用指定的页面。请注意，手册页在不同章节中没有重重复的页名。因此，通常使用 `man <程序名>` 就足够了。

# 结构

本书分为以下几个部分。

# 第一部分 - 引言

第一部分解释了关于如何进行 LFS 安装的一些重要注意事项。本部分还提供了关于书籍的元信息。

# 第二部分 - 构建准备工作

第二部分描述了如何为构建过程做准备——创建分区、下载软件包以及编译临时工具。

# 第三部分 - 构建 LFS 交叉工具链和临时工具

第三部分提供了用于构建最终 LFS 系统所需工具的说明。

# 第四部分 - 构建 LFS 系统

第四部分引导读者完成 LFS系统的构建——逐个编译并安装所有软件包、设置启动脚本并安装内核。生成的 Linux 系统是基础，可以在此基础上构建其他软件以根据需要扩展系统。在本书末尾，有一份易用的所有已安装程序、库和重要文件的参考列表。

# 第五部分 - 附录

第五部分提供了关于书籍本身的信息，包括缩写和术语、致谢、软件包依赖、LFS 启动脚本列表、书籍分发许可以及软件包、程序、库和脚本的综合索引。

# 错误列表与安全公告

用于创建 LFS 系统的软件会不断更新和增强。在 LFS 手籍发布后可能会出现安全警告和漏洞。在进行构建之前，为了检查此版本 LFS 中的包版本或指令是否需要任何修改以适应安全漏洞或其他错误，请访问 `https://www.linuxfromscratch.org/lfs/errata/11.0/`。你应该在构建 LFS 过程中注意任何显示的更改，并将其应用到书籍的相关章节。

此外，Linux From Scratch 编辑团队维护了一份在书籍发布后发现的安全漏洞列表。在进行构建之前，为了检查是否存在活跃的安全漏洞，请访问 `https://www.linuxfromscratch.org/lfs/advisories/`。在构建 LFS 系统的过程中，你应该记录任何公告并执行相应的步骤来修复任何安全漏洞。

# 第一部分. 引言

## 第 1 章 引言

### 1.1. 如何构建 LFS 系统

LFS 将通过使用已安装的 Linux 发行版（如 Debian、OpenMandriva、Fedora 或 openSUSE）来构建。这个现有的 Linux 系统（主机）将作为起点，提供必要的程序（包括编译器、链接器和 shell）用以构建新系统。在安装过程中选择“development”选项以便访问这些工具。

作为在你的机器上安装独立发行版的替代方案，你可能希望使用来自商用发行版的 LiveCD。

本书的第 2 章描述了如何创建一个新的 Linux 分区和系统。这是新的 LFS 系统将被编译和安装的地方。第 3 章解释了构建 LFS 系统需要下载哪些软件包和补丁，以及如何将它们存储在新的文件系统中。第 4 章讨论了适当工作环境的设置。请仔细阅读第 4 章，因为它解释了你在处理第 5 章及之后的内容之前可能意识到的重要问题。

第 5 章解释了如何使用交叉编译技术安装初始工具链（binutils、gcc 和 glibc），以将新工具与主机系统隔离开来。

第 6 章向你展示如何使用刚刚构建的交叉工具链交叉编译基础实用程序。

第 7 章随后进入“chroot”环境，并使用先前的工具构建构建和测试最终系统所需的额外工具。

这种将新系统从主机发行版隔离的努力似乎是过度的。关于为什么要做的完整技术解释将在“工具链技术说明”中提供。

在第 8 章中，将构建完整的 LFS 系统。chroot 环境提供的另一个优势是它允许你在构建 LFS 时继续使用主机系统。在等待软件包编译完成时，你可以像往常一样使用计算机。

要完成安装，第 9 章设置了基础系统配置，并在第 10 章设置了内核和引导加载程序。第 11 章包含了关于之后继续 LFS 体验的信息。在执行了书中的步骤后，计算机将准备好重启进入新的 LFS 系统。

这就是整个过程的简述。每个步骤的详细信息将在后续章节和软件包描述中讨论。可能看起来复杂的项目将得到澄清，当你开启 LFS 冒险之旅时，一切都会井井就位。

### 1.2. 自上一个发布以来的更新

在这一版本的 LFS 中，书籍进行了重大重组，使用的技术避免了更改主机系统，并提供了更直观的构建过程。

以下是自书籍上次发布以来进行的软件包更新列表。

升级到：

- Acl-2.3.1
- Attr-2.5.1
- Automake-1.16.4
- Bash 5.1.8
- Bc 5.0.0
- Binutils-2.37
- Bison-3.7.6
- DejaGNU-1.6.3
- Diffutils-3.8
- E2fsprogs-1.46.4
- Expat-2.4.1
- File-5.40
- GCC-11.2.0
- GDBM-1.20
- Glibc-2.34
- Grep-3.7
- GRUB-2.06
- IANA-Etc-20210611
- IPRoute-2-5.13.0
- Kmod-29
- Less-590
- Libcap-2.53
- Libelf-0.185 (from elfutils)
- Libffi-3.4.2
- Linux-5.13.12
- M4-1.4.19
- Man-pages-5.13
- Meson-0.59.1
- Openssl-1.1.11
- Perl-5.34.0
- Python-3.9.6
- Shadow-4.9
- Sysklog-1.5.1
- SysVinit-2.99
- Texinfo-6.8
- Util-Linux-2.37.2
- Vim-8.2.3337
- Zstd-1.5.0

新增：

- binutils-2.37-upstream_fix-1.patch
- gcc-11.1.0-upstream-fixes-1.patch

移除：

### 1.3. 更新日志

这是 2021 年 9 月 1 日版本的版本的 Linux From Scratch 书。如果此书较旧，请通过 `https://www.linuxfrom.org/` 检查新版本。

以下是自上次发布以来的更改列表。

日志条目：

- 2021-09-01: 升级到：
- 2021-08-25: 升级到：
- 2021-08-20: 升级到：
- 2021-08-18: 升级到：
- 2021-08-16: 升级到：
- 2021-08-15: 升级到：
- 2021-08-14: 升级到：
- 2021-08-13: 升级到：
- 2021-08-11: 升级到：
- 2021-08-10: 升级到：
- 2021-08-09: 升级到：
- 2021-08-08: 升级到：
- 2021-08-07: 升级到：
- 2021-08-06: 升级到：
- 2021-08-05: 升级到：
- 2021-08-04: 升级到：
- 2021-08-03: 升级到：
- 2021-08-02: 升级到：
- 2021-08-01: 升级到：
- 2021-07-27: 升级到：
- 2021-07-26: 修复 shadow-4.9 中的编程错误
- 2021-07-25: 添加正确剥离库的变通方法
- 2021-07-25: 在剥离期间对 Glibc NSS 模块使用变通方法以防止 bash 崩溃。

# Linux From Scratch - 版本 11

- [xry111] - 添加了安装 Binutils-2.37 手册页的解决方案。
- [bdubds] - 更新到 shadow-4.9。修复了 #4891。
- [bdubds] - 更新到 util-linux-2.37.1。修复了 #4890。
- 2021-07-23



# Linux From Scratch - 版本 11

## 2021-07-23
- [xry111] - 添加了安装 Binutils-2.37 手册页的解决方案。
- [bdubds] - 更新到 shadow-4.9。修复了 #4891。
- [bdubds] - 更新到 util-linux-2.37.1。修复了 #4890。

## 2021-07-22
- [renodr] - 更新到 meson-0.59.0。修复了 #4888。
- [renodr] - 更新到 binutils-2.37。修复了 #4887。
- [renodr] - 更新到 less-590。修复了 #4884。

## 2021-07-22
- [dj] - 修正了第 08 章 dejajnu, except, 和 tcl 中的页面 ID。
- [dj] - 确保 glibc 将 config 和 sln 安装到 `/usr/sbin`

## 2021-07-20
- [ken] - 更新到 linux-5.13.4（安全修复）。修复了 #4886。
- [xry111] - 为 tester 用户使用固定的非零 UID，并创建一个新的伪终端以满足 bash 测试套件的要求。

## 2021-07-19
- [renodr] - 在错误列表（Errata）页面添加了关于安全告的的文本。

## 2021-07-17
- [ken] - 通过在 perl 之前构建并修补 gdbm-1.20 突出的问题，修复了 perl-5.34.0 的测试失败。修复了 #4885。

## 2021-07-15
- [bdubds] - 移除了不再需要且对 m4 的修改。

## 2021-07-08
- [renodr] - 更新到 textinfo-6.8。修复了 #4880。
- [renodr] - 更新到 iproute2-5.13.0。修复了 #4879。
- [renodr] - 更新到 Python-3.9.6（安全更新）。修复了 #4878。
- [renodr] - 更新到 Linux-5.13.1。修复了 #4873。

## 2021-07-01
- [ken] - 修补 gcc 以修复某些回归问题（在 BLFS 中构建 firefox-91ESR 需要），并允许其构建 linux-5.13.0 内内核头。修复了 #4875。

## 2021-06-28
- [ken] - 如果安装单独的区域，添加 libstdc++-v3 测试中使用的 9。修复了 #4877。

## 2021-06-27
- [bdubds] - 更新到 bash-5.1.8。修复了 #4869。
- [bdubds] - 更新到 dejajnu-1.6.3。修复了 #4871。
- [bdubds] - 更新到 libcap-2.51。修复了 #4874。
- [bdubds] - 更新到 man-pages-5.1。修复了 #4876。

## 2021-06-18
- [bdubds] - 确保 libcap 安装 capsh。

## 2021-06-15
- [bdubds] - 更新到 iana-etc-202102611。解决 #4722。
- [bdubds] - 更新到 vim-8.2.3001。解决 #4500。
- [bdubds] - 更新到 util-linux-2.37。修复了 #4865。
- [bdubds] - 更新到 meson-0.58.1。修复了 #4867。
- [bdubds] - 更新到 linux-5.12.10。修复了 #4866。
- [bdubds] - 更新到 m4-1.49。修复了 #4864。
- [bdubds] - 更新到 grub-2.06。修复了 #4868。

## 2021-06-09
- [ken] 为了一致性，在 `/usr/lib` 中创建 cpp 链接。
- [ken] 将 iproute2 程序安装在 `/usr/sbin` 以保持一致性。

## 2021-06-08
- [bdubds] - 让关闭网络更具健壮。

## 2021-06-02
- [thomas] - 调整 sendskill 启动脚本以避免杀死 mdmod（如果已激活）。

## 2021-05-31
- [ken] - 更新到 linux-5.12.8（安全修复）。修复了 #4863。

## 2021-05-28
- [bdubds] - 更新到 iana-etc-20210526。解决 #4722。
- [bdubds] - 更新到 vim-8.2.2890。解决 #4500。
- [bdubds] - 更新到 zstd-1.5.0。修复了 #4858。
- [bdubds] - 更新到 perl-5.34.0。修复了 #4860。
- [bdubds] - 更新到 linux-5.12.7。修复了 #4857。
- [bdubds] - 更新到 libcap-2.50。修复了 #4862。
- [bdubds] - 更新到 kmod-29.9。修复了 #4859。
- [bdubds] - 更新到 expat-2.4.1。修复了 #4861。
- [bdubds] - 更新到 elfutils-0.185。修复了 #4855。
- [bdubds] - 更新到 bc-4.0.2。修复了 #4855。

## 2021-05-24
- [thomas] - 从 iproute2 命令中移除过时的 DOCDIR 选项。

## 2021-05-17
- [bdubds] - 调整 eudev 和 e2sprogs 的目录。感谢 Ryanaw 的报告。

## 2021-05-14
- [ken] - 添加关于 OpenSSL 的说明。

## 2021-05-12
- [bdubds] - 由于部分 LFS 环境中的无限挂起，删除了 Python。
- [renodr] - 将 LFS 移动到配置。感谢 Ruoy 完成所有工作。
- [renodr] - 更新到 gcc-11.1.0。修复了 #4847。
- [renodr] - 修复构建 glibc-2.33 时使用 gcc-11.1.0 的问题。
- [renodr] - 更新到 iproute2-5.12.0。修复了 #4852。
- [renodr] - 更新到 Python-3.9.5。修复了 #4854。
- [renodr] - 更新到 meson-0.58.0。修复了 #4853。
- [renodr] - 更新到 linux-5.12.2。修复了 #4840。

## 2021-04-28
- [bdubds] - 添加备用区域安装。修复了 #4844。
- [bdubds] - 微调启动脚本。感谢 Scott 的报告。

## 2021-04-26
- [bdubds] - 更新到 vim-8.2.2812。解决 #4500。
- [bdubds] - 更新到 iana-etc-20210407。解决 #4722。
- [bdubds] - 更新到 Python-3.9.4。修复了 #4843。
- [bdubds] - 更新到 meson-0.57.2。修复了 #4846。
- [bdubds] - 更新到 linux-5.11.16。修复了 #4840。
- [bdubds] - 更新到 less-581。修复了 #4849。
- [bdubds] - 更新到 file-5.40。修复了 #4839。
- [bdubds] - 更新到 bc-4.0.1。修复了 #4845。

## 2021-04-22
- [xry111] - 回滚 772bbc，因为建议的修复被维护者拒绝。

## 2021-04-06
- 此处的 XML 源从 SVN 迁移。

## 2021-03-26
- [renodr] - 更新到 openssl-1.1.1（安全更新）。修复了 #4838。
- [renodr] - 更新到 attr-2.5.1。修复了 #4833。
- [renodr] - 更新到 linux-5.11.10。修复了 #4834。
- [renodr] - 更新到 bc-3.3.4。修复了 #4835。
- [renodr] - 更新到 man-pages-5.11。修复了 #4836。
- [renodr] - 更新到 expat-2.3.0。修复了 #4837。
- [renodr] - 更新到 acl-2.3.1。修复了 #4832。

## 2021-03-17
- [xry111] - 使用 j1 安装 Binutils。来自 Hans Meier 的感谢。

## 2021-03-15
- [bdubds] - 更新到 vim-8.2.264。解决 #4500。
- [bdubds] - 更新到 iana-etc-20210304。解决 #4722。
- [bdubds] - 更新到 zstd-1.4.9。修复了 #4827。
- [bdubds] - 更新到 sysvisit-2.9.9。修复了 #4822。



- `[bdubds]` - 更新到 `linux-5.11.6`。修复了 `#4824`。
- `[bdubds]` - 更新到 `libcap-2.4.9`。修复了 `#4831`。
- `[bdubds]` - 更新到 `iproute2-5.11.0`。修复了 `#4823`。
- `[bdubds]` - 更新到 `e2sprogs-14.2`。修复了 `#4826`。
- `[bdubds]` - 更新到 `bison-3.7.6`。修复了 `#4828`。
- `[bdubds]` - 更新到 `bc-3.3.3`。修复了 `#4833`.

## 1.4. Resources

- [Frequently Asked Questions](https://www.linuxscratch.org/faq#generalfaq)
- [Mailing Lists](https://www.linuxscratch.org/mail.html)
- [IRC](https://irc.libera.chat)
- [Mirror Sites](https://www.linuxscratch.org/mirrors.html)
- [Search](https://www.linuxscratch.org/search.html)
- [Contact Information]

Please direct all your questions and comments to one of the mailing lists (see above).

# 1.5. Help

If an issue or a question is encountered while working through this book, please check the FAQ page at https://www.linuxscratch.org/faq#generalfaq. Questions are often answered there. If your question is not answered on this page, try to find the source of the problem. The following hint will give you some guidance for troubleshooting: https://www.linuxscratch.org/hints/downloads/files/errors.txt.

We also have a wonderful LFS community that is willing to offer assistance through the mailing lists and IRC (see the 1.4, "Resources" section of this book). However, we get several support questions every day and many of them can be easily answered by going to the FAQ and searching the mailing lists. So, for you to get the best assistance possible, you need to do some research on your first. If your searches do not produce a solution, please include all relevant information (mentioned below) in your request for help.

### 1.5.1. Things to Mention

Apart from a brief explanation of the problem being experienced, the essential things to include in any request for help are:

- The version of the book used (in this case 11.0)
- The host distribution and version being used to create LFS
- The output from the Host System Requirements script
- The package or section problem was encountered in
- The exact error message or symptom received
- Note whether you have deviated from the book at all

### 1.5.2. Configure Script Problems

If something goes wrong while running the configure script, review the config.log file. This file may contain errors encountered during configure which were not printed to the screen. Include the relevant lines if you need to ask for help.

## 1.5.3. 编译问题

屏幕输出和各种文件的内容对于确定编译问题的原因很有用。`configure` 脚本的屏幕输出和 `make` 的运行结果可能会帮助。没有包含全部输出，但要包含足够的相关信息。以下是 `make` 屏幕输出中包含信息的示例：

```
gcc -DALIASPATH="/mnt/lfs/usr/share/locale:"
-DLOCALEDIR="/mnt/lfs/usr/share/locale"
-LLDBDIR="/mnt/lfs/usr/lib"
-DINCLUDEDIR="/mnt/lfs/usr/include" -DHAVE_CONFIG_H -I. -I.
-g -o2 -c getoptl.c
gcc -g2 -static make ar arscan commands.o dir.o
expand.o file.o function.o signature.o implicit.o job.o main.o
misc.o read.me rule.o variable.o vpath.o
default.o remote-sub.version.o optl.o
-lutil job:`load_too_high`:n`/lfs/tmp/make-3.79.1/job.c:1565: undefined reference
to `getloadvay`
collect2: ld returned 1 exit status
make[2]: *** [make] Error 1
make[2]: Leaving directory `/lfs/tmp/make-3.79.1/
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory `/lfs/tmp/make-3.79.1/
make: *** [all-recursive] Error 2
```

在这种情况下，许多人只会包含底部的部分：

```
make [2]: *** [make] Error 1
```

这不足以正确诊断问题，因为只说明了发生了错误，而没有说明发生了什么错误。像上面示例那样的整个部分都应该被保存下来，因为它包含了已执行的命令以及相关的错误信息。

网上有一篇关于在网上寻求帮助的优秀文章：http://catb.org/-esr/faqs/smart-questions.html。阅读并遵循文档中的提示，可以增加获得你所需帮助的概率。

## 第二部分。准备构建

## 第 2 章.准备主机系统

### 2.1. 引言

在本章中，将检查构建 LFS 所需的主机工具并在必要时进行安装。然后准备一个用于托管 LFS 系统的分区。我们将创建分区本身，在上面创建文件系统并将其挂载。

### 2.2. 主机系统要求

你的主机系统应备有以下软件，并达到指定的最低版本。这对于大多数现代 Linux 发行版来说应该不是问题。还要注意，许多发行版会将头文件放在单独的包中，通常以“`<package-name>-devel`”或“`<package-name>-dev`”的形式存在。如果你的发行版提供了这些，请确保安装它们。

列出的软件包的早期版本可能有效，但尚未经过测试。

- Bash-3.2 (`/bin/sh` 应该是指向 bash 的符号链接或硬链接)
- Binutils-2.25 (不建议使用大于 2.37 的版本，因为尚未经过测试)
- Bison-2.7 (`/usr/bin/yacc` 应该是指向 bison 的链接或执行 bison 的小型脚本)
- Bzip2-1.0.4
- Coreutils-6.9
- Diffutils-2.8.1
- Findutils-4.2.31
- Gawk-4.0.1 (`/usr/bin/awk` 应该是指向 awk 的链接)
- GCC-6.2 包含 C++ 编译器 g++ (不建议使用大于 11.2.0 的版本，因为尚未经过测试)
- Glibc-2.11 (不建议使用大于 2.34 的版本，因为尚未经过测试)
- Grep-2.5.1a
- Gzip-1.3.12
- Linux Kernel-3.2

内核版本要求的原因是，根据开发者的建议，我们在第 5 章和第 8 章构建 glibc 时指定了该版本。udev 也要求此版本。

如果主机内核早于 3.2，你将需要内核替换为更更新的版本。有两种方法可以实现这一点。首先，如果你的 Linux 供应商提供了 3.2 或更高版本的内核包。如果是这样，你可能想要安装它。如果你的供应商没有提供接受的内核包，或者你不想安装它，你可以编译内核源码。编译内核和配置引导加载程序（假设主机使用 GRUB）的指令位于第 10 章。

- M4-1.4.10
- Make-4.0
- Patch-2.5.4
- Perl-5.8.8
- Python-3.4
- Sed-4.1.5
- Tar-1.22
- Texinfo-4.7
- Xz-5.0.0

### 重要

请注意，上述符号链接对于使用本书中的指令构建 LFS 系统是必须的。指向其他软件（如 dash、mawk 等）的符号链接可能有效，但未经过 LFS 开发团队测试或支持，并且可能需要来自指令或对某些包进行额外的补丁。

要查看你的主机系统是否具有所有适当的版本以及编译能力，请运行：

```bash
cat > version-check.sh << "EOF"
#!/bin/bash
# 列出关键工具版本的简单脚本
LC_ALL=C
bash --version | head -n1 | cut -d " " -f2
MYSH=$(readlink -f /bin/sh)
echo "/bin/sh -> $MYSH"
echo $MYSH -q bash || echo ERROR: /bin/sh does not point to bash

echo -n "Binutils: " --version | head -n1 | cut -d " " -f3
bison --version | head -n1

if [ -h /bin/yacc ]; then
echo "/yacc -> $(readlink -f /bin/yacc)"
elif [ -x /bin/yacc ]; then
echo "yacc is $(yacc --version | head -n1)"
else
echo "yacc not found"
fi

bzip2 --version 2>/dev/null | head -n1 | cut -d " " -f1
echo -n "Coreutils: "; chown --version | head -n1 | cut -d " " -f2
diff --version | head -n1
find --version | head -n1
gawk --version | head -n1

if [ -h /bin/awk ]; then
echo "/awk -> $(readlink -f /bin/awk)"
elif [ -x /bin/awk ]; then
echo "awk is $(awk --version | head -n1)"
else
echo "awk not found"
fi
EOF
```

`bash version-check.sh`

```bash
gcc --version | head -n1
g++ --version | head -n1
ld --version | head -n1 | cut -d " " -f2 # glibc version
grep --version | head -n1
gzip --version | head -n1
cat /proc/version | head -n1
m4 --version | head -n1
make --version | head -n1
patch --version | head -n1
python3 --version | head -n1
sed --version | head -n1
tar --version | head -n1
makeinfo --version | head -n1 # texinfo version
xz --version | head -n1
```

```bash
echo 'int main(){}' > dummy.c g++ -o dummy
if [ -x dummy ]; then
echo "g++ compilation OK";
else echo "g++ compilation failed"; fi
rm -f dummy.c dummy
```

## 2.3. 分阶段构建 LFS

LFS 设计在一个会话中构建。也就是说，指令假设系统在此过程中不会关闭。这并不意味着系统必须一次性完成。问题在于，如果在不同点重新启动 LFS，某些过程必须重新执行。

### 2.3.1. 第 1–4 章

这些章节在主机系统上完成。重启时，注意以下内容：

- 在第 2.4 节后以 *root* 执行的操作需要设置 LFS 环境变量。

### 2.3.2. 第 5–6 章

- 必须挂载 `/mnt/lfs` 分区。
- 这两个章节必须以 *root lfs* 执行。在这些章节的任何任务之前需要执行 `su -lfs`。这样做有将软件包安装到主机的风险，并可能使其不可用。
- 普通编译指令中的过程至关重要。如果对安装软件包有任何疑问，请删除之前解压的 tar 包，重新提取包文件，并完成该节的所有指令。

### 2.3.3. 第 7–10 章

- 必须挂载 `/mnt/lfs` 分区。

从“更改所有权”到“进入 chroot 环境”的几个操作必须由 root 用户执行，并为 root 用户设置 LFS 环境变量。进入 chroot 时，必须为 root 设置 LFS 环境变量。之后不再使用 LFS 变量。

必须挂载虚拟文件系统。可以在进入 chroot 之前或之后切换到主机终端，并以 root 身份运行第 7.3.2节“挂载并填充 `/dev`”和第 7.3.3节“挂载虚拟内核系统”。

## 2.4. 创建新分区

与大多数操作系统一样，LFS 通常安装在专用分区上。构建 LFS 系统的推荐方法是使用空分区或创建一个。

最小化系统需要一个 10 兆字节 (GB) 的分区。这足够存储所有源码 tar 包并编译软件包。然而，如果 LFS 系统旨在作为主 Linux 系统，可能可能会安装额外的软件，这将需要额外的空间。30 GB 分区是一个提供增长余的合理大小。LFS 系统本身不会占用太大空间。需要一个大分区来提供免费的临时存储以及在 LFS 完成后添加功能。此外，编译软件包需要大量的磁盘空间，这些空间在软件包安装后会被回收。

由于编译过程并不总是有足够的随机内存 (RAM)，使用一个小型磁盘分区作为交换是一个好主意。内核使用交换分区存储很少使用的数据，为活动进程留出更多内存。启动分区程序（如 `cfdisk` 或 `fdisk`），并使用命令行选项指定将创建新分区的硬盘——例如主驱动器 `/dev/sda`。如果需要，创建一个 Linux 分区和一个交换分区。如果你不知道如何使用这些程序，请参考 `cfdisk (8)` 或 `fdisk (8)`。

> 对于经验用户，其他分区方案是可能的。新的 LFS 系统可以在软件 RAID 数组或 LVM 逻辑卷上。然而，其中某些属于高级主题。这些分区方法不推荐首次 LFS 用户使用。

记住新分区的标识（例如 `sda5`）。本书将引用此 LFS 分区。还要记住分区的标识。这些名称以后将用于 `/etc/fstab` 文件。

### 2.4.1. 其他分区问题

关于系统分区的建议经常发布在 LFS 邮件列表中。这是一个高度主观的话题。大多数发行版的默认设置是使用整个硬盘，除了一个交换分区。对于 LFS 来说并不是最优的，原因有许多。它降低了灵活性，使得跨多个发行版或 LFS 构建的数据共享变得困难，备份更耗时，并可能由于文件系统结构的分配不当而浪费磁盘空间。

#### 2.4.1.1. 根分区

20 GB 的根 LFS分区（不要与 `/root` 目录混淆）对于大多数系统是一个很好的折中方案。它提供了足够的空间来构建 LFS 和大部分 BLFS，但又足够小，可以轻松创建许多分区进行实验。

## 2.4.1.2. 交换分区 (Swap Partition)

大多数发行版会自动创建交换分区。通常，建议的交换分区大小是物理内存大小的两倍，但这很少需要。如果磁盘空间有限，将交换分区保持在两个 GB，并监控磁盘交换量即可。



如果你需要 Linux 的休眠功能（挂起到磁盘），它会在关闭机器之前将 RAM 中的内容写入分区。在这种情况下，交换分区的大小至少要与 RAM 一大。交换（Swapping）永远不是什么好事。对于机械硬盘，你通常可以通过观察磁盘活动来判断系统是否正在进行交换。对于 SSD，你无法直接判断，但可以检查使用了多少空间。应尽可能地避免使用交换分区。如果交换成为常态，最佳解决方案是为你的系统购买更多内存。

## 2.4.1.3. 启动分区 (Boot Partition)

如果启动磁盘使用 GUID 分区表 (`GPT`) 进行分区，那么如果不存在该分区，则必须创建一个小的（通常为 1 MB）的分区。该分区不需要格式化，但必须可以使用 `gdisk` 供 `GRUB` 引导加载程序使用。`BIOS` 分区必须位于 `BIOS` 用于启动系统的驱动器上。这不一定与 `LFS` 根分区所在的驱动器相同。该分区的要求仅取决于分区类型。

## 2.4.1.4. 便利分区 (Convenience Partitions)

在设计磁盘布局时，还有其他不是必须但应该考虑的分区。以下列表并非详尽，但可以作为指南：

- 强烈建议。使用此分区存储内核和其他信息。为了尽量减少大磁盘可能出现潜在问题，将此分区设置为 200 兆字节就足够了。

- 强烈建议。在多个发行版或 `LFS` 构建之间共享你的 `home` 目录。其大小通常很大，取决于可用磁盘空间。

- 在 `LFS` 中，`/bin`、`/lib` 和 `/sbin` 是指向 `/usr` 中对应项的符号。对于 `LFS`，通常需要一个独立的 `/usr` 分区。如果你需要它，应该创建一个足够大的分区，以容纳系统中的所有程序和库。在这种配置下，根分区可以很小（可能只有 1 GB），它适用于无磁盘工作站（`/usr` 从远程服务器挂载）。然而，启动带有独立 `/usr` 分区的系统需要 `initramfs`（`LFS` 未涵盖）。

- 此目录对于 `LFS` 来说非常有用，当需要安装多个版本的大型包（如 Gnome 或 KDE），而无需将文件嵌入到 `/usr` 的层级结构中。如果使用，5 到 10 GB 通常足够了。

- `/tmp` – 独立的目录很罕见，但在配置轻型客户端时很有用。此分区如果使用，则不需要超过几个 GB。

- `/usr` – 这为 `LFS` 源代码文件提供一个位置并在多个 `LFS` 构建之间共享它们非常有用。它也可以用作构建 `LFS` 软件包的位置。一个 30-50 GB 的足够大的分区可以提供充足的空间。

任何在启动时自动挂载的独立分区都需要在 `/etc/fstab` 中指定。关于如何指定分区的细节将在第 10.2 节“创建 `/etc/fstab`”中讨论。

## 2.5. 在分区上创建文件系统

现在已经设置了分区，就可以创建文件系统了。`LFS` 可以任何 Linux 内核识别的文件系统，最常见的类型是 `ext3` 和 `ext4`。文件系统的选择可能很复杂，取决于文件的特性和分区的大小。例如：

- `ext2` 适用于频繁更新的小型分区，如 `/boot`。

- `ext3` 是 `ext2` 的升级版，包含一个日志，以帮助在非正常关机的情况下恢复分区状态。它通常用作通用文件系统。

- `ext4` 是 `ext` 系列分区类型的最新版本。它提供了几项新功能，包括非常大的文件 (16 TB)、纳秒时间戳以及速度改进。

其他文件系统 `FAT32`、`NTFS`、`ReiserFS`、`JFS` 和 `XFS` 用于特殊目的。关于这些文件系统的更多信息可以在 http://en.wikipedia.org/wiki/Comparison_of_file_systems 。

`LFS` 假设根系统 (`/`) 是 `ext4` 类型。要在 `LFS` 分区上创建 `ext4` 文件系统，运行：

```
mkfs -v -t ext4 /dev/<xxx>
```

将 `<xxx>` 替换为 `LFS` 分区的名称。

如果你正在使用交换分区，则不需要对其进行格式化。如果需要用此命令初始化一个新的交换分区：

```
mkswap /dev/<yy>
```

将 `<yy>` 替换为交换分区的名称。

## 2.6. 设置 $LFS 变量

在整书中，环境变量 `$LFS` 将被多次使用。你应该确保在 `LFS` 构建过程之前始终定义该变量。它应该被设置为你构建 `LFS` 系统的目录名称——我们将使用 `/mnt/lfs` 作为示例，但目录的选择由你决定。如果你在单独的分上构建 `LFS`，则该目录将是该分区的挂载点。选择一个目录位置并使用以下命令设置变量：

```bash
export LFS=/mnt/lfs
```

### 警告

上述指令假设你在整个 `LFS` 过程中不会重启计算机。如果你关闭了系统，你将需要在每次重新启动构建过程时重新挂载 `LFS` 分区，或者修改宿主系统的 `/etc/fstab` 文件以在内核启动时自动重新挂载它。例如：

| /dev/<xxx> | /mnt/lfs ext4 | defaults | 1 | 1 |

如果你使用了额外的可选分区，请务必也将它们添加进来。

如果你正在使用交换分区（swap），请确保使用 `swapon` 命令将其启用：

```
/sbin/swapon -v /dev/<zzz>
```

将 `<zzz>` 替换为交换分区的名字。

现在已经建立了一个工作场所，现在是时候下载软件包了。

# 第 3 章 软件包与补丁

## 3.1. 引言

本章包含了构建基础 Linux 系统需要下载的软件包列表。版本号对应于已知运行良好的软件版本，本书基于这些版本编写。我们强烈建议不要使用更新后的版本，因为一个版本的构建命令可能在更高版本上无法运行。最新的软件包版本可能存在需要变通解决方案的问题。这些变通方案将在本书的开发版本中开发并稳定。

下载位置并不总是可访问的。如果本书出版以来下载位置已发生变化，Google (`https://www.google.com/`) 为软件包提供了一个实用的引擎。如果搜索失败，请尝试从 `https://www.linuxscratch.org/lfs/mirrors.html#` 提供的其他替代方案下载。

下载的软件包和补丁需要存放在全书中方便访问的地方。还需要一个工作目录来解压源码并进行构建。`$LFS/sources` 可以作为存储 tar 包以及工作目录。通过使用此目录，所需的元素将位于 `LFS` 分区上，并在构建过程的所有阶段可用。

要创建此目录，请在开始下载会话之前以 *root* 身份执行以下命令：

```
mkdir -v $LFS/sources
```

将此目录设置为可写并设置粘滞位（Sticky）。“粘滞”意味着即使多个用户对目录具有写权限，也只有文件的所有者才能删除粘滞目录内的文件。以下命令将启用写入和粘滞模式：

```
chmod -v awt $LFS/sources
```

有几种方法可以获取构建 `LFS` 所需的软件包和补丁：

- *文件可以按照接下来两个节的描述单独下载。*

- 对于本书的稳定版本，可以从 `https://www.linuxscratch.org/mirrors.html` 列出的 `LFS` 镜像站之一下载所有所需文件的 tar 包。

- *可以使用下文描述的 *wget* 和 wget-list 下载文件。*

要使用 *wget* 作为 *wget* 命令的输入来下载所有软件包和补丁，请使用：

```
wget --input-file=wget-list --directory-prefix=$LFS/sources
```

此外，从 `LFS-7.0` 开始，有一个单独的文件 *md5sums*，用于在继续之前验证所有软件包是否已就绪。将该文件放在 `$LFS/sources` 中并运行：

```
pushd $LFS/sources
md5sum -c md5sums
pop
```

在通过下方列出的任何方法获取所需文件后可以使用此检查。

## 3.2. 所有软件包

下载或通过其他获取以下软件包：

### Acl (2.3.1) - 348 KB

主页：`https://savannah.ngnu.org/projects/acl`

下载：`https://download.savannah.gnu.org/releases/acl/acl-2.3.1.tar.xz`

MD5：`95ec715fe909acca7c12d3306d0f076b`

### Attr (2.5-1) - 456 KB

主页：`https://savannah.ngnu.org/projects/attr`

下载：`https://download.savannah.gnu.org/releases/attr/attr-2.5-1.tar.gz`

MD5：`ac5c5a7a0840f8f3b8cade34211f64d8`

### Autoconf (2.71) - 1,263 KB

主页：`https://www.gnu.org/software/autoconf/`

下载：`https://ftp.gnu.org/autoconf-2.71.tar.xz`

MD5：`12cfa16877fa22066337efe1a64416016`

### Autotake (1.16.4) - 1,564 KB

主页：`https://www.gnu.org/software/automake/`

下载：`https://ftp.gnu.org/automake/automake-1.16.4.tar.xz`

MD5：`88e8e68bd274ae6390a016c4d92c11267`

SHA256：`80ffa0cc9985a57e62d490972c0ae1089c5fa8f4d4c7efe5cbaea58e5085f13d66`

### Bash (5.0) - 420 KB

主页：`https://www.gnu.org/software/bash/`

下载：`https://ftp.gnu.org/bash-5.1.8.tar.gz`

MD5：`23ee6195b4731b9fd878e90ccb38`

### Binutils (2.37) - 22,390 KB

主页：`https://www.gnu.org/software/binutils/`

下载：`https://ftp.gnu.org/binutils-2.37.tar.xz`

MD5：`e789dff2976b745a348c1f27c7cb`

### Bison (3.7) - 2,566 KB

主页：`https://www.gnu.org/software/bison/`

下载：`https://ftp.gnu.org/bison-3.7.6.tar.xz`

MD5：`d61aa92e3562cbc7292004ce9617cf`

### Bzip2 (1.0.8) - 792 KB

下载：`https://www.sourcepeg.org/pub/bzip2/bzip2-1.0.8.tar.gz`

MD5：`67e0512680dc47ea773382f7500d5`

### Check (15.2) - 760 KB

主页：`https://libcheck.github.io/`

下载：`https://github.com/libcheck/releases/15.2.tar.gz`

MD5：`50caffecde5a80415b2e9c74e02`

### Coreutils (8.32) - 5,418 KB

主页：`https://www.gnu.org/software/coreutils/`

下载：`https://ftp.gnu.org/coreutils-8.32.tar.xz`

MD5：`02204269b5dbc1a93597d3566`

### DejaGNU (1.6) - 608 KB

主页：`https://www.gnu.org/software/dejagnu/`

下载：`https://ftp.gnu.org/dejagnu-1.6.tar.gz`

MD5：`6c85208c5823eba447d261522`

### Diffutils (3.8) - 1,548 KB

主页：`https://www.gnu.org/software/diffutils/`

下载：`https://ftp.gnu.org/diffutils-3.8.tar.gz`

MD5：`6a6b0f0d72acf3f289a4778c`

### E2fsprogs (14.4) - 9,298 KB

主页：`http://www.gnu.org/software/e2fsprogs`

下载：`https://downloads.sourceforge.net/project/e2fsprogs/e2fsprogs-14.4.tar.gz`

MD5：`128f5211a2f44e2fsprogs-144`

### Elfutils (185) - 973 KB

主页：`https://www.gnu.org/software/elfutils/`

下载：`https://ftp.gnu.org/elfutils-185.tar.gz`

MD5：`2b6c9359a7d3566823522`

### Evdev (3.2.10) - 916 KB

主页：`http://www.gnu.org/software/evdev`

下载：`https://ftp.gnu.org/evdev-3.2.10.tar.gz`

MD5：`50b13359a7d356682352`

### Expat (2.4) - 435 KB

主页：`https://www.gnu.org/software/expat/`

下载：`https://ftp.gnu.org/expat-2.4.tar.gz`

MD5：`a4f8b219442f57641392`

### Expect (5.4) - 618 KB

主页：`https://www.gnu.org/software/expect/`

下载：`https://ftp.gnu.org/expect-5.4.tar.gz`

MD5：`00f66851221f54447d22`

### File (5.40) - 981 KB

主页：`https://www.gnu.org/software/file/`

下载：`https://ftp.gnu.org/file-5.40.tar.gz`

MD5：`72542986c5512345678`

### Fudutils (4.8) - 1,940 KB

主页：`https://www.gnu.org/software/fudutils/`

下载：`https://ftp.gnu.org/gnu/fudutils-4.8.tar.gz`

MD5：`eefe26352211111`

### Flex (2.6) - 1,386 KB

主页：`https://www.gnu.org/software/flex/`

下载：`https://ftp.gnu.org/gnu/flex-2.6.tar.gz`

MD5：`288211111111111`

### Gawk (5.1) - 308 KB

主页：`https://www.gnu.org/software/gawk/`

下载：`https://ftp.gnu.org/gawk-5.1.tar.xz`

MD5：`7c99a7f2`

- Gzip (1.10) - 757 KB:

  主页：`https://www.gnu.org/software/gzip/`

  下载地址：`https://ftp.gnu.org/gnu/gzip/gzip-1.10.tar.xz`

  MD5 和：`69b1b221694c3394f1c537df4eee39d3`

- Iana-Etc (20210611) - 579 KB:

  主页：`https://www.iana.org/protocols`

  下载地址：`https://github.com/Mic92/iana-etc/releases/download/20210611/iana-etc-20210611.tar.gz`

  MD5 和：`f2854be572e28133fc736944844672df`

- Intutils (2.1) - 496 KB:

  主页：`https://www.gnu.org/software/inutils`

  下载地址：`https://ftp.gnu.org/gnu/inutils/inutils-2.1.tar.xz`

  MD5 和：`4e67c6d1980e57c7fd665e5c5c3c1047`

  SHA256：`01b9a4b7c3a47e6f6e8a07b6122d9ad2a24e6bf14870e9c1d660b547a222`

- Inttool (0.51.0) - 159 KB:

  主页：`https://freesktop.org/wiki/inttool`

  下载地址：`https://launchpad.net/inttool/trunk/0.51.0/download/inttool-0.51.0.tar.gz`

  MD5 和：`12e517ac2b5f7a250712ca335170f1e63`

- IPRoute2 (5.13.0) - 828 KB:

  主页：`https://www.kernel.org/pub/linux/utils/iproute2/`

  下载地址：`https://www.kernel.org/pub/linux/utils/iproute2/iproute2-5.13.0.tar.xz`

  MD5 和：`15fc3786033a173a14e180afe4cd2ecd`

- Kbd (2.4.0) - 1.095 KB:

  主页：`https://kbd-project.org/`

  下载地址：`https://www.kernel.org/pub/linux/utils/kbd/kbd-2.4.0.tar.xz`

  MD5 和：`3ac55be0096fcf7b32dcbd3cd358331380`

- Kmod (29) - 548 KB:

  主页：`https://www.kernel.org/pub/linux/utils/kernel/kmod-29.tar.xz`

  MD5 和：`e8163ac8d80697d001c8d85lac38ba0`

- Less (590) - 348 KB:



主页：https://www.greenwoodsoftware.com/less/

下载地址：https://www.greenwoodsoftware.com/less/less-590.tar.gz

MD5 和：f029087448357182fb4a50091a1172ab

- LFS-Bootscripts (20210608) - 33 KB:

  下载地址：https://www.linuxscratch.org/lfs/downloads/11.0/lfs-bootscripts-20210608.tar.xz

  MD5 和：6efd60044ad31a603a2c3c16891988

- Libpipeline (1.5.3) - 92 KB:

  主页：http://libpipeline.nongnu.org/

  下载地址：https://download.savannah.gnu.org/releases/libpipeline/libpipeline-1.5.3.tar.gz

  MD5 和：dad443d0911cf9f0f1bd90a334bc004

- Libitool (2.4.6) - 151 KB:

  主页：https://www.gnu.org/software/libitool/

  下载地址：http://ftp.gnu.org/libitool/libitool-2.4.6.tar.xz

  MD5 和：1bfcb9b923f2ce1339b4d2ce1807064aa

- Linux (5.13.12) - 116,545 KB:

  主页：https://www.kernel.org/

  下载地址：https://www.kernel.org/pub/kernel/v5.x/linux-5.13.12.tar.xz

  MD5 和：6e1728b2021ca99273f080ec644c7

  注意：Linux 内核更新相对频繁，很多时候是因为发现了安全漏洞。除非错误列表页面另有说明，否则可以使用最新的稳定内核版本。对于速度有限或带宽昂贵且希望更新 Linux 内核的用户，可以单独下载包的基础版本和补丁。这可以在次要版本内的后续补丁级别中节省一些时间或成本。

- M4 (1.4.19) - 1,617 KB:

  主页：https://www.gnu.org/software/m4/

  下载地址：http://ftp.gnu.org/gnu/m4-1.4.19.tar.xz

  MD5 和：09d0823e1426f1da2fd872df0311298d

- Make (4.3) - 2,263 KB:

  主页：https://www.gnu.org/software/make/

  下载地址：http://ftp.gnu.org/gnu/make-4.3.tar.gz

  MD5 和：fc7a67ea86ace131995b0ce83fd44

- Man-DB (2.9) - 1,665 KB:

  主页：https://www.iana.org/man-db/

  下载地址：https://download.savannah.gnu.org/releases/man-db-2.9

  MD5 和：62e23a5557b9aec2cdfaa3bcc

- Man-pages (5.13) - 1,752 KB:

  主页：https://www.kernel.org/doc/man-pages/

  下载地址：https://www.kernel.org/pub/linux/man-pages-5.13

  MD5 和：3ca2c4e86cfa26b01cb8763

- Meson (0.59.1) - 1,900 KB:

  主页：https://mesonbuild.com/

  下载地址：https://github.com/mesonbuild/releases/0.59.1

  MD5 和：9c8135ce8de2094be2f42fb5

- MPC (1.2) - 820 KB:

  主页：https://www.iana.org/mpc/

  下载地址：http://ftp.gnu.org/gnu/mpc-1.2

  MD5 和：9f16c97c25bb0f76b50274

- MPFR (4.1) - 1,490 KB:

  主页：https://www.mpfr.org/

  下载地址：https://www.mpfr.org/mpfr-4.1

  MD5 和：bdd3d5efba9cda8d35ec5bae

- Ncurses (6.2) - 3,346 KB:

  主页：https://www.gnu.org/software/ncurses/

  下载地址：https://ftp.gnu.org/ncurses-6.2

  MD5 和：e812da327b1c22a4ead432d

- Ninja (10.2) - 209 KB:

  主页：https://ninja-build.org/

  下载地址：https://github.com/ninja-build/archive/10.2

  MD5 和：6397f5c2ec3b194893af2c1

- OpenSSL (1.1.1) - 9,604 KB:

  主页：https://www.openssl.org/

  下载地址：https://www.openssl.org/source/openssl-1.1.1

  MD5 和：ac0d4387f3ba0ad71b058dd

- Patch (2.7) - 666 KB:

  主页：https://savannah.gnu.org/patch/

  下载地址：http://ftp.gnu.org/gnu/patch-2.7

  MD5 和：78ad9937e4ca1526ef1853

- Perl (5.34) - 12,580 KB:

  主页：https://www.perl.org/

  下载地址：https://www.perl.org/src/5.0/perl-5.34

  MD5 和：df7ec0653440b2dc9519d

- Pkg-config (0.2.2) - 1,970 KB:

  主页：https://www.freesktop.org/pkg-config

  下载地址：https://pkg-config.freesktop.org/releases/pkg-config-0.2.2

  MD5 和：f6e93119531736facdac0c

- Propcs (3.3.17) - 985 KB:

  主页：https://sourceforge.net/projects/procs-ng

  下载地址：https://sourceforge.net/projects/procs-ng/Files/Procs-ng-3.3.17

  MD5 和：d60613e88cc2442feb46b

- Psmic (23.4) - 362 KB:

  主页：https://github.com/psmic/psmic

  下载地址：https://sourceforge.net/projects/psmic/files/psmic/psmic-23.4

  MD5 和：8114c4d489b9530efe25

- Python (3.9.6) - 18,608 KB:

  主页：https://www.python.org/

  下载地址：https://www.python.org/ftp/python/3.9.6/Python-3.9.6

  MD5 和：ecc29a768f886e550d29dba

- Python Documentation (3.9.6) - 6,692 KB:

  下载地址：https://www.python.org/ftp/doc/3.9.6/python-3.9.6-docs-html.bz

  MD5 和：0dae29e4c38af1b61a86b

- Readline (8.1) - 2,924 KB:

  主页：https://tiswww.case.edu/php/chet/readline/

  下载地址：https://ftp.gnu.org/gnu/readline-8.1

  MD5 和：9557db5b149f5d7b37ef

- Sed (4.8) - 1,317 KB:

  主页：https://www.kernel.org/doc/sed/

  下载地址：https://ftp.gnu.org/gnu/sed-4.8

  MD5 和：3ca2c4e86cfa26

- Shadow (4.9) - 1,592 KB:

  主页：https://www.iana.org/shadow/

  下载地址：https://github.com/shadow/4.9

  MD5 和：15fc3786033a

- Syslog (1.5) - 88 KB:

  主页：https://www.iana.org/syslog/

  下载地址：https://www.iana.org/projects/syslog-1.5

  MD5 和：c705942237f

- Vinit (2.9) - 1,234 KB:

  主页：https://savannah.gnu.org/vinit/

  下载地址：https://savannah.gnu.org/releases/vinit-2.9

  MD5 和：a6b7f1e2c2

- Tar (5.34) - 2,174 KB:

  主页：https://www.gnu.org/tar/

  下载地址：https://ftp.gnu.org/gnu/tar-5.34

  MD5 和：9a08d2f7c1

- Tcl (8.6) - 3,121 KB:

  主页：https://www.tcl.org/

  下载地址：https://www.tcl.org/src/tcl8.6

  MD5 和：b5723a5557

- Udev (2017) - 11 KB:

  主页：https://www.iana.org/udev/

  下载地址：https://www.iana.org/projects/udev-2017

  MD5 和：e812da327b1

- Vim (8.2) - 5,411 KB:

  主页：https://github.com/vim/vim

  下载地址：https://github.com/vim/vim/archive/v8.2

  MD5 和：f3d7f5c2ec3

- Xz Utils (5.2.5) - 1,122 KB:

  主页：https://tukaani.org/xz/

  下载地址：https://tukaani.org/xz/xz-5.2.5

  MD5 和：aa61a2e70c1

- Zlib (1.2.11) - 457 KB:

  主页：https://www.zlib.net/

  下载地址：https://www.zlib.net/zlib-1.2.11

  MD5 和：85adefc2405

这些包的总大小：430 MB

- * Glibc FHS Patch - 2.8 KB:

下载：https://www.linuxfromscratch.org/patches/lfs/11/glibc-2.34-fhs-1.patch

MD5 和: 9a5997c3452909b1769918c759eff8a2

- * Kbd Backspace/Delete Patch - 12 KB:

下载：https://www.linuxfromscratch.org/patches/lfs/11/kbd-2.4.0-backspace-1.patch

MD5 和: f75cca1a638da6caa7d52151f7136895

- * Perl Upstream Fix Patch - 1.6 KB:

下载：https://www.linuxfromscratch.org/patches/lfs/11/perl-5.34.0-upstream_fixes-1.patch

MD5 和: fb4255b5b9ed95ee09bf1c19b8056

- * Sysvisit Consolidated Consolidated Patch - 2.4 KB:

下载：https://www.linuxfromscratch.org/patches/lfs/11/sysvisit-2.99-consolidated-1.patch

MD5 和: 4900322141d493e74020c9cf437b2cdc

这些补丁的总大小：约 194.4 KB

除了上述所需的补丁外，还有许多由 LFS 社区创建的可选补丁。这些可选补丁可以解决一些小问题或启用默认未开启的功能。欢迎随时浏览位于 https://www.linuxfromscratch.org/patches/downloads/ 的补丁数据库，并根据您的系统需求获取任何额外的补丁。

## 第 4 章 最后的准备

### 4.1. 引言

在本章中，我们将执行一些额外的任务来为构建临时系统做准备。我们将在 `$LFS` 中创建一组目录以用于安装临时工具，添加一个非特权用户以降低风险，并为该用户创建一个合适的构建环境。我们还将解释我们用于衡量 LFS 软件包构建所需的时间单位——“SBUs”（标准构建单元），并提供有关软件包测试套件的一些信息。

### 4.2. 在文件系统中创建限制的目录布局

LFS 分区的的第一项任务是创建一个受限的目录层次结构，以便第 6 章中编译的程序（如第 5 章中的 `glibc` 和 `libstdc++`）将安装在它们的最终位置。这样做是为了确保在第 8 章重新构建它们时，临时程序会被覆盖。

以 `*root*` 身份运行以下命令来创建所需的布局：

```bash
mkdir -pv $LFS/{etc,var} $LFS/{usr/{bin,lib,sbin}

for i in bin lib sbin; do
ln -sv usr $LFS/
done

case $(uname -m) in
x86_64) mkdir -pv $LFS/lib64
esac
```

> 注意
>
> 上述命令是正确的。`ln` 命令有几种语法版本，因此在报告你可能认为是错误之前，请务必检查 `info coreutils ln` 和 `man ln(1)`。

第 6 章中的程序将使用交叉编译器编译（更多细节见“工具链说明”部分）。为了将此交叉编译器与其他程序分开，它将被安装在一个特殊的目录中。创建此目录：

```bash
mkdir -pv $LFS/tools
```

### 4.3. 添加 LFS 用户

以 `root` 身份登录时，犯下一个一个错误就会损坏或破坏你的系统。因此，接下来两个章节中的软件包将以非特权用户的身份构建。你可以使用自己的名字，但为了方便设置纯洁的工作环境，请创建一个名为 `lfs` 的新用户作为组（也名为 `lfs`）的成员并在安装过程中使用该用户。以 `root` 身份执行以下命令来添加新用户：

```bash
groupadd lfs
useradd -s /bin/bash -g lfs -m -k /dev/null lfs
```

命令行选项的含义：

- `-s /bin/bash`

这使得 `bash` 成为用户 `lfs` 的默认 shell。

- `-g lfs`

此选项将用户 `lfs` 添加到 `lfs` 组。

- `-m`

这为 `lfs` 创建一个家目录。

- `-k /dev/null`

此参数通过将输入位置更改为特殊设备，防止从骨架目录（默认是 `/etc/skel`）可能复制文件。

- `lfs`

这是创建的用户的实际名称。

要登录 `lfs`（而不是在 `root` 登录后切换到用户 `lfs`，这不需要 `lfs` 用户拥有密码），请为 `lfs` 设置密码：

```bash
passwd lfs
```

通过让 `lfs` 成为目录所有者授予 `lfs` 对 `$LFS` 下所有目录的完全访问权限

```bash
chown -v lfs $LFS/*,lib,var,etc,bin,sbin,kernels
case $(uname) in in
x86_64) chown -v lfs $LFS/lib64 ;;
esac
```

如果按照建议创建了单独的工作目录，请将该目录的所有权交给用户 `lfs`：

```bash
chown -v lfs $LFS/sources
```

> 注意
>
> 在某些系统中，以下命令无法完成并将 `lfs` 用户的登录挂到后台。如果提示符 "`lfs:~`" 没有出现，输入 `fg` 命令将解决此问题。

接下来，登录 `lfs`。这可以通过虚拟控制台、显示管理器或使用以下命令创建一个新的非登录 shell 完成：

```bash
su - lfs
```

这两种 shell 之间的差异可以在 `bash` 中找到详细说明。

### 4.4. 设置环境

通过为 `bash` 创建两个新的启动文件来设置良好的工作环境。以用户 `lfs` 身份登录时，遵循以下命令创建一个新的 `.bash_profile`：

```bash
cat ~/.bash_profile << "EOF"
exec -i HOME=$HOME TERM=$PS1='\u@w$' /bin/bash
EOF
```

以 `root` 登录时，初始 shell 是登录 shell，它读取 `/etc/profile`（可能包含某些环境变量）然后是 `.bash_profile`。`exec -i/bin/bash` 将运行的 shell 替换为一个完全空的环境，除了 `HOME`、`TERM` 和 `POSIX` 变量。这确保了系统的意外环境变量泄漏到构建环境中。此处使用的实现了清洁环境的目标。非登录 shell 实例不读取、执行 `/etc/profile` 或 `.bash_profile` 内容，而是读取并执行 `.bashrc`。现在创建 `.bashrc` 文件：



```bash
cat ~/.bashrc << "EOF"
set +h
umask 022
LFS=/mnt/lfs
LC_ALL=POSIX
LFS_TGT=$(uname -m)-lfs-linux-gnu
PATH=/usr/bin
if [ ! -L /bin ]; then PATH=$bin:$PATH; fi
PATH=$LFS/tools/bin:$PATH
CONFIG_SITE=$LFS/usr/share/config.site
export LC_ALL LFS_TGT CONFIG_SITE
EOF
```

## `.bashrc` 中设置的含义：

- `set +h`

`set +h` 命令关闭 `bash` 的哈希函数。哈希通常很有有用——`bash` 使用哈希表记录执行文件的完整路径以避免搜索 `PATH`。然而，一旦安装了新工具，运行程序时 shell 将搜索 `PATH`。

- `umask 022`

将创建掩码 `umask` 设置为 `022` 可确保新创建的文件目录只有所有者可写，但任何人都可以读取和执行（假设系统使用默认模式，新文件权限为 `644`，目录为 `755`）。

- `LFS=/mnt/lfs`

`LFS` 变量应设置为所选的挂载点。

- `LC_ALL=POSIX`

`LC_ALL` 变量控制某些程序的本地化，使其遵循指定国家的约定。将 `LC_ALL` 设置为“`POSIX`”或“`C`”（两者等效）可以确保 `chroot` 环境下一切正常。

- `LFS_TGT=$(uname -m)-lfs-linux-gnu`

`LFS_TGT` 变量在编译交叉编译器和链接器时设置非默认的兼容机器描述。更多信息见“工具链技术说明”。

- `PATH=/usr/bin`

许多现代 Linux 发行版合并了 `/bin` 和 `/usr/bin`。如果是这样，第 6 章的环境 `PATH` 变量只需要设置为 `/usr/bin`。如果不是，则将以下行添加到路径：

```bash
if [ ! -L /bin ]; then PATH=$bin:$PATH; fi
```

如果 `/bin` 不是符号链接，则必须添加到 `PATH` 变量。`PATH=$LFS/tools/bin:$PATH`

将 `$LFS/tools/bin` 放在标准 `PATH` 之前，第 5 章开头的交叉编译器在安装后立即被 shell 选中。这结合关闭哈希，限制了使用主机编译器代替交叉编译器的风险。

- `CONFIG_SITE=$LFS/usr/share/config.site`

在第 5 章和第 6 章中，如果未设置此变量，配置脚本可能会从主机系统的 `/usr/share/config.site` 加载某些发行版的配置项。覆盖它以防止污染主机。

- `export ...`

虽然上述命令设置了一些变量，为了让它们在任何子 shell 中可见，我们导出了它们。

> 重要

> 几个商业发行版在 `bash` 的初始化中添加了未说明的 `/etc/bash.bashrc`。该文件有修改 `lfs` 用户环境的，可能会影响关键 LFS 软件包的构建。为了确保 `lfs` 用户的环境是清洁的，检查 `/etc/bash.bashrc` 是否存在并将其移走。以 `root` 用户身份运行：

```bash
[ ! -e /etc/bash.bashrc ] || mv -v /etc/bash.bashrc /etc/bash.bashrc.old
```

在 `lfs` 用户完成第 7 章初的任务后，你可以恢复 `/etc/bash.bashrc`（如果需要）。

注意，我们在第 8.34 节中构建的 LFS 软件包“`Bash-5.1.2`”未配置为加载或执行 `/etc/bash.bashrc`，因此该文件在完成的 LFS 系统中是没用的。

最后，为了为构建临时工具完全准备环境，`source` 刚刚创建的用户配置：

```bash
source ~/.bash_profile
```

### 4.5. 关于 SBU

许多人想提前知道每个软件包编译和安装大约需要多久。由于 Linux From Scratch 可以在许多不同的系统上构建，因此无法提供准确的时间估计。最大的软件包（`Glibc`）在最快的系统上大约需要 20 分钟，但在较慢的系统上可能需要三天。

SBU 衡量方法如下：在第 5 章中从此 `binutils` 开始编译的第一个软件包。编译该软件包所需的时间即被称为标准构建单元或 SBU。所有其他编译时间都相对于此时间表示。

# Linux From Scratch - Version 11.0

假设有一个包的编译时间为 4.5 SBU。这意味着如果一个系统编译和安装第一轮 `binutils` 需要花费 10 分钟，那么构建这个示例包大约需要 45 分钟。幸运的是，大多数构建所需时间都比 `binutils` 短。

总的来说，SBU 并不完全准确，因为它们取决于许多因素，包括宿主机系统的 `GCC` 版本。这里提供这些数值是为了对安装一个包可能所需的时间给出估算，但在某些情况下，数字差异可能高达几十分钟。

> 对于许多具有多个处理器（核心）的现代系统，可以通过设置环境变量或告诉程序可用多少个处理器来执行“并行 make”，从而缩短软件包的编译时间。例如，`Intel i5-6500 CPU` 可以通过以下方式支持四个并行进程：

```
export MAKEFLAGS='-j4'
```

或直接使用以下命令构建：

```
make -j4
```

当以这种方式使用多个处理器时，书中的 SBU 单位波动会比通常情况更大。在某些情况下，`make` 会直接失败。分析构建过程的输出将变得更加困难，因为不同进程的行是交织在一起的。如果你在构建步骤遇到问题，请切换回单处理器以正确分析错误信息。

## 6. 关于测试套件

大多数软件包都提供测试套件。为新构建的包运行测试套件是一个好主意，因为它可以提供一种“健全检查”，表明所有内容已正确编译。通过一组用例的测试套件通常证明该包的功能符合开发者的意图。然而，这并不能保证包完全 Bug。

某些测试比其他测试重要。例如，核心工具链包——`GCC`、`binutils` 和 `glibc` 的测试套件至关重要，因为它们在正常运行的系统中处于核心位置。`GCC` 和 `glibc` 的套件可能需要很长时间才能完成，尤其是在较慢的硬件上，但强烈建议运行。

> 在第 5 章和第 6 章运行测试套件是不可能的，因为程序是使用交叉编译器编译的，因此不应该在构建宿主机上运行。

`binutils` 和 `GCC` 测试套件的一个常见问题是伪终端（PTYs）耗尽。这会导致大量测试失败。这种情况可能由于几个原因，但最可能的原因是宿主机系统没有正确设置 `devpts` 文件系统。此问题在 https://linuxscratch.org/lfs/faq.html#no-ptys 有更详细的讨论。

有时测试套件会因为开发者认为非关键性的原因而失败。请查看位于 https://linuxscratch.org/lfs/build-logs/11.0/ 的日志，以验证这些失败是否在预期之中。该适用于书中的所有测试。

# 第三部分. 构建 LFS 交叉工具链和临时工具

### 重要预备材料

## 引言

这部分分为三个阶段：首先构建一个交叉编译器及其相关库；其次，使用此交叉工具链构建若干实用程序，并将它们与宿主机发行版隔离开；第三，进入交叉环境（这进一步增强了宿主机隔离性），并构建最终系统所需的其余工具。

> 重要

> 从这部分开始是构建新系统的实际工作。这需要非常的小心，确保完全按照书中所示执行指令。你应该尝试理解它们的作用，无论你多急于完成工作，都应该避免盲目地按照所示内容输入它们，而是在遇到你不理解的内容时查阅文档。此外，请记录你的输入和命令输出，使用 `tee` 工具将它们发送到文件中。这有助于在出现问题时进行更好的诊断。

下一节将给出构建过程的技术介绍，而接下来的部分包含非常重要的通用说明。

### 工具链技术说明

本节解释了整体构建方法背后的一些原理和技术细节。不需要立即理解本节的所有内容。在执行实际构建后，大部分信息将变得更加清晰。在过程中可以随时参考本节。

第 5 章和第 6 章的总目标是提供一个临时区域，其中包含一组已知良好的工具，这些工具可以与宿主机系统隔离。通过使用 `chroot`，后续章节中的命令将被包含在该环境中，确保 LFS 系统进行清洁、无故障的构建。构建过程的设计旨在最大限度地减少新读者的风险，同时提供最大的教育价值。

构建过程基于交叉编译过程。交叉编译通常用于为与构建机器不同的机器构建编译器及其工具链。对于 LFS 来说，这并非必须，因为运行新系统的机器与用于构建的机器是同一台。但交叉编译具有巨大的优势，即交叉编译不依赖于宿主机环境。

#### 关于交叉编译

交叉编译涉及一些值得单独成章的概念。虽然在初读时可能会省略这一节，但强烈建议稍后回来，以全面掌握构建过程。

让我们定义一下该背景下使用的术语：

- **build（构建机）**：我们构建程序的机器。注意，该机器在其他章节中被称为“host”（宿主机）。

- **host（宿主机）**：运行构建程序的机器/系统。注意此处“host”的用法不同。

- **target（目标机）**：为之构建程序的机器。例如，`Intel i5-6500 CPU` 可以通过以下方式支持四个并行进程：

```
export MAKEFLAGS='-j4'
```

或直接使用：

```
make -j4
```

当以这种方式使用多个处理器时，书中的 SBU 单位波动比通常情况更大。在某些情况下，`make` 会直接失败。分析构建过程的输出将变得更加困难，因为不同进程的行是交织在一起的。如果你在构建步骤遇到问题，请切换回单处理器以正确分析错误信息。

Linux From Scratch - Version 11.0

交叉编译具有巨大的优势，即交叉编译不依赖于宿主机环境。

示例中，让我们假设如下：

| 阶段 | 构建机 | 宿主机 | 目标机 | 操作 |
| --- | --- | --- | --- | --- |
| 1 | A | A | B | 使用 `cc1` 构建交叉编译器 |
| 2 | A | B | C | 使用 `cc1` 构建编译器 |
| 3 | B | C | C | 使用 `cc2` 构建交叉编译器 |
| 4 | C | C | C | 在 C 上重建并测试 `cc-lfs` |

### 交叉编译的实现

#### 注意

几乎所有的构建系统都使用 CPU-厂商-操作系统作为机器名称。敏锐的读者可能会疑惑为什么三元组是指由四个组件组成。原因是：最初，三个组件名称就足够，但随着新机器和系统的出现，这证明是不够的。确定机器三元组的简单方法是许多软件包的 `config.guess` 脚本。解压 `binutils` 源码并运行脚本：`./config.guess` 并记录输出。例如，对于 32 位 Intel 处理器，输出将为 `i686-linux-gnu`。在 64 位系统上将是 `x86_64-linux-gnu`。

此外，请注意动态链接器的名称，通常称为动态加载器（不要与二进制文件中的标准链接器混淆）。由 `Glibc` 提供的动态链接器查找并加载程序所需的共享库，准备程序运行并运行它。32 位机器的动态链接器名称将为 `ld-linux.so.2`（64 位系统为 `ld-linux-x86-64.so.2`）。确定动态链接器名称的安全方法是检查宿主机系统上的随机二进制文件，运行：`readelf -1 <二进制文件名> | grep interpreter` 并记录输出。涵盖所有平台的权威参考位于 `Glibc` 源码根目录下的 `shlib-versions` 文件中。

现在，涉及到更多的交叉编译：C 语言不仅仅是一个编译器，它还定义了一个标准库。在本书中使用了 GNU C 库，即 `glibc`。该库必须为目标机器进行编译，即使用交叉编译器 `gcc`。但编译器使用一个内部库，来实现汇编指令无法提供的复杂函数。这个内部库是 `libibc`，必须链接到 `glibc` 库才能发挥完整功能！此外，C++ 的标准库 (`lib++`) 也需要链接到 `glibc`。由于这个“有鸡还是有蛋”的问题，首先要构建一个精简版的 libc（缺少线程和异常处理等功能），然后使用这个精简版的 `glibc` 构建 `glibc`（`glibc` 本身不是精简的），接着是构建 `libstdc++`。但这个库将缺少与 `glibc` 相同的功能。

故事还没有结束：前一段的结论是，构建功能完整的 `lib++` 需要 `gcc`，但在第 2 阶段，这是构建 C/C++ 库的唯一可用编译器！事实上，第 2 阶段构建的编译器 `cc-fs` 能够构建这些库，但（1）`GCC` 的构建系统不知道它可以在目标机器上运行，且（2）在 pc 上使用它会有链接到 pc 库的风险，因为 `cc-fs` 是一个原生编译器。因此，我们稍后在此构建 `libstdc++`。

### 其他过程细节

交叉编译器将安装在 `$LFS/tools` 目录，因为它不是最终系统的一部分。

首先安装 `Binutils` 是因为 `GCC` 和 `Glibc` 的 `configure` 运行都会对汇编器和链接器执行各种特性测试，以确定启用或禁用哪些特性。这比人们想象的要重要得多。配置不当的 `GCC` 可能导致工具出现细微损坏，这种损坏的影响可能直到发行版构建结束时才会显现。测试套件会在执行过多额外工作之前突出此错误。

`Binutils` 按顺序安装其汇编器和链接器：`$LFS/tools/bin` 和 `$LFS/$FS_TGT/bin`。其中一个目录中的工具链接到另一个。链接器的一个重要因素是它的库搜索顺序。可以通过向 `ld` 传递 `--verbose` 标志获取详细信息。例如，`$LFS_TGT-ld --verbose` 将阐明当前的搜索路径和顺序。它显示了通过编译一个虚拟程序并向链接器传递 `--verbose` 开关，`ld` 链接了哪些文件。例如，`$LFS_TGT-gcc dummy.c -Wl,--2>&1 | grep` 将显示链接期间成功打开的文件。

下一个包是安装 `glibc`。运行期间可以看到的示例是：

```
checking assembler to use... /mnt/lfs/tools/i686-lfs-linux-gnu/bin
checking linker to use... /mnt/lfs/tools/i686-lfs-linux-gnu/bin/bin
```

这是由于上述原因。`configure` 脚本不会搜索 `PATH` 目录来寻找要使用的工具。然而，在 `gcc` 本身的实际操作过程中，并不一定使用相同的搜索路径。要确定 `gcc` 将使用哪个库，可以运行 `$LFS_TGT-gcc -print`。

可以在编译虚拟程序时通过传递 `--command line` 选项从 `gcc` 获取详细信息。例如，`gcc -v dummy.c` 将显示关于预处理器、编译器和汇编阶段的详细信息，包括搜索路径和顺序。

接下来安装经过清理的 Linux API 头文件。这些允许标准 C 库 (`Glibc`) 与 Linux 内核提供的功能建立接口。

安装的下一个包是 `Glibc`。构建 `Glibc` 最重要的考虑因素是编译器、二进制工具和内核头文件。编译器通常不是问题，因为 `Glibc` 总是会使用与其 `configure` 脚本中的 `--host` 参数相关的编译器；例如，在某种情况下，编译器将是 `$LFS_TGT-gcc`。二进制工具和内核头文件可能会复杂一些。不要冒险，使用可用开关来强制执行正确的选择。运行 `configure` 后，检查构建目录中 `config.file` 的内容以获取所有重要细节。注意使用 `CC="$LFS_TGT-gcc"`（已扩展 `$LFS_TGT`）来控制使用哪些二进制工具，以及 `-nostdinc -isystem` 标志来控制编译器的搜索路径。这些项目突出了 `Glibc` 包的一个重要方面——它在构建机制方面非常自给自足，通常不依赖于默认值。

最后，接下来编译标准 C++ 库，随后在第 6 章中构建所有需要自身构建的程序。所有包的安装步骤都使用 `DESTDIR` 变量将程序放入 LFS 文件系统。

第 6 章结束时安装了原生 LFS 编译器。首先构建 `binutils-pass2`，使用与其他程序相同的 `DESTDIR`；构建 `GCC` 的第二阶段，省略了 `libstdc++` 和其他不重要的库。由于 `GCC` `configure` 脚本中的某些奇怪逻辑，当主机与目标相同但与系统不同时，`CC_FOR_TARGET` 为空。这就是为什么将 `CC_FOR_TARGET=$LFS_TGT-gcc` 显式放入 `configure` 选项中。

在第 7 章进入 `ch` 环境后，第一个任务是安装 `libstdc++`。对工具链正常运行所需的程序进行临时安装。从现在开始，核心工具链是自包含且自托管的。在第 8 章中，将构建、测试并安装功能完整系统所需的全部包的版本。

### 通用编译说明

在构建包时有以下几个假设：

- 若干包在编译前经过补丁处理，但仅在需要时进行。补丁顺序在本章及后续章节中均有体现，有时位于一起。因此，如果补丁指令似乎缺失，请不要担心。

- 在许多包的编译期间，屏幕上会有多个警告滚过。这些是正常的，可以忽略。这些警告是关于 C 或 C++ 语法的过时而非无效用法。标准经常变化，某些包仍使用旧标准。这不是问题，但会引起警告。

- 最后一次检查 `LFS` 变量是否已正确设置：

```
echo $LFS
```

确保确保输出路径指向 LFS 挂载点，以我们的示例 `/mnt/lfs` 为例。

**重要**

构建说明假设主机系统要求（包括符号链接）已正确设置：

- `bash` 是正在使用的 shell。

- `sh` 是指向 `bash` 的符号链接。

- `/usr/bin/awk` 是指向 `gawk` 的符号链接。

- `/usr/bin/yacc` 是指向 `yacc` 的符号链接或执行 `bison` 的小型脚本。

再次强调构建过程：

1. 将所有源码和补丁放在从 `chroot` 环境可以访问的目录中，例如 `/mnt/lfs/sources`。

2. 进入源码目录。

3. 针对每个包：

   a. 使用 `tar` 程序提取要构建的包。在第 5 章和第 6 章中，确保您以 `lfs` 用户身份提取包。

   b. 进入提取包时创建的目录。

   c. 遵循书籍构建该包的指令。

   d. 返回源码目录。

   e. 删除提取的源码目录，除非另有说明。



## 5.2. Binutils-2.37 - 第一次编译

Binutils 软件包包含一个链接器、一个汇编器以及处理目标文件的其他工具。

近似编译时间：1 SBU

所需磁盘空间：602 MB

### 5.2.1. 安装交叉编译的 Binutils

+ 注意

请返回并重新阅读“通用编译指令”章节中的注意事项。理解标记为**important（重要）**的注释可以帮助你避免后续的问题。

Binutils 必须是第一个编译的包，这一点非常重要，因为 Glibc 和 GCC 都会对可用的链接器和汇编器进行各种测试，以确定启用它们的哪些功能。

Binutils 文档建议在专用目录中构建 Binutils：

```bash
mkdir -v build
cd build
```

+ 注意

为了使书中后续列出的 SBU 值具有参考价值（包括第一次安装），请测量从配置开始构建此包所需的时间。要实现这一点，请将命令包装在 `time` 命令中，例如：`time { ..configure ... make && make install; }`

现在为编译 Binutils 准备工作：

```bash
--prefix=$LFS/tools \
--with-sysroot=$LFS \
--target=$LFS_TGT \
--disable-nls \
--disable-werror
```

配置选项的含义：

`--prefix=$LFS/tools`

这告诉 `configure` 脚本准备将 binutils 程序安装到 `$LFS/tools` 目录。

`--with-sysroot=$LFS`

对于交叉编译，这告诉构建系统在需要时在 `$LFS` 中查找目标系统库。

`--target=$LFS_TGT`

由于变量 `$LFS_TGT` 中的机器描述与 `config.guess` 脚本返回的值略有不同，此开关将告诉 `configure` 脚本调整 binutils 的构建系统以构建交叉链接器。

`--disable-nls`

这禁用国际化，因为临时工具不需要 i18n。

`--disable-werror`

这防止构建在宿主机编译器出现警告时停止。

继续编译该包：

```bash
make
```

安装该包：

```bash
make install -j1
```

make 参数的含义：

```bash
-j1
```

构建系统中的某些问题可能导致在 `MAKEFLAGS` 中使用 `-j N` 时安装失败。覆盖它以绕过此问题。

关于此包的详情请参见第 8.18.2 节，“Binutils 内容”。

## 5.3. GCC-11.2.0 - 第一次编译

GCC 软件包包含 GNU 编译器集，包括 C 和 C++ 编译器。

近似编译时间：12 SBU

所需磁盘空间：3.4 GB

GCC 需要 GMP、MPFR 和 MPC 包。由于这些包可能未包含在宿主机，它们中，它们它们一起构建。将每个包解压到 GCC 源码目录并重命名生成的目录，以便 GCC 构建能够自动使用它们：

> 注意

对本章存在许多误解。操作步骤与之前的任何其他章节（包构建指令）相同。首先从源码目录提取 gcc tar 包，然后进入该目录。只有在此之后才按照指令操作。

```bash
tar -xf ../mpfr-4.1.0.tar.xz
mv -v mpfr-4.1.0 mpfr
tar -xf ../gmp-6.2.1.tar.xz
mv -v gmp-6.2.1 gmp
tar -xf ../mpc-1.2.1.tar.gz
mv -v mpc-1.2.1 mpc
```

在 x86_64 宿主机上，将 64 位库的默认目录名设置为“lib64”：

```bash
case $(uname -m) in
x86_64)
sed -e '/m64=/s/lib/lib64/' -i.orig gcc/config/linux.c;
esac
```

GCC 文档建议在专用目录中构建 GCC：

```bash
mkdir -v build
cd build
```

为编译准备 GCC：

```bash
./configure \
--target=$LFS_TGT \
--prefix=$LFS/tools \
--with-glibc-version=2.11 \
--with-sysroot=$LFS \
--with-newlib \
--without-headers \
--enable-initfini-array \
--disable-nls \
--disable-shared \
--disable-multilib \
--disable-decimal-float \
--disable-threads \
--disable-libatomic \
--disable-gomp \
--disable-libquadmath \
--disable-libsssp \
--disable-libvtv \
--disable-libstdcxx \
--enable-languages=c,c++
```

选项的含义：

`--with-glibc-version=2.11`

此选项确保软件包与宿主机的 glibc 兼容。它设置为宿主机系统要求的最低 glibc 版本。

`--with-newlib`

由于还没有可用的 C ，这确保在构建 libgcc 时定义 `inhibit_lib`常量。这防止编译任何需要 lib 支持的代码。

`--without-headers`

创建完整的交叉编译器时，GCC 需要与目标系统兼容的标准头。对于我们的目的，不需要这些头文件。此开关阻止 GCC 查找它们。

`--enable-initfini-array`

此开关强制使用构建交叉编译器时无法检测的一些内部数据结构。

`--disable-shared`

此开关强制 GCC 静态链接其内部库。我们需要这样做，因为标准库需要 glibc，而目标系统尚未安装它。

`--disable-multilib`

在 x86_64 上，LFS 不支持 multilib 配置。此开关对 x86 是无害的。

`--disable-decimal-float`, `--disable-libatomic`, `--disable-gomp`, `--disable-libquadmath`, `--disable-libsssp`, `--disable-libvtv`, `--disable-libstdcxx`

这些开关分别禁用了十进制浮点扩展、线程、libgomp、libquadmath、libsssp、libvtv 以及 C++ 标准库。这些功能在构建交叉编译器时会编译失败，且对于所需的必需。

`--enable-languages=c,c++`

此选项确保只构建 C 和 C++ 编译器。

## 5.5. Glibc-2.34

Glibc 包包含主 C 语言库。该库为内存分配、目录搜索、打开和关闭文件、读写文件、字符串处理、模式匹配、算术等提供了基础例程。

**估计编译时间：** 4.2 SBU

所需的磁盘空间：744 MB

### 5.5.1. 安装 Glibc

首先，为符合 LSB 兼容性创建一个符号链接。此外，对于 x86_64，创建一个动态库加载器正常运行所需的兼容性符号链接：

```bash
case $(uname -m) in
i386)      ln -sfv ../lib/ld-linux.so.2 $LFS/lib/ld-linux.so
      ;
x86_64)  ln -sfv ../lib/ld-linux-x86-64.so.2 $LFS/lib64
           ln -sfv ../lib/ld-linux-x86-64.so.2 $LFS/lib64/ld-linux-x86-64.so.3
      ;
esac
```

某些 Glibc 程序使用不符合 FHS 的 `/var/db` 目录来存储其运行时数据。应用以下补丁使这些程序将运行时数据存储在符合 FHS 的位置：

```bash
patch -Np1 -i ../glibc-2.34-fhs-1.patch
```

Glibc 文档建议在专门的构建目录中编译 Glibc：

```bash
mkdir -v build
cd build
```

确保 `ldconfig` 工具安装到 `/usr/sbin:` 中：

```bash
echo "rootsbindir=/usr/sbin" > configparms
```

接下来，为编译 Glibc 做准备：

```bash
./configure \
  --prefix=/usr-$TGT \
  --host=$LFS_TGT \
  --build=$(../scripts/config.guess) \
  --enable-headers=$LFS/usr/include \
  --with-libc_vslibdir=/usr/lib
```

configure 选项的含义：

`host=$LFS_TGT`, `--build=$(../scripts/config.guess)`

这些开关的组合效果是 Glibc 的系统构建配置自己为交叉编译，使用 `$LFS/tools` 中的交叉链接器和交叉编译器。

`--enable-kernel=3.2`

这告诉 Glibc 编译支持 3.2 及更高版本 Linux 内核的二进制文件。未启用针对旧内核的变通方法。

`--with-headers=$LFS/usr/include`

这告诉 Glibc 针对新安装到 `$LFS/usr/include` 目录的头文件进行编译，这样它就能确切知道内核包含的内容并据此进行自身优化。

`libc_cv_slicer=/usr/lib`

这确保该库在 64 位机器上安装在 `/usr/lib` 中，而不是默认的 `/lib64`。

在此阶段，会出现以下警告：

```
configure: WARNING:
*** 这些辅助程序缺失或
*** 版本不兼容: msgfmt
*** 某些将被禁用。
*** 请检查 INSTALL 文件所需的版本。
```

缺失或不兼容的 `msgfmt` 程序通常是无害的。该 `msgfmt` 程序是 Gettext 包的一部分，主机发行版应该提供该包。

> 注意

有报告显示，该包在以“并行编译 (parallel make)”模式构建时可能会失败。如果发生这种情况，请使用 "-j1" 选项重新运行 `make` 命令。

编译包：

```bash
make
```

安装包：

> 警告

如果 LFS 未正确设置，且尽管有建议，你以 root 身份进行构建，下一个命令会将新构建的 glibc 安装到你的主机系统，这可能导致其无法使用。在运行以下命令之前，双击环境已正确设置。

```bash
DESTDIR=$LFS install
```

make install 选项的含义：

`DESTDIR=$LFS`

`DESTDIR` make 变量几乎被所有包用于定义包安装的位置。如果没有设置，它默认到根目录 `/`。在这里我们指定安装在 `$LFS`，这在执行第 7.4 节“进入 chroot 环境”后将成为根目录。

修复 `ldd` 脚本中硬编码的可执行文件路径：

```bash
sed '/RTLDLIST=/s@/usr@@' -i $LFS/usr/bin/ldd
```

### 注意

此时，必须停止并确保新工具链的基本功能（编译和链接）按预期工作。进行健全检查，运行以下命令：

```bash
echo 'int main(){}' dummy.c
$LFS_TGT-gcc dummy.c
readelf -l a.out | grep '/ld-linux'
```

如果一切运行正常，则不应有错误，最后一个命令的输出将具有如下形式：

```
[Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
```

注意，对于 32 位机器，解释器名称将是 `/lib/ld-linux.so`。

（此处原文中存在大量重复内容，已根据翻译要求过滤并保留核心逻辑）

## 第 6 章 交叉编译临时工具

### 6.1. 引言

本章展示了如何使用刚刚构建的交叉工具链交叉编译基本实用。这些工具被安装到它们的最终位置，但尚无法使用。基本任务仍然依赖于主机的工具。然而，在链接时会使用已安装的库。在下一节进入“chroot”环境后，可以使用这些工具。但在在本章中构建的所有包必须在执行该操作之前完成。因此，我们现在无法独立于主机系统。

### 6.2. M4-1.4.19

M4 包包含一个宏处理器。

估计编译时间：0.2 SBU

所需的磁盘空间：32 MB

### 6.2.1. 安装 M4

为编译 M4 做准备：

```bash
./configure --prefix=/usr \
--host=$LFS_TGT \
--build=$(build-aux/config.guess)
```

编译包：

```bash
make
```

安装包：

```bash
make DESTDIR=$LFS install
```

此包的详情位于第 8.12.2 节，“Contents of M4.”

## 6.3. Ncurses-6.2

Ncurses 软件包包含了用于终端无关的字符屏幕处理的库。

预计编译时间：0.7 SBU

所需的磁盘空间：48 MB

### 6.3.1. 安装 Ncurses

首先，确保在配置期间首先找到 gawk：

```
sed -i s/mawk// configure
```

然后，运行以下命令在构建宿主机上构建 “tic” 程序：

```
mkdir build
pushd build
../configure
make -C include
make -C progs tic
popd
```

为编译准备好 Ncurses：

```bash
./configure --prefix=$usr /
--host=$LFS_TGT /
--build=$(./config.guess) /
--mandir=/usr/share/man /
--with-manpage-format=normal /
--with-shared /
--without-debug /
--without-ada /
--without-normal /
--enable-widec /
```

新 configure 选项的含义：

- `--with-manpage-format=normal`

  这可以防止 Ncurses 安装压缩的帮助页，如果宿主机发行版本身压缩了帮助页，可能会发生这种情况。

- `--without-ada`

  这确保 Ncurses 不支持为 Ada 编译器进行构建，该编译器可能存在于宿主机，但在我们进入 chroot 环境时将不可用。

- `--enable-widec`

  这将构建宽字符库（例如 `libcursesw.so.6.2`）而不是普通库（例如 `libcurses.so.6.2`）。这些宽字符库在多字节和传统的 8 位本地语言中均可用，而普通库仅在 8 位本地语言中工作。宽字符库和普通库在源码上兼容，但在二进制上不兼容。

- `--without-normal`

  此开关禁用构建和安装大部分静态库。

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS TIC_PATH=$(pwd) /build/progs/tic install
echo "INPUT(-lncursesw)" > $LFS/usr/lib/libncurses.so
```

安装选项的含义：

`TIC_PATH=$(pwd) /build/progs/tic`

我们需要将刚刚构建的 tic 路径传递给构建机器运行，这样就可以无错误地创建终端数据库。

`echo "INPUT(-lncursesw)" > $LFS/usr/lib/libncurses.so`

我们将构建的几个软件包需要 `libncurses.so` 库。我们创建了这个小的链接脚本，因为这是第 8 章中执行的操作。

关于此软件包的详情位于第 8.28.2 节，“Ncurses 的内容”。

## 6.4. Bash-5.1.8

Bash 软件包包含了 Bourne-Again Shell。

预计编译时间：0.4 SBU

所需的磁盘空间：64 MB

### 6.4.1. 安装 Bash

为编译准备 Bash：

```bash
./configure --prefix=/usr \
  --build=$(support/config.guess) \
  --host=$LFS_TGT \
  --without-bash-malloc
```

configure 选项的含义：

```
--without-bash-malloc
```

此选项禁用了 Bash 的内存分配（malloc）函数，该函数已知会导致段错误。通过关闭此选项，Bash 将使用更稳定的 Glibc 的 malloc 函数。

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

为使用 sh 作为 shell 的程序创建一个链接：

```
ln -sv bash $LFS/bin/sh
```

关于此软件包的详情位于第 8.34.2 节，“Bash 的内容”。

## 6.5. Coreutils-8.32

Coreutils 软件包包含了显示和设置基本系统特征的工具。

预计编译时间：0.6 SBU

所需的磁盘空间：151 MB

### 6.5.1. 安装 Coreutils

为编译准备 Coreutils：

```bash
./configure --prefix=$usr \
--host=$LFS_TGT \
--build=$(build-aux/config.guess) \
--enable-install-program=hostname \
--enable-install-program=kill uptime
```

configure 选项的含义：

- `--enable-install-program=hostname`

启用 `hostname` 二进制文件的构建和安装——它默认是禁用的，但 Perl 测试套件需要它。

编译软件包：



```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

将程序移动到最终预期位置。虽然在这个环境中并非必要，但我们必须这样做，因为某些程序硬编码了位置：

```bash
mv -v $LFS/usr/bin/chroot $LFS/sbin
mkdir -p $LFS/share/man/man8 $LFS/share/man/man8
mv -v $LFS/share/man/man1/chroot.1 $LFS/share/man/man1/
sed -i 's/"8"/'
```

关于此软件包的详情位于第 8.53 节，“Coreutils 的内容”。

## 6.6. Diffutils-3.8

Diffutils 软件包包含了显示文件或目录差异的程序。

预计编译时间：0.2 SBU

所需的磁盘空间：28 MB

### 6.6.1. 安装 Diffutils

为编译准备 Diffutils：

```bash
./configure --prefix=/usr --host=$LFS_T
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.55 节，“Diffutils 的内容”。

## 6.7. File-5.40

File 软件包包含了确定给定文件或文件类型的工具。

预计编译时间：0.2 SBU

所需的磁盘空间：31 MB

### 6.7.1. 安装 File

构建宿主机上的 file 命令需要与我们正在构建的版本相同。运行以下命令进行构建：

```bash
mkdir build
pushd build
  ./configure --disable-bzlib \
  --disable-libccomp \
  --disable-xzlib \
make
pop
```

新 configure 选项的含义：

- --disable-*

配置脚本尝试使用宿主机某些软件包。如果存在库文件但不存在相应的头文件，可能会导致编译失败。这些选项防止使用宿主机不需要的功能。

为编译准备 File：

```bash
./configure --prefix=/usr --host=$LFS_TGT --build=$(./config.guess)
```

编译软件包：

```bash
make FILE_COMPILE=$(pwd) /build/src/file
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.10 节，“File 的内容”。

## 6.8. Findutils-4.8.0

Findutils 软件包包含了查找文件的程序。这些程序用于递归搜索目录树以及创建、维护和搜索数据库（如果最近没有更新数据库，则不可靠）。

预计编译时间：0.2 SBU

所需的磁盘空间：40 MB

### 6.8.1. 安装 Findutils

为编译准备 Findutils：

```bash
./configure --prefix=/usr \
--localstatedir=/var/lib \
--host=$LFS_TGT \
--build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.57 节，“Findutils 的内容”。

## 6.9. Gawk-5.1.0

Gawk 软件包包含了处理文本文件的程序。

预计编译时间：0.2 SBU

所需的磁盘空间：43 MB

### 6.9.1. 安装 Gawk

```bash
sed -i 's/extras//*' Makefile.in
```

为编译准备 Gawk：

```bash
./configure --prefix=/usr \
--host=$LFS_TGT \
--build=$(./config.guess)
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.56 节，“Gawk 的内容”。

## 6.10. Grep-3.7

Grep 软件包包含了搜索文件内容的程序。

预计编译时间：0.2 SBU

所需的磁盘空间：25 MB

### 6.10.1. 安装 Grep

为编译准备 Grep：

```bash
./configure --prefix=/usr \
--host=$LFS_TGT
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.33 节，“Grep 的内容”。

## 6.11. Gzip-1.10

Gzip 软件包包含了压缩和解压缩文件的程序。

预计编译时间：0.1 SBU

所需的磁盘空间：10 MB

### 6.11.1. 安装 Gzip

为编译准备 Gzip：

```bash
./configure --prefix=/usr --host=$LFS_TGT
```

编译软件包：

```
make
```

安装软件包：

```bash
make DESTDIR=$LFS install
```

关于此软件包的详情位于第 8.60 节，“Gzip 的内容”。

## 6.12. Make-4.3

Make 软件包包含一个程序，用于从源文件控制包的可执行文件和其他非源文件的生成。

预计编译时间：0.1 SBU

所需磁盘空间：15 MB

### 6.12.1. 安装 Make

为编译准备 Make：

```
./configure --prefix=/usr \
--without-guile \
--host=$LFS_TGT \
--build=$(build-aux/config.guess)
```

新 configure 选项的含义：

- --without-guile

  尽管尽管我们正在进行交叉编译，但如果 configure 在构建宿主机上找到 guise，它会尝试使用它。这会导致编译失败，因此此开关可以防止使用它。

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.64.2 节，“Make 的内容”。

## 6.13. Patch-2.7.6

Patch 软件包包含一个程序，用于通过应用通常由 diff 程序创建的“patch”文件来修改或创建文件。

预计编译时间：0.1 SBU

所需磁盘空间：12 MB

### 6.13.1. 安装 Patch

为编译准备 Patch：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.65.2 节，“Patch 的内容”。

## 6.14. Sed-4.8

Sed 软件包包含一个流编辑器。

预计编译时间：0.1 SBU

所需磁盘空间：20 MB

### 6.14.1. 安装 Sed

为编译准备 Sed：

```
./configure --prefix=/usr \
--host=$LFS_TGT
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.29.2 节，“Sed 的内容”。

## 6.15. Tar-1.34

Tar 软件包提供了创建 tar 存档以及执行各种归档操作的能力。Tar 可用于之前创建的归档以提取文件、存储额外文件，或者更新或列出已存储的文件。

**预计编译时间：** 0.2 SBU

**所需磁盘空间：** 38 MB

### 6.15.1. 安装 Tar

为编译准备 Tar：

```
./configure --prefix=/usr \
  --host=$LFS_TGT \
  --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.66.2 节，“Tar 的内容”。

## 6.16. Xz-5.2.5

Xz 软件包包含压缩和解压缩文件的程序。它提供了对 Lma 和较新的 xz 压缩格式的支持。使用 **xz** 压缩文件得到的压缩率比使用传统的 **gzip** 或 **bzip2** 命令更好。

**预计编译时间：** 0.1 SBU

**所需磁盘空间：** 15 MB

### 6.16.1. 安装 Xz

为编译准备 Xz：

```
./configure --prefix=/usr \
--host=$LFS_TGT \
--build=$(build-aux/config.guess) \
--disable-static \
--docdir=/usr/share/doc/xz-5.2.5
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.8.2 节，“Xz 的内容”。

## 6.17. Binutils-2.37 - Pass 2

Binutils 软件包包含一个链接器、一个汇编器以及处理其他文件的工具。

预计编译时间：1.3 SBU

所需磁盘空间：505 MB

### 6.17.1. 安装 Binutils

再次创建一个独立的构建目录：

```
mkdir -v build
cd build
```

为编译准备 Binutils：

```bash
../configure /\
--prefix=/usr \
--build=$(../config.guess) \
--host=$LFS_TGT \
--disable-nls \
--enable-shared \
--disable-werror \
--enable-64-bit-bfd /
```

新 configure 选项的含义：

- --enable-shared

  将 libbfd 构建为共享库。

- --enable-64-bit-bfd

  启用 64 位支持（在字长位较窄的宿主机上）。在 64 位系统上可能不需要，但并无害处。

编译软件包：

```
make
```

安装软件包，并解决导致 libc.so 链接到宿主机发行版 zlib 的问题：

```
make DESTDIR=$LFS install -j1
install -vm755 libctf./libs/libc.so.0.0.0 $LFS/usr/lib
```

关于该软件包的详细信息位于第 8.8.2 节，“Binutils 的内容”。

## 6.18. GCC-11.2.0 - Pass 2

GCC 软件包包含一个编译器、一个 C++ 编译器以及用于构建的其他工具。

预计编译时间：12 SBU

所需磁盘空间：3.3 GB

### 6.18.1. 安装 GCC

再次创建一个独立的构建目录：

```bash
mkdir -v build
cd build
```

为编译准备 GCC：

```bash
../configure /\
--prefix=/usr \
--build=$(../config.guess) \
--host=$LFS_TGT \
--disable-nls \
--enable-shared \
--disable-werror \
--enable-64-bit-bfd /
```

新 configure 选项的含义：

- --with-sysroot=$LFS

  确保编译器在 $LFS 中查找头文件和库。

- --enable-array

  在构建 GCC 时自动启用。

编译软件包：

```
make
```

安装软件包，并解决导致 libc.so 链接到宿主机发行版 zlib 的问题：

```
make DESTDIR=$LFS install -j1
install -vm755 libctf./libs/libc.so.0.0.0 $LFS/usr/lib
```

关于该软件包的详细信息位于第 8.2.2 节，“GCC 的内容”。

## 6.19. Glibc-2.36

Glibc 软件包包含 GNU C 库，它是 Linux 系统的核心组件。

预计编译时间：2.5 SBU

所需磁盘空间：500 MB

### 6.19.1. 安装 Glibc

为编译准备 Glibc：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.11.2 节，“Glibc 的内容”。

## 6.20. Libcrypt-4.2.3

Libcrypt 软件包包含用于加密和解密的库。

预计编译时间：0.5 SBU

所需磁盘空间：10 MB

### 6.20.1. 安装 Libcrypt

为编译准备 Libcrypt：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.13.2 节，“Libcrypt 的内容”。

## 6.21. Zlib-1.3.1

Zlib 软件包包含用于数据压缩的库。

预计编译时间：0.2 SBU

所需磁盘空间：5 MB

### 6.21.1. 安装 Zlib

为编译准备 Zlib：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.15.2 节，“Zlib 的内容”。

## 6.22. Readline-8.2

Readline 软件包包含用于编辑格式化输入行的库。

预计编译时间：0.3 SBU

所需磁盘空间：5 MB

### 6.22.1. 安装 Readline

为编译准备 Readline：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.17.2 节，“Readline 的内容”。

## 6.23. Ncurses-6.4

Ncurses 软件包包含用于创建终端界面的库。

预计编译时间：0.5 SBU

所需磁盘空间：15 MB

### 6.23.1. 安装 Ncurses

为编译准备 Ncurses：

```
./configure --prefix=/usr \
    --host=$LFS_TGT \
    --build=$(build-aux/config.guess)
```

编译软件包：

```
make
```

安装软件包：

```
make DESTDIR=$LFS install
```

关于该软件包的详细信息位于第 8.19.2 节，“Ncurses 的内容”。

## Chapter 7. Entering Chroot and Building Tools

### 7.1. Introduction

本章介绍了如何构建各个软件包所需的最后工具。现在所有循环依赖已经解决，我们可以使用一个“chroot”环境，除了运行的内核之外，它是完全隔离的。

为了隔离环境的正常运行，必须与运行的内核建立通信。这是通过所谓的内核文件系统实现的，它们在进入 chroot 环境时必须挂载。在第 7.4 节进入 chroot 环境之前，命令必须以 root 身份运行并设置 IFS 变量。进入 chroot 后，所有命令都以 root 身份运行，幸运的是无法访问你构建 LFS 的操作系统。尽管如此，错误的命令很容易破坏系统。

### 7.2. Changing Ownership

> 注意 本书剩余部分必须以 root 用户身份执行。此外，检查 root 环境中的 IFS。

目前，`$IFS` 中的整个目录层次结构由用户 root 所有，该用户仅存在于宿主机系统中。如果 `$IFS` 下的目录和文件夹保持原样，它们将由一个没有相应账户的用户 ID 所有。这是危险的，因为以后创建的用户账户可能会获得相同的用户 ID 并拥有 `$LFS` 下的所有文件。

为了解决这个问题，通过运行以下命令将 `$LFS/*` 目录的所有权更改为用户 root：

```bash
chown -R root:root $IFS/{usr,lib,var,etc,bin,sbin,tools}
case $(uname -m) in
x86_64) chown -R root:root $LFS/lib64 ;;
esac
```



## 7.3. Preparing Virtual Kernel File Systems

内核提供的各种文件系统用于与内核本身进行通信。这些文件系统是虚拟的，因为它们不占用磁盘空间。文件系统的内容存储在内存中。

首先创建挂载这些文件系统的目录：

```bash
mkdir -pv $IFS/{dev,proc,sys,run}
```

## 7.4. Entering Chroot

在进入 chroot 环境之前，必须挂载必要的内核文件系统。执行挂载命令，并切换到 root 用户：

```bash
mount -t devfs /dev $IFS/dev
mount -t proc /proc $IFS/proc
mount -t sysfs /sys $IFS/sys
mount -t tmpfs /run $IFS/run
chroot $LFS /bin/bash
```

现在你已进入 chroot 环境，可以继续构建后续软件包。

### 7.3.1. 创建初始设备节点

内核启动系统时，需要一些设备节点，特别是控制台（console）和空设备（null）。这些设备节点必须在硬盘上创建，以便在内核 `/dev/` 之前可用，并且在使用 `init=/bin/bash` 启动 Linux 时。运行以下命令创建设备：

```bash
mknod -m 600 LFS/dev/console 5 1
mknod -m 666 LFS/dev/null c 1 3
```

### 7.3.2. 挂载并填充 /dev

向 `/dev` 目录填充设备的推荐方法是在 `/dev` 上挂载一个虚拟文件系统（如 `tmpfs`），并允许在检测或访问设备时在该虚拟文件系统上动态创建。设备创建通常在启动过程中由 Udev 完成。由于这个新系统还没有 Udev，因此有必要手动挂载并填充 `/dev`。这通过绑定主机系统的 `/dev` 目录来实现。绑定挂载（bind mount）是一种特殊的挂载类型，允许你将某个目录或挂载点的镜像创建到其他位置。使用以下命令来实现此：

```bash
mount -v --bind /dev LFS/$dev
```

### 7.3.3. 挂载虚拟内核文件系统

现在剩下虚拟内核文件系统：

```bash
mount -v --bind /dev/pts LFS/$dev/pts
mount -vt proc proc LFS/$proc
mount -vt sysfs sysfs LFS/$sys
mount -vt tmpfs tmpfs LFS/$run
```

在某些系统中，`/dev/shm` 是指向 `/run/shm` 的符号链接。由于 `run` `tmpfs` 已经挂载，因此在这种情况下只需要创建一个目录即可。

```bash
if [ -h LFS/$dev/shm ]; then
  mkdir -pv LFS/$(readlink LFS/$dev/shm)
fi
```

## 7.4. 进入 chroot 环境

现在构建其余所需工具的所有包已位于系统中，接下来是通过安装剩余的临时工具来进入 `chroot` 环境。该环境也将用于最终系统。以 root 身份运行以下命令进入该环境，该环境目前仅包含临时工具：

```bash
chroot LFS /usr/bin/env -i HOME=/root TERM=$TERM PATH=/usr/bin:/sbin /bash --login
```

`env` 命令提供的 `-i` 选项将清除 `chroot` 环境的所有变量。之后，再次设置 `HOME`、`TERM`、`PS1` 和 `PATH` 变量。`TERM=$TERM` 将 `chroot` 内部的 `TERM` 设置为与外部相同的值。`vim` 和 `less` 等程序需要此变量。如果需要其他变量（例如 `CFLAGS` 或 `CXXFLAGS`），这里是设置它们的好地方。

从现在开始，不再需要使用 LFS，因为所有工作都将限制在根目录（`/`）下。注意 `/tools/bin` 不在 `PATH` 中。这意味着 shell 将不会记住执行的二进制文件的位置——出于考虑，关闭了哈希（hashing）。

> 本章剩余部分及后续章节中的所有命令都必须在 `chroot` 环境中运行。如果你出于任何原因离开了此环境（例如重启），请确保在继续安装之前，已按照第 7.3.2 节“挂载并填充 /dev”和第 7.3.3 节“挂载虚拟文件系统”中的说明挂载了虚拟文件系统。

## 7.5. 创建目录

是时候在 LFS 系统中创建完整的结构了。通过执行以下命令创建之前章节中未包含根级目录：

```bash
mkdir -pv /{boot,home,mnt,opt,srv
```

通过执行以下命令在根级创建所需的子目录集：

```bash
mkdir -pv /etc/sysconfig
mkdir -pv /lib/firmware
mkdir -pv /media/{floppy,cdrom}
mkdir -pv /usr/local/{include,src}
mkdir -pv /usr/local/{bin,sbin}
mkdir -pv /usr/local/share/{core,doc,info,locale}
mkdir -pv /usr/local/share/{misc,tmp,zoneinfo}
mkdir -pv /usr/local/share/man/{1-8}
mkdir -pv /var/{cache,log,opt,spool}
mkdir -pv /var/lib/{color,misc,locate}
```

```bash
ln -sf /run /var/run
ln -sf /run/lock /var/lock
```

```bash
install -dv -m 0750 /root
install -dv -m 1777 /tmp /var/tmp
```

目录默认以权限 755 创建，但对于所有目录来说都是不理想的。在上面的命令中，做了两处更改——一个针对 root 的主目录，另一个针对临时文件目录。第一种模式确保没有人可以进入 `/root` 目录——就像普通用户对待自己的目录一样。第二种更改确保任何用户都可以向 `/tmp` 和 `/var/` 目录写入，但不能从其中删除其他用户的文件。后者受所谓的“粘性位”（sticky bit）保护，它是 1777 位权限中的最高位（1）。

### 7.5.1 FHS 合规性

该目录树基于文件系统层级标准（FHS）（可从 https://refspec.linux.foundation/org/fhs.html 获取）。FHS 还允许可选存在某些目录，例如 `/usr/local/games` 和 `/usr/share/games`。我们只创建需要的目录。不过，你可以自由创建这些目录。

## 7.6. 创建基本文件和符号链接

历史上，Linux 在 `/etc/mtab` 文件中维护一个挂载文件列表。现代内核在内部维护该列表并通过 `/proc` 文件系统导出。为了满足期望存在 `/etc/mtab` 的工具，请创建以下符号链接：

```bash
ln -sv /proc/self/mounts /etc/mtab
```

创建一个基础的 `/etc/hosts` 文件，以便在某些测试中引用，并在 Perl 的一个配置文件中使用：

```
127.0.0.1  localhost $(hostname)
::1        localhost
```

为了让 root 能够登录并识别名称 "root"，在 `/etc/passwd` 和 `/etc/group` 文件中必须有相关的条目。

通过运行以下命令创建 `/etc/passwd` 文件：

```bash
cat > /etc/passwd << "EOF"
root:x:0:root:/root:/bin/bash
bin:x:1:1:/dev/null:/bin/false
daemon:x:6:Daemon User:/dev/null:/bin/false
messagebus:x:18:18:D-Bus Message Daemon User:/run/dbus:/bin/false
uuid:x:80:80:UUID Generation Daemon User:/dev/null:/bin/false
group:x:99:Unprivileged User:/dev/null:/bin/false
EOF
```

root 的实际密码将在以后设置。通过运行以下命令创建 `/etc/group` 文件：

```bash
cat > /etc/group << "EOF"
root:x:0
bin:x:1
daemon:x:2
sys:x:3
kmem:x:4
tape:x:5
daemon:x:6
floppy:x:7
disk:x:8
tty:x:9
dialout:x:10
audio:x:11
video:x:12
tmp:x:13
video:x:14
input:x:15
adm:x:16
messagebus:x:18
cdrom:x:24
mail:x:34
lp:x:42
power:x:43
udev:x:54
vm:x:61
uuid:x:80
wheel:x:97
nogroup:x:99
users:x:999
EOF
```

## 7.7. 来自 GCC-11.2.0 的 Libstdc++, Pass 2

在构建 gcc-pass2 时，我们必须定义 C++ 标准库的安装位置，因为此时没有合适的编译器来编译它。我们不能使用该部分内置的编译器，因为它是原生编译器，不应在 chroot 之外使用，以防用某些组件污染库。

估算编译时间：0.8 SBU

所需的磁盘空间：1.1 GB

### 7.7.1. 目标 Libstdc++ 的安装

> 注意

Libstdc++ 是 GCC 源代码的一部分。你应该先解压 GCC 压缩包，并进入 gcc-11.2.0 目录。

在 gcc 目录树中构建 libstdc++ 时，创建一个存在的链接：

```
ln -s gtr-posix.h libgcc/gthr-default.h
```

为 libstdc++ 创建一个独立的构建目录并进入其中：

```
mkdir -v build
cd build
```

为编译 libstdc++-v3/ 准备：

```bash
./libstdc++-v3/configure \
  CXXFLAGS="-g -o2 -D_GNU_SOURCE" \
  --prefix=/usr \
  --disable-multilib \
  --disable-nls \
  --host=$(uname -m)-lfs-linux-gnu \
  --disable-libstdcxx-pch
```

配置选项的含义：

CXXFLAGS="-g -o2 -D_GNU_SOURCE"

这些标志由顶层 Makefile 在对 GCC 进行完整构建时设置。

--host=$(uname -m)-lfs-linux-gnu

我们必须模拟当此包作为完整编译器构建器的一部分进行构建时发生的情况。此开关将传递给 GCC 的构建机制。

--disable-libstdcxx-pch

此开关防止安装预编译的包含文件，这些文件在当前阶段是不需要的。

运行以下命令编译 libstdc++：

```
make
```

安装库：

```
make install
```

关于此包的详细信息见第 8.26.2 节，“GCC 内容”。

## 7.8. Gettext-0.21

Gettext 包包含了用于国际化和本地化的工具。这些工具允许程序在带有 NLS（原生语言支持）的情况下进行编译，使其能够以用户的母语言输出消息。

**估算编译时间：1.8 SBU**

**所需的磁盘空间：280 MB**

### 7.8.1. Gettext 的安装

对于我们的临时工具集，我们只需要从 Gettext 安装三个程序。

为 Gettext 准备编译：

```bash
./configure --disable-shared
```

**配置选项的含义：**

--disable-shared

我们现在不需要安装任何共享的 Gettext 库，因此没有必要构建它们。

编译该包：

```
make
```

安装 msgfmt、msgmerge 和 xgettext 程序：

```bash
cp -v gettext-tools/src/{msgfmt,msgmerge,xgettext} /usr/bin
```

关于此包的详细信息见第 8.31.2 节，“Gettext 内容”。

## 7.9. Bison-3.7.6

Bison 包包含一个解析器生成器。

估算编译时间：0.3 SBU

所需的磁盘空间：50 MB

### 7.9.1. Bison 的安装

为 Bison 准备编译：

```bash
./configure --prefix=/usr \
    --docdir=/usr/share/doc/bison-3.7.6
```

新配置选项的含义：

```
--docdir=/usr/share/doc/bison-3.7.6
```

这告诉构建系统将 bison 文档安装到带版本的目录中。

编译该包：

```
make
```

安装该包：

```
make install
```

关于此包的详细信息见第 8.32.2 节，“Bison 内容”。

## 7.10. Perl-5.34.0

Perl 包包含了实用提取和报告语言（Practical Extraction and Report Language）。

估算编译时间：1.7 SBU

所需的磁盘空间：272 MB

### 7.10.1. Perl 的安装

为 Perl 准备编译：

```bash
sh Configure -des \
  -Dprefix=/usr \
  -Dvendorprefix=/usr \
  -Dprivlib=/usr/lib/per15/5.34/core_perl \
  -Darchlib=/usr/lib/per15/5.34/core_perl \
  -Dsitelib=/usr/lib/per15/5.34/site_perl \
  -Dvendorlib=/usr/lib/per15/5.34/site_perl \
  -Dsitearch=/usr/lib/per15/5.34/site_perl \
  -Dvendorlib=/usr/lib/per15/5.34/vendor_perl \
  -Dvendorarch=/usr/lib/per15/5.34/vendor_perl
```

新 Configure 选项的含义：

-des

这是三个选项的组合：-d 对所有项目使用默认值；-e 确保完成所有任务；-s 静默非本质输出。

编译该包：

```
make
```

安装该包：

```
make install
```

关于此包的详细信息见第 8.41.2 节，“Perl 内容”。

## 7.11. Python-3.9.6

Python 3.9.6 包包含开发环境。它用于面向对象编程、编写脚本或开发整个应用程序。

估算编译时间：1.2 SBU

所需的磁盘空间：347 MB

### 7.11.1. Python 的安装

> 注意

有两个以“python”开头的文件。要提取的是 Python-3.9.6.tar.xz。

为 Python 准备编译：

```bash
./configure --prefix=/usr \
    --enable-shared \
    --without-ensurepip
```

配置选项的含义：

--enable-shared

此开关防止安装静态库。

--without-ensurepip

此开关禁用了 pip 安装程序。

编译该包：

```
make
```

> 注意

Python 模块无法构建，因为尚未安装依赖。构建系统仍然尝试构建它们，因此某些文件将失败并指示“致命错误”。该消息应当忽略。可选模块将在稍后构建。

安装该包：

```
make install
```

关于此包的详细信息见第 8.50.2 节，“Python 内容”。

## 7.12. Texinfo-6.8

Texinfo 包包含了用于读取、写入和转换 info 页面的程序。

估算编译时间：0.3 SBU

所需的磁盘空间：109 MB

### 7.12.1. Texinfo 的安装

首先，修复使用 Glibc-2.34 或更高版本构建包时出现的问题：

```bash
sed -e 's/_attribute_nonnull/__nonnull//' \
-i libinfo/malloc/malloc-skeleton.c
```

为 Texinfo 准备编译：

```bash
./configure --prefix=/usr
```

编译该包：

```
make
```

安装该包：

```
make install
```

关于此包的详细信息见第 8.67.2 节，“Texinfo 内容”。

## 7.13. Util-linux-2.37

Util-linux 包包含了杂用程序。

估算编译时间：0.7 SBU

所需的磁盘空间：128 MB

### 7.13.1. Util-linux 的安装

FHS 建议使用 /var/lib/hwclock 目录而不是通常 /etc 目录作为 adjtime 文件的位置。用以下命令创建此目录：

```
mkdir -pv /var/lib/hwclock
```

为 Util-linux 准备编译：



```bash
./configure ADJTIME_PATH=/var/lib/hwclock/adjtime \
    --libdir=/usr/lib \
    --docdir=/usr/share/doc/util-linux-2.37 \
    --disable-chfn-chsh \
    --disable-login \
    --disable-nologin \
    --disable-su \
    --disable-setpriv \
    --disable-runuser \
    --disable-pylibmount \
    --disable-static \
    --without-python \
    --statedir=/run
```

配置选项的含义：

`ADJTIME_PATH=/var/lib/hwclock/adjtime`

这根据 FHS 设置记录硬件时钟信息的位置。对于这个临时工具来说严格不需要，但它可以防止在另一个位置创建文件，该文件在构建 util-linux 包时不会覆盖或合并。

`--libdir=/usr/lib`

这确保 `.so` 符号链接直接指向同一目录（`/usr/lib`）下的共享库文件。

`--disable-*`

这些开关防止产生关于构建不在 BFS 或尚未安装的包组件的警告。

`--without-python`

此开关禁用了 Python。避免尝试构建需要的绑定。

`--statedir=/run`

此开关正确设置了 uuid 和 libuuid 使用的 socket 位置。

编译该包：

```
make
```

安装该包：

```
make install
```

关于此包的详细信息见第 8.72.2 节，“Util-linux 内容”。

## 14. 清理并保存临时系统

### 7.14.1. 清理

首先，移除当前安装的文档以防止进入最终系统，并节省约 35 MB：

```
rm -rf /usr/share/{info,man,doc}/*
```

其次，`.la` 文件仅在链接静态库时使用。在使用动态共享库时它们是不必要的且具有潜在危害的，特别是使用非自动构建系统时。在仍在 chroot 中，现在删除这些文件：

```
find /usr/lib, libexec -name *.la -delete
```

当前系统大小现在约为 3 GB，但 `/tools` 目录不再需要了。它占用约 1 GB 的磁盘空间。现在删除它：

```
rm -rf /tools
```

### 7.14.2. 备份

> 注意

本节中的剩余步骤都是可选的。尽管如此，一旦你开始在第 8 章中安装包，临时文件将被覆盖。因此，按照如下所述对当前系统进行备份可能是一个好主意。

以下步骤在 chroot 环境外执行。这意味着你必须在继续之前离开 chroot 环境。此此是为了访问 chroot 环境之外的文件位置来存储/读取备份存档，出于安全考虑，不应将其放在 `$LFS` 层次结构内。

> 重要

以下所有指令均由 root 执行。小心你将运行的命令，因为它们可能会修改你的主机系统。注意环境变量 `LFS` 默认对于用户 L，但对于 root 可能不是。当需要由 root 执行命令时，确保你已经设置了 `LFS`。这在第 2.6 节，“设置 $LFS 变量”中讨论过。

现在，如果你正在进行备份，请离开 chroot 环境：

```
exit
```

此时，基本程序和库已经创建，你的当前系统处于良好状态。如果在后续章节发生致命失败，通常证明删除所有内容并重新开始（更仔细地）是恢复的最佳选择。遗憾的是，所有临时文件将被删除，为了避免浪费额外重做已经成功构建的内容，进行备份。

确保 root 用户目录下至少有 1 GB 的可用磁盘空间（源压缩包将包含在备份存档中）。

# Linux 从头构建 - 版本 11.0

制作备份之前，请卸载虚拟系统：

```
umount $LFS/dev/{pts,}
umount $LFS/{sys,proc,run}
```

运行以下命令创建备份存档：

> 注意

备份存档是经过压缩的，即使在速度较快的系统上，也需要相当的时间（超过 10 分钟）。

此外，确保已为 root 用户设置了 `$LFS` 环境变量。

```
cd $LFS
tar -cJf $HOME/lfs-temp-tools-11.0.tar.xz
```

如果你不想将备份存储在 root 用户的家目录中，请将 `$LFS` 替换为你选择的目录。

## 7.14.3. 恢复

如果犯了某些错误并需要重新开始，可以使用此备份来恢复系统并节省一些恢复时间。由于源码位于 `$LFS` 下，它们也包含在备份存档中，不需要重新下载。在确认 `$LFS` 设置正确后，执行以下命令恢复备份：

> 警告

以下命令极其危险。如果你以 root 用户身份运行 `rm -rf/*`，且你没有更改 `$LFS` 目录或没有为 root 用户设置 `$LFS` 环境变量，它将破坏你的整个主机系统。你已被警告了。

```
cd $LFS
rm -rf ./
tar -xpf $HOME/lfs-temp-tools-11.0.tar.xz
```

再次双检环境是否已正确设置，并继续构建系统的部分。

> 重要

如果你退出了 chroot 环境以创建备份或使用恢复重新构建，请记住检查虚拟文件系统仍然挂载（`findmnt | grep $LFS`）。如果未挂载，请按照第 7.3 节“准备虚拟内核文件系统”中的描述删除它们，并在继续之前重新进入 chroot 环境（见第 7.4 节“进入 chroot 环境”）。

90

# 第四部分 构建 LFS 系统

## 第 8 章 安装基础系统软件

### 8.1. 引言

在本章中，我们开始正式构建 LFS 系统。

这些软件的安装是直接的。尽管在许多情况下，安装说明可以变得更短、更通用，但我们选择为每个软件包提供完整的说明，以尽可能减少出现错误的可能性。学习 Linux 系统如何运作的关键在于了解每个软件包的用途，以及为什么你（或系统）可能需要它们。

我们不建议使用优化。优化虽然可以使程序运行得更快，但可能导致编译困难以及运行程序时的问题。如果某个软件包拒绝使用优化编译，请尝试在不使用优化的情况下编译，看看是否能解决问题。即使软件包在使用优化时可以编译，也存在由于代码与工具之间复杂的相互作用导致其编译错误的风险。另请注意，书中未指定的 `-march` 和 `-mtune` 选项值未经过测试。这可能会导致问题（Binutils、GCC 和 Glibc）。使用编译器优化所带来的微小潜在收益往往大于其风险。鼓励 LFS 的首次构建者在不使用自定义优化的情况下构建。随后的系统仍然运行得非常快速且稳定。

在安装说明之前，每个安装页面都提供了有关软件包的信息，包括其内容的简要描述、构建大约需要多长时间以及在此过程中需要多少磁盘空间。在安装说明之后，列出了该软件包安装的程序和库列表（以及简要描述）。

> SBU 值和所需的磁盘空间包含了第 8 章中所有适用软件包的测试套件数据。SBU 值是使用单个 CPU 核心（`-j1`）对所有操作计算出的。

### 8.1.1. 关于库

通常，LFS 编辑不鼓励构建和安装静态库。大多数静态库的原始目的在现代 Linux 系统中已经过时。此外，将静态库链接到程序可能是有害的。如果需要更新库来消除安全问题，所有使用该静态库的程序都需要重新链接到新库。由于静态库的使用并不总是显而易见的，相关的程序（以及链接过程）甚至可能无人知的。

在本章的操作中，我们移除或禁用了大多数静态库的安装。这通常通过传递 `--disable-static` 配置选项来实现。在其他情况下，需要替代方案。在少数情况下，特别是 glibc，静态库的使用对于通用软件包构建过程仍然至关重要。

关于库的更全面讨论，请参阅 BLFS 书中的“库：静态的还是共享的？”讨论。

## 8.2. 软件包管理

包管理是 LFS 书中经常被要求的补充内容。包管理器允许跟踪文件的安装，从而轻松删除和升级软件包。除了二进制文件和库文件外，包管理器还将处理配置文件的安装。在你开始好奇之前，不——本节将不会讨论不推荐任何特定的包管理器。它提供了最流行技术及其工作原理的总结。最适合你的完美包管理器可能是这些技术之一，也可能是其中两种或更多技术的组合。本节简要提到了在升级软件包时出现的问题。

LFS 或 BLFS 中未提及包管理器的原因包括：

- 处理包管理会将注意力从这些书籍的目标转移开。

- 软件包版本与库名称之间没有关联。

### 8.2.1. 升级问题

包管理器使得升级到新版本变得容易。通常，LFS 和 BLFS 中的说明可以用于升级到新版本。关于软件包，你需要注意以下点：

- 如果内核需要升级（例如从 5.10.17 升级到 5.10.18），不需要重建其他内容。具体来说，API 头不需要也不应该）随内核一起升级。你需要重启系统以使用升级后的内核。

- 如果 API 头或 Glibc 需要升级到新版本（例如从 glibc-2.31 升级到 glibc-2.32），重新构建 LFS 更安全。你可能需要按照依赖顺序重建所有软件包。

- 如果包含共享库的软件包已更新，且库的名称发生了变化，那么动态链接到该库的软件包都需要重新编译以链接到新库。例如，考虑安装 lib.so.1 的软件包 foo-1.23。如果你将软件包升级到新版本 foo-1.24，它安装了 lib.so.2。在这种情况下，任何动态链接到 lib.so.1 的软件包都需要重新编译以链接到 lib.so.2，以便使用新的库版本。在所有重新编译之前，你不删除之前的库。

- 如果包含共享库的软件包已更新，且库的名称没有变化，如果库文件的版本号减少了（例如库名称保持为 libfoo.so.1，但文件名从 libfoo.so.1.25 变为 libfoo.so.1.24），你应该删除之前安装的 libfoo.so.1.25。或者，`ldconfig`（通过命令或某些软件包的安装）将重置符号链接 lib.so.1 指向该库文件，因为它的版本号看起来“更新”。这种情况可能发生在你必须降级软件包时，或者软件包更改了已安装库文件的方案。

```
grep -e 'libfoo.*deleted' /proc/*/maps |
  tr -cd 0-9\n xargs -rp ps u
```

# Linux 从头构建 - 版本 11.0

OpenSSH 正被用于访问系统并已链接到更新后的库，你需要重启 sshd 服务，注销并重新登录，然后再次运行该命令以确认没有程序程序在使用被删除的库。

- 如果二进制文件或共享库被覆盖，使用该二进制文件或库中的代码或数据可能会导致崩溃。更新二进制文件或共享库且不会导致进程崩溃的方法是先将其删除，然后将新版本安装到原位置。Coreutils 提供的 `install` 命令已经实现了这一点，且大多数软件包都使用它来安装二进制文件和库。这意味着在大多数情况下你不会受到此问题的困扰。然而，某些软件包的安装（特别是 BLFS 中的 Mozilla JS）只是在文件存在时直接覆盖该文件并导致崩溃，因此在更新软件包之前，保存你的工作并关闭未打开的进程会更安全。

## 8.2.2. 软件包管理技术

以下是一些常见的包管理技术。在决定使用包管理器之前，请对各种技术以及特定方案的缺点进行一些研究。

### 8.2.2.1. 全都在我脑子里！

是的，这是一种包管理技术。有些人认为没有必要使用包管理器，因为他们了解软件包，并且知道每个软件包安装了哪些文件。用户也不需要包管理，因为当软件包发生变化时，他们依赖重新构建整个系统。

### 8.2.2.2. 安装在独立目录

这是一种原始的包管理，不需要任何额外的软件包来管理安装。每个软件包都安装在独立的目录中。例如，软件包 `foo-1.1` 安装在 `/usr/pkg/foo-1` 中，并创建一个从 `/usr/pkg/foo` 到 `/usr/pkg/foo-1` 的软链接。安装新版本 `foo-1.2` 时，它被安装在 `/usr/pkg/foo-1.2` 中，之前的软链接被指向新版本的软链接替换。

环境变量如 `PATH`、`LD_LIBRARY_PATH`、`MANPATH`、`INFOPATH` 和 `CPPFLAGS` 需要扩展以包含 `/usr/pkg/foo`。对于少数软件包来说，这种方案变得难以忍受。

### 8.2.2.3. 符号链接风格包管理

这是前述包管理技术的变体。每个软件包的安装方式与前一种方案类似。但不是创建软链接，而是将每个包链接到 `/usr` 层次结构中。这消除了扩展环境变量的需求。虽然用户可以创建软链接来自动化创建，但包管理器一直在使用这种方法。一些流行的工具包括 Stow、Epkg、Graft 和 Depot。

安装需要是“伪装”的，使得软件包虽然安装在 `/usr` 中，但实际上是安装在 `/usr/pkg` 层次结构中的。以这种方式安装并非于易事。例如，假设你正在安装软件包 `libfoo-1.1`。以下指令可能无法正确安装该软件包：

```
./configure --prefix=/usr/pkg/libfoo/1.1
make
make install
```

安装将会运行，但依赖包可能不会像你预期的那样链接到 `libfoo`。如果有一个链接到 `libfoo` 的软件包，你可能会发现它链接到了 `/usr/pkg/libfoo/1.1/lib/libfoo.so.1`，而不是你预期的 `/usr/lib/libfoo.so.1`。正确的方法是使用 `DESTDIR` 策略对软件包进行伪装安装。该方法的工作原理如下：

```
./configure --prefix=/usr
make
make DESTDIR=/usr/pkg/libfoo/1.1 install
```

大多数软件包都支持这一点，但也有一些不支持。对于不符合标准的软件包，你可能需要手动安装软件包，或者你可能会发现将问题的软件包安装在 `/opt` 中更容易。

### 8.2.2.4. 基于时间戳

在这种技术中，在安装软件包之前会对文件标记时间戳。安装完成后，简单地使用 `find` 命令配合相应的选项，就可以生成时间戳文件创建后安装的所有文件的日志。使用这种方法编写的包管理器是 `install-log`。

尽管这种方案具有简单的优点，但它有两个缺点。在安装期间，文件使用的是除当前时间以外的任何时间戳，文件不会被包管理器跟踪。这种方案只能在一次安装一个软件包时使用。如果在两个不同的控制台上正在安装两个软件包，日志将是不可的。

### 8.2.2.5. 追踪安装脚本

在这种方法中，安装脚本的执行会被记录。可以使用两种技术：

可以将 `LD_PRELOAD` 环境变量设置为在安装前预加载的库。在安装期间，该库通过附加到各种可执行文件（如 `cp`、`install`）并跟踪修改系统的系统调用来跟踪正在安装的软件包。为了使此方法生效，所有可执行文件必须是动态链接且没有 `sudo` 或 `gid` 位。该库可能会安装过程中导致意外的副作用。因此，建议进行测试以确保包管理器没有破坏任何内容并记录了适当的文件。

第二种技术是使用 `strace`，它会记录执行安装脚本期间的所有系统调用。

### 8.2.2.6. 创建软件包存档

在这种方案中，安装如符号链接风格管理中描述的那样被伪装到单独树中。安装完成后，使用已安装的文件创建一个软件包存档。该存档随后被用于在其他机器上安装该软件包。

发行版中的大多数包管理器都使用这种方法。遵循这种方法的包管理器示例包括 RPM（顺便说，它是 Linux 标准要求的）、`pkg-utils`、Debian 的 `apt` 以及 Gent 系统。关于如何为 LFS 适配这种风格的包管理的提示位于 https://www.linuxscratch.org/hints/downloads/fakeroot.txt。

包含依赖信息的软件包创建是复杂的，超出了 LFS 的范围。

Slackware 使用基础系统进行软件包安装。该系统故意不处理像复杂的管理器那样的包依赖。Slack 包管理的详情请访问 http://www.slackbook.org/html/package-management.html。

### 8.2.2.7. 基于用户的方法

这种 LFS 特有的方案由 Matthias Benmann 设计，可在 Hints Project 获取。在这种方案中，每个软件包都作为一个单独的用户安装到标准位置。属于软件包的文件通过检查用户 ID 来识别。该方法的特点和缺点过于复杂，无法在本节中详细描述。详情请参见提示 https://www.linuxscratch.org/hints/downloads/files/more_control_and_pkg_man.txt。

## 8.2.3. 在多个系统部署 LFS

LFS 系统的优势之一是没有文件依赖于磁盘系统上的位置。将 LFS 构建克隆到与基础系统架构相同的计算机上，只需使用 `tar` 处理包含根目录的 LFS 分区（基础 LFS 构建解压后约 250MB），通过网络传输或光盘将该文件复制到新系统并进行解压即可。从那时起，必须更改一些配置文件：`/etc/hosts`、`/etc/fstab`、`/etc/passwd`、`/etc/shadow`、`/etc/ld.so.conf`、`/etc/sysconfig/rc.site`、`/etc/sysconfig/network` 以及网卡配置。

根据系统硬件和原始内核配置的差异，可能需要为新系统构建自定义内核。

> 注意

> 有报告称在相似但不相同的架构之间复制会出现问题。例如，Intel 系统的指令集与 AMD 处理器并不相同，某些处理器的后续版本可能具有早期版本不存在的指令。

最后，必须通过第 10.4 节“使用 GRUB 设置启动过程”使新系统能够启动。

## 8.3. Man-pages-5.13

Man-pages 软件包包含 2,200 多页帮助页。

**预计编译时间：** 少于 0.1 SBU

**所需的磁盘空间：** 33 MB

### 8.3.1. 安装 Man-pages

运行以下命令安装 Man-pages：

```
make prefix=/usr install
```

### 8.3.2. Man-pages 的内容

**已安装文件：** 各种 man 页

#### 概要说明

- man pages 描述 C 编程语言函数、重要的设备文件以及重要的配置文件



## 8.4. nmap-Etc-202102611

nmap-Etc 软件包为网络服务和协议提供数据。

预计编译时间：少于 0.1 SBU

所需的磁盘空间：4.7 MB

### 8.4.1. 安装 nmap-Etc

对于此软件包，我们只需要将文件复制到指定位置：

```
cp services protocols /etc
```

### 8.4.2. nmap-Etc 的内容

- 已安装文件：`/etc/protocols` 和 `/etc/services`

#### 概要说明

- `/etc/protocols` 描述从 TCP/IP 子系统可用的各种 DARPA 互联网协议

- `/etc/services` 提供互联网服务的友好文本名称与底层分配的端口号及协议类型之间的映射

## 8.5. Glibc-2.34

Glibc 软件包包含主 C 库。该库为内存分配、目录搜索、打开和关闭文件、读取和写入文件、字符串处理、模式匹配、算术等提供了基础例程。

预计编译时间：21 SBU

所需的磁盘空间：2.4 GB

### 8.5.1. 安装 Glibc

首先，修复上游发现的安全问题：

```
sed -e '/^NOTIFY_REMOVED/\s*\\&& data.attr != NULL)/' \
-i sysdeps=/usr/sys/linux/mq_notif.c
```

部分 Glibc 程序使用不符合 FHS 标准的 `/var/db` 目录来存储运行时数据。应用以下补丁以使此类程序将运行时数据存储在符合 FHS 标准的位置中：

```
patch -Npl1 -i ../glibc-2.34-fhs-1.patch
```

Glibc 文档建议在专门的构建目录中编译 Glibc：

```
mkdir -v build
cd build
```

确保 `ldconfig` 和 `sln` 工具已安装到 `/usr/sbin`：

```bash
echo "rootsbindir=/usr/sbin" > config.parms
```

为编译 Glibc 准备：

```
../configure --prefix=/usr \
--disable-error \
--enable-kernel=3.2 \
--enable-stack-protector=strong \
--with-headers=/usr/include \
libc_cv_slibdir=/usr/lib
```

`--disable-error`

此选项禁用传递给 GCC 的 -Werror 选项。这运行测试套件是必要的。

`--enable-kernel=3.2`

此选项告诉构建系统 glibc 可以用于低于 3.2 的内核。这意味着无法使用在后续版本引入的系统调用中生成的解决方案。

`--enable-stack-protector=strong`

此选项通过添加额外的代码来检查缓冲区溢出（如栈溢出攻击），从而增加系统安全性。

`--with-headers=/usr/include`

此选项告诉构建系统去哪里查找内核 API 头文件。

`libc_cv_sld=/usr/lib`

此变量为所有系统设置正确的库。我们不希望使用 lib64。

编译软件包：

```
make
```

> 重要
>
> 在本节中，Glibc 的测试套件是至关重要的。在任何情况下都不要跳过。

通常会有少数测试未通过。下面列出的测试失败通常可以忽略。

### make check

你可能会看到一些测试失败。Glibc 测试套件在某种程度上依赖于宿主机系统。4200 个测试中的少数几次失败通常可以忽略。以下是近期 LFS 版本中常见的常见问题列表：

- iojst-lcmod 已知在 LFS 环境中会失败。
- misc/ast-ttynam 已知在 LFS 环境中会失败。

尽管这是一个无害的消息，但 Glibc 的安装阶段会由于缺少 `/etc/ld.so.conf` 而报错。使用以下命令防止此警告：

```bash
touch /etc/ld.so.conf
```

修复生成的 Makefile，以跳过在 LFS 部分环境中失败的非必要完整性检查：

```
sed '/test-installation/s/@@$(PERL)@echo not running@' -i ..Makefile
```

安装软件包：

```bash
make install
```

修复 ldd 脚本中执行文件加载器的硬编码路径：

```bash
sed '/RTLDLIST=/s/@usr@g' -i /usr/bin/ldd
```

为 nscd 安装配置文件和运行时目录。

```
cp -v ../nscd/nscd.conf /etc/nscd.conf
mkdir -pv /var/cache/nscd
```

接下来，安装可以使系统以不同语言响应的区域设置（locales）。没有任何区域设置是必须，但如果缺少其中某些，未来软件包的测试套件将跳过重要的测试。

可以使用 `localedef` 程序安装单个区域设置。例如，下面的第一个 localedef 将 `/usr/share/locale18n/locales/cs_CZ` 定义与 `/usr/share/locale18n/charmaps/UTF-8.gz` 结合，并将结果附加到 `/usr/lib/locale-archive`。以下指令将安装为了最佳覆盖所需的区域设置：

```bash
mkdir -pv /usr/lib/locale
localedef -i POSIX -f UTF-8 2 > /dev/null || true
localedef -i cs_CZ -f UTF-8 cs_CZ.UTF-8
localedef -i de_DE -f ISO-8859-1 de_DE
localedef -i de_DE -f ISO-8859-15 de_DE
localedef -i de_DE -f UTF-8 de_DE.UTF-8
localedef -i el_GR -f ISO-8859-7 el_GR
localedef -i en_GB -f ISO-8859-1 en_GB
localedef -i en_GB -f UTF-8 en_GB.UTF-8
localedef -i en_HK -f ISO-8859-1 en_HK
localedef -i en_PH -f ISO-8859-1 en_PH
localedef -i en_US -f ISO-8859-1 en_US
localedef -i en_US -f UTF-8 en_US.UTF-8
localedef -i es_ES -f ISO-8859-15 es_ES
localedef -i es_MX -f ISO-8859-1 es_MX
localedef -i fa_IR -f UTF-8 fa_IR
localedef -i fr_FR -f ISO-8859-1 fr_FR
localedef -i fr_FR -f ISO-8859-15 fr_FR
localedef -i fr_FR -f UTF-8 fr_FR.UTF-8
localedef -i i_IS -f ISO-8859-1 i_IS
localedef -i i_IS -f UTF-8 i_IS.UTF-8
localedef -i it_IT -f ISO-8859-1 it_IT
localedef -i it_IT -f ISO-8859-15 it_IT
localedef -i it_IT -f UTF-8 it_IT.UTF-8
localedef -i ja_JP -f EUC-JP ja_JP 2 > /dev/null || true
localedef -i ja_JP -f SHIFT_JIS ja_JP.SIJS
localedef -i ja_JP -f UTF-8 ja_JP.UTF-8
localedef -i nl_NL -f ISO-8859-15 nl_NL
localedef -i ru_RU -f KOI8-R ru_RU.KOI8-R
localedef -i ru_RU -f UTF-8 ru_RU.UTF-8
localedef -i se_NO -f UTF-8 se_NO.UTF-8
localedef -i ta_IN -f UTF-8 ta_IN.UTF-8
localedef -i tr_TR -f UTF-8 tr_TR.UTF-8
localedef -i zh_CN -f GB18030 zh_CN.GB1830
localedef -i zh_HK -f BIG5-HKSCS zh_HK.BIG5-HKSCS
localedef -i zh_TW -f UTF-8 zh_TW.UTF-8
```

此外，安装适用于你国家、语言和字符集的区域设置。

或者，使用 `glibc-2.34/localedata/SUPPORTED` 文件（包含了上面列出的所有区域以及更多）通过以下耗时命令一次性安装所有区域设置：

```
make localed/install-locales
```

然后需要使用 `localedef` 命令创建并安装 `glibc-2.34/localedata/SUPPORTED` 文件中未列出的区域设置。例如，本章后面的某些测试需要以下两个区域设置：

```
localedef -i POSIX -f UTF-8 C.UTF-8 2> /dev/null || true
localedef -i ja_JP -f SHIFT_JIS ja_JP.SIJS 2> /dev/null || true
```

> 注意
>
> Glib 现在使用 `libidn2` 解析国际化域名。这是一个运行时依赖。如果启用了此功能，请参考 BLFS `libidn2` 页面的安装说明。

## 8.5.2. 配置 Glibc

### 8.5.2.1. 添加 nsswitch

需要创建 `/etc/nsswitch.conf` 文件，因为 Glibc 的默认设置在网络环境中运行良好。

运行以下命令创建一个新文件 `/etc/nsswitch.conf`：

```
cat > /etc/nsswitch.conf << "EOF"
# Begin /etc/nsswitch.conf
passwd: files
group: files
shadow: files

hosts: files dns
networks: files

protocols: files
services: files
ethers: files
rpc: files

# End /etc/nsswitch.conf
EOF
```

#### 添加区域数据

使用以下命令安装并设置区域数据：

```
tar -xf ../tzdata2021a.gz

ZONEINFO=/usr/share/zoneinfo
mkdir -pv $ZONEINFO/{posix,right}

for tz in etcetera southamerica northamerica europe africa antarctica asia australasia; do
    zic -L /dev/null -d $ZONEINFO/${tz}
    zic -L /dev/null -d $ZONEINFO/posix ${tz}
    zic -L leapseconds -d $ZONEINFO/right ${tz}
done
```

```
cp -vp zone.tab iso1970.tab iso366.tab $ZONEINFO
zic -P America/New_York
unset ZONEINFO
```

`zic` 命令的含义：

```
zic -L /dev/null
```

这创建了没有任何闰秒的 posix 时区。将它们放在 zoneinfo 和 zoneinfo/posix 中是常规做法。必须将 POSIX 时区放在 zoneinfo 中，否则不同的测试套件将报错。在嵌入式系统中，通过不使用 posix 目录可以节省 1.9 MB，但某些应用程序或测试套件可能会失败。

```
zic -L leapseconds
```

这创建了包含闰秒的时区。在空间紧张且你不打算更新时区或不在准确时间的嵌入式系统中，可以通过省略 right 目录节省 1.9MB。确定本地时区的一种方法是运行脚本：

# tzselect

在回答几个位置的问题后，脚本将输出时区的名称（例如 America/Edmonton）。在 `/usr/share/zoneinfo` 中列出了其他可能的时区，如 Canada/Eastern 或 ESTEDT，它们未被识别但可以使用。

然后运行以下命令创建 `/etc/localtime` 文件：

```
ln -sf /usr/share/zoneinfo/<xxx> /etc/localtime
```

将 `<xxx>` 替换为选定的时区名称（例如 Canada/Eastern）。

## 8.5.2.3. 配置动态加载器

默认情况下，动态加载器（`lib/ld-linux.so.2`）会在程序运行时搜索 `/lib` 和 `/usr/lib` 中的动态库。如果 `/lib` 和 `/usr/lib` 的其他目录存在库，则需要将它们添加到 `/etc/ld.so.conf` 文件中，以便动态加载器找到它们。通常已知包含额外库的目录有两个 `/usr/local/lib` 和 `/opt/lib`，因此将这些目录添加到动态加载器的搜索路径中。

运行以下命令创建一个新文件 `/etc/ld.so.conf`：

```
cat > /etc/ld.so.conf << "EOF"
# Begin /etc/ld.so.conf
/usr/local/lib
/opt/lib

EOF
```

如果需要，动态加载器还可以搜索目录并包含其中发现的文件的内容。通常该目录下的文件每行指定一个所需的库路径。通过运行以下命令来添加此功能：

```
cat >> /etc/ld.so.conf << "EOF"
# Add an include directory
include /etc/ld.so.conf/*

EOF
mdir -pv /etc/ld.so.conf
```

## 8.5.3. Glibc 内容

- 已安装程序：catchsegv, gencat, getcat, getent, iconv, iconconfig, ldconfig, ldd, ldlibc, locale, localedef, makedef, mtrace, nscd, pproffiledump, pldd, sln, sotuss, sprof, tzselect, xtrace, zdump, and zip

- 已安装库：ld-linux-x86-64.so.2, ld-linux.so.2, libbrokenlocale.{a,so}, libSegFault.{a,so}, liban.{a,so}, libc.{a,so}, lib_nonshared.a, libdl.{a.2}, libga.{a,so}, libibmcheck.a, libmemusage.a, libnvec.{a,so}, libnsld.1, libns_compat.so, libdnss.so, libnfs_files.so, libnhesid.so, libprofile.so, libthread.{a.0}, resolv.{a.so}, librt.{a.1}, libthread_da, and libutil.{a.1}

- 已安装目录：/usr/include/apro, /usr/include/bits, /gnu, /usr/include/net/, netash, /usr/include/netatalk, /usr/include/netx25, /usr/include/metonecet, /usr/include/netinet, /usr/include/netipx, /usr/include/netivuc, /usr/include/netpacket, /usr/include/netrum, /usr/include/netrose, /usr/include/nfs, /usr/include/protocols, /usr/include/rpc, /usr/include/sys, /usr/lib/audit, /usr/lib/gconv, /usr/lib/local, /libexec/getconf, /usr/share/libinfo, /usr/share/zoneinfo, and /var/lib/nss_

## 简描述

- catchsegv 可用于程序因段错误终止时跟踪堆栈回溯
- gencat 生成消息目录
- getconf 显示文件系统特定变量的系统配置值

# Linux From Scratch - 版本 11.0

- getent: 从管理数据库获取条目
- iconv: 执行字符集转换
- iconvconfig: 创建快速加载的 iconv 模块配置文件
- ldconfig: 配置动态链接器运行时绑定
- ldd: 报告每个程序或共享库所需的共享库
- lddlib4: 辅助 ldd 处理对象文件
- locale: 打印关于当前区域设置的各种信息
- localef: 从文本输入编译区域设置规范
- makedb: 从文本输入创建简单的数据库
- mtrace: 读取并解释内存跟踪文件，并以人类可读的格式显示摘要
- nssd: 守护进程为最常见的名称服务请求提供缓存
- ppprofiledump: 转储 PC 性能分析生成的信息
- pldd: 列出运行进程使用的动态共享对象
- sln: ln 的静态链接版本
- sotuss: 跟踪指定命令的共享库调用
- sprof: 读取并显示共享对象性能分析数据
- tzselect: 询问用户系统位置并报告相应的时区描述



- `xtrace`: 通过打印当前执行的函数来跟踪程序的执行

- `zdump`: 时区编译器

- `zic`: 共享库可执行文件的辅助程序

- `ld-*.so`: Glibc 内部使用的粗略方法，用于运行损坏的程序（例如某些 Motif ）。更多信息请见 `glibc-2.34/locale/broken_cur_max.c` 中的注释

- `libSegFault`: 段错误信号处理器，`catchsegv` 使用

- `liban`: 异步查找库

- `libc`: 主 C 库

- `libcrypt`: 密码库

- `libdl`: 不包含任何函数的占位库。以前是动态链接接口库，其函数现在位于 `libc` 中

- `libg`: 不包含任何函数的占位库。以前是 `g++` 的运行时库

- `libm`: 数学库

- `libcheck`: 链接时开启内存分配检查

- `libmemusage`: 被 `memusage` 使用，帮助收集程序的内存使用信息

- `libnsl`: 网络服务库

- `libnss`: 名称服务切换

# Linux From Scratch - 版本 11.0

## 8.8. Xz-5.2.5

`Xz` 包包含用于压缩和解压缩文件的程序。它提供了对 Lzma 和较新的 `xz` 压缩格式的支持。使用 `xz` 压缩文本文件比传统的 `gzip` 或 `bzip2` 命令具有更高的压缩率。

**预计编译时间：** 0.2 SBU

**所需的磁盘空间：** 15 MB

### 8.8.1. 安装 Xz

准备编译 `Xz`：

```
./configure --prefix=/usr \
    --disable-static \
    --docdir=/usr/share/doc/xz-5.2.5
```

编译软件包：

```
make
```

若要测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

### 8.8.2. Xz 包含物物

**已安装的程序：** `lzcat`（链接到 `xz`）、`lzmp`（链接到 `xdiff`）、`lzdiff`（链接到 `xdiff`）、`lzgrep`（链接到 `xzgrep`）、`lzfgrep`（链接到 `xgrep`）、`lzrep`（链接到 `xgrep`）、`lzless`（链接到 `xxz`）、`lzma`（链接到 `xz`）、`lzmacade`、`lzmaininfo`、`lzmore`（链接到 `xzmore`）、`unlzma`（链接到 `xz`）、`unxz`（链接到 `xz`）、`xz`、`xzcat`（链接到 `xz`）、`xzcomp`（链接到 `xdiff`）、`xzdecompress`、`xzdiff`、`xzgrep`（链接到 `xgrep`）、`xzfgrep`（链接到 `xgrep`）、`xxz`，以及 `xzmore`

**已安装的库：** `libzma.so`

**已安装的目录：** `/usr/include/lz` 和 `/usr/share/doc/xz-5.2.5`

### 简要描述

- `lzcat` 解压缩到标准输出

- `lzcmp` 在 LZMA 压缩文件上运行

- `lzdiff` 在 LZMA 压缩文件上运行 `diff`

- `lzgrep` 在 LZMA 压缩文件上运行 `grep`

- `lzfgrep` 在 LZMA 压缩文件上运行 `grep`

- `lzgrep` 在 LZMA 压缩文件上运行 `grep`

- `lzless` 在 LZMA 压缩文件上运行 `less`

- `lzma` 使用 LZMA 格式压缩或解压缩文件

- `lzmadec` 一个针对 LZMA 压缩文件的小型快速解密器

- `lzmainfo` 显示 LZMA 压缩文件头中存储的信息

- `lzmore` 在 LZMA 压缩文件上运行 `more`

- `unlzma` 使用 LZMA 格式解压缩文件

- `xz` 使用 XZ 格式解压缩文件

- `xzcat` 使用 XZ 格式压缩或解压缩文件

- `xzcmp` 解压缩到标准输出

- `xzcmp` 在 X 压缩文件上运行 `cmp`

- `xddec` 一个针对 X 压缩文件的小型快速解密器

- `xdiff` 在 X 压缩文件上运行 `diff`

- `xegrep` 在 X 压缩文件上运行 `egrep`

- `xfgrep` 在 X 压缩文件上运行 `fgrep`

- `xzgrep` 在 X 压缩文件上运行 `grep`

- `xzless` 在 X 压缩文件上运行 `less`

- `xzmore` 在 X 压缩文件上运行 `more`

`liblzma` 库实现了 Lempel-Ziv-Markov 链算法的无损块排序数据压缩。

## 8.9. Zstd-1.5.0

`Zstd` 是一种实时压缩算法，提供高压缩率。它提供了非常广泛的压缩/速度权衡，并由一个极快的解密器支持。

**预计编译时间：** 1.4 SBU

**所需的磁盘空间：** 60 MB

### 8.9.1. 安装 Zstd

编译软件包：

```
make
```

> **注意**
>
> 在测试输出中有几处显示 'failed'。这些是预期之中的，只有 'FAIL' 才是真正的测试失败。不应该有任何测试失败。

若要测试结果，请执行：

```
make check
```

安装软件包：

```
make prefix=/usr install
```

删除静态库：

```
rm -v /usr/lib/libzstd.a
```

### 8.9.2. Zstd 包含物

**已安装的程序：** `zstd`、`zstdcat`（链接到 `zstd`）、`zstdgrep`、`zstdless`、`zstdmit`（链接到 `zstd`）以及 `unzstd`（链接到 `zstd`）

**已安装的库：** `libzstd.so`

### 简要描述

- `zstd` 使用 ZSTD 格式压缩或解压缩文件

- `zstdgrep` 在 ZSTD 压缩文件上运行 `grep`

- `zstdless` 在 ZSTD 压缩文件上运行 `less`

- `libzstd` 使用 ZSTD 算法实现无损数据压缩库

## 8.10. File-54

`File` 包包含一个确定给定文件或多个文件类型的工具。

预计编译时间：0.1 SBU

所需的磁盘空间：15 MB

### 8.10.1. 安装 File

准备编译 `File`：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

若要测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

### 8.10.2. File 包含物

- 已安装的程序：`file`

- 已安装的库：`libmagic.so`

### 简要描述

- `file`: 尝试对每个给定的文件进行分类；它通过执行若干测试来实现——文件系统测试、魔数测试和语言测试

- `libmagic`: 包含用于魔数识别的程序，被 `file` 程序使用

## 8.11. Readline-8.1

`Readline` 包是一组提供命令行编辑和历史记录功能的库。

预计编译时间：0.1 SBU

所需的磁盘空间：15 MB

### 8.11.1. 安装 Readline

重新安装 `Readline` 会导致旧库被移动到 `<libraryname>.old`。虽然通常这不是问题，但在某些情况下可能会触发 `ldconfig` 中的链接器 bug。可以通过执行以下两个种子命令来避免：

```
sed -i '*/.old/d' Makefile.in
sed -i '/(LDSUFF)/c\' support/shlib-install
```

准备编译 `Readline`：

```
./configure --prefix=/usr \
--disable-static \
--with-curses \
--docdir=/usr/share/doc/readline-8.1
```

`configure` 选项的含义：

```
--with-curses
```

该选项告诉 `Readline` 可以在 `curses` 库中找到 `termcap` 库函数，而不是单独的 `termcap` 库。它允许生成正确的 `readline.pc` 文件。

编译软件包：

```
make SHLIB_LIBS="-incursesw"
```

`make` 选项的含义：

```
SHLIB_LIBS="-incursesw"
```

该选项强制 `Readline` 链接到 `libcurses` 库。

此软件包不带测试套件。

安装软件包：

```
make SHLIB_LIBS="-incursesw" install
```

如果需要，安装文档：

```
install -v -m644{pdf,html,dvi} /usr/share/doc/readline-8.1
```

### 8.11.2. Readline 包含物

已安装的库：`library.so` 和 `readline.so`

已安装的目录：`/usr/include/readline` 和 `/usr/share/doc/readline-8.1`

### 简要描述

- `history` 为回溯历史行提供了一致的用户界面

- `readline` 提供了一组命令，用于操作程序交互式会话中输入的文本

## 8.12. M4-1.4.1

`M4` 包包含一个宏处理器。

预计编译时间：0.7 SBU

所需的磁盘空间：48 MB

### 8.12.1. 安装 M4

准备编译 `M4`：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

若要测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

### 8.12.2. M4 包含物

已安装的程序：`m4`

### 简要描述

- `m4` 在复制给定文件时展开其包含的宏。这些宏这些是内置的或用户定义的，并且可以接受任意数量的参数。除了执行宏展开外，`m4` 具有内置函数用于包含命名文件、运行 Unix 命令、执行整数算术、处理文本、递归等。`m4` 程序既可以作为编译器的前端使用，也可以作为宏处理器独立使用。

## 8.13. Bc-5.0.0

`Bc` 包包含一种任意精度数值处理语言。

预计编译时间：小于 0.1 SBU

所需的磁盘空间：6.7 MB

### 8.13.1. 安装 Bc

准备编译 `Bc`：

```
CC=gcc . /configure --prefix=/usr -G -O3
```

`configure` 选项的含义：

- `CC=gcc` 此参数指定要使用的编译器。

- `-O3` 指定要使用的优化级别。

- `-G` 忽略在没有 GNU 的情况下无法工作的测试套件部分。

编译软件包：

```
make
```

要测试 `bc`，运行：

```
make test
```

安装软件包：

```
make install
```

### 8.13.2. Bc 包含物

已安装的程序：`bc` 和 `dc`

### 简要描述

- `bc` 命令行计算器

- `dc` 逆波表达式命令行计算器

## 8.14. Flex-2.6.4

`Flex` 包包含一个用于生成识别文本中模式程序的实用工具。

预计编译时间：0.4 SBU

所需磁盘空间：32 MB

### 8.14.1. 安装 Flex

为编译准备 `Flex`：

```
./configure --prefix=/usr \
    --docdir=/usr/share/doc/flex-2.6.4 \
    --disable-static
```

编译软件包：

```
make
```

要测试结果（约 0.5 SBU），执行：

```
make check
```

安装软件包：

```
make install
```

有少数程序尚未识别 `flex`，并会尝试运行其前身 `lex`。为了支持这些程序，请创建一个符号链接 `lex`，让其在 `lex` 仿真模式下运行 `flex`：

```
ln -sv flex /usr/bin/lex
```

### 8.14.2. Flex 的内容

- 安装的程序：`flex`, `flex++`（指向 `flex` 的链接），以及 `lex`（指向 `flex` 的链接）

- 安装的库：`libfl.so`

- 安装目录：`/usr/share/doc/flex-2.6.4`

#### 简描述

- `flex`：一种用于生成识别文本模式程序的工具；它允许灵活地指定模式查找规则，消除了开发专门程序的需要。

- `flex++`：`flex` 的扩展，用于生成 C++ 代码和类。它是指向 `flex` 的符号链接

- `lex`：一个在 `lex` 仿真模式下运行 `flex` 的符号链接

- `libfl`：`flex` 库

## 8.15. Tcl-8.6.11

`Tcl` 包包含工具命令语言（Tool Command Language），这是一种强大的通用脚本语言。`Expect` 包用 `Tcl` 语言编写。

**预计编译时间：** 3.7 SBU

**所需磁盘空间：** 80 MB

### 8.15.1. 安装 Tcl

安装此软件包及后续两个（`Expect` 和 `DejaGNU`）是为了支持运行 `binutils`、`GCC` 以及其他软件包的测试套件。为了测试目的安装软件包似乎有些过度，但如果知道最重要的工具运行正常，将会是非常令人放心的，甚至是必不可少的。

首先，使用以下命令解压文档：

```
tar -xf ../tcl8.6.11-html.tar.gz --strip-components=1
```

为编译准备 `Tcl`：

```bash
SRCDIR=$(pwd)
cd unix
./configure --prefix=/usr \
--mandir=/usr/share/man \
$ [ "$(uname -m)" = x86_64 ] && echo --enable-64bit
```

`configure` 选项的含义：

```
$ [ "$(uname -m)" = x86_64 ] && echo --enable-64bit
```

构造部分（<shell command>）被 shell 命令的输出所替换。如果在 32 位机器上运行，该输出为空；如果在 64 位机器上运行，则输出为 `--enable-64bit`。

构建软件包：

```bash
make

sed -e "s|$$SRCDIR/unix/usr/lib|" \
-e "s|$$SRCDIR/unix/usr/include|" \
-i tclConfig.sh

sed -e "s|$$SRCDIR/unix/pkgs/tdbcl.1.2/|/usr/lib/tdbcl.1.2/" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/generic/|/usr/include|" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/library/|/usr/lib/tcl8.6|" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/|/usr/include|" \
-i pkgs/tdbcl.1.2/tdbConfig.sh

sed -e "s|$$SRCDIR/unix/pk/itcl4.2.1/|/usr/lib/itcl4.2.1/" \
-e "s|$$SRCDIR/pkgs/itcl4.2.1/generic/|/usr/include|" \
-e "s|$$SRCDIR/pkgs/itcl4.2.1/|/usr/include|" \
-i pkgs/itcl4.2.1/itclConfig.sh
```

```bash
unset SRCDIR
```

- `tclsh8.6`：Tcl 命令 shell

- `tclsh`：指向 `tclsh8.6`

- `libtcl8.6.so`：Tcl 库

- `libtclstub8.6.a`：Tcl Stub 库

## 8.16. Expect-5.45.4

`Expect` 包包含了通过脚本自动化交互式应用程序，如 `telnet`、`passwd`、`fsck`、`login`。`Expect` 也用于测试这些应用程序，以及其他极其困难的任务。`DejaNu` 框架用 `Expect` 编写。

预计编译时间：0.2 SBU

所需磁盘空间：3.9 MB

### 8.16.1. 安装 Expect

为编译准备 `Expect`：

```bash
./configure --prefix=/usr \
  --with-tcl=/usr/lib \
  --enable-shared \
  --mandir=/usr/share/man \
  --with-tclinclude=/usr/include
```

`configure` 选项的含义：

- `--with-tcl=/usr/lib`：此参数用于告诉 `configure` `telConf.sh` 脚本的位置。

- `--with-tclinclude=/usr/include`：这显式告诉 `Expect` 去哪里寻找 Tcl 的头文件。

构建软件包：

```bash
make
```

要测试结果，执行：

```bash
make test
```

安装软件包：

```bash
make install
ln -svf expect5.45.4/libexpect5.45.4.so /usr/lib
```

### 8.16.2. Expect 的内容

- 安装的程序：`expect`

- 安装的库：`libexpect-5.45.so`

#### 简描述（此处无具体描述）

## 8.17. DejaGNU-1.6

`DejaNu` 框架用 `Expect` 编写，而 `Expect` 用 `Tcl` 编写。

预计编译时间：0.2 SBU

所需磁盘空间：6.9 MB

### 8.17.1. 安装 DejaGNU

为编译准备 `DejaGNU`：

```bash
./configure --prefix=/usr \
  --with-tcl=/usr/lib \
  --enable-shared \
  --mandir=/usr/share/man \
  --with-tclinclude=/usr/include
```

`configure` 选项的含义：

- `--with-tcl=/usr/lib`：此参数用于告诉 `configure` `telConf.sh` 脚本的位置。



进入`/usr/include`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

- `--with-tclinclude=/usr/include`：这显式告诉 Expect 去哪里寻找 Tcl 的头文件。

构建软件包：

```bash
make
```

要测试结果，执行：

```bash
make test
```

安装软件包：

```bash
make install
ln -svf expect5.45.4/libexpect5.45.4.so /usr/lib
```

### 8.17.2. DejaGNU 的内容

- 安装的程序：`expect`

- 安装的库：`libexpect-5.45.so`

#### 简描述（此处无具体描述）

## 8.18. Binutils-2.37

`Binutils`包包含链接器、汇编器和其他工具。

预计编译时间：6.3 SBU

所需磁盘空间：4.5 MB

### 8.18.1. 安装 Binutils

为编译准备 Binutils：

```bash
SRCDIR=$(pwd)
cd unix
./configure --prefix=/usr \
--mandir=/usr/share/man \
$ [ "$(uname -m)" = x86_64 ] && echo --enable-64bit
```

`configure`选项的含义：

```
$ [ "$(uname -m)" = x86_64 ] && echo --enable-64bit
```

构造部分（`<shell command>`）被 shell 命令的输出所替换。如果在 32 位机器上运行，该输出为空；如果在 64 位机器上运行，则输出为 `--enable-64bit`。

构建软件包：

```bash
make
```

```bash
sed -e "s|$$SRCDIR/unix/usr/lib|" \
-e "s|$$SRCDIR/unix/usr/include|" \
-i tclConfig.sh
```

```bash
sed -e "s|$$SRCDIR/unix/pkgs/tdbcl.1.2/|/usr/lib/tdbcl.1.2/" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/generic/|/usr/include|" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/library/|/usr/lib/tcl8.6|" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/|/usr/include|" \
-i pkgs/tdbcl.1.2/tdbConfig.sh
```

```bash
sed -e "s|$$SRCDIR/unix/pk/itcl4.2.1/|/usr/lib/itcl4.2.1/" \
-e "s|$$SRCDIR/pkgs/itcl4.2.1/generic/|/usr/include|" \
-e "s|$$SRCDIR/pkgs/itcl4.2.1/|/usr/include|" \
-i pkgs/itcl4.2.1/itclConfig.sh
```

```bash
unset SRCDIR
```

- **`tclsh8.6`**：Tcl 命令 shell

- **`tclsh`**：指向 `tclsh8.6`

- **`libtcl8.6.so`**：Tcl 库

- **`libtclstub8.6.a`**：Tcl Stub 库

### 8.18.2. Binutils 的内容

- 安装的程序：`expect`

- 安装的库：`libexpect-5.45.so`

# Linux From Scratch - 版本 11

- `ar`: 创建、修改、从归档中提取

- `as`: 汇编器，将 gcc 的输出汇编为对象文件

- `c++filt`: 链接器用于去符号 C++ 和 Java 符号，并防止重载函数冲突

- `dwp`: DWARF 封装工具

- `elfedit`: 更新 ELF 文件的 ELF 头部

- `gprof`: 显示调用分析数据

- `ld`: 链接器，将多个对象文件和归档文件合并为一个文件，重定位其数据并绑定符号引用

- `ld.gold`: `ld`的精简版本，仅支持 elf 文件格式

- `ld.bfd`: `ld`的硬链接

- `nm`: 列出给定对象文件中出现的符号

- `objcopy`: 将其中一种对象文件转换为另一种对象文件，可以通过选项控制特定的显示信息；其显示的信息对正在开发编译工具的程序员有用

- `objdump`: 显示给定对象文件的信息，可以通过选项控制特定的显示信息；其显示的信息对正在开发编译工具的程序员有用

- `ranlib`: 生成归档内容的索引并将其存储在归档中；该索引列出了所有由归档成员（可重定位对象文件）定义的符号

- `readelf`: 显示 ELF 类型二进制文件的信息

- `size`: 列出给定对象文件的段大小和总大小

- `strings`: 输出每个给定文件中长度至少为指定长度的可打印字符序列（默认为四）；对于对象文件，默认只打印初始化和加载部分的字符串，而对于其他类型的文件，它会扫描整个文件

- `strip`: 丢弃对象文件中的符号

- `libbfd`: 二进制文件描述符库

- `libctf`: 兼容 ANSI-C 类型格式调试支持库

- `libctf-nobfd`: `libctf`的变体，不使用 `libbfd`功能

- `libopcodes`: 用于处理操作码的库——即处理器指令的“可读文本”；用于构建如 `objdump`等工具

## 8.19. GMP-6.2.1

`GMP`软件包包含数学库。这些用于任意精度算术的函数非常用用。

预估的编译时间：1.0 SBU

所需的磁盘空间：52 MB

### 8.19.1. 安装 GMP

> 注意

如果你正在为 32 位 x86 编译，但你的 CPU 能够运行 64 位代码且你在环境变量中指定了 `CFLAGS`，则配置脚本将尝试配置为 64 位并失败。通过调用下面的配置 命令可以避免这种情况：

```
ABI=32 ./configure .
```

> 注意

`GMP`的默认设置会产生针对主机处理器优化的库。如果需要处理能力低于主机 CPU 的适用于处理器的库，可以通过运行以下命令创建通用库：

```
cp -v config.sub.guess config.guess
cp -v config.sub.sub config.sub
```

为编译准备 `GMP`：

```bash
./configure --prefix=/usr \
  --enable-cxx \
  --disable-static \
  --docdir=/usr/share/doc/gmp-6.2.1
```

新配置 选项的含义：

- `--enable-cxx`: 此参数启用 C++ 支持

- `--docdir=/usr/share/doc/gmp-6.2.1`: 此变量指定文档的正确位置。

编译软件包并生成 HTML 文档：

```
make
make html
```

> 重要

本节中的 `GMP` 测试套件被认为是关键的。在任何情况下都不要跳过。

测试结果：

```
make check 2>&1 | tee gmp-check-log
```

# Linux From Scratch - 版本 11.0

> `gmp` 中的代码针对其构建时所在的处理器进行了高度优化。偶尔，检测处理器的代码会误判系统能力，导致测试或其他使用 `gmp` 库的应用程序中出现带有““Illegal instruction”（非法指令）消息的错误。在这种情况下，应使用 `--build=x86_64-pc-linux-gnu` 选项重新配置 `gmp` 并重建。

确保测试套件中的所有 197 个测试均通过。通过执行以下命令检查结果：

```
awk '/# PASS:/{total=$3} ; END(print total)' gmp-check-log
```

安装软件包及其文档：

```
make install
make install-html
```

### 8.19.2. GMP 的内容

- 安装的库：`libgmp.so` 和 `libgmpxx.so`

安装目录：`/usr/share/doc/gmp-6.2.1`

#### 简述

- `libgmp` 包含精度数学函数

- `libgmpxx`：包含 C++ 精度数学函数

## 8.20. MPFR-4.1.0

`MPFR`软件包包含多精度数学的函数。

预估的编译时间：0.8 SBU

所需的磁盘空间：38 MB

### 8.20.1. 安装 MPFR

为编译准备 `MPFR`：

```bash
./configure --prefix=/usr \
    --disable-static \
    --enable-thread-safe \
    --docdir=/usr/share/doc/mpfr-4.1.0
```

编译软件包并生成 HTML 文档：

```
make
make html
```

> **重要**

本节中的 `MPFR` 测试套件被认为是关键的。在任何情况下都不要跳过。

测试结果：

```
make check
```

安装软件包及其文档：

```
make install
make install-html
```

### 8.20.2. MPFR 的内容

- 安装的库：`libmpfr.so`

安装目录：`/usr/share/doc/mpfr-4.1.0`

#### 简述

- `libmpfr` 包含多精度数学

## 8.21. MPC-1.2.1

`MPC`软件包包含任意精度复数的库。

预估的编译时间：0.3 SBU

所需的磁盘空间：21 MB

### 8.21.1. 安装 MPC

为编译准备 `MPC`：

```bash
./configure --prefix=/usr \
    --disable-static \
    --sysconfdir=/etc \
    --docdir=/usr/share/doc/mpc-1.2.1
```

编译软件包并生成 HTML 文档：

```
make
make html
```

测试结果：

```
make check
```

安装软件包及其文档：

```
make install
install-html
```

### 8.21.2. MPC 的内容

- 安装的库：`libmpc.so`

安装目录：`/usr/share/doc/mpc-1.2.1`

#### 简述

- `libmpc` 包含精度函数

## 8.22. Attr-2.5.1

`attr`软件包包含管理文件系统扩展属性的工具。

预估的编译时间：0.1 SBU

所需的磁盘空间：4 MB

### 8.22.1. 安装 Attr

为编译准备 `Attr`：

```bash
./configure --prefix=/usr \
    --disable-static \
    --sysconfdir=/etc \
    --docdir=/usr/share/doc/attr-2.5.1
```

编译软件包并生成 HTML 文档：

```
make
make html
```

测试结果：

```
make check
```

安装软件包及其文档：

### 8.22.2. Attr 的内容

- 安装的程序：`attr`, `getattr` 和 `setattr`

- 安装的库：`libattr.so`

安装目录：`/usr/share/doc/attr-2.5.1`

#### 简述

- `attr`：扩展文件系统的扩展属性

- `getattr`：获取文件系统的扩展属性

- `setattr`：设置文件系统的扩展属性

- `libattr` 包含处理扩展属性的库

## 8.23. Acl-2.3.1

`acl`软件包包含管理访问控制列表（ACL）的工具，这些列表用于为文件和目录定义更细粒度的权限。

预估的编译时间：0.1 SBU

所需的磁盘空间：6 MB

### 8.23.1. 安装 Acl

为编译准备 `Acl`：

```bash
./configure --prefix=/usr \
  --disable-static \
  --docdir=/usr/share/doc/acl-2.3.1
```

编译软件包并生成 HTML 文档：

```
make
make html
```

测试结果：

```
make check
```

安装软件包及其文档：

```
make install
```

### 8.23.2. Acl 的内容

- 安装的程序：`chacl`, `getfacl`, `setfacl`

- 安装的库：`libacl.so`

安装目录：`/usr/share/doc/acl-2.3.1`

#### 简述

- `chacl`：更改文件或目录的访问控制列表

- `getfacl`：获取文件访问控制列表

- `setfacl`：设置文件访问控制列表

- `libacl` 包含处理访问控制列表的库

## 2.24. Libcap-2.53

`Libcap`包实现了 Linux 内核中可用的 POSIX 1003.1le 能力（capabilities）的用户空间接口。这些能力将所有强大的 root 权限划分为一组不同的权限。

**预计编译时间：** 耗于 0.1 SBU

**所需磁盘空间：** 3.2 MB

### 2.24.1. 安装 Libcap

防止安装静态库：

```bash
sed -i '/install -m.**STA/d' libcap/Makefile
```

编译该包：

```bash
make prefix=/usr lib=lib
```

`make`选项的含义：

`lib=lib`

此参数将库目录设置为 `/usr/lib`，而不是 x86_64 架构上的 `/usr/lib64`。它对 x86 没有任何影响。

要测试结果，请执行：

```bash
make test
```

安装该包：

```bash
make prefix=/usr lib=lib install
```

调整共享库的权限：

```bash
chmod -v 755 /usr/lib/lib(cap,psx).so.2.53
```

### 2.24.2. Libcap 内容

**安装的程序：** `capsh`, `getcap`, `getpcaps` 和 `setcap`

**安装的库：** `libcap.so` 和 `libpssx`

**短期说明**

- `capsh`: 用于探索和限制能力支持的封装

- `getcap`: 检查文件能力

- `getpcaps`: 显示查询进程（进程）上的能力

- `setcap`: 设置文件能力

- `libcap`: 包含操作 POSIX 1003.1le 能力的库函数

- `libpssx`: 包含支持 pthread 库相关的系统调用 POSIX 语义的函数

## 8.25. Shadow-4.9

`Shadow`包包含了以安全方式处理密码的程序。

预计编译时间：0.2 SBU。所需磁盘空间：45 MB。

### 8.25.1. 安装 Shadow

> 注意：如果你想强制使用强密码，请参考 https://www.linuxfromscratch.org/blfs/view/11.0/postifs/cracklib.html 在构建 Shadow 之前安装 CrackLib。然后在配置命令中添加 `--with-libcrack`。

禁用 `groups`程序及其页面，因为 Coreutils 提供了更好的替代方案。同时防止安装位于 8.3 节“Man-pages-5.13”中的手册。

```bash
sed -i '/s/groups$ (EXEEXT) //' src/Makefile.in
find man -name Makefile.in -exec sed -i '/s/groups\.1 / /' {} \
find man -name Makefile.in -exec sed -i '/s/getspnam\.3 / /' {} \
find man -name Makefile.in -exec sed -i '/s/password\.5 / /' {} \
```

不要使用 crypt 方法，而是使用更安全的 SHA-512 进行密码加密，这允许密码超过 8 个字符。此外，有必要更改当前使用的过旧 `/var/spool/mail` 位置。从 PATH 中移除 `/bin` 和 `/sbin`，因为它们是指向 `/usr` 中对应文件的符号链接。

> 注意：如果由于某些原因倾向于保留 `/bin` 和 `/sbin`，请在 LTS 完成后修改 `.bashrc` 中的 PATH。

```bash
sed -e 's:ENCRYPT_METHOD DES:ENCRYPT_METHOD SHA512: ' \
-e 's:/var/spool/mail:/var/mail:' ' \
-e '/PATH={s/sbin:@;s/bin:@}' \
-i etc/login.defs
```

> 注意：如果你选择构建带有 Cracklib 支持的 Shadow，请运行以下命令：

```bash
sed -i 's:DICTPATH:*:DICTPATH\t/lib/cracklib/pw_dict: ' etc/login.defs
```

通过以下命令修改文件修复简单的编程错误：

```bash
sed -e "224s/rounds/min_rounds/" -i libmisc/salt
```

为编译准备准备 Shadow：

```bash
touch /usr/bin/passwd
./configure --sysconfdir=/ \
--with-group-name-max-length=52
```

# Linux From Scratch - 版本 11.0

`config`选项的含义：

`touch /usr/bin/passwd` 需要存在，因为它的位置在某些程序中是硬编码的，如果不存在默认值是不正确的。

### --with-group-name-max-length=32

最大用户名为 32 个字符。使最大组名也保持相同。

编译该包：

```bash
make
```

此包不带测试套件。

安装该包：

```bash
make exec_prefix=/usr install
make -C man install-man
mkdir -p /etc/default
useradd -D --gid 999
```



## 8.25. 配置 Shadow

此包包含添加、修改和删除用户及组的实用程序；设置和更改它们的密码；执行其他管理任务。关于 shadowing 含义的完整解释，请参阅解压源文件中的 `doc/HOWTO` 文件。使用 Shadow 支持时，请记住需要验证密码的程序（显示管理器、FTP 程序、pop3 守护进程等）必须符合 Shadow 标准。它们需要能够处理加密后的密码（shadowed passwords）。要启用加密密码，请记住需要验证密码的程序（显示管理器、FTP 程序、pop3 守护进程等）必须符合 Shadow 标准。它们需要能够处理加密后的密码。

## 8.26. GCC-11.2.0

`GCC` 软件包包含 GNU 编译器集，其中包括 C 和 C++ 编译器。

预计编译时间：`164 SBU`（包含测试）。所需磁盘空间：`4.3 GB`

### 8.26.1. GCC 的安装

首先，修复一个导致 `libasan` 损坏的问题，在 `Glibc-2.34` 下构建此包时会出现该问题：

```
sed -e '/static.*SIGTSKSZ/d' \
-e '/s/return KStacksize/return SIGTSKSZ * 4/' \
-i libsanitizer/sanitizer_common/sanitizer_posix_libcdep.cpp
```

如果在 `x86_64` 上构建，库的默认目录名称为 "`lib`"：

```
case $ $(uname -m) in
x86_64)
  sed -e '/m64=/s/lib64/lib/' \
  -i.orig gcc/config/i386/t-linux64
esac
```

`GCC` 文档建议在专用目录中构建 `GCC`：

```
mkdir -v build
cd build
```

为编译准备 `GCC`：

```bash
../configure --prefix=/usr \
LD=ld \
  --enable-languages=c,c++ \
  --disable-multilib \
  --disable-bootstrap \
  --with-system-zlib
```

注意，对于所有编程语言，某些先决条件尚未满足。请参考 BLFS `GCC` 页面中关于如何构建 `GCC` 支持的所有语言的说明。

新配置参数的含义：

`LD=ld`

此参数使 `configure` 脚本使用早在本节之前构建的 `binutils` 安装的 `ld`，而不是在其他情况下使用的交叉编译版本。

`--with-system-zlib`

此开关告诉 `GCC` 链接到系统安装的 `zlib` 库副本，而不是其内部副本。

编译该包：

```
make
```

### 重要提示

在本节中，`GCC` 的测试套件被认为是至关重要的。在任何情况下都请不要跳过它。

`GCC` 测试套件中的其中一个测试已知会耗尽默认栈，因此在运行测试之前请增加栈大小：

```
ulimit -s 32768
```

作为非特权用户测试结果，但遇到错误不要停止：

```
chown -Rv tester
su tester -c "PATH=$PATH make -k check"
```

要接收测试套件结果的摘要，请运行：

```
../contrib/test_summary
```

只需要摘要，请通过 `grep -A7 Summ` 输出。

结果可以与位于 `https://www.linuxfromscratch.org/lfs/build-logs/11.0/` 和 `https://gnu.org/ml/gcc-lfs-testresults/` 的结果进行比较。

已知八个与分析器相关的测试失败。

一个名为 `asan_test.C` 的测试已知失败。

在 `libstdc++` 中，有一个名为 `49745.cc` 的测试已知失败，因为 `glibc` 中的头文件依赖发生了变化。

在 `libstdc++` 中，有一个 `numpunct` 测试和六个与 `get_time` 相关的测试已知失败。这些都是因为 `glibc` 中的区域设置（locale）定义发生了变化，但 `libstdc` 目前不支持这些更改。

少数意外的失败是无法避免的。`GCC` 开发人员通常知晓这些问题，但尚未解决它们。除非测试与上述 URL 中的结果非常不同，否则可以继续。

安装该包并删除不必要的目录：

```
make install
rm -rf /usr/lib/gcc/$(gcc-dumpmachine)/11.2.0/include-fixed/bits/
```

现在 `GCC` 目录归 `tester` 所有，安装的头文件目录（及其内容）的所有权是正确的。将所有权更改为 `root` 用户和组：

```
chown -v -R root:root /usr/lib/gcc/*linux-gnu-11.2.0/include-fixed
```

创建 FHS 需要的软链接：

```
ln -svr /usr/bin/cpp /usr/lib
```

添加链接时优化（LTO）构建程序的软链接：

```
ln -sf ../libexec/gcc/$(gcc-dumpmachine)/11.2.0/libto_plugin.so /usr/lib/plugins/
```

现在我们的最终工具链已就绪，确保编译和链接按预期工作非常重要。通过执行一些完整性检查来实现：

```
echo 'int main() {}' > dummy.c
cc dummy.c -v
readelf -l a.out | grep ':lib'
```

应该没有错误，且最后一个命令的输出将（考虑到特定的动态链接器差异：`lib64/ld-linux-x86_64.so.2`）。现在确保我们设置了使用正确的：

```
grep -o '/usr/lib.*crt[1].' dummy.log
```

最后一个命令的输出应该是：

```
/usr/lib/gcc/x86_64-pc-linux-gnu/11.2.0/../../../../lib/crt1.o
/usr/lib/gcc/x86_64-pc-linux-gnu/11.2.0/../../../../lib/crti.o
/usr/lib/gcc/x86_64-pc-linux-gnu/11.2.0/../../../../lib/crt.o
```

根据你的架构，上述可能会略有不同。区别在于 `/usr/lib/gcc` 目录下所有的 `crt*.o` 文件。验证编译器正在搜索正确的头文件：

```
grep -B 4 '^include' dummy.log
```

此命令应该返回：

```
#include <...> search here
/usr/lib/gcc/x86_64-pc-linux-gnu/11.2.0/include
/usr/local/include
/usr/lib/gcc/x86_64-pc-linux-gnu/11.2.0/include
```

再次，名为 `triplet` 的目录可能与上述不同。接下来，验证新的链接器使用了正确的搜索路径：

```
grep 'SEARCH_DIR' dummy.log | sed 's|//g'
```

包含 `-linux-gnu` 的引用应该被忽略，否则最后一个命令的输出应该是：

```
SEARCH_DIR("/x86_64-pc-linux-gnu/lib64")
SEARCH_DIR("/usr/local/lib64")
SEARCH_DIR("/usr/lib/lib64")
SEARCH_DIR("/x86_64-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
```

Linux 32 位系统可能会看到几个不同的目录。例如，这里是 `i686` 机器的输出：

```
SEARCH_DIR("/i686-pc-linux-gnu/lib32")
SEARCH_DIR("/usr/local/lib32")
SEARCH_DIR("/usr/lib32")
SEARCH_DIR("/i686-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
```

确保我们使用的是正确的 `lib`：

```
grep "/libc.so.6" dummy.log
```

最后一个命令的输出应该是：

```
attempt to open /usr/lib/libc.so.6
```

确保 `GCC` 使用正确的动态链接器：

```
grep dummy.log
```

最后一个命令的输出应该是（考虑到动态链接器名称的平台差异）：

```
found ld-linux-x86_64.so.2 at /usr/lib
```

如果输出未所示或完全没有，说明有问题。调查并跟踪步骤以找出问题所在并纠正它。在继续过程之前需要解决任何问题。

一旦一切运行正常，清理测试文件：

```
rm -v dummy.c a.out
```

最后，一个放置错误的文件：

```
mkdir -pv /usr/share/gdb/auto-load
mv -v /usr/lib/*.gdbpy /usr/share/gdb/auto-load/
```

## 8.2.6 GCC 的内容

- 安装的程序：`c++`, `cc`（链接到 `gcc`），`cpp`, `g++`, `gcc-nm`, `gcc-ranlib`, `gcov-dump` 和 `gcov-tool`

- 安装的库：`libsan`, `libc1`, `libgcc`, `gcc_s`, `libgomp`, `libm`, `libsan`, `liblto_plugin`, `libquadmath`, `libsp`, `libstdc++`, `libstdc++fs`, `libstdcc++`, `libsan`.

- 安装的目录：`/usr/include/c++`, `/usr/lib/gcc`, `/usr/libexec/gcc` 以及 `/usr/share/gcc-11.2.0`

## 简短描述

- `c++` C++ 编译器

- `cc`: C 编译器

- `cpp`: C 预处理器；编译器用于展开源文件中的 `#include` 和 `#define` 等语句

- `g++`: C++ 编译器

- `gcc`: C 编译器

- `gcc-ar`: `ar` 的包装器，为命令行工具添加了插件。该程序仅用于“链接时优化”，对默认构建不可用。

- `gcc-nm`: `nm` 的包装器，为命令行工具添加了插件。该程序仅用于“链接时优化”，对默认构建不可用。

- `gcc-ranlib`: `ranlib` 的包装器，为命令行工具添加了插件。该程序仅用于“链接时优化”，对默认构建不可用。

- `gcov`: 覆盖测试工具；它用于分析程序以确定优化效果最显著的地方

- `gcov-dump`: 离线 `gcda` 和 `gnome` dump 工具

- `gcov-tool`: 离线 `gcda` 处理工具

- `libasan`: 地址消毒器运行时库

- `libatomic`: `GCC` 原子运行时库

- `libcc1`: C 预处理库

- `libgcc`: gcc 的运行时支持

- `libgcov`: 当 `GCC` 指令启用分析时，此库会被链接到程序

- `libgomp`: 用于 C/C++ 和 Fortran 多平台共享内存并行编程的 OpenMP API GNU 实现

- `libasan`: 内存泄漏消毒器运行时库

- `liblto_plugin`: `GCC` 链接时优化 (LTO) 插件允许 `GCC` 跨编译单元进行优化

- `libquadmath`: `GCC` 高精度数学库 API

- `libssp`: 包含 `GCC` 栈保护功能的例程

- `libstdc++`: 标准 C++ 库

- `libstdc++fs`: ISO/IEC TS 18822:2015 文件系统库

- `libsupc++`: 为 C++ 语言提供支持例程

- `libtsan`: 线程消毒器运行时库

- `libubsan`: 未定义行为消毒器运行时库

Linux From Scratch - 版本 11

## 8.27. Pkg-config-0.29.2

`pkg-config` 包包含一个工具，用于在软件包安装的 `configure` 和 `make` 阶段将包含路径和/或库路径传递给构建工具。

预估的编译时间：`0.3 SBU`

所需的磁盘空间：`29 MB`

### 8.27.1. Pkg-config 的安装

为编译 `Pkg-config` 做准备：

```
./configure --prefix=/usr \
--with-internal-glib \
--disable-host-tool \
--docdir=/usr/share/doc/pkg-config-0.29.2
```

新 `configure` 选项的含义：

`--with-internal-glib`

这这将允许 `pkg-config` 使用其内部的 Glib 版本，因为 LFS 中没有提供外部版本。

`--disable-host-tool`

此选项禁用了对 `pkg-config` 程序创建不需要的硬链接。

编译软件包：

```
make
```

测试结果：

```
make check
```

安装软件包：

```
make install
```

### 8.27.2. Pkg-config 的内容

安装的程序：`pkg-config`

安装的目录：`/usr/share/doc/pkg-config-0.29.2`

# 要描述

`pkg-config` 返回指定库或软件包的元信息

## 8.28. Ncurses-6.2

`Ncurses` 包包含用于与终端无关字符屏幕处理的库。

预估的编译时间：`0.4 SBU`

所需的磁盘空间：`34 MB`

### 8.28.1. Ncurses 的安装

为编译 `Ncurses` 做准备：

```
./configure --prefix=/usr \
    --mandir=/usr/share/man \
    --with-shared \
    --without-debug \
    --without-normal \
    --enable-pc-files \
    --enable-wide
```

新 `configure` 选项的含义：

`--enable-wide`

此开关会导致构建宽字符库（例如 `libncurses.so.6.2`）而不是普通库（例如 `libncurses.so.6.2`）。这些宽字符库可以在多字节和 8 位本地化中使用，而普通库仅在 8 位本地化中使用。宽字符库和普通库在源码上是的，但在二进制上不兼容。

`--enable-pc-files`

此开关为 `pkg-config` 生成并安装 `.pc` 文件。

`--without-normal`

此开关禁用构建和安装大多数静态库。

编译软件包：

```
make
```

此软件包有一个测试套件，但它只能在软件包安装后运行。测试位于 `test/` 目录。请查看该目录下的 `README` 文件获取更多详情。

安装软件包：

```
make install
```

许多应用程序期望链接器能够找到非宽字符的 `Ncurses` 库。通过符号链接和链接脚本欺骗此类应用程序链接到宽字符库：

```
for lib in ncurses form panel; do
  rm -vf /usr/lib/${lib}.so
  echo "INPUT-${lib}w" > /usr/lib/${lib}.so
  ln -sfv ${lib}.w /usr/lib/pkgconfig/${lib}.so
done
```

Linux From Scratch - 版本 11.0

最后，确保在构建时查找 `-lcurses` 的旧应用程序仍然可以构建：

```
rm -vf /usr/lib/libcurses.so
echo "INPUT(-lncursesew)" > /usr/lib/libcurses.so
ln -sfv libcurses.so /usr/lib/libcurses.so
```

删除一个未被 `configure` 处理的静态库：

```
rm -fv /usr/lib/libncursesw.a
```

如果需要，安装 `Ncurses` 文档：

```
mkdir -v /usr/share/doc/ncurses-6.2
cp -v -R doc* /usr/share/doc/ncurses-6.2
```

> 注意

> 上述指令不会创建非字符 `Ncurses` 库，因为从源码编译安装的任何软件包在运行时都不会链接到它们。然而，已知的链接到非字符 `Ncurses` 库的仅限二进制的应用程序需要版本 5。如果由于某些仅限二进制的应用程序或为了符合 LSB 标准，你必须拥有此类库，请使用以下命令重新构建软件包：

```
make distclean
./configure --prefix=/usr \
--with-shared \
--without-normal \
--without-debug \
--without-cxx-binding \
--with-abi-version=5
make sources libs
cp -av lib*.so.5* /usr/lib
```

### 8.2.2. Ncurses 的内容

`capinfo` (链接到 `tic`), `infocmp`, `infot` (链接到 `tic`), `ncursesw6-config`, `reset` (链接到 `tset`), `tabs`, `tic`, `tpe`, 和 `tset`

安装的程序：

`libcurses.so` (指向 `libcurses.so` 的符号链接和链接脚本), `libformw.so`, `libmenw.so`, `ncursesw.so`, `libpanew.so`, 以及它们在库名中对应的非字符版本 "`w`"。

安装的库：

`/usr/share/tset`, `/usr/share/terminfo`, 以及 `/usr/share/doc/ncurses-6.2`

安装的目录：

# 要描述

- `capinfo`: 将 termcap 描述转换为 terminfo 描述

- `clear`: 清除屏幕

- `infocmp`: 显示 terminfo 描述

- `infot`: 输出 terminfo 描述



### 命令列表

- `ncursesw6-config`: ncursesw6 配置
- `reset`: 重置设置
- `tabs`: 选项卡
- `tic`: 编译 terminfo
- `tpe`: 终端类型打印
- `tset`: 设置终端
- `capinfo`: 将 termcap 描述转换为 terminfo 描述
- `clear`: 清除屏幕
- `infocmp`: 显示 terminfo 描述
- `infot`: 输出 terminfo 描述

## 8.29. Sed-4.8

Sed 包包含一个流编辑器。

预估的编译时间：0.5 SBU

所需的磁盘空间：30 MB

### 8.29.1. Sed 的安装

为编译 Sed 做准备：

```
./configure --prefix=/usr
```

编译软件包并生成 HTML：

```
make
make html
```

测试结果，执行：

```
make check
```

安装软件包及其文档：

```
make install
```

### 8.29.2. Sed 的内容

安装的程序：`sed`

安装的目录：`/usr/share/sed`

# 要描述

`sed`: 单次通过并转换文本

## 8.30. Psmisc-2

Psmisc 包包含用于显示进程信息的程序。

预估的编译时间：0.1 SBU

所需的磁盘空间：5.6 MB

### 8.30.1. Psmisc 的安装

为编译 Psmisc 做准备：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

此软件包没有测试套件。

安装软件包：

```
make install
```

### 8.30.2. Psmisc 的内容

安装的程序：`fuser`, `killall`, `peekfd`, `prstat`, `pslog`, `pstree`, 和 `pstree-x1` (链接到 `pstree`)

# 要描述

- `fuser`: Report使用文件或文件系统的进程 ID (PID)
- `killall`: 按名称杀死进程；向所有发送信号
- `peekfd`: 查看进程的文件描述符
- `prstat`: 输出关于进程的信息
- `pslog`: 进程的当前路径
- `pstree`: 以树的形式显示运行的进程
- `pstree-x1`: 与 `pstree`相同，但等待确认

## 31. Getextte-0.21

Getextte 包包含国际化和本地化工具。这些工具允许程序编译为 NLS（原生语言支持），以便以用户的语言输出。

预估的编译时间：2.9 SBU

所需的磁盘空间：231 MB

### 31.1.1. Getextte 的安装

为编译 Getextte 做准备：

```
./configure --prefix=/usr \
--disable-static \
--docdir=/usr/share/doc/getextte-0.21
```

编译软件包：

```
make
```

测试结果（这需要很长时间，大约3个 SBU），执行：

```
make check
```

安装软件包：

```
make install
chmod -v 0755 /usr/lib/preload_libintl.so
```

### 31.2.2. Getextte 的内容

安装的程序：`autopoint`, `envsubst`, `getext`, `getext.sh`, `gettextize`, `msgattrib`, `msgcat`, `mscgmp`, `msgsubcom`, `msgconv`, `msgen`, `msgexec`, `msgfilter`, `msfmt`, `msggrepp`, `msginit`, `msgmerge`, `msgunfmt`, `msguniqu`, `ngetext`, `recode-sr-latin`, 和 `getextte`

安装的库：`libasprint.so`, `libgettext.so`, `libgetextpo.so`, `libgetextsrc.so`, `libtextstyle.so`, 以及 `preload_libintl.so`

# 要描述

- `autopoint`: 将 Get Getext基础设施文件复制到源码包
- `envsubst`: 替换器字符串中的环境变量
- `getext`: 通过在消息目录中查找将自然语言消息翻译成用户的语言
- `getext.sh`: 主要作为 getext 的 shell 函数库
- `gettextize`: 将所有标准的 Getext 文件拷贝到包的根目录以开始国际化
- `msgattrib`: 根据其属性过滤翻译目录的消息并操作这些属性

# Linux From Scratch - 版本 11.0

`msgcat`

连接并合并给定的 .po 文件

`msgcmp`

比较两个 .po 文件，以检查它们是否包含相同的 msgid 字符串集

`msgcomm`

查找给定 .po 文件中共有的消息

`msgconv`

将翻译目录转换为不同的字符编码

`msggen`

创建一个英语翻译目录

`msgexec`

对翻译目录的所有翻译应用一个命令

`msgfilter`

对翻译目录的所有翻译应用一个过滤器

`msgfmt`

从翻译目录生成二进制消息目录

`msggrep`

从翻译目录中提取匹配给定模式或属于某些源文件的所有消息

`msginit`

创建一个新的 .po 文件，使用用户环境中的值初始化元数据

`msgmerge`

将两个翻译合并到一个文件中

`msgunfmt`

将二进制消息目录反编译为原始翻译文本

`msguniq`

统一翻译目录中的重复翻译

`ngettext`

显示文本消息的母语言翻译，其语法形式取决于一个数字

`recode-sr-latin`

将塞尔维亚语文本从西里尔字母重新编码为拉丁字母脚本

`xget`

从给定的源文件中提取可翻译的消息行，以创建第一个翻译模板

`libasprintf`

定义 autoprint 类，使得 C 格式化输出程序可以在 C++ 程序中使用，并与 <string> 字符串和 <iostream> 流配合

`libgettextlib`

一个包含各种 Gettext 程序使用的常用例程的私有库；这些程序不供通用使用

`libgettextpo`

用于编写处理 .po 文件的特殊程序；当 Gettext 随附的标准应用程序（如 msgcomm、msgcmp、msgattrib 和 msggen）无法满足时，使用此库

`libgettextsrc`

一个包含各种 Gettext 程序使用的常用例程的私有库；这些程序不供通用使用

`libtextstyle`

文本样式库

`preloadable_libintll`

一个用于 LD_PRELOAD 的库，协助 libintl 记录未翻译的消息

# 8.32. Bison-3.7.6

Bison 软件包包含一个解析器生成器。

估计编译时间：6.3 SBU

所需的磁盘空间：53 MB

# 8.32.1. 安装 Bison

为编译准备 Bison：



```
./configure --prefix=/usr --docdir=/usr/share/doc/bison-3.7.6
```

编译软件包：

```
make
```

测试结果（约 5.5 SBU），执行：

```
make check
```

安装软件包：

```
make install
```

# 8.32.2. Bison 的内容

- 安装的程序：`bison` 和 `yacc`
- 安装的库：`liby.a`
- 安装的目录：`/usr/share/bison`

# 简描述

- `bison` 根据一系列规则生成一个用于分析文本文件结构的程序；`bison` 是 Yacc（Yet Another Compiler Compiler）的替代品
- `yacc` `bison` 的包装器，用于仍然调用 `yacc` 而不是 `bison` 的程序；它会带 `-option` 参数调用 `bison`
- `liby` Yacc 库，包含与 Yacc 兼容的 `yerror` 和 `main` 函数的实现；此库通常用不大，但 POSIX 要求使用它

# 8.33. Grep-3.7

Grep 软件包包含用于搜索文件内容的程序。

估计编译时间：0.8 SBU

所需的磁盘空间：36 MB

# 8.33.1. 安装 Grep

为编译准备 Grep：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

测试结果，执行：

```
make check
```

安装软件包：

```
make install
```

# 8.33.2. Grep 的内容

安装的程序：`egrep`、`fgrep` 和 `grep`

# 简描述

- `egrep` 打印匹配扩展正则表达式的行
- `fgrep` 打印匹配固定字符串列表的行
- `grep` 打印匹配基础正则表达式的行

# 8.34. Bash-5.1.8

Bash 软件包包含 Bourne-Again Shell。

估计编译时间：1.6 SBU

所需的磁盘空间：50 MB

# 8.34.1. 安装 Bash

为编译准备 Bash：

```
./configure --prefix=/usr \
--docdir=/usr/share/doc/bash-5.1.8 \
--without-bash-malloc \
--with-installed-readline \
```

新配置选项的含义：

`--with-installed-readline`

此选项告诉 Bash 使用系统已安装的 readline 库，而不是使用自己的 readline 版本。

编译软件包：

```
make
```

如果不运行测试套件，请直接跳到“安装软件包”。

要准备测试，请确保 `tester` 用户可以写入源码树：

```
chown -Rv tester
```

该软件包的测试套件设计为作为非 root 用户运行，该用户拥有连接到标准输入的终端。为了满足这一要求，请使用 Expect 启动一个新的伪终端，并以 `tester` 用户身份运行测试：

```
su -s /usr/bin/expect tester << EOF
set timeout -1
spawn make tests
expect eof
EOF
```

安装软件包：

```
make install
```

# 8.34.2. Bash 的内容

## 8.37. Gperf-3.1

Gperf 根据一组键生成一个完美哈希函数。

预计编译时间：少于 0.1 SBU

所需磁盘空间：6.0 MB

### 8.37.1. 安装 Gperf

为编译准备 Gperf：

```
./configure --prefix=/usr --docdir=/usr/share/doc/gperf-3.1
```

编译软件包：

```
make
```

众所周知，当运行多个并行测试时（`-j` 选项大于 1），测试可能会失败。如需测试结果，请执行：

```
make -j1 check
```

安装软件包：

```
make install
```

### 8.37.2. Gperf 的内容

已安装程序：`gperf`

已安装的目录：`/usr/share/doc/gperf-3.1`

# 简短描述

- `gperf` 从一组键生成完美哈希

## 8.38. Expat-2.4.1

Expat 软件包包含一个用于解析 XML 的流式 C 库。

预计编译时间：0.1 SBU

所需磁盘空间：13 MB

### 8.38.1. 安装 Expat

为编译准备 Expat：

```
./configure --prefix=/usr \
--disable-static \
--docdir=/usr/share/doc/expat-2.4.1
```

编译软件包：

```
make
```

测试结果：

```
make check
```

安装软件包：

```
make install
```

如果需要，安装文档：

```
install -v -m644 doc/*.(html,png,css) /usr/share/doc/expat-2.4.1
```

### 8.38.2. Expat 的内容

- 已安装程序：`xmlwf`
- 已安装的库：`libexpat.so`
- 已安装的目录：`/usr/share/doc/expat-2.4.1`

# 简短描述

- `xmlwf` 是一个非校验的实用程序，用于检查 XML 文档是否格式良好
- `libexpat` 包含用于解析 XML 的 API 函数

## 8.39. Inutils-2.1

Inutils 软件包包含基础网络相关的程序。

预计编译时间：0.3 SBU

所需磁盘空间：30 MB

### 8.39.1. 安装 Inutils

为编译准备 Inutils：

```
./configure --prefix=/usr \
--bindir=/usr/bin \
--localstatedir=/var \
--disable-logger \
--disable-whois \
--disable-rcp \
--disable-rexec \
--disable-login \
--disable-rsh \
--disable-servers
```

配置选项的含义：

`--disable-logger`

此选项防止 Inutils 安装 `logger`（脚本通过该程序将消息传递给系统日志守护进程）。不要安装它，因为 Util-linux 安装了更此版本。

`--disable-whois`

此选项禁用了 Inutils `whois` 客户端的构建，该客户端已过时。关于更佳 `whois` 的说明请参阅 BLFS 书籍。

`--disable-r*`

这些参数禁用了由于安全问题而不应被使用的过时程序的构建。这些程序提供的功能可以通过 BLFS 书中的 `openssh` 软件包提供。

`--disable-servers`

此选项禁用了 Inutils 软件包中包含的各种网络服务器。这些服务器在基础 LFS 系统中被认为是不适当的。它们本质上是不安全的，仅在信任的网络上被认为是安全的。请注意，这些服务器有更好的替代方案。

编译软件包：

```
make
```

测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

将程序移动到正确位置：

```
mv -v /usr/{,}bin/ifconfig
```

### 8.39.2. Inutils 的内容

已安装程序：`dnsdomainname`, `ftp`, `ifconfig`, `hostname`, `ping`, `ping6`, `talk`, `telnet`, `tftp`, `traceroute`

# 简短描述

- `dnsdomainname` 显示系统的 DNS 域名
- `ftp` 是文件传输协议程序
- `hostname` 报告或设置主机名
- `ifconfig` 管理网络接口
- `ping` 发送回显包并测量回复所需的时间
- `ping6` 用于 IPv6 网络的 `ping` 版本
- `talk` 用于与另一个用户聊天
- `telnet` TELNET 协议的接口
- `tftp` 简单的文件传输程序
- `traceroute` 追踪数据包从你工作的主到网络上另一个主机的路由，显示沿途中所有的中间跳（网关）

## 8.40. Less-590

Less 软件包包含一个文本文件查看器。

预计编译时间：少于 0.1 SBU

所需磁盘空间：4.2 MB

### 8.40.1. 安装 Less

为编译准备 Less：

```
./configure --prefix=/usr --sysconfdir=/etc
```

配置选项的含义：

`--sysconfdir=/etc`

此选项告诉软件包创建的程序在 `/etc` 中查找配置文件。

编译软件包：

```
make
```

此软件包不带测试套件。

安装软件包：

```
make install
```

### 8.40.2. Less 的内容

已安装程序：`less`, `lesecho` 和 `lesskey`

# 简短描述

- `less` 文件查看器或分页器；它显示给定文件的内容，允许用户滚动、查找字符串并跳转到标记
- `lesecho` 需要在 Unix 系统的文件名中扩展元字符（如 `*` 和 `?`）
- `lesskey` 用于指定 `less` 的按键绑定

## 8.41. Perl 5.34.0

Perl 软件包包含了实用提取和报告语言（Practical Extraction and Report Language）。

预计编译时间：10 SBU

所需磁盘空间：226 MB

### 8.41.1. 安装 Perl

首先，应用补丁以准备 Perl 编译：

```
patch -p1 < perl-5.34.0.patch
```

```
./configure --prefix=/usr \
--bindir=/usr/bin \
--localstatedir=/var \
--disable-logger \
--disable-whois \
--disable-rcp \
--disable-rexec \
--disable-login \
--disable-rsh \
--disable-servers
```

编译软件包：

```
make
```

测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

将程序移动到正确位置：

```
mv -v /usr/{,}bin/ifconfig
```

### 8.39.2. Inutils 的内容

已安装程序：`dnsdomainname`, `ftp`, `ifconfig`, `hostname`, `ping`, `ping6`, `talk`, `telnet`, `tftp`, `traceroute`

# 简短描述

- `dnsdomainname` 显示系统的 DNS 域名
- `ftp` 是文件传输协议程序
- `hostname` 报告或设置主机名
- `ifconfig` 管理网络接口
- `ping` 发送回显包并测量回复所需的时间
- `ping6` 用于 IPv6 网络的 `ping` 版本
- `talk` 用于与另一个用户聊天
- `telnet` TELNET 协议的接口
- `tftp` 简单的文件传输程序
- `traceroute` 追踪数据包从你工作的主到网络上另一个主机的路由，显示沿途中所有的中间跳（网关）

## 8.40. Less-590



Less 软件包包含一个文本文件查看器。

预计编译时间：少于 0.1 SBU

所需磁盘空间：4.2 MB

### 8.40.1. 安装 Less

为编译准备 Less：

```
./configure --prefix=/usr --sysconfdir=/etc
```

配置选项的含义：

`--sysconfdir=/etc`

此选项告诉软件包创建的程序在 `/etc` 中查找配置文件。

编译软件包：

```
make
```

此软件包不带测试套件。

安装软件包：

```
make install
```

### 8.40.2. Less 的内容

已安装程序：`less`, `lesecho` 和 `lesskey`

# 简短描述

- `less` 文件查看器或分页器；它显示给定文件的内容，允许用户滚动、查找字符串并跳转到标记

- `lesecho` 需要在 Unix 系统的文件名中扩展元字符（如 `*` 和 `?`）

- `lesskey` 用于指定 `less` 的按键绑定

## 8.41. Perl-5.34.0

Perl 软件包包含了实用提取和报告语言（Practical Extraction and Report Language）。

预计编译时间：10 SBU

所需磁盘空间：226 MB

### 8.41.1. 安装 Perl

(注：原文后续部分存在大量重复的 patch 命令和错乱文本，此处已根据核心逻辑翻译并过滤冗余内容)

Perl 安装验证程序；可用于验证 Perl 及其库是否已正确安装

`perlivp`

用于生成发送给 Perl 开发者的感谢邮件

`perthanks`

字符编码转换器 `iconv` 的 Perl 版本

`piconv`

一个用于将 Perl-p1 文件转换为 Perl5 -pm 模块的粗略工具

`pl2pm`

将 pod 格式的文件转换为 HTML 格式

`pod2html`

将 pod 数据转换为格式化的 *roff 输入*

`pod2man`

将 pod 数据转换为格式化的 ASCII 文本

`pod2text`

从文件中嵌入的 pod 文档中打印用例消息

`pod2usage`

检查 pod 格式文档文件的语法

`podchecker`

显示 pod 文档的选定部分

`podselect` 用于针对 Test::Harness 模块运行测试的命令行工具

`prove`

用 Perl 编写的类似 tar 的程序

`ptar`

一个比较提取出的归档与未提取归档的 Perl 程序

`ptardiff`

对 tar 归档中的文件内容应用模式匹配的 Perl 程序

`ptargrep`

打印或检查 SHA 校验和

`shashum`

用于在 Perl 中强制进行详细警告诊断

`splain`

将 Perl XS 代码转换为 C 代码

`xubpp`

显示 Zip 文件的内部结构详情

`zipdetails`

## 8.42. XML::Parser-246

`XML::Parser` 模块是 James Clark 的 XML 解析器 Expat 的 Perl 接口。

近似构建时间：少于 0.1 SBU

所需磁盘空间：2.4 MB

### 8.42.1. 安装 XML::Parser

为编译准备 `XML::Parser`：

```
perl Makefile.PL
```

编译包：

```
make
```

要测试结果，执行：

```
make test
```

安装包：

```
make install
```

### 8.42.2. XML::Parser 的内容

已安装的模块：`Expat.so`

# 要描述

`Expat` 提供 Perl Expat 接口

## 8.43. Intltool-0.51.0

`Intltool` 是一种国际化工具，用于从源文件中提取可翻译的字符串。

近似构建时间：少于 0.1 SBU

所需磁盘空间：1.5 MB

### 8.43.1. 安装 Intltool

首先修复由 per-5.22 及更高版本引起的警告：

```
sed -i 's:\\\\\\\\\\\\\\\\:' intltool-update.in
```

> 注意

上面的正则表达式由于大量的反斜杠而看起来很寻常。它的作用是在序列 \$[' 中的右大括号字符之前添加一个反斜杠，结果变为 \($

为编译准备 `Intltool`：

```
./configure --prefix=/usr
```

编译包：

```
make
```

测试结果：

```
make check
```

安装包：

```
make install -v -Dm644 doc/I18N-HOWTO /usr/share/doc/intltool-0.51.0/I18N-HOWTO
```

### 8.43.2. Intltool 的内容

已安装的程序：`intltool-extract`、`intltool-merge`、`intltool-prepare`、`intltool-update` 和 `intltool`

已安装的目录：`/usr/share/doc/intltool-0.51.0` 和 `/usr/share/doc/intltool`

# 要描述

- `intltoolize` 准备一个使用 `intltool` 的包

- `intltool-extract` 生成供 gettext 读取的头文件

- `intltool-merge` 将字符串合并到各种文件类型

- `intltool-prepare` 更新 pot 文件并与翻译文件合并

- `intltool-update` 更新 po 模板文件并与翻译文件合并

## 8.44. Autoconf-2.71

`Autoconf` 包包含了生成 shell 脚本的程序，这些脚本可以自动配置源代码。

近似构建时间：少于 0.1 SBU（带测试约 7.3 SBU）

磁盘空间：24 MB

### 8.44.1. 安装 Autoconf

为编译准备 `Autoconf`：

```
./configure --prefix=/usr
```

编译包：

```
make
```

要测试结果，执行：

```
make check
```

> 注意

在多核系统上，可以显著缩短 autoconf 的测试时间。要做到这一点，请在上方行后添加 `TESTSUFLAGS=-j<N>`。例如，使用 `-j4` 可以减少 60% 以上的测试时间。

安装包：

```
make install
```

### 8.44.2. Autoconf 的内容

- 已安装的程序：`autoconf`, `autoheader`, `autom4te`, `autoconf`, `autoscan`, `autoupdate` 和 `ifnames`

已安装的目录：`/usr/share/autoconf`

### 短描述

- `autoconf` 生成自动配置软件源代码包的脚本，以适应各种 Unix 类系统；它生成的配置脚本是独立的——运行它们不需要安装 `autoconf` 程序

- `autoheader` 一个用于创建 C #define 语句模板文件的工具，供 configure 使用

- `autom4te` M4 宏处理器的封装

- `autoconf` 按正确顺序运行 `autoconf`、`autoheader`、`aclocal`、`automate`、`gettextize` 和 `libtoolize`

- `autoscan` 扫描源代码的特征并生成 autoconf 模板

- `autoupdate` 更新 autoconf 模板文件

- `ifnames` 为源代码生成头文件

## 8.45. Automake-1

`Automake` 包包含了生成 Makefiles 的程序。

近似构建时间：少于 0.1 SBU（带测试约 8.9 SBU）

所需磁盘空间：15 MB

### 8.45.1. 安装 Automake

为编译准备 `Automake`：

```
./configure --prefix=/usr
--docdir=/usr/share/automake
```

编译包：

```
make
```

测试结果，执行：

```
make -j check
```

安装包：

```
make install
```

### 8.45.2. Automake 的内容

| 已安装的程序 | 已安装的目录 |
| :--- | :--- |
| `aclocal`, `automake`, `automake-m4`, `aidehelper-m4`, `autoconfig.classify`, `autoheader-m4`, `config.guess.m4` | `/usr/share/automake` |

### 短描述

- `aclocal` 根据 `configure.in` 内容生成 `aclocal.m4` 文件

- `automake` 从 `Makefile.am` 生成 Makefiles

- `automake-m4` 用于 automake 的 M4 宏

- `aidehelper-m4` 用于 aidehelper 的 M4 宏

- `autoconfig.classify` 用于 autoconfig 的 M4 宏

- `autoheader-m4` 用于 autoheader 的 M4 宏

- `config.guess.m4` 用于 config.guess 的 M4 宏

## 8.46. Kmod-29

`Kmod` 包包含了加载内核模块的库和工具

近似构建时间：0.1 SBU

所需磁盘空间：12 MB

### 8.46.1. 安装 Kmod

为编译准备 `Kmod`：

```
./configure --prefix=/usr
--sysconfdir=/etc
--with-xz
--with-zstd
--with-zlib
```

这些选项允许 `Kmod` 处理压缩内核模块。

编译包：

```
make
```

此包未提供可在 LFS chroot 环境运行的测试套件。至少需要 `git` 程序，并且许多测试在 git 仓库之外运行。

安装包并为兼容 Module-Init-Tools（以前处理 Linux 内核模块的包）创建符号链接：

```
make install
```

```
for target in depmod insmod modinfo modprobe rmmod; do
ln -sfv ../bin/kmod /usr/sbin/$target
done
```

```
ln -sfv kmod /usr/bin/lsmod
```

### 8.46.2. Kmod 的内容

- 已安装的程序：`depmod`, `insmod`, `kmod`, `lsmod`, `modinfo`, `modprobe` 和 `rmmod`
- 已安装的库：`libkmod.so`

# 短描述

- `depmod` 根据在现有模块集中找到的符号创建依赖文件；该依赖文件被 `modprobe` 用于自动加载所需的模块
- `insmod` 在运行的内核中插入可加载模块
- `kmod` 加载和卸载内核模块
- `lsmod` 列出当前已加载的模块
- `modinfo` 检查与内核模块相关的对象文件并显示其能获取的任何信息
- `modprobe` 使用 `depmod` 创建的依赖文件自动加载相关模块
- `rmmod` 从运行的内核中卸载模块
- `libkmod` 这一库被其他程序用于加载和卸载内核模块

## 8.47. 源自 elfutils-0.185 的 Libelf

`Libelf` 是一个用于处理 ELF（可执行和可链接格式）文件的库。
估计编译时间：0.9 SBU
所需的磁盘空间：115 MB

### 8.47.1. 安装 Libelf

`Libelf` 是 `elfutils-0.185` 软件包的一部分。使用 `elfutils-0.185.tar.bz2` 作为源码 tar 包。

为编译准备 `Libelf`：

```bash
./configure --prefix=/usr \
    --disable-debuginfod \
    --enable-libdebuginfod=dummy
```

编译包：

```bash
make
```

要测试结果，请执行：

```bash
make check
```

仅安装 `Libelf`：

```bash
make -c libelf install
install -vm644 config/libelf.pc /usr/lib/pkgconfig
rm /usr/lib/libelf.a
```

### 8.47.2. Libelf 的内容

已安装的库：`libelf.so`（符号链接）和 `libelf-0.185.so`
已安装目录：`/usr/include/elfutils`

### 简描述

- `libelf` 包含处理 ELF 对象文件的 API 函数

## 8.48. Libffi-3.4.2

`Libffi` 库提供了一个用于各种调用约定的可移植的、高级的编程接口。这允许程序员在运行时调用调用接口描述中指定的任何函数。

**估计编译时间：**2.0 SBU
**所需的磁盘空间：**10 MB

### 48.4.1. 安装 Libffi

> 与 GMP 类似，`libffi` 在构建时会针对正在使用的处理器进行特定优化。如果为另一个系统进行构建，请导出 `CFLAGS` 和 `CXXFLAGS` 以为你的架构指定通用构建。如果未这样做，所有链接到 `libffi` 的应用程序都将触发非法操作错误（Illegal Operation Errors）。

为 `libffi` 准备编译：

```bash
./configure --prefix=/usr \
    --disable-static \
    --with-gcc-arch=native \
    --disable-exec-static-tramp
```

**configure 配置的含义：**

`--with-gcc-arch=native`
确保 GCC 为当前系统进行优化。如果未指定，系统将进行猜测，生成的代码对于某些系统可能不正确。如果生成的代码从原生系统复制到能力较弱的系统，请使用较弱的系统作为参数。有关替代系统类型的详情，请参见 *GCC 手册中的 x86 系统。*

`--disable-exec-static-tramp`
禁用静态蹦板（trampoline）支持。这是 `libffi` 的一项新安全功能，但某些 BLFS 软件包（特别是 GJS 和对象检查）尚未适配该功能。

编译包：

```bash
make
```

要测试结果，请执行：

```bash
make check
```

安装包：

```bash
make install
```

### 48.4.2. Libffi 的内容

**已安装的库：**`libffi.so`

### 简描述

- `libffi` 包含外部函数接口 API 函数

## 8.49. OpenSSL-1.1.11

`OpenSSL` 软件包包含了与加密相关的管理工具和库。这些对于为其他包提供加密函数（例如 `OpenSSH`、电子邮件应用程序和网络浏览器用于访问 HTTPS 网站）非常有用。

估计编译时间：2.2 SBU
所需的磁盘空间：154 MB

### 8.49.1. 安装 OpenSSL

为 `OpenSSL` 准备编译：

```bash
./config --prefix=/usr \
      --opensslldir=/etc/ssl \
      --libdir=lib \
      --shared \
      --zlib-dynamic
```

编译包：

```bash
make
```

要测试结果，请执行：

```bash
make test
```

一个测试 `30_test_afalg` 已知在某些内核配置下会失败（取决于 `CONFIG_CRYPTO_USER_API*` 设置的不一致值）。如果它失败，可以安全地忽略。

安装包：

```bash
sed -i '/INSTALL_LIBS/s/libcrypto.a libssl.a//' Makefile
make MANSUFFIX=install
```

将版本号添加到文档目录名称，以与其他包保持一致：

```bash
mv -v /usr/share/doc/openssl /usr/share/doc/openssl-1.1.11
```

如果需要，安装一些额外的文档：

```bash
cp -vfr doc/* /usr/share/doc/openssl-1.1.11
```

> 注意
> 当发布了修复漏洞的新版本时，你应该更新 `OpenSSL`。发布版本是系列化的，每个初始发布版本都有一个发布版本（例如 1.1.1, 1.1.1a, 1.1.1b, 等）。由于 LFS 仅安装共享库，因此在同一系列中升级时，不需要重新编译链接到 `libcrypto.so` 或 `libssl.so` 的包。
然而，任何链接到这些库的运行程序都需要停止并重启。请阅读第 8.2.1 节中的相关条目。

8.49.2. OpenSSL 的内容

已安装的库：`libcrypto.a` 和 `libssl.a`
已安装的程序：`openssl`
已安装的目录：`/etc/ssl`, `/usr/include/openssl`, `/usr/share/doc/openssl-1.1.11`

### 描述

- `libcrypto.a` 实现了加密算法
- `libssl.a` 实现了传输层安全（TLS）协议
- `openssl` 是一个命令行工具，用于使用各种加密函数

## 8.50. Python-3.9.6

Python 3 软件包包含了开发环境。它用于面向对象编程、编写脚本或开发应用程序。

估计编译时间：4.4 SBU
所需的磁盘空间：260 MB

### 8.50.1. 安装 Python

为 Python 准备编译：

```bash
./configure --prefix=/usr \
    --enable-shared \
    --with-system-expat \
    --with-system-ffi \
```



`--with-pip=yes` \
`--enable-optimizations`

**`configure` 配置的含义：**

`--with-system-expat`
链接到系统的 `Expat`。
`--with-system-ffi`
链接到系统的 `libffi`。
`--with-pip=yes`
构建 `pip` 和 `setuptools`。
`--enable-optimizations`
启用稳定但耗时较大的优化。

编译包：

```bash
make
```

在此处运行测试是不推荐的。测试在部分 LFS 环境下无限挂起。如果需要，可以在本末尾或重新安装 Python 时重新运行。如果仍要运行测试，请执行 `make test`。

安装包：

```bash
make install
```

如果需要，安装预格式化的文档：

```bash
install -v -dm755 /usr/share/doc/python-3.9.6/html
```

```bash
tar --strip-components=1 \
--no-same-owner \
--no-same-permissions \
-n C /usr/share/doc/python-3.9.6/html \
-xvf ../../python-3.9.6-docs-html.bz2
```

### 8.50.2. Python 的内容

已安装的程序：`2to3`, `idle3`, `pip3`, `pydoc3`, `python3` 和 `python3-config`
已安装的库：`libpython3.9.so` 和 `libpython3.so`
已安装的目录：`/usr/include/python3.9`, `/usr/lib/python3` 和 `/usr/share/doc/python-3.9.6`

### 描述

- **`2to3`** 是一个 Python 程序，读取 Python 2.x 源码并应用一系列修复将其转换为有效的 Python 3.x 代码
- **`idle3`** 是一个包装脚本，用于打开 Python 的 GUI 编辑器。要运行此脚本，你必须在安装 Python 之前安装 `Tk`，以便构建 `Tkinter` Python 模块
- **`pip3`** Python 的包安装器。你可以使用 `pip` 从 Python Package Index 其他索引安装包。
- **`pydoc3`** 是 Python 文档工具
- **`python3`** 是一种解释型的、交互式的、面向对象的编程语言

## 8.51. Ninja-1.10.2

`Ninja` 是一个专注于速度的小型构建系统。

预计构建时间：0.2 SBU
所需磁盘空间：64 MB

> 提示
> 如果没有使用 `systemd`，此部分对于 LFS 来说不是强制要求的。另一方面，`ninja` 与 `meson` 结合形成了一个强大的构建系统组合，预计将被使用得越来越频繁。它是 BLFS 书中几个软件包的必需项。

## 8.51.1. 安装 Ninja

运行 `ninja` 时，通常会并行运行最大数量的进程。默认情况下，该数量为系统核心数加二。在某些情况下，这可能会导致 CPU 过热或内存耗尽。如果从命令行运行，传递 `-j` 参数将限制并行进程的数量，但某些软件包启用了 `ninja` 的执行且没有传递 `-j` 参数。

使用下面的优化程序，允许用户通过环境变量 `NINJAJOBS` 限制并行进程的数量。例如，设置：

```
export NINJAJOBS=4
```

将把 `ninja` 限制为四个并行进程。

如果需要，通过运行以下命令添加使用环境变量 `NINJAJOBS` 的能力：

```
sed -i '/int Guess/a \
int j =0;
char* jobs = getenv("NINJAJOBS");
if (j != NULL) j = atoi(jobs);
if (j > 0) return j;
src/ninja.cc
```

使用以下命令构建 Ninja：

```
python3 configure.py --bootstrap
```

构建选项的含义：

```
--bootstrap
这强制 ninja 为当前系统重新构建自身。
```

要测试结果，执行：

```
./ninja ninja_test
./ninja_test --gtest_filter=SubprocessTest.SetWithLots
```

安装软件包：

```
install -vm755 ninja /usr/bin/
install -vDm644 misc/bash-completion /usr/share/bash-completion/completions/ninja
install -vDm644 misc/zsh-completion /usr/share/zsh/site-functions/ninja
```

## 8.51.2. Ninja 的内容

已安装程序：`ninja`

### 简描述

`ninja` 是 Ninja 构建系统

## 8.52. Meson-0.59.1

`Meson` 是一个开源构建系统，旨在既极快速又尽可能对用户友好。

预计构建时间：小于 0.1 SBU
所需磁盘空间：40 MB

> 提示
> 如果没有使用 `systemd`，此部分对于 LFS 来说不是强制要求的。另一方面，`meson/ninja` 是一个强大的构建系统，预计将被使用得越来越频繁。它是 BLFS 书中几个软件包的必需项。

## 8.52.1. 安装 Meson

使用以下命令编译 Meson：

```
python3 setup.py build
```

该软件包不带测试套件。

安装软件包：

```
python3 setup.py install --root=dest
cp -rv dest* /*
install -vdm644 data/shell-completions/bash/meson /usr/share/bash-completion-completions/
install -vdm644 data/shell-completions/zsh/_meson /usr/share/zsh/site-functions/_meson
```

安装参数的含义：
`--root=dest`

默认情况下，`python3 setup.py` 将各种文件（如 man 页）安装到 Python Eggs 中。通过指定的根位置，`setup.py` 将这些文件安装到标准层次结构中。然后可以将该层次结构复制到标准位置。

## 8.52.2. Meson 的内容

已安装程序：`meson`
安装目录：`/usr/lib/python3.9/site-packages/meson-0.59.1-py3.9.egg-info` 和 `/usr/lib/python3.9/site-packages/mesonbuild`

### 简描述

`meson` 一个高生产率构建系统

## 8.53. Coreutils-8.32

`Coreutils` 软件包包含显示和设置基本系统特征的实用。
**预计构建时间：**2.6 SBU
**所需磁盘空间：**153 MB

## 8.53.1. 安装 Coreutils

POSIX 要求 `Coreutils` 中的程序即使在多字节本地化区域中也能正确识别字符边界。以下补丁修复了这一不合规问题以及与其他国际化相关的错误。

```
patch -Npl1 -i ../coreutils-8.32-h18n-1.patch
```

> 笔记本
> 在过去，此补丁中发现了许多错误。在向 `Coreutils` 维护者报告新错误时，请先检查在没有此补丁的情况下是否可以重现。

现在为编译 `Coreutils` 做准备：

```
autoreoconf -fiv
FORCE_UNSAFE_CONFIGURE=1 ./coreutils \
  --prefix=/usr \
  --enable-no-install=kill,uptime
```

配置选项的含义：

```
autoreoconf
```

```
FORCE_UNSAFE_CONFIGURE=1
```
该环境变量允许以 root 用户身份构建软件包。
`--enable-no-install=program,`
该开关的作用防止 `Coreutils` 安装将由其他软件包安装的二进制文件。

编译软件包：

```
make
```

如果不运行测试套件，请跳到“安装软件包”。现在测试套件已准备就绪。首先，运行旨在以用户身份运行的测试：

```
make NON_ROOT=tester
```

我们将以 `tester` 身份运行剩余测试。某些测试要求用户是多个组的成员。如果跳过了这些测试，添加一个临时组 `tester`：

```
echo "dummy:x:tester" >> /etc/group
```

修复某些权限以便非 root 用户可以编译和运行测试：

```
chown -Rv tester
```

现在运行测试：

```
su -c "PATH=$PATH" tester=yes
```

移除临时组：

```
sed -i '/dummy/d' /etc/group
```

安装软件包：

```
make install
```

将程序移动到指定的路径：

```
mv -v /usr/bin /usr/share/man/1/chroot
sed -i "s/1/" /usr/share/man/8/chroot
```

## 8.53.2. Coreutils 的内容

已安装程序：
- `base32` `base64`
- `basename`
- `cat`
- `chrgrp`
- `chown`
- `cksum`
- `comm`
- `cp`
- `csplit`
- `date`
- `dd`
- `df`
- `dir`
- `dircolors`
- `dirname`
- `du`
- `echo`
- `expand`
- `factor`
- `false`
- `fmt`
- `fold`
- `groups`
- `head`
- `hostid`
- `id`
- `install`
- `join`
- `link`
- `ln`
- `logname`
- `ls`
- `md5sum`
- `mkdir`
- `mkfifo`
- `mktemp`
- `pwd`
- `path`
- `realpath`
- `rm`
- `nice`
- `nproc`
- `paste`
- `prime`
- `rsync`
- `sort`
- `sha1sum`
- `shred`
- `sleep`
- `split`
- `stat`
- `sync`
- `tail`
- `timeout`
- `touch`
- `true`
- `truncate`
- `tsort`
- `tty`
- `uniq`
- `users`
- `wc`
- `who`
- `whoami`

已安装库：`libcoreutils.so` (in `/libexec/utils`)

### 简描述

- `base32`：`/usr/bin/test` 命令的别名。编码和解码数据为 base32 规范 (RFC4648)
- `base64`：编码和解码数据为 base64 规范 (RFC4648)
- `b2sum`：打印或检查 BLAKE2 (512位)校验和
- `basename`：从文件名中删除任何路径和指定的后缀
- `cat`：将文件连接到标准输出
- `chchon`：（注意：`chmod`）更改文件和目录的安全上下文
- `chrgrp`：更改文件和目录的组所有
- `chmod`：更改每个文件的权限；模式可以是符号表示或八进制数
- `chown`：更改文件和目录的用户/组所有
- `chroot`：在指定的目录下运行命令
- `cksum`：打印循环冗余检查 (CRC)校验和每个文件的字节计数
- `comm`：比较两个文件，分三列输出唯一和共同行
- `cp`：复制文件
- `csplit`：根据给定模式或行号将文件分成多个新文件
- `cut`：根据字段或位置选择行
- `date`：显示当前时间或设置系统日期
- `dd`：使用块大小和计数复制文件，同时可选对其进行转换
- `df`：报告所有挂载文件系统（以及）或所选文件系统的可用磁盘空间
- `dir`：列出每个给定目录的内容（与 `ls` 命令相同）
- `dircolors`：输出更改 `LS_COLOR` 环境变量以更改 `ls` 方案方案
- `dirname`：从文件名中删除非目录后缀
- `du`：报告当前目录、每个给定目录（包括所有子目录）或给定文件使用的磁盘空间
- `echo`：显示给定的字符串
- `env`：在修改的环境中运行命令
- `expand`：将制表转换为空格
- `expr`：求表达式
- `factor`：打印所有整数的质因数
- `false`：无所事，失败；它始终以指示失败的状态码退出
- `fmt`：重新格式化给定文件的段落
- `fold`：折叠给定文件的行
- `groups`：报告用户的组组成
- `head`：打印每个文件的前十行（或指定的行数）
- `hostid`：报告主机的数字标识符（十六进制）
- `id`：报告当前用户或指定用户的有效 UID、组ID 和组组成
- `install`：复制文件并设置它们的权限模式，如果可能的设置所有者和组
- `join`：合并两个独立文件中相同连接字段的行
- `link`：为文件创建一个指定名称的硬链接
- `ln`：在文件之间创建硬链接或软（符号）链接
- `logname`：报告当前用户的登录名
- `ls`：列出每个给定目录的内容
- `md5sum`：报告或检查消息散列 5 (MD5)校验和
- `mkdir`
- `mkfifo`
- `mktemp`
- `pwd`
- `path`
- `realpath`
- `rm`
- `nice`
- `nproc`
- `paste`
- `prime`
- `rsync`
- `sort`
- `sha1sum`
- `shred`
- `sleep`
- `split`
- `stat`
- `sync`
- `tail`
- `timeout`
- `touch`
- `true`
- `truncate`
- `tsort`
- `tty`
- `uniq`
- `users`
- `wc`
- `who`
- `whoami`

# Linux From Scratch - 版本 11.0

- `mkdir` 创建指定名称的目录
- `mkfifo` 创建指定名称的先入队列（FIFOs），在 UNIX 术语中称为“命名管道”
- `mknod` 创建指定名称的设备节点；设备节点可以是字符特殊文件、块特殊文件或 FIFO
- `mktemp` 以安全方式创建临时文件；用于脚本
- `mv` 移动或重命名文件或目录
- `nice` 以修改后的调度优先级运行程序
- `nl` 对指定文件的行进行编号
- `nohup` 运行忽略挂断信号的命令，其输出被重定向到日志文件
- `nproc` 打印进程可用的处理单元数量
- `numfmt` 将数字转换为八进制或人类可读的字符串
- `od` 以八进制及其他格式倾储文件内容
- `paste` 合并文件，将对应行按顺序并排合并，并用制表符分隔
- `pathchk` 检查文件名是否有效或具有可移植性
- `pinky` 是一个轻量级客户端；它报告有关指定用户的一些信息
- `pr` 为打印文件进行分页和分列处理
- `printenv` 打印环境变量
- `printf` 根据给定的格式打印给定的参数，类似于 C 语言的 `printf` 函数
- `ptx` 从指定文件中打印允许的索引，并带有每个关键词的上下文
- `pwd` 报告当前工作目录的名称
- `readlink` 报告给定的符号链接的值
- `realpath` 打印解析后的路径
- `rm` 如果文件为空则删除文件
- `rmdir` 如果目录为空则删除目录
- `runcon` 以指定的安全上下文运行命令
- `seq` 在给定范围内并按给定的增量打印数字序列
- `sha1` 打印或检查 160 位的安全哈希算法 1 (SHA1) 校验和
- `sha224sum` 打印或检查 224 位安全哈希算法校验和
- `sha256sum` 打印或检查 256 位安全哈希算法校验和
- `sha384sum` 打印或检查 384 位安全哈希算法校验和
- `sha512sum` 打印或检查 512 位安全哈希算法校验和
- `shred` 用复杂模式反复覆盖指定的文件，使数据难以恢复
- `shuf` 乱乱文本行
- `sleep` 暂停指定的时间
- `sort` 排序指定文件的行
- `split` 将指定的文件按大小或行数拆分为多个部分
- `stat` | 显示文件或文件系统状态
- `stdbuf` | 使用更改后的标准流缓冲操作来运行命令
- `stty` | 设置或重置终端行设置
- `sum` | 打印每个指定文件的校验和和块计数
- `sync` | 刷新系统缓冲区；强制将更改的块写入磁盘并更新超级块
- `tac` | 反序连接指定的文件
- `tail` | 打印每个指定文件的最后十行（或指定的行数）
- `tee` | 从标准输入读取内容，同时写入标准输出和指定的指定文件
- `test` | 比较值并检查文件类型
- `timeout` | 在时间限制内运行命令
- `touch` | 修改时间戳，将指定文件的访问和修改时间设置为当前时间；不存在的文件将创建长度为零的文件
- `tr` | 从标准输入翻译、分离并删除给定的字符
- `true` | 什么都不做，并成功执行；它始终以表示成功的状态码退出
- `truncate` | 将文件缩小或扩展到指定大小
- `tsort` 执行拓扑排序；它根据给定文件的部分序关系写入一个完全有序的列表
- `tty` | 报告连接到标准输入的终端文件名
- `uname` | 报告系统信息
- `unexpand` | 将空格转换为制表符
- `uniq` | 忽略连续相同行中的所有重复行
- `unlink` | 删除指定的文件
- `users` | 报告当前登录用户的名称
- `vdir` 等同于 `ls -l`
- `wc` | 报告每个指定文件的行数、单词数和字节数，给出多个文件时显示总计
- `who` | 报告谁正在登录
- `whoami` | 报告与当前有效用户 ID 关联的用户名
- `yes` | 重复输出“y”或指定的字符串，直到被杀死
- `libstdbuf` | `stdbuf` 使用的库

# Linux From Scratch - 版本 11.0

## 8.54. Check-0.15.2

`Check` 是一个用于 C 语言的单元测试框架。

估计构建时间：0.1 SBU（带有测试约为 4.1 SBU）
所占磁盘空间：12 MB

## 8.54.1. 安装 Check

为编译准备 `Check`：

```



`./configure --prefix=/usr --disable-static`

```
构建包：
```

```
make
```

编译已完成。要运行 Check 测试套件，执行以下命令：

```
make check
```

安装包：

```
make docdir=/usr/share/doc/check-0.15.2 install
```

## 8.54.2. Check 的内容

安装的程序：`checkmk`
安装的库：`libcheck.so`

### 简述

- `checkmk`
一个 Awk 脚本，用于生成供 Check 单元测试框架使用的 C 语言单元测试
- `libcheck.{a,so}`
包含允许从测试程序中调用 Check 的函数

## 8.55. Diffutils-3.8

Diffutils 包包含显示文件或目录之间差异的程序。

估计构建时间：0.7 SBU
所占磁盘空间：36 MB

## 8.55.1. 安装 Diffutils

为编译准备 Diffutils：

```
./configure --prefix=/usr
```

编译包：

```
make
```

要测试结果，执行：

```
make check
```

安装包：

```
make install
```

## 8.55.2. Diffutils 的内容

安装的程序：`cmp`, `diff`, `diff3`, `sdiff`

### 简述

- `cmp` 比较两个文件并报告它们是否有差异
- `diff` 比较两个文件并报告哪些行不同
- `diff3` 按行比较三个文件
- `sdiff` 比较两个文件并交互式输出

## 8.56. Gawk-5.0

Gawk 包包含处理文本的程序。

估计构建时间：0.4 SBU
所占磁盘空间：42 MB

## 8.56.1. 安装 Gawk

首先，确保某些未使用的文件未安装：

```
sed -i 's/\//*' Makefile.in
```

为编译准备 Gawk：

```
./configure --prefix=/usr
```

编译包：

```
make
```

要测试结果，执行：

```
make check
```

安装包：

```
make install
```

如果需要，安装文档：

```
mkdir -v /usr/share/doc/gawk-5.0
```

## 8.56.2. Gawk 的内容

安装的程序：`awk` 指向 `gawk` 的链接, `gawk`
安装的库：`filefuncs.so`, `fnmatch.so`, `fork.so`, `inplace.so`, `intdiv.so`, `readdir.so`, `readline.so`, `revoutput.so`, `retext.so`, `time.so`
安装的目录：`/lib/gawk`, `/libexec/awk`, `/share/awk`

### 简述

- `awk` 指向 `gawk` 的链接
- `gawk` 一个处理文本的程序；它是 `awk` 的 GNU 实现

## 8.57. Findutils-..

Findutils 包包含查找文件的程序。这些程序通过递归搜索目录树来创建、维护和搜索数据库（通常比递归查找 `find` 快，但如果数据库没有更新，则是不可靠的）。

估计构建时间：0.9 SBU
所占磁盘空间：52 MB

## 8.57.1. 安装 Findutils

为编译准备 Findutils：

```
./configure --prefix=/usr --localstatedir=/var/lib/locate
```

编译包：

```
make
```

要测试结果，执行：

```
chown -Rv tester .

su tester -c "PATH=$PATH make check"
```

安装包：

```
make install
```

## 8.57.2. Findutils 的内容

安装的程序：`find`, `locate`, `updatedb` 和 `xargs`
安装的目录：`/var/lib/locate`

### 简述

- `find` 在指定的目录树中搜索符合标准的文件
- `locate` 搜索文件名数据库并报告包含给定字符串或匹配给定模式的名称
- `updatedb` 更新 `locate` 数据库；扫描整个文件系统（包括当前挂载的其他文件系统，除非另有说明），并将找到每个文件放入数据库
- `xargs` 可用于将给定的命令应用于文件列表

# 58. Groff-1.22.4

Groff 软件包包含了用于处理和格式化文本的程序。
近似编译时间：0.5 SBU
所需的磁盘空间：88 MB

## 5.58.1. 安装 Groff

Groff 期望环境变量 `PAGE` 包含默认纸张大小。对于美国用户，`PAGE=letter` 是合适的。在其他地方，`PAGE=A4` 可能更合适。虽然默认纸张大小是在编译期间配置的，但可以通过向 `/etc/papersize` 文件中回显“A4”或“letter”来覆盖它。

为 Groff 准备编译：

```
PAGE=<paper_size> .configure --prefix=/usr
```

此软件包不支持并行编译。编译该软件包：

```
make -j1
```

此软件包不附带测试套件。

安装该软件包：

```
make install
```

## 5.58.2. Groff 的内容

已安装的程序：

`addftinfo`, `afmotid`, `chem`, `eqn`, `eqn2graph`, `giffmk`, `glylipond`, `gperl`, `gpinyin`, `graph2graph`, `grn`, `godvi`, `groff`, `gropper`, `grog`, `golbp`, `golji4`, `grops`, `grotty`, `hpfdotinfo`, `indxbib`, `lkbib`, `lookbib`, `mroff`, `neqn`, `nroff`, `pdfdm`, `pdfroff`, `pbtfops`, `pic`, `pic2graph`, `post-grohtml`, `pre-grohtml`, `refer`, `roff2ddi`, `roff2html`, `roff2pdf`, `roff2ps`, `roff2text`, `roff2x`, `soelim`, `tbl`, `tmfotdid` 以及 `troff`

已安装的目录：

`/usr/lib/groff` 和 `/usr/share/doc/groff-1.22.4`, `/usr/share/groff`

# 简述

- `addftinfo`: 读取字体文件并添加一些 groff 系统 使用的额外字体度量信息
- `afmotid`: 创建一个供 groff 使用并分组的字体
- `chem`: 用于生成化学结构图的 Groff 预处理器
- `eqn`: 将嵌入字体输入中的方程描述编译为 `troff` 可理解的命令
- `eqn2graph`: 将 `troff` EQ（方程）转换为裁剪后的图像
- `giffmk`: 标记 `groff/nroff` 文件之间的差异
- `glylipond`: 将 `lylipond` 语言编写的脚本音乐转换为 `groff` 语言
- `gperl`: `groff` 的预处理器，允许在 `groff` 文件中添加 `perl` 代码
- `gpinyin`: `groff` 的预处理器，允许在 `groff` 文件中添加类欧洲的中文拼音
- `grap2graph`: 将图表转换为裁剪后的位图
- `grn`: 用于 `gremlin` 文件的 Groff 预处理器
- `godvi`: 产生 TeX `dvi` 格式的 `groff` 驱动程序
- `groff`: `groff` 格式系统的前端；通常，它运行 `troff` 程序以及适用于选择设备的后处理器
- `groffer`: 在 X 和 y 终端上显示 `groff` 文件和页面
- `grog`: 读取文件并指导打印文件需要哪些 `groff` 选项 `-e`, `-man`, `-me`, `-mm`, `-ms`, `-p`, `-s` 和 `-t`，并报告包含这些选项的 `groff` 命令
- `golbp`: 佳 CAPSL 打印机（LBP-4 和 LBP-8 激光打印机）的驱动程序
- `gojl4`: 适用于 HP LaserJet 4 打印机的 PCL5 格式输出的 `groff` 驱动程序
- `grodf`: 将 GNU `troff` 的输出转换为 PDF
- `grops`: 将 GNU `troff` 的输出转换为 PostScript
- `grotty`: 将 GNU `troff` 的输出转换为适用于打字机设备的格式
- `hpftoid`: 从 HP 标记的度量文件为 `groff-Tlfj` 创建字体文件
- `indbib`: 使用指定的文件为参考文献数据库创建倒排索引
- `lkbib`: 在参考文献数据库中搜索指定的键并报告找到的引用
- `lookbib`: 从标准输入获取关键词并在标准输出打印找到的引用
- `mmrof`: `groff` 的简单预处理器
- `neqn`: 为美国信息代码（ASCII）输出格式化方程
- `nroff`: 使用 `groff` 执行 `noff` 命令的脚本
- `pdfmom`: 封装 `mom` 宏 格式的文件生成 PDF 文档
- `pdfroff`: 使用 `groff` 创建 PDF 文档
- `pfbtops`: 将 `.pbf` 格式的 PostScript 字体转换为 ASCII
- `pic`: 将嵌入 `troff` 或 TeX 输入文件中的图片描述编译为 TeX 或 `troff` 可理解的命令
- `pic2graph`: 将 PIC 图转换为裁剪后的图像
- `post-grohtml`: 将 GNU `troff` 的输出转换为 HTML
- `preconv`: 将输入文件转换为 GNU `troff` 理解的编码
- `pre-grohtml`: 将 GNU `troff` 的输出转换为 HTML
- `refer`: 将文件内容复制到标准输出，但 `.l` 和 `.j` 行解释为引用，`.R1` 和 `.R2` 行解释为处理引用的命令
- `roff2dvi`: 将 `roff` 文件转换为 DVI 格式
- `roff2html`: 将 `roff` 文件转换为 HTML
- `roff2pdf`: 将 `roff` 文件转换为 PDF
- `roff2ps`: 将 `roff` 文件转换为 ps
- `roff2text`: 将 `roff` 文件转换为文本
- `roff2x`: 将 `roff` 文件转换为 x
- `soelim`: 消除 `troff` 文件中的符号
- `tbl`: 处理表格
- `tmfotdid`: 处理 `troff` 文件
- `troff`: `groff` 基础的原始格式化系统

## 8.60. Gzip-1.10

Gzip 软件包包含了用于压缩和解压缩文件的程序。

预计编译时间：0.1 SBU
所需的磁盘空间：19 MB

### 8.60.1. 安装 Gzip

为编译准备 Gzip：

```
./configure --prefix=/usr
```

编译包：

```
make
```

要测试结果，请执行：

```
make check
```

安装包：

```
make install
```

### 8.60.2. Gzip 目录

**已安装的程序：** `gunzip`, `gzexe`, `gzip`, `uncompress` 与 `gzip` 的硬链接, `zcat`, `zcmp`, `zdiff`, `zgrep`, `zfrep`, `zforce`, `zless`, `zmore`, 和 `znew`

# 简要描述

- **gunzip** 解压缩后的文件
- **gzexe** 创建自解压的可执行文件
- **gzip** 使用 Lempel-Ziv `LZ77` 编码压缩给定的文件
- **uncompress** 解压缩压缩过的文件
- **zcat** 将给定的 zip 文件解压到标准输出
- **zcmp** 在压缩文件上运行 `cmp`
- **zdiff** 在压缩文件上运行 `diff`
- **zgrep** 在压缩文件上运行 `grep`
- **zfrep** 在压缩文件上运行 `grep`
- **zforce** 强制为所有给定的 zip 文件添加 gz 扩展名，这样 `gzip` 就不会再次对它们进行压缩；这在文件名在文件传输过程中被截断时非常有用
- **zgrep** 在压缩文件上运行 `grep`
- **zless** 在压缩文件上运行 `less`
- **zmore** 在压缩文件上运行 `more`
- **znew** 将文件从 `compress` 格式重新压缩为 `gzip` 格式。Z 转换为 `.gz`

## 8.61. IPRoute-5.13.0

IPRoute 软件包包含了用于基础和高级基于 IP4 网络的程序。

**预计编译时间：** 0.2 SBU
所需的磁盘空间：15 MB

### 8.61.1. 安装 IPRoute

此包包含的 `arpd` 程序将不会被，因为它依赖于 Berkeley DB，而 LFS 中没有安装它。但是，仍然会安装 `arpd` 目录和 man 手页。运行以下命令来防止这种情况。如果需要 `arpd` 二进制文件，可以在 BL Book 中找到 Berkeley DB 的编译说明，地址为 `https://www.linuxfromscratch.org/blfs/view/11.0/server/db.html`。

```
sed -i /arpd/d Makefile

rm -fv man/man8/arpd.8
```

还需要禁用两个需要 `https://www.linuxfromscratch.org/blfs/view/11.0/postfifs.html.` 的模块：`ss` 和 `tc`

```
sed -i 's/.mipt.o//' tc/Makefile
```

编译包：

```
make
```

此包没有可运行的测试套件。

安装包：

```
mkdir -v /usr/share/doc/iproute2-5.13.0

cp -v COPYING README* /usr/share/doc/iproute2-5.13.0
```

如果需要，安装文档：

### 8.62. IPRoute2 目录

**已安装的程序：** `bridge`, `cstat` 对应 `lnstat`, `gen`, `ifcg`, `ifstat`, `ip`, `lnstat`, `rout`, `routef`, `rtacl`, `rctmon`, `rptr`, `rstat` 对应 `lnstat`, `ss`, 和 `tc`

**已安装的目录：** `/etc/iproute2`, `/usr/lib/tc`, 以及 `/usr/share/doc/iproute2-5.13.0`

# 简要描述

- **bridge** 配置网络桥器
- **cstat** 连接状态工具
- **gen** 通用 netlink 工具前端
- **ifcg** `ip` 命令的 shell 包装器 [注意，它需要从 `http://www.skbuff.net/iputils/` 找到 `iputils` 中的 `arping` 和 `rdisk` 程序]
- **ifstat** 显示接口统计数据，包括每个接口发送和接收的数据包数量

---

# Linux From Scratch - 版本 10.0

主可执行文件。它有几个不同的功能：

- **ip link <device>** 允许用户查看设备状态并进行更改
- **ip addr** 允许用户查看地址及其属性、添加新地址并删除旧地址
- **ip neighbor** 允许用户查看邻居绑定及其属性、添加新邻居条目并删除旧条目
- **ip rule** 允许用户查看路由策略并更改它们
- **ip route** 允许用户查看路由表并更改路由表规则
- **ip tunnel** 允许用户查看 IP 隧道及其属性并更改它们
- **ip maddr** 允许用户查看多播地址及其属性并更改它们
- **ip mroute** 允许用户设置、更改或删除多播路由
- **ip monitor** 允许用户持续监控设备、地址和路由的状态

**Instat** 提供 Linux 网络统计数据；它是旧 **rstat 程序** 的通用且功能更完备的替代品

显示网络统计数据

这是 **ip route** 的一个组件。这用于刷新路由表

这是 **ip route** 的一个组件。这用于列出路由表

显示 `/proc/net/rt_acct` 的内容

- 显示 `/proc/net/rt_acct` 的内容

路由监控工具

将 **ip -o** 的输出转换回可读格式

路由状态工具

类似于 **netstat** 命令；显示活动连接

流量控制可执行文件；这用于服务质量 `QOS` 和服务类别 `COS` 的实现

**tc qdisc** 允许用户设置队列规则

**tc class** 允许用户根据队列规则设置类

**tc estimator** 允许用户估计进入网络的数据流

**tc filter** 允许用户设置 QOS/COS 数据包过滤

**tc policy** 允许用户设置 QOS/COS 策略

## 8.62. Kbd-2.4.0

Kbd 软件包包含了键表文件、控制字体和键盘工具。

预计编译时间：0.2 SBU
所需的磁盘空间：33 MB

### 8.62.1. 安装 Kbd

退格键和删除键的行为在 Kbd 包的不同键图中并不一致。以下补丁修复了 i386 内核的此问题

```
patch -Npl -i ../kbd-2.4.0-backspace-1.patch
```

补丁完成后，退格键生成代码为 127 的字符，删除键生成一个转义序列。

删除冗的 `resizecons` 程序（它防止了失效的 `svgalib` 提供视频模式文件 - 对于正常的 `setfont`，控制台会适当设置）以及它的 man 页。

```
sed -i '/RESIZECONS_PROGS=/s/yes/no/' configure

sed -i 's/resizecons.8 //' docs/man/man8/Makefile.in
```

为编译准备 Kbd：

```
./configure --prefix=/usr --disable-vlock
```

配置 选项的含义：

```
--disable-vlock
```

此选项防止构建 `vlock` 工具，因为它需要 PAM 库，而该库在 chroot 环境中不可用。

编译包：

```
make
```

要测试结果，请执行：
```



make check

```
安装包：
```

make install

```
> 注意：对于某些语言（例如白俄罗斯语），键图假设使用 ISO-8859-5 CP251。此类语言的用户必须单独下载键图。

如果需要，安装文档：
```
mkdir -v /usr/share/doc/kbd
cp -R docs/* /usr/share/doc/kbd
```

### 8.62.2. Kbd 目录

**已安装的程序：** `chvt`, `dealloc`, `dumpkeys`, `fgconsole`, `getkeycodes`, `kbdinfo`, `kbd_mode`, `kbrate`, `loadkeys`, `loadumap`, `openvt`, `psfaddtable` (对应 `psxtable`), `psfgtable`, `psfstriptable` (对应 `psxtable`), `setfont`, `setkeycodes`, `setled`, `metamode`, `setvrgb`, `showconsolefont`, `psxtable`, `unicode_start`, 和 `unicode_stop`

**已安装的目录：** `/usr/share/consolefonts`, `/usr/share/consolestrans`, `/usr/share/keymaps`, `/usr/share/doc/kbd-2.4.0`, 以及 `/usr/share/unimap`

# 简要描述

- **chvt** 切换虚拟终端
- **dealloc** 释放空闲虚拟终端
- **dumpkeys** 打印键表
- **fgconsole** 打印活动虚拟终端编号
- **getkeycodes** 打印内核扫描码映射
- **kbdinfo** 获取控制台信息
- **kbd_mode** 报告或设置键盘模式
- **kbrate** 设置键盘重复和延迟速率
- **loadkeys** 加载键表
- **loadunimap** 加载内核 unicode 到字体映射表
- **openvt** 在新的虚拟终端 (VT) 上启动程序
- **psfaddtable** 为控制字体添加 Unicode 字符表
- **psfgtable** 从控制字体提取嵌入的 Unicode 字符表
- **psfstriptable** 从控制字体移除嵌入的 Unicode 字符表
- **setfont** 修改控制台上的 EGA/VGA 字体
- **setkeycodes** 加载内核扫描码映射条目；当键盘上有特殊键时这非常有用
- **setled** 设置键盘标志和发光二极管 (LED)
- **metamet** 定义键盘元键处理
- **setvrgb** 设置所有虚拟终端的颜色映射
- **showconsolefont** 显示当前的 EGA/VGA 控制台字体
- **showkey** 报告按上的键、扫描码和 ASCII
- **unicode_start** 将键盘和控制台置于 Unicode 模式 [除非键图文件采用 ISO-8859-1 编码，否则不要使用此程序。对于其他编码，此实用程序会产生错误的结果。]
- **unicode_stop** 从 Unicode 模式退出键盘和控制台

## 8.63. Libpipeline-1.5.3

Libpipeline 软件包包含一个用于以灵活且方便的方式操作子进程管道的库。

估算编译时间：0.1 SBU
所需磁盘空间：9.1 MB

### 8.63.1. 安装 Libpipeline

为编译准备 Libpipeline：
```
./configure --prefix=/usr
```
编译软件包：
```
make
```
如需测试结果，请执行：
```
make check
```
安装软件包：
```
make install
```

### 8.63.2. Libpipeline 的内容

已安装的库：`libpipeline.so`

#### 简短描述

- libpipeline：此库用于用于在子进程之间安全地构建管道。

## 8.64. Make-4.3

Make 软件包包含一个程序，用于从源文件控制软件包的可执行文件和其他非源文件的生成。

**估计编译时间：0.6 SBU**
**所需磁盘空间：13 MB**

### 8.64.1. 安装 Make

为编译准备 Make：

编译软件包：
```
make
```
如需测试结果，请执行：
```
make check
```
安装软件包：
```
make install
```

### 8.64.2. Make 的内容

**已安装的程序：** `make`

#### 简短描述

- **make**：自动确定软件包的哪些部分需要（重新）编译，然后发布相关命令。

## 8.65. Patch-2.7.6

Patch 软件包包含一个程序，通过应用通常由 diff 程序创建的“补丁”文件来修改或创建文件。

估算编译时间：0.2 SBU
所需磁盘空间：12 MB

### 8.65.1. 安装 Patch

为编译准备 Patch：
```
./configure --prefix=/usr
```
编译软件包：
```
make
```
如需测试结果，请执行：
```
make check
```
安装软件包：
```
make install
```

### 8.65.2. Patch 的内容

已安装的程序：`patch`

#### 简短描述

- patch：根据补丁文件修改文件（补丁文件通常是用 diff 程序创建的差异列表。通过将这些差异应用到原始文件，patch 创建了补丁版本。）

## 8.66. Tar-1.34

Tar 软件包提供了创建 tar 归档以及执行各种类型归档操作的能力。Tar 可用于之前创建的归档以提取文件、存储额外文件，或更新或列出已存储的文件。

- **估计编译时间：1.9 SBU**
**所需磁盘空间：40 MB**

### 8.66.1. 安装 Tar

为编译准备 Tar：
```
FORCE_UNSAFE_CONFIGURE=1 \
./configure --prefix=/usr
```
configure 选项的含义：

> `FORCE_UNSAFE_CONFIGURE=1`
> 这强制以 root 身份运行 mknod 测试。通常情况下，以用户身份运行此测试被认为是危险的，但由于它是在一个仅部分构建的系统上运行，覆盖它是可以的。

编译软件包：
```
make
```
如需测试结果，
```
make check
```
其中一项测试（功能：二进制存储/恢复）已知在运行时会失败（LFS 缺少 selinux），但如果主机内核不支持用于构建 LFS 的文件系统的扩展属性，则将跳过。

安装软件包：
```
make install
make -C doc install-html docdir=/usr/share/doc/tar-1.34
```

### 8.66.2. Tar 的内容

- **已安装的程序：** `tar`
**已安装目录：** `/usr/share/doc/tar-1.34`

#### 简短描述

- tar：创建、从归档中提取文件并列出归档的内容，也称为 tarballs。

## 8.67. Texinfo-6.8

Texinfo 软件包包含用于读取、写入和转换 info 页面的程序。

估算编译时间：0.6 SBU
所需磁盘空间：112 MB

### 8.67.1. 安装 Texinfo

为编译准备 Texinfo：
```
./configure --prefix=/usr
```
再次，修复一个与 Glibc-2.34 或更高版本保持该软件包的问题：
```
sed -e 's/__attribute_nonnull__/_nonnull_/' \
-i gnulib/lib/malloc/dynarray-skeleton.c
```
编译软件包：
```
make
```
如需测试结果，请执行：
```
make check
```
安装软件包：
```
make install
```
可选地，安装属于 Texinfo 安装的组件：
```
make TEXMF=/usr/share/texmf install-tex
```
参数的含义：
```
TEXMF=/usr/share/texmf
```
Texinfo 的 make 变量持有 TeX 树根目录的位置，例如，一个 Tex 软件包将安装在这里。

Info 文档系统使用纯文本来存储其菜单项列表。该文件位于 `/usr/share/info/dir`。遗憾的是，由于各种软件包 Makefile 中偶尔出现的问题，它有时会与系统上安装的 info 页面不同步。如果需要重建 `/usr/share/info/dir`，以下命令将完成此任务：
```
pushd /usr/share/info
rm -rf dir
for f in *; do
  info -d
done
popd
```

### 8.67.2. Texinfo 的内容

已安装的程序：`info`, `install-info`, `makeinfo`, `teedx`, `tty`, `texfmt`, `texinfo`

已安装的库：`libinfo.so`

已安装目录：`/usr/share/info`

#### 简短描述

- info：读取 info 页面。
- install-info：安装 info 页面。
- makeinfo：生成 info 页面。
- texinfo：将 tex 转换为 info。
- teedx：将 info 转换为 tex。
- tty：处理 texinfo 输入。
- texfmt：格式化 texinfo 页面。
- texinfo：处理 info 页面。

## 8.68. Vim-8.2.3

Vim 软件包包含一个强大的文本编辑器。

**估计编译时间：2.3 SBU**
**所需磁盘空间：19 MB**

> Vim 的替代方案
> 如果你倾向于使用其他编辑器——如 Emacs、Joe 或 Nano——请参阅 https://www.linuxfrom.org/blfs/view/11.0/post/vim.html

### 8.68.1. 安装 Vim

首先，将默认的 `vimrc` 位于 /etc：
```
echo 'set nvim' > /etc/vimrc
```
为编译准备 Vim：
```
./configure --prefix=/usr
```
编译软件包：
```
make
```
为了准备测试，确保 `tester` 用户可以写入源码树：
```
chown -R tester .
```
现在以 `tester` 用户身份运行测试：
```
su tester -c "LANG=en_US.UTF-8 make test" > test.log
```
测试套会在屏幕输出大量数据。通过重定向输出可以避免这个问题。

安装软件包：
```
make install
```
许多用户习惯使用 `vi` 而不是 `vim`。为二进制文件和 man 页创建软链接：
```
ln -sv /usr/bin/vim
for L in /usr/share/man/*1; do
  ln -sv $(dirname $L)/vi
done
```
默认情况下，vim 的文档安装在 /usr/share/doc/。以下软链接允许通过 /usr/share/doc/vim 访问文档：
```
ln -sv ../vim/ /usr/share/doc/vim-8.237
```
如果 LFS 系统要安装 X 窗口，可能需要在安装 X 后重新编译 vim。Vim 自带一个 GUI 版本的编辑器，需要 X 和一些额外的库。更多信息请参阅 vim 文档以及 BLFS 书中的 vim 安装页：https://www.linuxscratch.org/blfs/view/11.0/post/vim.html。

`set incompatible` 让 vim 以更有用的方式（默认）运行，而不是 vi 兼容模式运行。删除“no”以保留旧的行为。`set backspace=2` 允许退格删除换行符、自动缩进和插入开始处。

创建一个默认的 vim 配置文件：
```bash
cat /etc/vimrc << "EOF"
  Begin /etc/vimrc
  确保在自定义设置之前设置默认，而不是之后
  source $VIMRUNTIME/defaults.vim
  let skip_defaults_vim=1
set incompatible
set backspace=2
set mouse=
syntax on
if ($term == "xterm") || ($term == "putty")
  set background=dark
endif
  End /etc/vimrc
EOF
```

```
### 注意

默认情况下，vim 只安装了英语的拼写文件。要安装你喜爱语言的拼写文件，请从 http://ftp.vim.org/pub/runtime/spell/ 下载对应语言和字符编码的 *.spl 文件以及可选的 *.s 文件，并将它们保存到 `/usr/share/vim/vim82/spell/`。

要使用这些拼写文件，需要在 `/etc/vimrc` 中进行一些配置，例如：
```
set spellang=en,ru
set spell
```
欲更多信息，请参考上述 URL 对应的 README 文件。

## 8.6.3. Vim 的内容

- 已安装的程序：`ex`（链接到 vim）、`rview`（链接到 vim）、`rvim`（链接到 vim）、`vi`（链接到 vim）、`view`（链接到 vim）、`vim`、`vimdiff`（链接到 vim）、`vimtutor` 以及 `xxd`

- 已安装目录：`/usr/share/vim`

# 简述

- ex: 以 ex 模式启动 vim

- review: 是 view 的受限版本；不能启动 shell 命令且 view 不能挂起

- rvim: 是 vim 的受限版本；不能启动 shell 命令且 vim 不能挂起

- vi: 链接到 vim

- view: 以只读模式启动 vim

- vim: 是编辑器

- vimdiff: 使用 vim 编辑两个或三个版本的的文件并显示差异

- vimtutor: 教授 vim 的基础键和命令

- xxd: 创建给定文件的十六进制转储；它也可以反向操作，因此用于二进制补丁

## 8.69. Eudev-3.2.10

Eudev 软件包包含动态创建设备节点的程序。

近似编译时间：0.2 SBU

所需磁盘空间：80 MB

### 8.69.1. 安装 Eudev

为编译 Eudev 准备：
```
./configure --prefix=/usr \
  --bindir=/usr/sbin \
  --sysconfdir=/etc \
  --enable-manpages \
  --disable-static
```
编译软件包：
```
make
```
现在创建测试所需的目录，这些目录也将作为安装的一部分使用：
```
mkdir -pv /usr/lib/udev/rules.d
mkdir -pv /etc/udev/rules.d
```
要测试结果，执行：
```
make check
```
安装软件包：
```
make install
```
安装一些在 LFS 环境中有用的自定义规则和支持文件：
```
tar -xvf ../udev-lfs-20171102.tar.xz
make -f udev-lfs-20171102/Makefile.lfs install
```

### 8.69.2. 配置 Eudev

硬件设备的信息维护在 `/etc/udev/hwdb.d` 和 `/usr/lib/hwdb.d` 中。Eudev 需要这些信息将其编译为二进制数据库 `/etc/udev/hwdb.bin`。创建初始数据库：
```
udevadm hwdb --update
```
每次更新硬件信息时，都需要运行此命令。

### 8.69.3. Eudev 的内容

- 已安装的程序：`udevadm` 和 `uudev`

- 已安装的库：`libudev.so`

- 已安装的目录：`/etc/udev`、`/usr/lib/udev` 以及 `/usr/share/doc/udev-lfs-20171102`

# 简述

**udevadm** 通用 udev 管理工具：控制 udev 守护进程，提供来自 Udev 数据库的信息，监控 uevents，等待 uevents 完成，测试 Udev 配置并为给定设备触发 uevents

**udevd** 在 netlink 套字上监听 uevents 的守护进程，创建设备并响应这些 uevents 运行配置的外部程序

**libudev** 指向 udev 设备信息的库接口

**/etc/udev** 包含 Udev 配置文件、设备权限和设备命名规则

## 70. Man-DB-2.9.4

Man-DB 软件包包含查找和查看帮助页（man pages）的程序。

近似编译时间：0.4 SBU

所需磁盘空间：38 MB

### 8.70.1. 安装 Man-DB

为编译 Man-DB 准备：
```
./configure --prefix=/usr
--doccdir=/usr/share/doc/man-db-2.9.4
--sysconfdir=/etc
--disable-setuid
--enable-cache-owner=bin
--with-browser=/usr/bin/lynx
--with-vgrind=/usr/bin/vgrind
--with-grap=/usr/bin/grap
--with-systemdtmpfilesdir=
--with-systemdunitdir=
```
配置选项的含义：

--disable-setuid



此选项禁用 `man` 程序设置 `setuid` 为用户 `man`。

`--enable-cache-owner=bin`

这使得系统范围的缓存文件所有者变为用户 `bin`。

`--with-...`

这些参数用于设置默认参数。`lynx` 是一个基于文本的浏览器（安装说明请参考 BLFS），`vgrind` 将程序转换为 Groff 输入，而 `grap` 对于在 Groff 文档中排版图表非常有用。在查看帮助页时通常不需要 `vgrind` 和 `grap` 程序。它们不是 LFS 或 BLFS 的一部分，但如果你想这样做，应该在完成 LFS 之后安装它们。

`--with-systemd...`

编译软件包：

```
make
```

要测试结果，执行：

```
make check
```

安装软件包：

```
make install
```

### 8.70.2. 非英语帮助页

下表显示了 Man-DB 假设安装在 `/usr/share/man/` 下的帮助页字符集。此外，Man-DB 还能正确确定安装在该目录下的帮助页是否为 UTF-8 编码。

# 旧位帮助页编码

| 语言 (代码) | 编码 | 语言 (代码) | 编码 |
| :--- | :--- | :--- | :--- |
| 丹语 | ISO-8859-1 | 克罗地亚语 | ISO-8859-2 |
| 德语 | ISO-8859-1 | 匈牙利语 | ISO-8859-2 |
| 英语 | ISO-8859-1 | 日本语 | EUC-JP |
| 西班牙语 | ISO-8859-1 | 韩语 | EUC-KR |
| 爱沙兰语 | ISO-8859-1 | 立陶宛语 | ISO-8859-13 |
| 芬兰语 | ISO-8859-1 | 拉脱维亚语 | ISO-8859-13 |
| 法语 | ISO-8859-1 | 马其顿语 | ISO-8859-5 |
| 爱尔兰语 | ISO-8859-1 | 波兰语 | ISO-8859-2 |
| 银河语 | ISO-8859-1 | 罗马语 | ISO-8859-2 |
| 印尼语语 | ISO-8859-1 | 俄罗斯语 | KOI-R |
| 冰岛语 | ISO-8859-1 | 斯洛伐克语 | ISO-8859-2 |
| 意大利语 | ISO-8859-1 | 斯洛文尼亚语 | ISO-8859-2 |
| 挪威语 (nb) | ISO-8859-1 | 塞尔维语 (latin) | ISO-8859-2 |
| 荷兰语 | ISO-8859-1 | 塞尔维语 | ISO-8859-5 |
| 挪威语 (nn) | ISO-8859-1 | 土耳其语 | ISO-8859-9 |
| 挪威语 (no) | ISO-8859-1 | 乌克兰语 | KOI-U |
| 葡萄牙语 | ISO-8859-1 | 越南语 | CPVC1252 |
| 瑞典语 | ISO-8859-1 | 简体中文 (zh_CN) | GBK |
| 白俄罗斯语 | CP1251 | 简体中文 (zh_SG) | GBK |
| 保加利亚语 | CP1251 | 繁体中文 (zh_HK) | BIG5 |
| 捷克语 | ISO-8859-2 | 繁体中文 (zh_TW) | BIG5 |
| 希腊语 | ISO-8859-7 | | |

注意：不支持列表中语言的帮助页。

## 8.70.3. Man-DB 的内容

- 已安装的程序：`accessdb`、`apropos`（链接到 `whatis`）、`catman`、`lerog`、`man`、`mandb`、`manpath` 以及 `whatis`
- 已安装的库：`libman.so` 和 `libmandb.so`（均在 `/usr/lib/man-db`）
- 已安装的目录：`/usr/lib/man-db`、`/usr/libexec/man-db` 以及 `/usr/share/doc/man-db-2.9.4`

# 简述

`accessdb` 以人类可读格式转储 `whatis` 内容

`apropos` 搜索 `whatis` 数据库并显示包含给定字符串的系统命令摘要

`catman` 创建或更新预格式帮助页

`lerog` 显示给定帮助页的单行摘要

`man` 格式化并显示请求的帮助页

`mandb` 创建或更新 `whatis` 数据库

`manpath` 显示 `$MANPATH` 的内容或 `whatis` 搜索 `whatis` 数据库并显示包含给定关键词作为独立单词的系统命令

`libman` 包含 `man` 的运行时支持

`libmandb` 包含 `man` 的运行时支持

## 8.1. Proccs-ng-3.3.17

`Proccs-ng` 软件包包含监控进程的程序。

注意：此软件包提取到目录 `proccs-3.3.17`，而不是预期的 `proccs-ng-3.3.17`。

近似编译时间：0.5 SBU

所需磁盘空间：19 MB

### 8.1.1. 安装 Proccs-ng

为编译 `proccs-ng` 准备：

```
./configure --prefix=/usr \
--docdir=/usr/share/doc/proccs-ng-3.3.17 \
--disable-static \
--disable-kill
```

配置选项的含义：

`--disable-kill` 此开关禁用构建由 Util-linux 软件包安装的 `kill` 命令。

编译软件包：

```
make
```

运行测试套件，执行：

```
make check
```

已知五个与 `pkill` 相关的测试会失败，由于未更新的测试的问题。

安装软件包：

```
make install
```

### 8.1.2. Proccs-ng 的内容

已安装的程序：`free`、`pgrep`、`pidof`、`pkill`、`ps`、`pwdx`、`slabtop`、`sysctl`、`tload`、`top`、`vmstat` 以及 `watch`

已安装的库：`proccs.so`

已安装的目录：`/usr/include/proc` 以及 `/usr/share/doc/proccs-ng-3.3.17`

### 简述

- `free` 报告系统中空闲和已使用的内存（包括物理内存和交换内存）
- `pgrep` 根据名称和其他属性查找进程
- `pidof` 报告给定程序的 PID
- `pkill` 根据名称和其他属性向进程发送信号
- `pmap` 报告给定进程的内存映射
- `ps` 列出当前运行的进程
- `pwait` 在执行前等待进程结束
- `pwdx` 报告进程当前的工作目录
- `slabtop` 实时显示详细的内核 slab 缓存信息
- `sysctl` 在运行时修改内核参数
- `tload` 打印当前系统负载平均值的图表
- `top` 显示最消耗 CPU 的密集型进程列表；它提供了对处理器活动的的实时查看
- `uptime` 报告系统运行了多久、登录了多少个用户以及系统负载平均值
- `vmstat` 报告虚拟内存统计信息，提供关于进程、内存、分页、块级输入/输出 (IO)、陷阱 (traps) 和 CPU 活动的信息
- `w` 显示哪些用户当前登录、在何处登录以及何时登录
- `watch` 重复运行给定命令，并显示其输出的第一屏内容；这允许用户观察输出随时间推移的变化
- `libprocps` 包含此包中大多数程序使用的函数

## 8.72. Util-linux-2.372

`Util-linux` 软件包包含各种杂项实用程序。其中包含了处理文件系统、控制台、分区和消息的工具。

**近似编译时间：** 1.1 SBU

**所需磁盘空间：** 261 MB

### 8.72.1. 安装 Util-linux

为编译准备 `Util-linux`：

```bash
./configure ADJTIME_PATH=/var/lib/hwclock \
    --libdir=/usr/lib \
    --docdir=/usr/share/doc/util-linux-2.37.2 \
    --disable-chfn-chsh \
    --disable-login \
    --disable-nologin \
    --disable-su \
    --disable-setpriv \
    --disable-runuser \
    --disable-pylibmount \
    --disable-static \
    --without-python \
    --without-systemd \
    --without-systemdsunitdir \
    runstated=run
```

`--disable` 和 `--without` 选项可以防止在构建需要 LFS 中不存在的包或与其他包安装的程序不一致的组件时出现警告。

编译包：

```bash
make
```

如果需要，以非 root 用户身份运行测试套件：

> 警告：以 root 用户身份运行测试套件会对系统产生危害。要运行它，当前运行的系统中必须可用内核 CONFIG_SCSI_DEBUG 选项，并且必须以模块形式构建。将其构建进内核会导致无法启动。为了完全覆盖，必须安装其他 BLFS 包。如果需要，可以在重启进入完成的 LFS 系统并运行以下命令后进行测试：

```bash
bash tests/run.sh --scrdir=$PWD --builddir=$PWD
```

### 注意

有一个测试在 chroot 环境中失败并导致测试无限挂起。问题在 chroot 环境外不会发生。要解决此问题，请删除该测试：

```bash
rm tests/ts/lsns/ioctl_ns
chown -Rv tester .
su tester -c "make -k check"
```

安装包：

```bash
make install
```

## 8.72. Util-linux 目录

已安装的程序：

`addpart`, `agetty`, `bldiscard`, `blkid`, `blkzone`, `blockdev`, `cal`, `cfdisk`, `cpchu`, `chemem`, `choom`, `chrt`, `col`, `colert`, `colm`, `column`, `crtlalld`, `delpart`, `dmesg`, `evict`, `allocate`, `fformat`, `fincore`, `findsind`, `findmnt`, `flock`, `fsk`, `fck-kramfs`, `fck-minix`, `fsfree`, `fstrim`, `hexdup`, `hwclock`, `i386`, `ionice`, `ipcmk`, `ipcrm`, `ips`, `isozlice`, `kill`, `last`, `last` (链接到列表), `lddatch`, `linux32`, `linux64`, `logger`, `look`, `losetup`, `isblk`, `islspu`, `islocks`, `lslogins`, `lsnsns`, `mseek`, `meskg`, `mkfs`, `mks-bfs`, `mks-kramfs`, `mkfs-minix`, `mkswap`, `more`, `mount`, `mountpoint`, `namei`, `isnter`, `parts`, `pivot_root`, `plimit`, `raw`, `readprofile`, `rename`, `resize`, `respart`, `rev`, `rftkill`, `script`, `scriptplay`, `setarch`, `setch`, `setter`, `sfdisk`, `swolin`, `swapon`, `swappoff` (链接到 spawn), `switch`, `switch_root`, `taskset`, `ul`, `umount`, `uname26`, `share`, `utmdup`, `uuid`, `uuidigen`, `uisparse`, `wall`, `wdtl`, `wepeif`, `x86_64`, 以及 `zraml`

已安装的库：

已安装的目录：

`/usr/include/blkid`, `/usr/include/bfdisk`, `/usr/include/mount`, `/usr/include/blkid.so`, `libdisk.so`, `libsmartsols.so`, 和 `libuid.so`

`libsmartsols/usr/share/doc/util-linux-2.37.2`, 以及 `/var/lib/hwclock`

# 描述

| 命令 | 描述 |
| :--- | :--- |
| `addpart` | 通知 Linux 内核新分区 |
| `agetty` | 打开 tty，提示登录名并调用登录程序 |
| `bldiscard` | 丢弃设备上的扇区 |
| `blkid` | 用于定位和打印块设备属性的命令行工具 |
| `blkzone` | 在给块上运行 zone 命令 |
| `blockdev` | 允许用户从命令行调用块设备 ioctls |
| `cal` | 显示日历 |
| `cfdisk` | 简单的磁盘分区编辑器 |
| `cpchu` | 配置 CPU 亲和性 |
| `chemem` | 管理内存 |
| `choom` | 调整 OOM-killer 分数 |
| `chrt` | 为程序设置实时优先级 |
| `col` | 过滤冗余行 |
| `colert` | 将文本转换为彩色 |
| `colm` | 将输出格式化为多列 |
| `column` | 将输入格式化为列 |
| `crtlalld` | 控制 Ctrl+Alt+Del |
| `delpart` | 删除分区 |
| `dmesg` | 打印内核缓冲区 |
| `evict` | 从缓存中驱除页 |
| `allocate` | 在文件中分配空间 |
| `fformat` | 以十六格式化文件 |
| `fincore` | 读取内核分析信息 |
| `findsind` | 查找实例 |
| `findmnt` | 列出挂载文件系统的信息 |
| `flock` | 获取文件锁 |
| `fsk` | 检查文件系统完整性 |
| `fck-kramfs` | 检查 kramfs 文件系统 |
| `fck-minix` | 检查 minix 文件系统 |
| `fsfree` | 报告空闲空间 |
| `fstrim` | 修剪文件系统 |
| `hexdup` | 重复十六进制 |
| `hwclock` | 设置硬件时钟 |
| `i386` | 32 位兼容性 |
| `ionice` | 设置 I/O 调度类 |
| `ipcmk` | 创建 IPC 资源 |
| `ipcrm` | 移除 IPC 资源 |
| `ips` | 提供 IPC 状态 |
| `isozlice` | 处理 iso |
| `kill` | 向进程发送信号 |
| `last` | 显示登录的用户 |
| `last` (链接到列表) | 显示登录尝试 |
| `lddatch` | 附加行律 |
| `linux32` | 32 位兼容性 |
| `linux64` | 64 位兼容性 |
| `logger` | 向日志记录消息 |
| `look` | 显示以字符串开头的行 |
| `losetup` | 设置并控制循环设备 |
| `isblk` | 列出所有块设备 |
| `islspu` | 输出 架构 |
| `islocks` | 列出本地锁 |
| `lslogins` | 显示用户信息 |
| `lsnsns` | 列出命名空间 |
| `mseek` | 列出可用内存范围 |
| `meskg` | 向其他用户发送消息 |
| `mkfs` | 在设备上创建文件系统 |
| `mks-bfs` | 创建 bfs 文件系统 |
| `mks-kramfs` | 创建 cramfs 文件系统 |
| `mkfs-minix` | 创建 Minix 文件系统 |
| `mkswap` | 初始化交换区域 |
| `more` | 分页文本 |
| `mount` | 挂载文件系统 |
| `mountpoint` | 检查是否为挂载点 |
| `namei` | 显示符号链接 |
| `nsenter` | 在命名空间中运行 |
| `partx` | 告诉内核分区 |
| `pivot_root` | 使系统成为新根 |
| `plimit` | 获取和设置资源限制 |
| `raw` | 绑定原始字符设备 |
| `readprofile` | 读取内核分析 |
| `rename` | 重命名文件 |
| `renice` | 更改进程优先级 |
| `respart` | 请求内核调整分区 |
| `rev` | 反转行 |
| `rtkill` | 启用/禁用无线设备 |
| `script` | 制作脚本 |
| `scriptplay` | 回放脚本 |
| `setarch` | 设置架构 |
| `setch` | 设置时间 |
| `setter` | 设置用户属性 |
| `sfdisk` | 简单的磁盘分区编辑器 |
| `swolin` | 显示交换状态 |
| `swapon` | 启用交换 |
| `swappoff` | 禁用交换 |
| `switch` | 切换用户 |
| `switch_root` | 切换根文件系统 |
| `taskset` | 设置 CPU 亲和性 |
| `ul` | 实用程序列表 |
| `umount` | 卸载文件系统 |
| `uname26` | 打印系统信息 |
| `share` | 共享文件 |
| `utmdup` | 转储 utmp 文件 |
| `uuidigen` | 生成 UUID |
| `uisparse` | 解析选项 |
| `wall` | 向所有用户发送消息 |
| `wdtl` | 看门狗计时 |
| `wepeif` | 启用/禁用接口 |
| `x86_64` | 64 位工具 |
| `zraml` | 压缩内存磁盘工具 |

# Linux From Scratch - Version 11

- `setarch`

在新的程序环境中报告架构并设置个性化标志

- `setid`

在新会话中运行给定的程序

- `setterm`

设置终端属性

- `sfdisk`

一个磁盘分区表操作器

- `sulogin`

允许 root 登录；它通常在系统进入单用户模式时由 init 调用

- `swaplabel`

允许更改交换区域的 UUID 和标签

- `swappoff`

禁用用于分页和交换的设备和文件

- `swapon`

启用用于分页和交换的设备和文件，并列出当前正在使用的设备和文件

- `switch_root`



切换到另一个文件系统作为挂载树的根节点

- `tailf`

跟踪日志文件的增长；显示日志文件的最后 10 行，然后在新条目创建时继续显示日志中的任何新内容

- `taskset`

获取或设置进程的 CPU 亲和性

- `ul`

一种过滤器，用于将下划线转换为表示当前终端下划线的转义序列

- `umount`

从系统文件树中断开文件系统

- `uname2`

指向 `stat` 的符号链接

- `unshare`

在共享父进程某些命名空间的情况下运行程序

- `utmpdump`

以用户友好的格式显示给定日志文件的内容

- `uuidid`

UUID 库使用的守护进程，用于以安全且保证唯一的方式生成基于时间器 UUID

- `uuidgen`

创建新的 UUID。每个 UUID 在本地系统和其他系统（包括过去和未来）创建的所有 UUID 之间，都可以合理地被认为是唯一的

- `uuidparse`

一个用于解析唯一标识符的工具

- `wall`

在所有当前登录用户的终端上显示文件内容（或默认情况下显示标准输入）

- `wdctl`

显示硬件看门狗状态

- `whereis`

报告给定命令的二进制文件、源码和手册页的位置

- `wipes`

从设备上擦除文件系统签名

- `x86_64`

指向 `i86` 的符号链接

- `zramctl`

一个用于设置和控制 zram（压缩内存磁盘）设备的程序

- `libblkkid`

包含设备识别和令牌提取的例程

- `libdisk`

包含操作分区表的例程

- `libmount`

包含块设备挂载和卸载的例程

- `libsmartcols`

包含以表格格式对齐屏幕输出的例程

- `libuuid`

包含为可能在本地系统之外的对象生成唯一标识符的例程

## 8.73. E2fsprogs-1.46.4

`e2fsprogs` 包包含处理 ext2 文件系统的工具。它还支持 ext3 和 ext4 日志文件系统。

预计构建时间：机械硬盘上为 4.4 SBU，在 SSD 上为 1.5 SBU

所需磁盘空间：93 MB

### 8.73.1. 安装 E2fsprogs

`e2fsprogs` 文档建议在源码树的子目录中构建包：

```
mkdir -v build
cd build
```

为编译 `e2fsprogs` 做好准备：

```
./configure --prefix=/usr
    --sysconfdir=etc
    --enable-elf-shlibs
    --disable-libblkid
    --disable-libuuid
    --disable-uuid
    --disable-fsck
```

`configure` 选项的含义：

- `--enable-elf-shlibs`

这创建了该包中某些程序使用的共享库。

- `--disable-*`

这防止 `e2fsprogs` 构建并安装 `libuuid` 和 `libblkid` 库、`uuid` 守护进程以及 `fschck` 封装，因为 `util-linux` 安装了更更新的版本。

编译包：

```
make
```

运行测试，执行：

```
make check
```

其中一个测试 `u_direct_io` 已知在某些系统上失败。

安装包：

```
make install
```

删除无用的静态库：

```
rm -fv /usr/lib/{libcom_err,lib2fs,libext2fs,libss}.a
```

此包安装了一个 gzip 压缩的 `.info` 文件，但不会更新系统级目录。解压此文件并使用以下命令更新系统目录：

```
gunzip -v /usr/share/info/libext2fs.gz
install-info --dir-file=/usr/share/info/dir /usr/share/info/libext2fs.info
```

如果需要，可以使用以下命令创建并安装额外的文档：

```
getinfo -o doc/com_err.info ../lib/ext/com_err.texinfo
install -v -m644 doc/com_err.info /usr/share/info
install --dir-file=/usr/share/info /usr/share/info/com_err.info
```

## 8.73. e2fsprogs 内容

- **已安装的程序：** `badblocks`, `chatter`, `deflate`, `debugfs`, `dumpe2fs`, `e2freefrag`, `e2fsck`, `e2image`, `e2label`, `e2mpstatus`, `e2scrub`, `e2scrub_all`, `e2ndcrypt`, `e4defrag`, `filefrag`, `fsckext2`, `fsckext3`, `fsckext4`, `logsave`, `lsattr`, `mkcd`, `mkefs`, `mkfsext2`, `mkfsext3`, `mkfsext4`, `mkplusfound`, `resize`, and `tune2fs`

- **已安装的库：** `libcom.so`, `lib2bp.so`, `lib2fs.so`, and `libss.so`

- **已安装的目录：** `/usr/include`, `/usr/lib`, `/var/lib`

## 要说明

- **`badblocks`:** 搜索设备的坏块

- **`chatter`:** 检查 ext2 文件系统

- **`deflate`:** 压缩文件

- **`debugfs`:** 用于 ext2 文件系统的交互式

- **`dumpe2fs`:** 打印 ext2 块信息

- **`e2freefrag`:** 估计 ext2 文件系统的碎片程度

- **`e2fsck`:** 检查并修复 ext2 文件系统

- **`e2image`:** 创建 ext2 文件系统的镜像

- **`e2label`:** 设置 ext2 文件系统的标签

- **`e2mpstatus`:** 显示多个分区的状态

- **`e2scrub`:** 检查 ext2 文件系统的错误

- **`e2scrub_all`:** 检查所有 ext2

- **`e2ndcrypt`:** 加密 ext2 文件系统

- **`e4defrag`:** 整理 ext4 文件系统

- **`filefrag`:** Report文件碎片程度

- **`fsckext2`:** 检查并修复 ext2 文件系统

- **`fsckext3`:** 检查并修复 ext3 文件系统

- **`fsckext4`:** 检查并修复 ext4 文件系统

- **`logsave`:** 保存命令输出

- **`lsattr`:** 列出文件属性

- **`mkcd`:** 在 ext2 文件系统中创建目录

- **`mkefs`:** 创建 ext2 文件系统

- **`mkfsext2`:** 创建 ext2 文件系统

- **`mkfsext3`:** 创建 ext3 文件系统

- **`mkfsext4`:** 创建 ext4 文件系统

- **`mkplusfound`:** 在文件系统中创建 lost+found 目录

- **`resize2fs`:** 调整 ext2 文件系统大小

- **`tune2fs`:** 调整 ext2 文件系统参数

## 8.74. Syslog-1.5.1

`syslog` 包包含记录系统消息的程序，例如内核发生异常时提供的消息。

预计构建时间：小于 0.1 SBU

所需磁盘空间：0.6 MB

### 8.74.1. 安装 syslog

首先，修复 `klog` 在某些情况下导致段错误的问题并修复过时的程序结构：

```
sed -i '/Error loading kernel symbols/;n;n;d' ksym_mod.c
sed -i '/s/union wait/int/' syslog.c
```

编译包：

```
make
```

此包未提供测试套件。

安装包：

```
make BINDIR=/sbin install
```

### 8.74.2. 配置 syslog

通过运行以下命令创建新的 `/etc/syslog.conf`：

```
cat > /etc/syslog.conf << "EOF"
# Begin /etc/syslog.conf

auth,authpriv. -*/var/log/auth.log
*.,authpriv.none -*/var/log/sys.log
daemon. -*/var/log/daemon.log
kern. -*/var/log/kern.log
mail. -*/var/log/mail.log
user. -*/var/log/user.log
*.emerg *

# End /etc/syslog.conf
EOF
```

## 8.74. syslog 内容

- `klogd`: 一个用于拦截和记录内核消息的系统守护进程

- `syslog`: 用于记录系统消息的程序

# syslogd

记录系统程序提供的日志消息。[每条记录的日志至少包含一个时间戳和一个主机名，通常还包含程序名称，但这取决于日志守护进程被设置的信任程度。]

## 8.75. Sysv-2.99

`Sysv` 软件包包含了控制系统启动、运行和关闭的程序。

预计构建时间：少于 0.1 SBU

所需磁盘空间：1.4 MB

### 8.75.1. 安装 Sysv

首先，应用补丁以移除由其他软件包安装的几个程序，澄清一条消息并修复编译器警告：

```
patch -Npl -i ../sysvinit-2.99-consolidated-1.patch
```

编译软件包：

```
make
```

此软件包不附带测试套件。

安装该软件包：

```
make install
```

### 8.75.2. Sysv 的内容

**已安装的程序：** `bootlogd`, `fstab-decode`, `halt`, `init`, `killall5`, `poweroff`（链接到 `halt`）, `reboot`（链接到 `halt`）, `runlevel`, `shutdown` 以及 `telinit`（链接到 `init`）

# 简述

- **`bootlogd`** 将启动消息记录到日志文件

- **`fstab-decode`** 使用 `fstab` 编码的参数运行命令

- **`halt`** 通常情况下带 `-h` 选项调用 **`shutdown`**，但在运行级别 0 时除外，此时它通知内核停止系统；它会在 `/var/log/tmp` 文件中记录系统已关机

- **`init`** 内核初始化硬件后启动的第一个进程，它接管启动过程并启动其配置文件指定的所有进程

- **`killall5`** 向所有进程发送信号，但当前会话中的进程除外，因此它不会杀死其父 shell

- **`poweroff`** 告诉内核停止系统并关闭电脑（**参见 `halt`**）

- **`reboot`** 告诉内核重启系统（**参见 `halt`**）

- **`runlevel`** 报告上一个当前的运行级别，如 `/run/utmp` 中最后一次运行级别记录所示

- **`shutdown`** 以安全的方式关闭系统，向所有进程发送信号并通知所有登录用户

- **`telinit`** 告诉 **`init`** 要切换到哪个运行级别

## 8.77. 关于调试符号

大多数程序和库默认都是带有调试符号进行编译的（使用 `gcc -g` 选项）。这意味着当调试一个带有调试信息的程序或库时，调试器不仅可以提供内存地址，还可以提供例和变量的名称。

然而，包含这些调试符号会显著增大程序或库的大小。以下是这些符号所占空间的示例：

- 带有调试符号的 `bash` 二进制文件：1200 KB

- 不带调试符号的 `bash` 二进制文件：480 KB

- 带有调试符号的 Glibc 和 GCC 文件 (`/lib` 和 `/usr/lib`)：87 MB

- 不带调试符号的 Glibc 和 GCC 文件：16 MB

大小可能取决于使用的编译器和 C 标准库，但在比较带有和不带调试符号的程序时，差异通常在二到五倍之间。

## 8.77. 去除符号 (Stripping)

此选项是可选的。如果用户不是程序员，且没有计划对系统软件进行任何调试，通过从二进制文件和库中移除调试符号，可以将系统体积减少约 2 GB。这除了无法再次调试软件外，不会带来任何不便。

使用上述命令的人大多数不会遇到任何困难。然而，很容易拼写错误导致新系统无法使用，因此在运行 `strip` 命令之前，最好对当前状态的 LFS 系统进行备份。

所选库的调试符号被放置在单独的文件中。以后在 BLFS 中使用 `valgrind` 或 `gdb` 运行回归测试时则需要这些调试信息。

注意 `strip` 会覆盖它正在处理的二进制或库文件。这可能会导致使用该文件代码或数据的进程崩溃。如果运行 `strip` 的进程本身受到影响，被去除符号的二进制文件或库可能会损坏并导致系统完全无法使用。为了避免这种情况，我们将一些库和二进制文件复制到 `/tmp`，在其中进行 `strip` 处理，然后使用 `install` 命令将其装回。阅读第 8.2.1 节“升级问题”中的相关条目了解在此使用 `install` 命令的原理。

`libitim.so.1.0.0`

`libatomic.so.1.2.0`

```
cd /usr/lib

for LIB in $save_usrlib; do
objcopy --only-keep-debug $LIB $LIB.dbg
cp $LIB /tmp/$LIB
strip --strip-unneeded /tmp/$LIB
objcopy --add-gnu-debuglink-$LIB.dbg /tmp/$LIB
install -vm755 /tmp/$LIB /usr/lib
rm /tmp/$LIB
done
```

```
online_usrbin="bash find strip
online_usrlib="libbfd-2.37.so
libbithistory.so.8.1
libncursesw.so.6.2
lib.so.6
libreadline.so.8.1
libz.so.1.2.11
$(cd /usr/lib; find libinnss.* -type f)
```

```
for BIN in $online_usrbin; do
cp /usr/bin/$BIN /tmp/$BIN
strip --strip-unneeded /tmp/$BIN
install -vm755 /tmp/$BIN /usr/bin
rm /tmp/$BIN
done
```

```
for LIB in $online_usrlib; do
cp /usr/lib/$LIB /tmp/$LIB
strip --strip-unneeded /tmp/$LIB
install -vm755 /tmp/$LIB /usr/lib
rm /tmp/$LIB
done
```

```
for i in $(find /usr/lib -type f -name "*.so*" ! -name "*.dbg") \
$(find /usr/lib -type f -name "*.a") \
$(find /usr/bin,sbin,libexec) -type f); do
case "$online_usrlib $online_usrbin $save_usrlib" in
  *$($(basename $i)*)
    *) strip --strip-unneeded $i;;
esac
done
```

`unset BIN LIB save_usrlib online_usrbin online_usrlib`

大量文件将被报告为文件格式无法识别。这些警告可以安全地忽略。它们表示这些文件是脚本而不是二进制文件。

## 8.78. 清理

最后，清理运行测试后留下的某些文件：

```
rm -rf /tmp/*
```

现在退出并使用更新 `chroot` 命令进入 `chroot` 环境。从现在起，当你需要在退出后进入 `chroot` 环境时，请使用此 `chroot` 命令：

`logout`

```
chroot "$LFS" /usr/bin/env -i \
HOME=/root "$TERM" \
PS1=(lfs chroot) \u:\w\\$ \
PATH=/usr/bin:/usr/sbin \
/bin/bash --login
```

这里不再使用 `+h` 选项，因为之前的程序已被替换：因此可以使用加密。

如果虚拟内核文件系统已手动或通过重启卸载，确保在重新进入 `chroot` 时挂载虚拟内核文件系统。该过程在第 7.3.2 节“挂载虚拟内核文件系统并填充 `/dev`”和第 7.3.3 节“挂载虚拟内核文件系统”中进行了解释。

`/usr/libexec` 中安装的几个文件也不需要。要删除它们，

```
find /usr -depth -name $(uname -m)-linux-gnu* | xargs rm -rf
```

在第 6 章和第 7 章构建的编译器仍然部分安装且不需要。使用以下命令删除：

```
find /usr -name *.la -delete
```

有关 `libtool` 文件的更多信息，请参见 BLFS 部分“About Lib Archive”。

最后，删除上一章开头创建的 `tester` 用户账户。

```
userdel -r tester
```

## 9.2. LFS-Bootstraps-20210608

`LFS-Bootstraps` 软件包包含一组脚本，用于在启动/关机时启动/停止 LFS 系统。自定义启动过程所需的配置文件和步骤将在随后的章节中进行描述。

- 大致编译用时间：少于 0.1 SBU

- 所需磁盘空间：440 KB

### 9.2.1. 安装 LFS-Bootstraps

安装该软件包：

```
make install
```

### 9.2.2. LFS-Bootstraps 的内容



已安装的脚本：`checkfs`, `cleanfs`, `console`, `functions`, `halt`, `ifdown`, `ifup`, `localnet`, `modules`, `mountfs`, `mountvirtfs`, `network`, `reboot`, `sendsignals`, `setclock`, `ipv4-static`, `swatic`, `syslog`, `template`, `update` 以及 `dev_retry`

已安装的目录：`/etc/rc.d`, `/etc/init.d`（符号链接），`/etc/sysconfig`, `/lib/services`, `/lib/lib`（符号链接）

### 简述

- **`checkfs`**: 在挂载文件系统之前检查其完整性（日志和基于网络的文件系统除外）

- **`cleanfs`**: 移除重启期间不应保留的文件，例如 `/run/` 和 `/var/log/` 中的文件；它会重新创建 `/run/utmp` 并删除当前的 `/etc/nologin`、` /fastboot` 和 `/forcefsck` 文件

- **`console`**: 为所需的键盘布局加载正确的键位映射；它还会设置屏幕字体

- **`functions`**: 包含常用函数（例如错误和状态检查），这些函数被多个启动脚本使用

- **`halt`**: 停止系统

- **`ifdown`**: 停止网络设备

- **`ifup`**: 初始化网络设备

- **`localnet`**: 设置系统的主机名和本地回环设备

- **`modules`**: 加载 `/etc/sysconfig/modules` 中的内核模块，并使用该处给出的参数

- **`mountfs`**: 挂载所有文件系统，标记为 noauto 的非自动挂载或基于网络的系统除外

- **`mountvirtfs`**: 挂载虚拟内核文件系统，如 proc

- **`network`**: 设置网络接口（如网卡）并设置默认网关（如果适用）

- **`rc`**: 主运行级别控制脚本；它负责按照正在处理的链接名称确定的顺序逐个运行所有启动脚本

- **`reboot`**: 重启系统

- **`sendsignals`**: 确保在系统重启或停止之前每个进程都已终止

- **`setclock`**: 将内核时钟重置为本地时间，以硬件时钟未设置为 UTC 时间

- **`ipv4-static`**: 提供为网络接口分配静态 Internet协议 (IP) 地址所需的功能

- **`swap`**: 启用和禁用交换文件和分区

- **`sysctl`**: 如果存在 `/etc/sysctl.conf` 文件，则将其中的系统配置值加载到运行的内核中

- **`syslogd`**: 启动和停止系统内核日志守护进程

- **`template`**: 为其他守护进程创建自定义启动脚本的模板

- **`udev`**: 准备 `/dev` 目录并启动 Udev

- **`udev_retry`**: 重试失败的 udev uevent，并在需要时将生成的规则文件从 `/run/udev` 复制到 `/etc/udev/rules.d`

## 9.3. 设备和模块处理概述

在第 8 章中，我们在构建 edev 时安装了 udev 软件包。在详细介绍其工作原理之前，有必要简要介绍一下以前处理设备的方法。

通常 Linux 系统传统使用静态设备创建方法，即在 `/dev` 下创建了大量的设备节点（有时是数千个节点），无论相应的设备是否实际存在。这通常通过 `MAKEDEV` 脚本完成，该脚本包含对 `mknod` 程序的多次调用，为世界上可能存在的每个设备提供相关的主设备号和次要设备号。

使用 udev 方法，仅为内核检测到的设备创建相应的设备节点（dev device nodes）。因为这些设备节点会在每次系统启动时被创建，所以它们被存储在 dev.tmpfs 文件系统中（一个完全位于系统内存中的虚拟文件）。设备节点不需要多少空间，因此所使用的内存可以忽略不计。

### 9.3.1. 历史

2000 年 2 月，一种名为 devfs 的新文件系统被合并到 2.3.4 内核中，并在 2.4 系列稳定内核中可用。尽管该方法存在于内核源码中，但这种动态创建设备的方法从未获得核心内核开发者的压倒支持。

devfs 采用的方法主要问题在于它处理设备检测、连接和命名的方式。后期问题，即设备命名可能是最关键的。人们通常认为，如果允许名称是配置的，那么设备命名策略应该由系统管理员决定，而不是由任何特定的开发者实施。devfs 文件还受到其设计中固有的竞态条件的影响，如果不对内核进行实质性修订将无法修复。由于缺乏维护，它长期以来被标记为废弃，并最终于 2006 年 6 月从内核中移除。

随着不稳定的 2.5 内核树的发展（后作为 2.6 系列稳定内核发布），名为 sysfs 的新文件系统诞生了。sysfs 的工作是向用户导出信息。

### 9.3.2. Udev 实现

使用 udev 方法，仅为内核检测到的设备创建设备节点（dev device nodes）。因为这些设备节点会在每次系统启动时被创建，所以它们被存储在 dev.tmpfs 文件系统中（一个完全位于系统内存中的虚拟文件）。设备节点不需要多少空间，因此所使用的内存可以忽略不计。

### 9.3.2. Sysfs

通常 Linux 系统传统使用静态设备创建方法，即在 `/dev` 下创建了大量的设备节点（有时是数千个节点），无论相应的设备是否实际存在。这通常通过 `MAKEDEV` 脚本完成，该脚本包含对 `mknod` 程序的多次调用，为世界上可能存在的每个设备提供相关的主设备号和次要设备号。

2000 年 2 月，一种名为 devfs 的新文件系统被合并到 2.3.4 内核中，并在 2.4 系列稳定内核中可用。尽管该方法存在于内核源码中，但这种动态创建设备的方法从未获得核心内核开发者的压倒支持。

devfs 采用的方法主要问题在于它处理设备检测、连接和命名的方式。后期问题，即设备命名可能是最关键的。人们通常认为，如果允许名称是配置的，那么设备命名策略应该由系统管理员决定，而不是由任何特定的开发者实施。devfs 文件还受到其设计中固有的竞态条件的影响，如果不对内核进行实质性修订将无法修复。由于缺乏维护，它长期以来被标记为废弃，并最终于 2006 年 6 月从内核中移除。

随着不稳定的 2.5 内核树的发展（后作为 2.6 系列稳定内核发布），名为 sysfs 的新文件系统诞生了。sysfs 的工作是向用户导出信息。

### 9.3.2. 设备创建

通常 Linux 系统传统使用静态设备创建方法，即在 `/dev` 下创建了大量的设备节点（有时是数千个节点），无论相应的设备是否实际存在。这通常通过 `MAKEDEV` 脚本完成，该脚本包含对 `mknod` 程序的多次调用，为世界上可能存在的每个设备提供相关的主设备号和次要设备号。

### 9.3.2. 模块加载

udev 只有在它具有特定的总线别名且驱动程序向 sysfs 导出所需的别名时，才会加载模块。在其他情况下，应该通过其他方式触发模块加载。对于 Linux 5.13.12，udev 能够加载良好的驱动、PCI、USB、SCSI、SERIO 和 FireWire。

### 9.3.3. 加载和创建设备的问题

在自动创建设备节点存在一些可能的问题。

### 9.3.1. 内核模块未自动加载

udev 只有在它具有特定的总线别名且驱动程序向 sysfs 导出所需的别名时，才会加载模块。在其他情况下，应该通过其他方式触发模块加载。对于 Linux 5.13.12，udev 能够加载良好的驱动、PCI、USB、SCSI、SERIO 和 FireWire。

### 9.3.4. 处理热插拔/动态设备

当你插入一个设备时（例如通用总线（USB）MP3 播放器），内核识别到该设备已连接并生成 uevent。随后，该事件将由上述由 udev 处理。

## 9.3.3.2. 内核模块未自动加载，且 udev 并不打算加载

如果“封装”模块仅增强了某些模块提供的功能（例如，`snd-pcm` 通过让 OSS 应用可以使用音频来增强 `snd-pcm` 的功能），请配置 `modprobe` 在 udev 加载被封装模块后加载该封装模块。要做到这一点，请在 `/etc/modprobe.d/<filename>.conf` 行中添加 "softdep"。例如：

```
softdep snd-pcm post: snd-pcm-oss
```

注意，"softdep" 命令也允许 `pre:` 依赖，或者 `pre:` 和 `post:` 依赖的混合使用。有关 "softdep" 语法和功能，请参阅 `modprobe.d(5)` 手页。

如果所讨论模块不是封装模块而是独立使用的，请配置模块引导程序在系统启动时加载该模块。要做到这一点，请将模块名单独起行添加到 `/etc/sysconfig/modules` 文件中。这对于模块也有效，但在那种情况下并非优选。

## 9.3.3.3. Udev 加载了某些不需要的模块

不要编译该模块，或者在 `/etc/modprobe.d/blacklist.conf` 文件中加入黑名单，如下例中的 `forte` 模块所示：

```
blacklist forte
```

被黑名单的模块仍然可以通过显式的 `modprobe` 命令手动加载。

## 9.3.3.4. Udev 错误地创建了设备或建立了错误的符号链接

这通常发生在规则意外未能匹配到设备时。例如，一个编写不当的规则可能会根据厂商同时匹配到设备（符合预期）和相应的 SCSI 设备（错误）。可以在 `udevadm info` 命令的帮助下找到该规则并使其更具体化。

## 9.3.3.5. Udev 创建了不必要的规则

这可能是前一个问题的另一种表现形式。如果不是如此，且你的规则使用了 `sysfs` 属性，这可能是一个内核时序问题，将在后续内核中修复。现在你仍然通过创建一个等待 `sysfs` 属性的规则并将其附加到 `/etc/udev/rules.d/10-wait_for_sysfs.rule`（如果该文件不存在则创建它）来规避它。如果你这样做并有所帮助，请通知 Udev 开发列表。

## 9.3.3.6. Udev 未创建设备

后续文本显示，该设备已构建在内核中或已作为模块加载，并且它没有将数据导出到 `sysfs`。

如果内核驱动程序未将其数据导出到 `sysfs`，udev 就没有信息来创建设备节点。这对于内核外部的第三方驱动程序很常见。可以在 `/usr/lib/udev/devices` 中创建一个具有适当主/次数的静态设备节点（参见内核文档中的 `devices.txt` 或第三方驱动供应商提供的文档）。该静态设备将被复制到 `/dev udev`。

## 9.3.3.7. 设备命名顺序在重启后随机变化

这是由于 udev 在设计上并行处理事件并加载模块，因此以一种不可预测的顺序执行。这永远不会被“修复”。你不应该依赖内核设备名称是稳定的。相反，请创建自己的规则，根据设备的某些属性（例如序列号或 udev 安装的 `*_id` 工具的输出）创建具有稳定名称的符号链接。示例请参见第 9.4 节“管理设备”和第 9.5 节“通用网络配置”。

## 9.3.4. 推荐阅读

以下站点可以获取额外的帮助文档：

- [devfs 的用户空间实现](http://www.roah.com/linux/talks/ols_2003_udev_paper/Reprint-Koah-Hartman-OLS2003.pdf)

- [sysfs 文件系统](http://www.kernel.org/pub/linux/kernel/people/doc/papers/ols-2005-mchel.pdf)

## 9.4. 管理设备

### 9.4.1. 网络设备

udev 默认根据固件/BIOS 数据或物理特性（总线、插槽或 MAC 地址）命名网络设备。这种命名规范的目的是确保网络设备的命名是一致的，而不是基于网卡被发现的时间。例如，在一台拥有 Intel 和 Realtek 的两个网卡的电脑上，Intel 制造的网卡可能变为 `eth0`，而 Realtek 网卡变为 `eth1`。在某些情况下，重启后网卡可能会反过来命名。

在新的命名方案中，典型的网络设备名称将变为 `emp5s0` 或 `wlp3s`。如果不需要这种命名，可以实现传统的命名方案或自定义方案。

#### 9.4.1.1. 在内核命令行上禁用持久性命名

可以通过在内核命令行上添加 `net.ifnames=0` 来恢复使用 `eth0`、`eth1` 的传统命名方案。这对于只有一个同类型设备的系统最为合适。笔记本电脑通常有多个命名为 `eth0` 和 `wlan0` 的以太网连接，也是这种方法的候选。该命令在 GRUB 配置文件中传递。参见第 10.4.4 节“创建 GRUB 配置”。

#### 9.4.1.2. 自定义 Udev 规则

可以通过创建自定义 udev 规则来自定义命名方案。其中包含了一个生成初始规则的脚本。这些规则可以被修改：

```bash
bash /usr/lib/udev/init-net-rules
```

注意

在某些情况下，重启后网卡可能会反过来命名。

在新的命名方案中，典型的网络设备名称将变为 `emp5s0` 或 `wlp3s`。如果不需要这种命名，可以实现传统的命名方案或自定义方案。

可以通过创建自定义 udev 规则来自定义命名方案。其中包含了一个生成初始规则的脚本。这些规则可以被修改：

```bash
bash /usr/lib/udev/init-net-rules
```

注意

在某些情况下，重启后网卡可能会反过来命名。

如果你想查看 udev 脚本将要使用的值，那么对于相应的 CD-ROM 设备，进入 /sys 下对应的目录（例如，这可以是 /sys/block/hddn），并运行类似下面所示的命令：

```
udevadm test /sys/block/hdd
```

查看包含 *_id 程序* 输出的几行。"by-id" 模式如果 `ID_SERIAL` 值存在且不为空，则将使用该值，否则将使用 `ID_MODEL` 和 `ID_REVISION` 的组合。"by-path" 模式将使用 `ID_PATH` 值。

如果默认模式不适用于你的情况，则可以对 /etc/udev/rules.d/83-cdrom-symlinks.rules 文件进行如下修改（其中 mode 为 "by-id" 或 "by-path"）：

```bash
sed -e '/write_cd_rules/"write_cd_rules mode/' \
-i /etc/udev/rules.83-cdrom-symlinks.rules
```

请注意，此时创建规则或符号链接是非常重要的，因为你已经将主机的 /dev 目录挂载到了 LFS 系统，且我们假设系统存在于主机上。规则将在你首次启动 LFS 系统时创建。

然而，如果你有多个 CD-ROM 设备，那么那时生成的符号链接指向的设备可能与你在主机上指向的设备，因为系统是稳定的，这仅在你需要两边的符号链接都指向同一个设备时发生。如果你需要这样做，请在启动之前检查（可能编辑）/etc/udev/rules.d/70-persistent-cd.rules 文件，以使所有符号链接符合你的要求。

## 9.4.3. 处理重复设备

如第 9.3 节“设备和模块处理概述”所述，相同功能的设备在 /dev 中出现的顺序是随机的。例如，如果你有一个 USB 摄像头和一个电视调谐器，有时 /video0 指向摄像头，而 /video1 指向调谐器，而有时重启后会改变这种顺序。对于声卡和网卡以外的所有类硬件，这可以通过为自定义的持久化链接创建 udev 规则来解决。网卡的情况在第 9.5 节“通用网络配置”中单独介绍，声卡配置可以在 BLFS 中找到。

对于你的每个可能出现此问题（如果该问题在你当前的 Linux 发行版中不存在）的设备，在 /sys/class 或 /sys/block 下找到对应的目录。对于视频设备，检查标识设备的属性（通常是厂商和 ID 产品）并分配名称的方法是可行的：

```
udev info -a -p /sys/class/video4linux/video0
```

编写创建符号链接的规则，例如：

```bash
cat > /etc/udev/rules.83-duplicate_devices.rules << "EOF"

# 摄像头和调谐器的持久链接
KERNEL="video*", ATTRS(idProduct)="1910", ATTRS(idVendor)="0d81", SYMLINK+="video"
KERNEL="video*", ATTRS(device)="0306f", ATTRS(vendor)="0109e", SYMLINK+="tuner"

EOF
```

结果是 /dev/video0 和 /dev/video1 设备仍然指向调谐器和摄像头（因此不应直接使用），但存在 /dev/tvtuner 和 /dev/webcam 符号链接，它们始终指向正确的设备。

## 9.5. 通用网络配置

### 9.5.1. 创建网络接口配置文件

网络脚本启动和关闭哪些接口通常取决于 /etc/sysconfig/ 中的文件。该目录应该为每个要配置的接口包含一个文件，例如 ifconfig.xyz，其中 "xyz" 说明网卡。接口名称（例如 eth0）通常是合适的。该文件内部是接口的属性，例如其 IP 地址、子网掩码等。文件名的主干必须是 ifconfig。

> 注意：如果没有使用上一一节中的步骤，udev 将根据系统物理特征（如 en2s1）分配网卡接口名称。如果你不确定接口名称是什么，可以在启动系统后运行 `ip link` 或 `ls /sys/class/net`。

以下命令为具有静态 IP 地址的 eth0 设备创建一个示例文件：

```bash
cd /etc/sysconfig/
cat > ifconfig.eth0 << "EOF"
ONBOOT=yes
IFACE=eth0
SERVICE=ipv4-static
IP=192.168.1.2
GATEWAY=192.168.1.1
PREFIX=24
BROCASTCAST=192.168.1.255
EOF
```

斜体中的值必须在每个文件中更改，以匹配适当的设置。



如果 `ONBOOT` 变量设置为 `"yes"`，系统网络脚本将在系统启动过程中启用网卡（NIC）。如果设置为 `"yes"` 之外的任何值，网卡将被网络脚本忽略且不会自动启动。可以使用 `ifup` 和 `ifdown` 命令手动启动或停止接口。

`IFACE` 变量定义了接口名称，例如 `eth0`。所有网络配置文件都需要它。文件扩展名必须匹配此值。

`SERVICE` 变量定义了用于获取 IP 地址的方法。LFS-Bootscripts 包具有模块化的 IP 分配格式，创建额外的文件可以实现此功能。

`GATEWAY` 变量应包含默认网关。

`PREFIX` 变量包含子网掩码位数。如果没有提供，则默认为 24。`BROADCAST` 变量是广播地址。根据设置更改 `PREFIX` 值。如果掩码是 255.255.255.0，则为 24 位。如果掩码是 255.255.255.128，则为 25 位。如果掩码是 255.255.0.0，则为 16 位。如果掩码是 255.0.0.0，则为 8 位。

`IP` 变量是 IP 地址。

如果 `ONBOOT` 变量设置为 `"yes"`，系统网络脚本将在系统启动过程中启用网卡（NIC）。如果设置为 `"yes"` 之外的任何值，网卡将被网络脚本忽略且不会自动启动。

`nameserver` 变量包含主 DNS 服务器地址。

### 9.5.2. 创建 resolv.conf 文件

为了解析域名，系统需要在 `/etc/resolv.conf` 文件中放置 DNS 服务器地址。如果需要，请在启动前创建文件。`resolv.conf` 文件可以包含多个 `nameserver` 条目，以备用 DNS 服务器地址。

`domain` 语句可以定义搜索域。如果不需要，可以将其注释掉。

通过运行以下命令创建 `/etc/resolv.conf`：

```bash
cat /etc/resolv.conf << "EOF"
# Begin /resolv.conf

domain <Domain>
nameserver <DNS 服务器地址>
nameserver <备用 DNS 服务器地址>

EOF
```

### 9.5.3. 配置系统 hostname

在启动过程中，系统使用 `/etc/hostname` 文件来确定主机名。通过运行以下命令创建 `/etc/hostname`：

```bash
echo "<hostname>" > /etc/hostname
```

### 9.5.4. 定制 /etc/hosts 文件

即使不使用网络连接，有效的 FDN 也对于某些程序的正确运行是必须的。在 `/etc/hosts` 文件中使用 IP 地址、完全限定域名（FQDN）以及可能的别名。格式如下：

```
IP_address myhost aliases
```

除非计算机对互联网可见，否则确保 IP 地址在私有网络范围内：

```
127.0.0.1 localhost.localdomain
127.0.1.1 <FQDN> <HOSTNAME>
<192.168.1.1> <FQDN> <HOSTNAME> [alias1] [alias2 ...]
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

创建 `/etc/hosts` 文件：

```bash
cat > /etc/hosts << "EOF"
# Begin /etc/hosts

127.0.0.1 localhost.localdomain
127.0.1.1 <FQDN> <HOSTNAME>
<192.168.1.1> <FQDN> <HOSTNAME> [alias1] [alias2 ...]
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

# End /etc/hosts
EOF
```

## 9.6. System V 引导脚本使用与配置

### 9.6.1. System V 启动脚本是如何工作的？

Linux 使用一种基于运行级别（run-levels）概念的特殊启动方式 SysVinit。它在不同系统之间可能不同，因此不能假设某个特定的 Linux 发行版中的某些操作是有效的，它们会以自己的方式工作，但遵循了通用的标准。

SysInit（下文简称为“init”）使用运行级别（run-level）方案工作。共有七个（编号从 0 到 6）运行级别（实际上，还有更多运行级别，但它们用于特殊情况，通常不被使用）。详情请参阅 `init`（第 8 节），其中每一个运行级别都对应于计算机启动时应该执行的动作。默认运行级别为 3。以下是已实现的不同运行类别的描述：

```
0: 停止计算机
1: 单用户模式
2: 不带网络的多用户模式
3: 带网络的多用户模式
4: 留作自定义，否则功能与 3 相同
5: 与 4 相同，通常用于 GUI 登录（如 X 的 xdm 或 KDE 的 kdm）
6: 重启计算机
```

## 9.6.2. 配置 Sysinit

在内核初始化期间，运行的第一个程序是在命令行上指定的，或者默认为 `init`。该程序读取初始化文件 `/etc/inittab`。通过以下命令创建此文件：

```
cat > /etc/inittab << "EOF"
# Begin /etc/inittab
id3:initdefault:

s::sysinit:/etc/rc.d/init.d/rc

10:0:wait:/etc/rc.d/init.d/rc 0
11:1:wait:/etc/rc.d/init.d/rc 1
12:2:wait:/etc/rc.d/init.d/rc 2
13:3:wait:/etc/rc.d/init.d/rc 3
14:4:wait:/etc/rc.d/init.d/rc 4
15:5:wait:/etc/rc.d/init.d/rc 5
16:6:wait:/etc/rc.d/init.d/rc 6

ca:12345:ctrlaltdel::/bin/shutdown -tl -a -r now

su:SO106:once:/sbin/sulogin

1:2345:respawn:/sbin/agetty --nuclear tty1 9600
2:2345:respawn:/sbin/agetty tty2 9600
3:2345:respawn:/sbin/agetty tty3 9600
4:2345:respawn:/sbin/agetty tty4 9600
5:2345:respawn:/sbin/agetty tty5 9600
6:2345:respawn:/sbin/agetty tty6 9600

# /etc/inittab
EOF
```

关于此初始化文件的解释位于 `inittab` 的主页。对于 LFS 而言，运行的命令是 `rc`。上述初始化文件将指示 `rc` 运行 `/etc/rc.d` 中所有以 S 开头的脚本，紧接着运行 `/etc/rc.d` 中所有以 S 开头的脚本，其数字由默认值指定。

为了方便起见，`rc` 脚本会读取 `/lib/init-functions` 中的函数库。该库还会读取一个可选的配置文件 `/etc/sysconfig/rc`。后续章节中描述的任何系统参数都可以备选放在此文件中。

为了调试方便，脚本将所有输出记录到 `/run/log`。`/run` 目录是 `tmpfs`，此文件在重启后不会持久，但在启动过程结束时，会被追加到持久文件 `/var/log/boot` 中。

## 9.6.2. 修改运行级别

更改运行级别通过 `init <runlevel>` 完成，其中 `runlevel` 是目标运行级别。例如，要重启计算机，用户可以使用 `init 6` 命令，它是 `reboot` 命令的别名。同样，`init 0` 用于 `halt` 命令。

在 `/etc/rc.d` 下有许多看起来像 `rc.d?` 的目录（其中 `?` 是运行级别的数字），所有它们都包含许多符号链接。某些以 `K` 开头，另一些以 `S` 开头以启动服务。数字决定了脚本从 0 到 99 的执行顺序——数字越小执行越早。当 `init` 切换到另一个运行级别时，将根据所定的运行级别启动或停止相应的服务。

真正的脚本位于 `/etc/rc.d/init.d` 中。它们执行实际工作，所有的符号链接都指向它们。K 链接和 S 链接指向 `/etc/rc.d/init.d` 中的同一个脚本。当遇到 K 链接时，带 `stop` 参数运行相应的脚本。当遇到 S 链接时，带 `start` 参数运行相应的脚本。

此说明有一个例外。在 `rc.0` 和 `rc.d` 目录中以 S 开头的链接不会导致任何启动。如果系统只需要停止，它们将带有参数被调用。

以下是这些参数如何使脚本执行的描述：

- `start`: 启动服务。
- `stop`: 停止服务。
- `restart`: 停止服务然后重新启动。
- `reload`: 在修改配置文件后更新服务的配置，而无需重启。
- `status`: 告知服务是否正在运行以及具有哪些 PID。

可以随意修改启动过程的工作方式（毕竟，这是你自己的 LFS 系统）。这里提供的文件是实现如何操作的示例。

## 9.6.3. Udev 启动脚本

在内核初始化期间，运行的第一个程序是在命令行上指定的，或者默认为 `init`。该程序读取初始化文件 `/etc/inittab`。上述初始化文件将指示 `rc` 运行 `/etc/rc.d` 中所有以 S 开头的脚本，紧接着运行 `/etc/rc.d` 中所有以 S 开头的脚本，其数字由默认值指定。

为了方便起见，`rc` 脚本会读取 `/lib/init-functions` 中的函数库。该库还会读取一个可选的配置文件 `/etc/sysconfig/rc`。后续章节中描述的任何系统参数都可以备选放在此文件中。

为了调试方便，脚本将所有输出记录到 `/run/log`。`/run` 目录是 `tmpfs`，此文件在重启后不会持久，但在启动过程结束时，会被追加到持久文件 `/var/log/boot` 中。

更改运行级别通过 `init <runlevel>` 完成，其中 `runlevel` 是目标运行级别。例如，要重启计算机，用户可以使用 `init 6` 命令，它是 `reboot` 命令的别名。同样，`init 0` 用于 `halt` 命令。

在 `/etc/rc.d` 下有许多看起来像 `rc.d?` 的目录（其中 `?` 是运行级别的数字），所有它们都包含许多符号链接。某些以 `K` 开头，另一些以 `S` 开头以启动服务。数字决定了脚本从 0 到 99 的执行顺序——数字越小执行越早。当 `init` 切换到另一个运行级别时，将根据所定的运行级别启动或停止相应的服务。

真正的脚本位于 `/etc/rc.d/init.d` 中。它们执行实际工作，所有的符号链接都指向它们。K 链接和 S 链接指向 `/etc/rc.d/init.d` 中的同一个脚本。当遇到 K 链接时，带 `stop` 参数运行相应的脚本。当遇到 S 链接时，带 `start` 参数运行相应的脚本。

此说明有一个例外。在 `rc.0` 和 `rc.d` 目录中以 S 开头的链接不会导致任何启动。如果系统只需要停止，它们将带有参数被调用。

以下是这些参数如何使脚本执行的描述：

- `start`: 启动服务。
- `stop`: 停止服务。
- `restart`: 停止服务然后重新启动。
- `reload`: 在修改配置文件后更新服务的配置，而无需重启。
- `status`: 告知服务是否正在运行以及具有哪些 PID。

可以随意修改启动过程的工作方式（毕竟，这是你自己的 LFS 系统）。这里提供的文件是实现如何操作的示例。

## 9.6.5. 配置 Linux 控制台

本节讨论了如何配置控制台，设置键盘映射、字体和内核级别。非 ASCII 字符（如版权符号）将使用，控制台是美国式的，否则不是。如果没有配置（或 `rc` 中的相应设置），启动脚本将无所作为。`/etc/sysconfig/console` 文件应该包含 `VARIABLE="value"` 格式的行。以下变量是可识别的：

- `LOGLEVEL`: 该变量指定通过 `dmesg -n` 发送到控制台的内核日志级别。有效范围从“1”（无消息）到“8”。默认级别为“7”。
- `KEYMAP`: 该变量指定 `loadkeys` 程序的参数，通常是要加载的映射名称，例如 "it"。如果未设置变量，启动脚本将不会运行 `loadkeys` 程序，并将使用默认内核映射。注意某些映射具有同名的多个版本（qwerty/ 中的 cz 及其变体以及 olpc/ 中的 trf）。在这些情况下，还应指定父目录（例如 qwerty/）以确保加载正确的映射。
- `KEYMAP_CORRECTIONS`: 该（很少使用的）变量指定 `loadkeys` 程序的参数。如果键映射不完全满意且必须进行微调，则非常有用。例如，为了将欧元符号引入通常没有它的键图中，将此变量设置为 "euro2"。
- `FONT`: 该变量指定 `setfont` 程序的参数。通常包括字体名称、"-m" 以及要加载的应用程序字符映射名称。例如，为了加载 "lat16" 字体配合 "8859-1" 字符映射（这在美国是合适的），将此变量设置为 lat16 -m 8859-1。在 UTF-8 模式下，内核使用应用程序字符映射将键映射中的 8 位代码转换为 UTF-8，因此 "-m" 参数的设置应设置为组合键码的编码。
- `UNICODE`: 将此变量设置为 "1"、yes" 或 "true" 以将控制台处于 UTF-8 模式。这对于 UTF-8 区域语言很有用，否则会有害。

## LEGACY_CHARSET

对于许多键盘布局，Kbd 软件包中没有内置的 Unicode 键位图。如果此变量设置为可用的非 UTF-8 键位图的编码，控制台启动脚本将动态将可用的键位图转换为 UTF-8。

以下是一些示例：

- 对于非 Unicode 的设置，通常只需要 `KEYMAP` 和 `FONT` 变量。例如，对于波兰语设置，可以使用以下内容：

```
cat /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

KEYMAP="pl22"
FONT="lat2a-16 -m 8859-22"

# End /etc/sysconfig/console
EOF
```

- 如上所述，有时需要对内置键位图进行微调。以下示例为德语键位图增加了欧元符号：

```
cat /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

KEYMAP="de-latin1"
KEYMAP_CORRECTIONS="euro2"
FONT="lat0-16 -m 8859-15"
UNICODE="1"

# End /etc/sysconfig/console
EOF
```

- 以下是一个适用于保加利亚语的 Unicode 示例，其存在内置的 UTF-8 键位图：

```
cat /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

UNICODE="1"
KEYMAP="bg_bds-utf8"
FONT="LatArCyrHeb-16"

# End /etc/sysconfig/console
EOF
```

由于上一个示例使用了 512 字符的 LatArCyrHeb-16 字体，除非使用帧缓冲区（framebuffer），否则 Linux 控制台将无法使用亮色。如果希望在不使用帧缓冲区的情况下使用亮色且不出现非本语言字符，仍然可以使用特定语言的 256 字符字体，如下所示：

```
cat > /etc/sysconfig/console << "EOF"
# /etc/sysconfig

UNICODE="1"
KEYMAP="bg_bd-utf8"
FONT="cyr-sun16"

# /etc/sysconfig/console
EOF
```

以下示例说明了键位图从 ISO-8859-15 到 UTF-8 的自动转换，并在 Unicode 模式下启用死键（dead keys）：

```
cat > /etc/sysconfig/console << "EOF"
# /etc/sysconfig

UNICODE="1"
KEYMAP="de-latin1"
KEYMAP_CORRECTIONS="euro2"
LEGACY_CHARSET="iso-8859-15"
FONT="LatArCyrHeb-16 -m 8859-15"

# /etc/sysconfig/console
EOF
```

某些键位图可能包含死键（即本身不产生字符，但会在下一个按键产生的字符上添加重音符号）或定义组合规则（例如：默认键位图中的“按下 Ctrl. A 获取 Æ”）。Linux-5.13 在非多字节模式下可以正确解释键位图中的死键和组合规则。这种缺陷不会影响欧洲语言的按键，因为这些语言通过添加重音来避免使用 ASCII 字符或组合两个 ASCII 字符。然而，在 UTF-8 中这是一个问题；例如对于希腊语，需要在字母“alpha”上加上重音符号。解决方案是避免使用 UTF-8，或者安装在输入处理上不具有此局限性的 Windows 系统。

对于中文、日语、韩语及某些其他语言，Linux 控制台无法配置为显示所需的字符。需要这些语言的用户应该安装 X Window 系统、涵盖必要字符范围的字体以及适当的输入法（例如支持多种语言的 SCIM）。

> [!TIP]
> `/etc/sysconfig/console` 文件仅控制 Linux 文本控制台的本地化。它与 X Window 系统中设置正确的键盘布局和终端功能、ssh 会话或串口控制台无关。在这些情况下，上述最后两项中提到的局限性并不适用。

## 9.6.6. 在启动时创建文件

有时在启动时创建文件是有意义的。例如，通常需要 `/tmp/.ICE-unix` 目录。这可以通过在 `/etc/sysconfig/createfiles` 配置脚本创建一个条目来实现。该文件的格式嵌入在默认配置文件的注释中。



## 9.6.7. 配置 syslog 脚本

`syslog`脚本作为 System V 初始化的一部分调用`syslog`程序。`-m`选项会关闭`syslog`默认每 20 分钟写入日志文件的周期性时间戳标记。如果你想开启周期性时间戳标记，可以编辑`/etc/sysconfig/rc.site`并定义变量`SYSLOG_PARMS`为所需值。要移除所有参数，请将变量设置为空值：

```
SYSLOG_PARMS=
```

更多选项请参阅`syslog`。

## 9.6.8. rc.site 文件

可选的`/etc/rc.site`文件包含了为每个 System 启动脚本自动设置的配置。它也可以设置位于`/etc/sysconfig/`目录下`hostname`、`console`和`clock`文件指定的值。如果相关变量在这些独立的文件和`rc.site`中同时，则脚本中指定的值具有优先级。

`rc.site`还包含可以自定义启动过程其他方面的参数。设置`PROMPT`变量将启用选择性运行启动脚本。其他选项在文件中描述。该文件的默认版本为：

```
# rc.site
# 启动脚本的可选参数。

# 发行版信息
# 如果在这里指定这些值，将覆盖默认值
#DISTRO="Linux From Scratch" # 发行版名称
#DISTRO_CONTACT="lfs-dev@linuxfromscratch.org" # 错误报告地址
#DISTRO_MINI="LFS" # 发行版配置文件名使用的短名称

# 定义打印到控制台的消息的自定义颜色

# 更多信息请咨询 `console_codes`
# `ECMA-48 Set Graphics Rendition` 章节
# 警告：当从 8 位字体切换到 9 位字体时，
# linux 控制台将重新解释粗体 (1)；
# 高 2 位
```

通常情况下，`/tmp`目录下的所有文件在启动时会被删除。根据存在的文件或目录数量，这可能会导致启动过程明显延迟。要跳过这些文件，请设置变量`SKIPMTCLEAN=y`。

在启动过程中，`init`进程向其启动的每个程序发送一个`TERM`信号（例如等待一段时间（3秒），并每个进程发送一个`KILL`信号并等待。该过程在`signal-script`中重复，适用于任何未被所有者关闭的进程。`init`的延迟可以通过传递参数来设置。例如，要移除`init`的延迟，可以在关机或重启时设置`-t0`。可以通过设置参数`KILLDELAY=0`来跳过`signal-script`的延迟。

## 9.7. Bash 启动文件

shell 程序`/bin/bash`（称为“shell”）使用一组启动文件来创建一个运行环境。每个文件都有特定的用途，并可能影响登录和交互式环境。`/etc`目录下的不同文件提供了全局设置。如果主目录中存在相应的文件，它可能会覆盖全局设置。

交互式登录 shell 在成功登录后，使用`/bin/login`或读取`/etc/passwd`文件启动。交互式非登录 shell 在命令行启动（例如 `[prompt]#bin/bash`）。当运行 shell 脚本时，通常存在一个非交互式 shell。它是非交互性的，因为它正在处理脚本，而不是在命令下等待用户输入。

欲了解更多信息，请参阅 Bash 启动文件（Bash Startup Files）和交互章节（Interactive Sections）。

当 shell 作为交互式登录 shell 被调用时，会读取`/etc/profile`和`~/.bash_profile`。下方的`/etc/profile`设置了一些原生语言支持所需的环境变量变量。正确设置这些变量将导致：

- 程序的输出被翻译为本地语言
- 将字符正确分类为字母、数字和其他类别。这对于 bash 在非英语语言区域设置的命令行中接受非 ASCII 字符是必要的
- 该国家正确的字母排序顺序
- 恰当的默认纸张大小
- 货币、时间和日期值的正确格式化

将`<LL>`替换为所需语言的两个字母代码（例如“en”），将`<CC>`替换为相应国家的两个字母代码（例如“GB”）。`<charmap>`应该替换为所选语言区域的标准格式。可选的修饰符如“@euro”也可能存在。

运行以下命令可以获取 Glibc 支持的所有区域（locales）列表：

```
locale -a
```

字符映射（Charmaps）可以有多个别名，例如，“ISO-8859-1”也被称为“iso8859-1”和“iso88591”。某些应用程序无法正确处理各种同义词（例如要求将“UTF-8”写为“UTF-8”而不是“utf8”），因此在大多数情况下，为特定语言区域选择标准别名是最安全的。要确定标准名称，运行以下命令，`<locale name>`是`locale -a`为你喜好的区域提供的输出（在我们的示例中为“en_GB.iso88591”）。

```
LC_ALL=<locale name> locale charmap
```

# Linux From Scratch - 版本 11.0

对于“en_GB.iso88591”语言区域，上述命令将打印：

```
ISO-8859-1
```

这将导致最终语言区域设置为“en_GB.ISO-8859-1”。在将上述启发式方法找到的语言区域添加到 Bash 启动文件之前，对其进行测试是重要的：

```
LC_ALL=<locale name>  locale language
LC_ALL=<locale name>  locale charset
LC_ALL=<locale name>  locale int_curr_symbol
LC_ALL=<locale name>  locale int_prefix
```

上述命令应该打印语言名称、该区域使用的字符编码、本地货币以及进入该国家所需的拨打号码的前缀。如果上述任何命令失败并显示类似下面的消息，则意味着你的语言区域未在第 8.5 节“Glibc-2.34”中安装，或者不被 Glibc 的默认安装支持。

```
locale: Cannot set LC* to default locale: No file or directory
```

如果发生这种情况，你应该使用`localef`命令安装所需的语言区域，或者考虑选择不同的语言区域。进一步的说明将确保 Glib 不会出现此类错误信息。

如果语言区域名称不符合预期，其他软件包也可能运行异常（但可能显示任何错误消息）。在这种情况下，调查其他 Linux 发行版如何支持你的语言区域可能会提供一些有用信息。

一旦确定了正确的语言区域设置，创建`/etc/profile`文件：

```
cat /etc/profile << "EOF"
# Begin /etc/profile

export LANG=$LANG.<CC>.<charset><@modifiers>

# End /etc/profile
EOF
```

“C”（默认）和“en_US.utf-8”（为美国英语用户推荐的）语言区域是不同的。“C”使用 US-ASCII 7 位字符集，并将带有高位位的字节视为无效字符。这就是为什么，例如，`ls`命令在语言区域中用问号提交它们。此外，当尝试从 Mint 或 Petri 在不符合 RFC 标准的消息中发送此类字符时（输出中的字符集被指示为“unknown 8-bit”）。因此，只有在你确定时才能使用“C”语言区域。

UTF-8 语言区域不被某些程序支持。参见 https://www.linuxfromscratch.org/blfs/view/11.0/locale-issues.html。

## 9.8. 创建 /etc/inputrc

`inputrc`文件是 readline 库的配置文件，当用户在终端输入行时提供编辑功能。它被 bash 以及许多其他应用程序使用。

大多数人不需要用户特定的功能，如果你以后决定基于单个用户覆盖默认设置，可以在用户的主目录下创建一个`.inputrc`文件。

欲了解如何编辑`inputrc`的更多信息，请参阅 info 下的 Readline 章节。

下方的全局`inputrc`带有注释说明各个选项的作用。使用以下命令创建供所有登录用户使用的文件：

```
# Begin /etc/inputrc
# Modified by Chris Lynn <roryo@dynup.net>

# 允许命令提示符换行到下一行
set horizontal-scroll-mode Off
```

```
# 启用8位输入
set meta-flag On
set input-meta On
```

```
# 关闭8位剥离
set convert-meta Off
```

```
# 保留第8位用于显示
set output-meta On
```

```
# 可见或可听的
set bell-style none
```

```
# 将列表 1 中的所有转义序列映射到 readline 特定函数
"\ed0": backward-word
"\ec0": forward-word
```

```
# 用于 linux 控制台
"\e[1~\
```

```
# 用于 xterm
"\e0H~\
```

```
# 用于 Konsole
"\e[H~\
```

```
# End /etc/inputrc
EOF
```

## 9.9. 创建 /etc/shells 文件

`shells`文件包含系统上的登录 shell 列表。应用程序使用此文件确定 shell 是否有效。对于每个 shell 应该存在单行，由相对于目录结构根（/）的 shell 路径组成。

例如，`chsh`通过此文件判断非权限用户是否可以更改其帐户的登录 shell。如果命令名称未列表中，用户将被拒绝更改 shell 的权限，或者 FTP 守护程序拒绝访问未包含在此文件中的 shell 的用户。

这是 GDM 等应用程序的要求，如果它找不到`/etc/shells`，则不会填充脸浏览器，或者 FTP 守护程序拒绝访问未包含在此文件中的 shell 的用户。

```
cat > /etc/shells << "EOF"
# Begin /etc/shells
/bin/sh
/bin/bash

# End /etc/shells
EOF
```

# 第 10 章.让 LFS 系统可启动

## 10.1. 引言

现在是让 LFS 系统可以启动了。本章将讨论创建`/etc/fstab`文件、为新的 LFS 系统构建内核，以及安装 GRUB 引导加载程序，以便在启动时选择 LFS 系统。

## 10.2. 创建 /etc/fstab 文件

`/etc/fstab`文件被某些程序用于确定哪些文件系统默认挂载、挂载顺序，以及在挂载之前必须检查哪些文件系统（完整性条目）。创建一个新的文件系统表如下：

```
cat > /etc/fstab << "EOF"
# Begin /etc/fstab
# file system mount-point type options dump fsck order
/dev/<xxx> / <fff> defaults 1 1
/dev/<yyy> swap swap pri=1 0 0
/proc /proc proc nouid,noexec, nodev 0 0
sysfs /sys sysfs nouid,noexec, nodev 0 0
devpts /dev/pts devpts gid=5,mode=620 0 0
tmpfs /run tmmpfs defaults 0 0
devmtmps /dev devmtmps mode=0755,nosuid 0 0
# End /etc/fstab
EOF
```

将`<xxx>`、`<yyy>`和`<fff>`替换为适用于系统的值，例如`sda2`、`sda5`和`ext4`。

关于文件的详细信息，请参阅`man fstab`。

源自 MS-DOS 或 Windows 文件系统（即 vfat, nfsfs, cifs, iso9660, udf）需要特殊的选项`utf8`，以便文件名中的非 ASCII 字符能够被正确解释。对于非 UTF-8 的本地化区域（locale），`iocharset`的值应设置为与本地区域的字符集相同，并调整到内核可以接受。如果相关的字符集已编译进内核或作为模块，这种方法是有效的。然而，如果本地区域的字符集是 UTF-8，则`iocharset=utf8`选项会使文件系统变得敏感。为此，对于 UTF-8 本地化区域，请使用`iocharset=utf8`的特殊选项`utf8`。vfat 和 smbfs 文件系统还需要`codepage`选项。它应该被设置为你国家 MS-DOS 下使用的代码页数字。例如，为了挂载 USB 驱动器，`_RU_KOI8-R`用户可能需要在分区中使用以下选项：

```
noauto,user,quiet, showexec, codepage=866, iocharset=koi8r
```

对于`_RU_UTF-8`用户对应的选项片段为：

```
noauto,user,quiet, showexec, codepage=866, utf8
```

注意，使用`iocharset`是 iso8859-1 的默认设置（这保持文件系统大小不敏感），`utf8`选项告诉内核使用 UTF-8 转换文件名，以便在 UTF-8 本地化区域中解释。

在内核配置期间，也可以为某些文件系统指定默认 codepage 和 iocharset 值。相关参数命名为“Default NLS Option”（CONFIG_NLS_DEFAULT）、“Default Remote NLS Option”（CONFIG_SMB_NLS_DEFAULT）、“Default codepage for FAT”（CONFIG_FAT_DEFAULT_CODEPAGE）以及“Default iocharset for FAT”（CONFIG_FAT_DEFAULT_IOCHARSET）。在内核编译时无法为 nfs 文件系统指定这些设置。

对于某些硬盘类型，可以使 ext3 文件系统在断电后依然可靠。为了做到，在`/etc/fstab`中相应的条目中添加`barrier=1`挂载选项。要检查磁盘驱动是否支持此选项，请在相应的磁盘上运行`hdparm`。例如，如果：

```
hdparm -I /dev/sda | grep NCQ
```

返回非空输出，则支持该选项。

注意：基于逻辑卷管理（LVM）的分区无法使用 barrier选项。

## 10.3. Linux-5.13.12

Linux 包包含 Linux 内核。

**预计构建时间：**1.5 - 130.0 SBU（通常约为 12 SBU）

**所需的磁盘空间：**1200 - 8800 MB（通常约为 1700 MB）

### 10.3.1. 内核的安装

构建内核涉及几个步骤——配置、编译和安装。阅读内核源码树中的 README 文件，以获取除本书配置内核方法之外的替代方法。

运行以下命令准备编译：

```
make mrproper
```

这确保了内核树是绝对干净的。内核团队建议在每次内核编译之前使用此命令。不要依赖解压后的内核源码是干净的。

有几种方法配置内核选项。通常，通过菜单驱动界面完成，例如：

```
make menuconfig
```

**可选 make 环境变量的含义：**

```
LANG=<host_LANG_value> LC_ALL=
```

这会将本地化设置设置为与主机使用的相同设置。这可能用于在 UTF-8 文本控制台上正确绘制 menuconfig curses 界面的线条。

如果使用，请确保将`<host_LANG_value>`替换为主机上 `$LANG`变量的值。你也可以改用主机的 `$LC_ALL`或 `$LC_CTYPE`的值。

**make menuconfig**

这会启动一个 ncurses 驱动的界面。对于其他（图形化）界面，输入**make help**。

有关内核配置的通用信息，请参阅 https://www.linuxfromscratch.org/hints/downloads/files/kernel-configuration.txt。BLFS 有一些关于 LFS 之外软件包特定内核配置要求的信息，请见 https://www.linuxfromscratch.org/blfs/view/11.0/longindex.html#kernel-config-index。关于构建和内核的更多信息可以在 http://krowhow.com/ln/ 找到。

> 设置内核配置的一个良好起点是运行**make defconfig**。这将基础配置设置为考虑了你当前系统架构的状态。

请确保启用/禁用以下功能，否则系统可能无法正常工作或完全无法启动：

```
Device Drivers --->
Generic Driver Options --->
[] Support for uevent helper [CONFIG_UEVENT_HELPER]
[*] Maintain a devtmpfs [CONFIG_DETMPFS]
```

# Linux From Scratch - 版本 11.0

根据需要，可能存在其他选项。对于 BLFS 所需的选项列表，请参阅 BLFS内核设置（https://www.linuxfromscratch.org/blfs/v11.0/longindex.html#kernel-config-index）。如果硬件使用 UEFI 你想启动它，应该按照 BLFS 调整某些内核配置。

上述配置项的原理：

- Support for uevent helper：在使用 Udev 时这可能会干扰设备管理。
- Maintain a devtmpfs：即使没有 Udev，内核也会创建设备节点。它在此基础上运行管理权限并添加符号链接。此配置项对于所有 Udev 用户都是必需的。

或者，在某些情况下 `make oldconfig` 可能合适。更多信息请见 README 文件。



如果需要，可以通过从主机系统（假设可用）拷贝内核配置文件 `.config` 到解压的 `linux-5.13.12` 目录来跳过内核配置。然而，我们不建议这种选项。最好探索所有内核菜单并从头创建内核配置。

编译内核映像和模块：

```
make
```

如果使用内核模块，可能需要模块配置。有关模块和内核配置的信息位于第 9.3 节“设备和模块概述”以及 `linux-5.13.12/Documentation` 目录下的内核文档。此外，`modprobe.d(5)` 可能让你感兴趣。

除非内核配置中内置模块支持，否则：

```
make modules_install
```

内核编译完成后，还需要额外的步骤来完成安装。某些文件需要拷贝到 `/boot` 目录。

> 如果系统有单独的 `/boot` 分区，拷贝的文件应该放在那里。最简单的方法是在继续之前，将主机（外部）的 `/boot` 挂载到 `/mnt/lfs/boot`。你系统中的 root 用户：

```
mount --bind /boot /mnt/lfs/boot
```

内核映像的路径可能根据使用的平台而异。下面的文件名可以根据情况更改，但文件名的主干为 `vmlinux`，以便与下一节描述的启动过程自动设置兼容。以下命令假设为 x86 架构：

```
cp -iv arch/x86/boot/bzImage /boot/vmlinuz-5.13.12-lfs-11.0
```

# Linux From Scratch - 版本 11.0

`System.map` 是内核的符号文件。它映射了内核 API 中每个函数的入口点，以及运行内核的内核数据结构的地址。它被用作调查内核问题时的一种资源。执行以下命令安装该文件：

```bash
cp -iv System.map /boot/System.map-5.13.12
```

由 `make menuconfig` 步骤产生的内核配置文件 `.config` 包含了所编译内核的所有配置选项。保留此文件以备后参考之用是一个好主意：

```bash
cp -iv .config /boot/config-5.13.12
```

安装 Linux 内核文档：

```bash
install -d /usr/share/doc/linux-5.13.12
cp -r Documentation/* /usr/share/doc/linux-5.13.12
```

需要注意的是，内核源码目录中的文件并不归 root 所有。当以 root 身份解压包时（我们在我们在 chroot 内部的操作的），文件将拥有打包者计算机上相应的用户 ID 和组 ID。这对于安装后删除任何包来说通常不是问题。然而，Linux 源码树通常会被保留很长时间。由于由于，包使用的任何用户 ID 可能会分配给机器上的某人。那个人将获得访问内核的权限。

> 注意

在许多情况下，对于以后在 BLFS 中安装的包，需要更新内核配置。与其他包不同，安装新构建的内核后没有必要删除内核源码树。

如果要保留内核源码树，请对 `linux-5.13.12` 目录运行 `chown -R 0:0` 以确保所有文件都归用户 root 所有。

> 警告

某些内核文档建议从 `/usr/src` 创建指向内核源码目录的符号链接。这适用于 2.6 系列之前的内核，并且在 LFS 文件系统中禁止创建，因为它可能会导致你希望在完整的 BLFS 系统上构建的软件包出现问题。

> 警告

系统包含目录 (`/usr/include`) 中的头文件始终应该是编译 libc 时所使用的那些头文件，即在第 5.4 节“Linux-5.13.12 API Headers”中安装的清理头文件。因此，它们绝不能被原始内核头文件或任何其他经过清理的内核头文件所替换。

## 10.3.2. 配置 Linux 模块加载顺序

大多数 Linux 模块会自动加载，但有时需要特定的指导。加载模块的程序 `modprobe` 或 `insmod` 使用 `/etc/modprobe.d/usb.conf` 来实现此目的。需要创建此文件，以便 USB 驱动程序（`ehci_hcd`、`ohci_hcd` 和 `uhci_hcd`）在构建为模块时能够按照正确的顺序加载；`ehci_hcd` 需要在 `ohci_hcd` 和 `uhci_hcd` 之前加载，以避免启动时出现警告。

运行以下命令创建一个新文件 `/etc/modprobe.d/usb.conf`：

```bash
install -v -m755 -d /etc/modprobe.d
cat /etc/modprobe.d/usb.conf << "EOF"
# Begin /etc/modprobe.d/usb.conf
install ohci_hcd /sbin/modprobe ehci_hcd ; /sbin/modprobe -i ohci_hcd ; true
install uhci_hcd /sbin/modprobe ehci_hcd ; /sbin/modprobe -i uhci_hcd ; true
# End /etc/modprobe.d/usb.conf
EOF
```

## 10.3.3. Linux 的内容

安装的文件：`config-5.13.12`, `vmlinuz-5.13.12-lfs-11.0` 和 `System.map-5.13.12`

安装的目录：`/lib/modules`, `/usr/share/doc/linux-5.13.12`

## 要描述

- `config-5.13.12` 包含了内核的所有配置选项

- `vmlinuz-5.13.12-lfs-11.0` Linux 系统的引擎。当启动电脑时，内核是操作系统第一个加载的部分。它检测并初始化计算机硬件的所有组件，然后将这些组件作为文件树的形式提供给软件，并将单 CPU 转换为一台能够看似同时运行数十个程序的多任务机器。

- `System.map-5.13.12` 地址和符号的列表；它映射了内核中所有函数和数据结构的入口点和地址

## 10.4. 使用 GRUB 设置启动过程

> 注意：如果你的系统支持 UEFI 且你想通过 UEFI 启动 LFS，你应该跳过此页，并使用 BLFS 页面提供的说明配置支持 UEFI 的 GRUB。

### 10.4.1. 介绍

> 警告：错误地配置 GRUB 会导致你的系统无法运行，除非有 CD-ROM 或可启动 USB 驱动器等其他启动设备。启动你的 LFS 系统并不此部分。你可能只想修改你的引导程序，例如 Grub-Legacy、GRUB2 或 LILO。

确保启动磁盘已就绪。为了使其工作，你必须挂载 chroot。如果你不在 chroot 中，请执行：

```bash
cd /mnt/lfs
chroot /mnt
```

如果你已处于 chroot 中，请继续下一步。

生成 GRUB 镜像：

```bash
grub --output=/boot/grub.img /dev/sda
```

### 10.4.2. GRUB 命名规范

GRUB 使用 `(hdn,m)` 格式的命名，其中 n 是磁盘编号，m 是分区编号。磁盘编号从 0 开始，但分区编号从 1 开始。例如，`da1` 是 `(hd0,1)`。

### 10.4.3. 设置配置

GRUB 通过向分区写入数据来工作。建议为 `/boot` 使用较小的（200 MB）分区。

以下命令将覆盖当前的引导加载程序。如果不希望这样做（例如使用第三方引导管理器），请勿运行该命令。

```bash
grub-install /dev/sda
```

### 10.4.4. 创建 GRUB 配置文件

生成 `/boot/grub/grub.cfg`：

```bash
cat /boot/grub/grub.cfg << "EOF"
# Begin /boot/grub/grub.cfg
set default=0
set timeout=5

insmod ext2
set root=(hd0,2)
\menuentry "GNU/Linux, Linux 5.13.12-lfs-11.0" {
    linux /boot/vmlinuz-5.13.12-lfs-11.0 root=/dev/sda2 ro
}
EOF
```

## 第 11 章 结束

### 11.1. 结束

做得好！新的 LFS 系统已安装完成！祝愿你那闪亮的全新定制 Linux 系统上取得巨大成功。

创建一个 `/etc/lfs-release` 文件可能是一个好主意。通过这个文件，你（以及在我们某某时刻需要寻求帮助时）可以很容易地找到系统中安装了哪个版本的 LFS。运行以下命令创建此文件：

```
echo 11.0 > /etc/lfs-release
```

描述已安装系统的两个文件可以被安装在系统上的软件包使用，既可以是二进制形式，也可以通过构建的方式。

第一个文件显示了你的新系统相对于 Linux 标准基础（LSB）的状态。要创建此文件，运行：

```
cat > /etc/lfs-release << "EOF"
DISTRIB_ID="Linux From Scratch"
DISTRIB_RELEASE="11.0"
DISTRIB_CODENAME="<在此处输入名称>"
DISTRIB_DESCRIPTION="Linux From Scratch"
EOF
```

第二个包含大致相同的信息，被 systemd 和某些图形桌面环境使用。要创建此文件，运行：

```
cat > /etc/os-release << "EOF"
NAME="Linux From Scratch"
VERSION="11.0"
ID=lfs
PRETTY_NAME="Linux From Scratch 11.0"
VERSION_CODENAME="<在此处输入名称>"
EOF
```

请确保对 `DISTRIB_CODENAME` 和 `VERSION_CODENAME` 字段进行某种自定义，使你的系统独一无二。

### 11.2. 注册计数

既然你已经读完了这本书，你想要被记录为一名 LFS 用户吗？前往 https://www.linuxfromscratch.org/cgi-bin/lfscounter.php，通过输入你的名字和使用过的第一个 LFS 版本来注册成为 LFS 用户。

现在，让我们重启进入 LFS 吧。

### 11.3. 重启系统

现在所有软件都安装完毕，是时候重启你的电脑了。然而，你应该注意几点。你创建的系统是非常精简的，很可能不具备你继续后续所需的功能。通过在当前的 chroot 环境中从 BLFS 书中安装几个额外的软件包，你可以让自己在重启进入 LFS 安装系统后处于更好的后续位置。以下是一些建议：

- 像 Lynx 这样的文本浏览器将允许你在一个虚拟终端中轻松查看 BLFS 书，同时在另一个终端中构建软件包。

- `make-ca` 软件包将允许你设置本地信任的锚点证书，使系统能够验证远程服务器提供的 SSL 证书（例如，使用 HTTPS 的网站）。

- GPM 将允许你在虚拟终端中执行复制/粘贴操作。

- 如果你处于 `dhcpconfig` 不符合你网络需求的情况，安装如 `dhcpcd` 或 `dhcp` 的客户端部分软件包可能会有所帮助。

- 安装 `sudo` 对于以非 root 用户身份构建软件包并轻松将生成的包安装到你的系统中可能很有帮助。

- 如果你想在舒适的 GUI 环境中从远程系统访问你的新系统，请安装 `openssh`。

- 为了从互联网获取文件，请安装 `wget`。

- 为了连接无线接入点进行网络连接，请安装 `wpa_supplicant`。

- 最后，在此时阶段审查以下配置文件也是合适的：

  - `/etc/bashrc`

  - `/etc/dircors`

  - `/etc/fstab`

  - `/etc/hosts`

  - `/etc/inputrc`

  - `/etc/profile`

  - `/etc/resolv.conf`

  - `/etc/vimrc`

  - `/root/bash_profile`

  - `/root/bashrc`

  - `/etc/sysconfig/ifconfig.eth0`

既然我们已经说了这么多，让我们第一次启动我们那闪亮的全新 LFS 安装吧！从 chroot 环境退出：

```
logout
```

卸载 LFS 文件系统层次结构：

```
umount -Rv $LFS
```

现在，使用以下命令重启系统：

```
shutdown -r now
```

假设 GRUB 引导程序已如之前所述进行了设置，则菜单已设置为自动启动 LFS 11.0。

重启后，LFS 系统已准备就绪，并且可以根据需要添加更多软件。

### 11.4. 接下来怎么办？

感谢阅读这本 LFS 书。我们希望你发现这本书很有帮助，并学习了更多关于系统构建的知识。

现在 LFS 系统已经安装，你可能会想“接下来怎么办？”为了回答这个问题，我们为你整理了一份资源列表。

- 维护

  所有软件都会定期报告漏洞和安全公告。由于 LFS 系统是从源码编译的，因此跟进此类报告取决于你。有几个在线资源可以跟踪此类报告，下面列出了其中：

  - CERT（计算机应急响应小组）

    CERT 拥有一个邮件列表，用于发布有关各种操作系统和应用程序的安全警报。订阅信息可以在 http://www.us-cert.gov/cas/signup.html 获取。

  - Bugtraq

    Bugtrap 是一个完全公开的社区安全邮件列表。它发布新发现的安全问题，偶尔还会发布这些问题的潜在修复。订阅信息可以在 http://www.security.com/archive 获取。

  - Beyond Linux From Scratch

    《Beyond Linux Scratch》书籍涵盖了广泛软件的安装程序。

- LFS 提示

  LFS 提示是由志愿者提交的关于 Linux 之外问题的文档。位于 https://www.linuxscratch.org/blfs/view/11.0/

- 邮件列表

如果你需要帮助、想了解最新进展、想为项目做贡献等，可以订阅多个邮件列表。见第 11 章 - 邮件列表。

- Linux 文档项目

  Linux 文档项目 (TLDP) 的目标是协作解决所有 Linux 问题。TLDP 包含了大量的 HOWTO、指南和手册。位于 http://www.ldp.org/

## 第 V 部分 附录

# 附录 A 缩写与术语

- ABI 应用二进制接口

- ALFS 自动化 Linux From Scratch

- API 应用程序接口

- ASCII 信息交换标准

- BIOS 基础输入输出系统

- BLFS Beyond Linux Scratch

- BSD 软件发行版

- chroot 

- CMOS 互补金属氧化半导体

- COS 服务类别

- CPU 中央处理器

- CRC 冗余校验

- CVS 并版本系统

- DHCP 动态主机配置协议

- DNS 域名系统

- EGA 增强显卡

- IDE 集成驱动器

- IEEE 电气电子工程师学会

- IO 输入/输出

- IP 网络协议

- IPC 进程间通信

- IRC 即时聊天

- ELF 可执行可链接格式

- ext2 第二代扩展文件系统

- ext3 第三代扩展文件系统

- FAQ 常见问题解答

- FHS 文件层次结构标准

- FIFO 先入先出

- FQDN 完全限定域名名

- FTP 文件传输协议

- GB 千字节

- GCC GNU 编译器集

- GID 组标识

- GMT 格林尼标准时间

- HTML 超文本标记语言

- LED 发光二极管

- LFS Linux From Scratch

- LSB Linux 标准基础

- MB 字节

- MBR 主引导记录

- MD5 消息摘要 5

- NIC 网卡

- NLS 原生语言支持

- NNTP 网络新闻传输协议

- NPTL 原生 POSIX 线程库

- OSS 开放音频系统

- PCH 预编译头文件

- PCRE Perl正则表达式

- PID 进程标识

- PTY 伪终端

- QOS 服务质量

- RAM 随机访问内存

- RPC 远程过程调用

- RTC 实时钟

- SBU 标准构建单元

- SCO 圣十字公司

- SHA1 安全哈希算法 1

- TLDP Linux 文档项目

- TFTP 简单文件传输协议

- TLS 线程本地存储

- UID 用户标识

- umask 用户文件创建掩码

- USB 通用总线

- UTC 协调世界时

UUID 全局唯一标识符

VC 虚拟控制台

VGA 视频图形阵

VT 虚拟终端

# 附录 B 致谢

我们要感谢以下个人和组织对 Linux From Scratch (LFS) 所出的贡献。

- Gerard Beekmans <gerard@linuxfromscratch.org> – LFS 创建者

- Bruce Dubbs <dbubms@linuxfromscratch.org> – LFS 管理编辑

- Jim Gifford <jim@linuxfromscratch.org> – CLFS 项目共同领导人

- Pierre Labastie <pierre@linuxfromscratch.org> – BLFS 节点和 ALFS 负责人

- DJ Lucas <dj@linuxfromscratch.org> – LFS 和 BLFS 节点

- Ken Moffat <ken@linuxfromscratch.org> – BLFS 节点

- LFS 和 BLFS 邮件列表中的无数其他人员，他们通过提供建议、测试书籍以及提交错误报告（bug reports）、说明以及以及安装各种软件包的经验，帮助了这本书的成为可能。

## 翻译者

- Manuel Canales Esparca <macana@macenas-es.com> – 西班牙语 LFS 翻译项目

- Johan Lenglet <johan@linuxfromscratch.org> – 直至 2008 年法语 LFS 翻译项目



- Jean-Philippe Mengual <jmengual@linuxfromscratch.org> – 2008-2016 年法语 LFS 翻译项目
- Julien Lepiller <jlepiller@linuxfromscratch.org> – 2017 年至今的法语 LFS 翻译项目
- Anderson Lizarro <lizardardo@linuxfromscratch.org> – 葡萄牙语 LFS 翻译项目
- Thomas Reitelbach <trt@erdfunkstelle.de> – 德语 LFS 翻译项目
- Anton Maisak <info@linuxfromscratch.org> – 俄语 LFS 翻译项目
- Elena Shevcova <helen@linuxfromscratch.org> – 俄语 LFS 翻译项目

## 镜像维护者

### 美洲镜像
- Scott Kveton <scott@uosl.org> – lfs.oregonstate.edu 镜像
- William Astle <last@l-web.net> – ca.linuxfromscratch.org
- Eujon Sellers <jpolen@rackspace.com> – lfs.introspeed.com 镜像
- Justin Knier <tim@edge.net> – lfs-matrix.net

### 南美镜像
- Manuel Canales Esparca <manuel@linuxfromscratch.org> – Lsfmirror,lfs-es.edu 镜像
- Luis Falcon <Luis Falcon> – torredehanoi.org 镜像

### 欧洲镜像
- Guido Passet <guido@primelay.net> – nl.linuxfromscratch.org 镜像
- Bastian Jacques <baafie@planet.nl> – lfs.pagefault.net 镜像
- Sven Cransoff <sven.cransoff@line.be> – lfs.line.be 镜像
- Scarlet Belgium – lfs.scarlet.be 镜像
- Sebastian Faulborn <info@alaliensoft.org> – lfs.aliensoft.org 镜像
- Siuat Fox <stuart@dentouse.me> – lfs.dentouse.me 镜像
- Ralf Uhhmann <admin@realhost.de> – LFS.oss-fromscratch.org 镜像
- Anton Sprinz <anton.sprinz@tuwien.ac.at> – at.linuxfromscratch.org 镜像
- Fredrik Danerklint <fredan-lfs.fredan.org> – se.linuxfromscratch.org 镜像
- Franck <frank@linuxpurtourscom.org> – lfs.linuxpurtourscom.org 镜像
- Philippe Baque <baque@cict.fr> – lfs.cict.fr 镜像
- Vitaly Cheekasin <gjouya@pilgrims.org> – Lfs.pilgrims.org 镜像
- Benjamin Heil <kontakt@wankoo.org> – Lfs.wankoo.org 镜像
- Anton Maisak <anton@linuxfromscratch.org.ru> – linuxfromscratch.org.ru 镜像

### 亚洲镜像
- Satit Phhermsawang <satit@wbac.th> – lfs.phayonne.org 镜像
- Shizuel Co., Ltd., <info@shizu-net.jp> – lfs.mirror.shizu-net.jp 镜像
- Init World <http://www.initworld.com/> – Lfs.initworld.com 镜像

### 澳洲镜像
- Jason Arande <jason@dstc.edu.au> – au.linuxfromscratch.org 镜像

### 前项目团队成员
- Christine Barczak <theladyskye@linuxfromscratch.org>
- Archaic <archaic@linuxfromscratch.org> – LFS 技术撰作者/编辑、HLFS 项目负责人、BLFS 节点、Hinches and Patches 项目维护者
- Matthew Burgess <mathew@linuxfromscratch.org> – LFS 项目负责人、LFS 技术撰作者/编辑
- Nathan Coulson <nathan@linuxfromscratch.org> – LFS-Bootscripts 维护者
- Timothy Bauscher
- Robert Briggs
- Ian Colton
- Jeroen Coumans <jeroen@linuxfromscratch.org> – 网站开发者、FAQ 维护者
- Manuel Canales Esparcia <manuel@linuxfromscratch.org> – 网站开发者、FAQ 维护者
- Alex Greenoud
- Mark Herend
- Jeremy Hunt
- Bryan
- Bryan Kadz <bryan@linuxfromscratch.org>
- Randy McMurchy <randy@linuxfromscratch.org>
- Daniel Nicholson <dnicholson@linuxfromscratch.org>
- Alexander
- Nicholas Leipe <nicholas@linuxfromscratch.org>
- Seth W.Klein
- Zack Winkles <zwink@gmail.com>
- Jeremy Utley <jeremy@linuxfromscratch.org>
- Tushar <tushar@linuxfromscratch.org>
- James Robertson <jober@linuxfromscratch.org>
- Jesse Tie <jesse@linuxfromscratch.org>
- Greg Schafer <gschafer@zip.com>
- Ryan Oliver <ryan@linuxfromscratch.org>
- Douglas Reno <renod@linuxfromscratch.org>
- Scot Mcerson <scot@linuxfromscratch.org>

# 附录 C 依赖

LFS 构建的每个软件包都依赖于一个或多个依赖项。由于这些依赖，软件包的构建顺序非常重要。本页目的是记录每个软件包的依赖关系。对于每个构建的软件包，下面列出了三种有时是五种类型的依赖。第一列表列出了编译和安装该软件包所需的软件包。第二列表列出了在使用该软件包的程序或库时必须提供的软件包。第三列表列出了除了第一列表中的软件包外，运行测试套件所需的软件包。最后的依赖列表是 LFS 未涉及但对用户可能需要的可选软件包。这些软件包本身可能有额外的强制或可选依赖。对于这些依赖项，建议的做法是在完成 LFS 书后安装它们，并重新构建 LFS 软件包。在某些情况下，重新安装将在 BLFS 中说明。

### Acl
- 安装依赖：Attr, Bash, Binutils, Coreutils, GCC, Getext, Grep, M4, Make, Perl, Sed 和 Texinfo
- 运行时需要：Attr 和 Glibc
- 测试依赖：Automake, Diffutils, Findutils 和 Libool
- 必须在以下之前安装：Coreutils, Sed, Tar 和 Vim
- 可选依赖：无

### Attr
- 安装依赖：Bash, Binutils, Coreutils, GCC, Glibc, Grep, M4, Make, Perl, Sed 和 Texinfo
- 运行时需要：Glibc
- 测试依赖：Automake, Diffutils, Findutils 和 Libool
- 必须在以下之前安装：Acl 和 Libcapac
- 可选依赖：无

### Autoconf
- 安装依赖：Bash, Coreutils, Grep, M4, Make, Perl, Sed 和 Texinfo
- 运行时需要：Bash, Coreutils, Grep, M4, Make, Sed 和 Texinfo
- 测试依赖：Automake, Diffutils, Findutils, GCC 和 Libool
- 必须在以下之前安装：Automake
- 可选依赖：Emac

## Automile
安装依赖于：Autoconf, Bash, Coreutils, Gettext, Grep, M4, Make, Perl, Sed, 以及 Texinfo
运行时需要：Bash, Coreutils, Grep, M4, Sed 和 Texinfo
测试套件依赖于：Binutils, Bison, Bzip2, DejGNU, Diffutils, Expect, Findutils, Flex, GCC, Gettext, Gzip, Libtool 和 Tar
必须先安装于：无
可选依赖：无

## Bash
安装依赖于：Bash, Binutils, Bison, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, Make, Ncurses, Patch, Readline, Sed, 以及 Textinfo
运行时需要：Glib, Ncurses 和 Readline
测试套件依赖于：Expect 和 Shadow
必须先安装：无
可选依赖：Xorg

## Bc
安装依赖于：Bash, Binutils, Coreutils, GCC, Glib, Grep 和 Make
运行时需要：Glib, Ncurses 和 Readline
测试套件依赖于：Gawk
必须先安装：Linux
可选依赖：无

## Binutils
安装依赖于：Bash, Binutils, Coreutils, Diffutils, File, Flex, Gawk, GCC, Glibc, Grep, Make, Perl, Sed, Texinfo, 以及 Zlib
运行时需要：Glibc 和 Zlib
测试套件依赖于：DeGNU 和 Expect
必须先安装：无
可选依赖：Elfutils

## Bison
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Grep, M4, Make, Perl 和 Sed
运行时需要：Glibc
测试套件依赖于：Diffutils, Findutils 和 Flex
必须先安装：Kbd 和 Tar
可选依赖：Doxygen

## Bzip2
安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Glibc, Make 和 Patch
运行时需要：Glibc
测试套件依赖于：无
必须先安装：File
可选依赖：无

## Check
安装依赖于：Gawk, GCC, Grep, Make, Sed 和 Texinfo
运行时需要：Bash 和 Gawk
测试依赖于：无
必须先安装：无
可选依赖：无

## Coreutils
安装依赖于：Bash, Binutils, Coreutils, GCC, Glibc, GMP, Grep, Libcap, Make, Perl, Sed, 以及 Texinfo
运行时需要：Glibc
测试依赖于：Diffutils, E2fsprogs, Findutils, Shadow 和 Util-linux
必须先安装：Bash, Diffutils, Eudev, Findutils 和 Man-DB
可选依赖：Expect.pm 和 IO::Tty

## DejaGNU
安装依赖于：Bash, Coreutils, Diffutils, Expect, GCC, Grep, Make, Sed 和 Texinfo
运行时需要：Expect 和 Bash
测试依赖于：无
必须先安装：无
可选依赖：无

## Diffutils
安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Gettext, Glibc, Grep, Make, Sed 以及 Texinfo
运行时需要：Glibc
测试依赖于：Perl
必须先安装：无
可选依赖：无

## E2fsprogs
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Gzip, Make, Texinfo 以及 Util-linux
运行时需要：Glibc 和 Util-linux
测试依赖于：Procs-ng 和 Psmisc
必须先安装：无
可选依赖：无

## Eudev
安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Glibc, Gperf, Make, Sed 以及 Util-linux
运行时需要：Glibc, Kmod, Xz, Util-linux 和 Zlib。
测试依赖于：无
必须先安装：无
可选依赖：无

## Expat
安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Glib, Grep, Make 和 Sed
运行时需要：Glibc
测试套件依赖于：无
必须先安装：Python 和 XML::Parser
可选依赖：无

## Expect
安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Glib, Grep, Make, Patch, Sed 以及 Tcl
运行时需要：Glibc 和 Tcl
测试套件依赖于：无
必须先安装：无
可选依赖：Tk

## File
安装依赖于：Bash, Binutils, Bzip2, Coreutils, Diffutils, Gawk, GCC, Glib, Grep, Make, Sed, Xz 以及 Zlib
运行时需要：Glib, Bzip2, Xz 和 Zlib
测试套件依赖于：无
必须先安装：无
可选依赖：libsecc

## Fuditils
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Grep, Sed 以及 Texinfo
运行时需要：Bash 和 Glib
测试套件依赖于：DejaGNU, Diffutils 和 Expect
必须先安装：无
可选依赖：无

## Flex
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Grep, M4, Make, Patch, Sed 以及 Texinfo
运行时需要：Bash, Glibc 和 M4
测试套件依赖于：Bison 和 Gawk
必须先安装：Binutils, IProute2, Kbd

## Gawk
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Grep, M4, Make, Sed 以及 Texinfo
运行时需要：Bash 和 Glib
测试套件依赖于：DejaGNU, Diffutils 和 Expect
必须先安装：无

## From Scratch 1.0
安装依赖于：Bash, Binutils, Coreutils, GCC, Glib, Grep, Patch, Sed,info
运行时需要：Glibc 和 Tcl
测试套件依赖于：无
必须先安装：无
可选依赖：Tk

## GDB
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Grep, Make, Perl, Sed
运行时需要：Glib 和 Readline
测试套件依赖于：Gawk
必须先安装：Linux
可选依赖：无

## Gettext
安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Grep, Sed 以及 Texinfo
运行时需要：Glib 和 Readline
测试套件依赖于：Shadow
必须先安装：无
可选依赖：无

## Glibc
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Gzip, Make, Texinfo 以及 Util-linux
运行时需要：Util-linux
测试依赖于：Procs-ng 和 Psmisc
必须先安装：无
可选依赖：无

## GMP
安装依赖于：Bash, Binutils, Coreutils, GCC, Glibc, Grep, Libcap, Make, Perl, Sed, 以及 Texinfo
运行时需要：Glibc
测试依赖于：Diffutils, E2fsprogs, Findutils, Shadow 和 Util-linux
必须先安装：Bash, Diffutils, Eudev, Findutils 和 Man-DB
可选依赖：Expect.pm 和 IO::Tty

## Gperf



# Linux From Scratch - Version 11.0

## 安装依赖于
`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Glibc`, `Gperf`, `Make`, `Sed` 以及 `Util-linux`

运行时需要：`Glibc`, `Kmod`, `Xz`, `Util-linux` 和 `Zlib`。

测试依赖于：无

必须先安装：无

可选依赖：无

## Grep

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Gettext`, `Glibc`, `Grep`, `Make`, `Sed` 以及 `Texinfo`

运行时需要：`Glibc`

测试依赖于：`Perl`

必须先安装：无

可选依赖：无

## Groff

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `GCC`, `Gettext`, `Glib`, `Grep`, `M4`, `Make`, `Patch`, `Sed`，以及 `Texinfo`

运行时需要：`Bash`, `Glibc` 和 `M4`

测试套件依赖于：`Bison` 和 `Gawk`

必须先安装：`Binutils`, `IProute2`, `Kbd`

## 安装依赖于
`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Glibc`, `Glib`, `Grep`, `Make`, `Ncurses`, `Sed`, `Texinfo`，以及 `Xz`

运行时需要：`Glibc`, `Kmod`, `Xz`, `Util-linux` 和 `Zlib`。

测试依赖于：无

必须先安装：无

可选依赖：无

## Gzip

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `GCC`, `Glibc`, `Make` 和 `Patch`

运行时需要：`Glibc`

测试套件依赖于：无

必须先安装：`File`

可选依赖：无

## GRUB

安装依赖于：`Bash`, `Binutils`, `Bison`, `Coreutils`, `Diffutils`, `GCC`, `Getext`, `Glibc`, `Grep`, `Make`, `Ncurses`, `Sed`, `Texinfo`，以及 `Xz`

运行时需要：`Bash`, `Getext`, `Glibc`, `Xz` 和 `Sed`。

测试依赖于：无

必须先安装：无

可选依赖：无

## iana-Etc

安装依赖于：`Coreutils`

运行时需要：无

测试依赖于：无可用测试套件

必须先安装：`Perl`

可选依赖：无

## Inutils

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Grep`, `Make`, `Ncurses`, `Patch`, `Sed`, `Texinfo`，以及 `Zlib`

运行时需要：`GCC`, `Glibc`, `Ncurses` 和 `man`

测试套件依赖于：无

必须先安装：`Tar`

可选依赖：无

# Inttool

安装依赖：`Bash`, `Gawk`, `Glibc`, `Make`, `Perl`, `Sed`，以及 `XML::Parser` `Autoconf`, `Automake`, `Bash`, `Glibc`, `Grep`, `Perl`, 和 `Sed`

运行时需要：

测试套件依赖：`Perl`

必须在之前安装：无

可选依赖：无

# IProute2

安装依赖：`Bash`, `Bison`, `Coreutils`, `Flex`, `GCC`, `Glibc`, `Libcap`, `Libelf`, `Linux API Headers`，以及 `Zlib`

运行时需要：`Bash`, `Coreutils`, `Glibc`, `Libcap`, `Libelf` 以及 `Zlib`

测试套件依赖：无可用的测试套件

必须在之前安装：无

可选依赖：`Berkeley D` 和 `iptables`

# Jinja2

安装依赖：`MarkupSafe` 和 `Python`

运行时需要：`MarkupSafe` 和 `Python`

测试套件依赖：无可用的测试套件

必须在之前安装：`Systemd`

可选依赖：无

# Kbd

安装依赖：`Bash`, `Binutils`, `Bison`, `Check`, `Coreutils`, `Flex`, `GCC`, `Gettext`, `Glibc`, `Gzip`, `Patch`, `Make`，和 `Sed`

运行时需要：`Bash`, `Coreutils` 和 `Glibc`

测试套件依赖：无

必须在之前安装：无

可选依赖：无

# Kmod

安装依赖：`Bash`, `Binutils`, `Bison`, `Coreutils`, `Flex`, `GCC`, `Gettext`, `Glibc`, `Gzip`, `Make`, `Pkg-config`, `Sed`, `Xz` 以及 `Zlib`

运行时需要：`Glibc`, `Xz` 以及 `Zlib`

测试套件依赖：无可用的测试套件

必须在之前安装：`Eudev`

可选依赖：无

# Less

安装依赖：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `GCC`, `Grep`, `Ncurses`，以及 `Sed`

运行时需要：`Glibc` 和 `Ncurses`

测试套件依赖：无可用的测试套件

必须在之前安装：`Gzip`

可选依赖：`PCRE`

# Libcap

安装依赖：`Attr`, `Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Perl`, `Make`，和 `Sed`

运行时需要：`Glibc`

测试套件依赖：无

必须在之前安装：`IPRoute2` 和 `Shadow`

可选依赖：`Linux-PAM`

# Libelf

安装依赖：`Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc` 以及 `Make`

运行时需要：`Glibc` 和 `Zlib`

测试套件依赖：无

必须在之前安装：`IPRoute2` 和 `Linux`

可选依赖：无

# Libffi

安装依赖：`Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Make`，以及 `Sed`

运行时需要：`Glibc`

测试套件依赖：`DejaGnu`

必须在之前安装：`Python`

可选依赖：无

# Libpipeline

安装依赖：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Gawk`, `GCC`, `Glibc`, `Grep`, `Make`, `Sed`，以及 `Texinfo`

运行时需要：`Glibc`

测试套件依赖：`Check`

必须在之前安装：`Man-DB`

可选依赖：无

# Libtool

安装依赖：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Gawk`, `GCC`, `Glibc`, `Grep`, `Make`, `Sed` 以及 `Texinfo`

运行时需要：`Autoconf`, `Automake`, `Bash`, `Binutils`, `Coreutils`, `File`, `GCC`, `Glibc`, `Grep`, `Make` 以及 `Sed`

测试套件依赖：`Autoconf`, `Automake` 以及 `Findutils`

必须在之前安装：无

可选依赖：无

# Linux

安装依赖：`Bash`, `Bc`, `Binutils`, `Coreutils`, `Diffutils`, `Findutils`, `GCC`, `Glibc`, `Grep`, `Gzip`, `Kmod`, `Libelf`, `Make`, `Ncurses`, `OpenSSL`, `Perl`，以及 `Sed`

运行时需要：无

测试套件依赖：无可用的测试套件

必须在之前安装：无

可选依赖：无

## Linux API Headers

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Findutils`, `GCC`, `Glibc`, `Grep`, `Gzip`, `Make`, `Perl` 以及 `Sed`

运行时需要：无

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## M4

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Grep`, `Make`, `Sed` 以及 `Texinfo`

运行时需要：`Bash` 和 `Glibc`

测试套件依赖于：`Diffutils`

必须在之前安装：`Autoconf` 和 `Bison`

可选依赖：`libsigsegv`

## Make

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `GCC`, `Gettext`, `Glibc`, `Grep`, `Make`, `Sed` 以及 `Texinfo`

运行时需要：`Glibc`

测试套件依赖于：`Perl` 和 `Procps-ng`

必须在之前安装：无

可选依赖：`Guile`

## Man-DB

安装依赖于：`Bash`, `Binutils`, `Bzip2`, `Coreutils`, `Flex`, `GCC`, `GBM`, `Gettext`, `Glibc`, `Grep`, `Groff`, `Gzip`, `Less`, `Libpipeline`, `Make`, `Sed` 以及 `Xz`

运行时需要：`Bash`, `GBM`, `Groff`, `Glibc`, `Gzip`, `Less`, `Libpipeline` 以及 `Zlib`

测试套件依赖于：`Util-linux`

必须在之前安装：无

可选依赖：`libsecomp`

## Man-Pages

安装依赖于：`Bash`, `Coreutils` 和 `Make`

运行时需要：无

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## MarkupSafe

安装依赖于：`Python`

运行时需要：`Python`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Systemd`

可选依赖：

## Meson

安装依赖于：`Python`

运行时需要：`Python`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Systemd`

可选依赖：无

## Procps-ng

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Gawk`, `Glibc`, `Grep`, `Make`, `Patch`, `Sed`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Linux`

可选依赖：无

## Ninja

安装依赖于：`Binutils`, `Coreutils`, `GCC`, `Python`

运行时需要：`Python`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Meson`

可选依赖：无

## Popt

安装依赖：`pkg-config`

运行时需要

必须在之前安装：`Kmod`

可选依赖：`OpenSSL`

## Ppsisc

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Grep`, `Ncurses`, `Sed`

运行时需要：`Glibc`, `Ncurses`

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## Python

安装依赖：`Bash`, `Binutils`, `GCC`, `Glibc`, `Make`

运行时需要：`Python`

## Perl

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Grep`, `Make`, `Sed`

运行时需要：`Glibc`

测试套件依赖于：`Diffutils`

必须在之前安装：`Python`

可选依赖：无

## Readline

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Glibc`, `Grep`, `Make`, `Texinfo`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试件

必须在之前安装：无

可选依赖：无

## Sed

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Grep`, `Make`, `Sed`, `Texinfo`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## Syslog

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Grep`, `Make`, `Texinfo`

运行时需要：`Glibc`, `Perl`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Coreutils`

可选依赖：无

## Sysd

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Make`, `Patch`, `Sed`

运行时需要：`Glibc`

测试套件依赖于：无

必须在之前安装：无

可选依赖：无

## Texinfo

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Gawk`, `Glibc`, `Grep`, `Make`, `Sed`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## Vim

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Grep`, `Make`, `Sed`, `Texinfo`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## Zlib

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Make`

运行时需要：`Glibc`

测试套件依赖于：无

必须在之前安装：无

可选依赖：无



运行时需要：`Autoconf`, `Automake`, `Bash`, `Binutils`, `Coreutils`, `File`, `GCC`, `Glibc`, `Grep`, `Make` 以及 `Sed`

测试套件依赖：`Autoconf`, `Automake` 以及 `Findutils`

必须在之前安装：无

可选依赖：无

# Linux

安装依赖：`Bash`, `Bc`, `Binutils`, `Coreutils`, `Diffutils`, `Findutils`, `GCC`, `Glibc`, `Grep`, `Gzip`, `Kmod`, `Libelf`, `Make`, `Ncurses`, `OpenSSL`, `Perl`, 以及 `Sed`

运行时需要：无

测试套件依赖：无可用的测试套件

必须在之前安装：无

可选依赖：无

# Linux From Scratch - Version 11.0

## Linux API Headers

**安装依赖于：**`Bash`, `Binutils`, `Coreutils`, `Findutils`, `GCC`, `Glibc`, `Grep`, `Gzip`, `Make`, `Perl` 以及 `Sed`

**运行时需要：**无

**测试套件依赖于：**无可用的测试套件

**必须在之前安装：**无

**可选依赖：**无

## M4

**安装依赖于：**`Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Grep`, `Make`, `Sed` 以及 `Texinfo`

**运行时需要：**`Bash` 和 `Glibc`

**测试套件依赖于：**`Diffutils`

**必须在之前安装：**`Autoconf` 和 `Bison`

**可选依赖：**`libsigsegv`

## Make

**安装依赖于：**`Bash`, `Binutils`, `Coreutils`, `GCC`, `Gettext`, `Glibc`, `Grep`, `Make`, `Sed` 以及 `Texinfo`

**运行时需要：**`Glibc`

**测试套件依赖于：**`Perl` 和 `Procps-ng`

**必须在之前安装：**无

**可选依赖：**`Guile`

## Man-DB

**安装依赖于：**`Bash`, `Binutils`, `Bzip2`, `Coreutils`, `Flex`, `GCC`, `GBM`, `Gettext`, `Glibc`, `Grep`, `Groff`, `Gzip`, `Less`, `Libpipeline`, `Make`, `Sed` 以及 `Xz`

**运行时需要：**`Bash`, `GBM`, `Groff`, `Glibc`, `Gzip`, `Less`, `Libpipeline` 以及 `Zlib`

**测试套件依赖于：**`Util-linux`

**必须在之前安装：**无

**可选依赖：**`libsecomp`

## Man-Pages

**安装依赖于：**`Bash`, `Coreutils` 和 `Make`

**运行时需要：**无

**测试套件依赖于：**无可用的测试套件

**必须在之前安装：**无

**可选依赖：**无

## MarkupSafe

**安装依赖于：**`Python`

**运行时需要：**`Python`

**测试套件依赖于：**无可用的测试套件

**必须在之前安装：**`Systemd`

**可选依赖：**无

## Linux From Scratch - 11.0

## Meson

安装依赖于：`Ninja`, `Python`

运行时需要：`Python`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Systemd`

可选依赖：无

## MPC

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Diffawk`, `Glibc`, `Gp`, `Grep`, `Make`, `Sed`, `Texinfo`

运行时需要：`Glibc`

套套依赖依赖于：无

必须在之前安装：`GCC`

可选依赖：无

## MPFR

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Gawk`, `Gp`, `Grep`, `Texinfo`

运行时需要：`Glibc`, `GMP`

测试套件依赖依赖：无

必须在之前安装：`Coreutils`

可选依赖：无

## Procps-ng

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Gawk`, `Glibc`, `Grep`, `Make`, `Patch`, `Sed`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Linux`

可选依赖：无

## Ninja

安装依赖于：`Binutils`, `Coreutils`, `GCC`, `Python`

运行时需要：`Python`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Meson`

可选依赖：无

## Popt

安装依赖：`pkg-config`

运行时需要

必须在之前安装：`Kmod`

可选依赖：`OpenSSL`

## Ppsisc

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Grep`, `Ncurses`, `Sed`

运行时需要：`Glibc`, `Ncurses`

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## Python

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Expat`, `GCC`, `Gdbm`, `Gettext`, `Glibc`, `Grep`, 运行时需要

运行时需要：`pat`, `Gdbm`, `Glibc`, `Libffi`, `Ncurses`, `OpenSSL`, `Zlib`

测试套件依赖：`DBDB Valgrind`

必须在之前安装：`Ninja`

可选依赖：`Berkeley DB`, `nsl`, `Tk`

## Readline

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Glibc`, `Grep`, `Make`, `Ncurses`, `Sed`, `Texinfo`

运行时需要：`Glibc`, `Ncurses`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Bash` 和 `Gawk`

可选依赖：无

## Sed

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gettext`, `Glibc`, `Grep`, `Make`, `Sed`, `Texinfo`

运行时需要：`Accl`, `Attr`, 以及 `Glibc`

测试套件依赖于：`Diffutils` 和 `Gawk`

必须在之前安装：`E2fprogs`, `File`, `Libtool` 以及 `Shadow`

可选依赖：无

## Shadow

安装依赖于：`Acl`, `Attr`, `Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Findutils`, `Gawk`, `GCC`, `Gettext`, `Grep`, `Libcap`, `Make`, 以及 `Sed`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试套件

必须在之前安装：`Coreutils`

可选依赖：`CrackLib` 和 `Linux-PAM`

## Syslogd

安装依赖于：`Binutils`, `Coreutils`, `GCC`, `Glibc`, `Make`, 以及 `Patch`

运行时需要：`Glibc`

测试套件依赖于：无可用的测试套件

必须在之前安装：无

可选依赖：无

## Systemd

安装依赖于：`Acl`, `Attr`, `Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Expat`, `Gawk`, `GCC`, `Glibc`, `Gperf`, `Gre`, `Inttool`, `Jinja2`, `Libcap`, `Meson`, `Sed`, 以及 `Util-linux`

运行时需要：`Accl`, `Glibc`, `Libcap` 以及 `Util-linux`

测试套件依赖：无

必须在之前安装：无

# Sysinit

- **安装依赖于：** `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Make`, 和 `Sed`
- **运行时需要：** `Glibc`
- **测试套件依赖于：** 无可用的测试套件
- **必须先安装：** 无
- **可选依赖项：** 无

# Tar

- **安装依赖于：** `Acl`, `Attr`, `Binutils`, `Bison`, `Coreutils`, `GCC`, `Gettext`, `Glibc`, `Grep`, `Inutelis`, `Make`, `Sed`, 和 `Texinfo`
- **运行时需要：** `Acl`, `Attr`, `Bzip2`, `Glibc`, `Gzip`, 和 `Xz`
- **测试套件依赖于：** `Autoconf`, `Diffutils`, `Findutils`, `Gawk`, 和 `Gzip`
- **必须先安装：** 无
- **可选依赖项：** 无

# Tcl

- **安装依赖于：** `Bash`, `Binutils`, `Coreutils`, `Diffutils`, `GCC`, `Glibc`, `Grep`, `Make`, 和 `Sed`
- **运行时需要：** `Glibc` 和 `Zlib`
- **测试套件依赖于：** 无
- **必须先安装：** 无
- **可选依赖项：** 无

# Texinfo

- **安装依赖于：** `Bash`, `Binutils`, `Coreutils`, `GCC`, `Gettext`, `Glibc`, `Grep`, `Make`, `Ncurses`, `Patch`, 和 `Sed`
- **运行时需要：** `Glibc` 和 `Ncurses`
- **测试套件依赖于：** 无
- **必须先安装：** 无
- **可选依赖项：** 无

# Util-linux

- **安装依赖于：** `Bash`, `Binutils`, `Coreutils`, `Diffutils`, `Eudev`, `Findutils`, `Gawk`, `GCC`, `Gettext`, `Grep`, `Libcap`, `Make`, `Ncurses`, `Sed`, 和 `Zlib`
- **运行时需要：** `Glibc`, `Libcap`, `Ncurses`, `Readline`, 和 `Zlib`
- **测试套件依赖于：** 无
- **必须先安装：** 无
- **可选依赖项：** `smartmontools`

# Vim

- **安装依赖于：** `Acl`, `Attr`, `Binutils`, `Coreutils`, `Diffutils`, `GCC`, `Glibc`, `Grep`, `Make`, `Ncurses`, 和 `Sed`
- **运行时需要：** `Acl`, `Attr`, `Glibc`, `Python`, `Ncurses`, 和 `Tcl`
- **测试套件依赖于：** 无
- **必须先安装：** 无
- **可选依赖项：** `Xorg`, `GTK+2`, `LessTif`, `Ruby`, 和 `GPM`

# Linux From Scratch - 版本 11.0

# XML::Parser

- **安装依赖于：** `Bash`, `Binutils`, `Coreutils`, `Expat`, `GCC`, `Glibc`, `Make`, 和 `Perl`
- **运行时需要：** `Expat`, `Glibc`, 和 `Perl`
- **测试套件依赖于：** `Perl`
- **必须先安装：** `Tool`
- **可选依赖项：** 无

# Xz

- **安装依赖于：** `Bash`, `Binutils`, `Coreutils`, `Diffutils`, `GCC`, `Glibc`, 和 `Make`
- **运行时需要：** `Glibc`
- **测试套件依赖于：** 无
- **必须先安装：** `Eudev`, `File`, `GRUB`, `Kmod`, 和 `Man-Dev`
- **可选依赖项：** 无

# Zlib

- **安装依赖于：** `Bash`, `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Make`, 和 `Sed`
- **运行时需要：** `Glibc`
- **测试套件依赖于：** 无
- **必须先安装：** `File`, `Kmod`, `Perl`, 和 `Util-linux`
- **可选依赖项：** 无

# Zstd

- **安装依赖于：** `Binutils`, `Coreutils`, `GCC`, `Glibc`, `Gzip`, 和 `Xz`
- **运行时需要：** `Glibc`
- **测试套件依赖于：** 无
- **必须先安装：** `GCC`
- **可选依赖项：** 无

# 附录 D. Boot 和 sysconfig 脚本版本-20210608

附录中的脚本按照它们通常所在的目录列出。顺序为 `/etc/rc.d/init.d`、`/etc/sysconfig/etc/sysconfig/network-devices` 以及 `/etc/sysconfig/network-devices`。在每个章节内部，文件按照它们通常调用的顺序列出。

## D.1. /etc/rc.d/init.d/rc

`rc` 脚本是 `init` 调第一个脚本，并启动引导过程。

```bash
#!/bin/bash
################################################################
# 开始 rc

#get：主运行级别控制脚本
# 作者：Gerard Beekemans - gerard@linuxfromscratch.com
# DJ Lucas - djlucas@linuxfromscratch.com
# 更新：Bruce Dubbes - bdbubbs
# 版本：LFS 7.0
################################################################

/lib/lsb/init-functions

print_error_msg() {
    # 调用时会设置 log_failure_msg
    MSG="失败：\n你不应该读取此错误消息。\n"
    MSG="${MSG}这意味着发生了一个不可预见的错误\n"
    MSG="${MSG}$(i),\n"
    MSG="${MSG}$(其以返回值 ${error_value} 退出。\n"

    MSG="如果你能将此错误追踪到 ${DISTRO_MINI} 书中提供的\n"
    MSG="${MSG}文件中的一个，\n"
    MSG="${MSG}请通过 ${DISTRO_CONTACT} 告知我们。\n"
    log_failure_msg "${MSG}"
}

log_info_msg "按回车键继续..."
    wait_for_user
}
```

```bash
check_status_script() {
    # 调用时会设置 $i
    if [ ! -f ${i} ]; then
        log_warning_msg "${i} 不是一个有效的符号链接。"
        SCRIPT_STAT="1"
    fi
}
```

```bash
if [ -x ${i} ]; then
  log_warning_msg "${i} 不可执行。"
  SCRIPT_STAT="1"
fi
```

```bash
run() {
  if [ -z ${interactive} ]; then
    ${1} ${2}
    return $?
  fi
while true; do
  read -p "运行 ${1} ${2}？(是/否/继续) " -n 1
  echo
  case ${1} in
    c | C)
      interactive=""
      ${1} ${2}
      ret=$?
      break
      ;;
    n | N)
      return 0
      ;;
    y | Y)
      ${1} ${2}
      ret=$?
      break
      ;;
  esac
done
return $ret
}
```

```bash
# 读取任何本地设置/覆盖
[ -r /etc/sysconfig/rc.site ] && source /etc/sysconfig/rc.site

DISTRO=${DISTRO:-"Linux Scratch"}
DISTRO_CONTACT=${DISTRO_CONTACT:-"lfs-dev@linuxscratch.com"}
DISTRO_MINI=${DISTRO_MINI:-"LFS"}
PROMPT=${PROMPT:-"no"}

# 这些信号会导致脚本退出
trap "" INT

[ "${1}" != "" ] && runlevel=${1}

if [ -z "${runlevel}" ]; then
  echo "用法: $0 <runlevel>" >&2
  exit 1
fi
```

```bash
previous=${PREVLEVEL}
[ "${previous}" == "" ] && previous=N

if [ -d /etc/rc.d/${runlevel} ]; then
  log_info_msg "/etc/rc.d/${runlevel} 不存在。"
  exit 1
fi

if [ "${runlevel}" == "6" -o "${runlevel}" == "0" ]; then PROMPT="no"; fi

# 注意：在 '${runlevel}-7' 中是 'dash'
if [ "${runlevel}" == "S" ]; then
  [ -r /etc/sysconfig/console ] && source /etc/sysconfig/console
  dmesg -n "${runlevel}-7"
fi

if [ "${PROMPT}" == "yes" -a "$S" ]; then
  wlen=$(echo "欢迎来到 ${DISTRO}" | wc -c)
  welcome_message=$(echo "欢迎来到 ${DISTRO}")
  ilen=$(echo "按键进入交互式启动" | wc -c)
  i_message=$(echo "按键： ${PROMPT}")
  wcol=$(( (COLUMNS - wlen) / 2 ))
  col=$(( (COLUMNS - ilen) / 2 ))
```



```bash
time=":3"

echo -e "\n"

echo -e "\033${wcol}G${welcome_message}"

echo -e "\033${col}G${i_message}"

echo ""

read -t "$time" -n 1 interactive 2>&1 < /dev/null

fi
```

# 转换为小写

```bash
[ "${interactive}" == "I" ] && interactive="i"

[ "${interactive}" != "i" ] && interactive=""
```

# 如果存在，读取运行级别的状态文件

```bash
[ -r /run/interactive ] && source /run/interactive
```

# 尝试停止上一个运行级别启动的所有，在此运行级别被杀死

```bash
if [ "${previous}" != "!" ]; then

  for i in $(ls -v /etc/rc.d/${runlevel}.d* 2>/dev/null)
  do

    check_status_script

    if [ "${SCRIPT_STAT}" == "1" ]; then

      SCRIPT_STAT="0"

      continue

    fi

    suffix=${i#*/}/etc/rc.d/rc${runlevel}.D[0-9][0-9]
    prev_start=/etc/rc.d/${runlevel}.d/S[0-9][0-9]$suffix
    sys_istint_start=/etc/rc.d/${runlevel}.d/S[0-9][0-9]$suffix

    if [ "${runlevel}" != "6" ]; then
      if [ ! -f ($prev_start) -a ! -f ($sys_istint_start) ]; then
        MSG="警告：\nS${i}无法"
        MSG="${MSG}执行，因为它没有在"
        MSG="${MSG}上一个"
        MSG="${MSG}运行级别 (${previous})."
        continue
      fi
    fi

    run ${i} stop
    error_value=$?

    if [ "${error_value}" != "0" ]; then print_error_msg; fi
  done
fi
```

```bash
if [ "${previous}" != "N" ]; then export IN_BOOT=1; fi
if [ "${runlevel}" = "G" -a n "${FASTBOOT}" ]; then
  touch /fastboot
fi
```

# 启动此运行级别的所有函数

```bash
for i in $(ls -v /etc/rc.d/rc${runlevel}.d/S* 2>/dev/null)
do
# ... (注：此处由于原文重复且不完整，已根据逻辑停止翻译重复部分)
```

```bash
if [ "${error_value}" != "0" ]; then print_error_msg; fi

done
```

```bash
# 在切换到运行级别 S 时存储交互式变量，如果不存在则删除

if [ "${runlevel}" == "S" -a "${interactive}" == "i" ]; then

  echo interactive="i" > /run/interactive

else

  rm -f /run/interactive 2>/dev/null

fi
```

```bash
# 仅在初始启动时拷贝启动日志

if [ "${previous}" == "N" -a "${runlevel}" != "S" ]; then

  cat BOOTLOG >>var/log/boot.log

fi
```

```bash
# 标记启动结束

echo "----------" >> /var/log/boot.log
```

```bash
# 删除临时文件

rm -f BOOTLOG 2>/dev/null

# 结束 rc
```

## D.2. `/lib/lsb/init-functions`

```sh
#!/bin/sh

################################################################################

# 开始 /lib/lsb/init-functions

# ：运行级别控制函数

# 作者 :: Gerard Beekemans - gerard@linuxfromscratch.org

          : D Lucas - dj@linuxfromscratch.org

# 更新 :: Bruce Dubbs - bdububs@linuxfromscratch.org

# 版本 :: LFS 7.0

# 注意：代码基于 Matthias Benkens 的 simpleinit-msb

          http://winterdreche.de/linux/newboot/index.html

################################################################################
```

```bash
# 该文件应位于 /lib/lsb 目录下

################################################################################

## 环境设置

# 为环境设置默认值

umask 022

export PATH=/bin:/usr/bin:/usr/sbin

# 设置颜色命令，通过 echo 使用

# 请参阅 console_codes 获取更多信息

# 位于“ECMA-48 Set Graphics Rendition”章节

# 警告：当从 8 位字体切换到 9 位字体时，

# linux 控制台将重新解释加粗 (1)；

# 使用 9 位字体的前 256 个字符形。这不会影响帧缓冲控制台 (framebuffer consoles)

NORMAL="\033[39m"      # 标准控制台灰色

SUCCESS="\033[32m"      # 成功绿色

WARNING="\033[33m"     # 警告黄色

FAILURE="\033[31m"     # 失败红色

INFO="\033[36m"        # 信息浅青

BRACKET="\033[34m"     # 括号蓝色

# 使用带颜色的前缀

BMPREFIX=""

SUCCESS_PREFIX=$(SUCCESS) * $(NORMAL) ""

FAILURE_PREFIX=$(FAILURE) $(NORMAL) ""

WARNING_PREFIX=$(WARNING) *** $(NORMAL) ""

SKIP_PREFIX=$(INFO) S $(NORMAL) ""

SUCCESS_SUFFIX=$(SUCCESS) OK $[BRACKET]$(NORMAL)

FAILURE_SUFFIX=$(FAILURE) $[BRACKET] FAIL $[BRACKET]$(NORMAL)

WARNING_SUFFIX=$(WARNING) $[WARN]N $[BRACKET]$(NORMAL)

SKIP_SUFFIX=$(BRACKET) $[INFO] SKIP $[BRACKET]$(NORMAL)

BOOTLOG=/run/bootlog

KILLDELAY=0

SCRIPT_STAT="0"

# 设置任何用户定义的环境变量。无界面

[ -r /etc/config/rc.site ] && . /etc/config/rc.site

# 屏幕尺寸

# 查找当前屏幕大小

if [ -z "$(COLUMNS)" ]; then

  COLUMNS=$(stty)

  COLUMNS=${COLUMNS##*}

fi

# 当使用远程连接（如串口）时，tty尺寸返回

if [ "$COLUMNS" = "0" ]; then

  COLUMNS=80

fi

# 用于定位结果消息的测量

COL=$($($(COLUMNS) - 8))

WCOL=$($($(WCOL) - 2))

# 设置光标位置命令，通过 echo 使用

SET_COL="\033[$$(COL)H"      # 在 $COL 处

SET_WCOL="\033[$$(WCOL)G"     # 在 $WCOL 处

CUR_UP="\033[1A\033[0G"     # 向上移动，位于第0个字符

CURS_ZERO="\033[0G"
```

```bash
# start_daemon()

# 用法: start_daemon [-f] [-n nicelevel] [-p pidfile] filename [args...]

# 目的：将指定的程序作为守护进程运行

# 输入: -f (强制) 即使程序已运行也运行程序。

# -n nicelevel: 指定 nice 级别。参见 'man nice(1)'。

# -p pidfile: 使用指定的文件确定 PID。

# pathname: 指定程序的完整路径

# args: 传递给程序 (pathname) 的额外参数

# 返回值（由 LSB 退出状态码定义）：

#   - 0 - 程序正在运行或服务正常

#   - 1 - 通用或未指定的错误

#   - 2 - 无效或过多的参数

#   - 5 - 程序未安装

################################################################################

start_daemon()
{

  local force=""

  local nice=""

  local pidfile=""

  local retval=""

  # 处理参数
  while true
  do
    case "${1}" in
      -f)
        force="1"
        shift 1
        ;;
      -n)
        nice="${2}"
        ;;
      -p)
        pidfile="${2}"
        shift 2
        ;;
      -*)
        return 2
        ;;
      *)
        program="${1}"
        break
        ;;
    esac
  done

  # 检查程序是否存在
  if [ ! -f "$program" ]; then return 5; fi
  if [ -n "$pidfile" ]; then
    # 检查 PID 是否运行
    if kill -0 `cat "$pidfile"` 2>/dev/null; then
      return 0 # 程序正在运行
    fi
  fi

  # 执行程序
  if [ -n "$nice" ]; then
    nice -n "$nice" "$program" "$@" &
  else
    "$program" "$@" &
  fi

  local pid=$!

  if [ -n "$pidfile" ]; then
    echo $pid > "$pidfile"
  fi

  return 0
}
```

```bash
# killproc()

# 用法: killproc [-p pidfile] [signal]

# 目的：向程序发送信号

# 输入：-p pidfile 指定包含 PID 文件

# signal：要发送的信号（默认 TERM）

# pathname：要停止的程序

# 返回值（由 LSB 退出状态定义）：

#   - 0 - 程序已停止

#   - 1 - 通用或未指定的错误

#   - 2 - 无效或过多的参数

#   - 5 - 程序未找到

killproc()
{

  local pidfile=""

  local signal="${TERM}"

  local pathname

  # 处理参数
  while true
  do
    case "${1}" in
      -p)
        pidfile="${2}"
        shift 2
        ;;
      -*)
        signal="${1# -}"
        shift
        ;;
      *)
        pathname="${1}"
        break
        ;;
    esac
  done

  # 检查 PID
  if [ -n "$pidfile" ]; then
    local pid=$(cat "$pidfile" 2>/dev/null)
    if [ -z "$pid" ]; then
      return 0 # PID 文件不存在，视为停止
    fi

    # 发送信号
    kill -"$signal" "$pid" 2>/dev/null
    if [ $? -eq 0 ]; then
      # 等待进程退出
      local timeout=0
      while kill -0 "$pid" 2>/dev/null; do
        sleep 1
        timeout=$((timeout + 1))
        if [ $timeout -ge 10 ]; then
          kill -9 "$pid" 2>/dev/null
          return 1 # 超时错误
        fi
      done

      rm -f "$pidfile"
      return 0
    else
      return 1 # 发送信号失败
    fi
  else
    # 如果没有 PID 文件，使用 pkill
    if pkill -f "$pathname" 2>/dev/null; then
      return 0
    else
      return 1
    fi
  fi
}
```



# 为退出信号和控制信号执行不同的操作
`check_sig_type` "${signal}"

```bash
if [ "${?}" -eq "0" ]; then # 信号用于终止程序

  # 考虑到 pidlist 为空（pid 文件仍然存在且没有
  # 信号）
  if [ "${pidlist}" != "" ]; then

    # 杀死 pid 列表
    for pid in ${pidlist}; do
      do
        kill -0 "${pid}" > /dev/null

        if [ "${?}" -ne "0" ]; then
          # 进程已死，继续处理下一个并假设一切正常
          continue
        else
          kill "${signal}" "${pid}" 2 >/dev/null
        fi
      done

      # 如果设置了备选方案且程序仍在运行，
      # 使用备选方案
      if [ -n "${fallback}" -a [ "${piddead}" != "1" ]; then
        kill "${fallback}" "${pid}" 2>/dev/null
        sleep 0.1
      fi

      # 再次检查，如果仍在运行
      kill -0 "${pid}" 2>/dev/null && return 1
    fi

    # 检查并移除过时的 PID 文件。
    if [ -z "${pidfile}" ]; then
      # 获取 $program 的 basename
      prefix=$(echo "${program}" | sed 's/[^\/]*$//')
      progname=$(echo "${program}" | sed "s@${prefix}@")

      if [ -e "run/${progname}.pid" ]; then
        rm -f "run/${progname}.pid" 2>/dev/null
      fi
    else
      if [ -e "${pidfile}" ]; then rm -f "${pidfile}" 2>/dev/null; fi
    fi
  fi

# 对于不期望程序退出的信号，
# 让 kill 执行工作，并评估 kill 的返回值
else # check_sig_type - 信号未用于终止程序
  for pid in $(pidlist); do
    kill "${signal}" "${pid}"
    if [ "$?" -ne "0" ]; then return 1; fi
  done
fi
```

################################################################
# `pidrofproc()`
# 用法: `pidrofproc [-p pidfile] pathname`
# 目的：此函数返回特定守护进程的一个或多个 pid
# 输入: `-p pidfile`，使用指定的 pidfile 代替 pidof
#   `pathname`，指定程序的路径
# 返回值（由 LSB 状态码定义）：
#   0 - 成功（将 PID 输出到标准输出）
#   1 - 程序已死，pid 文件仍然存在（输出剩余的 PID）
#   3 - 程序未运行（无输出）
################################################################
```bash
pidrofproc() {
  local pidfile
  local program
  local prefix
  local progname
  local pidlist
  local lpid
  local exitstatus="0"

  # 处理参数
  while true; do
    case "${$1}" in
      -p)
        pidfile="${$2}"
        shift 2
        ;;
      *)
        program="${$1}"
        if [ -n "${$2}" ]; then
          # 参数过多
          # 既然是状态查询，返回未知
          return 4
        else
          break
        fi
    esac
  done

  # 如果未指定 PID 文件，则尝试查找一个。
  if [ -z "${pidfile}" ]; then
    # 获取程序的 basename
    prefix=$(echo "${program}" | sed 's/[^\/]*//')

    if [ -z "${prefix}" ]; then
      progname="${program}"
    else
      progname=$(echo "${program}" | sed "s@${prefix}@")
    fi

    # 如果存在同名的 PID 文件，则假设就是它。
    if [ -e "run/${program}.pid" ]; then
      pidfile="run/${program}.pid"
    fi

    # 如果设置了 PID 文件的文件，则使用它。
    if [ -n "${pidfile}" -a -e "${pidfile}" ]; then
      # 使用 pid 文件第一行的值
      pidlist=$(/bin/head -n 1 "${pidfile}")
      # 这可以可选写入 'sed 1q' 来替换 'head -n1'
      # 如果 LFS 将 /bin/head 移动到 /usr/bin/head
    else
      # 使用 pidof
      pidlist=$(pidof "${program}")
    fi

    # 确定所有列出的 PID 是否都在运行。
    for pid in ${pidlist}; do
      kill -0 ${pid} 2>/dev/null
      if [ "$?" -eq "0" ]; then
        lpids="${pid}"
      else
        exitstatus="1"
      fi
    done

    if [ -z "${pidfile}" -a ! -f "${pidfile}" ]; then
      return 3
    else
      echo "${lpids}"
      return "${exitstatus}"
    fi
}
```

####################################################################################
# `statusproc()`
# 用法: `statusproc [-p pidfile] pathname`
# 目的：此函数将特定守护进程的状态打印到标准输出
# 输入: `-p pidfile`，使用指定的 pidfile 代替 pidof
#   `pathname`，指定程序的路径
# 返回值：
#   0 - 状态已打印
#   1 - 输入错误。未指定要检查的守护进程。
################################################################
```bash
statusproc() {
  local pidfile
  local pidlist

  if [ "$#" -ne 0 ]; then
    echo "Usage: statusproc [-p pidfile] program"
    exit 1
  fi

  # 处理参数
  while true; do
    case "$1" in
      -p)
        pidfile="${$2}"
        shift 2
        ;;
      *)
        program="${$1}"
        if [ -n "${$2}" ]; then
          # 参数过多
          return 1
        else
          break
        fi
    esac
  done

  if [ -n "${pidfile}" ]; then
    pidlist=$(pidrofproc -p "${pidfile}")
  else
    pidlist=$(pidrofproc "${program}")
  fi

  if [ -n "${pidlist}" ]; then
    echo -e "${INFO}${program} is running"
  else
    if [ -n "${program}" ]; then
      echo -e "${WARNING}${program} is not running but run/${program}.pid exists"
    fi
    if [ -n "${pidfile}" ]; then
      echo -e "${WARNING}${program} is not running but ${pidfile} exists"
    else
      echo -e "${INFO}${program} is not running."
    fi
  fi
}
```

################################################################
# `timespec()`
# 目的：为启动日志格式化时间戳。
# 设置 `STAMP` 变量。
# 返回值：未使用
```bash
timespec() {
  STAMP="$(date +'%b %T `hostname`')"
  return 0
}
```

################################################################
# `log_success_msg()`
# 用法: `log_success_msg ["message"]`
# 目的：将成功状态打印到屏幕和
# 启动日志。
# 输入: $@ - 
# 返回值：未使用
################################################################
```bash
log_success_msg() {
  echo -n "${BMPPREFIX}$@"
  echo -e "${CURS_ZERO}${SUCCESS_PREFIX}${SET_COL}${SUCCESS_SUFFIX}"

  # 从日志文件中移除不可打印字符
  logmessage=$(echo "$@" | sed 's/\033[a-zA-Z]*///')

  timespec
  echo -e "${STAMP} ${logmessage} OK" >> ${BOOTLOG}

  return 0
}

log_success_msg2() {
  echo -n "${BMPPREFIX}$@"
  echo -e "${CURS_ZERO}${SUCCESS_PREFIX}${SET_COL}${SUCCESS_SUFFIX}"

  echo "OK" >> ${BOOTLOG}

  return 0
}
```

# Linux From Scratch - 版本11

######################################################################
# `log_failure_msg()`
# 用法: `log_failure_msg ["message"]`
# 目的：将失败状态打印到屏幕和
# 启动日志。
# 输入: $@ - 消息
# 返回值：未使用
######################################################################
```bash
log_failure_msg() {
  echo -ne "${BMPPREFIX}$@"
  echo -e "${CURS_ZERO}${FAILURE_PREFIX}${SET_COL}${FAILURE_SUFFIX}"

  # 从日志文件中移除不可打印字符
  logmessage=$(echo "$@" | sed 's/\033[a-zA-Z]*///')

  timespec
  echo -e "${STAMP} ${logmessage} FAIL" >> ${BOOTLOG}

  return 0
}
```

######################################################################
# `log_warning_msg()`
# 用法: `log_warning_msg ["message"]`
# 目的：将警告状态打印到屏幕和
# 启动日志。
# 返回值：未使用
######################################################################
```bash
log_warning_msg() {
  echo -ne "${BMPPREFIX}$@"
  echo -e "${CURS_ZERO}${WARNING_PREFIX}${SET_COL}${WARNING_SUFFIX}"

  # 从日志文件中移除不可打印字符
  logmessage=$(echo "$@" | sed 's/\033[a-zA-Z]*///')

  timespec
  echo -e "${STAMP} ${logmessage} WAR" >> ${BOOTLOG}

  return 0
}
```

```bash
log_skip_msg()
```

```bash
/bin/echo -ne "${BMPREFIX}${@}"

/bin/echo -ne "${CURS_ZERO}${SKIP_PREFIX}${SET_COL}${SKIP_SUFFIX}"

# 从日志文件中移除非打印字符

logmessage=$(echo "$@" | sed 's/\\033[a-zA-Z]*///g')

/bin/echo "$SKIP" >> $BOOTLOG

return 0
```

################################################################################

# `log_info_msg()`

# 用法: `log_info_msg message`

# 目的: 将信息消息打印到屏幕和

#  启动日志文件中。不打印末尾换行符。

# 返回值: 无

################################################################################
```bash
log_info_msg() {

  /bin/echo -ne ""${BMPREFIX}${@}"

  # 从日志文件中移除非打印字符

  logmessage=$(echo "$@" | sed 's/\\033[a-zA-Z]*///g'

  timesep

  /bin/echo -ne "${STAMP}${logmessage}" >> $BOOTLOG

  return 0

}
```

```bash
log_info_msg2() {

  /bin/echo -ne "${?}"

  # 从日志文件中移除非打印字符

  logmessage=$(echo "$@" | sed 's/\\033[a-zA-Z]*///g'

  /bin/echo -ne "${logmessage}" >> $BOOTLOG

  return 0

}
```

################################################################################

# `evaluate_retval()`

# 用法: 评估返回值并根据情况打印成功或失败

# 目的: 用于结束信息消息的便利函数

# 返回值: 无

################################################################################
```bash
evaluate_retval() {

  local error_value="${?}"

  if [ ${error_value} = 0 ]; then

    log_success_msg2

```

# Linux 从头构建 - 版本 11

```bash

else

log_failure_msg2

fi
```

```bash
################################################################################

# `check_signal()`

# 用法: `check_signal [ {-signal} ]`

# 目的: 检查有效信号。这没有在任何 LSB 草案中定义，

#   然而，它需要检查信号以确定

#   所选信号是否是其他函数的无效参数。

# # 输入: 接受形式为 {-signal} 的单个字符串值

# # 返回值:

#   0 - 成功（信号有效）

#   1 - 信号无效

################################################################################
```

```bash
check_signal() {

  local valsig

  # 为无效信号添加错误处理
```



```bash
valsig="ALRM-HUP-INT-KILL-PIPE-POLL-PROF-TERM-USR1-USR2"

valsig="$(valsig)-VTALM-STKILL-PWR-WINCH-CHRG-TSTP-TTIN"

valsig="$(valsig)-TTOU-STOP-ABRT-FPE-ILL-QUIT-SEGV-TRAP"

valsig="$(valsig)-SYS-BUS-CPU-XFSZ-0 -1 -2 -3 -4 -5 -6 -8 -9"

valsig="$(valsig)-SCPU -11 -13 -14 -15"

echo "$valsig" | grep -q "$1" > /dev/null

if [ "$2" -eq "0" ]; then

  return 0

else

  return 1

fi

}
```

```bash
################################################################################
# check_sig_type()
# 用法: check_signal [ {-signal} | {signal} ]
# 目的: 检查信号是否是程序终止信号或控制信号
#   这没有在任何 LSB 草案中定义，然而，需要
#   检查信号以确定它们是用于结束程序
#   还是仅仅是控制它。
# # 输入: 接受形式为 {-signal} 或 {signal} 的单个字符串值
# # 返回值:
#   0 - 信号用于程序终止
#   1 - 信号用于程序控制
################################################################################
```

```bash
check_sig_type() {
  local valsig
# 终止信号列表（限制为通用使用的项目）
valig="-ALRM -INT-KILL -TERM -PWR-STOP -ABRT-QUIT -2 -3 -6 -9 -14-15 "
echo "${valig}" | grep -q "$1" > /dev/null
if [ "$1" -eq "0" ]; then
    return 0
else
    return 1
fi
################################################################################
# wait_for_user()
# 目的: 如果不是无头系统则等待用户响应
################################################################################
wait_for_user()
{
    # 默认等待用户
    [ "${HEADLESS:=0}" = "0" ] && read ENTER
    return 0
}
################################################################################
# is_true()
# 目的: 测试变量是否为 true | yes | 1 的工具函数
################################################################################
is_true()
{
    [ "$1" = "1" ] || [ "$1" = "yes" ] || [ "$1" = "true" ] || [ "$1" = "y" ] || [ "$1" = "t" ]
}
# 结束 /lib/lsb/init-functions
```

## D.3. /etc/rc.d/init.d/mountvirtfs

```bash
#!/bin/bash
################################################################
# mountvirtfs
# 目的: 挂载虚拟文件系统
# 作者: Gerard Beekmans - gerard@linux.org
#        DJ Lucas - dj@linuxscratch.org
# 更新: Bruce Dubbs - dubds@linuxscratch.org
# 版本: LFS 7.0
################################################################

### BEGIN INIT INFO
# Provides: mountvirtfs
# Required-Start: localnet
# Should-Start:   modules
# Required-Stop:
# Should-Stop:
# Default-Start:  S
# Default-Stop:
# Short-Description: 挂载 /proc, /sys 和 /run
# Description: 挂载内核文件系统。
# Provided-By: LFS
### END INFO

# 确保内核支持模块
[ -e /proc/modules ] || exit 0

case "$1" in
start)
  # 如果没有模块文件则退出
  [ -r /etc/sysconfig/modules ] || exit 0

  log_info_msg "挂载系统: "

# 只有当用户提供了某些模块时尝试加载
while read module args; do
  # 忽略注释和空行
  case "$module" in
    ""|*#*) continue;;
  esac

  # 尝试加载模块，传递任何参数
  modprobe ${module} $args >/dev/null

  # 如果成功则打印模块名，否则记录
  if [ $? -eq 0 ]; then
    log_info_msg2 "${module}"
  else
    failedmod=${failedmod} ${module}
  fi
done < /etc/sysconfig/modules

# 在正确行打印成功加载模块的消息
log_success_msg2

# 打印可能失败加载的模块列表
if [ -n "${failedmod}" ]; then
    log_failure_msg "加载模块失败:${failedmod}"
    exit 1
fi
  ;;

)
  echo "用法: $0 {start}"
  exit 1
  ;;
esac
```

## D.4. /etc/rc.d/init.d/modules

```bash
#!/bin/bash
################################################
# modules
# 目的: 模块自动加载脚本
# 作者: Gerard Beekmans - gerard@linux.org
#        DJ Lucas - dj@linuxscratch.org
# 更新: Bruce Dubbs - dubds@linuxscratch.org
# 版本: LFS 7.0
################################################

### BEGIN INIT INFO
# Provides: modules
# Required-Start: mountvirtfs
# Should-Start:   modules
# Required-Stop:
# Should-Stop:
# Default-Start:  S
# Default-Stop:
# Short-Description: 加载 /etc/sysconfig/modules 中的模块
# Description: 加载模块。
# Provided-By: LFS
### END INFO

# 如果没有模块文件或没有有效条则退出
[ -r /etc/sysconfig/modules ] || exit 0
egrep -qv '^#' /etc/sysconfig/modules || exit 0

log_info_msg "加载模块: "

# 只有当用户确实提供了某些模块时尝试加载
while read module args; do
  # 忽略注释和空行
  case "$module" in
    ""|*#*) continue;;
  esac

  # 尝试加载模块，传递任何参数
  modprobe ${module} $args >/dev/null

  # 如果成功则打印模块名，否则记录
  if [ $? -eq 0 ]; then
    log_info_msg2 "${module}"
  else
    failedmod=${failedmod} ${module}
  fi
done < /etc/sysconfig/modules

# 在正确行打印成功加载模块的消息
log_success_msg2

# 打印可能失败加载的模块列表
if [ -n "${failedmod}" ]; then
    log_failure_msg "加载模块失败:${failedmod}"
    exit 1
fi
  ;;

)
  echo "用法: $0 {start}"
  exit 1
  ;;
esac
```

## D.5. /etc/rc.d/init.d/udev

```bash
#!/bin/bash
################################################
# udev
# 目的: udev 冷热拔脚本
# 作者: Zack Winkles, Alexander E. Patrakov,
#        DJ Lucas - dj@linuxscratch.org
# 更新: Bruce Dubbs - dubds@linuxscratch.org
# 版本: LFS 7.0
################################################

### BEGIN INIT INFO
# Provides: udev $time
# Required-Start: localnet
# Should-Start:   modules
# Required-Stop:
# Should-Stop:
# Default-Start:  S
# Default-Stop:
# Short-Description: 填充 /dev 中的设备节点
# Description: 挂载设备文件系统。
# Provided-By: LFS
### END INFO

# 确保内核支持模块
[ -e /proc/modules ] || exit 0

case "$1" in
start)
  # 如果没有 /run 则退出
  mountpoint /run || exit 0

  log_info_msg "挂载系统: "

  # 挂载 /proc, /sys 和 /run
  if mountpoint /proc; then
    log_info_msg2 "/proc"
  else
    mount -t procfs proc /proc || exit 1
  fi

  if mountpoint /sys; then
    log_info_msg2 "/sys"
  else
    mount -t sysfs sysfs /sys || exit 1
  fi

  if mountpoint /run; then
    log_info_msg2 "/run"
  else
    mount -t tmpfs tmpfs /run || exit 1
  fi

  log_info_msg "启动 udev: "
  udevadm trigger >/dev/null
  if [ $? -eq 0 ]; then
    log_info_msg2 "udev trigger"
  else
    log_failure_msg "udev trigger"
  fi
  ;;

stop)
  log_info_msg "停止 udev: "
  udevadm stop >/dev/null
  if [ $? -eq 0 ]; then
    log_info_msg2 "udev stop"
  else
    log_failure_msg "udev stop"
  fi
  ;;

)
  echo "用法: $0 {start}"
  exit 1
  ;;
esac
```

# Linux From Scratch - 版本 11.0

# Description: 在 /dev 上挂载临时文件并启动 udev 守护进程。

# X-LFS-Provided-By: 设备节点根据 udev 定义创建。

### END INIT INFO

```bash
. /lib/lsb/init-functions

case "$1" in
start)
  log_info_msg "正在向 /dev 填充设备节点..."
  if ! grep -q '[[space:]]sysfs/proc/mounts'; then
    log_failure_msg
    msg="失败：无法创建 "
    msg="${msg}没有 SysFS 文件系统的设备\n\n"
    msg="${msg}在您按下回键后，此系统将"
    msg="${msg}停止并关机。\n\n"
  fi
  log_info_msg "$msg"
  log_info_msg "按回车继续..."
  wait_for_user
  /etc/rc.d/init.d/halt stop
fi

# 启动 udev 守护进程以持续监控并处理
# uevents
/sbin/udev --daemon

# 现在遍历 /sys 以“热插拔”已经
# 的设备
/sbin/udevadm trigger --action=add --type=subsystems
/sbin/udevadm trigger --action=add --type=devices
/sbin/udevadm trigger --action=change --type=devices

# 现在等待 udev 处理我们触发的 uevents
if ! is_true "$OMIT_UDEV_SETTLE"; then
  /sbin/udevadm settle
fi
# 如果系统上有基于 LVM 的分区，请确保它们
# 已被激活以便使用。
if [ -x /sbin/vgchange ]; then /sbin/vgchange -a y >/dev/null; fi

log_success_msg2
*)
echo "用法: ${0}"
exit 1
esac

exit 0

# End udev
```

## D.6. /etc/rc.d/init.d/swap

```bash
#!/bin/sh
################################################################
# Begin swap
# Description : 交换分区控制脚本
# Authors : Gerard Beekemans - gerard@linuxfrom.com
# DJ Lucas - dj@linuxfrom.com
# Update : Bruce Dubbs - dububs@linuxfrom.com
# Version : 7.0
################################################################

### BEGIN INIT INFO
# Provides : swap
# Required-Start: udev
# Should-Start: modules
# Required-Stop: local
# Should-Stop: localfs
# Default-Start: S
# Default-Stop: 0
# Short-Description: 挂载和卸载交换分区。
# Description: 挂载和卸载 /etc/fstab 中定义的分区。
# X-LFS-Provided-By: LFS
### END INIT INFO

. /lib/lsb/init-functions

case "$1}" in
start)
    log_info_msg "正在激活所有交换/分区..."
    swapon -a
    evaluate_retval
    ;;

stop)
    log_info_msg "正在停用所有交换/分区..."
    swapoff -a
    evaluate_retval
    ;;

restart)
    $0 stop
    sleep 1
    $0 start
    ;;

status)
    log_success_msg "正在检索交换状态。"
    swapon -s
    ;;

*)
echo "用法: ${0} {start|stop|restart|status}"
exit 1
;;
esac

exit 0

# End swap
```

## D.7. /etc/rc/init.d/setclock

```bash
#!/bin/sh

################################################################

# Begin setclock

# Description : 设置时钟

# Authors : Gerard Beekemans - gerard@linuxfrom.com
```



# DJ Lucas - `dj@linuxfrom.com`

# Update : Bruce Dubbs - `dububs@linuxfrom.com`

# Version : 7.0

################################################

### BEGIN INIT INFO

# Provides:

# Required-Start: modules

# Should-Start:

# Required-Stop: syslog

# Default-Start: S

# Default-Stop:

# Short-Description: 从硬件时钟存储和恢复时间

# 在系统启动时，系统时间从 hwclock 获取。硬件时钟也可以在关机时设置。

# X-LFS-Provided-By: LFS

### END INIT INFO

```bash
. /lib/lsb/init-functions

[ -r /etc/sysconfig/clock ] && . /etc/sysconfig/clock

case "$(UTC)" in

yes|true|1)

CLOCKPARAMS="${CLOCKPARAMS} --utc"

;;

false|0)

CLOCKPARAMS="${CLOCKPARAMS} --localtime"

;;

esac

case "$1}" in

start)

hwclock ${CLOCKPARAMS} >dev/null

;;

stop)

log_info_msg "正在设置硬件时钟..."

hwclock ${CLOCKPARAMS} >dev/null

evaluate_retval

;;

*)

echo "用法: ${0} {start|stop}"

exit 1

;;

esac

exit 0
```

## D.8. `/etc/rc/init.d/checkfs`

```bash
#!/bin/sh
####################################################################
# Begin checksfs
# Description : 文件系统检查
# Authors : Gerard Beekemans - gerard@linuxfrom.com
# Luebeck - luebek@users.sourceforge.net
# DJ Lucas - dj@linuxfrom.com
# Update : Bruce Dubbs - dububs@linuxfrom.com
# Version : 7.0
# 基于 LFS-3.1 及早版本的 checksfs 脚本。
# 来自 man fsck
# 0 - 无错误
# 1 - 已纠正文件系统错误
# 2 - 系统已重启
# 4 - 留有未修复的文件系统错误
# 8 - 运行错误
# 16 - 使用或语法错误
# 32 - 用户取消
# 128 - 共享库错误
####################################################################

### BEGIN INIT INFO
# Provides: checksfs
# Required-Start: udev swap
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:
# Default-Stop:
# Short-Description: 在挂载前检查本地文件系统。
# Description: 在挂载前检查本地文件系统。
# X-LFS-Provided-By: LFS
### END INIT INFO

. /lib/lsb/init-functions

case "${1}" in
start)
  if [ -f /fastboot ]; then
    msg="发现 fastboot，将跳过"
    msg="${msg}按请求的文件系统检查。\n"
    log_info "${msg}"
    exit 0
  fi

  log_info "正在以只读模式挂载文件系统..."
  mount -n -o remount,ro /dev/null

  if [ $? != 0 ]; then
    log_failure_msg2
    msg="${msg}\n无法检查，因为无法挂载"
    msg="${msg}只读模式下的文件系统，n\n"
    msg="${msg}在您按下回键后，此系统将"
    msg="${msg}停止并关机。\n\n"
    log_failure_msg2 "${msg}"

    log_info "按回车继续..."
    wait_for_user
  fi

  if [ -f /forcefsck ]; then
    msg="发现 /forcefsck，强制强制"
    msg="${msg}按请求的文件系统检查。\n"
    log_info "${msg}"
  fi

  log_info "正在检查文件系统..."
  # （注意：提供的 OCR 文本是片段化的；
  # 以下逻辑遵循所提供页面的流程。）
```

# Linux From Scratch - 版本 11.0

```bash
;;
stop)
  # 不要卸载虚拟文件系统如 /run
  log_info_msg "Unmounting all currently mounted file systems..."
  # 确保移除任何回环设备
  elsetup -D
  umount --all --detach-loop --read-only \
      --types notmpfs,nosysfs,nodevmtfs,noproced,nodepvts >/dev/null
  evaluate_retval

  # 确保 / 以只读模式挂载（仅限 bug）
  mount --options remount, / /

  # 在适当的情况下将所有 LVM 卷组设置为不可用
  # 如果 swap 或 / 在 LVM 分区上，此操作将失败
  #if [ -x /sbin/vgchange ]; then /sbin/vgchange -an /dev/null; fi
  ;;

  *)
    echo "Usage: $0 (start|stop)"
    exit 1
    ;;
esac
# End mountfs
```

## D.10.`/etc/rc.d/init.d/udev_retry`

```bash
#!/bin/sh
################################################################
# 开始 udev_retry
# Description : Udev 热插拔脚本（重试）
# Authors     : Alexander E. Patrakov
#              DJ Lucas - dj@linuxfromscratch.org
# Update      : Bruce Dubbs - dbubbs@linuxfromscratch.org
#              Bryan Kadban
# Version      : LFS 7.0
################################################################

### BEGIN INIT INFO
# Provides       : udev_retry
# Required-Start: udev
# Should-Start:  $local_fs cleansfs
# Required-Stop:
# Should-Stop:
# Default-Start:  S
# Default-Stop: 
# Short-Description: 重放失败的 uevents 并创建额外的设备。
# Description    : 重放任何因初始化缓慢而跳过的失败的 uevents，
#                   并创建所需的设备节点
#
# X-LFS-Provided-By: LFS
### END INIT INFO

/lib/lsb/init-functions

case "${1}" in
  start)
    log_info_msg "Retrying failed uevents, if any..."

    # 从 udev-186 开始开始，--run 选项不再有效
    #rundir=$(/sbin/udevadm --run)
    rundir=/run/udev
    # 自于 Debian：“复制在 / 挂载为可读写之前生成的规则”

    for file in ${rundir}/tmp-rules--*; do
      dest=${file##tmp-rules--}
      [ "${dest}" = "" ] && break
      cat "$file" >> /etc/udev/rules.d/$dest
      rm -f "$file"
    done

    # 重新触发可能失败的 uevents，
    # 期望它们现在可以成功
    /bin/sed -e 's/$.//*//' /etc/sysconfig/udev_retry | /bin/grep -v '^$' | \
    while read line; do
      for subsystem in $line; do
        /sbin/udevadm trigger --subsystem-match=$subsystem --action=add
      done
    done

    # 现在等待 udev 处理我们触发的 uevents
    if ! is_true "OMIT_UDEV_RETRY_SETTLE"; then
      /sbin/udevadm settle
    fi

    evaluate_retval
    ;;

  *)
    echo "Usage ${0} {start}"
    exit 1
    ;;
esac
```

## D.11.`/etc/rc.d/init.d/cleansfs`

```bash
#!/bin/sh
#####################################################################
# 开始 cleansfs
#
# Description : 清理文件系统
# Authors : Gerard Beekmans - gerard@linuxfromscratch.org
# Update : Bruce Dubbs - bdbubms@linuxfromscratch.org
# Version : LFS 7.0

################################################### BEGIN INIT INFO
# Provides: cleansfs
# Required-Start: $local_fs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 在启动过程早期清理临时目录。
# Description: 清理临时目录 /run、/var/lock 以及可选的 /tmp。cleansfs 还会创建 /run/utmp 以及在 /etc/sysconfig/createfiles 中定义的文件。
# X-LFS-Provided-By: LFS
### END INIT INFO

. /lib/lsb/init-functions

# 在启动时创建文件/目录的函数
{
  # 输入到文件描述符 9 并输出到标准输入（重定向）
  exec 9</ /etc/sysconfig/createfiles
  while read name type usr grp dtype maj min
  do
    # 忽略注释和空行
    case "${name}" in
      ""|"(\#*") continue; ;;
    esac

    # 忽略已存在的文件
    if [ ! -e "${name}" ]; then
      # 根据类型创建内容。
      case "${type}" in
        dir)
          mkdir "${name}"
          ;;
        file)
          > "${name}"
          ;;
        dev)
          case "${dtype}" in
            char)
              mkfont "${name}" c ${maj}
              ;;
            block)
              mkfont "${name}" b ${maj}
              ;;
          esac
          ;;
        pipe)
          mkfifo "${name}"
          ;;
        *)
          echo "Unknown type: ${type}" >&2
          ;;
      esac
    fi
  done
  exec 9>&-
}
```

```
exit 1
esac
# End console
```

## D.13. `/etc/rc.d/init.d/localnet`

```bash
#!/bin/sh
############################################################
# Begin localnet
#
# Description : 回环设备
# Authors : Gerard Beekemans - gerard@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
#
# Version : LFS 7.0
############################################################
```

```bash
### BEGIN INIT INFO
# Provides: localnet
# Required-Start: mountvirtfs
# Should-Start: modules
# Required-Stop: 
# Should-Stop: 
# Default-Start: S
# Default-Stop: 0
# Short-Description: 启动本地网络。
# Description: 设置机器的主机并启动回环接口。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
- /lib/lsb/init-functions
[ - /etc/sysconfig/network ] && . /etc/sysconfig/network
[ - /etc/hostname ] && HOSTNAME=$(cat /etc/hostname)
```

```bash
case "$1" in
start)
  log_info_msg "正在启动回环接口..."
  ip addr add 127.0.0.1/8 dev lo
  ip link set lo up
  evaluate_retval

  log_info_msg "正在设置主机名为 ${HOSTNAME}..."
  hostname ${HOSTNAME}
  evaluate_retval
  ;;

stop)
  log_info_msg "正在关闭回环接口..."
  ip link set lo down
  evaluate_retval
  ;;

restart)
  ($0) stop
  sleep 1
  ($0) start
  ;;

status)
  echo "Hostname is: $(hostname)"
  ip link show lo
  ;;

*)
  echo "Usage: $(0) {start|stop|restart|status}"
  exit 1
  ;;
esac

exit 0

# End localnet
```

## D.14. `/etc/rc.d/init.d/sysctl`

```bash
#!/bin/sh
############################################################
# Begin sysctl
#
# Description : 使用 /etc/sysctl.conf 设置内核运行时
#              参数
# Authors : Nathan Coulson (nathan@linuxfromscratch.org)
#           Matthew Burgess (matthew@linuxfromscratch.org)
#           DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdbubbs@linuxfromscratch.org
# Version : LFS 7.0
############################################################
```



### BEGIN INIT INFO sysctl
# Provides: mountvirtfs
# Required-Start: console
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 对 proc 文件系统进行更改
# Description: 根据 /etc/sysctl.conf 定义对 proc 文件系统进行更改。参见 'man sysctl(8)'
# X-LFS-Provided-By:
### END INIT INFO

`/lib/lsb/init-functions`

```bash
case "${1}" in
start)
  if [ -f /etc/sysctl.conf ]; then
    log_info_msg "设置内核运行时参数..."
    sysctl -q -p
    evaluate_retval
  fi
  ;;

status)
  sysctl -a
  ;;

*)
  echo "Usage: $0 {start|status}"
  exit 1
  ;;
esac
```

## D.15. /etc/rc.d/init.d/syslogd

```bash
#!/bin/sh
######################################################################
# Begin syslogd
# Description : syslogd 加载器
# Authors      : Gerard Beekmans - gerard@linuxfromscratch.org
#               DJ Lucas - dj@linuxfromscratch.org
# Update      : Bruce Dubbs - bdbubbs@linuxfromscratch.org
# Version      : LFS 7.0
######################################################################
```

```
### BEGIN INIT INFO
# Provides:         $syslog
# Required-Start:   $first localnet
# Should-Start:
# Required-Stop:    $local_fs
# Should-Stop:      sendsignals
# Default-Start:     3 4 5
# Default-Stop:      0 1 2
# Short-Description:  启动内核和系统日志守护进程。
# Description:       启动内核和系统日志守护进程。
#                     /etc/fstab.
# X-LFS-Provided-By:  LFS
### END INIT INFO
```

# 注意：syslogd 不在运行级别 2 中启动，因为可能

# 远程日志配置

`/lib/lsb/init-functions`

```bash
case "${1}" in
start)
  log_info_msg "启动日志守护进程..."
  parms=${SYSLOGD_PARMS:-'-m 0'}
  start_daemon /sbin/syslogd $parms
  evaluate_retval

  log_info_msg "启动内核日志守护进程..."
  start_daemon /sbin/klog
  evaluate_retval
  ;;

stop)
  log_info_msg "停止内核日志守护进程..."
  killproc /sbin/klog
  evaluate_retval

  log_info_msg "停止系统守护进程..."
  killproc /sbin/syslogd
  evaluate_retval
  ;;

reload)
  log_info_msg "重新加载系统守护进程..."
  pid=$(pidof syslogd)
  kill "${pid}"
  evaluate_retval
  ;;

restart)
  ($0) stop
  sleep 1
  ($0) start
  ;;

status)
  statusproc /sbin/syslogd
  statusproc klog
  ;;

*)
  echo "Usage: $0 {start|stop|reload|status}"
  exit 1
  ;;
esac

exit 0

# End syslogd
```

## D.16. /etc/rc.d/init.d/network

```bash
#!/bin/sh

##################################################

# Begin network

# Description : 网络控制脚本

# Authors      : Gerard Beekemans - gerard@linuxfromscratch.org

#               Nathan Coulson - nathan@linuxfromscratch.org

#               Kevin Fleming - fleming@linuxfromscratch.org

#               DJ Lucas - dj@linuxfromscratch.org

# Update      : Bruce Dubbs - bdubbs@linuxfromscratch.org

# Version      : LFS 7.0

##################################################
```

```bash
### BEGIN INIT INFO

# Provides:      $network

# Required-Start:  $local_fs swap

# Should-Start:    $iptables

# Required-Stop:   $local_fs swap

# Should-Stop:     $iptables

# Default-Start:   3 4 5

# Default-Stop:    0 1 2

# Short-Description: 启动并配置网络接口。

# Description:      启动并配置网络接口。

# X-LFS-Provided-By: LFS

### END INIT INFO
```

```bash
case "$1" in

start)

  # 启动所有网络接口

  for file in /etc/sysconfig/ifconfig/*

  do

    interface=${file*/}

    # 如果接口为 * 则跳过

    if [ "$interface" = "*" ]; then continue; fi

    /sbin/ifup "${interface}"

  done

stop)

  # 卸载任何挂载的文件系统

  umount --all --force --types nfs,cifs,nfs

  # 反向列表

  net_files=""

  for file in /etc/sysconfig/ifconfig/*

  do

    net_files="$file $net_files"

  done

  # 停止所有网络接口

  for file in $net_files

  do

    interface=${file*/}

    # 如果接口为 * 则跳过

    if [ "${interface" = "*" ]; then continue; fi

    # 检查接口是否存在

    if [ -e /sys/class/net/"interface" ]; then continue; fi

    # 接口是否为 UP？

    ip link show "$interface" 2>/dev/null | grep -q "state UP"

    if [ $? -ne 0 ]; then continue; fi

    /sbin/ifdown "${interface}"

  done

  ;;

restart)

  ($0) stop

  sleep 1

  ($0) start

  ;;

*)

  echo "Usage: $0 {start|stop|restart}"

  exit 1

  ;;

esac

exit 0

# End network
```

## D.17. /etc/rc.d/init.d/sendsignal

```bash
#!/bin/sh
######################################################
# Begin sendsignal
# Description : sendsignal 脚本
# Authors      : Gerard Beekemans - gerard@linuxfromscratch.org
#               DJ Lucas - dj@linuxfromscratch.org
# Update      : Bruce Dubbs - dbubds@linuxfromscratch.org
# Version      : LFS 7.0
######################################################
```

```
### BEGIN INIT INFO
# Provides:		sendsignal
# Required-Start:   $local_fs swap localnet
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:		0 6
# Default-Stop:
# Short-Description: 尝试杀死剩余进程。
# Description:       尝试杀死剩余进程。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
. /lib/lsb/init-functions

case "$1" in
stop)
  omit=$(pidof mdmon)
  [ -z "$omit" ] && omit=""

  log_info_msg "向所有进程发送 TERM 信号..."
  killall -15 $omit
  error_value=$?

  sleep ${KILDELAY}

  if [ "${error_value}" = 0 -o "${error_value}" = 2 ]; then
    log_success_msg
  else
    log_failure_msg
  fi

  log_info_msg "向所有进程发送 KILL 信号..."
  killall -9 $omit
  error_value=$?
  sleep ${KILDELAY}

  if [ "${error_value}" = 0 -o "${error_value}" = 2 ]; then
    log_success_msg
  else
    log_failure_msg
  fi
  ;;

*)
  echo "Usage: $0"
  exit 1
  ;;
esac

exit 0
```

## D.18. /etc/rc.d/init.d/reboot

```bash
#!/bin/sh

##################################################

# Begin reboot

# Description : 重启脚本

#

# Authors : Gerard Beekemans - gerard@linuxfromscratch.org

```
```bash
# DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - bdbubs@linuxfromscratch.org
# 版本 : LFS 7.0
######################################################################
```
```bash
### BEGIN INIT INFO
# Provides: reboot
# Required-Start:
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: 6
# Default-Stop:
# Short-Description: 重启系统。
# Description: 重启系统。
# X-LFS-Provided-By: LFS
### END INIT INFO
```
```bash
/usr/lib/init-functions
case "${1}" in
stop)
  log_info_msg "正在重启系统..."
  reboot -d f -i
  ;;
*)
  echo "用法: $0 {stop}"
  exit 1
  ;;
esac
# End reboot
```

## D.19. /etc/rc.d/init.d/halt

```bash
#!/bin/sh
######################################################################
# Begin halt
# Description : 停机脚本
# Authors : Gerard Beemans - gerard@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - bdbubs@linuxfromscratch.org
# 版本 : LFS 7.0
######################################################################
```
```bash
### BEGIN INIT INFO
# Provides: halt
# Required-Start:
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:
# Default-Stop:
# Short-Description:
# Description:
# X-LFS-Provided-By:
### END INIT INFO
```
```bash
case "${1}" in
    halt -d -f -i -p
        ;;
    *)
        echo "用法: {stop}"
        exit 1
        ;;
esac
```
停止系统。
停止系统。

# End halt

## D.20. /etc/rc.d/init.d/template

```bash
#!/bin/sh
################################################################
# Begin scriptname
# Description :
#
# Authors :
#
# Version : LFS x.x
#
# Notes :
#
################################################################
### BEGIN INIT INFO
# Provides         template
# Required-Start:
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:
# Default-Stop:
# Short-Description:
# Description:
# X-LFS-Provided-By:
### END INIT INFO
. /var/lib/lsb/init-functions
```
```bash
case "${1}" in
    start)
        log_info_msg "正在启动..."
        start_daemon fully_qualified_path
        ;;
    stop)
        log_info_msg "正在停止..."
        killproc fully_qualified_path
        ;;
    restart)
        $0 stop
        sleep 1
        $0 start
        ;;
    *)
        echo "用法: $0 {start|stop|restart}"
        exit 1
        esac
;;
exit 0
# End scriptname
```



## D.21. `/etc/sysconfig/modules`

```
####################################################################
# Begin /etc/sysconfig/modules
# Description : 模块自动加载配置
# Authors :
# Version : 00.00
# Notes : 此文件的语法如下：
# <module> [<arg1> <arg2> ...]

# 每个模块应该独占一行，任何想要传递给模块的选项
# 都应该紧随其后。行分隔符可以是空格或制表符。
####################################################
# End /etc/sysconfig/modules
```

## D.22. `/etc/sysconfig/createfiles`

```
####################################################

# Begin /etc/sysconfig/createfiles

# Description : Createfiles 配置

# Authors :

# Version : 00.00

# Notes : 此文件的语法如下：

# 如果 type 等于 "file" 或 "dir"

# <filename> <type> <permissions> <user> <group>

# 如果 type 等于 "dev"

# <filename> <permissions> <user> <devtype> <major> <minor>

# <filename> 是创建的文件名

# <type> 为 file, dir 或 dev 之一

# file 创建新文件

# dir 创建一个目录

# dev 创建一个设备

# block 创建一个块设备

# char 创建一个字符设备

# pipe 创建一个管道，这将忽略 <major> 和 <minor> 字段

# <major> 和 <minor> 不用于设备。
```

## D.23. `/etc/sysconfig/udev`

```
####################################################

# Begin /etc/sysconfig/udev

# Description : udev 脚本配置

# Authors :

# Version : 00.00

# Notes : 挂载后可能需要触发的每个子系统

# 都应该列在此文件中。可能的子系统列在此处，

# 是于 /var/lib/hwclock/adjtime 和 sound（由于两者 /var/lib/alsa/asound.state）

# 条目之间用空格分隔。

####################################

# End /etc/sysconfig/udev
```

## D.24. `/sbin/ifup`

```bash
#!/bin/sh

################################################################

# (此处文本不完整，未翻译后续内容)

# Linux From Scratch - Version 11.0
```
```bash
if [ $ -gt 0 ]; do
  case "$1" in
    --help | -h)
      help="y"; break ;;

    --version | -V)
      echo "${VERSTR}"; exit 0 ;;

    -*)
      echo "${1}: invalid option" >&2
      echo "${USAGE}" >&2
      exit 2 ;;

    break ;;
  esac
fi

if [ -n "$help" ]; then
echo "${VERSTR}"
echo "${USAGE}"
echo

cat << HERE_EOF
down 命令用于关闭网络接口。接口参数（例如 eth0 或 eth0:2）必须匹配接口规范文件的末尾部分，例如 /etc/sysconfig/ifconfig.eth0:2。

HERE_EOF
exit 0

file=/etc/sysconfig/ifconfig.$1

```
```bash
# 跳过备份文件
[ "$file" = "${file%~}" ] || exit 0
/lib/lsb/init-functions
```
```bash
if [ -r "$file" ]; then
log_warning_msg "$file" 缺失或无法访问。
exit 1
fi

$file
```
```bash
if [ "$INTERFACE" = "" ]; then
log_failure_msg "$file" 未定义接口 [IFACE]。
exit 1
fi

# 我们只需要第一个服务来关闭接口
S=$(echo "${SERVICE}" | cut -f1 -d " ")
```
```bash
exit 1

fi

else

  log_warning_msg "接口 ${1} 不存在。"

fi

```
```bash
# 如果设备中还有其他额外的接口，则保留该接口

link_status=$(ip link show ${IFACE} 2>/dev/null)

if [ -n "${link_status}" ]; then

  if [ "$(echo "${link_status}" | grep UP)" != "" ]; then

    if [ "$(ip addr show ${IFACE}" | grep 'inet ') ="" ]; then

      log_info_msg "正在关闭 ${IFACE} 接口..."

      ip link set ${IFACE} down

    fi

  fi

fi

evaluate_retval

fi

```
```bash
# 结束 /sbin/ifdown
```

## D.26. `/lib/services/ipv4-static`

```bash
#!/bin/sh

################################################################################

# 开始 /lib/services/ipv4-static

################################################################################

# ：IPv4 静态启动脚本

#

# 作者：Nathan Colson - nathan@linuxfromscratch.org

           Kevin P. Fleming - kpfleming@linuxfromscratch.org

           Bruce Dubbs - bdubbs@linuxfromscratch.org
# 更新： 
# 版本  : LFS 7.0
################################################################################
```
```bash
/lib/sb/init-functions

. ${IFCONFIG}

if [ -z "${IFACE}" ]; then

  log_failure_msg "\n${IFCONFIG} 中缺少 IP 变量，无法继续。"

  exit 1

fi
```
```bash
if [ -z "${PREFIX}" -a -z "${PEER}" ]; then

  log_warning_msg "\n${IFCONFIG} 中缺少 PREFIX 变量，假设为 24。"

  PREFIX=24

  args="${args} ${IP}/${PREFIX}"
```
```bash
elif [ -n "${PREFIX}" -a -n "${PEER}" ]; then

  log_failure_msg "\n${IFCONFIG} 中同时指定了 PREFIX 和 PEER，无法继续。"

  exit 1
```
```bash
elif [ -n "${PREFIX}" ]; then

  args="${args} ${IP}/${PREFIX}"
```
```bash
elif [ -n "${PEER}" ]; then

args="${args} peer ${PEER}"
fi

if [ -n "${LABEL}" ]; then

args="${args} label ${LABEL}"
fi

if [ -n "${BROCAST}" ]; then

args="${args} broadcast ${BROCAST}"
fi

case "${2}" in

up)

  if [ $(ip addr show ${1} 2>/dev/null | grep ${$IP}/) = "" ]; then

    log_info_msg "正在向 ${1} 接口添加 IPv4 地址 ${$IP}..."

    ip addr add ${$IP} dev ${1}

    evaluate_retval

  else

    log_warning "无法向 ${1} 添加 IPv4 地址 ${$IP}。已存在。"

  fi

down)

  if [ $(ip addr show ${1} 2>/dev/null | grep ${$IP}/) != "" ]; then

    log_info_msg "正在从 ${1} 接口移除 IPv4 地址..."

    ip addr del ${$IP} dev ${1}

    evaluate_retval

  fi

  if [ -n "${GATEWAY}" ]; then

    # 只有在没有剩余 ipv4 地址时才移除网关

    if [ $(ip addr show ${1} 2>/dev/null | grep 'inet') != "" ]; then

      log_info_msg "正在移除默认网关..."

      ip route del default

      evaluate_retval

    fi

  fi

*)

  echo "用法: ${0} [interface] (up|down)"

  exit 1

esac
```

## D.27. `/lib/services/ipv4-static-route`

```bash
#!/bin/sh

################################################################################

# 开始 /lib/services/ipv4-static-route

################################################################################

# ：IPv4 静态路由脚本
# 描述：IPv4 静态路由脚本
# 作者：Kevin P. Fleming - kpfleming@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# 更新：Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本：LFS 7.0
################################################################################
```
```bash
/lib/lsb/init-functions

. ${IFCONFIG}

case "${TYPE}" in

  ("network")

    need_ip=1

    need_gateway=1

  ;;

  ("default")

    need_gateway=1

    args="${args} default"

    desc="default"

  ;;

  ("host")

    need_ip=1

  ;;

  ("unreachable")

    need_ip=1

    args="${args} unreachable"

    desc="unreachable"

  ;;

  (*)

    log_failure_msg "${IFCONFIG} 中未知路由类型 ${TYPE}无法继续。"

    exit 1

esac

if [ -n "${GATEWAY}" ]; then

  MSG="静态路由无法在 ${IFCONFIG} 中设置 GATEWAY 变量。"

  log_failure_msg "${MSG} 使用 STATIC_GATEWAY，无法继续"

  exit 1

fi

if [ -n "${need_ip}" ]; then

  if [ -z "${IP}" ]; then

    log_failure_msg "${IFCONFIG} 中缺少 IP 变量，无法继续。"

    exit 1

  fi

fi

if [ -z "${PREFIX}" ]; then

  log_failure_msg "${IFCONFIG} 中缺少 PREFIX 变量，无法继续。"

  exit 1

fi

args="${args}(${PREFIX}"

desc="${desc}/${PREFIX}"

if [ -n "${need_gateway}" ]; then

  if [ -z "${STATIC_GATEWAY}" ]; then

    log_failure_msg "${IFCONFIG} 中缺少 STATIC_GATEWAY 变量，无法继续。"

    exit 1

  fi

  args="${args} via ${STATIC_GATEWAY}"

fi

if [ -n "${SOURCE}" ]; then

  args="${args} src ${SOURCE}"

fi

case "$2" in

  up)

    log_info_msg "正在向 ${1} 接口添加 '${desc}' 路由..."

    ip route add ${args} dev ${1}

    evaluate_retval

  ;;

  down)

    log_info_msg "正在从 ${1} 接口移除 '${desc}' 路由..."

    ip route del ${args} dev ${1}

    evaluate_retval

  ;;

  *)

    echo "用法: ${0} [interface] {up|down}"

    exit 1

esac

# 结束 /lib/services/ipv4-static-route
```

## 附录 E. Udev 配置规则

附录中的规则是为了方便列出。安装通常通过第 8.6 节完成。

## E.1. 55-lfs.rules

```bash
# /etc/udev/rules.d/55-lfs.rules: LFS 规则定义

# 内核设备

# 这使得 /dev/rtc 可用时立即设置系统时钟
SUBSYSTEM="rtc", ACTION="add", MODE="0644", RUN+="/etc/rc.d/init.d/setclock"
KERNEL="rtc", ACTION="add", MODE="0644", RUN+="/etc/rc.d/init.d/setclock"

# 通信设备

KERNEL="ippp[0-9]*", GROUP="dialout"
KERNEL="isdn[0-9]*", GROUP="dialout"
KERNEL="isdnctrl[0-9]*", GROUP="dialout"
KERNEL="dcbri[0-9]*", GROUP="dialout"
```

## 附录 F. LFS 许可证

本书根据知识共享 署名-非商业-相同性 2.0 许可证许可。

计算机指令可以根据 MIT 许可证从书中提取。

## F.1. 知识共享法律代码

知识共享 署名-非商业-相同性 2.0

> **重要信息**
> 知识共享公司不是律师事务所，不提供法律服务。本许可证的分发不构成律师与客户关系。知识共享按“原样”提供此类信息。知识共享对所提供的信息不作任何保证，并对其在使用可能造成的损害不承担责任。

许可证

本作品（下所示）根据知识共享通用许可证（“CCPL”或“许可证”）的条款提供。

作品受版权和/其他适用法律保护。除本许可证或版权法允许外，对作品的任何使用都是禁止的。

通过行使此处提供的作品的任何权利，您即接受并同意受本许可证条款的约束。许可方考虑到您接受此类条款和条件，特授予您此处包含的权利。

+ 1. 定义

a. “集体作品”是指一种作品，例如期刊杂志、选集或百科全书，其中作品的完整且未经修改的形式，连同若干其他本身构成独立作品的贡献，被汇成一个整体。构成集体作品的作品在在本许可证的目的下不被视为衍生作品（见下文定义）。

b. “衍生作品”是指基于作品或作品与其他现有作品而创作的作品，例如翻译、音乐改编、戏剧化、虚构化、电影版本、声音录制品，作为复制、节选、浓缩或作品可能重构、转换或改编的任何其他形式，构成集体作品的作品在本许可证的目的下不被视为衍生作品。为避免疑问，当作品为音乐作品或声音录制品时，作品与移动图像的时间关系同步（“同步”）在本许可证的目的下被视为衍生作品。

c. “许可方”是指根据本许可证条款提供作品的个人或实体。

d. “原作者”是指创作作品的个人或实体。



e. “作品”是指根据本许可证条款提供的受版权保护的作品。

f. “您”是指行使作品权利的个人或实体，该实体此前未就作品违反过本许可证条款，或者尽管此前违规，但已获得许可方的明确许可根据本许可证行使权利。

g. “许可元素”指的是许可者选择并在本权利标题中指出的以下高级许可属性：署名、非商业性、相同方式。

## 2. 公平使用
本许可中的任何内容均不旨在减少、限制或约束根据版权法或其他适用法律，因自由使用、首次销售或其他对版权所有者专有权利的限制限制而产生的任何权利。

## 3. 许可授予
在遵守本许可条款和条件的前提下，许可者授予您一个全球性的、免版费的、非独的、永久的（在适用版权有效期内）许可，以按下述行使作品中的权利：

- a. 复制作品，将作品并入一个或多个集体作品中，并复制作品
- b. 创建并复制衍生作品；
- c. 分发作品的副本或录音制品、公开展示、公开表演，以及通过数字音频传输公开表演作品（包括并入集体作品中的部分）；
- d. 分发衍生作品的副本或录音制品、公开展示、公开表演，以及通过数字音频传输公开表演衍生作品；

上述权利可以在现在或以后开发的任何媒体和格式中行使。上述权利包括在其他媒体和格式中行使权利所需的、上必要的此类修改的权利。许可者未明确授予的所有权利均予以保留，但不限于第 4(e) 节和 4(f) 节中规定的权利限制。

## 4. 限制
第 3 节授予的许可明确受以下限制并受其约束：

- a. 您仅可以在本许可的条款下分发、公开展示、公开表演或数字表演作品，且您必须在分发、公开展示、公开表演或数字表演作品的每份副本或录音制品中，包含本许可的副本或本许可的统一资源标识符（URI）。您不能对作品提供或施加任何更改或限制本许可条款或接收者行使本许可下授予权利的条款。您可以保留所有引用本许可及免责声明的通知。您不能使用任何与本许可协议不符的控制作品访问或使用的技术措施来分发、公开展示、公开表演或数字表演作品。上述规定适用于并入集体作品中的作品，但并不要求作品本身之外的集体作品必须遵守本许可的条款。如果您创建了集体作品，在收到任何许可者的通知后，请根据要求从作品中删除任何对许可者或原作者的引用。如果您创建了衍生作品，在收到任何许可者的通知后，您必须在可行范围内从作品中删除任何对许可者或您的引用。
- b. 您仅可以在本许可条款、具有与本许可相同许可元素的本许可后续版本、或包含与本许可相同许可元素的 Commons 许可（例如：署名-非商业性-相同方式 2.0）条款下，分发、公开展示、公开表演或数字表演衍生作品。您在分发、公开展示、公开表演或数字表演每份衍生作品的副本或录音制品中，必须包含本许可或前版本中指定的其他许可的副本或其 URI。您不能对衍生作品提供或施加任何更改或限制本许可条款或接收者行使本许可下授予权利的条款。您可以保留所有引用本许可及免责声明的通知。您不能使用任何与本许可协议条款不符的控制作品访问或使用的技术措施来分发、公开展示、公开表演或数字表演衍生作品。上述规定适用于并入集体作品中的衍生作品，但并不要求衍生作品本身之外的集体作品必须遵守本许可的条款。
- c. 您不得以任何主要旨在获取直接商业利益或私人货币补偿的方式行使上述第 3 节授予您的任何权利。通过数字文件共享或其他方式用作品与其他版权作品交换，不应被视为旨在或指向直接商业利益或私人货币补偿，前提是交换版权作品交换过程中没有支付任何货币补偿。
- d. 如果您分发、公开展示、公开表演或公开表演作品以及任何衍生作品或集体作品，您必须保留作品的所有版权声明，并根据您所使用的媒体或手段向原作者提供合理的说明，方式包括提供您的姓名（或笔名）作为原作者（如已出版）；所使用的作品标题；在合理可行范围内，提供许可者指定的与作品关联的 URI（如有），除非该 URI 不指向作品的版权声明或许可信息；以及在衍生作品的情况下，提供一份说明在衍生作品中使用该作品的说明（例如“原作者作品的法文译本”或“基于原作者创作的剧本”）。此类说明可以以任何合理方式实施；但是，在衍生作品或集体作品的情况下，此类说明至少应出现在任何其他作者署名出现的地方，且其方式至少应与其他类似的作者署名一样显著。
- e. 为免疑问，当作品为音乐作品时：
    - i. 概括许可下的版税。许可者保留单独地（或通过权利协会，例如 ASCAP、BMI、SESAC）收取作品公开表演或公开数字表演（如网络广播）版税的专有权利，如果该表演主要指向商业利益或私人货币补偿。
    - ii. 机械权利和法定版税。许可者保留单独地（或通过音乐权利机构或指定代理，例如 Harry Fox Agency）收取来自作品的任何录音制品（“翻唱版”）版税并进行分发的专有权利，但受美国版权法第 17 卷第 115 节强制许可（或其他司法管辖区的等同规定）的限制，如果您对此类翻唱版的分发主要指向商业利益或私人货币补偿。网络广播录制。许可者保留单独地（或通过表演权利协会，例如 SoundExchange）收取作品公开数字表演（如网络广播）版税的专有权利，但受美国版权法第 17 卷第 114 节（或其他司法管辖区的等同规定）强制许可的，如果您的公开数字表演主要指向商业利益或私人补偿。
- f. 网络广播权利和法定版税。为免疑问，当作品为录音制品时，许可者保留单独地（或通过表演权利协会，例如 SoundExchange）收取作品公开数字表演（如网络广播）版税的专有权利，但受美国版权法第 17 卷第 114 节（或其他司法管辖区的等同规定）强制许可的，如果您的公开数字表演主要指向商业利益或私人补偿。

## 5. 陈述、保证与免责声明
除非双方另有书面约定，许可者按原样提供作品，并不对作品作出任何形式的（无论是明示的、法定的或其他形式）陈述或保证，包括但不限于对所有权、可销性、特定用途的适用性、不侵权或不存在缺陷的保证。

## 6. 责任限制
在法律要求的范围内，在任何情况下，许可者均不根据任何法律理论对因本许可或使用作品而产生的任何特殊、间接、后果性、惩罚性或示例性损害承担您的责任，即使许可者已被告知发生此类损害的可能性。

## 7. 终止
a. 本许可及下述授予的权利将在您违反本许可的任何条款时自动终止。根据本许可获得衍生作品或集体作品的个人或实体，只要此类实体保持完全合规，其许可将不会终止。
b. 在上述条款和条件的基础上，此处授予的许可是永久的（在适用版权有效期内）。尽管有如此，许可者保留根据不同的许可条款发布作品或随时停止作品的权利；但是，任何此类选择都不会撤回本许可（或根据本许可条款已授予或必须授予的任何其他许可），除非许可如上述已终止。

## 8. 其他
a. 每当您分发或公开表演作品或集体作品时，许可者向接收者提供与授予您的许可相同的条款和条件的作品许可。
b. 每当您分发或公开表演衍生作品时，许可者向接收者提供与授予您的许可相同的条款和条件的原始作品许可许可。
c. 如果本许可的任何条款在适用法律下无效或不可执行，则不影响本许可其余条款的有效性或可执行性，且在协议双方无需进一步采取的情况下，该条款应被修订至所需的最低限度以使其有效且可执行。
d. 本许可的任何条款或规定均不被视为放弃，且对此类放弃或同意的确认必须以书面形式并由责任方签字方有效。
e. 本许可构成了双方就此处许可的作品达成的完整协议。对于此处未说明的作品，不存在其他理解、协议或陈述。许可者不受您的信来中可能出现的任何附加条款的约束。未经许可者和您的共同同意，本许可不可修改。

从零开始 Linux - 版本 11.0

# 重要说明

知识共享（Creative Commons）并非本许可的方，且不对本作品提供任何形式的保证。无论何种法律理论，知识共享不对您或任何方的任何损害均承担责任，包括但不限于与本许可相关的任何一般、特殊、偶然或间接损害。尽管有上述两（2）句的规定，如果知识共享已明确标识其为许可方，则此处将拥有许可方的所有权利和义务。

除了向公众表明该作品根据 CCPL 许可的有限目的外，任何其他方在未经知识共享事先同意的情况下不得使用“Creative Commons”商标或其相关的任何商标或标志。任何允许的使用都应遵守知识共享当时有效的使用指南，这些指南可能在其网站上发布，或根据要求随时提供。

可以通过 `http://creativecommons.org` 联系知识共享。

# F.2 MIT 许可证

版权所有 © 1999-2021 Gerard Beekmans

特此授权

上述版权声明和本许可声明应包含在软件的所有副本或主要部分。

软件按“原样”提供，不带有任何形式的明示或暗示保证，包括但不限于对商品性、特定用途的适用性以及不侵权的保证。在任何情况下，作者或版权所有者均不对因软件或使用软件或其他处理软件而引起的、无论是基于合同、侵权或其他诉的任何索赔、损害或其他责任承担责任。

# 目录

# 软件包

- `Acl`: 130
- `Attr`: 131
- `Autoconf`: 166
- `Automake`: 168
- `Bsh`: 152
- `tools`: 58
- `Bash`: 152
- `Bc`: 117
- `Binutils`: 123
- `tools, pass 1`: 44
- `tools, pass 2`: 71
- `Bison`: 150
- `tools`: 83
- `Bootscripts`: 230
- `usage`: 240
- `Bzip2`: 108
- `Check`: 185
- `Coreutils`: 180
- `tools`: 59
- `DejaVu`: 122
- `Diffutils`: 186
- `tools`: 60
- `E2fprogs`: 220
- `Eudev`: 208
- `configuring`: 208
- `Expat`: 157
- `Expect`: 121
- `File`: 113
- `tools`: 61
- `Findutils`: 188
- `tools`: 62
- `Flex`: 118
- `Gawk`: 187
- `tools`: 63
- `GCC`: 137
- `tools, libstdc++ pass 1`: 53
- `tools, libstdc++ pass 2`: 80
- `tools, pass 1`: 46
- `tools, pass 2`: 72
- `GDBM`: 155
- `Gettext`: 148
- `tools`: 82
- `Glibc`: 99
- `tools`: 50
- `GMP`: 126
- `Gperfl`: 156
- `Grep`: 151
- `tools`: 64
- `Groff`: 189
- `GRUB`: 192
- `Gzip`: 194
- `tools`: 65
- `Iana-Etc`: 98
- `Intutils`: 158
- `Inttool`: 162
- `IPRoute`: 195
- `Kbd`: 197
- `Kmod`: 169
- `Less`: 160
- `Libcap`: 132
- `Libelf`: 171
- `Libffi`: 172
- `Libpipeline`: 199
- `Libtool`: 154
- `Linux`: 257
- `tools, API headers`: 49
- `M4`: 116
- `tools`: 55
- `MPFR`: 128
- `N--curses`: 143
- `Make`: 200
- `tools`: 66
- `Man-DB`: 210
- `Man-pages`: 97
- `Meson`: 179
- `MPC`: 129
- `Ninja`: 177
- `OpenSSL`: 173
- `Patch`: 201
- `tools`: 67
- `Pconfig`: 142
- `Prop-ng`: 213
- `Psmisc`: 147
- `Python`: 175
- `Readline`: 114
- `Sed`: 146
- `tools`: 68
- `Shadow`: 133
- `tools`: 134
- `Syslogd`: 223
- `Sysinit`: 225
- `Tar`: 202
- `tools`: 69
- `Tcl`: 119
- `Texinfo`: 203
- `tools`: 86
- `Udev usage`: 232
- `Util-linux`: 215
- `tools`: 87
- `Vim`: 205
- `XML::Parser`: 164
- `Xz`: 110
- `tools`: 70
- `Zlib`: 107
- `zstd`: 112
- `blkid`: 215
- `blkzone`: 215
- `blockdev`: 215
- `bootlogd`: 225
- `bridge`: 195
- `bunzip2`: 108
- `bzcat`: 108
- `bzcmp`: 108
- `bzdiff`: 108
- `bzgrep`: 108
- `bzgrep`: 108
- `bzip2`: 108
- `bzip2recover`: 108
- `bzless`: 108
- `bzore`: 108
- `c++`: 137
- `c++filt`: 123
- `cal`: 215
- `capsaps`: 132
- `captoinfo`: 143
- `cat`: 180
- `catchseg`: 99
- `catman`: 210
- `cc`: 137
- `cfdisk`: 215
- `acl`: 131
- `chage`: 133
- `chattr`: 220
- `chcon`: 180
- `chepu`: 215
- `checkmk`: 185
- `chem`: 189
- `chfnn`: 133
- `chgpasswd`: 133
- `chgrp`: 180
- `chhemm`: 215
- `chmod`: 180
- `choom`: 215
- `chown`: 180
- `chpasswd`: 133
- `chroot`: 180
- `chrt`: 215
- `chsh`: 133
- `chvt`: 197
- `cksum`: 180
- `clear`: 143

# 程序

- `accessdb`: 210
- `aclocal`: 168
- `aclocal-1.16`: 168
- `addinfo`: 189
- `addpart`: 215
- `addline`: 123
- `agetty`: 215
- `as`: 123
- `attr`: 130
- `autoconf`: 166
- `autader`: 166
- `automake`: 168
- `automake-1`: 166
- `autopoint`: 148
- `autoscan`: 166
- `autoupdate`: 166
- `awk`: 187
- `bsum`: 180
- `badlocks`: 220
- `base`: 180
- `base64`: 180
- `basename`: 180
- `bash`: 152
- `bashbug`: 152
- `bc`: 117
- `bison`: 150
- `bldiscard`: 215
- `cmp`: 186
- `col`: 215
- `colcrt`: 215
- `colrm`: 215
- `column`: 215
- `comm`: 180
- `compile`: 220
- `cp`: 180
- `cpan`: 161
- `cpp`: 137
- `csplit`: 180
- `ctrlld`: 215
- `ctstat`: 195
- `cut`: 180
- `date`: 180
- `dc`: 117
- `dd`: 180
- `deallocovt`: 197
- `debugfs`: 220
- `delpart`: 215
- `depmod`: 169
- `diff`: 180
- `diff3`: 186
- `dir`: 180
- `dircolors`: 180
- `dirmame`: 180
- `dmesg`: 215
- `dnsdomainname`: 158
- `du`: 180
- `dumperfs`: 220
- `dumpkeys`: 197
- `e2freefrag`: 220
- `e2fck`: 220
- `e2image`: 220
- `e2label`: 220
- `e2mmstatus`: 220
- `e2scrub`: 220
- `e2scrub_all`: 220
- `e2undo`: 220
- `e4crypt`: 220
- `e4defrag`: 220
- `echo`: 180
- `eegrep`: 151
- `eject`: 215
- `elfedit`: 123
- `enc2xs`: 161
- `encguss`: 161
- `env`: 180
- `envsubst`: 148
- `eqqn`: 189
- `eqqn2graph`: 189
- `ex`: 205
- `expand`: 180
- `xpect`: 121
- `expiry`: 133
- `expr`: 180
- `factor`: 180
- `faillog`: 133
- `fallocate`: 215
- `false`: 180
- `dfformat`: 215
- `fdisk`: 215
- `fgconsole`: 197
- `fgrep`: 151
- `file`: 113
- `filefrag`: 220
- `find`: 188
- `finds`: 215
- `fmnt`: 215
- `flex`: 118
- `flex++`: 118
- `flock`: 215
- `fmt`: 180
- `fold`: 180
- `free`: 213
- `fsck`: 215
- `fsckram`: 215
- `fsck2`: 220
- `fskext`: 220
- `fskst`: 220
- `fskmin`: 220
- `fskmix`: 215
- `fsfreeze`: 215
- `stab`: 225
- `flip`: 158
- `fuser`: 147
- `g++`: 137
- `gawk`: 187
- `gawk-5.1`: 187
- `gcc`: 137
- `gc-ar`: 137
- `gc-nm`: 137
- `gc-ranlib`: 137
- `cov`: 137
- `ggov-dump`: 137
- `ggov-tool`: 137
- `gdbm`: 155
- `gdbm_dump`: 155
- `gdbm_load`: 155
- `gdbmk`: 155
- `gencat`: 99
- `genl`: 195
- `getcap`: 132
- `getconf`: 99
- `getent`: 99
- `getfacl`: 131



# Linux 从头开始 - 版本 11.0

- `getftarr`: 130
- `getkeys`: 197
- `getopt`: 215
- `getcaps`: 132
- `gettext`: 148
- `getext.sh`: 148
- `getextize`: 148
- `glypintw`: 189
- `gpasswd`: 133
- `gperf`: 156
- `gperfl`: 156
- `ginyin`: 189
- `gprof`: 123
- `grap2graph`: 189
- `grep`: 151
- `grn`: 189
- `grodvi`: 189
- `groff`: 189
- `groffer`: 189
- `grog`: 189
- `golbp`: 189
- `grolj4`: 189
- `gropdf`: 189
- `grops`: 189
- `grotty`: 189
- `groupadd`: 133
- `groupel`: 133
- `groupmems`: 133
- `groupmod`: 133
- `groups`: 180
- `gprck`: 133
- `gngpconv`: 133
- `gprunconv`: 133
- `ggrub-bios-setup`: 192
- `ggrub-editenv`: 192
- `ggrub-file`: 192
- `ggrub-fstest`: 192
- `ggrub-glue-efi`: 192
- `ggrub-install`: 192
- `ggrub-kbdcomp`: 192
- `ggrub-macless`: 192
- `ggrub-menlust2cfg`: 192
- `ggrub-mkconfig`: 192
- `ggrub-mkimage`: 192
- `ggrub-mklayout`: 192
- `ggrub-mknetdir`: 192
- `ggrub-mkpasswd-pkbddf`: 192
- `ggrub-mkrelpleth`: 192
- `ggrub-mkres`: 192
- `ggrub-mkstandalone`: 192
- `ggrub-ofpathname`: 192
- `ggrub-probe`: 192
- `ggrub-reboot`: 192
- `ggrub-render-label`: 192
- `ggrub-script-check`: 192
- `ggrub-set-default`: 192
- `ggrub-setup`: 192
- `ggrub-syslinux2cfg`: 192

| `ifstat`: 195, 195 |
| `ndxbxb`: 189, 190 |
| `info`: 203, 204 |
| `infocmp`: 143, 144 |
| `infotocap`: 143, 144 |
| `init`: 225, 225 |
| `sismod`: 169, 169 |
| `install`: 180, 182 |
| `install-info`: 203, 204 |
| `stmodsh`: 161, 162 |
| `intlool-extract`: 165, 165 |
| `intool-merge`: 165, 165 |
| `intool-update`: 165, 165 |
| `intoolize`: 165, 165 |
| `ionice`: 215, 217 |
| `ip`: 195, 196 |
| `ipcmk`: 215, 217 |
| `iperm`: 215, 217 |
| `ipcs`: 215, 217 |
| `isosizize`: 215, 217 |
| `join`: 180, 182 |
| `json_pp`: 161, 162 |
| `bdinfo`: 197, 198 |
| `kbdrate`: 197, 198 |
| `kbd_mode`: 197, 198 |
| `kill`: 215, 217 |
| `killall`: 147, 147 |
| `kill5`: 225, 225 |
| `klod`: 223, 223 |
| `kmod`: 169, 169 |
| `last`: 215, 217 |
| `astb`: 215, 217 |
| `dlastlog`: 133, 135 |
| `dl`: 123, 125 |
| `dld.bf`: 123, 125 |
| `dld.gold`: 123, 125 |
| `dlatch`: 215, 217 |
| `dconfig`: 99, 105 |
| `dd`: 99, 105 |
| `dibc4`: 99, 105 |
| `less`: 160, 160 |
| `lesseho`: 160, 160 |
| `lex`: 118, 118 |
| `lexgrog`: 210, 212 |
| `lfskernel-5.13.12`: 257, 260 |
| `libasan`: 137, 141 |
| `libatomic`: 137, 141 |
| `libcc1`: 137, 141 |
| `libnetcfg`: 162, 162 |
| `libtool`: 154, 154 |
| `libtoolize`: 154, 154 |
| `link`: 180, 182 |
| `linux32`: 215, 217 |
| `linux64`: 215, 218 |
| `lkbib`: 189, 190 |
| `In`: 180, 182 |
| `Inst`: 195, 196 |
| `loadkeys`: 197, 198 |
| `loadunimap`: 197, 198 |
| `locale`: 99, 105 |
| `localedef`: 99, 105 |
| `locate`: 188, 188 |
| `logger`: 215, 218 |
| `login`: 133, 135 |
| `logname`: 180, 182 |
| `logoutd`: 133, 135 |
| `logsave`: 220, 221 |
| `look`: 215, 218 |
| `lookbib`: 189, 190 |
| `losetup`: 215, 218 |
| `lIs`: 180, 182 |
| `lsattr`: 220, 221 |
| `lblk`: 215, 218 |
| `lscpu`: 215, 218 |
| `lispc`: 215, 218 |
| `lslocks`: 215, 218 |
| `lslogs`: 215, 218 |
| `lsmem`: 215, 218 |
| `lsimod`: 169, 170 |
| `lsns`: 215, 218 |
| `dzcat`: 110, 110 |
| `dzcmmp`: 110, 110 |
| `dziff`: 110, 110 |
| `dzegrep`: 110, 110 |
| `lzgrep`: 110, 110 |
| `lzgrep`: 110, 110 |
| `lzless`: 110, 110 |
| `lzma`: 110, 110 |
| `lzmadec`: 110, 111 |
| `lzminfo`: 110, 111 |
| `lzmore`: 110, 111 |
| `m44`: 116, 116 |

| `make`: 200, 200 |
| `makedb`: 99, 105 |
| `makeinfo`: 203, 204 |
| `man`: 210, 212 |
| `mandb`: 210, 212 |
| `manpath`: 210, 212 |
| `mapscr`: 197, 198 |
| `cookie`: 215, 218 |
| `md5sum`: 180, 182 |
| `mesg`: 215, 218 |
| `meson`: 179, 179 |
| `mkdir`: 180, 183 |
| `mk2fs`: 220, 222 |
| `mkffio`: 180, 183 |
| `mkffs`: 215, 218 |
| `mkfs.ramfs`: 215, 218 |
| `mkfs.ext2`: 220, 222 |
| `mkfs.ext3`: 220, 222 |
| `mkfs.minix`: 215, 218 |
| `mlostfound`: 220, 222 |
| `mklod`: 180, 183 |
| `mkswap`: 215, 218 |
| `mktemp`: 180, 212 |
| `mk_cmds`: 220, 222 |
| `mroff`: 189, 190 |
| `modinfo`: 169, 170 |
| `modprobe`: 169, 170 |
| `more`: 215, 218 |
| `mount`: 215, 218 |
| `mountpoint`: 215, 218 |
| `msgatt`: 148, 148 |
| `msgcat`: 148, 149 |
| `msgcmp`: 148, 149 |
| `msgcomm`: 148, 149 |
| `msgconv`: 148, 149 |
| `msgggen`: 148, 149 |
| `msggeec`: 148, 149 |
| `msgfilter`: 148, 149 |
| `msgfnt`: 148, 149 |
| `msgrep`: 148, 149 |
| `msgnit`: 148, 149 |
| `msnerge`: 148, 149 |
| `msgunft`: 148, 149 |
| `msgunqi`: 148, 149 |
| `trace`: 99, 105 |
| `mv`: 180, 183 |
| `namei`: 215, 218 |
| `namew6-config`: 143, 144 |
| `neq`: 189, 190 |
| `newgidmap`: 133, 136 |
| `newgrp`: 133, 136 |
| `newuidmap`: 133, 136 |
| `newusers`: 133, 136 |
| `ngetext`: 148, 149 |
| `nice`: 180, 183 |
| `inja`: 177, 178 |
| `nnl`: 180, 183 |
| `nm`: 123, 125 |
| `nohup`: 180, 183 |
| `nnlogin`: 133, 166 |
| `nproc`: 180, 183 |
| `nroff`: 189, 190 |
| `nscd`: 99, 105 |
| `nsenter`: 215, 218 |
| `stat`: 195, 196 |
| `numfmt`: 183, 183 |
| `objcopy`: 123, 125 |
| `objdump`: 125, 125 |
| `od`: 180, 183 |
| `openssl`: 173, 174 |
| `opensvent`: 197, 198 |
| `partx`: 215, 218 |
| `passwd`: 133, 136 |
| `paste`: 180, 183 |
| `patch`: 201, 201 |
| `pathck`: 180, 183 |
| `pcprofiledump`: 99, 105 |
| `dpdfmf`: 189, 190 |
| `droff`: 189, 190 |
| `dpdfexti2dvi`: 203, 204 |
| `peekfd`: 147, 147 |
| `perl`: 161, 162 |
| `perl5.34:0`: 162, 162 |
| `perlbug`: 162, 162 |
| `perdoc`: 162, 162 |
| `perlivp`: 161, 163 |
| `perlthanks`: 163, 163 |
| `pfbtops`: 189, 190 |
| `pgrep`: 213, 213 |
| `pic`: 180, 190 |
| `pic2graph`: 189, 190 |
| `piconv`: 163, 163 |
| `pidof`: 213, 213 |
| `ping`: 158, 159 |
| `ping6`: 158, 159 |
| `pinky`: 180, 183 |
| `pip3`: 175 |
| `pivot`: 205, 218 |
| `pkg-config`: 142, 142 |
| `pkkill`: 213, 213 |
| `pl2pm`: 161, 163 |
| `pldd`: 99, 105 |
| `pmap`: 213, 214 |
| `pod2html`: 161, 163 |
| `pod2man`: 161, 163 |
| `pod2text`: 203, 204 |
| `pod2text`: 161, 163 |
| `podusage`: 161, 163 |
| `podchecker`: 161, 163 |
| `podselect`: 161, 163 |
| `post-grohtml`: 189, 190 |
| `poweroff`: 225, 225 |
| `pr`: 180, 183 |
| `pre-grohtml`: 189, 190 |
| `pre-conv`: 189, 190 |
| `printenv`: 180, 183 |
| `printf`: 180, 183 |
| `prlimit`: 215, 218 |
| `prove`: 161, 163 |
| `prstat`: 147, 147 |
| `ps`: 213, 214 |
| `psdatable`: 197, 198 |
| `psgettable`: 197, 198 |
| `psriptable`: 197, 198 |
| `psxtable`: 197, 198 |
| `pslog`: 147, 147 |
| `pstree`: 147, 147 |
| `pstree.x1`: 147, 147 |
| `ptar`: 161, 163 |
| `ptiff`: 161, 163 |
| `ptargrep`: 161, 163 |
| `ptx`: 180, 183 |
| `pwait`: 213, 214 |
| `pwck`: 133, 136 |
| `pwconv`: 133, 136 |
| `pwdx`: 213, 214 |
| `pwunconv`: 133, 136 |
| `pydoc`: 175 |
| `python3`: 175 |
| `ranlib`: 123, 125 |
| `raw`: 215, 218 |
| `readelf`: 123, 125 |
| `readlink`: 180, 183 |
| `readprofile`: 215, 218 |
| `reboot`: 225, 225 |
| `recode-sr`: 148, 149 |
| `refer`: 189, 190 |
| `rename`: 215, 218 |
| `renice`: 215, 218 |
| `reset`: 143, 146 |
| `resize2fs`: 220, 222 |
| `resizeepart`: 215, 218 |
| `rev`: 215, 218 |
| `rkfile`: 215, 218 |
| `rm`: 180, 183 |
| `rdir`: 180, 183 |
| `rmmod`: 169, 170 |
| `roff2vi`: 189, 190 |
| `roffhtml`: 189, 191 |
| `roff2pdf`: 189, 191 |
| `roff2ps`: 189, 191 |
| `roff2text`: 189, 191 |
| `roff2x`: 189, 191 |
| `route`: 195, 196 |
| `routed`: 195, 196 |
| `rtac`: 195, 196 |
| `rcwake`: 215, 218 |
| `rtmon`: 195, 196 |
| `rtpr`: 195, 196 |
| `rtstat`: 195, 196 |
| `runcon`: 180, 183 |
| `runlevel`: 225, 225 |
| `runtest`: 122, 122 |
| `rview`: 205, 207 |
| `rvim`: 205, 207 |
| `script`: 215, 218 |
| `scriptreplay`: 215, 218 |
| `sdiff`: 186, 186 |
| `sed`: 146, 146 |
| `seq`: 180, 183 |
| `setarch`: 215, 219 |
| `setcap`: 132, 132 |
| `setfac`: 131, 131 |
| `setattr`: 130, 130 |
| `setfont`: 197, 198 |
| `setcodes`: 197, 198 |
| `setled`: 197, 198 |
| `setmetethod`: 197, 198 |
| `setsid`: 215, 219 |
| `setterm`: 215, 219 |
| `setvrgb`: 197, 198 |
| `sfdisk`: 215, 219 |
| `sg`: 133, 136 |
| `sh`: 152, 153 |
| `sha1`: 180, 183 |
| `sha24um`: 180, 183 |
| `sha256um`: 180, 183 |
| `sha512um`: 180, 183 |
| `shaum`: 161, 163 |
| `showconsole`: 197, 198 |
| `showkey`: 197, 198 |
| `shred`: 180, 183 |
| `shuf`: 180, 183 |
| `shutdown`: 225, 225 |
| `size`: 123, 125 |
| `slabtop`: 213, 214 |
| `sleep`: 180, 183 |
| `sln`: 99, 105 |
| `soelim`: 189, 191 |
| `sort`: 180, 183 |
| `sotrus`: 99, 105 |
| `splain`: 161, 163 |
| `split`: 180, 183 |
| `sprof`: 99, 105 |
| `ss`: 195, 196 |
| `stat`: 180, 184 |
| `stbuf`: 180, 184 |



`strings`: 123, 125
`strip`: 123, 125
`stty`: 180, 184
`su`: 133, 136
`sulogin`: 133, 136
`sum`: 180, 184
`swapable`: 215, 219
`swapoff`: 215, 219
`swapon`: 215, 219
`switch_root`: 215, 219
`sync`: 180, 184
`sysctl`: 213, 214
`syslogd`: 223, 224
`tabs`: 143, 145
`tac`: 180, 184
`tail`: 180, 184
`tailf`: 215, 219
`talk`: 158, 159
`taskset`: 215, 219
`tbl`: 189, 191
`tc`: 195, 196
`tclsh`: 119, 120
`tclsh8`: 119, 120
`tee`: 180, 184
`telinit`: 225, 225
`telnet`: 158, 159
`test`: 180, 184
`text2vi`: 203, 204
`texi2pdf`: 203, 204
`texi2any`: 203, 204
`texindex`: 203, 204
`theta`: 189, 191
`tfmtd`: 189, 191
`tftp`: 158, 159
`tic`: 143, 145
`timeout`: 180, 184
`tload`: 213, 214
`toe`: 143, 145
`top`: 213, 214
`touch`: 180, 184
`tputut`: 143, 145
`tr`: 180, 184
`tracoute`: 158, 159
`troff`: 189, 191
`true`: 180, 184
`truncate`: 180, 184
`tset`: 143, 145
`tsort`: 180, 184
`tty`: 180, 184
`tune2fs`: 220, 222
`ulect`: 99, 105
`udevam`: 208, 209
`udevev`: 208, 209
`ul`: 215, 219
`um`: 215, 219
`uname`: 180, 184
`uname26`: 215, 219
`uncompress`: 194, 194
`unexpand`: 180, 184
`unicode_start`: 197, 198
`unicode_stop`: 197, 198
`uniq`: 180, 184
`unlink`: 180, 184
`nlzma`: 110, 111
`unshare`: 215, 219
`unxzz`: 110, 111
`updated`: 128, 188
`uptime`: 213, 214
`useradd`: 133, 136
`userdel`: 133, 136
`usermod`: 133, 136
`users`: 180, 184
`utmp`: 215, 219
`uditt`: 215, 219
`uid`: 215, 219
`uidparse`: 215, 219
`vim`: 215, 219
`view`: 205, 207
`vi`: 205, 207
`what`: 180, 184
`where`: 215, 219
`wc`: 180, 184
`wipe`: 215, 219
`x86`: 110, 111
`xargs`: 188, 188
`xgettext`: 148, 149
`xmlf`: 157, 157
`xubpp`: 161, 163
`xtrace`: 99, 105
`xxd`: 205, 207
`xz`: 110, 111
`xcat`: 110, 111
`xczmp`: 110, 111
`xdec`: 110, 111
`xdd`: 110, 111
`xgrep`: 110, 111
`xfgrep`: 110, 111
`xgrep`: 110, 111
`xless`: 110, 111
`xmore`: 110, 111
`yacc`: 150, 150
`yes`: 180, 184
`ycat`: 194, 194
`zczmp`: 194, 194
`zdiff`: 194, 194
`zump`: 99, 105
`zegrep`: 194, 194
`zfgrep`: 194, 194
`zforce`: 194, 194
`zgrep`: 194, 194
`zic`: 99, 105
`zetails`: 161, 163
`zless`: 194, 194
`zmore`: 194, 194
`znew`: 194, 194
`zramctl`: 215, 219
`znstd`: 112, 112
`zstdgrep`: 112, 112
`zstless`: 112, 112

# Libraries

`Expat`: 164, 164
`ld-2.34.so`: 99, 105
`libac`: 131, 131
`liban`: 99, 105
`libprintf`: 148, 149
`libattr`: 130, 130
`libbfd`: 123, 125
`libbkid`: 215, 219
`libBrokenLocale`: 99, 105
`libbz2`: 108, 109
`libc`: 99, 105
`libcap`: 132, 132
`libcheck`: 185, 185
`libcom_err`: 222, 222
`libcrypt`: 99, 105
`libcrypto.so`: 173, 174
`libctf`: 123, 125
`libctf-nobfd`: 123, 125
`libcursesw`: 143, 145
`libdl`: 99, 105
`lib2p`: 220, 222

# 从零开始构建 Linux - 版本 11.0

`libelf`: 171, 171
`libexpat`: 157, 157
`libexpect-5.45`: 121, 121
`lib2fs`: 220, 222
`libfdisk`: 215, 219
`libffi`: 172
`libfl`: 118, 118
`libform`: 143, 145
`libyy`: 99, 105
`libgcc`: 137, 141
`libcov`: 137, 141
`libdbm`: 155, 155
`libdbm_compat`: 155, 155
`libgetextlib`: 148, 149
`libgetextpo`: 148, 149
`libgetextsrc`: 148, 149
`libgmp`: 126, 127
`libmpx`: 126, 127
`libomp`: 137, 141
`libhistory`: 114, 114
`libmod`: 169
`liblsan`: 137, 141
`libutdl`: 154, 154
`liblto_plugin`: 137, 141
`libma`: 110, 111
`libyy`: 99, 105
`libmagic`: 113, 113
`libman`: 210, 212
`libmandb`: 210, 212
`libcheck`: 99, 105
`libusage`: 99, 105
`libmenuw`: 143, 145
`libmount`: 215, 219
`libmpc`: 129, 129
`libmpfr`: 128, 128
`libncurses`: 143, 145
`liblsnl`: 99, 105
`libss`: 99, 105
`libpcodes`: 123, 125
`libpanelw`: 143, 145
`libprofile`: 99, 106
`libpipeline`: 199
`libproctps`: 213, 214
`libpsx`: 132, 132
`libthread`: 99, 106
`libquadmath`: 137, 141
`libreadline`: 114, 115
`libresolv`: 99, 106
`librt`: 99, 106
`libSegFault`: 99, 105
`libsmartools`: 215, 219
`libss`: 220, 222
`libss.so`: 173, 174
`libsp`: 137, 141
`libstdbuf`: 180, 184
`libdc++`: 137, 141
`libstdc++`: 137, 141
`libupc`: 137, 141
`libbtl6.so`: 119, 120
`libctub8.4`: 119, 120
`libtextstyle`: 148, 149
`libthread_db`: 99, 106
`libtsan`: 137, 141
`libubsan`: 137, 141
`libudev`: 208, 209
`libutil`: 99, 106
`libuud`: 215, 219
`liby`: 150, 150
`libz`: 107, 107
`libzstd`: 112, 112
`preloading_libintl`: 148, 149

# 脚本

`checkfs`: 230, 230
`cleansf`: 230, 230
`console`: 230, 230
`configuring`: 244
`console`: 230, 230
`configuring`: 244
`functions`: 230
`halt`: 230
`hostname`: 230, 230
`hostname`: 230, 230
`ifdown`: 230, 230
`ifup`: 230, 230
`ipv4-static`: 230, 230
`localnet`: 230, 230
`localnet`: 230, 230
`mount`: 215, 219
`mountvirt`: 230, 230
`modules`: 230
`network`: 230, 230
`network`: 230, 230
`rc`: 230
`reboot`: 230, 230
`sendsignal`: 230, 230
`setclock`: 230, 230
`setclock`: 230, 230
`swap`: 230
`sysctl`: 230, 231
`syslogd`: 230, 231
`syslogd`: 230, 231
`template`: 230, 231
`udev`: 230, 231
`udev_retry`: 230, 231

# 其他

`/boot/config-5.13.12`: 257, 260
`/boot/System.map-5.13.12`: 257, 260
`/dev/*`: 74
`/etc/fstab`: 255
`/etc/group`: 77
`/etc/hosts`: 239
`/etc/initab`: 241
`/etc/ld.so.conf`: 104
`/etc/lfs-release`: 263
`/etc/localtime`: 102
`/etc/lsb-release`: 263
`/etc/modprobe.usb.conf`: 259
`/etc/nsswitch.conf`: 102
`/etc/os-release`: 263
`/etc/passwd`: 77
`/etc/profile`: 250
`/etc/protocols`: 98
`/etc/resolv.conf`: 239
`/etc/services`: 98
`/etc/syslog.conf`: 223
`/etc/udev`: 209, 209
`/etc/udev/hwdb.bin`: 208
`/etc/vmire`: 206
`/run`: 77
`/usr/include/asm-generic/*.h`: 49, 49
`/usr/include/asm/*.h`: 49, 49
`/usr/include/drm/*.h`: 49, 49
`/usr/include/linux/*.h`: 49, 49
`/usr/include/misc/*.h`: 49, 49
`/usr/include/mtd/*.h`: 49, 49
`/usr/include/rdma/*.h`: 49, 49
`/usr/include/scsi/*.h`: 49, 49
`/usr/include/sound/*.h`: 49, 49
`/usr/include/video/*.h`: 49, 49
`/usr/include/xen/*.h`: 49, 49
`/var/log`: 77
`/var/log/lastlog`: 77
`/etc/shells`: 254
`man pages`: 97, 97
