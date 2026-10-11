
# Linux From Scratch - 8.0 版本

## 7. 系统配置

### 7.1. 引言

### 7.2. LFS-Bootscripts-20150222

### 7.3. 设备与模块处理概述

### 7.4. 设备管理

### 7.5. 普通网络配置

### 7.6. 系统启动脚本的使用与配置

### 7.7. Bash Shell 启动文件

### 7.9. 创建 `/etc/initrc` 文件

### 8.0. 制作启动盘

### 8.1. 引言

### 8.2. 创建 `/etc/fstab` 文件

### 8.3. Findutils-4.6.0

### 8.4. 使用 IPRoute-2-4.9.0

### 8.5. 配置 GRUB 过程

### 8.6. 结束

### 8.7. 结束

### 8.8. 结束

### 8.9. 结束

### 9.0. 结束

# 前言

# 序

我学习和理解 Linux 的之旅始于十多年前，也就是 1998 年。那时我刚刚安装了我的第一个 Linux 发行版，并迅速被 Linux 背后的整个概念和哲学所吸引。

为了真正让它成为我自己的，我决定从源码编译一切内容，而不是使用预编译的二进制包。这个“完美”的系统将具有各种系统的优点，同时避开它们认为的缺点。起初，这个想法相当令人生畏。但我始终坚持“可以构建出一个系统”这一理念。

在处理了循环依赖和编译错误等问题后，我终于构建了一个定制的 Linux 系统。它运行完全正常，并且像其他任何 Linux 系统一样可以完美使用。但这是我自己的创造。亲手组装出一个属于自己的系统让我非常有成就感。唯一更好的想法就是能亲手创建每一件软件，但这已经是次其次的完美方案了。

当我与 Linux 社区的其他成员分享我的目标和经验时，显然大家对这些想法有着持续的兴趣。显而易见，定制的 Linux 系统不仅能满足特定需求，还为程序员和系统管理员提升（现有的）Linux 技能提供了理想的学习机会。正是在这种广泛兴趣的基础上，“从零构建 Linux”（Linux From Scratch，简称 LFS）项目诞生了。

这本书《Linux From Scratch》是该项目的核心。它为你提供了构建并拥有你自己的系统所需的背景和指令。本书提供了一个可以生成运行系统的模板，你可以自由地修改指令，而这正是该项目的重要部分。你保持着控制权；我们只是在你开启自己的旅程时提供帮助。

我衷心希望你在构建自己的 Linux From Scratch 系统时度过良好的时光，并享受拥有真正属于自己的系统所带来的诸多好处。

```
--
Gerard Beekemans
gerard@linuxfromscratch.org
```

# 目标读者

有很多理由让你想要读读这本书。许多人提出的问题之一是：“既然可以直接下载并安装现有的发行版，为什么要费尽精力从零开始手动构建一个 Linux 系统呢？”

该项目存在的一个原因是是帮助你学习 Linux 系统从内到外是如何运作的。构建一个 LFS 系统展示了 Linux 的运行机制，以及各个组件是如何相互工作和相互依赖的。这种学习体验提供的最好处之一，就是能够根据你的独特需求定制 Linux 系统的能力。

LFS 的另一个关键优势是，它让你对系统拥有更多的控制权，而不依赖于别人的实现。通过 LFS，你处于主驾驶位置，并决定系统的每一个方面。

LFS 允许你创建非常紧凑的 Linux 系统。在安装普通发行版时，你往往被迫安装许多可能永远不会使用或理解的程序。这浪费了资源。你可能会认为，如今的硬盘和 CPU，这些资源不再是考虑因素。然而，如果没有，你仍然受到尺寸考虑的限制。想想可启动光盘、USB 闪盘和嵌入式系统，这些都是 LFS 大显异场的领域。

定制 Linux 系统的另一个优势是安全性。通过从源码编译整个系统，你有权编辑并验证包含的所有安全补丁。你不再需要等待某人编译修复安全漏洞的二进制包。除非你检查该包并实现它，否则你无法保证新的二进制文件是否构建正确，以及是否充分地修复了问题。

Linux From Scratch 的目标是构建一个完整且实用的基础系统。如果你不想从零开始构建自己的系统，你可能无法从书中的信息中获益。

构建自己的 LFS 系统的理由太多，无法在此全部列出。归结底，教育是目前最强大的理由。当你继续你的 LFS 体验时，你将发现它带来的信息和知识。

LFS 的主要目标架构是 AMD/x86 (32位) 和 x86_64 (64位) CPU。另一方面，书中的指令也被已知经过某些修改后可以在 Power PC 和 ARM CPU 上运行。要构建使用这些 CPU 之一的系统，除了接下来几页的内容外，主要前提是已有一个现有的 LFS 系统，例如早期的 LFS 安装、Ubuntu、Red Hat/Fedora、SuSE 或针对你所想要架构的其他发行版。你还会注意到，32 位发行版可以在 64 位 Intel/AMD 设备上构建并作为宿主机使用。

关于 64 位系统的其他一些事实也需要在此补充。与 32 位系统相比，可执行程序的尺寸略大，执行速度稍快。在基于 Core2 Duo CPU 的 LFS-6.5 测试中，评测得了以下统计数据：

| 架构 | 编译时间 | 编译大小 |
| :--- | :--- | :--- |
| 32位 | 198.5 分钟 | 64 MB |
| 64位 | 190.6 分钟 | 709 MB |

如你所见，64 位构建仅比 32 位构建快 4%，大出 9%。迁移到 64 位系统的收益相对较小。当然，如果你需要超过 4GB 的内存，或者想要处理超过 4GB 的数据，64 位系统的优势是巨大的。

LFS 生成的默认 64 位构建被认为是“纯”64 位的。LFS 产生的是一个支持 64 位可执行文件的系统。构建多库系统需要很多时间，且在 LFS 中并不直接支持。你可以参考 Linux Scratch 项目了解这一高级主题。

LFS 的结构尽可能地遵循 Linux 标准。主要标准包括：

- 文件系统层次结构标准 (FHS) 版本 3.0

LFS 有四个独立章节：核心、桌面、运行时语言和图形。除了通用需求外，还有针对架构的需求。还有两个尝试性领域：Gtk3 和图形。LFS 尝试符合前面讨论的架构。



# LSB 与 LFS 兼容性

许多人并不认同 LSB 的要求。定义它的主要目的是确保专用软件能够在兼容系统中安装并正常运行。由于 LFS 是基于源码的，用户完全控制所需的软件包，且许多人选择不安装 LSB 提供的包。

创建一个能够通过 LSB 认证的完整 LFS 系统是可能的，但需要许多超出 LFS 范围的额外包。这些额外包的安装指令在 BLFS 中。

## LSB 组件列表

- 桌面: None

- 图形: None

- 桌面: Als, Cairo, Desktop-file-utils, freetype, Config, Gdk-pixbuf, Glib2, GTK+2, Icon-naming, Libjpeg-turbo, Libpng, Libtiff, Libxml2, MesaLib, Pango, Qt4, Xdg-utils, Xorg

- 图形: CUPS, Cups-filters, Ghostscript, SANE

LSB Desktop: 无

## LFS 系统目标与软件包说明

如前所述，LFS 的目标是构建一个完整且可用的基础级系统。这包括复制自身所需的所有软件包，同时提供了一个相对最小的基础，以便用户根据自己的选择定制出更完整的系统。这并不意味着 LFS 是最小的系统。其中包含了一些并非严格必需的重要软件包。以下列表记录了书中每个软件包的理由。

此包包含主 C 库。没有它，Linux 程序将无法运行。

此包包含数学库，提供任意精度算术的有用函数。构建 Gcc 需要它。

此包包含一个从键值集生成完美哈希函数的程序。Eudev 需要它。

此包包含用于搜索文件的程序。这些程序被大多数软件包的构建脚本使用。

此包是统一引导加载程序。它是若干引导加载程序之一，但是最灵活的。

此包包含压缩和解压文件的程序。解密 LFS 及其它的许多软件包需要它。

此包为网络服务和协议提供数据。启用适当的网络功能需要它。

- Inutils

- Int-gettext

- IPRoute2

此包包含键表文件、键盘实用程序以及若干控制台字体。

此包包含管理内核模块的程序。

此包包含一个非常好文本查看器，允许向上或向下滚动查看文件。它也被 Man-DB 用于查看帮助页。

此包实现了 Linux 内核中提供的 POSIX 1003.1 能力（capabilities）的用户空间接口。

Pipeline 包包含一个以灵活方式操作子进程管道的库。Man-DB 软件包需要它。

此包包含 GNU 库支持脚本。它将共享库复杂性封装在一致的可移植接口中。其他 LFS 软件包的测试套件需要它。

此软件包包含了用于监控进程的程序。这些程序对于系统管理非常有用，也被用于 LFS 引导程序（Bootstraps）。

此软件包包含了显示运行进程信息的程序。这些程序对于系统管理非常有用。

- Readline

此软件包允许在不打开文本编辑器的情况下对文本进行编辑。大多数 LFS 软件包的配置脚本也需要它。

- Shadow

此软件包包含了记录系统消息的程序，例如内核或守护进程在发生异常事件时提供的消息。

- Sysinit

此软件包为 LFS 中使用的几乎所有软件包提供了归档和提取能力。

- T

此软件包包含了读取、写入和转换 info 页面程序。它被用于许多 LFS 软件包的安装过程。

此软件包包含了杂用实用程序。其中包含处理文件系统、控制台、分区和消息的工具。

此软件包包含一个编辑器。选择它是因为它与经典的 vi 编辑器兼容，并且拥有大量强大的功能。编辑器对许多用户来说是一个非常个人的选择，如果需要，可以使用任何其他编辑器。

此软件包是一个与 Expat 接口的 Perl 模块。

此软件包包含了压缩和解压文件的程序。它提供了通常情况下最高的压缩率，对于 XZ 或 LZMA 格式的解压包很有用。

此软件包包含了某些程序使用的压缩和解压程序。

## 构建 LFS 的前提要求

构建 LFS 系统不是一项简单的任务。它要求具备一定水平的 Unix 系统管理知识，以便解决问题并正确执行列出的命令。特别是，作为一个初学者，你应该始终具备使用命令行（shell）复制或移动文件和目录、目录文件及其内容以及更改当前目录的能力。同时也预计你对使用和安装 Linux 软件有合理的了解。

由于 LFS 手籍看起来至少需要这种基础技能，因此各种 LFS 支持论坛不太可能在这些方面为你提供太多帮助。你会发现，你关于此类知识的问题可能得不到回答，或者你会被引向 LFS 核心预读列表。

在构建 LFS 系统之前，我们建议以下内容：

这是一份关于在 Linux 上构建和安装“通用”Unix 软件软件包的全面指南。尽管它是几以前编写的，但它仍然为构建和安装软件所需的基础技术提供了良好的总结。

本指南对从源码构建软件所需的基础技能和技术提供了良好的总结。

## 排版规范示例

为了方便跟读，全书中多处使用了几种排版规范。本节包含了《Linux From Scratch》中贯排版格式的一些示例。

```
./configure --prefix=/usr
```

这种形式的文本设计为除非周围文字另有说明，否则应完全输入。它也被用于解释部分，以标识引用了哪些命令。

在某些情况下，逻辑行通过行尾的反斜杠扩展到两个或多个物理行。

```
CC=gcc -B/usr/bin/../binutils-2.18/configure \ --prefix=/tools --disable-nls --disable-werror
```

注意，反斜杠后必须紧跟一个回车。其他空白字符（如空格或制表符）将产生错误的结果。

```
install-info: unknown option '--dir-file=mnt/lfs/usr/info/dir/
```

这种形式（等宽文本）显示屏幕输出，通常是所发出的命令的结果。这种格式也用于显示文件名，例如 `/etc/ld.so.conf`。

*斜体*

这种形式的文本在书中有多种用途。其主要目的是强调重要的要点或项目。

`http://www.linuxfromscratch.org/`

这种格式用于 LFS 社区内部和外部页面的超链接。它包含了 HOWTO、下载位置、`<<EOF|`

```
cat $LFS/etc/group << "EOF"
root:x:0:
bin:x:1:
...
EOF
```

这种格式用于创建配置文件。第一条命令告诉系统根据后续行中输入的任何内容创建 `$LFS/etc/group` 文件，直到遇到文件结束（EOF）序列。因此，这整个部分都是通用类型输入的。

这种格式用于封装不可见的文本或用于“复制-粘贴”的操作。

这种格式用于封装可选文本。

`passwd(5)`

这种格式用于引用特定的手册（man page）。括号内的数字表示手册内部的特定章节。例如，passwd 有两个页面。对于 LFS 安装说明，这两个页面位于 `/usr/share/man/man5/passwd.5.gz` 和 `/usr/share/man/man5/passwd.5.gz`。

构建 LFS 系统不是一项简单的任务。它要求具备一定水平的 Unix 系统管理知识，以便解决问题并正确执行列出的命令。特别是，作为一个初学者，你应该始终具备使用命令行（shell）复制或移动文件和目录、目录文件及其内容以及更改当前目录的能力。同时也预计你对使用和安装 Linux 软件有合理的了解。

由于 LFS 手籍看起来至少需要这种基础技能，因此各种 LFS 支持论坛不太可能在这些方面为你提供太多帮助。你会发现，你关于此类知识的问题可能得不到回答，或者你会被引向 LFS 核心预读列表。

在构建 LFS 系统之前，我们建议以下内容：

这是一份关于在 Linux 上构建和安装“通用”Unix 软件软件包的全面指南。尽管它是几以前编写的，但它仍然为构建和安装软件所需的基础技术提供了良好的总结。

本指南对从源码构建软件所需的基础技能和技术提供了良好的总结。

为了方便跟读，全书中多处使用了几种排版规范。本节包含了《Linux From Scratch》中贯排版格式的一些示例。

```
./configure --prefix=/usr
```

这种形式的文本设计为除非周围文字另有说明，否则应完全输入。它也被用于解释部分，以标识引用了哪些命令。

在某些情况下，逻辑行通过行尾的反斜杠扩展到两个或多个物理行。

```
CC=gcc -B/usr/bin/../binutils-2.18/configure \ --prefix=/tools --disable-nls --disable-werror
```

注意，反斜杠后必须紧跟一个回车。其他空白字符（如空格或制表符）将产生错误的结果。

```
install-info: unknown option '--dir-file=mnt/lfs/usr/info/dir/
```

这种形式（等宽文本）显示屏幕输出，通常是所发出的命令的结果。这种格式也用于显示文件名，例如 `/etc/ld.so.conf`。

*斜体*

这种形式的文本在书中有多种用途。其主要目的是强调重要的要点或项目。

`http://www.linuxfromscratch.org/`

这种格式用于 LFS 社区内部和外部页面的超链接。它包含了 HOWTO、下载位置、`<<EOF|`

```
cat $LFS/etc/group << "EOF"
root:x:0:
bin:x:1:
...
EOF
```



这种格式用于创建配置文件。第一条命令告诉系统根据后续行中输入的任何内容创建 `$LFS/etc/group` 文件，直到遇到文件结束（`EOF`）序列。因此，这整个部分都是通用类型输入的。

这种格式用于封装不可见的文本或用于“复制-粘贴”的操作。

这种格式用于封装可选文本。

`passwd(5)`

这种格式用于引用特定的手册（man page）。括号内的数字表示手册内部的特定章节。例如，`passwd` 有两个页面。对于 LFS 安装说明，这两个页面位于 `/usr/share/man/man5/passwd.5.gz` 和 `/usr/share/man/man5/passwd.5.gz`。

## 结构

本书分为以下几个部分：

### 第一部分 - 引言

第一部分提供了 LFS 的概述以及相关概念。

### 第二部分 - 准备构建

第二部分描述了如何设置环境。

### 第三部分 - 构建系统

第三部分指导你完成实际的构建过程。

## 错误列表

本节包含了书中已知错误和修正。

## 1.2 自上一个版本以来的更新

以下是自本书上一个版本发布以来软件包的更新列表。

已升级到：

- Bash 4.4

- Check 0.11.0

- Eudev 3.2.1

- E2fsprogs 1.43.4

- File 5.30

- Flex 2.6.3

- Gawk 4.1.4

- GCC 6.3.0

- Glibc 2.25

- GMP 6.1.2

- Grep 3.0

- Route2 4.9.0

- Kbd 2.0.4

- Linux 4.9.9

- Man-DB 2.7.6.1

- Man-pages 4.09

- MPFR 3.1.5

- Perl 5.24.1

- Readline 7.0

- Sed 4.4

- Shadow 4.4

- Texinfo 6.3

- Tzdata 2016j

- Util-Linux 2.29.1

- Vim 8.0.069

- XZ-Utils 5.2.3

- Zlib 1.2.11

新增：

- bash-4.4-upstream_fixes-1.patch

移除：

- bash-4.3.30-upstream_fixes-3.patch

- readline-6.3-upstream_fixes-3.patch

这是《从零开始构建 Linux》的 8.0 版本，日期为 2017 年 2 月 25 日。如果这本书已经超过六个月，可能已经有了更新且更好的版本。如需确认，请通过 `http://www.linuxfromscratch.org/mirrors.html` 查看一个镜像站点。

以下是自本书上一个版本发布以来更改列表。

更新条目：

* *2017-02-25*

    - [dbdubs] - 发布 LFS-8.0。

    - [ken] - 注释掉 coreutils、findutils、gettext 中的 test-lock 测试，因为在某些机器上它现在会死循环。

* *2017-02-19*

    - [dbdubs] - 为 shadow 添加一个修复（嵌入补丁）以修复上游 Bug。

* *2017-02-13*

    - [dbdubs] - 更新到 file-5.30。修复 #4047。

* *2017-02-10*

    - [dbdubs] - 更新到 grep-3.0。修复 #4045。

    - [dbdubs] - 更新到 linux-4.9.9。修复 #4046。

* *2017-02-08*

    - [dj] - 恢复 binutils 在第 5 章中构建 bison 构建。

    - [dj] - 使用 binutils 构建 gold 链接器。bfd 链接器保持为默认值。

* *2017-02-07*

    - [dbdubs] - 添加 bash-4.4 上游补丁。

* *2017-02-05*

    - [dbdubs] - 更新到 glibc-2.25。修复 #4043。

    - [dbdubs] - 将 gperf 回滚到版本 3.0.4。修复 #4044。

    - [dbdubs] - 更新到 linux-4.9.8.tar.xz。修复 #4036。

    - [dbdubs] - 更新到 check-0.11.0。修复 #4035。

    - [dbdubs] - 更新到 shadow-4.4。修复 #4037。

    - [dbdubs] - 更新到 e2fsprogs-1.43.4。修复 #4039。

    - [dbdubs] - 更新到 sed-4.4。修复 #4041。

* *2017-01-22*

    - [dbdubs] - 更新到 linux-4.9.5.tar.xz。修复 #4030。

    - [dbdubs] - 更新到 kbd-2.0.4。修复 #4029。

    - [dbdubs] - 更新到 perl-5.24.1。修复 #4031。

    - [dbdubs] - 更新到 zlib-1.2.11。修复 #4032。

    - [dbdubs] - 更新到 util-linux-2.29.1。修复 #4034。

* *2017-01-08*

    - [dbdubs] - 更新到 linux-4.9.1.tar.xz。修复 #4028。

    - [dbdubs] - 更新到 sed-4.3.tar.xz。修复 #4025。

    - [dbdubs] - 更新到 gperf-3.1。修复 #4026。

* *2017-01-03*

    - [dj] - 更新到 zlib-1.2.10。修复 #4023。

    - [dj] - 更新到 m4-1.48。修复 #4022。

    - [dj] - 开启 LTO 构建 binutils。

* *2017-01-01*

    - [dbdubs] - 更新到 flex-2.6.3。修复 #4020。

    - [dbdubs] - 更新到 xz-5.2.3。修复 #4021。

    - [dbdubs] - 更新到 gcc-6.3.0。修复 #4018。

    - [dbdubs] - 更新到 gmp-6.1.2。修复 #4017。

    - [dbdubs] - 更新到 ip2-4.9。修复 #4016。

    - [dbdubs] - 更新到 man-pages-4.09。修复 #4015。

    - [dbdubs] - 更新到 man-db-2.7.6。修复 #4014。

    - [dbdubs] - 更新到 linux-4.9.9。修复 #4013。

    - [dbdubs] - 更新到 eudev-3.2.1。修复 #4013。

* *2016-12-18*

    - [dj] - 为 x86_64 构建工具链。

    - [dj] - 为 x86_64 修复。

* *2016-12-10*

    - [dbdubs] - 更新到 linux-4.8.1。修复 #4012。

    - [dj] - 更新到 grep-2.27。修复 #4011。

    - [dbdubs] - 修复第 5 章的 #4004。

* *2016-12-03*

    - [dj] - 更新到 coreutils-8.26。修复 #4010。

    - [dj] - 更新到 linux-4.8.12。修复 #4008。

    - [dj] - 更新到 tzdata-2016j。修复 #4007。

* *2016-11-22*

    - [dbdubs] - 更新到 linux-4.8.10。修复 #4005。

    - [dj] - 添加 flex-2.6-1。修复 #4003。

* *2016-11-17*

    - [dbdubs] - 更新到 linux-4.8.8。修复 #4002。

* *2016-11-09*

    - [dbdubs] - 更新到 vim-8.0.069。修复 #4001。

    - [dbdubs] - 更新到 tzdata-2016i。修复 #3999。

    - [dbdubs] - 更新到 file-5.29。修复 #3998。

    - [dbdubs] - 更新到 flex-2.6.2。修复 #3997。

    - [dbdubs] - 更新到 linux-4.8.6。修复 #3996。

    - [dbdubs] - 更新到 util-linux-2.29。修复 #3987。

* *2016-11-07*

    - [dbdubs] - 解释 `/etc/inputrc` 的功能。

    - [ken] - 更新到 iproute2-4.8。修复 #3992。

    - [ken] - 更新到 tzdata-2016h。修复 #3995。

    - [ken] - 更新到 linux-4.8.3。修复 #3994。

* *2016-10-09*



- [dbdubs] - 更新到 `linux-4.8.1`。修复 `#3983`。

- [dbdubs] - 更新到 `mpfr-3.1.5`。修复 `#3984`。

- [dbdubs] - 更新到 `tzdata-2016g`。修复 `#3985`。

- [dbdubs] - 更新到 `grep-2.26`。修复 `#3988`。

- [dbdubs] - 更新到 `man-pages-4.08`。修复 `#3991`。

## *2016-09-16*

- [dbdubs] - 更新到 `bash-4.4`。修复 `#3981`。

- [dbdubs] - 更新到 `readline-7.0`。修复 `#3982`。

- [dbdubs] - 更新到 `linux-4.7.4`。修复 `#3980`。

## *2016-09-14*

- [dbdubs] - 更新到 `LFS-8.0` 发布。

除了对遇到的问题进行简要说明外，任何帮助请求中必须包含的关键内容还有：

- 正在使用的书籍版本（在本例中为 `8.0`）

- 创建 TFS 的宿主机发行版及版本

- `Host System Requirements` 脚本的输出

- 遇到问题的软件包或章节

- 接收到的准确错误信息或症状

- 注意你是否完全偏离了本书的内容

> 偏离本教程并不意味着我们不会为你提供帮助。毕竟，TFS 关乎个人喜好。诚实说明对既定程序的任何更改将有助于我们评估并确定你问题的可能原因。

如果在运行 `configure` 脚本时发生错误，请检查 `config.log` 文件。该文件可能包含 `configure` 过程中遇到的错误。如果你需要帮助，请查看相关行。

屏幕输出和各种文件的内容对于确定编译问题的原因很有用。`configure` 脚本和 `make` 运行的屏幕输出可能有所帮助。没有**必要**包含整个输出，但请包含每项相关信息。以下是你的屏幕 `make` 输出中应包含的信息示例：

```
gcc -DALIASPATH="/mnt/lfs/usr/share/locale:\"
-DLOCALEDIR="/mnt/lfs/usr/share/locale\"
-DLDBDIR="/mnt/lfs/usr/lib\"
-DINCLUDED="/mnt/lfs/usr/include\" -DHAVE_CONFIG_H -I. -I.
-g -o2 -c getopt1.c
gcc -g -o2 -static make -o arscan commands.o dir.o
expand.o file.o getopt implicit.o job main.o
misc.o read.make rule.o variable.o vpath.o
default.o remote-stub.o version.o opt1.o-. In function load_too_high:
/lfs/tmp/make-3.79.1/job.c:1565: undefined reference
to 'getocldagav'
collect2: 13 returned 1 status
make[2]: *** [make] Error 1
make[2]: Leaving directory '/lfs/tmp/make-3.79.1/
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory '/lfs/tmp/make-3.79.1/
make: *** [all-recursive-am] Error 2
```

在这种情况下，许多人只会包含底部部分：

```
make [2]: *** [make] Error 1
```

这些信息不足以正确诊断问题。应该像上面的示例一样保存整个部分，因为那里发生了错误，并且包含了已执行的命令以及相关的错误信息。

关于如何在互联网上寻求帮助的优秀文章可以在网上找到：http://catb.org/~esrf/faqs/smart-questions.html。阅读并遵循本文中的提示可以增加获得所需帮助的概率。

### 2.1. 引言

在本章中，将检查构建 LFS 所需的主机工具，并在必要时进行安装。然后准备一个用于存放 LFS 系统的分区。我们将创建该分区本身，在其上创建文件系统并将其挂载。

### 2.2. 主机系统要求

你的主机系统应具备以下内容，并达到指示的最低版本。这对于大多数 Linux 发行版来说不应该是问题。另外请注意，许多发行版会将头文件放在单独的包中，通常格式为 `<package-name>-devel` 或 `<package-name>-dev`。如果你的发行版提供了这些包，请务必安装它们。

列出的软件包的早期版本可能有效，但尚未经过测试。

- `Bash-3.2` (`/bin/sh` 应该是指向 `bash` 的符号链接或硬链接)

- `Binutils-2.17` (不建议使用大于 `2.27` 的版本，因为尚未经过测试)

- `Bison-2.3` (`/usr/bin/yacc` 应该是指向 `bison` 的链接或执行 `bison` 的小型脚本)

- `Bzipz-1.0.4`

- `Coreutils-6.9`

- `Diffutils-2.8.1`

- `Findutils-4.2.31`

- `Gawk-4.0.1` (`/usr/bin/awk` 应该是指向 `gawk` 的链接)

- `GCC-4.7`，包括 C++ 编译器 `g++` (不建议使用大于 `6.3.0` 的版本，因为尚未经过测试)

> 注意：在某些发行版中，有报告说 `gcc` 使用的一些库可能处于不一致状态，这会干扰某些 LFS 软件包的构建。要检查这一点，请查看 `/usr/lib` 以及可能的 `/usr/lib64` 中的 `libjmp`、`libmpfr` 和 `libmpc`。这三个者应该同时存在或缺失，而不应只有其中两个。如果你的系统存在此问题，请重命名或删除 `.la` 文件，或安装缺失的包。

- `Glibc-2.25` (不建议使用大于 `2.25` 的版本，因为尚未经过测试)

- `Grep-2.5.1a`

- `Gzip-1.3.12`

> 注意：在某些发行版中，有报告说 `gcc` 使用的一些库可能处于不一致状态，这会干扰某些 LFS 软件包的构建。要检查这一点，请查看 `/usr/lib` 以及可能的 `/usr/lib64` 中的 `libjmp`、`libmpfr` 和 `libmpc`。这三个者应该同时存在或缺失，而不应只有其中两个。如果你的系统存在此问题，请重命名或删除 `.la` 文件，或安装缺失的包。

- `Glibc-2.25` (不建议使用大于 `2.25` 的版本，因为尚未经过测试)

- `Grep-2.5.1a`

- `Gzip-1.3.12`

> 注意：在某些发行版中，有报告说 `gcc` 使用的一些库可能处于不一致状态，这会干扰某些 LFS 软件包的构建。要检查这一点，请查看 `/usr/lib` 以及可能的 `/usr/lib64` 中的 `libjmp`、`libmpfr` 和 `libmpc`。这三个者应该同时存在或缺失，而不应只有其中两个。如果你的系统存在此问题，请重命名或删除 `.la` 文件，或安装缺失的包。

- `Glibc-2.25` (不建议使用大于 `2.25` 的版本，因为尚未经过测试)

- `Grep-2.5.1a`

- `Gzip-1.3.12`

> 注意：在某些发行版中，有报告说 `gcc` 使用的一些库可能处于不一致状态，这会干扰某些 LFS 软件包的构建。要检查这一点，请查看 `/usr/lib` 以及可能的 `/usr/lib64` 中的 `libjmp`、`libmpfr` 和 `libmpc`。这三个者应该同时存在或缺失，而不应只有其中两个。如果你的系统存在此问题，请重命名或删除 `.la` 文件，或安装缺失的包。

- `Glibc-2.25` (不建议使用大于 `2.25` 的版本，因为尚未经过测试)

- `Grep-2.5.1a`

- `Gzip-1.3.12`

> 注意：在某些发行版中，有报告说 `gcc` 使用的一些库可能处于不一致状态，这会干扰某些 LFS 软件包的构建。要检查这一点，请查看 `/usr/lib` 以及可能的 `/usr/lib64` 中的 `libjmp`、`libmpfr` 和 `libmpc`。这三个者应该同时存在或缺失，而不应只有其中两个。如果你的系统存在此问题，请重命名或删除 `.la` 文件，或安装缺失的包。

- `Glibc-2.25` (不建议使用大于 `2.25` 的版本，因为尚未经过测试)

- `Grep-2.5.1a`

- `Gzip-1.3.12`



### 软件包列表

- `Bash-3.2` (`/bin/sh` 应该是指向 bash 的符号链接或硬链接)
- `Binutils-2.17` (不建议使用大于 2.27 的版本，因为尚未经过测试)
- `Bison-2.3` (`/usr/bin/yacc` 应该是指向 bison 的链接或执行 bison 的小型脚本)
- `Bzipz-1.0.4`
- `Coreutils-6.9`
- `Diffutils-2.8.1`
- `Findutils-4.2.31`
- `Gawk-4.0.1` (`/usr/bin/awk` 应该是指向 gawk 的链接)
- `GCC-4.7`，包括 C++ 编译器 `g++` (不建议使用大于 6.3.0 的版本，因为尚未经过测试)

> 注意：在某些发行版中，有报告说 `gcc` 使用的一些库可能处于不一致状态，这会干扰某些 LFS 软件包的构建。要检查这一点，请查看 `/usr/lib` 以及可能的 `/usr/lib64` 中的 `libjmp`、`libmpfr` 和 `libmpc`。这三个者应该同时存在或缺失，而不应只有其中两个。如果你的系统存在此问题，请重命名或删除 `.la` 文件，或安装缺失的包。

- `Glibc-2.25` (不建议使用大于 2.25 的版本，因为尚未经过测试)
- `Grep-2.5.1a`
- `Gzip-1.3.12`

### 从零开始 Linux - 版本 8.0

- 在进入 chroot 时，必须为 root 用户设置 LFS 环境变量。否则，LFS 变量将不会被使用。
- 必须挂载虚拟文件系统。这可以在进入 chroot 之前或之后，通过切换到主机虚拟终端并以 root 身份运行第 6.2.2 节“挂载并填充 `/dev`”以及第 6.2.3 节“挂载虚拟文件系统”中的命令来实现。

## 2.4. 创建新分区

与其他操作系统一样，LFS 通常安装在专用分区上。构建 LFS 系统的推荐方法是如果你有足够的空间，使用一个未分区的空间来创建一个。

一个最小系统需要一个大约 6 GB 字节 (GB) 的分区。这足够存储所有的源码 tar 包和软件包了。然而，如果 LFS 打算作为主要的 Linux 系统，可能还会安装额外的软件，这将需要额外的空间。20 GB 的分区对于后续增长来说是一个合理的尺寸。LFS 系统不会占用这么多空间。该分区的大部分空间将用于提供空临时存储，并用于在 LFS 完成后添加额外功能。此外，编译软件包可能需要大量的磁盘空间，这些空间在分区安装后会被回收。

由于没有足够的随机内存 (RAM) 用于编译过程，使用较小的交换空间 (`swap space`) 是好的。该空间供内核用于存储很少使用的数据，并为活动进程留出更多内存。LFS 系统的交换分区可以与你系统使用的分区相同，除非必须创建另一个。

使用 `cfdisk` 或 `fdisk` 启动分区程序，并使用命令行选项指定要在创建新分区的硬盘名称——例如，对于主集成电子设备 (IDE) 磁盘，使用 `/dev/sda`。创建一个 Linux 原生分区，如果需要，再创建一个交换分区。如果你不知道如何使用这些程序，请参阅 `cfdisk (8)` 或 `fdisk (8)`。

> 注意
>
> 对于经验丰富的用户，可以采用其他分区方案。新的 LFS 系统可以位于软件 RAID 阵列或 LVM 逻辑卷上。然而，这些选项中的某些需要 `initramfs`，这是一个高级主题。这些分区方法不推荐初次使用 LFS 的用户。

记住新分区的标识（例如 `sda5`）。这将指向 LFS 分区。同时也请记住交换分区的标识。这些名称稍后用于 `/etc/fstab`。

### 2.4.1. 其他分区问题

关于系统分区的建议请求通常发布在 LFS 邮件列表中。这是一个非常主观的话题。大多数发行版的默认设置是使用整个硬盘，除了一个交换分区。由于几个原因，这对 LFS 并不是最优的。它降低了灵活性，使得在多个发行版或 LFS 构建之间共享数据变得困难，浪费了更多时间，并可能由于文件系统结构的分配效率而浪费空间。

#### 2.4.1.1. 根分区

十 GB 的根分区（不要与 `/root` 目录混淆）对于大多数系统来说是一个很好的折中。它提供了足够的空间来构建 LFS 和大部分 BLFS，但也足够小，可以很容易创建多个分区进行实验。

#### 2.4.1.2. 交换分区

大多数发行版会自动创建一个交换分区。通常推荐的交换分区大小约为物理 RAM 大小的两倍，但这很少需要。如果磁盘空间有限，将交换分区保持在两个 GB，并监控磁盘交换量。

交换（Swapping）永远不是好事。你通常可以通过监听磁盘活动并观察系统对命令的反应来判断系统是否正在进行交换。对交换的第一反应应该是检查是否有不合理的命令，例如编辑一个 5 GB 大的文件。如果交换变成常态，最佳解决方案是为你的系统购买更多 RAM。

#### 2.4.1.3. Grub Bios 分区

如果启动磁盘已使用 GUID 分区表 (GPT) 进行分区，那么如果它尚不存在，则必须创建一个较小的（通常为 1 MB）的分区。此分区不格式化，但必须供 GRUB 在安装引导加载程序期间使用。如果你使用类型为 EF02 的磁盘或使用 `gdisk`，此分区通常会被标记为 'BIOS Boot'。

> `Grub Bios` 分区必须位于 BIOS 用来启动系统的硬盘上。这与 LFS 根分区所在的硬盘不 necessarily同一个。系统上的磁盘可能使用不同的分区表类型。对此分区的要求仅取决于启动磁盘的分区类型。

#### 2.4.1.4. 便利分区

还有其他不是必需的分区，但在设计磁盘布局时应该考虑它们。以下列表并非详尽，但旨在作为指南。



- `boot` – 高度推荐。使用此分区存储内核和其他启动信息。为了尽量减少较大磁盘上潜在的启动问题，请将其设置为你第一块硬盘上的第一个物理分区。100 MB 的分区大小就足够了。

- `home` – 高度推荐。

- `usr` – 独立的 `/usr` 分区通常有用，用于跨发行版或 LFS 构建。大小通常很大，取决于可用磁盘空间。

- `opt` – 此目录用于安装 Gnome 或 KDE 等软件包，大小为 5 到 10 GB。

- `tmp` – 独立的 `/tmp` 分区很少见但有用。

- `usr/src` – 此目录用于存储源码。

## 2.5. 创建文件系统

现在已经建立了空白分区，可以创建文件系统。LFS 可以使用内核识别任何文件系统，最常见的类型是 `ext3` 和 `ext4`。

- `ext2` 适用于更新频繁的分区。

- `ext3` 是 `ext2` 的升级，包含日志以在异常关机的情况下恢复分区状态。

- `ext4` 是文件系统的最新版本，提供了纳秒时间戳和速度改进等新功能。

其他文件系统包括 `FAT32`、`NTFS`、`ReiserFS`、`JFS` 和 `XFS` 用于特殊用途。关于这些文件系统的更多信息可以访问 `http://en.wikipedia.org/wiki/Comparison_of_file_systems`。

LFS 假设根文件系统 (`/`) 是 `ext4` 类型。要在分区上创建 `ext4` 文件系统，运行：

```
mkfs -v -t ext4 /dev/xxx
```

如果你在使用交换空间，不需要对其格式化。如果创建了新的交换分区，需要初始化：

```
mkswap /dev/yyyy
```

将 `<yyyy>` 替换为交换分区的名称。

## 2.6. 设置 LFS 变量

在本书中 `LFS` 将被多次使用。你应该确保在整个 LFS 构建过程中该变量始终定义。它应该被设置为你构建 LFS 系统的目录名称——我们将使用 `/mnt/lfs` 作为示例，但选择取决于你。如果你在单独分区上构建 LFS，此目录将是该分区的挂载点。选择目录位置并使用以下命令设置变量：

```
export LFS=/mnt/lfs
```

拥有此变量对于诸如 `mkdir -v $LFS/tools` 的命令是有益的，shell 在处理命令行时会自动替换 `"$LFS"`（或你设置的任何值）。

> 警告

每当你离开并重新进入当前工作环境时（例如切换到 root 或其他用户），不要忘记检查 `LFS` 是否已设置。使用以下命令检查 `LFS` 变量是否设置正确：

```
echo $LFS
```

确保输出显示 LFS 系统构建位置的路径，如果按照示例操作，应为 `/mnt/lfs`。如果输出错误，请使用本页早前的命令将 `$LFS` 设置为正确的目录名称。

# 注意

## 2.7 挂载新分区

现在文件系统已经创建完成，需要使该分区变得可访问。为了实现这一点，需要将分区挂载到选定的点。对于本书而言，假设文件系统已挂载在上一节描述的 `LFS` 环境变量所指定的目录下。

运行以下命令创建挂载点并挂载 LFS 文件系统：

```
mkdir -pv $LFS
mount -v -t ext4 /dev/<xxx> $LFS
```

将 `<xxx>` 替换为 LFS 分区的标识。

如果为 LFS 使用多个分区（例如，一个用于 `/`，另一个用于 `/usr`），请使用以下命令挂载它们：

```bash
mkdir -pv $LFS
mount -v -t ext4 /dev/<xxx> $LFS
mkdir -v $LFS/usr
mount -v -t ext4 /dev/<yyy> $LFS
```

将 `<xxx>` 和 `<yyy>` 替换为相应的分区名称。

确保此新分区挂载时的权限过于严格（例如使用了 `nosuid` 或 `nodev` 选项）。在不带任何参数运行 `mount` 命令，以查看挂载的 LFS 分区设置了哪些选项。如果设置了 `nosuid` 或 `nodev`，则需要重新挂载分区。

如果你正在使用交换分区，请确保使用 `swapon` 命令将其启用：

```
/sbin/swapon -v /dev/<zzz>
```

将 `<zzz>` 替换为交换分区的名称。

现在已经建立了一个工作的地方，是时候下载软件包了。

# 第 3 章 软件包与补丁

## 3.1. 引言

本章包含了为了构建基础 Linux 系统需要下载的软件包列表。列出的版本号对应于已知良好的软件版本，本书也是基于这些版本的。我们强烈建议不要使用更新的版本，因为一个版本的构建命令可能不适用于较新的版本。最新的软件包版本也可能存在需要变通方案（work-arounds）解决的问题。这些变通方案将在本书的开发中进行开发和稳定。

下载位置并不总是可以访问的。如果本书出版以来下载位置发生了变化：

下载的软件包和补丁需要存储在一个在整个构建过程中都方便的地方。还需要一个工作目录来解包和构建这些软件包。`$LFS/sources` 既可以用于存储补丁，也可以作为工作目录。通过使用此目录，所需的元素位于 LFS 分区，并在构建过程的所有阶段都可用。

在开始下载阶段之前，以 root 用户执行以下命令创建此目录：

```
mkdir -p $LFS/sources
```

使此目录可写并设置粘位位。“粘位”意味着即使多个用户对目录具有写权限，只有文件的所有者才能删除粘位目录中的文件。以下命令将启用写粘位模式：

```
chmod -v awt $LFS/sources
```

下载所有软件包和补丁的一种简单方法是将 `wget-list` 作为 `wget` 的输入。例如：

```
wget --input-file=wget-list --continue --directory-prefix=$LFS/sources
```

此外，在 LFS-7.0 中，有一个单独的文件 `md5sums`，可用于在继续之前验证软件包是否正确。将其放在 `$LFS/sources` 中并运行：

```
pushd $LFS/sources
mdsum -c md5sums
popd
```

## 3.2. 所有软件包

下载或通过其他方式获取以下 KB：

- Acl (2.2.52) - 380 KB:

  下载：`http://download.savannah.gnu.org/releases/acl-2.2.52.src.tar.gz`

  MD5 和：`a614153124269c2212bd7dc7929abda`

- Attr (2.4.47) - 336 KB:

  首页：`http://savannah.nongnu.org/projects/attr`

  下载：`http://download.savannah.gnu.org/releases/attr-2.4.47.src.tar.gz`

  MD5 和：`84f58dec00b60f2dc8fd1c9709291cc7`

- Autoconf (2.69) - 1,186 KB:

  首页：`http://www.gnu.org/software/autoconf/`

  下载：`http://ftp.gnu.org/software/autoconf/autoconf-2.69.tar.xz`

  MD5 和：`50f97f415980e5374639a73e2636f22`

- Automake (1.15) - 1,462 KB:

  首页：`http://www.gnu.org/software/automake/`

  下载：`http://ftp.gnu.org/software/automake/automake-1.15.tar.xz`

  MD5 和：`9a1ddb0e053474d9d1105cfe39b0c48d`

- Bash (4.4) - 9,158 KB:

  首页：`http://www.gnu.org/software/bash/`

  下载：`http://ftp.gnu.org/software/bash/bash-4.4.tar.gz`

  MD5 和：`14888a87c95ac2370559b6f7dfe25`

- Bc (1.06.95) - 288 KB:

  首页：`http://www.gnu.org/software/bc/`

  下载：`http://alpha.gnu.org/bc-1.06.95.tar`

  MD5 和：`5126a721b739f3f2715bc72c3890`

- Binutils (2.27) - 25,488 KB:

  首页：`http://www.gnu.org/binutils/`

  下载：`http://ftp.gnu.org/binutils/binutils-2.27.tar.bz`

  MD5 和：`286c99b5e36e974acab4e9d68`

- Bison (3.0.4) - 1,928 KB:

  首页：`http://www.gnu.org/software/bison/`

  下载：`http://ftp.gnu.org/software/bison/bison-3.0.4.tar.xz`

  MD5 和：`c342201de104ccce0a21ead0d40`

- Bzip2 (1.0.6) - 764 KB:



首页：`http://www.bzip2.org/`

下载：`http://www.bzip2.org/bzip2-1.0.6.tar.gz`

MD5 和：`00b51f64704da7acb501ad9d76`

## Check (0.11.0) - 736 KB:
首页：`http://libcheck.io/`

下载：`https://github.com/libcheck/releases/0.11.0/check-0.11.0.tar.gz`

MD5 和：`9b9052b231f5628c20fdda3485`

## Coreutils (8.26) - 5,676 KB:
首页：`http://www.gnu.org/software/coreutils/`

下载：`http://ftp.gnu.org/gnu/coreutils-8.26.tar.xz`

MD5 和：`3da520a72f662d41189f4c63b`

## DejaGNU (1.6) - 512 KB:
首页：`http://www.gnu.org/software/degnu/`

下载：`http://ftp.gnu.org/gnu/degnu-1.6.tar.gz`

MD5 和：`1fdc2eb0d592c4f89d224df02b`

## Diffutils (3.5) - 1,330 KB:
首页：`http://www.gnu.org/software/diffutils/`

下载：`http://ftp.gnu.org/gnu/diffutils-3.5.tar.xz`

MD5 和：`695354697ff1cf9ade37813615`

## Eudev (3.2.1) - 1,778 KB:
下载：`http://dev.gnu.org/eudev/eudev-3.2.1.tar.gz`

MD5 和：`497f16fc2c711ea95b3c2075d45`

## E2fsprogs (1.4.3) - 7,376 KB:
首页：`http://e2fsprogs.sourceforge.net/`

下载：`http://downloads.sourceforge.net/project/e2fsprogs/v1.4.3/e2fsprogs-1.4.3.tar.gz`

MD5 和：`0bd1c74f357fe69ae2ab6fa6b9aea`

## Expat (2.2.0) - 405 KB:
首页：`http://expat.sourceforge.net/`

下载：`http://prdnowns.sourceforge.net/expat/expat-2.2.0.tar.bz`

MD5 和：`2f47841c8229facb36e6b3f521e2`

## Expect (5.45) - 614 KB:
首页：`http://expect.sourceforge.net/`

下载：`http://prdnowns.sourceforge.net/expect/expect-5.45.tar.gz`

MD5 和：`44e1a4f4c8779ddc5a542dfa7ecc9b`

## File (5.30) - 771 KB:
首页：`http://www.darwinsys.com/file/`

下载：`http://ftp.astron.com/public/file-5.30.tar.gz`

MD5 和：`35eaf05489eae566eafc4d26bb11cd90`

File (5.30) 可能不再可用。备用下载地址为 `http://www.gnu.org/`

## Findutils (4.6) - 3,692 KB:
首页：`http://www.gnu.org/findutils/`

下载：`http://ftp.gnu.org/gnu/findutils-4.6.tar.gz`

MD5 和：`9936aa809`

## Flex (2.6) - 1,373 KB:
首页：`https://github.com/libcheck/`

下载：`https://github.com/libcheck/releases/2.6/flex-2.6.tar.gz`

MD5 和：`a5f665`

## Gawk (4.1) - 2,313 KB:
首页：`http://www.gnu.org/gawk/`

下载：`http://ftp.gnu.org/gnu/gawk-4.1.tar.gz`

MD5 和：`4e72c13889`

## GCC (6.3) - 976 KB:
首页：`http://www.gnu.org/gcc/`

下载：`http://ftp.gnu.org/gnu/gcc-6.3.tar.bz`

MD5 和：`cc77a762c5ff9`

## GDB (1.12) - 822 KB:
首页：`http://www.gnu.org/gdb/`

下载：`http://ftp.gnu.org/gnu/gdb-1.12.tar.gz`

MD5 和：`96ff4c9e74`

## Gettext (0.19) - 7,041 KB:
首页：`http://www.gnu.org/gettext/`

下载：`http://ftp.gnu.org/gnu/gettext-0.19.tar.gz`

MD5 和：`df3f56990aa30fd22853`

## Iana-Etc (2.30) - 201 KB:
主页：`https://freecode.com/projects/iana-etc`

下载地址：`https://anduin.linuxfromscratch.org/LFS/iana-etc-2.30.tar.bz`

MD5: `3a3ab3fd1db26183d247f46cb135ee8`

## Inetutils (1.9.4) - 1,333 KB:
主页：`https://www.gnu.org/software/inetutils/`

下载地址：`https://ftp.gnu.org/gnu/inetutils/inetutils-1.9.4.tar.xz`

MD5: `877ef1a3f603aefc11c4dcc097af75e`

## Intool (0.51.0) - 159 KB:
主页：`https://freesktop.org/wiki/Software/intool`

下载地址：`https://launchpad.net/intool/trunk/0.51.0/download/intool-0.51.0.tar.gz`

MD5: `12e517cac2cb257a0121ca351570fele63`

## IPRoute2 (4.9.0) - 599 KB:
主页：`https://www.kernel.org/pub/linux/utils/net/iproute2/`

下载地址：`https://www.kernel.org/pub/linux/utils/net/iproute2-4.9.0.tar.xz`

MD5: `44a8371a4b2bc40e8e42c9f98cbd41391`

## Kbd (2.0.4) - 1008 KB:
主页：`https://ftp.altlinux.org/pub/people/legion/kbd`

下载地址：`https://www.kernel.org/pub/linux/utils/kbd-2.0.4.tar.xz`

MD5: `1c635a55a8b363aca7f973aeeb39ebaa6`

## Kmod (2.30) - 440 KB:
下载地址：`https://www.kernel.org/pub/linux/kernel/kmod-2.30.tar.xz`

MD5: `3cf469f40cec2d51f56b45a5ea03793e2`

## Less (481) - 310 KB:
主页：`https://www.greensoftsoftware.com/less/`

下载地址：`https://www.greensoftsoftware.com/less-481.tar.gz`

MD5: `50ef40605c65c6252714a743012352767`

## LFS-Bootstraps (20150222) - 31 KB:
下载地址：`https://www.linuxfromscratch.org/downloads/8.0/lfs-bootstraps-20150222.tar.bz`

MD5: `7ee67b16b3b453cd324ed481792169ed`

## Libcap (2.25) - 64 KB:
主页：`https://sites.google.com/site/fullycapable/`

下载地址：`https://www.kernel.org/pub/linux/security-privs/libcap-2.25.tar.xz`

MD5: `6666b839e55d46cad2dc33fc8a2ceb55f77`

## Libpipeline (1.4.1) - 78 KB:



主页：`https://libpipeline.nongnu.org/`

下载地址：`https://download.savannah.gnu.org/releases/libpipeline/libpipeline-1.4.1.tar.gz`

MD5: `e544590e68d6c1239f67b5b44e92022c`

## Libtool (2.4.6) - 951 KB:

主页：`https://www.gnu.org/software/libtool/`

下载地址：`https://ftp.gnu.org/gnu/libtool/libtool-2.4.6.tar.xz`

MD5: `lbfb9b923f2c1339b4d2ce218070644aa5`

### Linux From Scratch - Version 8.0

### Linux (4.9.9) - 91025 KB:

主页：`https://www.kernel.org/`

下载地址：`https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.9.9.tar.xz`

MD5 和：`de43a1a9e3ad19467c9a413bcdf896`

> 注意
>
> 内核更新频率相对较高，通常是因为发现了安全漏洞。除非错误列表页面（errata page）另有说明，否则应使用最新的 4.9.x 内核版本。
>
> 对于速度有限或带宽昂贵的想要更新 Linux 内核的用户，可以单独下载软件包的基版本和补丁。这可以在小版本发布内的后续补丁级别升级中节省一些时间或成本。

### M4 (1.4.18) - 1180 KB:

主页：`https://www.gnu.org/software/m4/`

下载地址：`http://ftp.gnu.org/gnu/m4-1.4.18.tar.xz`

MD5 和：`730bb15d966ffe4714d1e023af82`

### Make (4.2.1) - 1375 KB:

主页：`https://www.gnu.org/software/make/`

下载地址：`http://ftp.gnu.org/gnu/make-4.2.1.tar.bz`

MD5 和：`15b0d2617ec74c0ed4827169257ac`

### Man-DB (2.7.6) - 1506 KB:

主页：`https://www.nongnu.org/man-db/`

下载地址：`http://download.savannah.gnu.org/releases/man-db-2.7.6.tar.xz`

MD5 和：`2948d490d40e7265f0f83aa92698`

### Man-pages (4.09) - 1486 KB:

主页：`https://www.kernel.org/doc/man-pages/`

下载地址：`https://www.kernel.org/pub/linux/doc/man-pages-4.09.tar.xz`

MD5 和：`91c721409bbf8238f623a1fe8ae`

### MPC (1.0.3) - 65 KB:

主页：`https://www.multiprecision.org/`

下载地址：`http://www.multiprecision.org/download/mpc-1.0.3.tar.gz`

MD5 和：`d6a1d5f8dea3abd2cc3e5f385d26`

### MPFR (3.1.5) - 1101 KB:

主页：`https://www.mpfr.org/`

下载地址：`http://www.mpfr.org/mpfr-3.1.5.tar.xz`

MD5 和：`c4a22c71a4b2bc40e8e42c9f98cbd4`

### Ncurses (6.0) - 3859 KB:

主页：`https://www.gnu.org/software/ncurses/`

下载地址：`http://ftp.gnu.org/gnu/ncurses-6.0.tar.gz`

MD5 和：`e13d052e1ead26d0c2807f46ef`

### Patch (2.7.5) - 711 KB:

主页：`https://savannah.gnu.org/projects/patch/`

下载地址：`http://ftp.gnu.org/gnu/patch-2.7.5.tar.xz`

MD5 和：`e3da794043163fb65a01b1db7a`

### Perl (5.24.1) - 13759 KB:

主页：`https://www.perl.org/`

下载地址：`http://www.cpan.org/src/5.0/perl-5.24.tar.bz`

MD5 和：`178ee0e8fa544dc76d99cf041e2c`

### Pkg-config (0.29.1) - 967 KB:

主页：`https://www.freedesktop.org/wiki/pkg-config`

下载地址：`http://pkg-config.freedesktop.org/releases/pkg-config-0.29.1.tar.gz`

MD5 和：`f739a28cea4e0ca291f821d4ef07`

### Procs (3.3.12) - 826 KB:

主页：`https://sourceforge.net/projects/procs-ng`

下载地址：`http://sourceforge.net/projects/procs-ng/files/procs-ng-3.3.12.tar.xz`

MD5 和：`95e74e2ca8b913490b2111524a2b`

### Psmic (22.21) - 447 KB:

主页：`http://psmic.sourceforge.net/`

下载地址：`http://downloads.sourceforge.net/psmic/psmic-22.21.tar.gz`

MD5 和：`9350c7fd6eb20822882632b85fa6`

### Readline (7.0) - 2842 KB:

主页：`http://www.gnu.org/software/readline/readline-retop.html`

下载地址：`http://ftp.gnu.org/readline/readline-7.0.tar.gz`

MD5 和：`250b03a87fc83dab653b826c59b9f`

### Sed (4.4) - 1,154 KB:

主页：`http://www.gnu.org/software/sed`

下载地址：`http://ftp.gnu.org/gnu/sed/sed-4.4.tar.gz`

MD5 和：`e0c58d34c380095abd81cd540f6`

### Shadow (4.4) - 1993 KB:

主页：`https://github.com/shadow-main/shadow/download/4.4/shadow-4.4.tar.xz`

MD5 和：`c06f8c2571b44899e0602fa9d2`

### Syslogd (1.5.1) - 88 KB:

主页：`http://www.infrodrom.org/projects/syslogd`

下载地址：`http://www.infrodrom.org/projects/syslogd/syslogd-1.5.1.tar.gz`

MD5 和：`c7059abf0d37dfe2c9a5b7`

### Sysvinit (2.8) - 108 KB:

主页：`http://savannah.gnu.org/projects/sysvinit`

下载地址：`http://download.savannah.gnu.org/releases/sysvinit-2.8.tar.bz`

MD5 和：`6666b839e55d46cad2dc33fc8a`

### Tar (1.29) - 950 KB:

主页：`http://www.gnu.org/software/tar/`

下载地址：`http://ftp.gnu.org/gnu/tar-1.29.tar.xz`

MD5 和：`f739a28cea4e0ca291f821d4ef07`

### Tcl (8.6) - 5,731 KB:

主页：`http://sourceforge.net/projects/tcl`

下载地址：`http://sourceforge.net/projects/tcl/files/tcl-8.6.tar.gz`

MD5 和：`9350c7fd6eb2082288263b`

# Linux From Scratch - 版本 8.0

- **内存泄漏补丁 - 1.4 KB:**
  下载：`http://www.linuxfromscratch.org/patches/lfs/8.0/bc-1.06.95-memory_leak-l.patch`
  MD5 和：`877e81fba316fe487ec23501059d54b8`

- **Bzip2 文档补丁 - 1.6 KB:**



下载：http://www.linuxfromscratch.org/patches/lfs/8.0/bzip2-1.0.6-install_docs-l.patch

MD5 和：6a5ac7eb8b9791ae556de0f7459167f

- **Coreutils 国际化修复补丁 - 168 KB:**

  下载：http://www.linuxfromscratch.org/patches/lfs/8.0/coreutils-8.26-i18n-l.patch

  MD5 和：e1f87b10b23d6344e5e99e7fabfa7a2

- **Glibc FHS 补丁 - 2.8 KB:**

  下载：http://www.linuxfromscratch.org/patches/lfs/8.0/glibc-2.25-fhs-l.patch

  MD5 和：9a5997c3452990b1769918c759eff8a2

- **Kbd 退格格/删除键修复补丁 - 12 KB:**

  下载：http://www.linuxfromscratch.org/patches/lfs/8.0/kbd-2.0.4-backspace-l.patch

  MD5 和：f75cca16a38da6caa7d52151f7136895

- **Sysinit 整合补丁 - 3.9 KB:**

  下载：http://www.linuxfromscratch.org/patches/lfs/8.0/sysinit-2.88-dfs-consolidated-l.patch

  MD5 和：0b7b5ea568a78dfcc4057b2bf36e5cb

这些补丁的总大小：约 206.7 KB

除了上述所需的补丁外，还有许多由 LFS 社区创建的可选补丁。这些可选补丁解决了一些小问题，或者启用默认未开启的功能。欢迎随时查阅位于 http://www.linuxfromscratch.org/patches/downloads/ 的补丁数据库，并获取任何符合你系统需求的额外补丁。

## 第 4 章 最后的准备工作

### 4.1 引言

在本章中，我们将执行一些额外任务来为构建临时系统做准备。我们将在 `$LFS` 中创建一个目录供非特权用户使用以降低风险，并为该用户创建一个合适的构建环境。我们还将解释用于衡量构建 LFS 软件包所需时间的单位，即“SBUs”（标准构建单元），并提供一些关于软件包测试套件的信息。

### 4.2. 创建 LFS/tools 目录

在第 5 章中编译的所有程序将安装在 `$LFS/tools` 下，以便它们与第 6 章中编译的程序隔离开。在这里编译的程序是临时工具，不会成为最终 LFS 系统的一部分。通过将这些程序保留在单独目录中，可以在使用后轻松删除它们。这可以防止程序进入宿主机的生产目录（这在第 5 章中很容易发生）。

以 root 身份运行以下命令来创建所需的目录：

```bash
mkdir -v $LFS/tools
```

下一步是在宿主机系统上创建一个 `/tools` 符号链接。这将指向 LFS 分区上新创建的目录。同样以 root 身份运行此命令：

```bash
ln -sv $LFS/tools /
```

> 注意
>
> 上述命令是正确的。`ln` 命令有一些语法变体，因此在报告你认为可能是错误之前，请务必检查 `info coreutils ln` 和 `ln (-l)`。

该符号链接使得工具链能够被编译，使其始终引用 `/tools`，这意味着编译器、汇编器和链接器将将在第 5 章（当我们仍使用宿主机的一些工具时）以及下一章（当我们“切换根目录”到 LFS 分区时）中正常工作。

### 4.3. 添加 LFS 用户

当以 root 用户身份登录时，犯一个错误就可能损坏或破坏系统。因此，我们建议以非特权用户的身份构建本章中的软件包。你可以使用自己的用户名，但为了方便设置纯洁的工作环境，请在一个新组（也命名为 lfs）中创建一个新用户 lfs，并在安装过程中使用该用户。以 root 身份执行以下命令添加新用户：

```bash
groupadd lfs
useradd -s /bin/bash -g lfs -m -k /dev/null lfs
```

命令行选项的含义：

- `-s /bin/bash`

  这使得 bash 成为用户 lfs 的默认 shell。

- `-g lfs`

  此选项将用户 lfs 添加到 lfs 组。

- `-m`

  为 lfs 创建一个家目录。

- `-k /dev/null`

  此参数防止拷贝骨架目录（skeleton directory）。

### 4.4. 设置环境

为了为构建临时工具准备好环境，请加载刚刚创建的用户配置文件：

```bash
source ~/.bash_profile
```

### 4.5 关于 SBUs

许多人想预先知道编译安装每个软件包需要多长时间。由于 Linux From Scratch 可以在许多不同的系统上构建，因此无法提供准确的时间估计。最大的软件包（gcc）在最快的系统上大约需要 20 分钟，但在较慢的系统上可能花费三天时间！与其提供实际时间，我们将使用标准构建单元（SBU）衡量标准。

SBU 的工作原理如下：从本书开始编译的第一个软件包是第 5 章中的 Binutils。编译此软件包所需的时间将被称为标准构建单元或 SBU。所有其他时间将相对于此时间表示。

Linux From Scratch - 版本 8.0

考虑一个编译时间为 4.5 SBU 的包。这意味着如果一个系统编译和安装 Binutils 的第一遍需要 10 分钟，那么构建这个示例包大约需要 45 分钟。幸运的是，大多数时间都比 Binutils 短。

总的来说，SBU 并不完全准确，因为它们取决于许多因素，包括宿主系统的 GCC 版本。在这里提供这些数值是为了估算安装一个包可能需要的时间，但在某些情况下，数字的差异可能高达几十分钟。

![](img/a3d49d284a2c7779eb95d9a015d1bb7a_49_0.png)

# 注意

对于许多具有多个处理器（或核心）的现代系统，可以通过设置环境变量或告诉 make 可用多少程序，通过执行“并行编译”（parallel make），来缩短包的编译时间。例如，Core2Duo 可以通过方式支持两个同时运行的进程：

```
export MAKEFLAGS='j 2'
```

或直接进行构建：

```
make -j2
```

当像这样使用多个处理器时，书中的 SBU 波动会比通常大得。。在某些情况下，make 会直接变快。分析构建过程的输出也会更加困难，因为不同进程的行将交叉在一起。如果你在构建步骤遇到问题，请恢复到单处理器构建以正确分析错误信息。

## 4.6. 关于测试套件

大多数包都提供测试套件。为新构建的包运行测试套件是一个好主意，因为它可以提供“完整性检查”，表明所有内容已正确编译。通过一系列检查的测试套件通常证明该包按照开发者的意图运行。但这并不保证包完全没有 true。

某些测试比其他测试重要。例如，核心工具链包——GCC、Binutils 和 Glibc 的测试套件由于它们在运行系统中的核心作用，是最重要的。GCC 和 Glibc 的测试套件可能需要很长时间才能完成，特别是在较慢的硬件上，但强烈建议运行。

![](img/a3d49d284a2c7779eb95d9a015d1bb7a_49_1.png)

# 注意

经验表明，第 5 章中的测试套件几乎没有什么收获。不可避免的事实是，宿主系统总是会对该章节中的测试产生某些影响，通常会导致无法解释的失败。由于第 5 章中构建的工具是临时的并且最终会被丢弃，我们不建议普通读者运行第 5 章中的测试套件。运行这些测试套件的说明是为了测试人员和开发者的利益，但它们是严格可选的。

运行 Binutils 和 GCC 测试套件时的一个常见问题是伪线程（PTYs）。这可能导致大量测试失败。这种情况可能由于几个原因，但最可能的原因是宿主系统没有正确设置 devpts 文件系统。此问题在 http://www.linuxscratch.org/lsfqaj.html#no-ptys 有了更详细的讨论。

有时包测试套件会失败，但原因是开发者已知并认为非关键的。请查阅位于 http://www.linuxfromscratch.org/lfs/build-logs/8.0/ 的日志，以验证这些失败是否在预期之内。该站点对于书中所有测试都有效。

## 第 5 章. 构建临时系统

### 5.1. 引言

本章展示了如何构建一个最小的 Linux 系统。该系统将包含足够的工具来开始构建第 6 章中的最终 LFS 系统，并提供一个比最小环境更具用户便利性的工作环境。

构建这个最小系统有两个步骤。第一步是构建一个新的且与宿主无关的工具链（编译器、汇编器、链接器、库以及一些实用程序）。第二步是使用此工具链构建其他基本工具。

在本章中编译的文件将安装在 `$LFS/tools` 目录下，以将它们与下一章安装的文件以及宿主生产环境的文件隔离开。由于在这里编译的包是临时的，我们不希望它们污染即将建立的 LFS 系统。

### 5.2. 工具链技术说明



本节解释了整体构建方法背后的某些原理和技术细节。不需要立即理解本节中的所有内容。在执行实际构建后，大部分信息将变得更加清晰。在过程中可以随时参考本节。

第 5 章的总体目标是产生一个临时区域，其中包含一组已良好的工具，这些工具可以与宿主系统隔离开。通过使用 `chroot`，后续章节中的命令将包含在该环境中，确保 LFS 系统进行清洁、无故障的构建。构建过程的设计旨在最大限度地减少新读者的风险，同时提供最大的教育价值。

> 注意
>
> 在继续之前，请注意工作平台的性质，通常称为目标三元组（target triplet）。确定目标三元组名称的简单方法是运行许多包源码附带的 `config.guess` 脚本。解压 Binutils 源码并运行脚本：`./config.guess` 并注意输出。例如，对于 32 位 Intel 处理器，输出为 `x86-pc-linux-gnu`。对于 64 位 Intel 处理器，输出为 `x86_64-pc-linux-gnu`。

# Linux From Scratch - 版本 8.0

在第6章进入 `chroot` 环境后，第一个要安装的主要软件包是 Glibc，这是由于上述提到的它具有足够的默认设置。一旦 Glibc 安装到 `/usr`，我们将对工具链进行快速切换，然后继续构建目标 LFS 系统的其余部分。

## 5.3. 通用编译说明

在构建软件包时，说明中包含了几个假设：

- 有几个软件包使用了补丁后编译，但仅在需要通过补丁来规避问题时才这样做。在本章和下一章中都需要补丁，但有时只在其中一个章节中需要。因此，如果下载的补丁说明似乎缺失，请不要担心。应用补丁时也可能会遇到关于偏移（offset）或模糊（fuzz）的警告信息。不要担心这些警告，因为补丁已成功应用。
- 在大多数软件包的编译过程中，会有几个警告在屏幕滚动。这是正常现象，可以安全地忽略。这些警告正如它们出现时的那样——关于对 C 或 C++ 标准的过时但并非无效使用的警告。C 语言的变化频繁，某些软件包仍然在使用旧标准。这并不是问题，但会引起警告的产生。
- 最后检查一次 LFS 环境变量是否正确设置：

```
echo $LFS
```

确保输出显示了 LFS 分区挂载点的路径，在我们的示例中应为 `/mnt/lfs`。
- 最后，必须强调最后两个重要事项：

> **重要**
>
> 构建说明假设宿主机系统要求（包括符号链接）已正确设置：
>
> - `bash` 是正在使用的 shell。
> - `sh` 是指向 `bash` 的符号链接。
> - `/usr/bin/awk` 是指向 `gawk` 的符号链接。
> - `/usr/bin/yacc` 是指向 `bison` 的符号链接，或执行 `bison` 的小型脚本。

> **重要**
>
> 为了强调构建过程：
>
> 1. 将所有源代码和软件包放置在 `chroot` 环境可以访问的目录中，例如 `/mnt/lfs/sources/`。不要将源代码放在 `/mnt/lfs/tools/` 中。
> 2. 切换到源代码目录。
> 3. 对于每个软件包：
>   a. 使用 `tar` 程序解压要构建的软件包。在第 5 章中，确保在解压软件包时你是 LFS 用户。
>   b. 切换到解压软件包时创建目录。
>   c. 按照书籍说明构建软件包。
>   d. 除非另有说明，否则删除解压后的源代码目录。

## 5.4. Binutils-2.27 - 第一阶段

`Binutils` 软件包包含一个链接器、一个汇器以及处理目标文件的其他工具。

近似编译时间：1 SBU

所需的磁盘空间：519 MB

### 5.4.1. 安装 Binutils

> 注意：返回并重新阅读上一节中的注释。理解标记为“重要”的注释将帮助你以后避免很多问题。

让 `Binutils` 第一个编译的软件包是非常关重要的，因为 `Glibc` 和 `GCC` 都会对可用的链接器和汇器进行各种测试，以确定启用它们自己的功能。

`Binutils` 文档建议在专用构建目录中构建 `Binutils`：

```
mkdir -v build
cd     build
```

> 注意：为了使书中其他部分使用的 SBU 值具有意义，请测量从配置到首次安装（包含首次安装）构建此软件包所需的时间。为了实现这一点，请将命令封装在 `time` 命令中，如下：`time ( ./configure ... && make install; )`。

> 注意：第 5 章中的近似编译 SBU 值和所需的磁盘空间不包含测试套件数据。

现在准备编译 `Binutils`：

```bash
../configure --prefix=/tools \
      --with-sysroot=$LFS             \
      --with-lib-path=/tools/lib     \
      --target=$LFS_TGT               \
      --disable-nls                   \
      --disable-error
```

配置选项的含义：

`--prefix=/tools`

这告诉 `configure` 脚本在 `/tools` 目录中准备 `Binutils` 程序。

`--with-sysroot=$LFS`

对于交叉编译，这告诉构建系统根据需要从 `$LFS` 查找目标系统库。

`--with-lib-path=/tools/lib`

这指定了链接器应该配置为使用的库路径。

`--LFS_TGT`

由于 `LFS_TGT` 变量中的机器描述与 `config.guess` 脚本返回的值略有不同，此开关将告诉 `configure` 脚本调整 `Binutil` 的构建系统以构建交叉链接器。

`--disable-nls`

这禁用了国际化，因为临时工具不需要 i18n。

继续编译软件包：

```bash
make
```

编译现在已完成。通常情况下我们现在会运行测试套件，但在这个早期阶段，测试套件框架（Tcl、Expect 和 DejaGNU）尚未就绪。在此阶段运行测试的益处微乎其微，因为来自第一阶段的程序很快就会被第二阶段的程序所取代。

如果在 `x86_64` 上构建，请创建一个符号链接以确保工具链的健全性（sanity de-check）：

```bash
case $(uname -m) in
x86_64) mkdir -v /tools/lib ln -sv lib /tools/lib64 ;;
esac
```

安装软件包：

```bash
make install
```

关于此软件包的详情位于第 6.13.2 节。

## 5.5. GCC-6.3.0 - 第一阶段

`GCC` 软件包包含 C 和 C++ 编译器以及其他工具。

近似编译时间：8 SBU

所需的磁盘空间：5 GB

### 5.5.1. 安装交叉 GCC

`GCC` 需要 `GMP`、`MPFR` 和 `MPC`。在构建交叉编译器时，这些软件包必须可用。

`GCC` 文档建议在专用构建目录中构建 `GCC`：

```
mkdir -v build
cd     build
```

准备编译 `GCC`：

```bash
../configure
--target=$LFS_TGT
--prefix=/tools
--with-glibc-version=2.11
--with-sysroot=$LFS
--with-newlib
--without-headers
--with-local-prefix=/tools/include
--with-native-system-header-dir=/nls
--disable-shared
--disable-multilib
--disable-decimal-float
--disable-threads
--disable-libatomic
--disable-libgomp
--disable-libmpx
--disable-libquadmath
--disable-libsssp
--disable-libvtv
--disable-libstdcxx
--enable-languages=c,c++
```

配置选项的含义：

`--with-newlib`

由于尚无工作的 C 库，这确保在构建 `libc` 时定义 `inhibit_lib_constant`。这防止了需要库支持的代码的编译。

`--without-headers`

在创建完整的交叉编译器时，`GCC` 需要与目标系统兼容的标准头文件。对于我们的目的不需要这些头文件。此开关防止 `GCC` 查找它们。

`--with-local-prefix=/tools`

本地前缀是 `GCC` 搜索本地安装文件的位置。默认是 `usr/local`。将其设置为 `/tools` 有助于防止主机的 `/usr/local` 进入此 `GCC` 的搜索路径。

最后，在 `x86_64` 宿主机上，64 位库的默认名称为“lib”：

```bash
case $(uname -m) in
  x86_64)
    sed -e '/m64=/s/lib64/lib/' \
      -i.orig gcc/i86-t-linux
esac
```



以下命令将找到 `gcc/config` 中命名为 `linux.h`、`linux.64` 或 `sysv.h` 的所有文件。对于每个文件，我们将其复制到带有后缀 `.orig` 的同名文件中。

```bash
for file in gcc/config/{linux.h,linux.64,sysv.h}; do
  cp -uv $file $file.orig
  sed -e 's|/lib|/tools|' \
      -i.orig $file
  echo
  #undef START_FILE_1
  #undef START_FILE_2
  #define START_FILE_PREFIX "/tools/lib/" >> $file
  touch $file.orig
done
```

`--with-native-system-header-dir=/tools/include`

默认情况下，GCC 在 `/usr/include` 中搜索系统头文件。结合 sysroot 切换，这将映射到 LFS`/usr/include`。然而，在接下来的两个节中安装的头文件将存放在 LFS`/tools/include`。此切换确保了 gcc 能够正确找到它们。在 GCC 的第二次编译中，此切换将确保不会找到任何宿主系统的头文件。

`--disable-shared`

`--disable-threads` `--disable-libatomic`, `--disable-libgomp`, `--disable-libmpx`, `--disable-libquadmath`, `--disable-libssp`, `--disable-libvtv`, `--disable-libstdcxx` `--disable-decimal-float`, `--disable-multilib`

这些切换分别禁用了对十进制扩展、线程、`libatomic`、`libgomp`、`libmpx`、`libquadmath`、`libvtv` 以及 C++ 标准库的支持。在构建交叉编译器时，这些功能将导致编译失败，而且对于交叉编译 libc 的任务来说并不是必需。

`--disable-multilib`

在 x86_64 上，LFS 尚未支持 multilib 配置。此切换对 x86 是无害的。

`--enable-languages=c,c++`

此选项确保只构建 C 和 C++ 编译器。这些是目前需要的唯一语言。

运行以下命令编译 GCC：

```bash
# make
```

编译现在已完成。在此时，通常会运行测试套件，但如前所述，测试套件框架尚未就绪。在此时阶段运行测试的好处微乎其微，因为来自第一轮编译的程序很快就会被替换。

安装软件包：

```bash
# make install
```

关于此软件包的详细信息请参阅第 6.17.2 节，“GCC 的内容”。

## 5.6. Linux-4.9.9 API 头文件

Linux API 头文件（在 `linux-4.9.9.tar.xz` 中）暴露了内核的 API 供 Glibc 使用。

预计编译时间：少于 0.1 SBU

所需的磁盘空间：771 MB

### 5.6.1. 安装 Linux API 头文件

Linux 内核需要为系统的 C 语言库（LFS 中的 Glibc）暴露一个应用程序编程接口 (API)。这是通过对 Linux 内核源码压缩包中提供的各种 C 头文件进行清理来实现的。确保软件包中没有嵌入过期文件：

```bash
make mrproper
```

现在从源码中提取用户可见的内核头文件。它们被放置在一个中间本地目录，并复制到所需的位置。`HDR_PATH=dest` 会移除目标目录中的任何现有文件。

```bash
make INSTALL_HDR_PATH=dest headers_install
cp -rv dest/include/* /tools/include
```

关于此软件包的详细信息请参阅第 6.7.2 节，“Linux API 头文件的内容”。

## 5.7. Glibc-2.25

Glibc 软件包包含了主 C 库。该库提供了内存分配、目录搜索、打开和关闭文件、读和写文件、字符串处理、模式匹配、算术等基本例程。

**预计编译时间：**4.1 SBU

**所需的磁盘空间：**753 MB

### 5.7.1. 安装 Glibc

Glibc 文档建议在专用构建目录中构建 Glibc：

```bash
mkdir -v build
cd build
```

接下来，为编译 Glibc 准备：

```bash
../configure \
  --prefix=/tools \
  --host=$LFS_TGT \
  --build=$(../scripts/config.guess \
  --enable-kernel=2.6.32 \
  --with-headers=/tools/include \
  libc_cv_forced_unwind=yes \
  libc_cv_c_cleanup=yes
```

以下选项的含义如下：

```bash
--prefix=/tools \
--host=$LFS_TGT \
--build=$(../scripts/config.guess \
--enable-kernel=2.6.32 \
--with-headers=/tools/include \
libc_cv_forced_unwind=yes \
libc_cv_c_cleanup=yes
```

这些切换组合的效果是 Glibc 交叉编译，使用我们刚刚构建的交叉编译器而不是 `/usr/bin` 中的。

```bash
host=$LFS_TGT
--build=$(../scripts/config.guess \
--enable-kernel=2.6.32
--with-headers=/tools/include
```

此切换告诉 Glibc 针对 2.6.32 之后的内核进行。

```bash
--enable-kernel=2.6.32
```

此切换告诉 Glibc 在 tools 目录安装后进行编译。

```bash
--with-headers=/tools/include
```

此变量传递给 configure 脚本以告知 force-unwind 支持是有效的。

```bash
libc_cv_forced_unwind=yes
```

同样，我们通过 configure 向已安装的 header 传递 C cleanup 支持。

```bash
libc_cv_c_cleanup=yes
```

在此阶段可能会出现以下警告：

```bash
configure: WARNING:
*** These auxiliary programs are missing or
*** incompatible versions: msgfmt
*** some features will be disabled.
*** Check the host system.
```

`msgfmt` 缺失通常没事。如果发生这种情况，使用 `-j1` 重新运行命令。

编译软件包：

```bash
make
```

安装软件包：

```bash
make install
```

如果输出如上方所示，说明一切正常。调查并回溯找到问题所在并修复它。

关于此软件包的详细信息请参阅第 6.9.3 节，“Glibc 的内容”。

## 5.8. Libstdc++-6.3.0

Libstdc++ 是标准 C++ 库。它是 `g++` 编译器正常运行所需的

预计编译时间：0.4 SBU

所需的磁盘空间：898 MB

### 5.8.1. 安装目标 Libstdc++

Libstdc++ 是 GCC 源码的一部分。你首先应该解压 GCC 压缩包并进入 `gcc-6.3.0` 目录。

为 Libstdc++ 创建并进入独立的构建目录：

```bash
mkdir -v build
cd build
```

为编译 Libstdc++ 准备：

```bash
./libstdc++-v3/configure \
--host=$LFS_TGT \
--prefix=$tools \
--disable-multilib \
--disable-nls \
--disable-libstdccxx-threads \
--disable-libstdccxx-pch \
--with-gxx-include-dir=/tools/$LFS_TGT/include/c++/6.3.0
```

configure 选项的含义：

- `--host=...`指示使用我们刚刚构建的交叉编译器，而不是 `/usr/bin` 中的。

- `--disable-libstdccxx-threads`由于我们尚未构建 C 线程库，C++ 库也无法构建。

- `--disable-libstdccxx-pch`此切换阻止安装预编译包含文件，这些在在此阶段是不需要的。



- `--with-gxx-include-dir=/tools/$LFS_TGT/include/c++/6.3.0`这是 C++ 编译器搜索标准头文件的位置。在正常构建中，此信息会自动从顶层目录传递给 Libstdc++ 的 `configure` 选项。在我们的情况下，必须显式提供此信息。

运行以下命令编译 Libstdc++：

```bash
make
```

安装库：

```bash
make install
```

关于此软件包的详情见第 6.17.2 节，“GCC 的内容”。

## 5.9. Binutils-2.27 - 第 2

Binutils 软件包包含一个链接器、一个汇编器以及处理目标文件的工具。

预计构建时间：1.1 SBU

所需的磁盘空间：533 MB

### 5.9.1. 安装 Binutils

再次创建一个独立的构建目录：

```
mkdir -v build
cd build
```

为编译 Binutils 准备绪环境：

```
CC=$LS_TGT-gcc
AR=$LS_TGT-ar
RANLIB=$LS_TGT-ranlib
../configure
--prefix=/tools
--disable-nls
--disable-error
--with-lib-path=/tools/lib
--with-sysroot
```

新配置选项的含义如下：

`CC=$LS_TGT-gcc AR=$LS_TGT-ar RANLIB=$LS_TGT-ranlib`

由于这是新构建的 Binutils，设置这些变量可确保构建系统使用交叉编译器和汇编器，而不是宿主机系统上的工具。

`--with-lib-path=/tools/lib`

这告诉脚本在编译 Binutils 时指定库搜索路径，从而将 `/tools/lib` 传递给链接器。这防止了链接器搜索宿主机上的库目录。

`--with-sysroot`

`sysroot` 功能允许链接器找到由显式包含在链接器命令行中的其他共享对象所需的共享对象。如果没有它，某些软件包可能无法在某些宿主机上成功构建。

编译软件包：

```
make
```

安装软件包：

```
make install
```

现在为下一章中的“重新调整”阶段准备链接器：

```
make -C ld-d clean
make -C ld-d LIB_PATH=/usr/lib:/lib
cp -v ld/ld-new /tools/bin
```

## make 参数的含义：

- `-C ld clean`

这告诉 `make` 程序删除 `ld` 子目录中的所有已编译文件。

- `-C ld LIB_PATH=/usr/lib:/lib`

此选项会重新构建 `ld` 子目录中的所有内容。在命令行上指定 `LIB_PATH` Makefile 变量允许我们覆盖临时工具的默认值，并将其指向正确的最终路径。该变量的值指定了链接器的默认库搜索路径。此准备工作将在下一章中使用。

关于此软件包的详情见第 6.13.2 节，“Binutils 的内容”。

## 5.10. GCC-6.3.0 - 第 2

GCC 软件包包含 GNU 编译器集，包括 C 和 C++ 编译器。

预计构建时间：11 SBU

所需的磁盘空间：2.9 GB

### 5.10.1. 安装 GCC

我们第一次构建 GCC 时安装了几个内部系统头文件。通常其中一个 `limits.h` 将变为包含相应的系统 `limits.h`（在此例中为 `/tools/include/limits.h`）。然而，在第一次构建时，`/tools/include/limits.h` 并不存在，GCC 安装的内部头文件是一个部分的、自包含的文件，并且不包含系统头文件的扩展功能。这对于构建库工具已经足够了，但此版本的 GCC 需要完整的内部头文件。以下是 GCC 构建系统在正常情况下工作时使用的内部头文件的完整版本：

```
cat gcclimitx.h gcc/limits.h gcc/limits.h \ \
  `dirname $($LFS_TGT-gcc-file-name)`/include-fixed/limits.h`
```

再次更改 GCC 默认动态链接器的位置，使用安装在 `/tools` 中的那个。

```
for file in gcc/config/{linux,i386/linux,{64}}; do
  cp -uv ${file},.orig
  sed -e 's@|lib/(64)?\(2)\)|/?@/tools@g' \
  -e 's@/usr/tools@' ${file}.orig > ${file}
  echo
  #ifndef STANDARD_STARTFILE_PREFIX_1
  #ifndef STANDARD_STARTFILE_PREFIX_2
  #define STANDARD_STARTFILE_PREFIX_1 "/tools/lib/"
  #define STANDARD_STARTFILE_PREFIX_2 "/tools/lib/" >> ${file}
  touch ${file}.orig
done
```

如果在 x86_64 上构建，请将 64 位库的目录更改更改 `lib`。

```
case $(uname -m) in
x86_64)
  sed -e 's@|lib=@lib/64/lib/|' \
  -i.orig gcc/config/i386/t-linux
;;
esac
```

作为 GCC 的首次构建，它需要 GMP、MP 和 MPC 软件包。解压包并将它们移动到所需的目录：

```
tar -xf ../mpfr-3.1.5.tar.xz
mv -v mpfr-3.1.5 mpfr
tar -xf ../gmp-6.1.2.tar.xz
mv -v gmp-6.1.2 gmp
tar -xf ../mpc-1.0.3.tar.gz
mv -v mpc-1.0.3 mpc
```

## Linux From Scratch - 版本 8.0

创建一个独立的构建目录：

```
mkdir -v build
cd build
```

在开始构建 GCC 之前，请记住取消任何覆盖默认优化标志的环境变量。

现在为编译 GCC 准备环境：

```
CC=$LFS-gcc
CXX=$LFS-g++
AR=$LFS-ar
RANLIB=$LFS-ranlib
../configure
--prefix=/tools
--with-local-prefix=/tools
--with-system-header-dir=/tools/include
--enable-languages=c,c++
--disable-shared-pch
--disable-multilib
--disable-bootstrap
--disable-libgcc
```

新配置选项的含义如下：

`--enable-languages=c,c++`

此选项确保 C 和 C++ 编译器都同时被构建。

`--disable-shared-pch`

不构建预编译头文件，它占据了大量空间，而且我们不需要它。

`--disable-bootstrap`

对于 GCC 的原生构建，默认设置是“引导式”`bootstrap` 构建，即它不是直接编译 GCC，而是编译它几次。它使用第一轮的程序来编译自身，然后再次进行第三次。对第二次和第三次迭代进行比较，以确保它可以完美无缺地重现。这也意味着它被正确编译了。然而，LFS 构建方法应该提供一个可靠的编译器，而不需要每次都进行引导构建。

编译软件包：

```
make
```

安装软件包：

```
make install
```

作为收尾工作，创建一个符号链接。许多程序和脚本通过 `gcc` 代替运行，以保持程序在并非总是安装了 GNU 编译器的各种系统上的通用性和可用性。这让系统管理员可以自由决定安装哪种编译器：

```
ln -sv gcc /tools/bin/cc
```

## 注意事项

此时，务必确保新工具链的基础功能（编译和链接）按预期工作。若要进行健全性检查，请运行以下命令：

```
echo 'int main(){}' > dummy.c
cc dummy.c
readelf -l a.out | grep /tools/
```

如果一切运行正常，则不应该有错误，且最后一个命令的输出将如下所示：

```
Required program interpreter: /tools/lib/ld-linux.so.2
```

注意 `/tools/lib/` 显示为动态链接器的前缀。如果输出正确，则没有错误。如果没有任何输出，则说明有问题。请查阅第 4.4 节，“设置环境变量”。

当一切顺利后，清理测试文件：

```
rm -v dummy.c a.out
```

## 5.11. Tcl-core-8.6

Tcl 软件包包含工具命令语言。

预计构建时间：0.4 SBU

所需的磁盘空间：40 MB

### 5.11.1. 安装 Tcl-core



此软件包以及接下来的三个（`Expect`、`Denu` 和 `Check`）的安装是为了运行 `GCC` 和 `Binutils` 等软件包的测试套。为了测试目的安装四个软件包似乎过过了，但了解最重要的工具运行正常是非常必要的，即使不是强制的。此处使用的 `Tcl` 是最小版本。对于完整软件包，请 `BLFS Tcl` 程序。

为编译准备 `Tcl`：

```
cd unix
./configure --prefix=/tools
```

构建软件包：

```
make
```

编译已完成。如前所述，运行测试套并不是强制的。如果你仍想运行 `Tcl` 测试套，请执行以下命令：

```
TZ=UTC make test
```

`Tcl` 测试在某些无法理解的主机条件下可能会失败。因此，测试失败并不意外，也不被认为是致命的。`TZ=UTC` 参数在测试期间将时区设置为协调世界时（`UTC`）。这确保了时钟测试被正确执行。关于 `TZ` 环境变量的详情见第 7 节。

安装软件包：

```
make install
```

使已安装的库可写以便删除调试符号：

```
chmod -v u+w /tools/lib/libc8.6.so
```

安装 `Tcl` 的头文件。下一个软件包 `Expect` 需要它们来构建。

```
make install-private-headers
```

现在创建一个必要的符号链接：

```
ln -sv tcl8.6 /tools/bin/tclsh
```

## 5.11.2. Tcl-core 的内容

- 安装的程序：`tclsh`（指向 `tcl8.6`）和 `tclsh8.6`

- 安装的库：`libc8.6.so`, `libclstub8.a`

# 简描述

- **tclsh8.6** Tcl 命令外壳

- **tclsh** 指向 `tclsh8.6` 的链接

- **libtcl8.6.so** Tcl 库

- **libtclstub8.6.a** Tcl Stub 库

## 5.12. Expect-5.45

`Expect` 软件包包含一个程序，用于与其他交互式程序进行脚本化的对话。

预计的大致编译时间：0.1 SBU

所需的磁盘空间：4.3 MB

### 5.12.1. 安装 Expect

首先，强制 `Expect` 脚本使用 `/bin/stty` 而不是它可能在主机系统上找到的 `/usr/local/bin/stty`。这将确保我们的测试套件在工具链的最终构建中保持正常：

```bash
cp -v configure,.orig
sed 's:/usr/local/bin:$bin:|' configure.orig > configure
```

现在为编译 `Expect` 准备：

```bash
./configure --prefix=/tools \
--with-tcl=/tools/lib \
--with-tclinclude=/tools/include
```

`configure` 选项的含义：

- `--with-tcl=/tools/lib`

- `--with-tclinclude=/tools/include`

这确保了 `configure` 在临时工具位置找到 `Tcl` 安装目录，而不是可能在主机系统上找到一个。

使用此选项可以避免 `configure` 因为无法自动发现 `Tcl` 头文件位置而失败的情况。

构建软件包：

```bash
make
```

编译现在已完成。如之前讨论的，对于本章中的临时工具来说，运行测试套件并不是强制性的。如果仍要运行 `Expect` 测试套件，请执行以下命令：

```bash
make test
```

注意，已知 `Expect` 测试套件在某些我们无法控制的条件下可能会发生失败。因此，测试套件的失败并不令人意外，也不被认为是关键问题。

安装软件包：

```bash
make SCRIPTS="" install
```

`make` 参数的含义：

```bash
SCRIPTS=""
```

这防止了安装所需的辅助 `Expect` 脚本。

### 5.12.2. Expect 的内容

安装的程序：`expect`

安装的库：`libexpect-5.45.so`

# 简描述

- `expect`：根据脚本与其他交互式程序通信

- `libexpect-5.45.so`：包含允许 `Expect` 作为 `Tcl` 扩展使用，或直接从 `C` 或 `C++`（无需 `Tcl`）中调的函数

## 5.13. DejaGNU-1.6

`DejaGNU` 软件包包含一个用于测试其他程序的框架。

预计的大致编译时间：小于 0.1 SBU

所需的磁盘空间：3.2 MB

### 5.13.1. 安装 DejaGNU

为编译 `DejaGNU` 准备：

```bash
./configure --prefix=/tools
```

构建并安装软件包：

```bash
make install
```

要测试结果，执行：

```bash
make check
```

### 5.13.2. DejaGNU 的内容

安装的程序：`runest`

**简描述**

- `runest`：一个包装脚本，用于定位正确的 `expect` shell 然后运行 `DejaGNU`

## 5.14. Check-0.11.0

`Check` 是一个用于 `C` 语言的单元测试框架。

预计的大致编译时间：0.1 SBU

所需的磁盘空间：11 MB

### 5.14.1. 安装 Check

```bash
PKG_CONFIG= ./configure --prefix=/
```

`configure` 参数的含义：

`PKG_CONFIG=`

告知此 `configure` 脚本忽略任何可能导致系统尝试链接到 `/tools` 目录之外库的 `pkg-config` 选项。

构建软件包：

```bash
make
```

编译现在已完成。如之前讨论的，对于本章中的临时测试来说，运行测试套件并不是强制性的。如果仍要运行 `Check` 测试套件，请执行以下命令：

```bash
make check
```

注意，`Check` 测试套件可能花费相当长的时间（多达 4 SBU）。

安装软件包：

```bash
make install
```

### 5.14.2. Check 的内容

安装的程序：`checkmk`

安装的库：`libcheck.{a,so}`

**简描述**

- `checkmk`：用于为 `Check` 测试框架生成 `C` 单元测试的 `Awk` 脚本

- `libcheck.{a,so}`：包含允许从测试程序调用 `Check` 的函数

## 5.15. Ncurses-6.0

`Ncurses` 软件包包含用于独立于终端处理字符屏幕的库。

预计的大致编译时间：0.5 SBU

所需的磁盘空间：38 MB

### 5.15.1. 安装 Ncurses

首先，确保在配置期间首先找到 `gawk`：

```bash
sed -i s/awk// configure
```

为编译 `Ncurses` 准备：

```bash
./configure --prefix=/tools \
--with-shared \
--without-debug \
--without-ada \
--enable-wide \
--enable-overwrite
```

`configure` 选项的含义：

- `--without-ada`

这确保 `Ncurses` 不为 `Ada` 编译器构建支持，该编译器可能存在于主机上，但一旦我们进入 `chroot` 环境将不可用。

- `--enable-overwrite`

这告诉 `Ncurses` 将头文件安装到 `/tools/include` 而不是 `/tools/include/ncurses`，以确保其他软件包成功找到 `Ncurses` 头文件。

- `--enable-wide`

此开关导致宽字符库被构建。宽字符库（例如 `libncursesw.6.0`）将替换普通库（例如 `libncurses.6.0`），且它们在多字节区域设置中工作，而普通库仅在 8 位区域设置中工作。

构建软件包：

```bash
make
```

该软件包包含测试套件，但只有在安装软件包后才能运行。测试套件位于 `test/` 目录。查看该目录下的 `README` 文件以获取更多信息。

安装软件包：

```bash
make install
```

## 5.20. Diffutils-3.5

`Diffutils` 包包含显示文件或目录之间差异的程序。

估计编译时间：0.2 SBU

所需磁盘空间：22 MB

### 5.20.1. 安装 Diffutils

为编译准备 `Diffutils`：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 `Diffutils` 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.51.2 节，“`Diffutils` 的内容”。



## 5.21. File-5.30

File 包包含一个确定给定文件或多个文件类型的工具。

估计编译时间：0.1 SBU

所需磁盘空间：16 MB

### 5.21.1. 安装 File

为编译准备 File：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 File 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.12.2 节，“File 的内容”。

## 5.22. Findutils-4.6.0

Findutils 包包含查找文件的程序。这些程序用于通过递归搜索目录树来创建、维护和搜索数据库（通常比递归的 find 更快，但如果数据库没有最近更新，则不可靠）。

估计编译时间：0.3 SBU

所需磁盘空间：35 MB

### 5.22.1. 安装 Findutils

为编译准备 Findutils：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 Findutils 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.53.2 节，“Findutils 的内容”。

## 5.23. Gawk-4.1.4

Gawk 包包含处理文本文件的程序。

估计编译时间：0.2 SBU

所需磁盘空间：35 MB

### 5.23.1. 安装 Gawk

为编译准备 Gawk：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 Gawk 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.52.2 节，“Gawk 的内容”。

## 5.24. Getext-0.19.8.1

Getext 包包含用于国际化和本地化的工具。这些工具允许程序带有 NLS（原生语言支持）时进行编译，使其能够以用户的原生语言输出消息。

估计编译时间：0.9 SBU

所需磁盘空间：164 MB

### 5.24.1. 安装 Getext

对于我们的临时工具集，我们需要从 Getext 编译并安装三个程序。

为编译准备 Getext：

```
cd getext-tools
EMACS="no" ./configure --prefix=/tools --disable-shared
```

配置选项的含义：

`EMACS="no"`

这防止配置脚本确定安装 Emacs Lisp 文件的位置，因为因为已知测试在某些主机上会挂起。

`--disable-shared`

我们目前不需要安装任何共享的 Getext 库，因此没有必要构建它们。

编译软件包：

```
make -C gnulib-lib
make -C intl pluralx.c
make -C src msgfmt
make -C src msgmerge
make -C src gettext
```

由于只编译了三个程序，因此在不额外编译 Getext 包中其他库的情况下是不可能运行测试套件的。因此，不建议在此阶段尝试运行测试套件。

安装 msgfmt、msgmerge 和 gettext

```
cp -v src/{msgfmt,msgmerge,gettext} /tools/bin
```

关于该软件包的详细信息请见第 6.47.2 节，“Getext 的内容”。

## 5.25. Grep-3.0

Grep 包包含用于搜索文件的程序。

估计编译时间：0.2 SBU

所需磁盘空间：19 MB

### 5.25.1. 安装 Grep

为编译准备 Grep：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 Grep 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.31.2 节，“Grep 的内容”。

## 5.26. Gzip-1.8

Gzip 包包含压缩和解压文件的程序。

估计编译时间：0.1 SBU

所需磁盘空间：9 MB

### 5.26.1. 安装 Gzip

为编译准备 Gzip：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 Gzip 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.57.2 节，“Gzip 的内容”。

## 5.27. M4-1.4.18

M4 包包含一个宏处理器。

估计编译时间：0.2 SBU

所需磁盘空间：19 MB

### 5.27.1. 安装 M4

为编译准备 M4：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 M4 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.28.2 节，“M4 的内容”。

## 5.28. Make-4.2.1

Make 包包含用于编译软件包的程序。

估计编译时间：0.1 SBU

所需磁盘空间：12.5 MB

### 5.28.1. 安装 Make

为编译准备 Make：

```
./configure --prefix=/tools --without-guile
```

配置选项的含义：

`--without-guile`

确保 Make-4.2.1 不链接 Guile 库，这些库可能存在于主机上，但在下一章的 chroot 环境中不可。

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 Make 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.61.2 节，“Make 的内容”。

## 5.29. Patch-2.7.5

Patch 包包含通过应用由 diff 程序创建的“patch”文件来修改或创建程序。

估计编译时间：0.2 SBU

所需磁盘空间：11 MB

### 5.29.1. 安装 Patch

为编译准备 Patch：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。正如之前讨论的，对于本章中的临时工具，运行测试套件并不是强制性的。如果仍要运行 Patch 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.62.2 节，“Patch 的内容”。

## 5.30. Perl-5.24.1

Perl 包包含实用提取报告语言（Practical Extraction and Report Language）。

估计编译时间：1.3 SBU

所需磁盘空间：249 MB

### 5.30.1. 安装 Perl

为编译准备 Perl：

```
sh Configure -des -Dprefix=/tools -Dlibs=-lm
```

构建软件包：

```
make
```

虽然 Perl 附带测试套件，但最好等到下一章安装它后再进行。

目前只需要安装一些工具和库：

```
cp -v perl cpan/podlators/scripts/pod2man /tools/bin
mkdir -pv /tools/lib/perl5/5.24.1
cp -Rv lib/* /tools/lib/perl5/5.24.1
```

关于该软件包的详细信息请见第 6.40.2 节，“Perl 的内容”。

## 5.31. Sed-4.4

Sed 软件包包含一个流编辑器。

预计编译时间：0.1 SBU

所需的磁盘空间：16 MB



### 5.31.1. 安装 Sed

为编译准备 Sed：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。如前文所述的，对于本章中的临时工具来说，运行测试套件并不是强制的。但你仍要运行 Sed 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.24.2 节，“Sed 的内容”。

## 5.32. Tar-1.29

Tar 软件包包含一个归档程序。

预计编译时间：0.3 SBU

所需的磁盘空间：33 MB

### 5.32.1. 安装 Tar

为编译准备 Tar：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。如前文所述，对于本章中的临时工具来说，运行测试套件并不是强制的。但你仍要运行 Tar 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.68.2 节，“Tar 的内容”。

## 5.33. Texinfo-6.3

Texinfo 软件包包含用于读取、写入和转换 info 页的程序。

预计编译时间：0.2 SBU

所需的磁盘空间：99 MB

### 5.33.1. 安装 Texinfo

为编译准备 Texinfo：

```
./configure --prefix=/tools
```

> 注意

在配置过程中，会进行一项测试并显示 TestXS_la-TestXS.lo 错误。这与 LFS 无关，应该忽略它。

编译软件包：

```
make
```

编译现在已完成。如前文所述，对于本章中的临时工具来说，运行测试套件并不是强制的。但你仍要运行 Texinfo 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.69.2 节，“Texinfo 的内容”。

## 5.34. Util-linux-2.29.1

Util-linux 软件包包含杂杂实用程序。

预计编译时间：0.9 SBU

所需的磁盘空间：118 MB

### 5.34.1. 安装 Util-linux

为编译准备 Util-linux：

```
./configure --prefix=/tools \
    --without-python \
    --disable-makeinstall-chown \
    --without-systemdsystemunitdir \
    PKG_CONFIG=""
```

配置选项的含义：

- `--without-python`

该开关在主机系统安装了 Python 的情况下禁用使用 Python。它避免了尝试构建所需的绑定程序。

- `--disable-makeinstall-chown`

该开关在安装期间禁用 chown 命令。在安装到 `/tools` 目录时不需要此命令，并且避免了以 root 身份安装的必要。

- `--without-systemdsystemunitdir`

在使用 systemd 的系统中，软件包会尝试将一个 systemd 特定的文件安装到 `/tools` 中不存在的目录。该开关禁用了这一不必要的操作。

- `--PKG_CONFIG=""`

设置此环境变量可以防止添加主机上可能存在的未使用功能。注意，此处设置此环境变量的位置与 LFS 其他章节中在命令前设置变量的位置不同。显示此位置是为了演示在使用 configure 时设置环境变量的另一种方法。

编译软件包：

```
make
```

安装软件包：

```
make install
```

## 5.35. Xz-5.2.3

Xz 软件包包含用于压缩和解压缩文件的程序。它提供了对 Llama 和更新的 xz 压缩格式的支持。使用 xz 压缩文本文件比传统的 gzip 或 bzip2 命令具有更高的压缩率。

预计编译时间：0.2 SBU

所需的磁盘空间：16 MB

### 5.35.1. 安装 Xz

为编译准备 Xz：

```
./configure --prefix=/tools
```

编译软件包：

```
make
```

编译现在已完成。如前文所述，对于本章中的临时工具来说，运行测试套件并不是强制的。但你仍要运行 Xz 测试套件，请执行以下命令：

```
make check
```

安装软件包：

```
make install
```

关于该软件包的详细信息请见第 6.45.2 节，“Xz 的内容”。

## 3.36. 剥离 (Stripping)

本节的步骤是可选的，但如果 LFS 分区较小，学习移除不需要的项目是有益的。到目前为止的可执行文件和库包含了约 70 MB 不需要调试符号。使用以下命令移除它们：

```
strip --strip-debug /tools/lib/*
/usr/bin/strip --strip-unneeded /tools/{,bin}*
```

这些命令将跳过一些文件，并报告无法识别其文件格式。大多数脚本如此。使用系统命令将 strip 二进制文件包含在 `/tools` 中。注意不要对库使用 `--strip-unneeded`。静态库将被破坏，且工具链包将重新构建。

为了保存你的工作，请删除文档：

```
rm -rf /tools/{,info,man,doc}
```

此时，你的 `$LFS` 应该至少有 3 GB 的空闲空间，可用于下一阶段构建和安装 Glibc 和 Gcc。如果你能构建并安装 Glibc，你也可以安装其余部分。

## 3.37. 更改所有权

> 注意

书中剩余命令必须以 root 用户身份登录执行，而不再是 lfs 用户。此外，双重检查 `$LFS` 是否在 root 的环境中。

目前，`$LFS/tools` 目录由用户 lfs 所有，该用户仅存在于主机系统上。如果 `$LFS/tools` 目录保持原样，文件将属于一个没有对应账户的用户 ID。这是危险的，因为创建的用户账户可能会获得此 ID 并拥有 `$LFS/tools` 目录及其所有文件，从而导致这些文件遭受恶意操纵。

为了避免这种情况，你可以在以后创建 `/etc/passwd` 文件时将 lfs 用户添加到新的 LFS 系统中，并确保分配与主机系统相同的用户 ID 和组 ID。但现在请运行以下命令将 `$LFS/tools` 目录的所有权更改为用户 root：

```
chown -R root:root $LFS/tools
```

虽然 LFS 系统完成后可以删除 `$LFS/tools` 目录，但可以保留它以构建该书版本的其他 LFS 系统。如何备备份 `$LFS/tools` 是个人喜好问题。

> 警告

如果你打算保留临时工具以用于构建未来的 LFS 系统，现在是备份它们的时机。第 6 章中的后续命令将更改现有的工具，导致它们对未来的构建毫无用处。

# 第三部分. 构建 LFS 系统

## 第 6 章. 安装基础系统软件

## 6.1. 引言

在本章中，我们进入构建现场，并开始正式构建 L 系统。也就是说，我们将深入研究临时 Linux 系统，做一些准备，然后开始安装软件包。

该软件的安装是直观的。尽管在许多情况下，安装说明可以更简短、更通用，但我们选择为每个软件包提供完整的说明，以最大限度地减少错误可能。学习 Linux 系统如何工作的关键在于了解每个软件包的用途，以及为什么你（系统）可能需要它。

我们不建议使用优化。优化虽然可以使程序运行得更快，但也可能导致编译困难和运行程序时出现问题。如果某个软件包拒绝使用优化进行编译，尝试在不使用优化的情况下编译它，看看在使用优化时是否可以，但存在风险，因为由于代码与构建工具之间复杂的交互，它可能被错误地编译。此外请注意，使用书中未指定的数值的 `-march` 和 `-mtune` 选项未经过测试。这可能会导致工具链包（Binutils、GCC 和 Glibc）出现问题。使用编译器优化带来的微小收益通常无法抵消其风险。鼓励 LFS 的初学者在不使用自定义优化的情况下进行构建。随后的系统仍然运行快速且保持稳定。

必须严格遵循本章安装软件包的顺序，以确保没有程序意外获得硬编码内部的路径。出于相同原因，不要并行编译单独软件包。并行编译可能会失败（尤其是在双 CPU 机器上），并可能导致程序包含硬编码的 `/tools` 路径，从而在目录删除后停止工作。

在安装之前，每个安装页面都提供了有关软件包的信息，对其内容进行了简要描述、预计构建多长时间，以及在此过程中需要的磁盘空间。安装说明之后，列出了软件包安装的程序和库（以及简要描述）。

> 注意

SBU 值和所需的磁盘空间包含了第 6 章所有适用软件包的测试数据。

### 6.1.1. 关于库



通常情况下，LFS 在现代 Linux 系统中已过时。此外，将静态库链接到程序是有害的。如果需要更新库来修复安全问题，则使用静态库的所有程序都需要重新链接到新库。由于静态库的使用并不总是可见的，相关的程序（以及链接步骤）可能完全未知。

在第 6 章的步骤中，我们移除或禁用了大多数静态库的安装。在某些情况下，特别是 `glibc`，静态库的使用一直持续到软件包构建过程。这是通过向 `configure` 传递 `--disable-static` 选项实现的。在其他情况下，需要替代方法。

关于库的更完整讨论，请参见 BLFS 书中的“库：静态还是共享？”。

## 6.2. 准备虚拟内核文件系统

内核导出的各种文件系统用于与内核本身进行通信。这些文件系统是虚拟的，不占用任何磁盘空间。文件系统的内容存储在内存中。

首先创建将挂载这些文件系统的目录：

```
mkdir -pv $LFS/{dev,proc,sys,run}
```

### 6.2.1. 创建初始设备节点

内核启动时，需要一些设备节点，特别是控制台和空设备（null devices）。设备节点必须在硬盘上创建，以便它们在 `udev` 启动之前可用，并且在使用 `init=/bin/bash` 启动 Linux 时可用。运行以下命令创建设备：

```
mknod -m 600 $LFS/console c 5 1
mknod -m 666 $LFS/null c 1 3
```

### 6.2.2. 挂载并填充 /dev

向 `/dev` 目录填充设备的推荐方法是在 `/dev` 目录上挂载一个文件系统（如 `tmpfs`），这允许设备在被检测或访问时在虚拟文件系统上动态创建。设备创建是在启动过程中由 `Udev` 生成的。由于这个新系统还没有 `Udev` 且尚未启动，因此必须手动挂载并填充 `/dev`。这通过绑定挂载（bind mount）系统的 `/dev` 目录来实现。绑定挂载是一种特殊的挂载类型，允许你将目录或挂载点的镜像创建到其他某个位置。使用以下命令实现此操作：

```
mount -v --bind $LFS/dev
```

### 6.2.3. 挂载虚拟内核文件系统

现在挂载剩余的虚拟内核文件系统：

```
mount -vt devpts devpts $LFS/dev/pts -o gid=5,mode=0620
mount -vt proc proc $LFS/proc
mount -vt sysfs sysfs $LFS/sys
mount -vt tmpfs tmpfs $LFS/run
```

`devpts` 挂载选项的含义：

```
gid=5
```

这确保所有由 `devpts` 创建的设备节点都属于组 ID 5。这是我们稍后在 `tty` 组使用的 ID。我们使用组 ID 而不是名称，因为主机可能为其 `tty` 组使用不同的 ID。

```
mode=0620
```

这确保所有由 `devpts` 创建的设备节点模式均为 `0620`（用户可读写，组可写）。与该选项一起使用，确保了 `devpts` 创建的设备节点符合 `grantpt()` 的要求，这意味着不需要 `Glibc` `pt_chown` 辅助二进制文件（默认情况下未安装）。

### Linux From Scratch - Version 8.0

```
if [ -h $LFS/dev/shm ]; then
mkdir -pv $LFS/$(readlink $LFS/dev/shm)
fi
```

## 6.3. 包管理

包管理是 LFS 书中经常被请求的补充内容。包管理器允许跟踪文件的安装情况，从而轻松地删除和升级软件包。除了二进制和库文件外，包管理器还会处理配置文件的安装。在你开始好奇之前，不——这一节将不会讨论任何特定的包管理器。它提供的是对流行技术及其工作原理的概述。对你来说最完美的包管理器可能就在这些技术之中，或者是这些技术中两种或多种技术的组合。本节简要提到了升级软件包时可能出现的问题。

在 LFS 或 BLFS 中提到包管理的一些原因包括：

- 处理包管理会将注意力从这些书籍的目标转移开——教授如何构建 Linux 系统。
- 包管理有多种解决方案，每种方案都有其优缺点。一个满足所有要求的方案是难以企及的。

关于包管理主题有一些提示。访问“提示项目”（Hints Project）并看看其中某项是否符合你的需求。

### 6.3.1. 升级问题

包管理器使得在发布新版本时很容易升级到新版本。通常情况下，LFS 和 BLFS 书中的指令可以用于升级到新版本。在升级软件包时（特别是在运行中的系统上），你应该注意以下几点：

- 如果 `glibc` 需要升级到新版本（例如从 `glibc-2.19` 升级到 `glibc-2.20`），重新构建 LFS 会更安全。你可能需要按照依赖顺序重新构建所有软件包，否则我们不建议这样做。
- 如果包含共享库的软件包已更新，且库的名称发生了变化（注意软件包版本与库名称之间没有对应关系）。例如，一个名为 `foo-1.2.3` 的软件包安装了名为 `libfoo.so.1` 的共享库。假设你将软件包升级到新版本 `foo-1.2.4`，那么所有动态链接到 `libfoo.so.1` 的软件包都需要重新编译，以链接到 `libfoo.so.2`。注意，在依赖包重新编译之前，你不应该删除之前的库文件。

### 6.3.2. 包管理技术

以下是一些常见的包管理技术。在决定包管理器之前，先对各种技术进行研究，特别是特定方案的缺点。

#### 6.3.2.1. 全在我的脑子里

是的，这是一种包管理技术。有些人并不认为需要包管理器，因为他们对软件包非常熟悉，并知道每个软件包安装了哪些文件。某些用户也不需要包管理器，因为他们计划在软件包更改时重新构建整个系统。

#### 6.3.2. 独立目录安装

这是一种简单的软件包管理方式，不需要额外的软件包来管理。每个软件包安装在独立的目录。例如，`foo-1` 安装在 `/usr/pkg/foo-1`。当安装新版本 `foo-2` 时，它安装在 `/usr/pkg/foo-2`，并从 `foo-1` 处创建一个软链接指向 `foo-2`。环境变量如 `PATH`、`LD_LIBRARY_PATH`、`MANPATH`、`INFOPATH` 和 `CPPFLAGS` 需要被扩展。对于较多软件包，这种方案将变得难以管理。

#### 6.3.2. 软链接样式包管理

这是前一种包管理技术的变体。不是创建镜像，而是将每个软件包链接到 `/usr` 层次结构。这由用户创建软链接，许多包管理器使用了这种方法。流行的包括 `Stow`、`Epkg`、`Graft` 和 `Depot`。

以这种方式安装并非易事。例如，假设你正在安装软件包 `libfoo-1.1`。以下指令可能无法安装软件包：

```
/configure --prefix=/usr
make
make install
```

这种情况下，安装可以工作，但依赖包可能不会以你预期的方式链接 `libfoo`。如果你编译一个链接到 `libfoo` 的软件包，可能会发现它链接到了 `/usr/lib/libfoo.so.1`，而不是你预期的 `/usr/lib/libfoo.so.1`。正确的方法是使用 `DESTDIR` 策略来伪装安装。这种方法如下：

```
/configure --prefix=/usr
make
make DESTDIR=/usr/pkg/libfoo/1.1 install
```

大多数软件包都支持这种方法，但有些不支持。对于不合规的软件包，你可能需要手动安装，或者可能发现将某些问题软件包解决到 `/opt` 更容易。

#### 6.3.2.4. 基于时间戳

在这种技术中，在安装软件包之前对文件进行时间标记。安装完成后，简单地使用 `find` 命令配合适当选项即可生成时间戳文件创建后安装的所有文件的日志。使用这种方法编写的包管理器是 `install-log`。

尽管这种方案具有简单的优点，但它有两个缺点。如果在安装过程中，文件使用了任何非当前时间的时间戳，那么这些文件将不会被包管理器跟踪。此外，该方案只能在一次安装一个软件包时使用。如果在两个不同的控制台上安装两个软件包，日志将不可靠。

#### 6.3.2.5. 跟踪安装脚本

在这种方法中，记录安装脚本执行的命令。可以使用两种技术：

# Linux From Scratch - 版本 8.0

`LD_PRELOAD` 环境变量可以在安装前设置为指向某个库。在安装过程中，该库通过将自己挂载到 `cp`、`install`、`mv` 等各种可执行文件上来跟踪正在安装的软件包，并跟踪所有修改文件系统的调用。对于这种方法，所有可执行文件都需要是动态链接的，且没有设置 `suid` 或 `gid` 位。预加载该库可能会在安装期间产生意外的副作用，建议进行一些测试，以确保包管理器不会破坏任何内容并丢失所有适当的文件。

第二种技术是使用 `strace`，它可以在安装脚本执行期间拦截所有的系统调用。

## 6.3.2. 创建软件包存档

在这种方案中，安装过程如符号链接样式（Symlink style）包管理所述，被伪装在一个独立的树结构中。安装完成后，使用已安装的文件创建一个软件包存档。然后，该存档被用于将软件包安装到本地机器上，甚至用于安装到其他机器上。



商业发行版中大多数的包管理器都使用这种方法。遵循这种方法的包管理器示例包括 RPM（顺便说一下，它是 Linux 标准基准规范所需的）、`pkg-utils`、`Debian` 和 Gent 的 Portage 系统。关于如何为 LFS 系统采用这种风格的包管理的提示位于 `http://www.linuxfromscratch.org/hints/downloads/files/fakeroot.txt`。

创建包含依赖信息的软件包是复杂的，这超出了 LFS 的范围。Slack 使用基于 tar 的系统来处理软件包存档。该系统刻意没有像复杂的包管理器那样处理软件包依赖关系。有关 Slack 软件包管理细的详细信息，请参阅 `http://www.slackbook.org/html/package-management.html`。

## 6.3.2.7. 使用基于的管理

这种方案是 LFS 特有的，由 Matthias Benmann 设计，并可以在 Hints 项目中找到。在这种方案中，每个软件包都作为一个单独的用户安装到标准位置。通过检查用户 ID（UID），可以轻松识别属于某个软件包的文件。这种方法的优点和缺点过于复杂，无法在本节中详细描述。更多细节请参阅 `http://www.linuxfromscratch.org/hints/downloads/files/more_control_and_pkg_man.txt` 中的提示。

## 6.3.3. 在多个系统上部署 LFS

LFS 系统的优势之一是，磁盘系统上的文件位置没有差异文件。要将 LFS 克隆以构建另一台与基础系统架构相同的计算机，只需在包含根目录的 LFS 分区（一个基础 LFS 构建解压缩后为 250MB）上使用 `tar`，通过网络传输或 CD-ROM 将其拷贝到新系统并解压。从这一点起，必须更改一些配置文件。可能需要更新的配置文件有：`/etc/hosts`、`/etc/fstab`、`/etc/passwd`、`/etc/group`、`/etc/shadow`、`/etc/ld.so.conf`、`/etc/sysconfig/rc.site`、`/etc/sysconfig/network` 以及 `/etc/sysconfig/ifconfig.eth`。

根据硬件差异和原始内核配置，可能为新系统构建自定义内核。

> 有报告指出，在相似但非完全相同的架构之间拷贝时会出现问题。例如，Intel 系统的指令与 AMD 处理器并不相同，且某些处理器的后续版本可能包含早期版本中不可用的指令。

最后，必须通过第 8.4 节“使用 GRUB 设置引导过程”使新系统变得可引导。

## 6.4. 进入 chroot 环境

现在是进入 chroot 环境开始构建和安装最终的 LFS 系统了。以 root 用户身份运行以下命令，进入目前仅包含临时工具的领域：

```
chroot "$LFS" /tools/bin/env -i \
HOME=$root \
TERM=$TERM \
PS1=\u:\w$ \
PATH=$usr/bin:/usr/sbin:/usr/bin:/tools/bin \
/tools/bin/bash --login -h
```

`env` 命令的 `-i` 选项将清除 chroot 环境的所有变量。之后，将设置 `HOME`、`TERM`、`PS1` 和 `PATH` 变量。`TERM=$TERM` 将 chroot 内部的 TERM 变量设置为与外部相同的值。这是 `vim` 和 `less` 等程序正常运行所必需的。如果需要其他变量（例如 `CFLAGS`），这里是再次设置它们的好地方。

从现在开始，不再需要使用 `$LFS` 变量了，因为所有工作将受限制在 LFS 文件系统中。因为 Bash 已经被告知 `$LFS` 现在就是根（`/`）目录。

注意 `/tools/bin` 位于 `PATH` 的最后。这意味着一旦安装了最终版本，临时工具将不再被使用。这发生在 shell 不“记住”已执行二进制文件位置的情况下——为此原因，通过向 `bash` 传递 `+h` 选项关闭了哈希功能。

注意 `bash` 提示符会显示 I have no name!（我没有名字！）。这是正常的，因为 `/etc/passwd` 文件尚未创建。

- 本章剩余部分及后续章节中的所有命令必须在 chroot 环境内运行，这一点。。如果由于原因离开了此环境（例如重启），请确保按照第 6.2.2 节“挂载并填充 `/dev`”和第 6.2.3 节的说明挂载了虚拟内核文件系统。

## 6.5. 创建目录

是时候为 LFS 创建目录结构了。为了 LFS，我们使用以下命令创建必要的目录：

```bash
mkdir -p /dev /etc /lib /lib64 /root /opt /var /usr /usr/local /usr/bin /usr/sbin /usr/lib /usr/lib64 /usr/include /usr/share /usr/sbin
```

## 6.6. 创建文件

有些程序使用了硬编码的路径。为了满足这些需求，创建一些符号链接：

```bash
ln -s /tools/bash /bin/bash
ln -s /tools/cat /bin/cat
ln -s /tools/echo /bin/echo
ln -s /tools/pwd /bin/pwd
ln -s /tools/stty /bin/stty
ln -s /tools/perl /usr/bin/perl
ln -s /tools/lib/libgcc.so.1 /usr/lib/libgcc.so.1
ln -s /tools/lib/libstdc++.6 /usr/lib/libstdc++.6
ln -s /tools/lib/libstdc++.la /usr/lib/libstdc++.la
```

每个链接的作用：

- `/bin/bash`：许多 `bash` 脚本指定 `/bin/bash`。

- `/bin/cat`：Glibc 配置脚本硬编码了它。

- `/bin/echo`：为了满足 Glibc 测试套件中的某项测试需要。

- `/bin/pwd`：某些配置脚本（特别是 Glibc 的）硬编码了此路径。

- `/bin/stty`：Expect 使用此路径，因此为了 Binutils 和 GCC 测试套件的通过。

- `/usr/bin/perl`：许多 Perl 脚本硬编码了 `perl` 程序的路径。

- `/usr/lib/libgcc.so.1`：Glibc 需要它来线程库。

- `/usr/lib/libstdc++.6`：Glibc 测试套件中的几项测试以及 GMP 的 C++ 支持需要它。

- `/usr/lib/libstdc++.la`：在安装 GCC 后，防止 `/usr/lib/libstdc++.la` 中出现工具引用。

- `/bin/sh`：许多 shell 脚本硬编码了 `/bin/sh`。

运行以下命令创建 `/etc/passwd` 文件：

```
cat /etc/passwd << "EOP"
root:x:0:0:root:/root:/bin/bash
bin:x:1::dev/null:/bin/false
daemon:x:6:6:Daemon User:/dev/null:/bin/false
messagebus:x:18:18:D-Bus Message Daemon User:/var/run/dbus:/bin/false
nobody:x:99:99:Unprivileged User:/dev/null:/bin/false
EOP
```

root 的实际密码（这里使用的 "x" 只是一个占位符）

运行以下命令创建 `/etc/group` 文件：

```bash
cat /etc/group << "EOP"
root:x:0:
bin:x:1:daemon
sys:x:2:
kmem:x:3:
tape:x:4:
tty:x:5:
daemon:x:6:
floppy:x:7:
disk:x:8:
lp:x:9:
dialout:x:10:
audio:x:11:
video:x:12:
utmp:x:13:
usb:x:14:
cdrom:x:15:
mad:x:16:
messagebus:x:18:
syssystemd-journal:x:23:
input:x:24:
mail:x:34:
nogroup:x:99:
users:x:999
EOP
```

创建的组并不是任何标准的一部分——这些组部分取决于本章中 Udev 配置的要求，以及许多 Linux 发行版的约定。此外，某些测试仅依赖特定的用户或组。Linux 标准基础（LSB，可用 `http://www.linuxbase.org`）仅建议存在组 ID (GID) 为 0 的 root 组 GID 为 1 的 bin 组。所有其他组和 GID 都可以由系统管理员选择。良好的程序不依赖 GID 数字，而是使用组名。

要移除“I have no name!”提示，请启动一个新的 shell。由于在第 5 章中安装了完整的 Glibc 并且已经创建了 `/etc/passwd` 和 `/etc/group` 文件，现在用户名和组名解析将可以工作了：



```
exec /tools/bin/bash --login +h
```

注意 `+h` 指令的使用。它告诉 `bash` 不要使用其内部路径哈希（path hashing）。如果不这样做，`bash` 将记住它已执行过的二进制文件的路径。为了确保在安装新编译的二进制文件后立即使用它们，在本章期间将使用 `+h` 指令。

`login`、`getty` 和 `init` 程序（以及其他程序）使用许多日志文件来记录信息，例如谁在何时登录了系统。然而，如果这些日志文件尚不存在，这些程序将不会写入它们。初始化日志文件并赋予它们适当的权限：

```
touch /var/log/{btmp, lastlog, faillog, wtmp}
chgrp -v utmp /var/log/lastlog
chmod -v 664 /var/log/lastlog
chmod -v 600 /var/log/btmp
```

`/var/log/wtmp` 文件记录所有的登录和注销。`/var/log/lastlog` 文件记录每个用户最后登录的时间。`/var/log/faillog` 文件记录失败的登录尝试。`/var/log/btmp` 文件记录错误的登录尝试。

> 注意
>
> `/run/utmp` 文件记录了当前登录的用户。该文件在启动脚本中动态创建。

## 6.7. Linux-4.9.9 API 头文件

Linux-API 头文件（在 `linux-4.9.9.tar.xz` 中）暴露了供 `Glibc` 使用的内核 API。

预计构建时间：小于 0.1 SBU

所需的磁盘空间：767 MB

### 6.7.1. 安装 Linux API 头文件

Linux 内核需要为系统的 C库（LFS 中的 `Glibc`）暴露一个应用程序编程接口 (API)。这是通过对 Linux 内核源码 tar 包中提供的各种 C 头文件进行清理实现的。

确保没有来自之前活动的陈旧文件和依赖项：

```bash
make mrproper
```

现在从源码中提取用户可见的内核头文件。它们被放置在一个中间本地目录中，并复制到所需的位置，提取过程会移除目标目录中的任何现有文件。还有一些内核开发者包含但 LFS 未使用的头文件会从中间目录中移除。

```bash
make INSTALL_HDR_PATH=dest headers_install
find dest/include -name .install -o -name ...cmd -delete
cp -rv dest/include/* /usr/include
```

### 6.7.2. Linux API 头文件的内容

- 安装的头文件：

`/usr/include/asm/*.h`, `/usr/include/asm-generic/*.h`, `/usr/include/drm/*.h`, `/usr/include/linux/*.h`, `/usr/include/misc/*.h`, `/usr/include/mtd/*.h`, `/usr/include/rdma/*.h`, `/usr/include/include/scsi/*.h`, `/usr/include/sound/*.h`, `/usr/include/video/*.h`, and `/usr/include/xen/*.h`

- 安装的目录：

`/usr/include/asm`, `/usr/include/asm-generic`, `/usr/include/drm`, `/usr/include/linux`, `/usr/include/misc`, `/usr/include/mtd`, `/usr/include/rdma`, `/usr/include/scsi`, `/usr/include/sound`, `/usr/include/video`, and `/usr/include/xen`

#### 简述

- `/usr/include/asm/*.h` Linux API 头文件

- `/usr/include/asm-generic/*.h` Linux API ASM 通用头文件

- `/usr/include/drm/*.h` Linux API DRM 头文件

- `/usr/include/linux/*.h` Linux API Linux 头文件

- `/usr/include/mtd/*.h` Linux API MTD 头文件

- `/usr/include/rdma/*.h` Linux API RDMA 头文件

- `/usr/include/scsi/*.h` Linux API SCSI 头文件

- `/usr/include/sound/*.h` Linux API Sound 头文件

- `/usr/include/video/*.h` Linux API Video 头文件

- `/usr/include/xen/*.h` Linux API Xen 头文件

## 6.8. 手页 (Man-pages)

`Man-pages` 包包含 2000 多个页。

预计构建时间：小于 0.1 SBU

所需的磁盘空间：27 MB

### 6.8.1. 安装手页

`Man-pages` 包包含 2000 多个页。

通过运行以下命令安装手页：

```bash
make install
```

### 6.8.2. 手页的内容

- 安装的文件：

各种页

#### 简述

## 6.9. Glibc

`Glibc` 包包含主库。该库提供了内存分配、搜索、打开和关闭文件、字符串处理、算术等例程。

预计构建时间：20 SBU

所需的磁盘空间：1.5 GB

### 6.9.1. 安装 Glibc

> 注意
>
> 构建系统是自包含的，可以完美安装，尽管某些测试可能会失败。`Glibc` 建议在专用目录中构建 `Glibc`：

```bash
mkdir -v build
cd build
```

为编译准备 `Glibc`：

```bash
./configure --prefix=/usr
  --enable-kernel=2.32
  --enable-obsolete-rpc
  --enable-stack-protector=strong
  --libc_cv_libdir=/lib
```

编译包：

```bash
make
```

> 重要
>
> 在本节中，`Glibc` 测试套件被认为是至关重要的。在任何情况下都不要跳过它。

```bash
make check
```

通常会有测试未通过，你可以通常忽略任何测试失败。现在测试构建结果：`Glibc` 测试套件在某种程度上取决于主机系统。以下是常见问题列表

- `posix/tst-info4` 由于在运行时没有网络应用程序而总是失败。`posix/tst-info5` 也是也会失败。

- `rt/tst-cputimer1` 和 `rt/tst-cpuclock2` 测试已知失败。原因尚未完全明确，但迹象表明细微问题会触发这些失败。

- 数学测试在较新的 Intel 或 AMD 处理器上运行时有时会失败。

- `nptl/tst-thread-affinity-[pthread.thread2,sched]` 测试可能会失败，原因尚不确定。

- 在某些架构上已失败的其他测试是 `malloc/tst-malloc-usable` 和 `nptl/tst-cleanup4`。

尽管这是一个无害的消息，`Glibc` 的安装阶段会因为缺少 `/etc/ld.so.conf` 而报错。通过以下操作防止此警告：

```bash
touch /etc/ld.so.conf
```

安装包：

```bash
make install
```

为 `nscd` 安装配置文件和运行时目录：

```bash
cp -v ../nscd/nscd.conf /etc/nscd.conf
mkdir -pv /var/cache/nscd
```

接下来，安装可以让系统以不同语言响应的本地化。没有任何本地化是必须的，但如果缺少某些，未来软件包的测试套件将跳过重要的测试用例。

可以使用 `localedeff` 程序安装特定的区域设置（locale）。例如，下面的第一个 `localedeff` 命令将 `/usr/share/i18n/locales/cs_CZ` 字符无关区域设置定义与 `/usr/share/i18n/charmaps/UTF-8.gz` Map定义结合，并将结果追加到 `/usr/lib/locale-archive` 文件中。以下指令将安装为了优化测试覆盖所需的区域设置集：



```
mkdir -pv /usr/lib/locale
localedeff -i cs_CZ -f UTF-8 cs_CZ.UTF-8
localedeff -i de_DE -f ISO-8859-1_de
localedeff -i de_DE_euro -f ISO-8859-15_de_DE@euro
localedeff -i de_DE -f UTF-8 de_DE.UTF-8
localedeff -i en_GB -f UTF-8 en_GB.UTF-8
localedeff -i en_HK -f ISO-8859-1_en_HK
localedeff -i en_PH -f ISO-8859-1_en_PH
localedeff -i en_US -f ISO-8859-1_en_US
localedeff -i en_US -f UTF-8 en_US.UTF-8
localedeff -i es_MX -f ISO-8859-1_es_MX
localedeff -i fa_IR -f UTF-8 fa_IR
localedeff -i fr_FR -f ISO-8859-1_fr_FR
localedeff -i fr_FR@euro -f ISO-8859-15 fr_FR@euro
localedeff -i it_FR -f UTF-8 fr_FR.UTF-8
localedeff -i it_IT -f ISO-8859-1_it_IT
localedeff -i it_IT -f UTF-8 it_IT.UTF-8
localedeff -i ja_JP -f EUC-JP ja_JP
localedeff -i ru_RU -f KOI8-R ru_RU.KOI8-R
localedeff -i ru_RU -f UTF-8 ru_RU.UTF-8
localedeff -i tr_TR -f UTF-8 tr_TR.UTF-8
localedeff -i zh_CN -f GB18030 zh_CN.GB18030
tests:
```

此外，请安装适用于你所在国家、语言和字符集的区域设置。

或者，可以使用一个耗时的命令一次性安装 `glibc-2.25/localedata/SUPPORTED` 文件中的所有区域设置（它包含了上述列出的所有区域以及更多）：

```
make localedata/install-locales
```

然后，在极少数需要的情况下，使用 `localedeff` 命令创建并安装 `glibc-2.25/localedata/SUPPORTED` 文件中未列出的区域设置。

## 6.9.2. 配置 Glibc

### 6.9.2.1. 添加 nsswitch conf

需要创建 `/etc/nsswitch.conf` 文件，因为 Glibc 的默认设置在网络环境中工作并不良好。

运行以下命令创建一个新文件 `/etc/nsswitch.conf`：

```
cat > /etc/nsswitch.conf << "EOF"
# Begin /etc/nsswitch.conf

passwd: files
group: files
shadow: files

hosts: files
networks: files

protocols: files
services: files
ethers: files
rpc: files

# End /etc/nsswitch.conf
EOF
```

### 6.9.2.2. 添加时区数据

使用以下命令安装并设置时区数据：

```
tar -xf ../tzdata2016j.tar.gz
ZONEINFO=/usr/share/zoneinfo
mkdir -p $ZONEINFO/{posix,right}
```

```
for tz in et cetera southamerica northamerica europe africa antarctica \
    asia australia backward pacificmv systemv; do
    zic -L /dev/null -d $ZONEINFO -y "sh yearirstype.sh" $(tz)
    zic -L /dev/null -d $ZONEINFO/posix -y "sh yearirstype.sh" $(tz)
    zic -L leapseconds -d $ZONEINFO/right -y "sh yearirstype.sh" $(tz)
done
```

```
cp -v zone1970.tab iso3166.tab $ZONEINFO
zic -d $ZONEINFO -p America/New_York
unset ZONEINFO
```

`zic` 命令的含义：

```
zic -L /dev/null ...
```

这会创建不包含任何秒的时区。惯例上将它们同时放在 `zoneinfo` 和 `zoneinfo/posix` 中。有必要将 POSIX 时区放在 `zoneinfo` 中，否则各种测试套件将报告错误。在空间紧张且你不打算更新时区的嵌入系统中，通过不使用 `posix` 目录可以节省 1MB 空间，但某些应用程序或测试套件可能会失败。

`zic -L leapseconds ...`

这会创建包含闰秒的右时区。在空间紧张且你不打算更新时区或不在乎时间准确性的嵌入系统中，可以通过省略 `right` 目录来节省 1MB 空间。

`zic -L ... -P`

这会创建 POSIX 格式的时区。

`zic -L ... -y`

这会根据脚本指定的年份类型。

`zic`

这会创建时区。

# xtrace

通过打印当前执行的函数来跟踪程序的执行情况

# zdump

时区转储器

# zic

时区编译器

# ld-2.25.so

共享库可执行程序的辅助程序

# libBrokenLocale

Glibc 内部使用，作为一种粗略的手段（hack），用于运行某些损坏的程序（例如某些 Motif 应用）。更多信息请参阅 `glibc-2.25/locale/broken_cur_max.c` 中的注释。

# libSegFault

段错误处理器，被 `catchsegy` 使用。

# libanl

异步名称查找库

# liblibc

主 C 库

Glibc 内部使用，用于在 `getaddrinfo()` 函数中处理国际化域名。

# libcrypt

密码学库

# libdl

动态链接接口库

# libg

不包含任何函数的空库。以前曾是 g++ 的运行时库。

# libieee

在此模块中链接了由电气与电子工程师学会（IEEE）定义的数学函数错误处理规则。默认是 POSIX.1 错误处理。

# libm

数学库

# libcheck

链接时开启内存分配检查。

# libmemusage

`memusage` 使用，用于收集程序内存使用的信息。

# libnsl

网络服务库

# libnss

名称服务切换（Name Service Switch）库，包含解析主机名、用户名、组名、别名、服务、协议等函数。

# libthread

POSIX 线程库

# libresolv

包含创建、发送和拦截指向互联网名称服务器请求的函数。

# libprcsvc

包含提供杂杂 RPC 服务的函数。

# librt

包含提供 POSIX.1 实时扩展指定的多数接口的函数。

# libthread_db

包含构建多线程程序调试器的有用函数。

# libutil

包含许多不同 Unix 工具中使用的“标准”函数的代码。

## 6.10 调整工具链

现在最终的 C 库已经安装，是时候调整工具链了，以便任何新编译的程序都能链接到这些库。

首先，备份 `/tools` 链接器并将其替换为我们在第 5 章中制作的调整后的链接器。我们会在 `/tools/$(uname)-pc-linux-gnu/bin` 中为它的对应项创建一个链接：

```bash
mv -v /tools/bin/(ld,ld-old)
mv -v /tools/$(uname)-pc-linux-gnu/bin/{ld,ld-old}
mv -v /tools/bin/(ld-new,ld)
ln -sv /tools/bin/ld /tools/$(uname)-pc-linux-gnu/bin
```

接下来，修改 gcc spec 文件，使其指向新的动态链接器。只需删除所有 "tools" 实例，就就会留下指向动态链接器的正确路径。同时调整 spec 文件，让 gcc 知道去哪里寻找正确的头文件和 Glibc 起始文件。一个 sed 命令可以完成这一点：



```bash
gcc -dumpspec | sed -e '@/tools@$g' \
-e '@startfile_prefix_spec;/(n;s@.**/usr/lib/@' \
-e '@cpp:/n;s@@@-system /usr/include/@' \
-dinarame $(gcc --print-libgcc-file-name)`/specs
```

检查 `spec` 文件以验证预期更改已生效是一个好主意。

确保调整后的工具链的基本功能（编译和链接）按预期工作至关重要。为了做到，执行以下健全检查：

```bash
echo 'int main() {} > dummy.c
cc dummy.c -v -Wl,--verbose &> dummy.log
readelf -l a out | grep ':lib'
```

不应该有错误，且最后一个命令的输出将是（考虑到动态链接器名称的平台特定差异）：

> [Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]

关于 64 位系统的说明：`/lib` 是我们动态链接器的位置，但它是通过 `lib64` 中的符号链接访问的。

> 注意
> 在 32 位系统上，解释器应为 `/lib/ld-linux.so.2`。

现在确保你已准备好使用启动文件：

```bash
grep -o '/usr/lib.*/crt[lin].*s' dummy.c
```

上一个命令的输出应该是：

```
/usr/lib/../../crt1.o succeeded
/usr/lib/../../crt.o succeeded
/usr/lib/../../crtn.o succeeded
```

验证编译器正在搜索正确的头文件：

```bash
grep -B1 '^ /usr/include' dummy.log
```

此命令应返回以下输出：

```
#include <...> search starts here:
/usr/include
```

接下来，验证链接器是否使用了正确的搜索路径：

```bash
grep 'SEARCH.*/usr/lib' dummy.log | sed 's|;\n|g'
```

包含 `-linux-gnu` 组件的路径引用应该被忽略，否则上一个命令的输出应该是：

```
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/lib")
```

接下来确保我们使用的是正确的 `libc`：

```bash
grep "/lib*/libc.so.6 " dummy.log
```

上一个命令的输出应该是：

```
attempt to open /lib/libc.so.6
```

最后，确保我们使用的是正确的动态链接器：

```bash
grep "/lib*/libc.so.6 " dummy.log
```

最后一个命令的输出应该是：

```
attempt to open /lib/libc.so.6
```

## make 参数的含义

`tooldir=/usr`

通常情况下，`tooldir`（可执行文件最终将所在的目录）被设置为 `$(exec_prefix)/$(target_alias)`。例如，`x86_64` 机器会将其扩展为 `/usr/x86_64-unknown-linux-gnu`。由于这是一个自定义系统，不需要 `/usr` 下这个特定于目标的目录。`$(exec_prefix) / $(target_alias)` 将用于交叉编译（例如，在 Intel 机器上编译一个包，并生成一个可以在 PowerPC 机器上执行的代码）。

> 重要提示
> 本节中 Binutils 的测试套件被认为是至关重要的。在任何情况下都请勿跳过它。

测试结果：

```bash
make -k check
```

安装包：

```bash
make tooldir=/usr install
```

## 6.13.2. Binutils 目录

- **已安装的程序：** `addr2line`, `ar`, `as`, `c++filt`, `elfedit`, `gprof`, `ld`, `bfd`, `nm`, `objdump`, `ranlib`, `size`, `strings` 和 `strip`
- **已安装的库：** `libbfd.{a,so}` 和 `libcodes.{a,so}`
- **已安装的目录：** `/usr/lib/ldscripts`

## 概要说明

- **addr2line** 将地址转换为文件名和行号；给定一个地址和一个可执行文件的名称，它使用可执行文件中的调试信息来确定与地址相关的源文件和行号
- **ar** 创建、修改和从归档中提取内容
- **as** 汇编器，将 `gcc` 的输出汇编成目标文件
- **c++filt** 链接器用于反修饰 C++ 和 Java 符号，并防止重载函数导致崩溃
- **elfedit** 更新 ELF 文件的 ELF 头部
- **gprof** 显示调用图剖析数据
- **ld** 链接器，将多个目标文件和归档文件合并成单个文件，重定位它们的数据并连接符号引用
- **bfd** 将 `ld` 硬链接到 `ld`
- **nm** 列出给定目标文件中出现的符号
- **objcopy** 将一种类型的目标文件转换为另一种
- **objdump** 显示有关给定目标文件的信息，可以通过选项控制要显示的特定信息；显示的信息对于开发编译工具的程序员非常有用
- **ranlib** 生成归档内容的索引并将其存储在归档中；该索引列出了由归档成员（可重定位目标文件）定义的所有符号
- **readelf** 显示有关 ELF 类型二进制文件的信息
- **size** 列出给定目标文件的段大小和总大小
- **strings** 对于每个给定文件，输出至少达到指定长度（默认为四）的可打印字符序列；对于目标文件，默认只打印初始化和加载部分中的字符串，而对于其他类型的文件，它会扫描整个文件
- **strip** 丢弃目标文件中的符号
- **libbfd** 二进制文件描述符库
- **libopcodes** 一个用于操作码的库——即处理器指令的“可读文本”版本；它用于构建如 `objdump` 类的工具

## 6.14. GMP-6.1.2

GMP 包包含数学库。这些实用的函数为任意精度算术运算提供了支持。

**估算编译时间：** 1.3 SBU
**所需磁盘空间：** 59 MB

### 6.14.1. GMP 的安装

> 注意
> 如果你为 32 位 `x86` 编译，但你的 CPU 能够运行 64 位代码且你在环境中指定了 `CFLAGS`，则配置脚本将尝试为 64 位配置并失败。通过以下调用 `configure` 命令可以避免这种情况：
```
ABI=32 ./configure ...
```

为编译准备 GMP：

```
./configure --prefix=/usr \
    --enable-cxx \
    --disable-static \
    --docdir=/usr/share/doc/gmp-6.1.2
```

新配置选项的含义：

- `--enable-cxx` 此参数启用 C++ 支持
- `--docdir=/usr/share/doc/gmp-6.1.2` 此变量指定文档的正确位置。

编译包并生成 HTML 文档：

```
make
make html
```

> 重要提示
> 本节中 GMP 的测试套件被认为是至关重要的。在任何情况下都请勿跳过它。

测试结果：

```
make check 2>&1 | tee gmp-check-log
```

> 注意
> `gmp` 中的代码针对构建它的处理器进行了高度优化。偶尔，该代码会误判系统能力，导致测试或其他使用 `gmp` 库的应用程序中出现错误，并提示“Illegal instruction”（非法指令）。在这种情况下，应该使用 `--build=x86_64-unknown-linux-gnu` 选项重新配置 `gmp` 并重新构建。

确保测试套件中的所有 190 项测试均通过。通过执行以下命令检查结果：

```
awk '/# PASS:/{total+3} ; END{print total}' gmp-check-log
```

安装包及其文档：

```
make install
make install-html
```

### 6.14.2. GMP 目录

**已安装的库：** `libgmp.so` `libgmpxx.so`
**已安装的目录：** `/usr/share/doc/gmp-6.1.2`

## 概要说明

- `libgmp` 包含精度函数
- `libgmpxx` 包含 C++ 函数

## 6.15. MPFR-3.1.2

MPFR 包包含多精度函数。

**估算编译时间：** 0.8 SBU
**所需磁盘空间：** 45 MB

### 6.15.1. MPFR 的安装

为编译准备 MPFR：



```
./configure --prefix=/usr \
    --disable-static \
    --enable-thread-safe \
    --docdir=/usr/share/doc/mpfr-3.1.2
```

编译包并生成 HTML 文档：

```
make
make html
```

> 重要提示
>
> 本节中 MPFR 的测试套件被认为是至关重要的。在任何情况下都请勿跳过它。

测试结果：

```
make check
```

安装包及其文档：

```
make install
make install-html
```

## 6.15.2. MPFR 目录

**已安装的库：** `libmpfr.so`
**已安装的目录：** `/usr/share/doc/mpfr-3.1.2`

## 概要说明

- `libmpfr` 包含多精度函数

## 6.16. MPC-1.0.3

MPC 包包含一个具有任意高精度和正确舍数的库。
**估算编译时间：** 0.3 SBU
**所需磁盘空间：** 17 MB

## 6.16.1. MPC 的安装

为编译准备 MPC：

```
./configure --prefix=/usr \
    --disable-static \
    --docdir=/usr/share/doc/mpc-1.0.3
```

编译包并生成 HTML 文档：

```
make
make html
```

执行以下命令测试结果：

```
make check
```

安装包及其文档：

```
make install
make install-html
```

## 6.16.2. MPC 目录

**已安装的库：** `libmpc.so`
**已安装的目录：** `/usr/share/doc/mpc-1.0.3`

## 概要说明

- `libmpc` 包含复函数

## 6.17. GCC-6.3.0

GCC 包包含 GNU 编译器集合，包括 C 和 C++ 编译器。

**估算编译时间：** 82 SBU（带测试）
**所需磁盘空间：** 3.3 GB

## 6.17.1. GCC 的安装

如果是为 x86_64 编译，将 64 位库的默认目录更改为 "lib"：

```
case $(uname -m) in
x86_64)
  sed -e '/m64/s/lib64/lib/' \
  -i.orig gcc/config/i386/t-linux64
esac
```

GCC 文档建议在独立的目录中编译：

```
mkdir -v build
cd build
```

为编译准备 GCC：

注意对于其他语言，缺少某些先决条件。参见如何构建 GCC 支持的所有语言。

新配置参数的含义：

```
SED=sed
```

设置此环境变量可以防止硬编码路径到 `/tools/bin/`。

`--with-system-zlib`

这将切换 GCC 连接到系统安装的 Zlib 库，而不是其内部副本。

编译包：

```
make
```

> 重要提示
> 本节中，GCC 的测试套件被认为是至关重要的。在任何情况下都请勿跳过它。

GCC 测试套件中的一个测试已知会耗尽栈，因此在运行测试之前请增加栈大小：

```
ulimit -s 32768
```

测试结果，但不要因错误停止：

```
make -k check
```

要获取测试套件结果的摘要，请运行：

```
../contrib/test_summary
```

如果只需要摘要，将输出通过给 `grep -A7 Summ`。

可以将结果与位于 `http://www.linuxfromscratch.org/lfs/build-logs/8.0/` 和 `http://gcc.gnu/org/ml/gcc-testresults` 处的资源进行比较。

一些意料之外的失败是无法避免的。GCC 开发者通常知晓这些问题，但尚未解决它们。特别是 `libstdcc++` 测试套件中的少数测试用例在像我们这里这样以 root 用户身份运行时，可能会失败。除非测试结果与上述 URL 中的结果差异巨大，否则可以安全地继续。

安装包：

```
make install
```

出于“历史”原因，创建一个 FHS 要求的符号链接。

```
ln -sv ../usr/bin/cpp /lib
```

许多包使用 `cc` 名称来调用编译器（Compiler）。为了满足这些包的需求，创建一个符号链接：

```
ln -sv gcc /usr/bin/cc
```

添加兼容性符号链接以启用支持链接时优化（LTO）的程序：

```
install -v --dm75 /usr/lib/bfd-plugins
ln -sf ../../libexec/gcc/$(gcc --dumpmachine)/6.3.0/liblto_plugin.so \
/usr/lib/bfd-plugins
```

现在一切已准备就绪，确保编译和链接按预期工作至关重要。我们通过执行在本章早期进行过的相同的完整性检查来实现：

```
echo 'int main()' > dummy.c
cc dummy.c -v -Wl,--verbose 2> dummy.log
read -l a.out | grep ': ':lib'
```

不应该有错误，且最后一个命令的输出将显示（考虑到动态链接器名称的平台特定平台差异）：

```
[Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
```

现在确保我们已设置为使用正确的启动文件：

```bash
grep -o '/usr/lib.* /crt[lin].*' dummy.log
```

最后一个命令的输出应该显示：

```
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0../../../../lib/crt1.o succeeded
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0../../../../lib/crti.o succeeded
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0../../../../lib/crtn.o succeeded
```

根据你的机器架构，上述可能略有不同，区别通常在于 `/usr/lib/gcc` 之后的目录名称。这里需要寻找的是 gcc 是否已经在 `/usr/lib` 目录下找到了所有三个 `crt*.o` 文件。

验证编译器是否正在搜索正确的头文件：

```
grep -B4 '^ /usr/include' dummy
```

此命令应返回以下输出：

```
#include <...> search starts here:
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0/include
/usr/local/include
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0/include-fixed
/usr/include
```

再次注意，以三元组（triplet）命名的目录可能与上述不同，取决于你的架构。

> 从 4.3.0 版本开始，GCC 现在无条件地将 `limits.h` 文件安装到私有的 `include-fixed` 目录，并且该目录必须存在。

接下来，验证链接器是否使用了正确的路径：

```
grep 'SEARCH\*/usr/lib' dummy.log | sed '\s|;\n|g'
```

包含 'linux-gnu' 组件的路径引用应该被忽略，但否则最后一个命令的输出应为：

```
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib64")
SEARCH_DIR("/usr/local/lib64")
SEARCH_DIR("/usr/lib64")
SEARCH_DIR("/usr/lib64")
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/usr/lib")
```

32 位系统可能有几个不同的目录。例如，这里是 i86 机器的输出：

```
SEARCH_DIR("/usr/i686-pc-linux-gnu/lib32")
SEARCH_DIR("/usr/local/lib32")
SEARCH_DIR("/usr/lib32")
SEARCH_DIR("/usr/lib32")
SEARCH_DIR("/usr/i686-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/usr/lib")
```



接下来确保我们正在使用正确的 lib：

```
grep "/lib.*/libc.so.6 " dummy.log
```

最后一个命令的输出应该是：

```
attempt to open /lib/libc.so.6 succeeded
```

最后，确保 GCC 正在使用正确的动态链接器：

```
gcc found dummy.log
```

最后一个命令的输出应该是（考虑到动态链接器的平台特定差异）：

```
found ld-linux-x86-64.so.2 at /lib64/ld-linux-x86-64.so.2
```

如果输出与上述不匹配或完全没有收到，则说明出了问题。调查步骤以找到问题所在并进行纠正。最可能的原因是 `spec` 文件出了问题。如果一切运行正常，则请运行测试：

```
make -k check
```

最后，移动一个放置错误的文件：

```
mkdir -p /usr/share/gdb/auto-load/usr/lib
mv -v *.so /usr/share/gdb/auto-load/usr/lib
```

## 6.17 GCC 的内容

- 安装的程序：`c++`, `cc`（链接到 `gcc`），`cpp`, `g++`, `gcc-ar`, `gcc-nm`, `gcc-ranlib`, `gcov`
- 安装的库：`libasan.so`, `libatomic.so`, `libgcc.a`, `libgcc_eh.a`, `libgcc.so`, `libgcov.a`, `libomp.so`, `liberty.a`, `libstdc++.a`
- 安装的目录：`/include-fixed`, `/lib/bfd-plugins`, `/usr/bin/cc`, `/usr/lib/bfd-plugins`, `/usr/lib/gcc/$(gcc --dumpmachine)/6.3.0/liblto_plugin.so`

现在一切已准备就绪，确保编译和链接按预期工作至关重要。我们通过执行在本章早期进行过的相同的完整性检查来实现：

```
echo 'int main()' > dummy.c
cc dummy.c -v -Wl,--verbose 2> dummy.log
read -l a.out | grep ': ':lib'
```

不应该有错误，且最后一个命令的输出将显示（考虑到平台特定平台名称差异）：

```
[Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
```

现在确保我们已设置为使用正确的启动文件：

```
grep -o '/usr/lib.* /crt[lin].*' dummy.log
```

最后一个命令的输出应该显示：

```
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0../../../../lib/crt1.o succeeded
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0../../../../lib/crti.o succeeded
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0../../../../lib/crtn.o succeeded
```

根据你的机器架构，上述可能略有不同，区别通常在于 `/usr/lib/gcc` 之后的目录名称。这里需要寻找的是 `gcc` 是否已经在 `/usr/lib` 目录下找到了所有三个 `crt*.o` 文件。

验证编译器是否正在搜索正确的头文件：

```
grep -B4 '^ /usr/include' dummy
```

此命令应返回以下输出：

```
#include <...> search starts here:
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0/include
/usr/local/include
/usr/lib/gcc/x86_64-pc-linux-gnu/6.3.0/include-fixed
/usr/include
```

再次注意，以三元组（triplet）命名的目录可能与上述不同，取决于你的架构。

> 从 4.3.0 版本开始，GCC 现在无条件地将 `limits.h` 文件安装到私有的 `include-fixed` 目录，并且该目录必须存在。

接下来，验证链接器是否使用了正确的路径：

```
grep 'SEARCH\*/usr/lib' dummy.log | sed '\s|;\n|g'
```

包含 'linux-gnu' 组件的路径引用应该被忽略，但否则最后一个命令的输出应为：

```
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib64")
SEARCH_DIR("/usr/local/lib64")
SEARCH_DIR("/usr/lib64")
SEARCH_DIR("/usr/lib64")
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/usr/lib")
```

32 位系统可能有几个不同的目录。例如，这里是 i86 机器的输出：

```
SEARCH_DIR("/usr/i686-pc-linux-gnu/lib32")
SEARCH_DIR("/usr/local/lib32")
SEARCH_DIR("/usr/lib32")
SEARCH_DIR("/usr/lib32")
SEARCH_DIR("/usr/i686-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/usr/lib")
```

接下来确保我们正在使用正确的 lib：

```
grep "/lib.*/libc.so.6 " dummy.log
```

最后一个命令的输出应该是：

```
attempt to open /lib/libc.so.6 succeeded
```

最后，确保 GCC 正在使用正确的动态链接器：

```
gcc found dummy.log
```

最后一个命令的输出应该是（考虑到动态链接器的平台特定差异）：

```
found ld-linux-x86-64.so.2 at /lib64/ld-linux-x86-64.so.2
```

如果输出与上述不匹配或完全没有收到，则说明出了问题。调查步骤以找到问题所在并进行纠正。最可能的原因是 `spec` 文件出了问题。如果一切运行正常，则请运行测试：

```
make -k check
```

最后，移动一个放置错误的文件：

```
mkdir -p /usr/share/gdb/auto-load/usr/lib
mv -v *.so /usr/share/gdb/auto-load/usr/lib
```

## 6.17 Bzip2 的内容

- 安装的程序：`c++`, `cc`（链接到 `gcc`），`cpp`, `g++`, `gcc-ar`, `gcc-nm`, `gcc-ranlib`, `gcov`
- 安装的库：`libasan.so`, `libatomic.so`, `libgcc.a`, `libgcc_eh.a`, `libgcc.so`, `libgcov.a`, `libomp.so`, `liberty.a`, `libstdc++.a`
- 安装的目录：`/include-fixed`, `/lib/bfd-plugins`, `/usr/bin/cc`, `/usr/lib/bfd-plugins`, `/usr/lib/gcc/$(gcc --dumpmachine)/6.3.0/liblto_plugin.so`

### 18.1 Bzip2 的安装

Bzip2 包包含了用于压缩和解压缩程序的。使用 `bzip2` 压缩文件比传统的 `gzip` 具有更高的压缩率。

近似构建时间：少于 0.1 秒   所需的磁盘空间：0.9 MB

应用一个补丁以安装此包的文档：

```
patch -Np1 -i ../bzip2-1.6-install_docs.patch
```

以下命令确保符号链接是相对路径：

```
sed -i 's@(ln -ns \)\$(PREFIX)/bin/\1@' Makefile
```

确保手册安装在正确的位置：

```
sed -i "s@ $(PREFIX)/man@$(PREFIX)/share/man@" Makefile
```

准备 Bzip2 进行编译：

```
make -f Makefile-libbz2_so
make clean
```

`make` 参数的含义：

```
-f Makefile-libbz2_so
```



这将导致 Bzip2 使用不同的 Makefile，在这里是 `Makefile-libbz2_so`，它创建了一个动态 `libbz2.so` 库并将 Bzip2 工具链接到其上。

编译包：

```
make
```

安装程序：

```
make PREFIX=/usr install
```

将共享的 bzip2 二进制文件安装到 `/bin` 目录，创建必要的符号链接并清理：

```
cp -v bzip2-shared /bin/bzip2

cp -av libbz2.so* /lib

ln -sv ../../lib/libbz2.so.1.0 /usr/lib/libbz2

rm -v /usr/bin/(bzip2,bzcat,bzip2)

ln -sv bzip2 /bin/bzip2

ln -sv bzip2 /bin/bzcat
```

### 6.18.2 Bzip2 的内容

- 安装的程序：`bzip2`（链接到 `bzip2`），`bzcat`（链接到 `bzdiff`），`bdiff`, `bzgrep`（链接到 `bzgrep`），`bzfgrep`（链接到 `bzgrep`），`bzgrep`, `bzip2`, `bzip2recover`, `bz`（链接到 `bmore`），和 `bmore`
- 安装的库：`libbz2.[a,so]`
- 安装的目录：`/usr/share/doc/bzip2-1.0.6`

## 简述

`bunzip2` 解压 bzipped 文件

`bzcat` 将 bzipped 文件解压到标准输出

`bzcmp` 在 bzipped 文件上运行 `cmp`

`bzdiff` 在 bzipped 文件上运行 `diff`

`bzegrep` 在 bzipped 文件上运行 `egrep`

`bzfgrep` 在 bzipped 文件上运行 `fgrep`

`bzgrep` 在 bzipped 文件上运行 `grep`

`bzip2` 使用带有霍夫编码的 Burrows-Wheeler 块文本压缩算法对文件压缩；其压缩率优于使用“Lempel-Ziv”算法的更传统的压缩器，例如 `gzip`

`bzip2recover` 尝试从损坏的 bzipped 文件中恢复数据

`bzless` 在 bzipped 文件上运行 `less`

`bzmore` 在 bzipped 文件上运行 `more`

`libbz2` 使用 Burrows-Wheeler 算法实现无损块排序数据压缩的库

## 6.19. Pkg-config-0.29.1

Pkg-config 包包含一个工具，用于在配置和 make 文件执行期间向构建工具传递包含路径和/或库路径。

预计构建时间：0.4 SBU
所需空间：28 MB

### 6.19.1. 安装 Pkg-config

为编译准备 Pkg-config：

```
./configure --prefix=/usr \
  --with-internal-glib \
  --disable-compile-warnings \
  --disable-host-tool \
  --docdir=/usr/share/doc/pkg-config-0.29.1
```

新配置选项的含义：

- `--with-internal-glib`
这将允许 pkg-config 使用其内部版本的 Glib，因为 LFS 中不可用外部版本。

- `--disable-compile-warnings`
此选项防止构建系统在使用 GCC 6 编译时使用可能导致构建失败的编译器标记。

- `--disable-host-tool`
此选项禁用对 pkg-config 程序创建不必要的硬链接。

编译包：

```
make
```

测试结果，请执行：

```
make check
```

安装包：

```
make install
```

### 6.19.2. Pkg-config 的内容

| 安装的程序： | `pkg-config` |
| 安装目录： | `/usr/share/doc/pkg-config-0.29.1` |

简述

`pkg-config` 为指定的库或包返回元信息

## 6.20. Ncurses-6.0

Ncurses 包包含用于处理终端无关的字符屏幕的库。
预计构建时间：0.4 SBU
所需空间：39 MB

### 6.20.1. 安装 Ncurses

不要安装未由 configure 处理的静态库：

```
sed -i '/LIBTOOL_INSTALL/d' c++/Makefile.file
```

为编译准备 Ncurses：

```
./configure --prefix=/usr \
  --withmandir=/usr/share/man \
  --with-shared \
  --without-debug \
  --without-normal \
  --enable-pc-files \
  --enable-wide
```

新配置选项的含义：

- `--enable-wide`
这将切换为构建宽字符库（例如 `libncursesw.so.6.0`）而不是普通库（例如 `libncurses.so.6.0`）。这些宽字符库可以在多字节和传统的 8 位本地环境中中使用，而普通库在 8 位本地环境中正常工作。宽字符库和普通库是源码兼容的，但不是二进制兼容的。
- `--enable-pc-files`
此开关为 pkg-config 生成并安装 `.pc` 文件。
- `--without-normal`
此开关将禁用大部分静态库的构建和安装。

编译包：

```
make
```

该包有一个测试套件，但它在包安装后才能运行。测试位于 `test/` 目录。更多细节请参阅该目录下的 README 文件。

安装包：

```
make install
```

将共享库移动到 `/lib` 目录，这是它们预期的所在地：

```
mv -v /usr/lib/libncursesw.so* /lib
```

由于库已被移动，一个符号链接指向一个不存在的文件。重新创建它：

```
ln -sfv ../../lib/$(readlink /usr/lib/libncursesw.so) /usr/lib/libncurses.so
```

许多应用程序期望链接器能够找到非宽字符的 Ncurses 库。通过符号链接和链接器脚本欺骗此类应用程序链接宽字符库：

```
for lib ncurses menu; do
  rm -vf /usr/lib/lib${lib}.so
  echo "INPUT-${lib}w" > /usr/lib/lib${lib}.so
  ln -sf ${lib}w.pc /usr/lib/pkgconfig/${lib}.pc
done
```

最后，确保在构建时使用 `-lcurses` 的旧应用程序是可构建的：

```
rm -vf /usr/lib/libcurses.so
echo "INPUT-(ncursesw)" > /usr/lib/libcurses.so
```

如果需要，安装文档：

```
mkdir -p /usr/share/doc/ncurses
cp -r doc/* /usr/share/doc/ncurses
```

Linux From Scratch - 版本 8.0

许多应用程序期望链接器能够找到非宽字符的 Ncurses 库。通过符号链接和链接器脚本欺骗此类应用程序链接宽字符库：

最后，确保在构建时使用 `-lcurses` 的旧应用程序是可构建的：

`libattr` 包含了用于操作扩展属性的库函数

## 22. Acl-2.2.52

Acl 包包含了用于管理访问控制列表（Access Control Lists）的实用程序，这些列表用于为文件和目录定义更细粒度的裁量访问权限。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.8 MB

### 22.2.1. 安装 Acl

修改修改目录使其成为一个版本化目录：

```
sed -i -e 's|/@pkg_name@|@pkg_version@|' include/builddefs.in
```

修复一些损坏的用例：

```
sed -i " :; sed.*:*" test/(sbits-restore,cp,misc).test
```

此外，修复一个导致 `getfacl` 在处理组名过长时发生段错误的 bug：

```
sed -i -e "/TABS-1/a (x > (TABS-1)) x = (TABS-1);" "\nlibacl/__acl_to_any_text.c
```

为编译 Acl 准备：

```
./configure --prefix=/usr \
  --bindir=/bin \
  --disable-static \
  --libexecdir=/usr/lib
```

编译包：

```
make
```



Acl 的用例需要在支持访问控制的文件系统上运行，或者在构建 Coreutils 时已链接了 Acl 库。如果需要，可以在在本章后续构建完 Coreutils 后，返回此包并运行 `make -jl tests`。

安装包：

```
make install install-dev install-lib

chmod -v 755 /usr/lib/libacl.so
```

共享库需要移动到 `/lib`，结果是 `/usr/lib` 中的 `.so` 文件需要重新创建：

```
mv -v /usr/lib/libacl.so.* /lib

ln -sf /usr/lib/$(readlink /usr/lib/libacl.so) /usr/lib/libacl
```

## 22.2.2. Acl 的内容

- 已安装的程序：`chacl`, `getfacl`, 和 `setacl`
- 已安装的库：`libacl.so`
- 已安装的目录：`/usr/include/acld` 和 `/usr/share/doc/accl-2.2.52`

## 简述

- `chacl` 修改文件或目录的访问控制列表
- `getfacl` 获取文件访问控制列表
- `setacl` 设置文件访问控制列表
- `libacl` 包含了用于操作访问控制列表的库函数

## 23. Libcap-2.25

`Libcap` 包实现了 Linux 内核中可用的 POSIX 1003.1le 能力（capabilities）的用户空间接口。这些能力将所有强大的 root 权限划分为一组不同的权限。

**预计编译时间：** 少于 0.1 SBU
**所需磁盘空间：** 1.3 MB

### 6.23.1. 安装 Libcap

防止安装静态库：

```
sed -i '/install.*STALENAME/d' libcap/Makefile
```

编译包：

```
make
```

此包不附带测试套件。

安装包：

```
make RAISE_SETCAP=no lib=lib prefix=/usr install

chmod -v 755 /usr/lib/libcap.so
```

`make` 选项的含义：

> `RAISE_SETCAP=no`
此参数跳过尝试对自身使用 `setcap`。如果内核或文件系统不支持扩展能力，这可以避免安装错误。

> `lib=lib`
此参数将库安装在 `$prefix/lib` 中，而不是 x86_64 架构下的 `$prefix/lib64`。它对 x86 架构没有影响。

共享库被移动到 `/lib`，结果是 `/usr/lib/libcap` 中的 `.so` 文件将不会被重新创建。

```
mv -v /usr/lib/libcap.so.* /lib

ln -sfv ../lib$(readlink /usr/lib/libcap.so) /usr/lib/libcap.so
```

## 6.23.2. Libcap 的内容

- 已安装的程序：`capsh`, `getcap`, `getpcaps`, 和 `setcap`
- 已安装的库：`libcap`

## 简述

- `capsh`: 用于探索和限制能力支持的 shell 封装
- `getcap`: 检查文件能力
- `getpcaps`: 显示查询进程上的能力
- `libcap`: 包含了用于操作 POSIX 1003.1le 能力的库函数
- `setcap`: 设置文件能力

## 6.24. Sed-4.4

`Sed` 包包含一个流编辑器。

**预计编译时间：** 0.3 SBU
所需磁盘空间：25 MB

### 6.24.1. 安装 Sed

首先修复 LFS 环境中的一个问题并移除一个失败的测试用例：

```
sed -i '/s/usr/tools/'      build-aux/help2man

sed -i '/s/panic-tests.//' Makefile.in
```

为编译 `Sed` 准备：

```
./configure --prefix=/usr --bindir=/bin
```

编译包并生成 HTML 文档：

```
make

make html
```

要测试结果，执行：

```
make check
```

安装包及其文档：

```
make install

install -d -m755 /usr/share/doc/sed-4.4

install -m644 doc/sed.html /usr/share/doc/sed-4.4
```

## 6.24.2. Sed 的内容

- 已安装的程序：`sed`
- 已安装的目录：`/usr/share/doc/sed-4.4`

## 简述

- `sed` 单次通过过滤和转换文本文件

## 6.25. Shadow-4.4

`Shadow` 包包含了以安全方式处理密码的程序。

**预计编译时间：** 0.2 SBU
所需磁盘空间：2 MB

### 6.25.1. 安装 Shadow

> 如果你想强制使用强密码，请在构建 `Shadow` 之前参考 http://www.linuxfromscratch.org/view/posts/cracklib.html。然后在在 `configure` 命令中添加 `--with-libcrack`。

禁用组及其手动帮助页的安装，Coreutils 提供了更好的版本。同时防止安装已经安装过的手动帮助页：

```
sed -i 's/groups//' src/Makefile.in

find -name Makefile.in -exec sed -i 's/groups / /' \;

find -name Makefile.in -exec sed -i 's/groups / /' \;

find -name Makefile.in -exec sed -i 's/groups / /' \;
```



libattr 包含了用于操作扩展属性的库函数

## 22. Acl-2.2.52

Acl 包包含了用于管理访问控制列表（Access Control Lists）的实用程序，这些列表用于为文件和目录定义更细粒度的裁量访问权限。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.8 MB

### 22.2.1. 安装 Acl

修改修改目录使其成为一个版本化目录：

```
sed -i -e 's|/@pkg_name@|@pkg_version@|' include/builddefs.in
```

修复一些损坏的测试用例：

```
sed -i " :; sed.*:*" test/(sbits-restore,cp,misc).test
```

此外，修复一个导致 `getfacl` 在处理组名过长时发生段错误的 bug：

```
sed -i -e "/TABS-1/a (x > (TABS-1)) x = (TABS-1);" "\nlibacl/__acl_to_any_text.c
```

为编译 Acl 准备：

```
./configure --prefix=/usr \
  --bindir=/bin \
  --disable-static \
  --libexecdir=/usr/lib
```

编译包：

```
make
```

Acl 的用例需要在支持访问控制的文件系统上运行，或者在构建 Coreutils 时已链接了 Acl 库。如果需要，可以在在本章后续构建完 Coreutils 后，返回此包并运行 `make -jl tests`。

安装包：

```
make install install-dev install-lib
chmod -v 755 /usr/lib/libacl.so
```

共享库需要移动到 `/lib`，结果是 `/usr/lib` 中的 `.so` 文件需要重新创建：

```
mv -v /usr/lib/libacl.so.* /lib
ln -sf /usr/lib/$(readlink /usr/lib/libacl.so) /usr/lib/libacl
```

### 22.2.2. Acl 的内容

- 已安装的程序：`chacl`, `getfacl`, 和 `setacl`
- 已安装的库：`libacl.so`
- 已安装的目录：`/usr/include/acld` 和 `/usr/share/doc/accl-2.2.52`

## 简述

- **chacl** 修改文件或目录的访问控制列表
- **getfacl** 获取文件访问控制列表
- **setacl** 设置文件访问控制列表
- **libacl** 包含了用于操作访问控制列表的库函数

## 23. Libcap-2.25

Libcap 包实现了 Linux 内核中可用的 POSIX 1003.1le 能力（capabilities）的用户空间接口。这些能力将所有强大的 root 权限划分为一组不同的权限。

**预计编译时间：** 少于 0.1 SBU
**所需磁盘空间：** 1.3 MB

### 6.23.1. 安装 Libcap

防止安装静态库：

```
sed -i '/install.*STALENAME/d' libcap/Makefile
```

编译包：

```
make
```

此包不附带测试套件。

安装包：

```
make RAISE_SETCAP=no lib=lib prefix=/usr install
chmod -v 755 /usr/lib/libcap.so
```

`make` 选项的含义：

> `RAISE_SETCAP=no`
此参数跳过尝试对自身使用 `setcap`。如果内核或文件系统不支持扩展能力，这可以避免安装错误。

> `lib=lib`
此参数将库安装在 `$prefix/lib` 中，而不是 x86_64 架构下的 `$prefix/lib64`。它对 x86 架构没有影响。

共享库被移动到 `/lib`，结果是 `/usr/lib/libcap` 中的 `.so` 文件将不会被重新创建。

```
mv -v /usr/lib/libcap.so.* /lib
ln -sfv ../lib$(readlink /usr/lib/libcap.so) /usr/lib/libcap.so
```

### 6.23.2. Libcap 的内容

- 已安装的程序：`capsh`, `getcap`, `getpcaps`, 和 `setcap`
- 已安装的库：`libcap`

## 简述

- `capsh`: 用于探索和限制能力支持的 shell 封装
- `getcap`: 检查文件能力
- `getpcaps`: 显示查询进程上的能力
- `libcap`: 包含了用于操作 POSIX 1003.1le 能力的库函数
- `setcap`: 设置文件能力

## 6.24. Sed-4.4

Sed 包包含一个流编辑器。

**预计编译时间：** 0.3 SBU
所需磁盘空间：25 MB

### 6.24.1. 安装 Sed

首先修复 LFS 环境中的一个问题并移除一个失败的测试用例：

```
sed -i '/s/usr/tools/'      build-aux/help2man
sed -i '/s/panic-tests.//' Makefile.in
```

为编译 Sed 准备：

```
./configure --prefix=/usr --bindir=/bin
```

编译包并生成 HTML 文档：

```
make
make html
```

要测试结果，执行：

```
make check
```

安装包及其文档：

```
make install
```



`install -d -m755 /usr/share/doc/sed-4.4`

`install -m644 doc/sed.html /usr/share/doc/sed-4.4`

## 6.24.2. Sed 的内容

- 已安装的程序：`sed`
- 已安装的目录：`/usr/share/doc/sed-4.4`

## 简述

- `sed` 单次通过过滤和转换文本文件

## 6.25. Shadow-4.4

Shadow 包包含了以安全方式处理密码的程序。

**预计编译时间：0.2 SBU**
**所需磁盘空间：2 MB**

### 6.25.1. 安装 Shadow

> 如果你想强制使用强密码，请在构建 Shadow 之前参考 http://www.linuxfromscratch.org/view/posts/cracklib.html。然后在在 `configure` 命令中添加 `--with-libcrack`。

禁用组及其手动帮助页的安装，Coreutils 提供了更好的版本。同时防止安装已经安装过的手动帮助页：

```
sed -i 's/groups//' src/Makefile.in

find -name Makefile.in -exec sed -i 's/groups / /' \;
```



`make install`

`install -d -m755 /usr/share/doc/sed-4.4`

`install -m644 doc/sed.html /usr/share/doc/sed-4.4`

### 6.24.2. Sed 的内容

- 已安装的程序：`sed`
- 已安装的目录：`/usr/share/doc/sed-4.4`

## 简述

- `sed` 单次通过过滤和转换文本文件

## 6.25. Shadow-4.4

`Shadow` 包包含了以安全方式处理密码的程序。

**预计编译时间：0.2 SBU**
**所需磁盘空间：2 MB**

### 6.25.1. 安装 Shadow

> 如果你想强制使用强密码，请在构建 `Shadow` 之前参考 http://www.linuxfromscratch.org/view/posts/cracklib.html。然后在在 `configure` 命令中添加 `--with-libcrack`。

禁用组及其手动帮助页的安装，`Coreutils` 提供了更好的版本。同时防止安装已经安装过的手动帮助页：

```
sed -i 's/groups//' src/Makefile.in

find -name Makefile.in -exec sed -i 's/groups / /' \;
```

libattr 包含了用于操作扩展属性的库函数

## 22. Acl-2.2.52

`Acl` 包包含了用于管理访问控制列表（Access Control Lists）的实用程序，这些列表用于为文件和目录定义更细粒度的裁量访问权限。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.8 MB

### 22.2.1. 安装 Acl

修改修改目录使其成为一个版本化目录：

```
sed -i -e 's|/@pkg_name@|@pkg_version@|' include/builddefs.in
```

修复一些损坏的测试用例：

```
sed -i " :; sed.*:*" test/(sbits-restore,cp,misc).test
```

此外，修复一个导致 `getfacl` 在处理组名过长时发生段错误的 bug：

```
sed -i -e "/TABS-1/a (x > (TABS-1)) x = (TABS-1);" "\nlibacl/__acl_to_any_text.c
```

为编译 `Acl` 准备：

```
./configure --prefix=/usr \
  --bindir=/bin \
  --disable-static \
  --libexecdir=/usr/lib
```

编译包：

```
make
```

`Acl` 的用例需要在支持访问控制的文件系统上运行，或者在构建 `Coreutils` 时已链接了 `Acl` 库。如果需要，可以在在本章后续构建完 `Coreutils` 后，返回此包并运行 `make -jl tests` 。

安装包：

```
make install install-dev install-lib

chmod -v 755 /usr/lib/libacl.so
```

共享库需要移动到 `/lib`，结果是 `/usr/lib` 中的 `.so` 文件需要重新创建：

```
mv -v /usr/lib/libacl.so.* /lib

ln -sf /usr/lib/$(readlink /usr/lib/libacl.so) /usr/lib/libacl
```

## 22.2.2. Acl 的内容

- 已安装的程序：`chacl`, `getfacl`, 和 `setacl`
- 已安装的库：`libacl.so`
- 已安装的目录：`/usr/include/acld` 和 `/usr/share/doc/accl-2.2.52`

## 简述

- **chacl** 修改文件或目录的访问控制列表
- **getfacl** 获取文件访问控制列表
- **setacl** 设置文件访问控制列表
- **libacl** 包含了用于操作访问控制列表的库函数

## 23. Libcap-2.25

`Libcap` 包实现了 Linux 内核中可用的 POSIX 1003.1le 能力（capabilities）的用户空间接口。这些能力将所有强大的 root 权限划分为一组不同的权限。

**预计编译时间：** 少于 0.1 SBU
**所需磁盘空间：** 1.3 MB

### 6.23.1. 安装 Libcap

防止安装静态库：

```
sed -i '/install.*STALENAME/d' libcap/Makefile
```

编译包：

```
make
```

此包不附带测试套件。

安装包：

```
make RAISE_SETCAP=no lib=lib prefix=/usr install

chmod -v 755 /usr/lib/libcap.so
```

`make` 选项的含义：

> `RAISE_SETCAP=no`
此参数跳过尝试对自身使用 `setcap`。如果内核或文件系统不支持扩展能力，这可以避免安装错误。

> `lib=lib`
此参数将库安装在 `$prefix/lib` 中，而不是 x86_64 架构下的 `$prefix/lib64`。它对 x86 架构没有影响。

共享库被移动到 `/lib`，结果是 `/usr/lib/libcap` 中的 `.so` 文件将不会被重新创建。

```
mv -v /usr/lib/libcap.so.* /lib

ln -sfv ../lib$(readlink /usr/lib/libcap.so) /usr/lib/libcap.so
```

## 6.23.2. Libcap 的内容

- 已安装的程序：`capsh`, `getcap`, `getpcaps`, 和 `setcap`
- 已安装的库：`libcap`

## 简述

- `capsh`: 用于探索和限制能力支持的 shell 封装
- `getcap`: 检查文件能力
- `getpcaps`: 显示查询进程上的能力
- `libcap`: 包含了用于操作 POSIX 1003.1le 能力的库函数
- `setcap`: 设置文件能力

## 6.24. Sed-4.4

`Sed` 包包含一个流编辑器。

**预计编译时间：** 0.3 SBU
所需磁盘空间：25 MB

### 6.24.1. 安装 Sed

首先修复 LFS 环境中的一个问题并移除一个失败的测试用例：

```
sed -i '/s/usr/tools/'      build-aux/help2man

sed -i '/s/panic-tests.//' Makefile.in
```

为编译 `Sed` 准备：

```
./configure --prefix=/usr --bindir=/bin
```

编译包并生成 HTML 文档：

```
make

make html
```

要测试结果，执行：

```
make check
```

安装包及其文档：

```
make install

install -d -m755 /usr/share/doc/sed-4.4

install -m644 doc/sed.html /usr/share/doc/sed-4.4
```

## 6.24.2. Sed 的内容

- 已安装的程序：`sed`
- 已安装的目录：`/usr/share/doc/sed-4.4`

## 简述

- `sed` 单次通过过滤和转换文本文件

## 6.25. Shadow-4.4

`Shadow` 包包含了以安全方式处理密码的程序。

**预计编译时间：0.2 SBU**
**所需磁盘空间：2 MB**

### 6.25.1. 安装 Shadow

> 如果你想强制使用强密码，请在构建 `Shadow` 之前参考 http://www.linuxfromscratch.org/view/posts/cracklib.html。然后在在 `configure` 命令中添加 `--with-libcrack`。

禁用组及其手动帮助页的安装，`Coreutils` 提供了更好的版本。同时防止安装已经安装过的手动帮助页：

```
sed -i 's/groups//' src/Makefile.in
```



libattr 包含了用于操作扩展属性的库函数

## 22. Acl-2.2.52

Acl 包包含了用于管理访问控制列表（Access Control Lists）的实用程序，这些列表用于为文件和目录定义更细粒度的裁量访问权限。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.8 MB

### 22.2.1. 安装 Acl

修改修改目录使其成为一个版本化目录：

```
sed -i -e 's|/@pkg_name@|@pkg_version@|' include/builddefs.in
```

修复一些损坏的测试用例：

```
sed -i " :; sed.*:*" test/(sbits-restore,cp,misc).test
```

此外，修复一个导致 `getfacl` 在处理组名过长时发生段错误的 bug：

```
sed -i -e "/TABS-1/a (x > (TABS-1)) x = (TABS-1);" "\nlibacl/__acl_to_any_text.c
```

为编译 Acl 准备：

```
./configure --prefix=/usr \
  --bindir=/bin \
  --disable-static \
  --libexecdir=/usr/lib
```

编译包：

```
make
```

Acl 的用例需要在支持访问控制的文件系统上运行，或者在构建 Coreutils 时已链接了 Acl 库。如果需要，可以在在本章后续构建完 Coreutils 后，返回此包并运行 `make -jl tests`。

安装包：

```
make install install-dev install-lib
chmod -v 755 /usr/lib/libacl.so
```

共享库需要移动到 `/lib`，结果是 `/usr/lib` 中的 `.so` 文件需要重新创建：

```
mv -v /usr/lib/libacl.so.* /lib
ln -sf /usr/lib/$(readlink /usr/lib/libacl.so) /usr/lib/libacl
```

### 22.2.2. Acl 的内容

- 已安装的程序：`chacl`, `getfacl`, 和 `setacl`
- 已安装的库：`libacl.so`
- 已安装的目录：`/usr/include/acld` 和 `/usr/share/doc/accl-2.2.52`

## 简述

- `chacl` 修改文件或目录的访问控制列表
- `getfacl` 获取文件访问控制列表
- `setacl` 设置文件访问控制列表
- `libacl` 包含了用于操作访问控制列表的库函数

## 23. Libcap-2.25

Libcap 包实现了 Linux 内核中可用的 POSIX 1003.1le 能力（capabilities）的用户空间接口。这些能力将所有强大的 root 权限划分为一组不同的权限。

**预计编译时间：** 少于 0.1 SBU
**所需磁盘空间：** 1.3 MB

### 6.23.1. 安装 Libcap

防止安装静态库：

```
sed -i '/install.*STALENAME/d' libcap/Makefile
```

编译包：

```
make
```

此包不附带测试套件。

安装包：

```
make RAISE_SETCAP=no lib=lib prefix=/usr install
chmod -v 755 /usr/lib/libcap.so
```

`make` 选项的含义：

> `RAISE_SETCAP=no`
此参数跳过尝试对自身使用 `setcap`。如果内核或文件系统不支持扩展能力，这可以避免安装错误。

> `lib=lib`
此参数将库安装在 `$prefix/lib` 中，而不是 x86_64 架构下的 `$prefix/lib64`。它对 x86 架构没有影响。

共享库被移动到 `/lib`，结果是 `/usr/lib/libcap` 中的 `.so` 文件将不会被重新创建。

```
mv -v /usr/lib/libcap.so.* /lib
ln -sfv ../lib$(readlink /usr/lib/libcap.so) /usr/lib/libcap.so
```

### 6.23.2. Libcap 的内容

- 已安装的程序：`capsh`, `getcap`, `getpcaps`, 和 `setcap`
- 已安装的库：`libcap`

## 简述

- `capsh`: 用于探索和限制能力支持的 shell 封装
- `getcap`: 检查文件能力
- `getpcaps`: 显示查询进程上的能力
- `libcap`: 包含了用于操作 POSIX 1003.1le 能力的库函数
- `setcap`: 设置文件能力

## 6.24. Sed-4.4

Sed 包包含一个流编辑器。

**预计编译时间：** 0.3 SBU
所需磁盘空间：25 MB

### 6.24.1. 安装 Sed

首先修复 LFS 环境中的一个问题并移除一个失败的测试用例：

```
sed -i '/s/usr/tools/'      build-aux/help2man
sed -i '/s/panic-tests.//' Makefile.in
```

为编译 Sed 准备：

```
./configure --prefix=/usr --bindir=/bin
```

编译包并生成 HTML 文档：

```
make
make html
```

要测试结果，执行：

```
make check
```

安装包及其文档：

```
make install
install -d -m755 /usr/share/doc/sed-4.4
install -m644 doc/sed.html /usr/share/doc/sed-4.4
```

### 6.24.2. Sed 的内容

- 已安装的程序：`sed`
- 已安装的目录：`/usr/share/doc/sed-4.4`

## 简述

- `sed` 单次通过过滤和转换文本文件

## 6.25. Shadow-4.4

Shadow 包包含了以安全方式处理密码的程序。

**预计编译时间：0.2 SBU**
**所需磁盘空间：2 MB**

### 6.25.1. 安装 Shadow

> 如果你想强制使用强密码，请在构建 Shadow 之前参考 http://www.linuxfromscratch.org/view/posts/cracklib.html。然后在在 `configure` 命令中添加 `--with-libcrack`。

禁用组及其手动帮助页的安装，Coreutils 提供了更好的版本。同时防止安装已经安装过的手动帮助页：

```
sed -i 's/groups//' src/Makefile.in
find -name Makefile.in -exec sed -i 's/groups / /' \;
```



libattr 包含了用于操作扩展属性的库函数

## 22. Acl-2.2.52

Acl 包包含了用于管理访问控制列表（Access Control Lists）的实用程序，这些列表用于为文件和目录定义更细粒度的裁量访问权限。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.8 MB

### 22.2.1. 安装 Acl

修改目录使其成为一个版本化目录：

```
sed -i -e 's|/@pkg_name@|@pkg_version@|' include/builddefs.in
```

修复一些损坏的测试用例：

```
sed -i " :; sed.*:*" test/(sbits-restore,cp,misc).test
```

此外，修复一个导致 `getfacl` 在处理组名过长时发生段错误的 bug：

```
sed -i -e "/TABS-1/a (x > (TABS-1)) x = (TABS-1);" "\nlibacl/__acl_to_any_text.c
```

为编译 Acl 准备：

```
./configure --prefix=/usr \
  --bindir=/bin \
  --disable-static \
  --libexecdir=/usr/lib
```

编译包：

```
make
```

Acl 的用例需要在支持访问控制的文件系统上运行，或者在构建 Coreutils 时已链接了 Acl 库。如果需要，可以在在本章后续构建完 Coreutils 后，返回此包并运行 `make -jl tests`。

安装包：

```
make install install-dev install-lib
chmod -v 755 /usr/lib/libacl.so
```

共享库需要移动到 `/lib`，结果是 `/usr/lib` 中的 `.so` 文件需要重新创建：

```
mv -v /usr/lib/libacl.so.* /lib
ln -sf /usr/lib/$(readlink /usr/lib/libacl.so) /usr/lib/libacl
```

### 22.2.2. Acl 的内容

- 已安装的程序：`chacl`, `getfacl`, 和 `setacl`
- 已安装的库：`libacl.so`
- 已安装的目录：`/usr/include/acld` 和 `/usr/share/doc/accl-2.2.52`

## 简述

- `chacl` 修改文件或目录的访问控制列表
- `getfacl` 获取文件访问控制列表
- `setacl` 设置文件访问控制列表
- `libacl` 包含了用于操作访问控制列表的库函数

## 23. Libcap-2.25

Libcap 包实现了 Linux 内核中可用的 POSIX 1003.1le 能力（capabilities）的用户空间接口。这些能力将所有强大的 root 权限划分为一组不同的权限。

**预计编译时间：** 少于 0.1 SBU
**所需磁盘空间：** 1.3 MB

### 6.23.1. 安装 Libcap

防止安装静态库：

```
sed -i '/install.*STALENAME/d' libcap/Makefile
```

编译包：

```
make
```

此包不附带测试套件。

安装包：

```
make RAISE_SETCAP=no lib=lib prefix=/usr install
chmod -v 755 /usr/lib/libcap.so
```

`make` 选项的含义：

> `RAISE_SETCAP=no`
此参数跳过尝试对自身使用 `setcap`。如果内核或文件系统不支持扩展能力，这可以避免安装错误。

> `lib=lib`
此参数将库安装在 `$prefix/lib` 中，而不是 x86_64 架构下的 `$prefix/lib64`。它对 x86 架构没有影响。

共享库被移动到 `/lib`，结果是 `/usr/lib/libcap` 中的 `.so` 文件将不会被重新创建。

```
mv -v /usr/lib/libcap.so.* /lib
ln -sfv ../lib$(readlink /usr/lib/libcap.so) /usr/lib/libcap.so
```

### 6.23.2. Libcap 的内容

- 已安装的程序：`capsh`, `getcap`, `getpcaps`, 和 `setcap`
- 已安装的库：`libcap`

## 简述

- `capsh`: 用于探索和限制能力支持的 shell 封装
- `getcap`: 检查文件能力
- `getpcaps`: 显示查询进程上的能力
- `libcap`: 包含了用于操作 POSIX 1003.1le 能力的库函数
- `setcap`: 设置文件能力

## 6.24. Sed-4.4

Sed 包包含一个流编辑器。

**预计编译时间：** 0.3 SBU
所需磁盘空间：25 MB

### 6.24.1. 安装 Sed

首先修复 LFS 环境中的一个问题并移除一个失败的测试用例：

```
sed -i '/s/usr/tools/'      build-aux/help2man
sed -i '/s/panic-tests.//' Makefile.in
```

为编译 Sed 准备：

```
./configure --prefix=/usr --bindir=/bin
```

编译包并生成 HTML 文档：

```
make
make html
```

要测试结果，执行：

```
make check
```

安装包及其文档：

```
make install
install -d -m755 /usr/share/doc/sed-4.4
install -m644 doc/sed.html /usr/share/doc/sed-4.4
```

### 6.24.2. Sed 的内容

- 已安装的程序：`sed`
- 已安装的目录：`/usr/share/doc/sed-4.4`

## 简述

- `sed` 单次通过过滤和转换文本文件

## 6.25. Shadow-4.4

Shadow 包包含了以安全方式处理密码的程序。

**预计编译时间：0.2 SBU**
**所需磁盘空间：2 MB**

### 6.25.1. 安装 Shadow

> 如果你想强制使用强密码，请在构建 Shadow 之前参考 http://www.linuxfromscratch.org/view/posts/cracklib.html。然后在在 `configure` 命令中添加 `--with-libcrack`。

禁用组及其手动帮助页的安装，Coreutils 提供了更好的版本。同时防止安装已经安装过的手动帮助页：

```
sed -i 's/groups//' src/Makefile.in
find -name Makefile.in -exec sed -i 's/groups / /' \;
```



## 25.24. 影子的内容

已安装程序：
`chage`, `chfn`, `chpassword`, `chsh`, `expiry`, `faillog`, `gpassword`, `groupadd`, `groupdel`, `groupmems`, `groupdp`, `grck`, `grpconv`, `grpunconv`, `lastlog`, `login`, `logout`, `newgidmap`, `newgrp`, `newuid`, `news`, `passwd`, `pwcon`, `pwuncong`, `sg`（链接到 `newgrp`），`su`, `userm`, `userdel`, `usermod`, `vigr`（链接到 `vip`）和 `pipw`

已安装目录：
`/etc/default`

## 简短描述

- `chage`: 用于更改强制修改密码之间的最大天数
- `chfn`: 用于更改用户的全名及其他信息
- `chpassword`: 用于以批量模式更新组密码
- `chpasswd`: 用于以批量模式更新用户密码
- `chsh`: 用于更改用户的默认登录 shell
- `expiry`: 检查并强制执行当前的密码过期策略
- `faillog`: 用于检查登录失败日志，设置账户被锁定前的最大失败次数，或重置失败计数
- `gpassword`: 用于向组中添加和删除成员及管理员
- `groupadd`: 创建一个指定名称的组
- `groupdel`: 删除指定名称的组
- `groupmems`: 允许用户在不需要超级权限的情况下管理/自己的组所有权列表
- `groupmod`: 用于修改组名或 GID
- `grck`: 验证组文件 `/etc/group` 和 `/etc/shadow` 的完整性
- `grpconv`: 从普通组文件创建或更新 shadow 文件
- `grpunconv`: 从 `/etc/shadow` 更新 `/etc/group` 然后删除后者
- `lastlog`: 报告所有用户或指定用户的最近登录情况
- `login`: 用于让用户登录的系统程序
- `logout`: 一个用于对登录时间和端口实施限制的守护进程
- `newmap`: 用于设置用户命名空间的 gid 映射
- `newgrp`: 用于在登录会话期间更改当前 GID
- `newuidmap`: 用于设置用户命名空间的 uid 映射
- `newsers`: 用于创建或更新一系列用户账户
- `nologin`: 显示账户不可用的消息；被设计用于已禁用账户的默认 shell
- `passwd`: 用于更改用户或组账户的密码
- `pwck`: 验证密码文件 `/etc/passwd` 和 `/etc/shadow` 的完整性
- `pwconv`: 从普通密码文件创建或更新 shadow 密码文件
- `pwunconv`: 从 `/etc/shadow` 更新 `/etc/passwd` 然后删除后者
- `sg`: 在用户 GID 设置为指定的 GID 时执行给定命令
- `su`: 运行带有替换用户和组 ID 的 shell
- `useradd`: 创建一个指定名称的新用户，或更新默认的新用户信息
- `userdel`: 删除指定的用户账户
- `usermod`: 用于修改指定用户的登录名、用户标识 `UID`、shell、初始组、主目录等。
- `vigr`: 编辑 `/etc/group` 或 `/etc/shadow` 文件
- `vipw`: 编辑 `/etc/passwd` 或 `/etc/shadow` 文件

## 6.26. Psmisc-22.21

`Psmisc` 软件包包含用于显示运行进程信息的程序。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.0 MB

### 6.26.1. Psmisc 的安装

为编译准备 `Psmisc`：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

此软件包未附测试套件。

安装：

```
make install
```

最后，将 `killall` 和 `fuser` 程序移动到 FHS 指定的的位置：

```
mv -v /usr/bin/fuser /bin
mv -v /usr/bin/killall /bin
```

### 6.26.2. Psmisc 的内容

已安装程序：`fuser`, `killall`, `peekfd`, `prstat`, `pstree` 和 `pstree.x11`（链接到 `pstree`）

## 简短描述

- `fuser`: 报告使用给定文件或文件系统的进程进程 ID `PIDs`
- `killall`: 通过名称杀死进程；它向运行任何一个给定命令的所有进程发送信号
- `peekfd`: 给定定的 PID，查看运行进程的文件描述符
- `prstat`: 打印进程信息
- `pstree`: 以树形显示正在运行的进程
- `pstree.x11`: 与 `pstree` 相同，区别是在退出前会等待确认

## 6.27. iana-Etc-2.30

`IANA-Etc` 软件包提供了网络服务和协议的数据。

预计编译时间：少于 0.1 SBU
所需磁盘空间：2.3 MB

### 6.27.1. iana-Etc 的安装

以下命令将 IANA 提供的原始数据转换为 `/etc/protocols` 和 `/etc/services` 数据文件的正确格式：

```
make
```

此软件包未附测试套件。

安装软件包：

```
make install
```

### 6.27.2. iana-Etc 的内容

已安装文件：`/etc/protocols`, `/etc/services`

## 简短描述

- `/etc/protocols`: 描述各种协议
- `/etc/services`: 提供友好名称与端口之间的映射

## 6.28. m4-1.4

`m4` 软件包包含一个宏处理器。

预计编译时间：0.4 SBU
所需磁盘空间：31 MB

### 6.28.1. m4 的安装

为编译准备 `m4`：

```
./configure --prefix=/usr
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

### 6.28.2. m4 的内容

已安装程序：`m4`

## 简短描述

- `m4`: 用于扩展宏的工具；可以用于处理文本、递归等

## 6.29. Bison-3.0

`Bison` 软件包包含一个解析器生成器。

预计编译时间：0.3 SBU
所需磁盘空间：32 MB

### 6.29.1. Bison 的安装

为编译准备 `Bison`：

```
./configure --prefix=/usr --docdir=/usr/share/bison
```

编译软件包：

```
make
```

`bison` 和 `flex` 之间存在循环依赖。安装软件包：

```
make install
```

### 6.29.2. Bison 的内容

已安装程序：`bison`, `yacc`
已安装库：`liby.a`
已安装目录：`/usr/share/bison`

## 简短描述

- `bison`: 从一系列规则生成分析结构的解析器
- `yacc`: `bison`（另一个编译器）的封装
- `liby`: 包含 `yyerror` 和 `main` 函数的 Yacc 库

## 6.30. Flex-2.6.3

`Flex` 软件包包含一个用于生成识别文本模式的程序。

预计编译时间：0.4 SBU
所需磁盘空间：32 MB

### 6.30.1. Flex 的安装

构建过程假设 `help2man` 程序可用从可执行文件创建帮助页。该程序不存在，因此我们使用环境变量跳过此过程。现在，为编译准备 `Flex`：

```
HELP2MAN=/tools/bin/true \
./configure --prefix=usr --docdir=/usr/share/doc/flex-2.3
```

编译软件包：

```
make
```

测试结果（约 0.5 SBU）：

```
make check
```

其中一个测试 `cxx_restart` 已知失败。

安装软件包：

```
make install
```

### 6.30.2. Flex 的内容

已安装程序：`flex++`（链接到 `flex`）和 `lex`（链接到 `flex`）
已安装库：`libfl.so` 和 `libfl_pic.so`
已安装目录：`/usr/share/doc/flex-2.3`

## 简短描述

- `flex`: 用于生成识别文本中模式程序的工具；它允许指定模式规则的灵活性
- `flex++`: `flex` 的扩展，用于生成 C++ 代码和类
- `lex`: 以 `lex` 模拟模式运行 `flex` 的脚本
- `libfl`: `flex` 库

## 6.31. Grep-3.0

`Grep` 软件包包含了用于搜索文件的程序。
预计编译时间：0.4 SBU
所需磁盘空间：29 MB

### 6.31.1. 安装 Grep

为编译准备 `Grep`：

```
./configure --prefix=/usr --bindir=/bin
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

### 6.31.2. Grep 的包含内容

已安装的程序：`egrep`, `fgrep` 和 `grep`

#### 简短描述

- `egrep`: 打印匹配扩展正则表达式的行
- `fgrep`: 打印匹配固定字符串列表的行
- `grep`: 打印匹配基本正则表达式的行

## 6.32. Readline-7.0

Readline 软件包是一组库，提供了命令行编辑和历史记录功能。
预计编译时间：0.1 SBU
所需磁盘空间：15 MB

### 6.3.1. 安装 Readline

重新安装 Readline 会导致旧库移动到 `<libraryname>.old`。虽然这没有问题，但在某些情况下，它可能会触发 `ldconfig` 中的链接 bug。可以通过执行以下两条命令来避免这种情况：

```
sed -i '/MV.*old/d' Makefile.in
sed -i '/{OLDSUFF}/c:' support/shlib-install
```

为编译准备 Readline：

```bash
./configure --prefix=/usr --disable-static \
  --docdir=/usr/share/doc/readline-7.0
```

编译软件包：

```
make SHLIB_LIBS=-lncurses
```

该选项的含义：
`SHLIB_LIBS=-lncurses`
此选项强制 Readline 链接到 `libncursesw`（实际上是 `libncursesw`）库。
此软件包不带测试套件。

安装软件包：

```
make SHLIB_LIBS=-lncurses install
```

将动态库移动到更合适的位置并修复一些符号链接：

```bash
mv -v /usr/lib/lib{readline,history}.so.* /lib
ln -sf ../lib/$(basename /usr/lib/libreadline.so) /usr/lib/libreadline.so
ln -sf ../lib/$(basename /usr/lib/libhistory.so ) /usr/lib/libhistory.so
```

如果需要，安装文档：

```bash
install -v -m644 *.{pdf,html,dvi} /usr/share/doc/readline-7.0
```

### 6.3.2. Readline 的包含内容

已安装的库：`libhistory.so` 和 `readline.so`
已安装的目录：`/usr/include/readline`, `/usr/share/readline` 以及 `/usr/share/doc/readline-7.0`

#### 简短描述

- `history`: 为回溯历史行提供一致的用户界面
- `libreadline`: 帮助在需要提供命令行界面的离散程序之间保持用户界面的一致性

## 6.33. Bash-4.4

Bash 软件包包含了 Bourne-Again Shell 的修复。
预计编译时间：1.7 SBU
所需磁盘空间：56 MB

### 6.33.1. 安装 Bash

合并上游修复：

```bash
patch -Npl1 -i ../bash-4.4-upstream-fixes-1.patch
```

为编译准备 Bash：

```bash
./configure --prefix=/usr \
--docdir=/usr/share/doc/bash-4.4 \
--without-bash-malloc \
--with-installed-readline \
```

新配置选项的含义：

```
--with-installed-readline
```

此选项告诉 Bash 使用系统已安装的 readline 库，而不是使用它自带的 readline 版本。

编译软件包：

```bash
make
```

如果不运行测试套件，请跳到“安装软件包”。

要准备测试工作，请确保 `nobody` 用户可以向源码树写入内容：

```bash
chown -Rv nobody .
```

现在，以 `nobody` 用户身份运行测试：

```bash
su nobody -s /bin/bash -c "PATH=$PATH make tests"
```

安装软件包并将主执行文件移动到 `/bin`：

```bash
make install
mv -vf /usr/bin/bash /bin
```

运行新编译的 bash 程序（替换当前执行的程序）：

```bash
exec /bin/bash --login +
```

> 注意
> 使用的参数使 bash 进程成为交互登录 shell，并继续禁用哈希处理，以便在新程序可用时能被找到。

### 6.33.2. Bash 的包含内容

已安装的程序：`bash`, `bashbug` 和 `sh`（指向 bash 的链接）
已安装的目录：`/usr/share/doc/bash-4.4`

#### 简短描述

- `bash`: 一个广泛使用的命令解释器；它在执行给定命令行之前会对其进行许多类型的扩展和替换，因此使该解释器成为一个强大的工具
- `bashbug`: 一个 shell 脚本，帮助用户编写并发送关于 bash 的标准格式 bug 报告
- `sh`: 指向 bash 程序的符号链接；当作为 sh 被调用时，bash 尝试尽尽可能地模拟历史版本 sh 的启动行为，同时符合 POSIX 标准

## 6.34. Bc-1.06

Bc 软件包包含一个任意精度计算器。
预计编译时间：0.1 SBU
所需磁盘空间：6 MB

### 6.34.1. 安装 Bc

合并上游修复：

```bash
patch -Npl1 -i ../bash-4.4-upstream-fixes-1.patch
```

为编译准备 Bc：

```bash
./configure --prefix=/usr \
--with-readline \
--mandir=/usr/share/man \
--infdir=/usr/share/info
```

配置选项的含义：

```
--with-readline
```

此选项告诉 Bc 使用系统已安装的 readline 库。

编译软件包：

```bash
make
```

如果不运行测试套件，请跳到“安装软件包”。

要准备测试，请确保 `nobody` 用户可以向源码树写入内容：

```bash
chown -Rv nobody .
```

现在，以 `nobody` 用户身份运行测试：

```bash
su nobody -s /bin/bash -c "PATH=$PATH make tests"
```

安装软件包并将主执行文件移动到 `/bin`：

```bash
make install
mv -vf /usr/bin/bash /bin
```

运行新编译的 bash 程序（替换当前执行的程序）：

```bash
exec /bin/bash --login +
```

### 6.34.2. Bc 的包含内容

已安装的程序：`bc`, `dc`
已安装的目录：`/usr/share/doc/bc`

#### 简短描述

- `bc`: 任意精度计算器
- `dc`: 逆波兰表达式法计算器

## 6.35. Libtool-2.4

Libtool 软件包提供了通用的库构建支持。
预计编译时间：2.0 SBU
所需磁盘空间：43 MB

### 6.35.1. 安装 Libtool

为编译准备 Libtool：

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

### 6.35.2. Libtool 的包含内容

已安装的程序：`libtool`, `libtoolize` 和 `libtoold`
已安装的库：`libtool.so`
已安装的目录：`/usr/include/libtool`, `/usr/share/libtool`

#### 简短描述

- `libtool`: 提供通用的库构建服务
- `libtoolize`: 为软件包添加 libtool 支持的标准方法
- `libtoold`: 隐藏各种库的复杂性

## 6.36. GDBM-1.12

GDBM 软件包包含了 GNU 管理器。
预计编译时间：0.1 SBU
所需磁盘空间：9 MB

### 6.36.1. 安装 GDBM

为编译准备 GDBM：

```bash
./configure --prefix=/usr \
--enable-libgdbm-compat
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

### 6.36.2. GDBM 的包含内容

已安装的程序：`gdbm_dump`, `gdbm_load` 和 `gdbmtool`
已安装的库：`libgdbm.so` 和 `libgdbm_compat`

#### 简短描述

- `gdbm_dump`: 将 GDBM 数据库导出到文件
- `gdbm_load`: 从转储文件重建 GDBM 数据库
- `gdbmtool`: 测试和修改 GDBM 数据库

# 6.37. Gperf-3.0.4

`Gperf` 从键集生成完美哈希函数。

近似编译时间：少于 0.1 SBU
所需磁盘空间：5.4 MB

## 6.37.1. 安装 Gperf

为编译准备 `Gperf`：

```
./configure --prefix=/usr --docdir=/usr/share/doc/gperf-3.0.4
```

编译软件包：

```
make
```

众所周知，在运行多个并行测试时（`-j` 选项大于 1），测试将会失败。若要测试结果，请执行：

```
make -j1 check
```

安装软件包：

```
make install
```

## 6.37.2. Gperf 的内容

已安装的程序：`g`

已安装目录：`/usr/share/doc/gperf-3.0.4`

### 简短描述

- `gperf`: 从键集生成完美哈希

# 6.38. Expat-2.2.0

`Expat` 软件包包含一个用于解析 XML 的流式 C 库。

近似编译时间：少于 0.1 SBU
所需磁盘空间：6.1 MB

### 6.38.1. 安装 Expat

为编译准备 `Expat`：

```
./configure --prefix=/usr --disable-static
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

如果需要，安装文档：

```
install -v -dm755 /usr/share/doc/expat-2.2.0
install -v -m644 doc/*. (html,png,css) /usr/share/doc/expat-2.2.0
```

## 6.38.2. Expat 的内容

已安装的程序：`xmlwf`
已安装的库：`libexpat.so`
已安装目录：`/usr/share/doc/expat-2.2.0`

### 简短描述

- `xmlwf`: 一种用于检查 XML 文档是否格式良好的非校验工具
- `libexpat`: 包含解析 XML 的 API 函数

# 6.39. Inetutils-1.9.4

`Inetutils` 软件包包含基础网络所需的程序。
近似编译时间：0.4 SBU
所需磁盘空间：27 MB

## 6.39.1. 安装 Inetutils

为编译准备 `Inetutils`：

```
./configure --prefix=/usr
--localstatestir=/var
--disable-logger
--disable-whois
--disable-rpc
--disable-rexec
--disable-rlogin
--disable-rsh
--disable-servers
```

配置选项的含义：

- `--disable-logger`: 此选项防止 `Inetutils` 安装 `logger` 程序，该程序用于脚本将消息传递给系统日志守护进程（System Log Daemon）。如果 `Util-linux` 安装了更新版本，则不要安装。
- `--disable-whois`: 此选项禁用 `Inetutils` `whois` 客户端的构建，因为它已经过时。关于更好的 `whois` 客户端的说明请参考 BLFS 书籍。
- `--disable-r*`: 这些参数禁用了由于安全问题而不再使用的旧程序构建。这些程序提供的功能可以通过 BLFS 书籍中的 `openssh` 软件包提供。
- `--disable-servers`: 此选项禁用了作为 `Inetutils` 软件包一部分各种网络服务器的安装。这些服务器在基础 LFS 系统中认为是不适当的。某些本质上是不安全的，仅在受信任的网络上被认为是安全的。注意

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

移动部分程序，以便在 `/usr` 无法访问时可以使用它们：

```
mv -v /usr/bin/{hostname,ping,ping6,traceroute} /bin
mv -v /usr/bin/ifconfig /sbin
```

## 6.39.2. Inetutils 的内容

已安装的程序：`dnsdomainname`, `ftp`, `ifconfig`, `hostname`, `ping`, `ping6`, `talk`, `telnet`, `tftp` 和 `traceroute`

### 简短描述

- `dnsdomainname`: 显示系统的 DNS 域名
- `ftp`: 文件传输协议程序
- `hostname`: 报告或设置主机名
- `ifconfig`: 管理网络接口
- `ping`: 发送回显请求包并报告回复时间
- `ping6`: 适用于 IPv6 网络的 `ping` 版本
- `talk`: 用于与另一个用户聊天
- `telnet`: TELNET 协议的接口
- `tftp`: 简易文件传输程序
- `traceroute`: 追踪数据包从你工作的主机到网络上另一个主机的路径，显示途中所有的中间跳数（网关）

# 6.40. Perl-5.24.1

`Perl` 软件包包含了实用提取报告语言（Practical Extraction and Report Language）。

近似编译时间：5.9 SBU
所需磁盘空间：245 MB

## 6.40.1. 安装 Perl

首先创建一个 `/etc/hosts` 文件，供 `Perl` 的一个配置文件以及可选测试套件引用：

```
echo "127.0.0.1 localhost $(hostname)" > /etc/hosts
```

（注：由于原始文本存在大量重复和 OCR 错误，已提取并处理唯一的逻辑内容。）

# Linux From Scratch - 版本 8.0

- `pod2man` 将 pod 数据转换为格式化的 *roff 输入*
- `pod2text` 将 pod 数据转换为格式化的 ASCII 文本
- `pod2usage` 从文件内嵌入的 pod 文档中打印用法信息
- `podchecker` 检查 pod 格式文档文件的语法
- `podselect` 显示选定的 pod 文档部分
- `prove` 用于针对 `Test::Harness` 模块运行测试的命令行工具
- `pstruct` 倾储由 `cc -g -S stabs` 生成的 C 结构体
- `ptar` 一个用 Perl 编写的类 tar 程序
- `ptardiff` 一个比较已提取的归包与未提取的归包的 Perl 程序
- `ptargrep` 一个对 tar 归包内文件内容应用模式匹配的 Perl 程序
- `shasum` 打印或检查 SHA 校验和
- `splain` 用于在 Perl 中强制输出详尽的警告诊断
- `xsub` 将 Perl XS 代码转换为 C 代码
- `zipdetails` 显示 Zip 文件内部结构的详细信息

## 6.41. XML::Parser-2.44

`XML::Parser` 模块是用于 James Clark 的 XML 解析器 `Expat` 的 Perl 接口。

估计构建时间：少于 0.1 SBU
所需磁盘空间：2.0 MB

### 6.41.1. 安装 XML::Parser

为编译 `XML::Parser` 做好准备：

```
perl Makefile.PL
```

编译该包：

```
make
```

要测试结果，请执行：

```
make test
```

安装该包：

```
make install
```

### 6.41.2. XML::Parser 的内容

已安装模块：`Expat.so`

#### 简描述

- `Expat` 提供了 Perl Expat 接口

## 6.42. Intltool-0.51.0

`Intltool` 是一个国际化工具，用于从源文件中提取可翻译的字符串。

估计构建时间：少于 0.1 SBU
所需磁盘空间：1.5 MB

### 6.42.1. 安装 Intltool

首先修复由 `perl-5.22` 及更高版本引起的警告：

```
sed -i 's/\\($\\)/\1/' intltool-update.in
```

为编译 `Intltool` 做好准备：

```
./configure --prefix=/usr
```

编译该包：

```
make
```

要测试结果，请执行：



`make check`

```
安装该包：
```

```
install -v -Dm644 doc/I18N-HOWTO /usr/share/doc/intltool-0.51.0/I18N-HOWTO
```

### 6.42.2. Intltool 的内容

- 已安装程序：`intltool-extract`, `intltool-merge`, `intltool-prepare`, `intltool-update` 和 `intloolize`
- 已安装目录：`/usr/share/doc/intltool-0.51.0` 和 `/usr/share/intltool`

#### 简描述

- `intloolize` 为包使用 intltool 做好准备
- `intltool-extract` 生成 gettext 可以读取的头文件
- `intltool-merge` 将翻译后的字符串合并到各种文件类型中
- `intltool-prepare` 更新 pot 文件并将其与翻译文件合并
- `intltool-update` 更新 po 模板文件并将其与翻译合并

## 6.43. Autoconf-2.69

Autoconf 包包含用于生成 shell 脚本的程序，可以自动配置源代码。
估计构建时间：少于 0.1 SBU（带测试约为 3.5 SBU）
所需磁盘空间：17.3 MB

### 6.43.1. 安装 Autoconf

为编译 Autoconf 做好准备：

```
./.configure --prefix=/usr
```

编译该包：

```
make
```

要测试结果，请执行：

```
make check
```

这需要很长时间，大约 3.5 个 SBUs。此外，还跳过了几个使用 Automake 的测试。为了获得完整的测试覆盖，可以在 Automake 安装后重新测试 Autoconf。此外，由于 libtool-2.4.3 及更高版本的更改，有两个测试失败了。

安装该包：

```
make install
```

### 6.43.2. Autoconf 的内容

- 已安装程序：`autoconf`, `autoheader`, `autom4te`, `autoreconf`, `autoscan`, `autoupdate` 和 `ifnames`
- 已安装目录：`/usr/share/autoconf`

#### 简描述

- `autoconf` 生成自动配置源代码包以适应各种类 Unix 系统的脚本；它生成的配置脚本是独立的——运行这些脚本不需要 `autoconf` 程序
- `autoheader` 一个用于创建供 configure 调用的 C #define 语句模板文件的工具
- `autom4te` M4 宏处理器的封装器
- `autoreconf` 自动按照正确顺序运行 `autoconf`, `autoheader`, `aclocal`, `automake`, `gettextize` 和 `libtool`，以便在修改 `autoconf` 和模板文件时节省时间
- `autoscan` 帮助为软件包创建一个 configure.in 文件；它检查目录树中的文件，搜索常见的可移植性，并创建一个 configure.scan 文件作为该包的初步 configure.in 文件
- `autoupdate` 修改仍以旧名称调用 `autoconf` 宏的 configure.in 文件，以使用当前的宏名称
- `ifnames` `\text{ifnames}` 在为软件包编写 configure.in 文件时很有帮助；它打印包在 C 预处理器条件判断使用的标识符 [如果一个包已经设置了某些可移植性，此程序可以帮助确定 configure 需要检查什么。它还可以填补由 autoscan 生成的 configure.in 文件中的空白。]

## 44. Automake-1.15

Automake 包包含用于为配合 Autoconf 生成 Makefile 的程序。
估计构建时间：少于 0.1 SBU（带测试约为 7.5 SBU）
磁盘空间：110 MB

### 6.44.1. 安装 Automake

首先修复由 perl-5.22 及更高版本引起的 thaw错误：

```
sed -i 's/\//bin\/automake.in/'
```

为编译 Automake 做好准备：

```
./configure --prefix=/usr --docdir=/usr/share/doc/automake-1.15
```

编译该包

```
make
```

构建过程中存在一些错误。要测试结果，请执行：

```
make check
```

安装该包：

```
make install
```

### 6.44.2. Automake 的内容

- 已安装程序：`automake`, `autom4te`, `autoconf`, `aclocal`, `autoscan`, `autoupdate`, `ifnames`
- 已安装目录：`/usr/share/automake`

#### 简描述

- `automake` 生成用于配合 Autoconf 的 Makefile
- `autom4te` M4 宏处理器的封装器
- `autoconf` 生成自动配置源代码包以适应各种类 Unix 系统的脚本；它生成的配置脚本是独立的——运行这些脚本不需要 `autoconf` 程序
- `autoheader` 一个用于创建供 configure 调用的 C #define 语句模板文件的工具
- `autoreconf` 自动按照正确顺序运行 `autoconf`, `autoheader`, `aclocal`, `automake`, `gettextize` 和 `libtool`，以便在修改和模板文件时节省时间
- `autoscan` 帮助为软件包创建一个 configure.in 文件；它检查目录树中的文件，搜索常见的可移植性，并创建一个 configure.scan 文件作为该包的初步 configure.in 文件
- `autoupdate` 修改仍以旧名称调用 `autoconf` 宏的 configure.in 文件，以使用当前的宏名称
- `ifnames` 在为软件包编写 configure.in 文件时很有帮助；它打印包在 C 预处理器条件判断使用的标识符 [如果一个包已经设置了某些可移植性，此程序可以帮助确定 configure 需要检查什么。它还可以填补由 autoscan 生成的 configure.in 文件中的空白。]

## 6.45. Xz-5.2

Xz 包包含用于压缩和解压缩文件的程序。它提供了 Lma 格式。使用 xz 压缩文本比 gzip 或 bzip2 效果更好。

估计构建时间：0.2 SBU
所需磁盘空间：15 MB

### 6.45.1. 安装 Xz

为 Xz 编译做好准备：

```
./configure --prefix=/usr \
--disable-static \
    --docdir=/usr/share/doc/xz-5.2
```

编译包：

```
make
```

要测试结果，执行：

```
make check
```

安装该包并确保所有基本文件位于正确的目录：

```
make install
mv -v /usr/bin/{lzma,unlzma,lzcat,xz,unxz,xzcat} /bin
mv -v /usr/lib/liblzma.so.* /lib
ln -svf ../../usr/lib/liblzma.so /usr/lib/liblzma.so
```



### 6.45.2. Xz 的内容

- **已安装程序：** `lzcat` (link to `xz`), `lzcmp` (link to `xzdiff`), `lzdiff` (link to `xzdiff`), `lzgrep` (link to `xzgrep`), `lzfgrp` (link to `xzgrep`), `lgrep` (link to `xzgrep`), `lzless` (link to `xless`), `lzma` (link to `xz`), `xzcat` (link to `xz`), `xzcmp`, `lzmadec`, `lzmore` (link to `xmore`), `unlzma` (link to `xz`), `unxz` (link to `xz`), `xz`, `xzdiff` (link to `xzdiff`), `xde`, `xxdiff`, `xzgrep` (link to `xzgrep`), `xzrep` (link to `xzgrep`), `xgrep`, `xless`, 和 `xmore`
- **已安装库：** `liblzma.so`
- **已安装目录：** `/usr/include/lzma` 和 `/usr/share/doc/xz-5.2`

#### 简描述

- `lzcat` 解压到标准输出
- `lzcmp` 对 LZMA 压缩文件运行 `cmp`
- `lzdiff` 对 LZMA 压缩文件运行 `diff`
- `lzgrep` 对 LZMA 压缩文件运行 `egrep`
- `lzfgrp` 对 LZMA 压缩文件运行 `fgrep`
- `lgrep` 对 LZMA 压缩文件运行 `grep`
- `lzless` 对 LZMA 压缩文件运行 `less`
- `lzma` 链接到 `xz`

- `lzless` | 对 LZMA 压缩文件运行 `less`
- `lzma` | 使用 LZMA 格式对文件进行压缩或解压缩
- `lzmadec` | 一个用于 LZMA 压缩文件的轻量且快速解码器
- `lzinfo` | 显示 LZMA 压缩文件头中存储的信息
- `lzmore` | 对 LZMA 压缩文件运行 `more`
- `unlzma` | 使用 LZMA 格式解压缩文件
- `unxz` | 使用 XZ 格式解压缩文件
- `xz` | 使用 XZ 格式对文件进行压缩或解压缩
- `zczat` | 解压缩到标准输出
- `zczmp` | 对 XZ 压缩文件运行 `cmp`
- `xzdec` | 一个用于 XZ 压缩文件的轻量且快速的解码器
- `xzdiff` | 对 XZ 压缩文件运行 `diff`
- `xegrep` | 对 XZ 压缩文件运行 `egrep`
- `xzfgrep` | 对 XZ 压缩文件运行 `grep`
- `xzgrep` | 对 XZ 压缩文件运行 `grep`
- `xzless` | 对 XZ 压缩文件运行 `less`
- `xzmore` | 对 XZ 压缩文件运行 `more`
- `liblzma` | 实现无损、块排序数据压缩的库，使用 Lempel-Ziv-Markov 链算法

## 6.46. Kmod-23

`Kmod` 包包含用于加载内核模块的库和实用程序。

预计构建时间：0.1 SBU
所需磁盘空间：10.3 MB

### 6.46.1. 安装 Kmod

为编译准备准备 `Kmod`：

```bash
./configure --prefix=/usr \
--bindir=/bin \
--sysconfdir=/etc \
--with-rootlibdir=/lib \
--with-xz \
--with-zlib
```

配置选项的含义：

`--with-xz`, `--with-zlib`
这些选项允许 `Kmod` 处理压缩的内核模块。
`--with-rootlibdir=/lib`
此选项确保将不同的库相关文件放置在正确的目录中。

编译该包：

```bash
make
```

此包不包含可以在 LFS chroot 环境中运行的测试套件。至少需要 `git` 程序，且某些测试在 `git` 仓库之外无法运行。

安装该包，并为兼容 Module-Init-Tools（以前处理 Linux 内核模块的包）创建符号链接：

```bash
make install
```

```bash
for target depmod insmod lsmod modinfo modprobe rmmod; do
ln -sf ../bin/kmod /sbin/$target
done
```

```bash
ln -sf kmod /bin/lsmod
```

### 6.46.2. Kmod 的内容

已安装的程序：
`depmod`（指向 `kmod`）、`insmod`（指向 `kmod`）、`kmod`、`lsmod`（指向 `kmod`）、`modinfo`（指向 `kmod`）、`modprobe`（指向 `kmod`）以及 `rmmod`（指向 `kmod`）

已安装的库：
`libkmod.so`

## 简要描述

`depmod` | 根据在现有模块集中找到的符号创建依赖文件；该依赖文件用于 `modprobe` 自动加载所需的模块。

- `insmod` | 在运行的内核中安装可加载的模块

- `kmod` | 加载和卸载内核模块

- `lsmod` | 列出当前加载的模块

- `modinfo` |检查与内核模块相关的对象文件并显示它可以获取的任何信息

- `modprobe` | 使用 `depmod` 创建的依赖文件自动加载相关模块

- `rmmod` | 从运行的内核中卸载模块

- `libkmod` | 其他程序使用此库加载和卸载内核模块

## 6.47. Gettext-0.19.8.1

`Gettext` 包包含用于国际化和本地化的实用程序。这些工具允许程序在带有 NLS（原生语言支持）的情况下编译，使其能够以用户的母语言输出消息。

预计构建时间：2.9 SBU
所需磁盘空间：199 MB

### 6.47.1. 安装 Gettext

首先，消除可能导致某些机器无限循环的两个测试锁：

```bash
sed -i '/TESTS /=d/' gettext-runtime/tests/Makefile.in &&
sed -i '/s/test-lock..EXEEXT.//' gettext-tools/gnulib-tests/Makefile.in
```

为编译准备 `Gettext`：

```bash
./configure --prefix=/usr \
--disable-static \
--docdir=/usr/share/doc/gettext-0.19.8.1
```

编译该包：

```bash
make
```

要测试结果（这需要很长时间，大约 3 SBUs），执行：

```bash
make check
```

安装该包：

```bash
make install
chmod -v 0755 /usr/lib/preloading_libintl1.so
```



### 6.47.2. Gettext 的内容

- **已安装的程序：** `autopoint`, `envsubst`, `gettext`, `gettext.sh`, `getextize`, `msgfmt`, `msgcat`, `msgcmp`, `msgcomm`, `msgconv`, `msggen`, `msgetex`, `msgfile`, `msggper`, `msginit`, `msgmerge`, `msgunft`, `msgnui`, `ngetex`, `recode-rl.sh` 以及 `gettext`
- **已安装的库：** `libansprint.so`, `libgetextlib.so`, `libgetextpo.so`, `libgetextsrc.so` 以及 `preloading_libintl.so`
- **已安装的目录：** `/usr/lib/gettext`, `/usr/share/doc/gettext-0.19.8.1`

## 简要描述

- `autopoint` | 根据源文件创建提取点文件
- `envsubst` | 替换环境变量中的变量
- `gettext` | 用于翻译文本的工具
- `gettext.sh` | `gettext` 脚本
- `getextize` | 准备翻译所需的目录
- `msgfmt` | 将文本翻译文件转换为二进制格式
- `msgcat` | 合并 `.po` 文件
- `msgcmp` | 比较两个 `.po` 文件
- `msgcomm` | 查找消息的共同部分
- `msgconv` | 转换消息格式
- `msggen` | 生成 `msg` 模板文件
- `msgetex` | 扩展 `gettext` 功能
- `msgfile` | 列出消息文件内容
- `msggper` | 统计消息出现的频率
- `msginit` | 创建新的 `.po` 文件
- `msgmerge` | 合并翻译并更新
- `msgunft` | 显示未翻译的字符串
- `msgnui` | 翻译用户界面
- `ngetex` | 扩展 `gettext` 功能
- `recode-rl.sh` | 将西里尔字母转码为拉丁字母
- `libansprint` | 定义 `printf` 类
- `libgetextlib` | 用于 `gettext` 的扩展库
- `libgetextpo` | 用于写入 `.po` 文件
- `libgetextsrc` | 包含例的私有库
- `preload_libintl` | 辅助 `libintl` 处理翻译的库

## 6.8. Procps-ng-3.3.1

`Procps-ng` 包包含监控进程的程序。

预计构建时间：0.1 SBU
所需磁盘空间：14 MB

### 6.8.1. 安装 Procps-ng

现在为编译准备 `procps-ng`：

```bash
./configure --prefix=/usr \
--exec-prefix= \
--libdir=/usr/lib \
--docdir=/usr/share/procps-ng-3.3.1 \
--disable-static \
--disable-kill
```

编译该包：

```bash
make
```

测试套件针对 LFS 需要一些自定义。移除在脚本使用 `utty` 时失败的测试。要运行测试，执行以下命令：

```bash
sed -i -r '(pmap_initname)\$|\1| testsuite/pmap.test
make check
```

一个 `ps` 测试可能会失败，但在章节末尾重新运行时将通过。

安装该包：

```bash
make install
```

最后，将基本库移动到 `/usr` 未挂载时也能找到的位置。

```bash
mv -v /usr/lib/libprocps.so.* /lib
ln -sfv ../lib/$(readlink /usr/lib/libprocps.so) /usr/lib/libprocps.so
```

### 6.8.2. Procps-ng 的内容

- **已安装的程序：** `free`, `grep`, `pidof`, `pkill`, `pmap`, `ps`, `pwdx`, `slab`, `sysctl`, `toad`, `top`, `uptime`, `wstat` 以及 `watch`
- **已安装的库：** `libprocps.so`
- **已安装的目录：** `/usr/include/proc` `/usr/share/procps-ng-3.3.1`

- `pgrep` | 根据名称和其他其他属性查找进程
- `pidof` | 报告给定程序的 PID
- `pidkill` | 根据名称和其他其他属性向进程发送信号
- `map` | 报告给定进程的内存映射
- `ps` | 列出当前运行的进程
- `pwdx` | 报告进程的当前工作目录
- `slabtop` | 实时显示详细内核 slab 缓存信息
- `sysctl` | 在运行时修改内核参数
- `top` | 显示资源最密集型进程列表；它对处理器活动提供实时查看
- `uptime` | 报告系统运行时间、登录用户数以及系统负载平均值
- `vmstat` | 报告虚拟内存统计，提供关于进程、内存、分页、块输入/输出 (IO)、陷阱 (traps) 和 CPU 活动的信息
- `w` | 显示哪些用户当前登录、在何处以及何时登录
- `watch` | 重复运行给定命令，显示其输出的第一屏内容；这允许用户观察输出随时间发生的变化

`libprocps` 包含此包中大多数程序使用的函数

## 6.49. E2fsprogs-1.43.4

`E2fsprogs` 包包含用于处理 `ext2` 文件系统的实用程序。它还支持 `ext3` 和 `ext4` 日志系统。

近似编译时间：4.1 SBU
所需磁盘空间：57 MB

### 6.49.1. 安装 E2fsprogs

`E2fsprogs` 文档建议在源码树的子目录中构建该包：

```
mkdir -v build
cd build
```

为编译 `E2fsprogs` 准备工作：

```
LIBS=-L/tools/lib
CFLAGS=-I/tools/lib/pkgconfig
PKG_CONFIG_PATH=--prefix=usr
../configure --bindir=/bin
--with-root-prefix=""
--enable-elf-shlibs
--disable-libklkid
--disable-libuuid
--disable-uiddid
--disable-fsck
```

环境变量和配置选项的含义：

`PKG_CONFIG_PATH`, `LIBS`, `CFLAGS`
这些变量允许 `E2fsprogs` 使用之前构建的第 5.34 节“Ut-linux-2.29.1”包进行构建
`--with-root-prefix=""` 和 `--bindir=/bin`

某些程序（如 `efsck`）被视为基本程序。当例如，`/usr` 未挂载时，这些程序仍然需要可用。它们属于 `/lib` 和 `/sbin` 等目录。如果未将此选项传递给 `E2fsprogs` 的 `configure`，程序将被安装到 `/usr` 目录。

`--enable-elf-shlibs`
这会创建该包中某些程序使用的共享库。

`--disable-*`
这可以防止 `E2fsprogs` 构建并安装 `libuuid` 和 `libklkid` 库以及 `ffsck` 包装器，因为 Ut-Linux 安装了更此的版本。

编译包：

```
make
```

要设置并运行测试套件，我们首先需要将 `/tools/lib` 中的一些库链接到测试程序查找的位置。要运行测试，请执行：

```
ln -sfv /tools/lib/lib(blk,uu)id.so.1 lib
make LD_LIBRARY_PATH=/tools/lib check
```

Linux From Scratch - 版本 8.0

其中一个 `E2ffspros` 测试将尝试分配 256 MB 的内存。如果你的 RAM 不够大，请确保为测试启用足够的交换空间（`swap space`）。参见第 2.5 节。

安装二进制文件、文档和共享库：

```
make install
```

安装静态库和头文件：

```
make install-libs
```

处理已安装的静态库，以便稍后删除调试符号：

```
chmod -v uw /usr/lib/(libcom_err,lib2p,libext2fs,libss).a
```

此包包含一个 gzipped 的 `.info` 文件，但不会更新系统目录。使用以下命令解压此文件并更新系统目录：

```
gunzip -v /usr/share/info/libext2fs.info.gz
install-info --dir-file=/usr/share/info/dir /usr/share/info/libext2fs.info
```

如果需要，可以使用以下命令创建额外的文档：



`makeinfo -o doc/com_err.info ..lib/et/com_err.texinfo`

`install -v -m644 doc/com_err.info /usr/share/info`

`install-info --dir-file=/usr/share/info/dir /usr/share/info/com_err.info`

### 6.49.2. E2fspros 的内容

- 安装的程序：
`badblocks`, `chattr`, `compile_et`, `debugfs`, `e2fsck`, `e2free`, `e2fsck`, `e2image`, `label2 deundo`, `e4defrag`, `fileck`, `fsckext2`, `fsckext3`, `fsckext4`, `logsave`, `lsattr`, `mk_kdms`, `mkfs2`, `mkfs`, `mkfs3`, `mkfs4`, `mkfs4dev`, `mklost+found`, `resize2`, and `tune2fs`
- 安装的库：
`libcom_err.so`, `lib2p`, `libext2fs.so`, `libss.so`
`/usr/include/e2p`, `/usr/include/ext2fs`, `/usr/include/ss`

#### 描述
- `badblocks`: 在设备上的坏块
- `chattr`: 修改文件属性
- `compile_et`: 将名称转换为代码
- `debugfs`: 文件系统的调试器
- `e2fsck`: 用于检查和修复
- `e2free`: 报告可用空间
- `e2image`: 用于创建
- `label2`: 为文件系统标记
- `e2undo`: 重放撤销操作
- `e4defrag`: 在线碎片整理
- `fileck`: 检查文件错误
- `fsckext2`: 检查 ext2 系统
- `fsckext3`: 检查 ext3 系统
- `fsckext4`: 检查 ext4 系统
- `logsave`: 保存日志输出
- `lsattr`: 列出文件属性
- `mk_kdms`: 创建字符串表
- `mkfs2`: 创建 ext2 系统
- `mkfs`: 创建文件系统
- `mkfs3`: 创建 ext3 系统
- `mkfs4`: 创建 ext4 系统
- `mkfs4dev`: 创建 ext4 开发系统
- `mklost+found`: 创建 lost+found 目录
- `resize2`: 增大或缩小文件系统
- `tune2fs`: 调整调优参数
- `libcom_err`: 通用错误例程
- `lib2p`: 用于 dumpefs
- `libext2fs`: 用于 lsattr
- `libss`: 用于 debugfs

修复某些权限，以便非根用户可以编译并运行测试：

```
chown -Rv nobody .
```

现在运行测试。确保 `su` 环境中的 `PATH` 包含 `/tools/bin`。

```
su nobody -s /bin/bash \
-c "PATH=$PATH make RUN_EXPENSIVE_TESTS=yes check"
```

已知 `test-login` 测试在虚拟控制台（如这里的 chroot 环境）上会失败，但在 X 终端中运行则可以通过。

删除临时组：

```
sed -i '/dummy/d' /etc/group
```

安装软件包：

```
make install
```

将程序移动到 FHS 指定的位置位置：

```
mv -v /usr/bin/{cat,chgrp,chmod,chown,cp,date,dd,df,de,echo} /bin
mv -v /usr/bin/{false,ls,mkdir,knod,mv,mv,pwd,rm} /bin
mv -v /usr/bin/{rmdir,stty,sync,true,uname} /bin
mv -v /usr/bin/chroot /usr/bin
mv -v /usr/share/man/man1/chroot.1 /usr/share/man/man8/chroot.8
sed -i s/\1\8"/1 /usr/share/man/man8/chroot
```

LFS-Bootscripts 软件包的部分依赖于 `head`、`sleep` 和 `nice`。由于在启动早期阶段可能无法使用 `/usr`，这些二进制文件不在根分区上：

```
mv -v /usr/bin/{head, sleep,nice,test,[]} /bin
```



## 65.2. Coreutils 目录

+ 已安装的程序：
- `base32`,`base64`,`basename`,`cat`,`chechon`,`chgrp`,`chmod`,`chroot`,`cksum`,`comm`,`cp`,`csplit`,`cut`,`dd`,`df`,`dir`,`dirname`,`du`,`echo`,`env`,`exp`,`factor`,`false`,`fmt`,`fold`,`groups`,`head`,`hostid`,`id`,`join`,`link`,`ln`,`logname`,`md5sum`,`mkdir`,`mkfind`,`mknod`,`mv`,`nil`,`nl`,`nohop`,`nproc`,`numfmt`,`od`,`path`,`patch`,`prnk`,`prntiv`,`pivot`,`pwd`,`readlink`,`realpath`,`rm`,`rmdir`,`runcon`,`seq`,`shalsum`,`sha224sum`,`sha256sum`,`sha384sum`,`sha512sum`,`shred`,`shuf`,`sleep`,`sort`,`split`,`stat`,`stdbuf`,`sum`,`sync`,`tac`,`tail`,`tee`,`test`,`timeout`,`tr`,`truncate`,`tsort`,`tty`,`uname`,`uniq`,`unlink`,`users`,`vdir`,`wc`,`wc`,`whoami`,`and yes`

+ 已安装的库：
- `/usr/libdbuf/coreutils`

## 描述

+ `base32`: 根据 base32 规范 (RFC 4648) 编码和解码数据
+ `base64`: 根据 base64 规范 (RFC 4648) 编码和解码数据
+ `basename`: 从文件名中删除路径和指定的后缀
+ `cat`: 将文件连接到标准输出
+ `chcon`: 更改文件和目录的安全上下文
+ `chgrp`: 更改文件和目录的组所有权
+ `chmod`: 将每个文件的权限更改为指定的模式；模式可以是要进行更改的符号表示，也可以表示新权限的八进制数
+ `chown`: 更改文件和目录的用户和组所有权
+ `chroot`: 使用指定的目录作为 / 目录运行命令
+ `cksum`: 打印每个指定文件的循环冗余检查 (CRC) 校验和和字节计数
+ `comm`: 比较两个排序后的文件，以三列输出唯一的行和共同的行
+ `cp`: 复制文件
+ `split`: 将文件分成多个新文件，根据给定的模式或行号进行分离，并输出每个新文件的字节数
+ `cut`: 打印行的部分，根据给定的字段或位置选择部分
+ `date`: 以指定的格式显示当前时间，或设置系统日期
+ `dd`: 使用块大小和数量复制文件，同时可选对其进行转换
+ `df`: 报告所有挂载文件系统的可用（已用）磁盘空间，或仅报告托管选取文件的系统
+ `dir`: 列出每个目录的内容（与 `ls` 命令相同）
+ `dircolors`: 输出用于 `LS_COLOR` 环境变量的命令，以更改 `ls` 使用的方案
+ `dirname`: 从文件名中删除目录后缀
+ `du`: 报告当前目录、每个给定目录（包括所有子目录）或每个给定文件使用的磁盘空间
+ `echo`: 显示指定的字符串
+ `env`: 在修改的环境中运行命令
+ `expand`: 将制表转换为空格
+ `expr`: 评估表达式
+ `factor`: 打印所有指定整数的质因数
+ `false`: 什么都不做，失败；它始终以失败的状态码退出
+ `fmt`: 重新格式化给定文件的段落
+ `fold`: 折叠给定文件的行
+ `groups`: 报告用户的组组成
+ `head`: 打印每个给定文件的前十行（或指定的行数）
+ `hostid`: 报告主机数字标识符（十六进制）
+ `id`: 报告当前用户或指定用户的有效 UID、GID 和组组成
+ `install`: 在复制文件的同时设置其权限模式，如果可能，还设置所有者和组
+ `join`: 合并两个文件中相同连接字段的行
+ `link`: 为文件创建指定名称硬链接
+ `logname`: 报告登录名
+ `md5sum`: 打印摘要消息5 (MD5) 校验和
+ `mkdir`: 创建目录
+ `mknod`: 创建设备节点
+ `mv`: 移动或重命名
+ `nl`: 为行编号
+ `nohop`: 运行一个可以挂断的命令
+ `nproc`: 报告处理器数量
+ `numfmt`: 将数字转换为可读格式
+ `od`: 以八进制转储文件
+ `path`: 报告路径
+ `patch`: 检查文件是否有效
+ `prnk`: 打印参数
+ `prntiv`: 打印索引
+ `pivot`: 切换
+ `pwd`: 报告工作目录
+ `readlink`: 报告符号链接的值
+ `realpath`: 报告解析后的路径
+ `rm`: 删除文件
+ `rmdir`: 删除空目录
+ `runcon`: 使用指定的安全上下文运行命令
+ `seq`: 生成数字序列
+ `shalsum`: 输出安全哈希算法
+ `sha224sum`: 打印 224 位安全哈希算法校验和
+ `sha256sum`: 打印 256 位安全哈希算法校验和
+ `sha384sum`: 打印 384 位安全哈希算法校验和
+ `sha512sum`: 打印 512 位安全哈希算法校验和
+ `shred`: 重复覆盖文件
+ `shuf`: 洗乱行
+ `sleep`: 暂停指定的时间
+ `sort`: 对行排序
+ `split`: 分割文件
+ `stat`: 显示文件或文件系统状态
+ `stdbuf`: 使用更改的缓冲运行命令
+ `sum`: 打印校验和块计数
+ `sync`: 刷新系统缓冲区
+ `tac`: 反向连接文件
+ `tail`: 打印最后十行
+ `tee`: 读取输入的同时写入标准输出
+ `test`: 比较值并检查文件类型
+ `timeout`: 在时间限制内运行命令
+ `tr`: 翻译、压缩和删除字符
+ `truncate`: 缩小文件
+ `tsort`: 执行拓扑排序
+ `tty`: 报告终端名称
+ `uname`: 报告系统信息
+ `unexpand`: 将空格转换为制表符
+ `uniq`: 去除连续相同行的重复
+ `unlink`: 删除指定的文件
+ `users`: 报告当前登录用户的用户名
+ `vdir`: 等于 -l
+ `wc`: 报告行、字和字节数
+ `who`: 报告谁登录
+ `whoami`: 报告与有效 UID 的用户名
+ `yes`: 重复输出“y”或指定的字符串

## 6.51. Diffutils-3.5

Diffutils 软件包包含显示文件或目录之间差异的程序。近似编译时间：0.4 SBU
所需的磁盘空间：30 MB

### 6.51.1. 安装 Diffutils

首先修复一个文件以便安装区域设置（locale）文件：

```
sed -i 's/:@mkdir_p@: /bin/mkdir -p:' po/Makefile.in.in
```

为编译准备 Diffutils：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

如需测试测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

### 6.51.2. Diffutils 目录

已安装的程序：`cmp`,`diff`,`diff3` 和 `sdiff`

#### 简要说明

- `cmp` 比较两个文件，并报告它们在字节上是否不同
- `diff` 比较两个文件或目录，并报告文件中哪些行不同
- `diff3` 按行比较三个文件
- `sdiff` 合并两个文件并交互式输出结果

## 6.52. Gawk-4.1.4

Gawk 软件包包含处理文本文件的程序。

近似编译时间：0.3 SBU
所需的磁盘空间：36 MB

### 6.52.1. 安装 Gawk

为编译准备 Gawk：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

如需测试测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

如果需要，安装文档：

```
mkdir -v /usr/share/doc/gawk-4.1.4
cp -v doc/{gawk.txt,.*{eps,pdf,jpg}} /usr/share/doc/gawk-4.1.4
```



### 6.52.2. Gawk 目录

- 已安装的程序：`awk` (指向 `gawk` 的链接), `gawk-4.1.4` 和 `igawk`
- 已安装的库：`filefuncs.so`, `fnmatch.so`, `fork.so`, `inplace.so`, `ordchr.so`, `readdir.so`, `readfile.so`, `revoutput.so`, `revwtoway.so`, `rwarray.so`, `testext.so` 和 `time.so`
- 已安装的目录：`/usr/lib/gawk`, `/usr/libexec/awk`, `/usr/share/gawk` 和 `/usr/share/doc/gawk-4.1.4`

#### 简要说明

- `awk` 指向 `gawk` 的链接
- `gawk` 用于处理文本文件的程序；它是 awk 的 GNU 实现
- `gawk-4.1.4` 指向 `gawk` 的硬链接
- `igawk` 使 `gawk` 包含文件的能力

## 6.53. Findutils-4.6.0

Findutils 软件包包含查找文件的程序。这些程序通过递归搜索目录树来创建、维护和搜索数据库（通常比递归查找更快，但如果数据库最近没有更新，则可能不可靠）。

近似编译时间：0.9 SBU
所需的磁盘空间：48 MB

### 6.53.1. 安装 Findutils

首先，抑制一个在某些机器上可能会无限循环的测试：

```
sed -i 's/test-lock..EXEET.//' tests/Makefile.in
```

为编译准备 Findutils：

```
./configure --prefix=/usr --localstatedir=/var/lib/locate
```

配置选项的含义：

> `--localstatedir`
此选项将 locate 数据库的位置更改为 `/var/lib/locate`，这符合 FHS 标准。

编译软件包：

```
make
```

如需测试测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

LFS-Bootscripts 中的某些脚本依赖于 find。由于在启动早期阶段 `/usr` 可能不可用，因此此程序需要位于根分区上。还需要修改 updateddb 脚本以创建一个显式路径：

```
mv -v /usr/bin/find /bin
sed -i 's/find=$$(BINDIR)|find=/bin|' /usr/bin/updateddb
```

### 6.53.2. Findutils 目录

已安装的程序：`code`, `find`, `locate`, `oldfind`, `updateddb` 和 `xargs`

#### 简要说明

- `code` 曾用于定位 locate 数据库；它是 fcrode 的祖先
- `find` 在目录树中搜索匹配指定标准的文件
- `locate` 搜索文件名数据库并报告包含给定字符串或匹配给定模式的名称
- `oldfind` find 的旧版本，使用不同的算法
- `updatedb` 更新 locate 数据库；它扫描整个文件系统（包括其他文件系统）
- `xargs` 可用于处理文件列表

## 6.54. Groff-1.22.3

Groff 软件包包含处理和格式化文本的程序。

近似编译时间：0.5 SBU
所需的磁盘空间：82 MB

### 6.54.1. 安装 Groff

Groff 期望在编译时配置纸张。对于用户，为编译准备 Groff：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

安装软件包：

```
make install
```

### 6.54.2. Groff 目录

已安装的程序：`addinfo`, `afmotid`, `chem`, `eqn`, `eqn2graph`, `giffmk`, `gylpond`, `gperl`, `gpinyin`, `grap2graph`, `indxb`, `lkbib`, `lookbib`, `mmrof`, `neqnn`, `nroff`, `pdfmon`, `pdfroff`, `pftops`, `pic`, `pic2graph`, `post-grohtml`, `preconv`, `pre-grohtml`, `refer`, `roff2dvi`, `roff2html`, `roff2pdf`, `roff2ps`, `roff2text`

#### 简要说明

- `addinfo` 创建字体度
- `afmotid` 创建一个字体文件
- `chem` 生成化学结构的预处理器
- `eqn` 为美国信息交换代码输出格式化方程
- `eqn2graph` 将方程转换为图像
- `giffmk` 标记 groff 之间的差异
- `gylpond` 将 groff 的输出转换为 lypond 语言
- `gperl` groff 的预处理器
- `gpinyin` 将中文拼音转换为 groff
- `grap2graph` 将图表转换为图像
- `indxb` 为参考文献数据库创建倒索引
- `lkbib` 搜索包含特定键的参考文献数据库
- `lookbib` 搜索参考文献数据库
- `mmrof` groff 的简单预处理器
- `neqnn` 为 ASCII 输出格式化方程
- `nroff` 使用 groff 执行 noff 命令的脚本
- `pdfmon` groff 的封装，便于 PDF 文档的生成
- `pdfroff` 使用 groff 创建 pdf 文档
- `pftops` 将 .pbf 格式的 PostScript 字体转换为 ASCII
- `pic` 将 troff 或 TeX 输入文件中的嵌入图片编译为它们可理解的命令
- `pic2graph` 将 PIC 图转换为图像
- `post-grohtml` 将 groff 的输出转换为 HTML
- `preconv` 将文件输入编码为 GNU troff 可理解的内容
- `pre-grohtml` 将 groff 的输出转换为 HTML
- `refer` 将文件内容复制到标准输出
- `roff2dvi` 将 roff 文件转换为 DVI 格式
- `roff2html` 将 GNU troff 的输出转换为 HTML
- `roff2pdf` 将 GNU troff 的输出转换为 PDF
- `roff2ps` 将 GNU troff 的输出转换为 PostScript
- `roff2text` 将 GNU troff 的输出转换为文本

Linux From Scratch - 版本 8.0

| `roff2html` | 将 roff 文件转换为 HTML 格式 |
| `roff2pdf` | 将 roff 文件转换为 PDF |
| `roff2ps` | 将 roff 文件转换为 ps 文件 |
| `roff2text` | 将 roff 文件转换为文本文件 |
| `roff2x` | 将 roff 文件转换为其他格式 |
| `soelim` | 读取文件并将形如 `.so file` 的行替换为所提文件的内容 |
| `tbl` | 将嵌入在 troff 输入文件中的表格描述编译为 troff 可识别的命令 |
| `tfemontid` | 创建供 groff -Tdvi 使用的字体文件 |
| `troff` | 与 Unix troff 具有高度兼容性；通常使用 groff 命令调用它，该命令将按照适当顺序并使用适当选项运行预处理器和后处理器 |

181

## 55. GRUB-2.02-beta3

GRUB 软件包包含通用统一引导加载程序（GRand Unified Bootloader）。
估算构建时间：0.8 SBU
所需的磁盘空间：142 MB

### 6.55.1. 安装 GRUB

为编译 GRUB 做准备：

```bash
./configure --prefix=/usr
--sbindir=/sbin
--sysconfdir=/etc
--disable-efiemu
--disable-werror
```

新配置选项的含义：

- `--disable-werror`
这允许在带有较新版本 Flex 引入的警告的情况下完成。
- `--disable-efiemu`
此选项通过禁用 LFS 不需要的功能和测试程序，最大限度地减少构建的内容。

编译软件包：

```bash
make
```

此软件包不带测试套件。

安装软件包：

```bash
make install
```



使用 GRUB 使你的 L 系统可启动将在第 8.4 节“使用 GRUB 设置启动过程”中进行讨论。

### 6.55.2. GRUB 的内容

已安装程序：
`grub-bios-setup`, `grub-editenv`, `grub-file`, `grub-fstest`, `grub-glue-efi`, `grub-install`, `grub-kbdcomp`, `grub-macless`, `grub-menulst2cfg`, `grub-mkconfig`, `grub-mkimage`, `grub-mklayout`, `grub-mknetid`, `grub-mkpasswd-pbkdf2`, `grub-mkrelpath`, `grub-mkrescue`, `grub-mkstandalone`, `grub-mkofname`, `grub-probe`, `grub-reboot`, `grub-render-label`, `grub-script-check`, `grub-set-default`, `grub-sparc64-setup`, 和 `grub-syslinux2cfg`

已安装目录：
`/usr/lib/grub`, `/etc/grub.d`, `/usr/share/grub`, 以及 `boot`（当首次运行 `grub-install` 时）

### 简介绍

- `grub-bios-setup`
是 `grub-install` 的辅助程序
- `grub-editenv`
用于编辑环境块的工具
- `grub-file`
检查文件是否为指定类型。
- `grub-fstest`
调试文件系统驱动程序的工具
- `grub-glue-efi`: 处理 ia32 和 amd64 EFI 镜像并根据 Apple 格式将其粘在一起。
- `grub-install`: 在你的驱动器上安装 GRUB
- `grub-kbdcomp`: 将 xkb 布局转换为 GRUB 识别的脚本
- `grub-macless`: 在 HFS 或 HFS+ 文件上进行 Mac 式的 bless
- `grub-menulst2cfg`: 将 GRUB Legacy menu.1st 转换为用于 GRUB 2 的 grub.cfg
- `grub-mkconfig`: 生成 grub 配置文件
- `grub-mkimage`: 制作一个 GRUB 可启动镜像
- `grub-mklayout`: 生成 GRUB 键盘布局文件
- `grub-mknetdir`: 准备 GRUB 网络启动目录
- `grub-mkpasswd-pbkdf2`: 生成一个用于启动菜单的加密 PBKDF2 密码
- `grub-mkrelpath`: 使系统路径相对于其根目录变为相对
- `grub-mkrescue`: 制作适用于软盘或 CDROM/DVD 的 GRUB 可启动镜像
- `grub-mkstandalone`: 生成独立镜像
- `grub-opathname`: 是一个用于设置 GRUB 设备路径的辅助程序
- `grub-probe`: 为定的路径或设备探测设备信息
- `grub-reboot`: 仅为下次启动设置 GRUB 的默认启动项
- `grub-render-label`: 为 Apple Mac 渲染 Apple .disk_label
- `grub-script-check`: 检查 GRUB 配置脚本的语法错误
- `grub-set-default`: 设置 GRUB 的默认启动项
- `grub-sparc64-setup`: 是 grub-setup 的辅助程序
- `grub-syslinux2cfg`: 将 syslinux 配置文件转换为 grub.cfg 格式

## 6.56. Less-481

该包含包含文本文件查看器。

估算构建时间：小于 0.1 SBU
所需的磁盘空间：5 MB

### 6.56.1. 安装 Less

为编译 Less 做准备：

```bash
./configure --prefix=/usr
--sysconfdir=/etc
```

配置选项的含义：
- `--sysconfdir=/etc`
这告诉程序在 `/etc` 中查找配置。

编译软件包：

```bash
make
```

此软件包不带测试套件。

安装软件包：

```bash
make install
```

使用 Less 使你的 L 系统可启动将在第 8.4 节“使用 Less 设置启动过程”中进行讨论。

### 6.56.2. Less 的内容

已安装程序：
`less`, `lesscho`, `lesskey`

### 简介绍

- `less` 分页器；它允许用户滚动、查找并跳转到标记。
- `lesscho` 需要将字符扩展为文件名。
- `lesskey` 用于指定 less 的绑定。

## 6.57. Gzip-1

该软件包包含压缩和解压缩的程序。
估算构建时间：0.1 SBU
所需的磁盘空间：1 MB

### 6.57.1. 安装 Gzip

为编译 Gzip 做准备：

```bash
./configure --prefix=/usr
--sysconfdir=/etc
```

编译软件包：

```bash
make
```

此软件包不带测试套件。

安装软件包：

```bash
make install
```

### 6.57.2. Gzip 的内容

已安装程序：
`gzip`, `gzipcho`, `gzipkey`

### 简介绍

| 程序 | 描述 |
| :--- | :--- |
| `gzip` | 压缩文件 |
| `gzipcho` | 需要将字符扩展为文件名 |
| `gzipkey` | 用于指定 gzip 的绑定 |

## 6.58. IPRoute2-4.9

IPRoute2 软件包包含基础和高级网络程序。
估算构建时间：0.2 SBU
所需的磁盘空间：1 MB

### 6.58.1. 安装 IPRoute2

为编译 IPRoute2 做准备：

```bash
./configure --prefix=/usr
--sysconfdir=/etc
```

此软件包中的 `arpd` 程序将不会构建，因为它依赖 LFS 未安装的 Berkeley DB。文档文件和 `arpd` 目录会被安装。通过运行以下命令防止这一点：

```bash
sed -i /Arpd/d Makefile
sed -i 's/arpd.8//' man/man8/Makefile
rm -v doc/arpd.sgml
```

还需要禁用一个需要 iptables 的模块。

```bash
sed -i 's/m_ipt.//' tc/Makefile
```

编译软件包：

```bash
make
```

此软件包没有可用的测试套件。

安装软件包：

```bash
make DOCDIR=/usr/share/doc/iproute2-4.9.0 install
```



### 6.58.2. IPRoute2 的内容

已安装程序：
`bridge`, `ctstat`, `genl`, `ifcfg`, `ifstat`, `ip`, `nstat`, `routef`, `rout`, `rtacct`, `rtmon`, `rptrp`, `rtlink`, `ss`, 和 `tc`

### 简介绍

- `bridge` 配置网络桥
- `ctstat` 连接状态工具
- `genl` 通用网路前端
- `ifcfg` `ip` 命令的 shell 封装 [注意它需要 `iputils` 软件包中的 `arping` 和 `rdisk` 程序，位于 `http://www.kb.net/iputils/`]
- `ifstat` 显示接口统计，包括通过接口发送和接收的数据包数量
- `ip` 主执行文件。它有多个不同的功能：
- `ip link` `<device>` 允许用户查看设备状态并进行更改
- `ip addr` 允许用户查看地址并添加新地址以及删除旧地址

`ip neighbor` 允许用户查看邻居绑定及其属性、添加新的邻居条目并删除旧条目

`ip rule` 允许用户查看路由策略并进行更改

`ip route` 允许用户查看路由表并更改路由表规则

`ip tunnel` 允许用户查看 IP 隧道及其属性并对其进行更改

`ip madr` 允许用户查看多播地址及其属性并对其进行更改

`ip mroute` 允许用户设置、更改或删除多播路由

`ip monitor` 允许用户持续监控设备、地址和路由的状态

`lnstat` 提供 Linux 网络统计数据；它是旧 `rstat` 程序的通用且功能更全的替代品

`nstat` 显示网络统计数据

- `ip route` 的组件。用于刷新路由表
- `ip route` 的组件。用于列出路由表
- 显示 `/proc/net/rt_acct` 的内容
- 路由监控工具
- 将 `ip -o` 的输出转换回可读格式
- 路由状态工具
- 类似于 `netstat` 命令；显示活动连接
- 流量控制执行程序；用于服务质量 (QOS) 和服务类别 (COS) 的实现
- `tc qdisc` 允许用户设置队列规则
- `tc class` 允许用户根据队列规则调度设置类
- `tc estimator` 允许用户估计进入网络的流量
- `tc filter` 允许用户设置 QOS/COS 数据包过滤
- `tc policy` 允许用户设置 QOS/COS 策略

## 6.59. Kbd-2.0.4

Kbd 软件包包含键表文件、控制台字体和键盘工具。

**近似编译时间：** 0.1 SBU
**所需磁盘空间：** 29 MB

### 6.59.1. 安装 Kbd

Kbd 包中不同键位的 Backspace 和 Delete 键的行为不一致。以下补丁修复了 i386 键盘的这个问题：

```
patch -Np1 -i ../kbd-2.0.4-backspace-1.patch
```

补丁后，Backspace 会产生代码为 127 的字符，Delete 会产生一个标准的转义序列。

删除冗余的 `resizecons` 程序（它替换了失效的 svgalib 以提供视频模式文件——正常使用应适当设置 `setfont` 大小）以及对应的 manage 程序。

```
sed -i '/RESIZECONS_PROGS=\)yes/\1no/g' configure
sed -i '/s/resizecons.8 //' docs/man/man8/Makefile.in
```

为编译 Kbd 准备：

```
PKG_CONFIG_PATH=/tools/lib/pkgconfig ./configure --prefix=/usr --disable-vlock
```

配置选项的含义：

```
--disable-vlock
```

此选项防止构建 `vlock` 工具，因为它需要 PAM 库，而该库在 chroot 环境中不可用。

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

> 注意：对于某些语言（例如白俄罗斯语），Kbd 软件包未为“by”键位提供有用的键位，该键位假设使用 ISO-8859-5 编码，通常使用 CP1251 键位。此类语言的用户必须单独下载可用的键位。

如果需要，安装文档：

```
mkdir -v /usr/share/doc/kbd-2.0.4
cp -R docs/doc/* /usr/share/doc/kbd-2.0.4
```

### 6.59.2. Kbd 目录

安装的程序：`chvt`, `dealloc`, `dumpkeys`, `fgconsole`, `getkeys`, `kbdinfo`, `kbd_mode`, `kbdrate`, `loadkeys`, `loadunimap`, `mapscr`, `openvt`

安装的目录：`/usr/share/consolefonts`, `/usr/share/consolecion`, `/usr/share/keymaps`, `/usr/share/doc/kbd-2.0.4` 以及 `/usr/share/unimap`

## 简述

- `chvt`: 切换虚拟终端
- `dealloc`: 释放未使用的虚拟终端
- `dumpkeys`: 转储键位表
- `fgconsole`: 打印活动虚拟终端编号
- `getkeys`: 打印内核扫描码到键码的映射表
- `kbdinfo`: 获取控制台状态信息
- `kbd_mode`: 报告或设置键盘模式
- `kbdrate`: 设置键盘重复和延迟
- `loadkeys`: 加载键位表
- `loadunimap`: 加载内核 Unicode 到字体的映射表
- `mapscr`: 过时的程序，用于将用户定义的输出字符映射表加载到控制台驱动程序；现在由 `setfont` 完成
- `openvt`: 在新的虚拟终端 (VT) 上启动程序
- `psfaddtable`: 为控制字体添加 Unicode 字符表
- `psfgettable`: 从控制字体提取嵌入的 Unicode 字符表
- `psfstriptable`: 从控制字体移除嵌入的 Unicode 字符表
- `psfxtable`: 处理 Unicode 字符表
- `setfont`: 修改控制台
- `setkeys`: 设置控制台
- `settled`: 设置控制台
- `metamode`: 设置控制台
- `setvrgb`: 设置控制台
- `showconsolefont`: 显示控制台字体
- `unicode_start`: 启动控制台
- `unicode_stop`: 停止控制台

# syslogd

记录系统程序提供的日志消息。[每条被记录的日志至少包含一个时间戳和一个主机名，通常还包括程序名称，但这取决于对日志守护进程设置的信赖程度。]

## 64.4. Sysvinit-2.88dsf

Sysvinit 软件包包含了控制系统启动、运行和关闭的程序。

预计编译时间：少于 0.1 SBU
所需磁盘空间：1.1 MB

### 64.4.1. 安装 Sysvinit

首先，应用一个补丁以移除其他软件包安装的程序，澄清一条信息，并修复一个编译器警告：

```
patch -Np1 -i ../sysvinit-2.88dsf-consolidated-1.patch
```

编译该包：

```
make -C src
```

该软件包不带有测试套件。

安装该包：

```
make -C src install
```



### 64.4.2. Sysvinit 包含内容

**已安装的程序：** `bootlogd`, `fstab-decode`, `halt`, `init`, `killall5`, `poweroff`（链接到 `halt`）, `reboot`（链接到 `halt`）, `runlevel`, `shutdown`, 以及 `telinit`（链接到 `init`）

#### 简述

- `bootlogd` 将启动日志记录到日志文件
- `fstab-decode` 使用 `fstab` 编码的参数运行命令
- `halt` 通常情况下带 `-h` 选项调用 `shutdown`，除非已处于运行级别 0，在那种情况下，它会通知内核停止系统；它会在文件 `/var/log/tmp` 中记下系统已关机
- `init` 内核初始化硬件时启动的第一个进程，它接管启动过程并启动其配置文件中指定的所有进程
- `killall5` 向所有进程发送信号，但你当前会话中的进程除外，因此它不会杀死其父 shell
- `power` 告诉内核停止系统并关闭计算机（`halt`）
- `reboot` 告诉内核重启系统（`halt`）
- `runlevel` 报告之前的和当前的运行级别，如 `/var/run/utmp` 中最后一次运行级别记录所示
- `shutdown` 以安全的方式关闭系统，向所有进程发送信号并通知所有登录用户
- `telinit` 告诉 `init` 切换到哪个运行级别

## 6.65. Eudev-3.2.1

`Eudev` 软件包包含了动态创建设备节点的程序
预计编译时间：0.2 SBU
所需磁盘空间：78 MB

### 6.65.1. 安装测试脚本

首先，修复测试脚本：

```
sed -r -i 's|/usr/(bin/test)|\1|g' test/udev-test.pl
```

接下来，移除一行导致编译失败的用行：

```
sed -i '/keyboard_lookup_key/' src/udev/udev-builtin-keyboard.c
```

接下来，添加一个变通方案，以防止 `/tools` 目录被硬编码到 Eudev 二进制文件路径中：

```
cat > config.cache << "EOF"

HAVE_BLKID=1

BLKID_LIBS="-lblkid"

BLKID_CFLAGS="-I/tools/include"

EOF
```

为编译 Eudev 准备工作：

```
./configure --prefix=/usr \
  --bindir=/sbin \
  --sbindir=/sbin \
  --libdir=/usr/lib \
  --sysconfdir=/etc \
  --libexecdir=/lib \
  --with-rootprefix \
  --with-rootlibdir=/lib \
  --enable-manpages \
  --disable-static \
  --config-cache
```

编译该包：

```
LIBRARY_PATH=/tools/lib make
```

现在创建测试需要的、也将作为安装一部分的目录：

```
mkdir -pv /lib/udev/rules.d
mkdir -pv /etc/udev/rules.d
```

要测试结果，执行：

```
make LD_LIBRARY_PATH=/tools/lib check
```

安装该包：

```
make LD_LIBRARY_PATH=/tools/lib install
```

安装一些在 LFS 环境中实用的自定义规则和设置文件：

```
tar -xvf ../udev-lfs-20140408.tar.bz2
make -f udev-lfs-20140408/Makefile.lfs install
```

### 6.65.2. 配置 Udev

硬件设备的信息维护在 `/etc/udev/hwdb.d` 和 `/usr/lib/udev.d` 目录下。`udev` 需要将信息编译成二进制数据库 `/etc/udev/hwdb.bin`。创建初始数据库：

```
LD_LIBRARY_PATH=/tools/lib udevadm hwdb --update
```

此命令在每次硬件信息更新时都需要运行。

### 6.65.3. Udev 包含内容

- 安装的程序：`udevadm` 和 `udevd`
- 安装的库：`libudev.so`
- 安装的目录：`/etc/udev`, `/lib/udev`, 以及 `/usr/share/doc/udev-20140408`

#### 简述

- `udevadm`: 通用 `udev` 管理工具：控制 `udev` 守护进程，提供来自 `udev` 数据库的信息，监控 `uevents`，等待 `uevents` 完成，并为给定设备触发 `uevents`
- `udevd`: 监听 `netlink` 套接字 `uevents` 的守护进程，创建设备并响应这些事件运行外部程序
- `libudev`: `udev` 的库接口
- `/etc/udev`: 包含设备命名的 `udev` 配置、权限和规则

## Util-linux-2.29.1

`Util-linux` 软件包包含了各种杂用程序。其中包含处理文件系统、控制台、分区和消息的工具。

预计编译时间：1.0 SBU
所需磁盘空间：6 MB

### FHS 合规性

FHS 建议使用 `/var/lib/hwclock` 代替通常的 `/etc` 目录作为 `adjtime` 位置。为存储 `hwclock` 创建目录：

```
mkdir -pv /var/lib/hwclock
```

### 6.65.2. 安装 Util-linux

为编译 `Util-linux` 准备工作：

```
./configure ADJTIME_PATH=/var/lib/hwclock/adjtime \
  --docdir=/share/doc/util-linux \
  --disable-chsh \
  --disable-login \
  --disable-ologin
```

编译该包：

```
make
```

如果需要，以 root 用户运行测试套件：

```
make
```

**注意**：在重启后可以安全地运行，LFS 目录：

```bash
=$PWD
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
=$PATH"
```

**注意**：在重启后可以安全地运行，LFS 目录：

```chown -Rv nobody
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
=$PWD
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
,mkfs, mkfs.min
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
,make
```

**注意**：在重启后可以安全地运行，LFS 目录：

```
,mkfs.cramfs, mkfs.min, mkswap
```

安装该包：

```
make install
```



### 6.65.3. Util-linux 包含内容

- 安装的程序：`addpart`, `aget`, `biskard`, `blkid`, `blockdev`, `cal`, `cfdisk`, `chcpu`, `chrt`, `col`, `colert`, `colm`, `column`, `crtalldel`, `delpart`, `dmesg`, `fstrim`, `fallocate`, `fdisk`, `finds`, `findmd`, `flock`, `fsk`, `fsk.cramfs`, `mkfs`, `mkfs.minix`, `mkswap`, `mount`, `mountpoint`, `name`, `parts`, `script`, `pivot_root`, `prlimit`, `profile`, `rename`, `resize`, `reswarp`, `rtwck`, `retretay`, `setsid`, `setter`, `sfdisk`, `ulogin`, `swagen`, `swappart`（链接到 `swap`）, `switch`, `switch_root`, `tailset`, `ul`, `umount`, `uname`, `unshare`, `utmpdd`, `uidd`, `ualigen`, `wall`, `wetird`, `weipes`, `x86`, `x64`
- 安装的库：`libblkid.so`, `libdisk.so`, `libmount.so`, `libsmartcols.so`, `libuuid`
- 安装的目录：`/usr/include`, `/usr/share/doc/util-linux-2.29.1`, `/var/lib/hwclock`

## 简述

- `addpart` 通知内核有新分区
- `agety` 打开 tty 端口，提示登录名，然后调用登录程序
- `biskard` 丢弃设备上的扇区
- `blkid` 用于定位和打印块设备属性的命令行工具
- `blockdev` 允许从命令行调用块设备 ioctls
- `cal` 显示简单的日历
- `cfdisk` 操作给定设备的分区表
- `chcpu` 修改 CPU 状态
- `chrt` 修改进程的实时属性
- `col` 过滤掉重复换行符
- `colert` 为缺少某些功能（如叠加和半行）的终端过滤输出
- `colm` 过滤掉指定的列
- `column` 将文件格式化为多列
- `crtalldel` 将 Ctrl+Alt+Del 键组合设置为硬重启或软重置
- `delpart` 请求内核删除分区
- `dmesg` 倾储内核启动消息
- `fstrim` 整理磁盘空间
- `fallocate` 分配文件空间
- `fdisk` 分区工具
- `finds` 查找节点
- `findmd` 查找挂点
- `flock` 锁
- `fsk` 检查文件系统
- `fsk.cramfs` 检查 cramfs 文件系统
- `mkfs` 创建文件系统
- `mkfs.minix` 创建 minix 文件系统
- `mkswap` 创建交换空间
- `mount` 挂载
- `mountpoint` 检查挂载点
- `name` 命名
- `parts` 查看分区信息
- `script` 脚本工具
- `pivot_root` 切换根目录
- `prlimit` 进程资源限制
- `profile` 进程配置文件
- `rename` 重命名
- `resize` 调整大小
- `reswarp` 调整重写
- `rtwck` 检查
- `retretay` 返回
- `setsid` 设置会话 ID
- `setter` 设置器
- `sfdisk` 磁盘分区工具
- `ulogin` 用户登录
- `swagen` 交换
- `swappart`（链接到 `swap`）
- `switch` 切换
- `switch_root` 切换根目录
- `tailset` 跟踪集
- `ul` 用户工具
- `umount` 卸载
- `uname` 输出内核信息
- `unshare` 共享命名空间
- `utmpdd` 登录记录
- `uidd` 唯一 ID
- `ualigen` 生成 ID
- `wall` 广播消息
- `wetird` 写入擦写
- `weipes` 擦除
- `x86` x86 架构
- `x64` 64 位架构

# 从零构建 Linux (Linux) - 版本 8.0

- `fallocate`
为文件预分配空间

- `fdformat`
低级格式化软磁盘

- `fdisk`
操作给定设备的分区表

- `findfs`
通过标签 (`label`) 或全局唯一标识符 (`UUID`) 查找文件系统

- `findmtnt`
是 `libmount` 的命令行接口，包含 `mountinfo`、`fstab` 和 `mtab` 文件的处理

- `flock`
获取文件锁并在持有锁的情况下执行命令

- `fsck`
用于检查并（可选）修复文件系统

- `fsck.cranfs`
对给定设备上的 Cramfs 文件系统进行一致性检查

- `fsck.minix`
是 MIFFREEZE/FITHAW ioctl 内核驱动操作的非常简单的封装器

- `fsfreez`
丢弃已挂载文件系统中未使用的块

- `getopt`
解析给定命令行中的选项

- `hexdump`
以十六进制或其他格式转储文件系统

- `hwclock`
读取或设置系统硬件时钟，也称为实时时钟 (`RTC`) 或基本输入输出系统 (`BIOS`) 时钟

- `i386`
指向 `setarch` 的符号链接

- `ionice`
获取或设置程序的调度类和优先级

- `ipcmk`
创建 IPC 资源

- `ipcrm`
删除给定的进程间通信 (`IPC`) 资源

- `ipcs`
提供 iso9660 文件系统的大小

- `isize`
报告 iso9660 文件系统的大小

- `kill`
向进程发送信号

- `last`
显示哪些用户已登录（登录和登出），回溯搜索 `/var/log/wtmp` 文件；它显示了系统启动、关机和运行级别的更改

- `lastb`
显示记录在 `/var/log/btmp` 中的失败登录尝试

- `ldattach`
在串行线上附加行规律 (`line discipline`)

- `linux32`
指向 `setarch` 的符号链接

- `linux64`
指向 `setarch` 的符号链接

- `logger`
将给定消息输入系统日志。显示以给定字符串开头的行

- `look`
显示以给定字符串开头的行

- `losesetup`
设置并控制循环设备

- `lsblk`
以树状格式列出所有或选定块设备的信息

- `cpu`
打印 CPU 架构信息

- `lsipc`
打印系统当前使用的 IPC 设施信息

- `islocks`
列出本地系统锁

- `lslogins`
列出用户、组和系统账户的信息

- `cookie` | 为 `xauth` 生成魔法 쿠기（128 位随机十六进制数）

- `mesg` | 控制其他用户是否可以向当前用户的终端发送消息

- `mkfs` | 在设备上（通常是硬盘分区）上构建文件系统

- `mkfs.bfs` | 创建 Santa Cruz Operations (SCO) bfs 文件系统

- `mkfs.ramfs` | 创建 cramfs 文件系统

- `mkfs.minix` | 创建 Minix 文件系统

- `mkswap` | 初始化给定的设备或文件以作为交换区域 (`swap area`)

- `more` | 一页一页翻页文本的过滤器

- `mount` | 将给定设备上的文件系统挂载到文件系统树中的指定目录

- `mountpoint` | 检查目录是否为挂载点

- `namei` | 显示给定路径中的符号链接

- `nsenter` | 使用其他进程的命名空间运行程序

- `partx` | 告知内核磁盘上分区的存在和数量

- `pg` | 一页一页显示文本文件

- `pivot_root` | 将给定的文件系统设置为当前进程的新根文件系统

- `prlimit` | 获取并设置进程资源限制

- `raw` | 将原始字符设备绑定到块设备

- `readfile` | 读取内核分析信息

- `rename` | 重命名给定文件，用一个字符串替换为另一个

- `renice` | 更改运行进程的优先级

- `resizepart` | 请求内核调整分区大小

- `rev` | 反转给定文件的行

- `rwake` | 用于进入系统睡眠状态，直到指定的唤醒时间

- `script` | 创建终端会话类型

- `scriptreplay` | 使用计时信息回放脚本

- `setarch` | 在新的程序环境中更改报告的架构并设置特性标志

- `setid` | 在新会话中运行给定程序

- `seterm` | 设置终端属性

- `sfdisk` | 磁盘分区器

- `sologin` | 允许 root 登录；通常系统进入单用户模式时由 `init` 调用

- `swapable` | 允许更改交换区的 UUID 和标签

- `swapoff` | 禁用分页和交换的设备和文件，并列出当前使用的设备和文件

- `swapon` | 切换到另一个文件系统作为挂载树的根

- `tail` | 跟踪日志文件的增长；显示日志文件的最后 10 行，然后在日志文件创建新条目时继续显示

- `taskset`
检索或设置进程的 CPU 亲和性

- `ul`
将下划线转换为指示中使用终端下划线序列的过滤器

- `umount`
从系统文件树中断开文件系统

- `uname26`
指向 `setarch` 的符号链接

- `unshare` | 在某些命名空间与父进程分离的情况下运行程序

- `utmpdump`
以用户友好的格式显示 uuid 登录文件的内容

- `uuididd`
UUID 库使用的守护进程，以安全且保证唯一的方式生成基于时间的 UUID

- `uuidigen`
创建新的 UUID。每个新 UUID 在本地系统和其他系统上创建的所有 UUID 之间都可以被认为是唯一的

- `wall` | 显示所有当前登录终端的文件内容或其标准输入，在过去和未来

- `wdctl`
显示看门狗状态

- `whereis`
报告给定命令的位置、源和 man 页

- `wipefs`
擦除设备上的文件系统签名

- `x86_64`
指向 `setarch` 的符号链接

- `zramctl`
设置并控制 `zram`（内存磁盘）设备的程序

- `libblkid`
包含设备识别例程

- `libdisk`
包含操作分区表的例程

- `libmount`
包含块设备挂载和卸载的例程

- `libsmartcols`
包含表格形式输出的例程

- `libuuid`
包含生成超出本地系统的唯一标识符的例程

# 6.7. Man-DB

- `fsck.cranfs`
对给定设备上的 Cramfs 文件系统进行一致性检查

- `fsck.minix`
是 MIFFREEZE/FITHAW ioctl 内核驱动操作的非常简单的封装器

- `fsfreez`
丢弃已挂载文件系统中未使用的块

- `getopt`
解析给定命令行中的选项

- `hexdump`
以十六进制或其他格式转储文件系统

- `hwclock`
读取或设置硬件时钟，也称为实时时钟 (`RTC`) 或基本输入输出系统 (`BIOS`) 时钟

- `i386`
指向 `setarch` 的符号链接

- `ionice`
获取或设置程序的调度类和优先级

- `ipcmk`
创建 IPC 资源

- `ipcrm`
删除给定的进程间通信 (`IPC`) 资源

- `ipcs`
提供 iso9660 文件系统的大小

- `isize`
报告 iso9660 文件系统的大小

- `kill`
向进程发送信号

- `last`
显示哪些用户已登录（登录和登出），回溯搜索 `/var/log/wtmp` 文件；它显示了系统启动、关机和运行级别的更改

- `lastb`
显示记录在 `/var/log/btmp` 中的失败登录尝试

- `ldattach`
在串行线上附加行规律

- `linux32`
指向 `setarch` 的符号链接

- `linux64`
指向 `setarch` 的符号链接

- `logger`
将给定消息输入系统日志。显示以给定字符串开头的行

- `look`
显示以给定字符串开头的行

- `losesetup`
设置并控制循环设备

- `lsblk`
以树状格式列出所有或选定块设备的信息

- `iscpu`
打印 CPU 架构信息

- `lsipc`
打印系统当前使用的 IPC 设施信息

- `islocks`
列出本地系统锁

- `lslogins`
列出用户、组和系统账户的信息

- `cookie` | 为 `xauth` 生成魔法 쿠기（128 位随机十六进制数）

- `mesg` | 控制其他用户是否可以向当前用户的终端发送消息

- `mkfs` | 在设备上（通常是硬盘分区）上构建文件系统

- `mkfs.bfs` | 创建 Santa Cruz Operations (SCO) bfs 文件系统

- `mkfs.ramfs` | 创建 cramfs 文件系统

- `mkfs.minix` | 创建 Minix 文件系统

- `mkswap` | 初始化给定的设备或文件以作为交换区域

- `more` | 一页一页翻页文本的过滤器

- `mount` | 将给定设备上的文件系统挂载到文件系统树中的指定目录

- `mountpoint` | 检查目录是否为挂载点

- `namei` | 显示给定路径中的符号链接

- `nsenter` | 使用其他进程的命名空间运行程序

- `partx` | 告知内核磁盘上分区的存在和数量

- `pg` | 一页一页显示文本文件

- `pivot_root` | 将给定的文件系统设置为当前进程的新根文件系统

- `prlimit` | 获取并设置进程资源限制

- `raw` | 将原始字符设备绑定到块设备

- `readfile` | 读取内核分析信息

- `rename` | 重命名给定文件，用一个字符串替换为另一个

- `renice` | 更改运行进程的优先级

- `resizepart` | 请求内核调整分区大小

- `rev` | 反转给定文件的行

- `rwake` | 用于进入系统睡眠状态，直到指定的唤醒时间

- `script` | 创建终端会话类型

- `scriptreplay` | 使用计时信息回放脚本

- `setarch` | 在新的程序环境中更改报告的架构并设置特性标志

- `setid` | 在新会话中运行给定程序

- `seterm` | 设置终端属性

- `sfdisk` | 磁盘分区器

- `sologin` | 允许 root 登录；通常系统进入单用户模式时由 `init` 调用

- `swapable` | 允许更改交换区的 UUID 和标签

- `swapoff` | 禁用分页和交换的设备和文件，并列出当前使用的设备和文件

- `swapon` | 切换到另一个文件系统作为挂载树的根

- `tail` | 跟踪日志文件的增长；显示日志文件的最后 10 行，然后在日志文件创建新条目时继续显示

- `taskset`
检索或设置进程的 CPU 亲和性

- `ul`
将下划线转换为指示中使用终端下划线序列的过滤器

- `umount`
从系统文件树中断开文件系统

- `uname26`
指向 `setarch` 的符号链接

- `unshare` | 在某些命名空间与父进程分离的情况下运行程序

- `utmpdump`
以用户友好的格式显示 uuid 登录文件的内容

- `uuididd`
UUID 库使用的守护进程，以安全且保证唯一的方式生成基于时间的 UUID

- `uuidigen`
创建新的 UUID。每个新 UUID 在本地系统和其他系统上创建的所有 UUID 之间都可以被认为是唯一的

- `wall` | 显示所有当前登录终端的文件内容或其标准输入，在过去和未来

- `wdctl`
显示看门狗状态

- `whereis`
报告给定命令的位置、源和 man 页

- `wipefs`
擦除设备上的文件系统签名

- `x86_64`
指向 `setarch` 的符号链接

- `zramctl`
设置并控制 `zram`（内存磁盘）设备的程序

- `libblkid`
包含设备识别例程

- `libdisk`
包含操作分区表的例程

- `libmount`
包含块设备挂载和卸载的例程

- `libsmartcols`
包含表格形式输出的例程

- `libuuid`
包含生成超出本地系统的唯一标识符的例程

# 6.7. Man-DB

| Language (code) | Encoding | Language (code) | Encoding |
| --- | --- | --- | --- |
| Danish (da) | ISO-8859-1 | Croatian (hr) | ISO-8859-2 |
| German (de) | ISO-8859-1 | Hungarian (hu) | ISO-8859-2 |
| English (en) | ISO-8859-1 | Japanese (ja) | EUC-JP |
| Spanish (es) | ISO-8859-1 | Korean (ko) | EUC-KR |
| Estonian (et) | ISO-8859-1 | Lithuanian (lt) | ISO-8859 |
| Finnish (fi) | ISO-8859-1 | Latvian (lv) | ISO-8859-1 |
| French (fr) | ISO-8859-1 | Macedonian (mk) | ISO-8859-5 |
| Irish (ga) | ISO-8859-1 | Polish (pl) | ISO-8859-2 |
| Galician (gl) | ISO-8859-1 | Romanian (ro) | ISO-8859-2 |
| Indonesian (id) | ISO-8859-1 | Russian (ru) | KOI8-R |
| Icelandic (is) | ISO-8859-1 | Slovak (sk) | ISO-8859-2 |
| Italian (it) | ISO-8859-1 | Slovenian (sl) | ISO-8859-2 |
| Norwegian Bokmål (nb) | ISO-8859-1 | Serbian Latin (sr@cat) | ISO-8859-2 |
| Norwegian Nynorsk (nn) | ISO-8859-1 | Serbian (sr) | ISO-8859-5 |
| Norwegian (no) | ISO-8859-1 | Turkish (tr) | ISO-8859-9 |
| Portuguese (pt) | ISO-8859-1 | Ukrainian (uk) | KOI8-U |
| Swedish (sw) | ISO-8859-1 | Vietnamese (vi) | TCVN5712-1 |
| Belarus (be) | CP1251 | Simplified Chinese (zh_CN) | GBK |
| Bulgarian (bg) | CP1251 | Simplified Chinese, Singapore (zh_SG) | |
| Czech (cs) | ISO-8859-2 | Traditional Chinese, Hong Kong (zh_HK) | BIG5HKSCS |
| Greek (el) | ISO-8859-7 | Traditional Chinese (zh_TW) | BIG5 |

## 简述

`accessdb` 以人类可读的形式导出 `whatis` 数据库的内容

`apropos` 搜索 `whatis` 数据库并显示包含给定字符串的系统命令的短描述

`catman` 创建或更新预格式化的帮助页

`lexgrog` 显示给定帮助页的单行摘要信息

`man` 格式化并显示所请求的帮助页

`mandb` 创建或更新 `whatis` 数据库

`manpath` 显示 `$MANPATH` 的内容，或者（如果未设置 `$MANPATH`）显示基于 `man.conf` 设置和用户环境的合适搜索路径

`whatis` 搜索 `whatis` 数据库并显示包含给定关键词（作为独立单词）的系统命令的短描述

`libman` 包含 `man` 的运行时支持

`libmandb` 包含 `man` 的运行时支持

# 68. Tar-1.29

Tar 软件包包含一个归档程序。
预计编译时间：3.2 SBU
所需磁盘空间：40 MB

## 6.68.1. 安装 Tar

为编译准备 Tar：

```



`FORCE_UNSAFE_CONFIGURE=1` \
`./configure --prefix=/usr` \
`--bindir=/bin`

配置选项的含义：

`FORCE_UNSAFE_CONFIGURE=1`
这强制以 root 身份运行 `mknod`。通常情况下，作为 root 用户进行此测试被认为是危险的，但由于它运行在一个仅部分构建的系统上，覆盖它是可以的。

编译软件包：

```
make
```

测试结果（约 1 SBU），执行：

```
make check
```

安装软件包：

```
make install
make -C doc install-html docdir=/usr/share/doc/tar-1.29
```

### 6.68.2. tar 的内容

已安装程序：`tar`
已安装目录：`/usr/share/doc/tar-1.29`

# 简述

`tar`: 创建、从文件中提取文件并列出归档（也称为 tarballs）的内容

## 6.69. Texinfo-6.3

Texinfo 软件包包含用于读取、写入和转换 info 页的程序。

预计编译时间：0.5 SBU
所需磁盘空间：108 MB

### 6.69.1. 安装 Texinfo

为编译准备 Texinfo：

```
./configure --prefix=/usr --disable-static
```

配置选项的含义：

`--disable-static`
在这种情况下，顶层配置脚本将报错这是一个无法识别的选项，但 XSPParagraph 的配置脚本会识别它并使用它来禁用将静态 XSPParagraph 安装到 `/usr/lib/texinfo`。

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

可选地，安装属于 TeX 安装的组件：

```
make TEXMF=/usr/share/texmf install-tex
```

make 参数的含义：

`TEXMF=/usr/share/texmf`
`TEXMF` 变量持有 TeX 树根目录的位置，例如，TeX 软件包稍将安装在此处。

info 文档系统使用纯文本文件来存储其菜单项列表。文件位于 `/usr/share/info/dir`。遗憾的是，由于各种软件包 Makefile 中偶尔出现问题，它可能会与系统上安装的 info 页不同步。如果需要重建 `/usr/share/info/dir` 文件，可以使用以下命令完成任务：

```
pushd /usr/share/info

rm -v dir

for f in *
  do install-info $f 2>/dev/null
done

popd
```

### 6.69. Texinfo 的内容

已安装程序：`info`, `install-info`, `makeinfo` (链接到 `texiany`), `pdftexi2dvi`, `pod2texi`, `texiany`, `texi2pdf` 和 `texindex`

已安装库：`XSparagraph`

已安装目录：`/usr/share/texinfo` 和 `/usr/lib/texinfo`

# 简述

- `info`: 用于读取 info 页，这些页与 man 页类似，但通常比解释所有可用的命令行选项深入得多。[例如，比较 `man bison` 和 `info bison`。]
- `install-info`: 用于安装 info 页；它更新 info 索引文件中的条目
- `makeinfo`: 将指定的 Texinfo 源文档转换为 info 页、纯文本或 HTML
- `pdftex2dvi`: 用于将指定的 Texinfo 文档格式化为便携文档格式 (PDF) 文件
- `pod2texi`: 将 Pod 转换为 Texinfo格式
- `texiany`: 将 Texinfo 源文档翻译为各种其他格式
- `texi2dvi`: 用于将指定的 Texinfo 文档格式化为可以打印的设备无关文件
- `texi2pdf`: 用于将指定的 Texinfo 文档格式化为便携文档格式 (PDF) 文件
- `texindex`: 对 Texinfo 索引文件排序

## 67.0. Vim-8.0.069

Vim 软件包包含一个强大的文本编辑器

预计编译时间：1.3 SBU
所需磁盘空间：141 MB

如果你更倾向于其他编辑器——例如 Emacs、Joe 或 Nano——请参考 http://www.linuxfrom.org/blfs/view/8.0.html。

### 67.0.1. 安装 Vim

为编译准备 Vim：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

测试结果（约 1 SBU），执行：

```
make check
```

安装软件包：

```
make install
```

### 67.0.20. 配置 Vim

默认情况下，vim 以不兼容模式运行。这对于使用过其他编辑器的用户来说可能是新的。下方包含了“不兼容”设置，以突出正在使用新行为的事实。它还提醒那些想要更改为“兼容”模式的用户，这应该是配置中的第一个设置。运行以下命令创建默认配置文件：

```
cat /etc/vimrc << "EOF"

  Begin /etc/vimrc

set nocompat

set backspace=2

set mouse=r

syntax on

if ($term == "xterm") || ($term == "putty")

  set background=dark

endif

  End /etc/vimrc

EOF
```

通过运行以下命令可以获取其他可用选项的文档：

```
vim -c 'options:'
```

### 6.70.3. Vim 的内容

已安装程序：`ex`（链接到 `vim`）、`rview`（链接到 `vim`）、`rvim`（链接到 `vim`）、`vi`（链接到 `vim`）、`view`（链接到 `vim`）、`vim`、`vimdiff`（链接到 `vim`）、`vimtutor` 和 `xxd`

安装目录：`/usr/share/vim`

#### 简要描述

- `ex` 以 ex 模式启动 vim
- `rview` 是 `view` 的受限版本；无法启动 shell 命令且 view 无法被挂起
- `rvim` 是 vim 的受限版本；无法启动 shell 命令且 vim 无法被挂起
- `vi` 链接到 vim
- `view` 以只读模式启动 vim
- `vim` 是编辑器
- `vimdiff` 使用 vim 编辑两个或三个版本的文件并显示差异
- `vimtutor` 教授 vim 的基本键和命令
- `xxd` 创建给定文件的十六进制转储（hex dump）；它也可以进行反向操作，因此可用于二进制补丁

## 6.71. 关于调试符号

大多数程序和库默认情况下编译时都包含调试符号（使用 `gcc -g` 选项）。这意味着当你调试一个编译了调试信息的程序或库时，调试器不仅能提供内存地址，还能提供例和变量的名称。

然而，包含这些调试符号会显著增大程序或库的大小。以下是这些符号所占空间的示例：

- 带有调试符号的 bash 二进制文件：1200 KB
- 不带调试符号的 bash 二进制文件：480 KB
- 带有调试符号的 Glibc 和 GCC 文件 (`/lib` 和 `/usr/lib`)：87 MB
- 不带调试符号的 Glibc 和 GCC 文件：16 MB

大小取决于取决于使用的编译器和 C 库，但在比较带有和不带调试符号的程序时，差异将在两到五倍之间。

大多数用户永远不会在系统软件上使用调试器，通过移除这些符号可以恢复大量的磁盘空间。下一节将展示如何从程序和库中剥离调试符号。

## 6.72. 再次剥离

如果目标用户不是程序员且没有计划对系统软件进行任何调试，通过从二进制文件和库中移除调试符号，可以减少约 90 MB 的空间。除了无法完全调试软件外，不会带来任何不便。

大多数使用下方命令的人不会遇到任何困难。然而，很容易拼写错误导致新系统无法使用，因此在运行 `strip` 命令之前，对当前状态下的 LFS 系统进行备份是一个好主意。

在剥离之前，要特别确保没有要被剥离的二进制文件正在运行。如果不确定用户是否使用了第 6.4 节“进入 chroot 环境”中的命令进入 chroot，请先退出 chroot：

```bash
logout
```

然后使用以下命令进入：

```bash
chroot $LFS /tools/bin/env -i \
HOME=/root TERM=$TERM PS1=u:\w\$ \
PATH=/bin:/usr/bin:/sbin:/usr/sbin \
/tools/bin/bash --login
```

现在可以安全地剥离二进制文件和库了：

```bash
/tools/bin/find /usr/lib -type f -name *.a \
-exec /tools/bin/strip --strip-debug {} ';'
```



## 6.73. 清理

最后，清理运行测试留下的额外文件：

```bash
rm -rf /tmp/*
```

从现在起，退出后重新进入 chroot 环境时，使用以下修改后的 chroot 命令：

```bash
chroot "LFS" /usr/bin/env -i \
HOME=/root TERM='$TERM' PS1='u:w\$ ' \
PATH=/bin:/usr/bin:/bin:/sbin \
bin/bash --login
```

这是因为不再需要 `/tools` 中的程序。由于它们不再被需要，如果你需要，可以删除 `/tools` 目录。

> 注意
> `/tools` 还会移除用于运行工具链测试的 Tel、Expect 和 DejaGNU 的临时副本。如果你以后需要这些程序，则需要重新编译并安装。BLFS 书有相关说明（参见 http://www.linuxfromscratch.org/blfs/）。

如果虚拟内核文件系统已手动或通过重启卸载，则在重新进入 chroot 时会挂载虚拟内核文件系统。这一过程在第 6.2.2 节“挂载和填充 `/dev`”和第 6.2.3 节“挂载虚拟内核文件系统”中进行了解释。

最后，有几个静态库在之前的章节没有抑制，以满足多个包的回归测试。这些库来自 `binutils`、`bzip2`、`e2fsprogs`、`flex`、`libtool` 和 `zlib`。如果需要，现在可以删除它们：

```bash
rm -f /usr/lib/lib(bfd,opcodes)
rm -f /usr/lib/libbz2
rm -f /usr/lib/lib(ext2f,sprogs)
rm -f /usr/lib/libflex
rm -f /usr/lib/libtool
rm -f /usr/lib/libz
```

## 7. 系统配置

### 7.1. 介绍

启动 Linux 系统涉及几个步骤。System V 是许多发行版中使用的经典 init 系统。它支持运行级别（run levels），即系统可以处于的不同状态。

| 运行级别 | 描述 |
| :--- | :--- |
| 0 | 停止 |
| 1 | 单用户模式 |
| 2 | 维护模式 |
| 3 | 无图形多用户模式 |
| 4 | 未使用 |
| 5 | 带图形显示的多用户模式 |
| 6 | 重启 |

默认运行级别为 3。`/etc/init/runlevel` 文件决定系统启动到哪个运行级别。

#### 优点
- 易于理解。
- 易于自定义。

#### 缺点
- 启动较慢。
- 不支持 cgroups 等高级功能。
- 需要手动排序。

### 7.2. LFS-Bootstraps

`LFS-Bootstraps` 包包含一组用于启动/停止系统的脚本。

估计构建时间：少于 2 秒
所需磁盘空间：244 KB

#### 7.2.1. 安装 LFS-Bootstraps

安装包：

```bash
make install
```



# Linux From Scratch - 版本 8.0

## 7.2.2. LFS-Bootstraps 内容

已安装脚本：`checkfs`, `cleanfs`, `console`, `funcs`, `halt`, `ifdown`, `ifup`, `localnet`, `modules`, `mountfs`, `mountirts`, `network`, `reboot`, `sendsignal`, `setclock`, `syslog`, `template`, `update`

已安装目录：`/etc/rc.d` `/etc/init.d`（符号链接）`/etc/sysconfig` `/lib/services`

### 简要描述

- `checkfs` 在挂载前检查文件系统完整性（日志文件除外）
- `cleanfs` 移除重启后不应保留的文件，如 `/var/run/` 和 `/var/log/*`；重新创建 `/var/utmp` 并移除可能的 `/etc/noglogin`、`fastboot` 和 `forcefsck`
- `console` 加载所需的键盘布局映射；它设置屏幕字体
- `funcs` 包含多个引导使用的常用函数，例如错误和状态检查
- `halt` 停止系统
- `ifdown` 停止网络接口
- `ifup` 初始化网络接口
- `localnet` 设置系统主机名和本地回环设备
- `modules` 加载 `/etc/sysconfig/modules` 中的内核模块，使用那里给出的参数
- `mountfs` 挂载所有文件系统，除非是 `mouauto` 或基于网络的文件系统
- `mountirts` 挂载虚拟内核文件系统，如 `proc`
- `network` 设置网络接口（如网卡）并设置默认网关（如适用）
- `reboot` 重启系统
- `sendsignal` 确保在系统重启或停止之前每个进程都已终止
- `setclock` 在硬件钟未设置为 UTC 的情况下，将内核时重置为本地时间
- `syslog` 设置系统日志
- `template` 运行级别的模板
- `update` 更新系统

- `ipv4-static` 提供为网络接口分配静态网际协议 (IP) 地址所需的功能
- `swap` 启用和禁用交换文件和分区
- `sysctl` 如果 `/etc/sysctl.conf` 文件存在，则从该文件将系统配置值加载到运行的内核中
- `syslogd` 启动和停止系统及内核日志守护进程（system and kernel log daemons）
- `template` 用于为其他守护进程创建自定义启动脚本的模板
- `udev` 准备 `/dev` 目录并启动 Udev
- `udev_retry` 重试失败的 `udev` 事件（uevents），并在时将生成的规则文件从 `/run/udev` 复制到 `/etc/udev/rules.d`

## 7.3. 设备和模块处理概述

在第 6 章节中，我们安装了内置了 `eudev` 的 Udev 软件包。在深入细节介绍其工作原理之前，我们先简要回顾一下处理方法的历史。

Linux 系统传统上使用静态创建方法，即在 `/dev` 下创建大量的设备节点（device nodes），无论相应的硬件是否存在。这通常是通过一个 `MAKED` 脚本完成的，该脚本包含了对系统中每个可能的设备调用 `mknod` 程序以提供相应的设备号（major）和设备号（minor）。

使用 `udev` 方法，只有被内核检测到的设备节点会被创建。由于这些设备节点每次系统启动时都会创建，它们存储在 `devtmpfs` 文件系统中（一个虚拟文件系统）。设备节点不需要多少空间，因此使用的内存忽略不计。

### 7.3.1. 历史

2000年2月，一个名为 `devfs` 的新文件系统合并到了 2.3.4 内核，并在 2.4 系列内核中可用。尽管它存在于内核中，但这种创建设备的方法从未获得内核开发者的充分支持。

`devfs` 方法的主要问题在于它处理设备检测、创建和命名的方式。设备命名可能是最关键的问题。如果允许设备名称是可配置的，那么命名策略应该由系统管理员而非任何特定的开发者实施。`devfs` 文件系统还存在设计中固有的竞态条件，在不对内核进行重大修订的情况下无法修复。由于缺乏维护，它被废弃了，并最终于2006年6月从内核中移除。

随着不稳定的 2.5 内核树的发展，以及后来发布的 2.6 系列内核，一个名为 `sysfs` 的新文件系统诞生了。`sysfs` 的作用是将系统的硬件配置导出给用户进程。有了这种用户空间可见表示，开发 `devfs` 的替代方案变得可行。

### 7.3.2. Udev 实现

#### 7.3.2.1. Sysfs

上面简要提到了 `sysfs` 文件系统。人们可能会好奇 `sysfs` 如何知道系统中存在哪些设备以及应该为它们使用哪些设备节点。内核检测到驱动程序时，它们会向 `sysfs` 内部注册对象。对于编译进内核的驱动程序，这种注册会在模块加载时发生。当 `sysfs` 文件系统挂载在 `(/sys)` 时，驱动程序在 `sysfs` 中注册的数据对用户空间进程可用。

#### 7.3.2.2. 设备节点创建

设备文件由内核通过 `devtmpfs` 系统创建。任何想要注册设备节点的驱动程序都会通过 `devtmpfs`（通过设备核心）来实现。当 `devtmpfs` 实例挂载在 `(/dev)` 时，设备节点将以固定的名称、权限和所有者创建。

稍后，内核将发送一个 `udev`。根据 `/etc/udev/rules.d`、`/lib/udev/rules.d` 和 `/run/udev.rules` 目录下指定的规则，`udev` 将为设备节点创建所有符号链接，或更改其权限、所有者或组，或者修改对象的 `udev` 数据库。

这些目录中的规则是有编号的，大多数目录合并在一起。如果 `udev` 无法为正在创建的设备找到规则，它将保留 `devtmpfs` 最初使用的权限和所有权。

### 模块加载（Module Loading）

作为模块的设备驱动程序可能内置别名（aliases）。别名通常与 `modinfo` 程序的输出有关，是模块支持的特定设备。例如，`snd-f801` 驱动支持设备 ID 为 `0xc819` 和 `0xb801` 的 PCI 设备，并具有别名 `:pci:v00001319d0000b801s*s4c01*`。`udev` 创建通过 `sysfs` 处理该设备的驱动别名。例如，`/sys/bus/pci/devices/0000:00:0d.0/modfile` 可能包含字符串 `"pci:v00001319d0000b801sv00001319d00001319bc4c01"`。Udev 的默认规则将使用 `udev` 调用 `/sbin/modprobe`，并带有 `MODALIAS` 环境变量的内容（这应该与 `sysfs` 中 `modalias` 文件的内容相同），加载所有别名匹配此字符串通配符扩展的模块。

在这个示例中，除了 `snd-f801` 之外，如果可用，绝对的（且不需要的）`forte` 驱动程序将被加载。见下文防止卸载不需要的驱动的方法。

内核还能根据需要加载网络协议、文件系统和 NLS 支持。

### 7.3.4. 处理热插拔/动态设备

当你插入一个设备（如通用串行总线 USB MP3 播放器）时，内核识别到设备已连接并生成一个 `uevent`。随后由上述的 `udev` 处理。

### 7.3.3. 加载模块和创建设备的问题

在自动创建设备节点时存在一些可能的问题。

#### 7.3.3.1. 内核模块未自动加载

只有当模块具有特定总线的别名且总线驱动程序向 `sysfs` 导出必要的别名时，`udev` 才会加载该模块。在其他情况下，应该通过其他方式加载。在 4.9.9 内核中，`udev` 可以正常工作。

要确定模块是否支持，运行 `udev info`。

如果 `modalias` 文件存在，说明内核已添加。

在 4.9.9 内核中，`udev` 可以正常工作。

要确定模块是否支持，运行 `udev info`。

如果 `modalias` 文件存在，说明内核已添加。

这对于内核树之外的第三方驱动最为常见。在 `/lib/udev/devices` 创建静态设备节点（参见内核文档或第三方驱动供应商提供的文档）。该静态设备节点将被 `udev` 复制到 `/dev`。

#### 7.3.3.3. udev 加载了不需要的模块

要么不编译模块，要么在 `/etc/modprobe.d/blacklist.conf` 文件中将其黑名单化如下所示：

```
blacklist forte
```



黑色模块仍然可以使用 `modprobe` 命令手动加载。

### 7.3.3.4. udev 错误创建设备或创建错误的符号链接

这通常发生在规则意外匹配到设备时。借助 `udevadm` 命令找到规则并使其更具体。

### 7.3.3.5. udev 规则运行异常

这可能是上一个问题的另一种表现。如果不是，且你的规则使用了 `sysfs` 属性，可能是内核的时序问题，目前你可以通过创建一个等待 `sysfs` 属性的规则并将其添加到 `/etc/udev/rules.d/10-wait_for_sysfs.rules` 来绕过它（如果文件不存在则创建）。如果你这样做了，请通知 LFS 开发列表。

### 7.3.3.7. 重启后设备命名随机变化

这是由于 `udev` 设计上是并行处理 `uevents` 和模块，因此顺序是不可预测的。这永远不会被“修复”。你不应该依赖内核设备名。相反，你应该根据设备的某些属性（例如 `udev` 安装的序列号）创建规则建立稳定名称的符号链接。参见第 7.4 节“设备设备”和第 7.5 节“通用网络配置”的示例。

### 3.4. 扩展阅读

可以在以下网站获取额外的帮助文档：

- [devfs 的用户空间实现](http://www.chroah.com/linux/talks/ols_2003_udev_paper/Reprint-Koah-Hartman-OLS2003.pdf)
- [sysfs 文件系统](http://kernel.org/pub/linux/kernel/people/doc/papers/ols-2005-mochedev.pdf)

### 7.4. 管理设备

#### 7.4.1. 网络设备

`udev` 默认根据固件/BIOS 数据或物理特性（如总线或 MAC 地址）为设备命名。这种命名规范的目的是为了确保网络设备的命名是一致的，而不是基于网卡被发现的方式。例如，如果一台电脑有一块由 Intel 和 Realtek 制造的网卡，Intel 制造的网卡可能变为 `eth0`，而 Realtek 网卡可能变为 `eth1`。在某些情况下，重启后网卡的名称会反反过来。

在新的命名方案中，典型的网络设备名称将类似于 `enp5s0` 或 `wlp3s0`。如果不需要这种命名规范，可以实现传统的命名方案或自定义方案。

#### 7.4.1.1. 在内核命令行中禁用持久化

可以通过在内核命令行中添加 `net.ifnames=0` 来恢复使用 `eth0`、`eth1` 的传统命名方案。这对于那些只有一种类型设备的用户来说最为合适。笔记本电脑通常有多个命名为 `eth0` 和 `wlan0` 的以太网连接，也是这种方法的候选对象。命令行是在 GRUB 配置文件传递的。请参见第 8.4.4 节“创建 GRUB 配置”。

#### 7.4.1.2. 创建 Udev 规则

可以通过创建自定义 Udev 规则来定制命名方案。内核初始化中包含了一个脚本。运行以下命令生成这些规则：

```bash
bash /lib/udev/init-persistent-rules.sh
```

现在，检查 `/etc/udev/rules.d/70-persistent-net.rules` 文件，以找出哪个名称分配给了哪个网络设备：

```
cat /etc/udev/rules.d/70-persistent-net.rules
```

> 注意
> 在手动为网卡分配 MAC 地址，或者在 Qemu 或 Xen 等虚拟环境中的情况下，网络规则可能不会生成，因为地址分配不是一致的。在这种情况下，无法使用此方法。

该文件开头是一个注释块，随后是每个网卡控制器（NIC）的规则。第一行是注释描述，显示其硬件 ID（例如，如果是 PCI 卡，则显示其 PCI 供应商和设备 ID），以及括号中的驱动程序（如果驱动程序可以的话）。硬件 ID 或驱动程序都不用于确定给接口分配哪个名称；这些信息仅供参考。第二行是匹配此网卡并为其分配名称的 Udev 规则。

所有 Udev 规则由多个键组成，由逗号和可选的空白隔开。此规则的键及其对每个键的解释如下：

- `SUBSYSTEM="net"` - 这告诉 `udev` 忽略不是网卡的设备。
- `ACTION="add"` - 这告诉 `udev` 忽略非“添加”操作的 u 事件（“移除”和“更改”事件也是如此），但我们不需要重命名网络接口。
- `DRIVERS="*"` - 存在此项是为了 `udev` 忽略 VLAN 或网桥子接口（因为这些子接口没有驱动程序）。跳过这些子接口是因为分配的名称会与父设备发生冲突。
- `ATTR{address}` - 此键的值是网卡的 MAC 地址。
- `ATTR{type="*"}` - 这确保了在无线驱动程序（会创建多个接口）的情况下，规则只匹配主接口。跳过辅助接口的原因与跳过 VLAN 和网桥子接口的原因相同：否则会发生名称冲突。
- `NAME` - 此键的值是 `udev` 分配给此接口的名称。

`NAME` 的值是重要部分。在继续之前，请确保你已经知道每块网卡被分配了哪个名称，并在创建配置文件时务必使用 `NAME`。

### 7.4.2. CD-ROM 符号链接

你可能想要安装的一些软件（例如，各种媒体播放器）期望 `/dev/cdrom` 和 `/dev/dvd` 链接存在并指向 CD-ROM 或 DVD-ROM 设备。此外，根据每个设备的能力，在 `/etc/fstab` 中引用这些符号链接可能会很方便，你可以使用一个脚本来为这些符号链接生成规则，但你需要决定希望脚本使用哪种运行模式。

第一个脚本可以以“by-path”（通过路径）模式运行，这是 USB 和 FireWire 设备的默认模式，规则在 CD 或 DVD 设备的物理路径上创建。第二个脚本可以以“by-id”（通过 ID）模式运行（IDE 和 SCSI 设备的默认模式），规则创建取决于存储在 CD 或 DVD 设备路径中的标识字符串。路径由 `udev` 的 `path_id` 脚本确定，标识字符串通过其 `ata_id` 或 `scsi_id` 程序从硬件中读取，取决于你拥有的是哪种设备。

每种方法都有优点；使用哪种正确的方法取决于可能会发生什么种设备变化。如果你预计驱动器的物理路径（即它插入的端口和插槽）会发生变化，例如因为你计划将驱动器移动到 IDE 端口或不同的端口等——如果需要，请在启动后检查（并可能编辑）`/etc/udev/70-persistent-net.rules` 文件，确保符号链接符合你的需求。

> 重要
> 外部设备（例如，USB 连接的设备）不应使用默认命名方案，因为顺序可能会发生。对于这些设备，你应该使用“by-id” 或“by-path” 方案。

### 7.4.3. 处理重复设备

如第 7.3 节“设备和模块处理概述”所述，在 `/dev` 中出现具有相同功能的设备顺序本质上是随机的。例如，如果你有一个 USB 摄像头和一个电视调谐器，有时 `/dev/video0` 指向摄像头，而 `/dev/video1` 指向调谐器，重启后顺序会发生相反。对于声卡和网卡之外的所有硬件类，网络类的情况通过创建自定义 `udev` 规则来固定。网络类的情况在第 7.5 节“通用网络配置”中单独介绍，声卡配置可以在 BLFS 中找到。

对于你每个可能出现此问题的设备（即使该问题在你当前的 Linux 发行版中不存在），在 `/sys/class` 或 `/sys/block` 下找到相应的目录。对于视频设备，这可能是 `/sys/video4linux/videoX`。弄清楚识别设备的属性（通常是供应商产品 ID 和/或序列号）：

```
udevadm info -a -p /sys/video4linux/video0
```

然后通过以下命令创建符号链接：

```bash
cat > /etc/udev/rules.d/83-duplicate_dev.rules << "EOF"
KERNEL==="video*", ATTRS{idProduct}="1910", ATTRS{idVendor}="0d81", \
    SYMLINK+="webcam"
KERNEL==="video*", ATTRS{device}="0x036f", ATTRS{vendor}="0x109e", \
    SYMLINK+="vtuner"
EOF
```



结果是 `/dev/video0` 和 `/dev/video1` 仍然指向调谐器和摄像头（并且不应该直接使用），但有了 `/dev/vtuner` 和 `/dev/webcam` 始终指向正确的设备。

## 7.5. 通用网络配置

本节仅适用于需要配置网卡的情况。
如果不使用网卡，则可能不需要创建任何与网卡相关的配置文件。如果是如此，在第 7.2 节安装 "`LFS-Bootstraps-20150222`" 后，您需要从所有运行级别目录（`/etc/rc.d/rc*`）中删除网络符号链接。

### 7.5.1. 创建网络接口配置文件

网络脚本启动或关闭哪些接口通常取决于 `/etc/sysconfig/` 中的文件。该目录应该为每个要配置的接口包含一个文件，例如 `ifconfig.xyz`，其中 "xyz" 必须是网卡接口名称（例如 `eth0`）。该文件内部包含了接口的属性，如其 IP 地址（或）、子网掩码等。文件名必须以 `ifconfig.` 开头。

> 如果没有使用上一节中的程序，Udev 将根据系统物理特性（如 `en2s1`）分配网络接口名称。如果您不确定接口名称，只要已经启动了系统，就可以随时运行 `ip link`。再次，重要的是 `ifconfig` 必须以正确的网卡接口名称命名（例如 `ifconfig.en2s1` 或 `ifconfig.eth0`），否则您的网络接口在启动过程中不会被初始化。

以下命令为 `eth0` 设备创建一个带有静态 IP 地址的示例文件：

```
cd /etc/sysconfig/

cat << ifconfig.eth0 << "EOF"

ONBOOT=yes

IFACE=eth0

SERVICE=ipv4-static

IP=192.168.1.2

GATEWAY=192.168.1.1

PREFIX=24

BROADCAST=192.168.1.255

EOF
```

必须在每个文件中更改所使用的值以匹配适当的设置。

如果 `ONBOOT` 设置为 "yes"，则 System V 网络脚本将在系统启动期间启动网卡（NIC）。如果设置为 "no"，则网络脚本将忽略该网卡且不会将其自动启动。可以使用 `ifup` 和 `ifdown` 命令手动启动或停止接口。

`IFACE` 变量定义接口名称，例如 `eth0`。它是所有网络设备配置文件的项。

`SERVICE` 变量定义用于获取 IP 地址的方法。LFS-Bootstraps 包具有模块化的 IP 分配格式，在 `/lib/services/` 目录下创建额外的文件允许其他 IP 分配方法。这通常用于动态主机配置协议（DHCP），它将在 BLFS 文件中介绍。

`GATEWAY` 变量应该包含默认网关 IP 地址（如果存在）。如果没有，则完全注释掉该变量。

`PREFIX` 变量包含子网中使用的位数。IP 地址中的每个字节是 8 位。如果网络掩码是 `255.255.255.0`，则它使用前 24 个字节（位）来指定网络号。如果网络掩码是 `255.255.255.240`，则它使用前 28 位，这通常被 DSL 和电缆互联网服务提供商（ISP）使用。在示例中（`PREFIX=24`），网络掩码为 `255.255.255.0`。请根据您的特定子网调整 `PREFIX` 变量。如果省略，`PREFIX` 默认为 24。

更多信息请参见 `ifup` 手册页。

### 7.5.2. 创建 /etc/resolv.conf 文件

如果系统将连接到互联网，它需要一些域名解析服务（DNS）手段将互联网名称解析为 IP 地址，反之亦然。最佳方法是将来自 ISP 或网络管理员的 DNS 服务器 IP 地址放入 `/etc/resolv.conf`。运行以下命令创建文件：

```
cat /etc/resolv.conf << "EOF"

# Begin /etc/resolv.conf

domain <您的域名>

nameserver <主 DNS 服务器的 IP 地址>

nameserver <备用 DNS 服务器的 IP 地址>

# End /etc/resolv.conf

EOF
```

`domain` 语句可以省略，或者用 `search` 语句替换。详情请参见 `resolv.conf` 页面。

将 `<IP address of the DNS>` 替换为最适合设置的 DNS IP 地址。会有多个条目（需要备用服务器提供回退能力）。如果您只需要一个 DNS 服务器，请从文件中删除第二个 `nameserver` 行。该 IP 地址也可能是本地网络上的路由器。

> 注意：Google 公共 IPv4 DNS 地址为 8.8.8.8 和 8.8.4.4。

### 7.5.3. 配置系统主机名

在启动过程中，`/etc/hostname` 文件用于建立系统的主机名。运行以下命令创建 `/etc/hostname` 文件并输入主机名：

```
echo "<hostname> > /etc/hostname
```

`<hostname>` 需要替换为赋予计算机的名称。不要在此输入完全限定域名（FQDN）。信息存放在 `/etc/hosts` 文件中。

### 7.5.4. 自定义 /etc/hosts 文件

决定用于 `/etc/hosts` 文件的 IP 地址、完全限定域名（FQDN）以及可能的别名。语法如下：

```
IP_address myhost.example.org aliases
```

除非计算机要在互联网可见（即有注册的域名和分配的地址块），否则确保 IP 地址在私有网络范围内。有效范围如下：

| 私有网络地址范围 | 正常前缀 |
| :--- | :--- |
| 10.0.0.1 - 10.255.255.254 | 8 |
| 172.x.0.1 - 172.x.255.254 | 16 |
| 192.168.y.1 - 192.168.y.254 | 24 |

x 可以是 0-31 范围内的任何数字。y 可以 0-255 范围内的任何数字。一个有效的私有 IP 地址可以是 192.168.1.1。对于此 IP，有效的 FDN 可以是 `lfs.example`。即使不使用网卡，仍然需要有效的 FDN。这对于某些程序的正常运行是必要的。运行以下命令创建有效的 `/etc/hosts`：

```
cat /etc/hosts << "EOF"

# Begin /etc/hosts (network interface)

127.0.0.1 localhost

192.168.1.1 lfs.example

# End /etc/hosts

EOF
```

## 7.6. System V 脚本使用

### 7.6.1. 如何使用 System V 脚本？

Linux 使用一个名为 SysInit 的特殊设施，基于运行级别的概念。它有多个运行级别（实际上编号为 0 到 6），每个级别对应计算机启动时应该执行的操作。以下是这些运行级别的描述：

```
0: 停止

1: 单用户模式

2: 不带网络的多用户模式

3: 带网络的多用户模式

4: 预留

5: 同 3，通常用于 GUI 登录

6: 重启计算机
```

### 7.6.2. 配置 sysvinit

内核初始化期间，第一个运行的程序是在命令行指定的，或者默认是 `init`。该程序读取初始化文件 `/etc/inittab`。通过以下命令创建它：

```
cat /etc/inittab << "EOF"

# Begin /etc/inittab

id:initdefault

init::sysvinit:/etc/rc.d/init.d/rc

10:0:wait:/etc/rc.d/init.d/rc 0

11:1:wait:/etc/rc.d/init.d/rc 1

12:2:wait:/etc/rc.d/init.d/rc 2

13:3:wait:/etc/rc.d/init.d/rc 3

14:4:wait:/etc/rc.d/init.d/rc 4

15:5:wait:/etc/rc.d/init.d/rc 5

16:6:wait:/etc/rc.d/init.d/rc 6

root:12345:ctrlaltdel:/bin/shutdown -tl -a -r now

su:016:once:/sbin/sulogin

1:2345:respawn:/sbin/agetty --local tty1 9600

2:2345:respawn:/sbin/agetty tty2 9600

3:2345:respawn:/sbin/agetty tty3 9600

4:2345:respawn:/sbin/agetty tty4 9600

5:2345:respawn:/sbin/agetty tty5 9600

6:2345:respawn:/sbin/agetty tty6 9600

# End /etc/inittab

EOF
```



# 从零开始构建 Linux - 版本 8.0

关于此初始化文件的解释，请参见 `inittab` 的主页。对于 LFS，运行的关键命令是 `rc`。上面的初始化文件将指示 `rc` 运行 `/etc/rc.d/` 中所有以 S 开头的脚本，随后运行 `/etc/rc.d?` 中所有以 S 开头的脚本，问号由默认值指定。

为了方便起见，`rc` 脚本读取 `/lib/lsb/init-functions` 中的函数库。该库还会读取一个可选的配置文件 `/etc/sysconfig/rc.site`。后续章节中描述的任何系统配置参数都可以替代放置于此文件中——将所有系统参数在此处汇总。

为了调试方便，该函数脚本会将所有日志记录到 `/run/var/bootlog`。`/run` 目录是一个 `tmpfs`，它在启动之间不是持久的，但在启动过程结束时，它会被追加到更持久的文件 `/var/log/boot.log` 中。

## 7.6.2.1 更改运行级别

更改运行级别通过 `init <runlevel>` 完成，其中 `<runlevel>` 是目标运行级别。例如，为了重启电脑，用户可以使用 `init 6` 命令，它是 `reboot` 命令的别名。同样，`init 0` 是 `halt` 命令的别名。

在 `/etc/rc.d` 下有许多类似于 `rc?.d`（其中 `?` 是运行级别的数字）和 `rcinit.d` 的目录，它们都包含许多符号链接。某些链接以 K 开头，另一些以 S 开头并启动服务。它们在初始字母后面都跟有两个数字。`K` 表示停止（杀死）服务，`S` 表示启动服务。这些数字决定了脚本运行的顺序，从 00 到 99——数字越小，执行得越早。当 `init` 切换到另一个运行级别时，根据运行级别，相应的服务将被启动或停止。

真正的脚本位于 `/etc/rc.d/init.d`。它们执行实际工作，所有的符号链接都指向它们。K 链接和 S 链接指向 `/etc/rc.d/init.d` 中的同同一个脚本。这是因为脚本可以使用不同的参数调用，如 `start`、`stop`、`restart`、`reload` 和 `status`。当遇到 K 时，将带 `stop` 参数运行相应的脚本。当遇到 S 链接时，将带 `start` 参数运行相应的脚本。

此说明有一个例外。在 `rc0.d` 和 `rc6.d` 目录中以 S 开头的链接不会启动任何内容。它们将被带 `stop` 参数调用。这背后的逻辑是，当用户准备重启或停止系统时，系统只需要停止即可。

以下是脚本参数作用的描述：

- `start`: 启动服务。
- `stop`: 停止服务。
- `restart`: 停止服务然后重新启动。
- `reload`: 更新服务的配置。这在服务的配置文件被修改后使用，此时服务不需要重启。
- `status`: 告知服务是否正在运行以及对应的 PID 是。

你可以随意修改启动过程的工作方式（毕竟，这是你自己的 LFS）。这里提供的文件是此类操作的示例。

## 7.6.3. Udev 启动脚本

`/etc/rc.d/init.d/udev` 初始化脚本启动 `udev`，触发内核已创建的任何“冷热插”设备，并等待规则编译。该脚本还会取消 `udev` 处理程序从默认 `/sbin/hotplug` 的设置。这样做后内核不再需要调用实例。Udev 将在网络套接字上监听内核信号。

`/etc/init.d/udev_retry` 初始化脚本会对那些依赖文件系统的子系统调用重新触发，因为这些系统的规则在挂载脚本运行之前尚未挂载（特别是 `/usr` 和 `var` 可能会导致这种情况）。该脚本在挂载脚本之后运行，因此规则（如果重新触发）在第二次运行时应该会成功。它通过 `/etc/sysconfig/udev_retry` 配置；该文件中注释之外的任何单词都被视为触发重试的系统名称。要查找设备的子系统，请使用 `udevadm --attribute-<device>`，其中 `<device>` 是 `/dev` 或 `/sys` 中的绝对路径，例如 `/dev/s0` 或 `/sys/class`。

### 7.6.3.1. 模块加载

编译为模块的设备驱动程序可能内置别名。别名会在支持设备的 `modinfo bus-identifiers` 输出中显示。例如，`snd-fm801` 驱动程序支持供应商 ID `0x1319` 和设备 ID `0x0801`，并有一个别名 `"pci:v0000131900000801sv*dbc4c01*"`。对于大多数设备，驱动程序通过 sysfs 导出处理该设备的驱动别名，例如 `/sys/pci/devices/0000:00:0.d/alias` 可能包含字符串 `"pci:v0000131900000801u0000131900000801e000"`。Udev 提供的默认规则将根据 `MODALIAS` 环境变量的内容调用 `/sbin/modprobe`（内容应与 sysfs 中的 `modalias` 文件相同）。

*注：此处原文中存在大量重复段落，已根据“不要重复输出原文”的原则在译文中保留一份有效信息*

使用。请注意，某些关键键map具有同名的多个版本（`kterty/` 和 `query/ qwertz/` 中的 `cz` 及其变体，例如 `olpc/` 和 `query/`，以及 `ggGlod 和 query` 中的 `trf`）。在这些情况下，应该指定目录（例如 `query/`）以确保加载正确的键map。

### KEYMAP_CORRECTIONS

此变量指定了 `loadkeys` 程序第二次调用的参数。如果默认键map不完全令人满意且需要进行微调，则此变量非常有用。例如，为了在一个通常不包含欧元符号的键map中包含欧元符号，可以将此变量设置为 `"euro2"`。

### FONT

此变量指定了 `setfont` 程序的参数。通常，这包括名称、"m" 以及要加载的应用程序字符表名称。例如，为了加载 `"lat1-16"` 字体并配合 `"8859-1"` 应用程序字符表（这在美国下是合适的），请将此变量设置为 `"lat1-m 8859-1"`。在 UTF-8 中，内核使用应用程序字符表将键map 中的 8 位键码转换为 UTF-8，因此 `"-m"` 参数的参数值应设置为键map 中组合键码的编码。

### UNICODE

将变量设置为 `"1"`、`"yes"` 或 `"true"` 以控制台进入 UTF-8 模式。这在基于 UTF-8 的本地环境中非常有用，否则则会有害。

### LEGACY_CHARSET

对于许多键盘布局，Kbd 软件包中没有默认的 Unicode 键map。如果将此变量设置为可用非 UTF-8 键map 的编码，控制台启动脚本将动态将可用的键map 转换为 UTF-8。

一些示例：

- 对于非 unicode 的设置，通常只需要 `KEYMAP` 和 `FONT` 变量。例如，对于波兰设置，用户会使用：

```
cat > /etc/sysconfig/console << "EOF"

# Begin /etc/sysconfig/console

KEYMAP="pl12"

FONT="lat2a-16 -m 8859-2"

# End /etc/sysconfig/console

EOF
```

- 如上所述，有时需要对默认键map 进行微调。以下示例为德语键map 添加了欧元符号：

```
cat > /etc/sysconfig/console << "EOF"

# Begin /etc/sysconfig/console

KEYMAP="de-latin1"

KEYMAP_CORRECTIONS="euro2"

FONT="lat0-16 -m 8859-15"

# End /etc/sysconfig/console

EOF
```

以下是一个用于保加利亚语的 Unicode 示例，该语言存在默认 UTF-8 键map：

```
cat > /etc/sysconfig/console << "EOF"

# Begin /etc/sysconfig/console

UNICODE="1"

KEYMAP="bg_bds-utf8"

FONT="LatArCyrHeb-16"

# End /etc/sysconfig/console

EOF
```

由于上一个示例使用了 512 个字形的 LatArCyrHeb-16 字体，除非使用 framebuffer，否则 Linux 控制台将不再提供亮色。如果人们希望不使用不属于其语言的亮色字符，仍然可以使用特定语言的 256 字形字体，如下所示：

```
cat > /etc/sysconfig/console << "EOF"

# Begin /etc/sysconfig/console

UNICODE="1"

KEYMAP="bg_bds-sun16"

FONT="cyr-sun16"

# End /etc/sysconfig/console

EOF
```

以下示例说明了键map 从 ISO-8859-15 到 UTF-8 的自动转换，以及在 Unicode 模式下启用德语键：



```bash
cat > /etc/sysconfig/console << "EOF"

# Begin /etc/sysconfig/console

UNICODE="1"

KEYMAP="de-latin1"

KEYMAP_CORRECTIONS="euro2"

LEGACY_CHARSET="iso-8859-15"

FONT="LatArCyrHeb-16 -m 8859-15"

# End /etc/sysconfig/console

EOF
```

某些键 `map` 具有死键（即本身不产生字符的键，但会在下一个键产生的字符上加上重音符号）或定义了组合规则（例如：默认键 `map` 中的“按下 Ctrl+. A 以获得 Æ”）。`Linux-4.9.9` 仅当组合的源字符不是多字节时才在内核中正确解释死键和组合规则。这种缺陷影响了欧洲语言的键 `map`，因为重音被添加到无重音的 ASCII 字符上，或者 ASCII 字符组合在一起。然而在 UTF-8 中这是一个问题，例如对于希腊语，需要在字母“alpha”上加上重音。解决方案是避免使用 UTF-8，或者安装在输入处理上没有此限制的 X 窗口系统。

- 对于中文、日语、韩语和其他语言，Linux 控制台无法配置为显示所需的字符。需要此类语言的用户应该安装 X Window 系统、涵盖必要字符范围的字体以及正确的输入法（例如 `SCIM`），它支持多种语言。

> 注意
> `/etc/sysconfig/console` 文件仅控制 Linux 控制台的本地化。通过设置正确的键盘布局来控制。

## 7.6.6 创建文件

`/etc/sysconfig/console` 文件仅控制 Linux 控制台的本地化。通过设置正确的键盘布局来控制。在启动时创建文件，这可以通过 `/sysconfig/console` 默认文件实现。

## 7.6.7 配置 syslogd 脚本

`syslogd` 脚本调用 System V 初始化。默认情况下，每隔 20 分钟写入时间戳。要关闭此时间戳，将 `SYSLOGD_PARMS` 设置为空值：

```bash
SYSLOGD_PARMS=
```

## 7.6.8 rc.site 文件

`/etc/sysconfig/console` 文件包含了在启动时自动设置的设置。它可以交替设置主机名、控制台文件。如果在独立文件中存在相关变量，`rc.site` 具有优先级。

```bash
# rc.site

#发行版信息

# 这些值在此指定将覆盖默认值

DISTRO="Linux From Scratch" # 发行版名称

DISTRO_CONTACT="lfs-dev@linux.org" # 报告地址

DISTRO_MINI="IFS" # 用于文件名的短名称
```

```bash
# 在不等待 udev 等 settle 的情况下加速启动
#OMIT_UDEV_SETTLE=y

# 在不等待 udev_retry 等待 settle 的情况下加速启动
#OMIT_UDEV_RETRY_SETTLE=yes

# 如果为 yes 则跳过清理 /tmp
#SKIPTMPCLEAN=no

# 用于 setclock
#UTC=1
#CLOCKPARAMS=

# 用于 consolelog（注意：默认值 7=debug，会有大量输出）
#LOGLEVEL=7

# 用于网络
#HOSTNAME=mylfs

# 关机时 TERM 和 KILL 信号之间的延迟
#KILLDEAY=3

# 可选的 syslogd 参数
#SYSLOGD_PARMS="-m 0"

# 控制台参数
#UNICODE=1
#KEYMAP="de-latin1"
#KEYMAP_CORRECTIONS="euro2"
#FONT=1at0-16 8859-15
#LEGACY_CHARSET=
```

## 7.6.8.1. 自定义启动和关机 Shell

LFS 的启动脚本和关机系统以相当高效的方式运行，但你可以在 `rc.site` 文件中进行两项调整，以进一步提高速度并根据你的喜好调整消息。要实现这一点，请调整 `/etc/sysconfig/rc.site` 文件中的设置。

- 在启动脚本 `udev` 期间，会调用 `udev` `settle`，这需要一些时间来完成。这个时间取决于或可能取决于系统中的设备。如果你只有分区和一个以太网卡，该过程可能不会进行等待。要跳过此过程，请设置变量 `OMIT_UDEV_SETTLE=y`。
- 启动脚本 `udev_retry` 默认也会运行 `udev` `settle`。只有当 `/var` 目录单独挂载时，才需要此命令。如果时钟是 `/var/lib/hwclock/adjtime` 文件。其他自定义可能也需要等待 `udev` 完成，但在许多安装中这是并不需要的。通过设置变量 `OMIT_UDEV_RETRY_SETTLE=y` 可以跳过该命令。
- 默认情况下，文件系统检查是静默的。这在启动过程中可能表现为延迟。要开启 `fsck` 输出，请设置变量 `VERBOSE_FSCK=y`。
- 重启时，你可能想完全跳过文件系统检查 `fsck`。要这样做，要么创建 `/fastboot` 文件，要么现在使用命令 `/sbin/shutdown -f` 重启系统。相反，你可以通过 `/forcefsck` 或运行 `shutdown` 时使用 `-F` 代替 `-f` 来强制所有文件系统进行检查。

设置 `FASTBOOT=y` 将在启动过程中禁用 `fsck`，直到其移除。不建议长期这样做。

- 通常，`/tmp` 目录下的所有文件在启动时会被删除。取决于文件或目录的数量，这可能会导致启动过程出现明显的延迟。要移除这些文件，设置变量 `SKIPTMPCLEAN=y`。
- 在启动期间，`init` 程序会向它启动的每个进程（例如 `agetty`）发送 `TERM` 信号，等待设定的时间（3 秒），然后向每个进程发送 `KILL` 信号并再次等待。此过程对于所有未由其自己的脚本关闭的进程都会重复执行。`init` 中的延迟可以通过传递参数来设置。例如，在关机或重启时设置 `-0` 参数以移除 `init` 中的延迟（例如 `/sbin/shutdown -o -r now`）。通过设置参数 `KLLDELAY=0` 可以缩短 `sendsignal` 脚本的延迟。

## 7.7 Bash 启动文件

程序 `/bin/bash`（以下称为“shell”）使用一组文件来帮助创建运行所需的环境。每个文件都有特定的用途，并可能以不同的方式影响登录和交互式环境。`/etc` 目录下的文件提供全局设置。如果你的家目录中存在等效文件，它可能会覆盖全局设置。

交互式登录 `shell` 在成功登录后，使用 `/bin/login` 通过读取 `/etc/passwd` 文件启动。交互式非登录 `shell` 在命令行处启动（例如 `[prompt]$bin/bash`）。当 `shell` 运行时，通常会存在一个非交互式 `shell`。它是非交互的，因为它正在处理脚本，而不是在等待用户输入命令。

欲需更多信息，请参阅“Bash Startup Files and Interactive Shells”章节中的 `info bash`。

当 `shell` 被作为交互式登录 `shell` 调用时，会读取 `/etc/profile` 和 `~/.bash_profile`。设置这些文件并正确设置某些环境变量会导致：

- 程序的输出翻译为本地语言
- 字符正确分类为字母、数字和其他类别。这对于 `bash` 在非英语区域设置的命令行中正确接受非 ASCII 字符是必要的
- 该国家正确的字母排序顺序
- 适当的默认纸张大小
- 金钱、时间和日期值的正确格式

将 `<ll>` 替换为所需语言的两个字母代码（例如 "en"），将 `<CC>` 替换为相应国家的两个字母代码（例如 "GB"）。`<charmap>` 应被替换为所选区域的标准字符集。可能还存在可选的修符（如 "@euro"）。

通过运行 `locale -a` 可以获取 Glibc 支持的所有区域列表。（此处省略了原文中大量重复的 OCR 识别错误文本）。

以下是一个通用的 `inputrc` 文件，并附有解释各种选项作用的注释。注意，注释不能与命令在同一行。使用以下命令创建该文件：

```bash
cat > /etc/inputrc << "EOF"

# Begin /etc/inputrc

# Modified by Chris Lynn <rory@rory.dynup.net>
```

```bash
# 允许命令提示符换行到下一
set horizontal-scroll-mode Off
```

```bash
# 启用 8 位输入
set meta-flag On
set input-meta On
```

```bash
# 关闭第 8 位剥离
set convert-meta Off
```

```bash
# 保留第 8 位用于显示
set output-meta On
```

```bash
# 无、可见或听觉提示
set bell-style none
```

```bash
# 以下所有内容都将 lst 参数中值的转义序列
# 映射到 readline 特定函数
```



"\eOd": backward-word

"\eOc": forward-word

```bash
# 用于 linux 控制台

"\e[1-": beginning-of-line

"\e[4-": end-of-line

"\e[5-": beginning-of-history

"\e[6-": end-of-history

"\e[3-": delete-char

"\e[2-": quoted-term
```

```bash
# 用于 xterm

"\e0H": beginning-of-line

"\e0F": end-of-line
```

```bash
# 用于 Konsole

"\e[H-": beginning-of-line

"\e[F-": end-of-line
```

```bash
# End /etc/inputrc
EOF
```

## 7.9. 创建 `/etc/shells` 文件

`shells` 文件包含系统上登录 shell 的列表。应用程序使用此文件来确定 shell 是否有效。每行都应该单行存在，由 shell 的路径组成，该路径是相对于目录结构根目录（`/`）的相对路径。

例如，`chsh` 会查询此文件以确定非权限用户是否可以更改其账户的登录 shell。如果命令名称未在列表中，用户将被拒绝更改。

对于像 `GDM` 这样的应用程序这是一个要求，如果它找不到 `/etc/shells`，它将不会填充浏览器；或者对于 FTP 守护进程，传统上拒绝访问未包含在此文件中的 shell 的用户。

```bash
cat > /etc/shells << "EOF"

# Begin /etc/shells

/bin/sh

/bin/bash

# End /etc/shells

EOF
```

## 第 8 章. 使 LFS 系统可启动

### 8.1. 引言

是时候让 LFS 系统变得可启动了。本章讨论了创建 `fstab` 文件、为新的 LFS 系统构建内核，以及安装 `GRUB` 引导加载程序，以便在启动时可以选择启动 LFS 系统。

### 8.2. 创建 `/etc/fstab` 文件

`/etc/fstab` 文件被某些程序用于确定文件系统默认挂载到何处，以及哪些系统在挂载之前必须检查（完整性错误）。创建一个新的系统表如下所示：

```
cat > /etc/fstab << "EOF"

# Begin /etc/fstab

# file system mount-point type    options             dump fsck order
/dev/<xxx>  <fff> defaults       1 0
/dev/<yyy> swap    swap       pri=1                0
proc         /proc  proc       nosuid,noexec, nodev 0
sysfs        /sys    sysfs     nosuid,noexec, nodev 0
devpts       /dev/pts devpts      gid=5,mode=620      0
tmpfs        /run    tmpfs     defaults             0 0
devtmpfs     /dev    devtmpfs  mode=0755,nosuid 0

# End /etc/fstab

EOF
```

将 `<xxx>`, `<yyy>` 和 `<fff>` 替换为适用于系统、sda2、sda5 和 ext 4 的值。
关于此文件中六个字段的详细信息，请参 `man fstab`。

源自 MS-DOS 或 Windows 文件系统（例如：`vfat`, `ntfs`, `smbfs`, `cifs`, `iso9660`, `udf`）需要 `"iocharset"` 选项，以便文件名中的非 ASCII 字符能够被解释。该选项的值应与您的区域设置字符集相同，并进行调整以使内核能够理解。如果字符集定义（在“文件 -> 原生语言支持”下找到）已编译进内核或构建为模块，则此方法有效。`vfat` 和 `smbfs` 文件系统还需要 `"codepage"` 选项。它应该设置为您所在国家 MS-DOS 使用的代码页。例如，为了挂载 USB 闪存器，`ru_KOI8-R` 用户需要在 `/etc/fstab` 的挂载行选项部分包含以下内容：

```bash
noauto,user,quiet, showexec, iocharset=koi8, codepage=866
```

对应于 `ru_RU_UTF-8` 的选项片段为：

```bash
noauto,user,quiet, showexec, iocharset=utf8, codepage=866
```

### 注意

在后一种情况下，内核会发出以下消息：

> FAT: utf8 is not a recommended IO charset for FAT filesystems, filesystem will be case sensitive!

此负面建议应该被忽略，因为 `"iocharset"` 选项的所有其他值会导致 UTF-8 区域设置下的文件名显示错误。

可以在内核配置期间为某些文件系统指定默认的代码页和字符。相关参数命名为默认 NLS 选项（`CONFIG_NLS_DEFAULT`）、默认远程 NLS 选项（`CONFIG_SMB_NLS_DEFAULT`）、FAT 默认代码页（`CONFIG_FAT_DEFAULT_CODEPAGE`）以及 FAT 默认字符（`CONFIG_FAT_DEFAULT_IOCHARSET`）。在内核编译时无法为 nfs 文件系统指定这些设置。

```bash
hdparm -I /dev/sda | grep NCQ
```

返回非空输出则支持该选项。

注意：基于逻辑卷管理（LVM）的分区无法使用 barrier 。

### 8.3. Linux-4.9.9

Linux 包包含 Linux 内核。

估计构建时间：4.4 - 66.0 SBU（通常约为 6 SBU）
所需磁盘空间：960 - 1100 MB

#### 8.3.1. 安装

构建内核涉及几个步骤：配置、编译和安装。

运行以下命令准备内核源码：

```bash
make mrproper
```

编译内核和模块：

```bash
make
```

安装模块，如果内核配置使用了它们：

```bash
make modules_install
```

内核完成后，还需要额外的步骤来完成安装。某些文件需要复制到 `/boot` 目录。

# 注意

如果主机系统具有独立的 `/boot` 分区，则下方复制的文件应该存放在那里。最简单的方法是在继续之前，将主机上的 `/boot` 绑定到 `/mnt/lfs/boot`。在主机系统中的以 `root` 用户身份执行：

```
mount --bind /boot /mnt/lfs/boot
```

内核镜像的路径可能取决于所使用的平台。下面的文件名可以根据你的情况进行更改，但文件名的主干应为 `vmlinux`，以兼容下一节描述的启动过程自动设置。以下命令启用了 x86 架构：

```
cp -v arch/x86/boot/bzvmlinux-4.9.9-lfs-8.0
```

`System.map` 是内核的符号文件。它映射了内核 API 中每个条目的函数入口，以及运行内核的内核数据结构的地址。在调查内核问题时，它被用作资源。执行以下命令安装映射文件：

```
cp -v System.map /boot/System.map-4.9.9
```

由 `make menuconfig` 步骤生成的配置文件 `.config` 包含了刚刚编译的内核的所有配置选择。保留此文件以备后用是一个好主意：

```
cp -v .config /boot/config-4.9.9
```

安装 Linux 内核文档：

```
install -d /usr/share/doc/linux-4.9.9
cp -r Documentation/* /usr/share/doc/linux-4.9.9
```



注意的是，内核源码目录中的文件并不属于 `root`。每当以 `root` 用户身份解包软件包时（我们在 `root` 内部执行了此操作），文件将具有其在打包计算机上的用户 ID 和组 ID。对于安装任何其他软件包来说，这不是问题，因为源码树在安装后会被删除。然而，Linux 源码树通常会保留很长时间。正因如此，软件包使用的任何用户 ID 可能会分配给机器上的某人。那个人将对内核源码具有写权限。

# 注意

在许多情况下，对于以后在 BLFS 中安装的软件包，需要更新内核配置。与其他软件包不同，在安装新构建的内核后，没有移除源码树。

如果需要保留源码树，请对 `linux-4.9.9` 目录运行 `chown -R 0:0` 以确保所有文件都属于用户 `root`。

# 警告

某些内核文档建议从 `/usr/src/linux` 创建指向内核源码目录的符号链接。这专门针对 2.6 系列之前的内核，并且在 LFS 系统上不能创建它，因为可能会导致在你基础 LFS 系统完成后你可能想要构建的软件包出现问题。

# 警告

系统 `include` 目录（`/usr/include`）中的头文件**始终**应该是针对编译的 Glibc 编译的那些，即第 6.7 节“Linux-4.9.9 API Headers”中的清理头文件。因此，它们**绝不能**被内核头文件或其他内核清理头文件替换。

# 8.3.2. 配置 Linux 模块加载顺序

大多数情况下 Linux 模块会自动加载，但有时它们需要特定的指导。加载模块的程序 `modprobe` 或 `insmod` 使用 `/etc/modprobe.d/usb.conf` 实现此目的。如果 USB 驱动程序（`ehci_hccd`、`ohci_hccd` 和 `uhci_hccd`）已编译为模块，则需要创建此文件，以便它们按正确的顺序加载；`ehci_hccd` 必须在 `ohci_hccd` 和 `uhci_hccd` 之前加载，以避免启动时出现警告。

运行以下命令创建一个新文件 `/etc/modprobe.d/usb.conf`：

```
install -v -m755 -d /etc/modprobe.d

cat /etc/modprobe.d/usb.conf << "EOF"

# Begin /etc/modprobe.d/usb.conf

install ohci_hccd /sbin/modprobe ehci_hccd; /sbin/modprobe ohci_hccd; true

install uhci_hccd /sbin/modprobe ehci_hccd; /sbin/modprobe -i uhci_hccd; true

# End /etc/modprobe.d/usb.conf

EOF
```

# 8.3.3. Linux 的内容

- 安装的文件：`config-4.9.9`、`vmlinux-4.9.9-lfs-8.0` 和 `System.map-uhci-4.9.9`
- 安装的目录：`/lib/modules` `/usr/share/doc/linux-4.9.9`

# 简述

- `config-4.9.9`
包含了内核的所有配置选择

- `vmlinux-4.9.9-lfs-8.0`
Linux 系统的引擎。当启动计算机时，内核是操作系统加载的第一部分。它检测并初始化计算机硬件的所有组件，然后将这些组件作为文件树的形式提供给软件，并将单个 CPU 转换为一台能够同时运行数十个程序的多任务机器。

- `System.map-4.9.9`
地址和符号的列表；它映射了内核中所有函数和数据结构的入口点和地址。

## 8.4. 使用 GRUB-v 设置启动过程

### 8.4.1. 简介

> **警告** 错误配置 GRUB 可能会导致系统在没有备用启动设备（如 CD-ROM）的情况下无法运行。本节对于启动你的 LFS 系统不是必需的。你可能只是想修改当前的引导程序，例如 Grub-Legacy、GRUB2 或 LILO。

确保准备好一个紧急启动盘，以便在计算机无法使用（无法启动）时“救援”计算机。如果你没有启动设备，可以创建一个。为了让下面的步骤生效，你需要跳转到 BLFS 并从 `libisoburn` 软件包安装 `xorriso`。

```
/tmp

grub-mkrescue --output=grub-img.iso

xorriso -as cdrecord -v dev=/dev/cdrom rw blank=as_needed grub-img.iso
```



> 在启用了 UEFI 的系统上安装 LFS，内核需要按照下一节描述的带有 `CONFIG_EFI_STUB` 能力进行构建。

### 8.4.2. GRUB 命名规范

GRUB 使用它自己的格式来命名设备和分区，为 `(hdn,m)`，其中 `n` 是驱动器号，`m` 是分区。

### 8.4.3. 设置配置

GRUB 通过写入第一个轨道工作。位置是 `/boot/grub`。分区的位置是 2。

将 GRUB 文件安装到 `/boot/grub` 并设置启动：

``` 
**警告警告

以下命令将覆盖当前的.....

的 GRUB GRUB 文件安装到theboot/gr 位置到 /boot/gr. 并设置启动：
```

```
grub-install /dev/sda
```

### 8.4.4. 创建 GRUB 配置文件

生成 `/boot/grub/grub.cfg`：

```
cat > /boot/grub/grub.cfg << "EOF"
# Begin /boot/grub/grub.cfg
set default=0
set timeout=5

insmod ext2
set root=(hd0,2)

menuentry "GNU/Linux, Linux 4.9.9-lfs-8.0" {
    linux /boot/vmlinuz-4.9.9-lfs-8.0 root=/dev/sda2 ro
}
EOF
```

> 注意从 GRUB 的角度来看，内核文件相对于分区。如果你使用独立的 `/boot` 分区，从上面的 linux 行中删除 `/boot`。你还需要更改 `set root` 行指向分区。

GRUB 是一个非常强大的程序，它为从各种设备、操作系统和分区类型启动提供了大量的选项。还有自定义选项，例如图形启动屏幕、播放声音、鼠标输入等。这些选项的细节超出了本介绍的范围。

> ### 注意

有一个命令 `grub-mkconfig` 可以自动写入配置文件。它使用 `/etc/grub.d/` 中的一组脚本并破坏你做的任何自定义。这些脚本主要为非源码发行版设计，不建议用于 LFS。如果你安装了商业 Linux 发行版，该程序可能会被运行。请确保备份你的 `grub.cfg` 文件。

## 第 9 章. 结束

## 9.1. 结束

做得好！新的 LFS 系统已经安装完成！祝愿你那全新的、自定义构建的 Linux 系统取得巨大成功。

创建一个 `/etc/lfs-release` 文件可能是一个好主意。通过这个文件，你（以及在我们某次需要寻求帮助时）可以很容易地找到系统上安装的是哪个版本的 LFS。运行以下命令创建此文件：

```bash
echo 8.0 > /etc/lfs-release
```

创建一个用于显示你的新系统相对于 Linux 标准基础（LSB）状态的文件也是一个好主意。运行以下命令创建此文件：

```bash
cat > /etc/lsb-release << "EOF"
DISTRIB_ID="Linux From Scratch"
DISTRIB_RELEASE="8.0"
DISTRIB_CODENAME="<name here>"
DISTRIB_DESCRIPTION="Linux From Scratch"
EOF
```

务必对 'DISTRIB_CODENAME' 字段进行某种自定义，使你的系统独一无二。

## 9.2. 登记计数

现在你已经读完了这本书，想被记录为一名 LFS 用户吗？前往 http://www.linuxfromscratch.org/cgi-bin/lfscounter.php，通过输入你的名字和第一次使用的 LFS 版本来注册成为 LFS 用户。

让我们重启进入 LFS 吧。

## 9.3. 重启系统

现在所有软件都安装完毕，是时候重启你的电脑了。然而，你应该注意以下几点。你在书中创建的系统是非常精简的，很可能缺少你继续操作所需的功能。在当前当前环境中，通过从 BLFS 书籍中安装几个额外的软件包，可以让你在重启进入新的 LFS 系统后处于一个更好的境地以继续工作。以下是一些建议：

- 一个使用 `Lynx` 的文本浏览器将允许你能够在一个虚拟终端中方便地查看 BLFS 书籍，同时在另一个终端中构建软件包。
- `GPM` 软件包将允许你在虚拟终端中执行复制/粘贴操作。
- 如果你处于静态 IP 配置无法满足你的网络需求的情况下，安装如 `dhcped` 或 `dhcp` 客户端部分可能会有所帮助。
- 安装 `sudo` 可能对于以非 root 用户身份构建软件包以及在你的系统中轻松安装生成的软件包很有用。

Linux From Scratch - Version 8.0

- 如果你想在舒适的 GUI 环境下从远程系统访问你的新系统，请安装 `openssh` 及其先决依赖 `wget`。
- 为了能从互联网获取文件，请安装 `wget`。



- 如果你的一个或多个磁盘驱动具有 GUID 分区表 (`GPT`)，那么 `gptfdisk` 或 `parted` 将非常有用。

- 最后，此时对以下配置文件进行审查也是合适的。

- `/etc/bashrc`

- `/etc/colors`

- `/etc/fstab`

- `/etc/hosts`

- `/etc/inputrc`

- `/etc/profile`

- `/etc/resolv.conf`

- `/etc/vimrc`

- `/root/.bash_profile`

- `/root/.bashrc`

- `/etc/sysconfig/network`

- `/etc/sysconfig/ifconfig.eth0`

既然我们已经说了这么多，让我们第一次启动我们那闪闪新的 LFS 安装吧！首先退出 `chroot` 环境：

```bash
logout
```

然后卸载虚拟文件系统：

```bash
mount -v $LFS/dev/pts
mount -v $LFS/dev
mount -v $LFS/run
mount -v $LFS/proc
mount -v $LFS/sys
```

卸载 LFS 文件系统本身：

```bash
mount -v $LFS
```

如果创建了多个分区，请在卸载主分区之前卸载其他分区，如下：

```bash
mount -v $LFS/usr
mount -v $LFS/home
mount -v $LFS
```

现在，使用以下命令重启系统：

```bash
shutdown -r now
```

假设已经按照前面的说明方法设置了 `GRUB` 引导加载程序，菜单已设置为自动启动 LFS 8.0。

Linux From Scratch - Version 8.0

## 9.4. 现在该怎么办？

感谢阅读本 LFS 书。我们希望你发现这本书对你有帮助，并学习了更多关于系统创建的知识。

现在 LFS 系统已经安装，你可能在想“接下来？”为了回答这个问题，我们为你编写了一份资源列表。

- 维护

所有软件都会定期报告漏洞和安全通知。由于 LFS 系统是从源码编译的，因此由你来跟踪此类报告。有几个在线资源可以跟踪此类报告，其中一些显示如下：

- `CERT` (计算机应急响应小组)

`CERT` 有一个邮件列表，发布有关各种操作系统和应用程序的安全警报。订阅信息请见 http://www.us-cert.gov/cas/signup.html。

- `Bugtraq`

`Bugtraq` 是一个完全公开的安全邮件列表。它发布新发现的安全问题，并偶尔发布针对这些问题的潜在修复方案。订阅信息请见 http://www.securityfocus.com/。

- Beyond Linux From Scratch

《Beyond Linux From Scratch》书籍涵盖了 LFS 范围之外的广泛软件的安装程序。

- Linux Documentation Project

Linux 文档项目 (`TLDP`) 的目标是对所有问题进行协作。

第四部分. 附录

## 附录 A. 缩写与术语

- `ABI` Application Binary Interface 应用程序二进制接口

- `ALFS` Automated Linux From Scratch 自动化 Linux 从头

- `API` Application Programming Interface 应用程序编程接口

- `ASCII` American Code for Information Interchange 美国信息交换标准码

- `BIOS` Basic Input/Output System 基本输入/输出系统

- `BLFS` Beyond Linux From Scratch 超越 Linux 从头

- `BSD` Software Distribution BSD 软件发行版

- `chroot` 切换根

- `CMOS` Complementary Metal Semiconductor 互补金属半导体

- `COS` Class Of Service 服务类别

- `CPU` Central Processing Unit 中央处理器

- `CRC` Redundancy Check 冗余校验

- `CVS` Concurrent Versions System 并版本系统

- `DHCP` Dynamic Host Configuration Protocol 动态主机配置协议

- `DNS` Domain Name Service 域名服务

- `EGA` Enhanced Graphics Adapter 增强图形适配器

- `IEEE` Institute of Electrical and Electronic Engineers 电气工程师学会（通常是电气与电子）

- `ELF` Executable and Linkable Format 可执行链接格式

- `EOF` End of File 文件末尾

- `EQN` equation 方

- `ext2` second extended system 第二扩展文件系统

- `ext3` third extended system 第三扩展文件系统

- `ext4` fourth extended system 第四扩展文件系统

- `FAQ` Frequently Asked Questions 常见问题解答

- `FHS` Filesystem Hierarchy Standard 文件系统层次标准

- `FIFO` First-In, First Out 先后队列

- `FQDN` Fully Qualified Domain Name 完全限定域名

- `FTP` File Transfer Protocol 文件传输协议

- `GB` Gigabytes 吉字节

- `GCC` GNU Compiler Collection GNU 编译器

- `GID` Group Identifier 组标识符

- `GMT` Greenwich Mean Time 格林治标准时间

- `HTML` Hypertext Markup Language 超文本标记语言

- `IDE` Integrated Drive Electronics 集成式硬盘

- `IEEE` Institute of Electrical and Electronic Engineers 电气工程师学会

`IO` Input/Output 输入/输出

`IP` Internet Protocol 网协议

`IPC` Inter-Process Communication 进程间通信

`IRC` Internet Relay Chat 实时聊天

`ISO` International Organization for Standardization 国际标准组织

`ISP` Internet Service Provider 互联网服务提供

`KB` Kilobytes 千字节

`LED` Light Emitting Diode 发光二极管

`LFS` Linux From Scratch Linux 从头开始

`LSB` Standard Base Linux 标准基础

`MB` Megabytes 兆

`MBR` Master Boot Record 主引导记录

`MD5` Message Digest 5

`NIC` Network Card 网卡

`NLS` Native Language Support 原语言支持

`NNTP` Network News Transport Protocol 网络新闻传输协议

`NPTL` Native POSIX Threading Library POSIX 线程库

`OSS` Open Sound System 开源音频系统

`PCH` Pre-Compiled Headers 预编译头

`PCRE` Perl Regular Expression 兼容正则表达式

`PID` Process Identifier 进程标识符

`PTY` 伪终端

`QOS` Quality Of Service 服务质量

`RAM` Random Access Memory 随机访问内存

`RPC` Remote Procedure Call 远程过程调用

`RTC` Real Time Clock 实时时

`SBU` Standard Build Unit 标准构建单元

`SCO` The Santa Cruz Operation 产权公司

`SHA1` Secure-Hash Algorithm 1 安全哈希算法 1

`TLDP` The Linux Documentation Project Linux 文档项目

`TPTP` Trivial File Transfer Protocol 简单文件传输协议

`TLS` Thread-Local Storage 线程本地存储

`UID` User Identifier 用户标识符

`umask` user file-creation mask 用户创建掩码

`USB` Universal Serial Bus 通用总线

`UTC` Coordinated Universal Time 世界时

Linux From Scratch - Version 8.0



UUID Universally Unique Identifier 全局标识符

VC Virtual Console 虚拟控制台

VGA Video Graphics Adapter 视频适配器

VT Virtual Terminal 虚拟终端

## 附录 B. 致谢

感谢以下个人和组织对 Linux From Scratch 项目做出的贡献。

- Gerard Beekmans <gerard@linuxfromscratch.org> – LFS 创建者，LFS 项目负责人
- Matthew Dubbs <matthew@linuxfromscratch.org> – LFS 项目负责人，LFS 技术撰作者/编辑
- Bruce Dubbs <bdubbs@linuxfromscratch.org> – LFS 发布管理器，LFS 技术撰作者/编辑
- Jim Gifford <jim@linuxfromscratch.org> – CLFS 项目联合负责人
- Bryan Kadzban <bryan@linuxfromscratch.org> – LFS 技术撰作者
- Randy McMurchy <randy@linuxfromscratch.org> – BLFS 项目负责人，LFS way
- DJ Lucas <cd@linuxfromscratch.org> – LFS 和 BLFS 对应
- Ken Moffat <ken@linuxfromscratch.org> – LFS 和 CLFS 对应
- Ryan Oliver <ryan@linuxfromscratch.org> – CLFS 项目联合负责人
- 各 LFS 和 BLFS 邮件列表中的无数其他人员，他们通过建议、测试书籍、提交错误报告以及安装各种软件包的经验，使这本书得以成为。

## 翻译者

- Manuel Canales Esparcia <macana@macana-es.com> – 西班牙语 LFS 翻译项目
- Johan Lengelt <johan@linuxfromscratch.org> – 直至2008 年的法语 LFS 翻译项目
- Jean-Philippe Mengual <jmengual@linuxfromscratch.org> – 2008 年至今的法语 LFS 翻译项目
- Anderson Lizardo <lizardo@linuxfromscratch.org> – 葡萄牙语 LFS 翻译项目
- Thomas Reitelbach <tr@erdfunkstelle.de> – 德语 LFS 翻译项目

## 镜像维护者

### 美国镜像

- Scott Keton <scott@uosl.org> – lfs.oregonstate.edu 镜像
- William Axle <last@l-web.net> – ca.linuxfromscratch.org 镜像
- Ejon Sellers <jpolen@rackspace.com> – lfs.introspeed.com 镜像
- Justin Knierim <tim@edge.net> – lfs-matrix.net 镜像

### 南美镜像

- Manuel Canales Esparcia <manuel@linuxfromscratch.org> – Lsfmirror.lfs-es.info 镜像
- Luis Falcon <Luis Falcon> – torredehanoi.org 镜像

### 欧洲镜像

- Guido Passet <guido@primelay.net> – nl.linuxfromscratch.org 镜像
- Bastian Jacques <baafie@planet.net> – lfs.pagefault.net 镜像
- Sven Cranshof <sven.cranshof@lineo.be> – lfs.lineo.be 镜像
- Scarlet Belgium – lfs.scarlet.be 镜像
- Sebastian Faulborn <info@aliensoft.org> – Lfs.aliensoft.org 镜像
- Stuart Fox <stuart@dentouse.ms> – Lfs.dentouse.ms 镜像
- Ralf Uhlemann <admin@realhost.de> – Lfs-oss.ror.org 镜像
- Antonin Sprinzl <Antonin.Sprinzl@twien.at> – at.linuxfromscratch.org 镜像
- Fredrik Danerklint <fredan-lfs.fredan.org> – se.linuxfromscratch.org 镜像
- Franck <frank@linuxpoursit.com> – Lfs.linuxpoursit.com 镜像
- Philippe Baque <baque@cict.fr> – Lfs.cict.fr 镜像
- Vitaly Cheekasin <gyouja@pilgrims.ru> – Lfs.pilgrims.ru 镜像
- Benjamin Heel <kantakt@wankoo.org> – Lfs.wankoo.org 镜像

### 亚洲镜像

- Satit Phersmawang <satit@wbac.ac.th> – Lfs.phayone.org 镜像
- Shizunet Co.,Ltd. <info@shizu-net.jp> – Lfs.mirror.shizu-net.jp 镜像
- Init World <http://www.itworld.com> – Lfs.itworld.com 镜像

### 澳洲镜像

- Jason Andrade <jason@dst.edu.au> – au.linuxfromscratch.org 镜像

### 前项目团队成员

- Christine Barczak <theladyske@linuxfromscratch.org> – LFS 书籍编辑
- Archaic <archaic@linuxfromscratch.org> – LFS 技术撰作者/编辑，LFS 项目负责人，BLFS 编辑员，提示与补丁
- Nathan Coulson <nathan@linuxfromscratch.org> – Robert Briggs
- Timothy Boucher Ian Chilton
- Jeroen Coumans <jeroen@linuxfromscratch.org> – 网站开发者
- Manuel Canales <manuel@linuxfromscratch.org> – LFS/BLFS 和 XSL
- Alex Groenew Heerdink
- Jeremy Hunt <jhuntwork@linuxfromscratch.org> – 技术撰作者，LFS LiveCD
- Nicholson <dnicholson@linuxfromscratch.org> – Alexander E. Patrakov, LFS 国际化
- Simon McPherson <scot@linuxfromscratch.org> – Perreault
- Greg Schafer <gschafer@zip.com> – LFS 技术撰作者及下一代构建方法架构师
- James Robertson <jwrober@linuxfromscratch.org> – Jesse Tie-Queue
- Tushar <tushar@linuxfromscratch.org> – BLFS 书籍编辑，提示与脚本
- Winkles <winkles@gmail.com> –

## C. 依赖

许多软件包依赖于其他软件包才能构建或运行。在本章节中，我们将详细说明这些依赖关系。

# Linux 从头构建 版本 8.0

# DejaGNU

安装依赖于：`Bash`, `Coreutils`, `Diffutils`, `GCC`, `Grep`, `Make`, 和 `Sed`

测试套件依赖于：无

必须在之前：无

可选依赖：无

# Diffutils

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Gettext`, `Glib`, `Grep`, `Make`, `Sed`, 和 `Texinfo`

测试套件依赖于：`Diffutils`, `Perl`

必须在之前：无

可选依赖：无

# Eudev

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Glib`, `Grep`, `Gperf`, `Make`, 和 `Sed`

测试套件依赖于：无

必须在之前：无

可选依赖：无

# Expat

安装依赖于：`Bash`, `Binutils`, `Coreutils`, `Gawk`, `GCC`, `Glib`, `Grep`, `Make`, 和 `Sed`

测试套件依赖于：无

必须在之前：`XML::Parser`



# Linux 从头构建 版本 8.0

## Expect
安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Grep, Make, Patch, Sed, 和 Tcl
测试套件依赖于：无
必须在之前：无
可选依赖：无

## E2fsprog
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glib, Grep, Gzip, Texinfo, 和 Util-linux
测试套件依赖于：Procs-ng, Psmisc
必须在之前：无
可选依赖：无

## File
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glib, Grep, Make, Sed, 和 Zlib
测试套件依赖于：无
必须在之前：无
可选依赖：无

## Findutils
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Gep, Make, Sed, 和 Texinfo
测试套件依赖于：DejaGNU, Diffutils, 和 Expect
必须在之前：无
可选依赖：无

## Flex
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Gep, M4, Make, Patch, Sed, 和 Texinfo
测试套件依赖于：Bison 和 Gawk
必须在之前：IPRoute2, Kbd, 和 Man-DB
可选依赖：无

## Gawk
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, GMP, Gep, Make, MPFR, Patch, Sed 和 Texinfo
测试套件依赖于：Diffutils
必须在之前：无
可选依赖：无

## Gcc
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Findutils, Gawk, GCC, Gettext, Glib, GMP, Gep, M4, Make, MPC, MPFR, Patch, Perl, Sed, Tar, 和 Texinfo
测试套件依赖于：DejaGNU 和 Expect
必须在之前：CLooG-PPL, GNAT 和 PPL

## GDBM
安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Gep, Make, 和 Sed
测试套件依赖于：无
必须在之前：无
可选依赖：无

## Gettext
安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Glib, Gep, Make, Sed, 和 Texinfo
测试套件依赖于：Diffutils, Perl, 和 Tcl
必须在之前：Automake
可选依赖：无

## Glibc
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Gettext, Gep, Gzip, Linux API Headers, Make, Perl, Sed, 和 Texinfo
测试套件依赖于：File
必须在之前：无
可选依赖：无

## GMP
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, M4, Make, Sed 和 Texinfo
测试套件依赖于：无
必须在之前：MPFR, GCC
可选依赖：无

## Gperf
安装依赖于：Bash, Binutils, Coreutils, GCC, Make
测试套件依赖于：Diffutils, Expect
必须在之前：无
可选依赖：无

## Grep
安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Gettext, Glibc, Grep, Make, Patch, Sed, 和 Texinfo
测试套件依赖于：Gawk
必须在之前：Man-DB
可选依赖：Pcre

## Groff
安装依赖于：Bash, Binutils, Bison, Coreutils, Gawk, GCC, Grep, Make, Patch, Sed, 和 Texinfo
测试套件依赖于：无可用的测试套件
必须在之前：Man-DB 和 Perl
可选依赖：GPL Ghostscript

## GRUB
安装依赖于：Bash, Binutils, Bison, Coreutils, Diffutils, GCC, Gettext, Glibc, Grep, Make, Ncurses, Sed, Texinfo, 和 Xz
测试套件依赖于：无
必须在之前：无
可选依赖：无

## Gzip
安装依赖于：Bash, Binutils, Coreutils, GCC, Glibc, Grep, Sed, 和 Texinfo
测试套件依赖于：Diffutils
必须在之前：Man-DB
可选依赖：无

## Iana
安装依赖于：Coreutils, Gawk
测试套件依赖于：无测试套件
必须在之前：无

## Inetutils
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Grep, Make, Sed, 和 Texinfo
测试套件依赖于：无测试套件
必须在之前：无
可选依赖：无

## Intltool
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Perl
测试套件依赖于：
必须在之前：无
可选依赖：无

## IProute2
安装依赖于：Bash, Binutils, Coreutils, Flex, GCC, Glibc, Make
测试套件依赖于：无测试套件
必须在之前：无
可选依赖：无

## Kbd
安装依赖于：Bash, Binutils, Coreutils, Flex, Getext, Glibc, Gzip, Sed
测试套件依赖于：无测试套件
必须在之前：无
可选依赖：无

## Kmod
安装依赖于：Bash, Binutils, Bison, Coreutils, Flex, Getext, Glibc, Gzip, Make, Xz
测试套件依赖于：无测试套件
必须在之前：Eudev
可选依赖：无

## Less
安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Glibc, Grep, Ncurses, Sed
测试套件依赖于：无测试套件
必须在之前：Gzip
可选依赖：Pcre

## Libcap
安装依赖于：Attr, Bash, Binutils, Coreutils, GCC, Glibc, Perl, Sed
测试套件依赖于：无测试套件
必须在之前：无
可选依赖：Linux-PAM

## Libpipeline
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, Make, Sed, 和 Texinfo
测试套件依赖于：Check
必须在之前：Man-DB
可选依赖：无

## Libtool
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, Make, Sed, 和 Texinfo
测试套件依赖于：Autoconf, Automake, Findutils
必须在之前：无
可选依赖：无

## Linux Kernel
安装依赖于：Bash, Bc, Binutils, Coreutils, Diffutils, Findutils, GCC, Glibc, Grep, Gzip, Kmod, Make, Perl, 和 Sed
测试套件依赖于：无可用的测试套件
必须在之前：OpenSSL
可选依赖：无

## M4
安装依赖于：Bash, Binutils, Coreutils, GCC, Glibc, Grep, Make, Sed, 和 Texinfo
测试套件依赖于：Diffutils
必须在之前：Autoconf 和 Bison
可选依赖：libsigsev

## Make
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glibc, Grep, Make, Sed, 和 Texinfo
测试套件依赖于：Perl 和 Propcs-ng
必须在之前：无
可选依赖：无

## Man-DB



安装依赖于：Bash, Binutils, Bzip2, Coreutils, Flex, GCC, GDBM, Gettext, Glibc, Grep, Groff, Gzip, Less, Libpipeline, Make, Sed, 和 Xz

测试套件依赖于：Util-linux

必须在之前：无

可选依赖：无

# Man-Pages

安装依赖于：Bash, Coreutils, 和 Make

测试套件依赖于：无可用的测试套件

必须在之前：无

可选依赖：无

# Linux 从零开始 - 版本 8.0

## MPC

安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, GMP, Make, MPFR 和 Texinfo

测试套件依赖于：无

必须在 GCC 之前安装

可选依赖：无

## MPFR

安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, GMP, Make, Sed 和 Texinfo

测试套件依赖于：无

必须在 Gawk 之前安装

可选依赖：无

## Ncurses

安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, Make, Patch, Sed

测试套件依赖于：无可用的测试套件

必须在 Bash, GRUB, Inetutils, Less, Procs-ng, Psmisc, Readline, Texinfo, Util-linux 和 Vim 之前安装

可选依赖：无

## Patch

安装依赖于：Bash, Binutils, Coreutils, GCC, Glibc, Grep, Make 和 Sed

测试套件依赖于：Diffutils

必须在之前：无

可选依赖：Ed

## Perl

安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, GDBM, Glib, Grep, Groff, Make 和 Zlib

测试套件依赖于：Iana-Etc 和 Procs-ng

必须在 Autoconf 之前安装

可选依赖：无

## Pkg-config

安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Glibc, Grep, Make, Popt 和 Sed

测试套件依赖于：无

必须在 Kmod 之前安装

可选依赖：无

## Popt

安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Glibc, Grep, Make

测试套件依赖于：Diffutils 和 Sed

必须在 Pkg-config 之前安装

可选依赖：无

## Procs-ng

安装依赖于：Bash, Binutils, Coreutils, GCC, Glib, Make 和 Ncurses

测试套件依赖于：DejaGNUU

必须在之前：无

可选依赖：无

## Psmisc

安装依赖于：Bash, Binutils, Coreutils, GCC, Getext, Glibc, Grep, Make, Ncurses 和 Sed

测试套件依赖于：无可用的测试套件

必须在之前：无

可选依赖：无

## Readline

安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Glibc, Grep, Make, Ncurses, Patched, Sed 和 Texinfo

测试套件依赖于：无可用的测试套件

必须在 Bash, Gawk 之前安装

可选依赖：无

## Sed

安装依赖于：Bash, Binutils, Coreutils, GCC, Getext, Glibc, Grep, Make, Sed 和 Texinfo

测试套件依赖于：Diffutils 和 Gawk

必须在 E2fsprogs, File, Libtool 和 Shadow 之前安装

可选依赖：Cracklib

## Shadow

安装依赖于：Bash, Binutils, Coreutils, Diffutils, Findutils, Gawk, GCC, Getext, Glibc, Make 和 Sed

测试套件依赖于：无可用的测试套件

必须在 Coreutils 之前安装

可选依赖：Acl, Attr, Cracklib, PAM

## Syslogd

安装依赖于：Binutils, Coreutils, GCC, Glibc, Make 和 Patch

测试套件依赖于：无可用的测试套件

必须在之前：无

可选依赖：无

## Sysinit

安装依赖于：Binutils, Coreutils, GCC, Glibc, Make 和 Sed

测试套件依赖于：无可用的测试套件

必须在之前：无

可选依赖：无

## Tar

安装依赖于：Acl, Attr, Bash, Binutils, Bison, Coreutils, GCC, Gettext, Glibc, Grep, Inutils, Make, Sed 和 Texinfo

测试套件依赖于：Autocf, Diffutils, Findutils, Gawk 和 Gzip

必须在之前：无

可选依赖：无

## Tcl

安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Glib, Grep, Make 和 Sed

测试套件依赖于：无

必须在之前：无

可选依赖：无

## Texinfo

安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glib, Grep, Make, Ncurses, Patch 和 Sed

测试套件依赖于：无

必须在之前：无

可选依赖：无

## Util-linux

安装依赖于：Bash, Binutils, Coreutils, Diffutils, Findutils, Gawk, GCC, Gettext, Glibc, Grep, Ncurses, Sed, Eudev 和 Zlib

测试套件依赖于：无

必须在之前：无

可选依赖：libcap-ng

## Vim

安装依赖于：Acl, Attr, Bash, Binutils, Coreutils, Diffutils, GCC, Glibc, Grep, Make, Nursed 和 Sed

测试套件依赖于：无

必须在之前：无

可选依赖：Xorg, GTK+2, LessTif, Python, Tcl, Ruby 和 GPM

## XML::Parser

安装依赖于：Bash, Binutils, Coreutils, Expat, GCC, Glib, Make 和 Perl

测试套件依赖于：Perl

必须在 Inttool 之前安装

可选依赖：无

## XZ

安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Glib 和 Make。

测试套件依赖于：无

必须在 GRUB, Kmod, DB, Ude 之前安装

可选依赖：无

## Zlib

安装依赖于：Bash, Binutils, Coreutils, GCC, Glibc, Make 和 Sed

测试套件依赖于：无

必须在 File, Perl 和 Util-linux 之前安装

可选依赖：无

## 附录 D 启动和配置脚本

本附录中的脚本按它们通常所在的目录列出。顺序为 `/etc/rc.d/init.d/`、` /etc/sysconfig` `/etc/sysconfig/network-devices`。在每个部分中，文件按照正常调用的顺序列出。

### D1. /etc/rc.d/init.d/rc

rc 脚本是 init 调用的第一个脚本，并启动启动过程。

```bash
#!/bin/bash
################################################
# Main Run Level Script
# Authors : Gerard Beek - gerard@linuxscratch.org
# : DJ Lucas - dlj@linuxscratch.org
# Update : Bruce - bdbbs@linuxscratch.org
# Version : 7.0
################################################

/etc/rc.d/init.d/rc
```



```bash
if [ "${runlevel}" != "0" -a "${runlevel}" != "6" ]; then
  if [ ! -f ${prev_start} -a ! -f ${sysinit_start} ]; then
    MSG="警告:\n\(${i})无法执行，因为它没有在之前的运行级别 (${previous})中启动。"
    log_warning_msg "${MSG}"
    continue
  fi
fi

run $(i) stop
error_value=$(?)

if [ "${error_value}" != "0" ]; then
  print_error_msg
fi

if [ "${previous}" == "N" ]; then
  export IN_BOOT=1
fi
```

```bash
if [ "${runlevel}" == "6" -a -n "${FASTBOOT" ]; then
  touch /fastboot
fi

# 启动此运行级别下的所有函数
for i in $(ls -v /etc/rc.d/rc${runlevel}.d/$S 2> /dev/null)
do
  if [ "${previous}" == "N" ]; then
    suffix+=$(i#/etc/rc.d/rcrunlevel.d/$S[0-9])[0-9])
    stop=/etc/rc.d/rcrunlevel.d/K[0-9][0-9]$suffix
    prev_start=$(/etc/rc.d/S[0-9][0-9]$suffix)
  fi

  if [ -f ${prev_start} -a ! -f ${stop} ]; then
    continue
  fi

  check_script_status

  case ${runlevel} in
    0|6)
      run $(i) stop
      ;;
    *)
      run $(i) start
      ;;
  esac

  error_value=$(?)

  if [ "${error_value}" != "0" ]; then
    print_
# 在运行级别 S 上存储交互式开关，如果不存在则删除
if [ "${runlevel}" == "S" -a "${interactive}" == "i" ]; then
  echo "interactive=\$i" > /var/run/interactive
else
  rm -f /var/run/interactive > /dev/null
fi

# 仅在初始启动时复制启动日志
if [ "$previous" == "N" -a "$runlevel" != "S" ]; then
  cat $BOOTLOG >> /var/log/boot.log
fi

# 标记启动结束
echo "----------" >> /var/log/boot.log

# 删除临时文件
rm -f $BOOTLOG > /dev/null

fi

# 结束 rc
```

### D.2./lib/lsb/init-functions

```bash
#!/bin/sh
################################################################################
# 开始 /lib/lsb/init-functions
# 描述：运行级别控制函数
# 作者：Gerard Beekmans - gerard@linuxfromscratch.org
# : DJ Lucas - dj@linuxfromscratch.org
# 更新：Bruce Dubbs - dbubbs@linuxfromscratch.org
# 版本：LFS 7.0
# 备注：代码基于 Matthias Beckmann 的 simpleinit-msb
      http://winterdrache.de/linux/newboot/index.html
# 该文件应位于 /lib/lsb
```

#### 环境设置

# 设置环境的默认值

umask 022

export PATH=/var/bin:/usr/sbin:/usr/sbin

# 设置颜色命令，通过 echo 使用

# 请参阅 man console_codes 获取更多信息

# 位于 "ECMA-48 Set Graphics Rendition" 部分

# 警告：当从 8 位字体切换到 9 位字体时，

# linux 控制台将把粗体 (1) 重新解释为

# 9 位字体的前 256 个形状。这

# 不影响帧缓冲区控制台

```bash
NORMAL="\u0033[0;39m" # 标准控制台灰色
SUCCESS="\u0033[0;32m" # 为绿色
WARNING="\u0033[1;31m" # 警告为红色
FAILURE="\u0033[1;31m"
```

# 信息为浅青

# 括号为蓝色

```bash
# 使用彩色前缀
BMPREFIX=""

SUCCESS_PREFIX="$(SUCCESS) * $(NORMAL)"
FAILURE_PREFIX="$(FAILURE)****** $(NORMAL)"
WARNING_PREFIX="$(WARNING) *** $(NORMAL)"
SKIP_PREFIX="$(INFO) S $(NORMAL)"

SUCCESS_SUFFIX="$(BRACKET)][${$(SUCCESS)} OK ${BRACKET}$(NORMAL)}"
FAILURE_SUFFIX="$(BRACKET)][${$(FAILURE)} FAIL ${BRACKET}$(NORMAL)}"
WARNING_SUFFIX="$(BRACKET)][${$(WARNING)} WAR ${BRACKET}$(NORMAL)}"
SKIP_SUFFIX="$(BRACKET)][${$(INFO)} SKIP ${BRACKET}$(NORMAL)}"

BOOTLOG=/run/boot
KILLEDAY=3

# 设置任何用户定义的环境变量，例如 HEADLESS
- /etc/sysconfig/rc.site && . /etc/sysconfig/rc.site

# 屏幕尺寸
# Find当前屏幕大小
if [ -z "${COLUMNS}" ]; then
  COLUMNS=$(tty size)
  COLUMNS=$((COLUMNS))
fi

# 当远程连接时，例如串口端口，stty size 返回 0
if [ "${COLUMNS}" = "0" ]; then
  COLUMNS=80
fi

# 设置光标位置，通过 echo 使用
SET="\033[$G" # 在 $ 字符处
SET_W="\033[$W" # 见原文未完整显示，此处保持逻辑对齐
SET="\033[$G" # 在 $ 字符处
SET_W="\033[$W" # 见原文未完整显示，此处保持逻辑对齐
```

*(注：由于提供的原文文本在 SET_W 处出现了截断和重复，此处已根据上下文逻辑对翻译部分进行了处理。)*

### Linux From Scratch - Version 8

```bash
# 然而，它没有被当前的实现或标准使用。
pidlist="pidfof -p "${pidfile}" "${$1}"
retval="${retval}"
```



```bash
# 仅返回值
# 记录日志是初始化脚本（或发行版函数）的责任！
case "${retval}" in
  # 程序运行正常
  # 此处什么都不做，让 killproc 继续执行。
  ;;

  # 只有在没有传递信号时，这里才成功。
  if [ -n"${nosig}" ]; then
    return 0
  else
    return 7
  fi

  # 程序未运行且不存在 pidfile
  # 只有在没有传递信号时，这里才成功。
  if [ -n"${nosig}" ]; then
    return 0
  else
    return 7
  fi

  # 其他由状态值返回的内容不应被解释，
  # 并作为未知错误返回。
  return 1
esac

if [ "${retval}" -eq "0" ]; then # 信号用于终止程序
  # 考虑到 pidlist 为空（pid 文件仍存在且未给出信号
  if [ "${pidlist}" != "" ]; then
    # 杀死 PID 列表
    for pid in ${pidlist}; do
      kill -0 "$(pid)" 2> /dev/null
      if [ "$($?)" -ne "0" ]; then
        # 进程已死，继续处理并假设一切正常
        continue
      else
        kill "$(signal)" "$(pid)" 2> /dev/null
        # 等待最多 ${delay}/10 秒让 "$(pid)" 
        # 以 0.1 秒为单位进行终止
        while [ "${delay}" -ne "0" ]; do
          kill -0 "$(pid)" 2> /dev/null || piddead="1"
          if [ "${piddead}" = "1" ]; then break; fi
          sleep 0.1
          delay=$($($(delay) - 1))
        done

        # 如果设置了备用方案且程序仍在运行，
        # 则使用备用方案
        if [ -n "${fallback}" -a "${piddead}" != "1" ]; then
          kill "$(signal)" "$(pid)" 2> /dev/null
          sleep 1
          # 再次检查，如果仍在运行则失败
          kill -0 "$(pid)" 2> /dev/null && return 1
        fi
      fi
    done

    # 检查并移除过期的 PID 文件。
    if [ -z "${pidfile}" ]; then
      # 获取 $program 的基名
      prefix=$(echo "${program}" | sed 's/[^/]*$//')
      programe=$(echo "${program}" | sed "s@${prefix}*@")

      if [ -e "/var/run/${programe}.pid" ]; then
        rm -f "/var/run/${programe}.pid" 2> /dev/null
      fi
    fi
    if [ -f "${pidfile}" ]; then
      rm -f "${pidfile}" 2> /dev/null
    fi
  else
    # 对于不期望程序退出的信号，只需让
    # kill 执行工作，并对 kill 的返回值进行检查
    # check_sig_type - 信号未用于终止程序
    for pid in ${pidlist}; do
      kill "$(signal)" "$(pid)"
      if [ "$($?)" -ne "0" ]; then return 1; fi
    done
  fi
fi
```

################################################################################

# `pidofproc()`

# 用法: `pidofproc [-p pidfile] filename`

#

# 目的: 此函数返回某个特定守护进程的一个或多个 PID

#

# 输入: `-p pidfile`，使用指定的 `pidfile` 代替 `pidof` 路径，指定程序的路径

#

# 返回值（根据 LSB 状态码定义）：

# `0` - 成功（将 PID 输出到 stdout）

# `1` - 程序已死，PID 文件仍存在（输出剩余 PID）

# `3` - 程序未运行（无输出）

################################################################################

```bash
pidofproc()
{
  local pidfile
  local prefix
  local progname
  local pidlist
  local lpid
  local exitstatus="0"

  # 处理参数
  while true; do
    case "${1}" in
      -p)
        pidfile="${2}"
        shift 2
        ;;
      *)
        program="${1}"
        if [ -n "${2}" ]; then
          # 参数过多
          # 因为这是状态查询，返回未知
          return 4
        else
          break
        fi
    esac
  done

  # 如果未指定 PID 文件，尝试查找一个。
  if [ -z "${pidfile}" ]; then
      # 获取程序的基名
      prefix=$(echo "${program}" | sed 's/[^/]*$//')

      if [ -z "${prefix}" ]; then
        progname="${program}"
      else
        progname=$(echo "${program}" | sed "s@${prefix}*@")
      fi

      # 如果存在同名的 PID 文件，则假设它就是。
      if [ -e "/var/run/${progname}.pid" ]; then
        pidfile="/var/run/${progname}.pid"
      fi
  fi

  # 如果设置了 PID 文件且存在，则使用它。
  if [ -n "${pidfile}" -a -e "${pidfile}" ]; then
    # 使用 pidfile 第一行的值
    pidlist=$(head -n 1 "${pidfile}")
    # 这可以可选写为 'sed lq' 来替换 'head -nl'
    # 如果 LFS 将 /bin/head 移动到 /usr/bin/head
  else
    # 使用 pidof
    pidlist=$(pidof "${program}")
  fi

  # 确认所有列出的 PID 都在运行。
  for pid in ${pidlist}; do
    kill -0 "${pid}" 2> /dev/null
    if [ "$$?" -eq 0 ]; then
      lpids="${lpids}"
    else
      exitstatus="1"
    fi
  done

  if [ -z "${lpids}" ]; then
    return 3
  else
    return "${exitstatus}"
  fi
}
```

## 从日志文件中移除非可打印字符

```bash
timespec
logmessage=`echo "$@" | sed 's/\\033[a-zA-Z]*///g'
/bin/echo -e "${STAMP} ${logmessage} FAIL >> ${BOOTLOG}"

return 0
```

```bash
log_failure_msg2()
{
  /bin/echo -n -e "${BMPREFIX}${@"
  /bin/echo -e "${CURS_ZERO}${FAILURE_PREFIX}${SET_COL}${FAILURE_SUFFIX}"

  echo "FAIL" >> ${BOOTLOG}

  return 0
}
```



## `log_warning_msg()`

```bash
######################################################################
# log_warning_msg()
# 用法: log_warning_msg ["message"
#
#set: 将警告消息打印到屏幕和
# 启动日志文件。
#
# 返回值: 未使用
######################################################################
```

```bash
log_warning_msg()
{
  /bin/echo -n -e "${BMPREFIX}${@"
  /bin/echo -e "${CURS_ZERO}${WARNING_PREFIX}${SET_COL}${WARNING_SUFFIX}"

  # 从日志文件中移除非可打印字符
  logmessage=`echo "$@" | sed 's/\\033[a-zA-Z]*///g'
  timespec
  /bin/echo -e "${STAMP} ${logmessage} WAR >> ${BOOTLOG}"

  return 0
}
```

## `log_skip_msg()`

```bash
log_skip_msg()
{
  /bin/echo -n -e "${BMPREFIX}${@"
  /bin/echo -e "${CURS_ZERO}${SKIP_PREFIX}${SET_COL}${SKIP_SUFFIX}"

  # 从日志文件中移除非可打印字符
  logmessage=`echo "$@" | sed 's/\\033[a-zA-Z]*///g'
  /bin/echo -e "${SKIP} >> ${BOOTLOG}"

  return 0
}
```

## `log_info_msg()`

```bash
######################################################################
# log_info_msg()
# 用法: log_info_msg message
#
#set: 将信息消息打印到屏幕和
# 启动日志文件。不打印末尾换行字符。

# 返回值: 未使用
################################################################################################
log_info_msg()
{
  /bin/echo -ne "${BMPREFIX}${@}"

  # 从日志文件中移除非可打印字符
  logmessage=`echo "${@}" | sed 's/\\033\[a-zA-Z].*//g'
  timespec
  /bin/echo -ne "${STAMP} ${logmessage}" >> ${BOOTLOG}

  # 从日志文件中移除非可打印字符
  logmessage=`echo "${@}" | sed 's/\\033\[a-zA-Z].*//g'
  /bin/echo -ne "${logmessage}" >> ${BOOTLOG}

  return 0
}
```

## `evaluate_retval()`

```bash
################################################################################################
# evaluate_retval()
# 用法: 评估返回值并根据情况打印成功或失败
#set: 用于终止信息消息的便利函数
# 返回值: 未使用
################################################################################################
evaluate_retval()
{
  local error_value="${?}"
  if [ ${error_value} -eq 0 ]; then
    log_success_msg2
  else
    log_failure_msg2
  fi
}
```

## `check_signal()`

```bash
################################################################################################
# check_signal()
# 用法: check_signal [ -signal ] | [signal]
#set: 检查有效信号。这没有在任何 LSB 草案中定义，
# 然而，需要检查信号以确定其他函数选择的
# 信号是否为函数的无效参数。
# 输入: 接受格式为 -{signal} 或 {signal} 的单个字符串值
### Linux From Scratch - Version 8.0

# 返回值:
# 0 - 成功（信号有效）
# 1 - 信号无效

check_signal(){
    local valsig

    # 为无效信号添加错误处理
    valsig="-ALRM-HUP-INT-PIPE-POLL-PROF-TERM-USR1-USR2"
    valsig="$valsig -VTALRM-STKFLT-PWR-WINCH-ILL-URG-TSTP-TTIN"
    valsig="$valsig -TTOU-STOP-CONT-ABERT-PFE-ILL-QUIT-SEGV-TRAP"
    valsig="$valsig -SYS-EMT-BUS-XPU-XFSZ -0-1-2-3-4-5-6-8-9"
    valsig="$valsig -11 -13 -14 -15"

    echo "$valsig" | grep - "${1}" > /dev/null

    if [ "${1}" -eq "0" ]; then
        return 0
    else
        return 1
    fi
}
```

## `check_sig_type()`

```bash
# check_sig_type([ {signal} | {signal} ])
#set: 检查信号是程序终止信号还是控制信号
# 这没有在任何 LSB 草案中定义，有需要
# 检查信号以确定它们是意在结束程序
# 还是仅仅为了控制它。

# 输入: 接受格式为 -{signal} 或 {signal} 的单个字符串值
# 返回值:
# 0 - 成功（信号有效）
# 1 - 信号无效

check_sig_type(){
    local valsig

    # 为无效信号添加错误处理
    valsig="-ALRM-HUP-INT-PIPE-POLL-PROF-TERM-USR1-USR2"
    valsig="$valsig -VTALRM-STKFLT-PWR-WINCH-ILL-URG-TSTP-TTin"
    valsig="$valsig -TTOU-STOP-CONT-ABERT-PFE-ILL-QUIT-SEGV-TRAP"
    valsig="$valsig -SYS-EMT-BUS-XPU-XFSZ -0-1-2-3-4-5-6-8-9"
    valsig="$valsig -11 -13 -14 -15"

    echo "$valsig" | grep - "${1}" > /dev/null

    if [ "${1}" -eq "0" ]; then
        return 0
    else
        return 1
    fi
}
```

```bash
if [ -n "${failedmod}" ]; then
  log_failure_msg "加载模块失败:${failedmod}"
  exit 1
fi
;;

)
echo "用法: $(0) (start)"
  exit 1
  ;
esac

exit 0
```

### D.5. `/etc/rc.d/init.d/udev`



# D.6 /etc/rc.d/init.d/swap

```bash
#!/bin/sh
################################################################################
# 开始 swap
# 描述 : 交换控制脚本
#
# 作者 : Gerard Beekemans - gerard@linuxfromscratch.org
DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - bdububs@linuxfromscratch.org
#
# 版本 : LFS 7.0
################################################################################

### BEGIN INIT INFO
# Provides: swap
# Required-Start: udev
# Should-Start: modules
# Required-Stop: localnet
# Should-Stop: S
# Default-Start: 0 6
# Default-Stop:
# Short-Description: 挂载和卸载交换分区。
# Description: 挂载和卸载 `/etc/fstab` 中定义的交换分区。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions

case "$1" in
  start)
  log_info_msg "激活所有交换文件/分区..."
  swapon -a
  evaluate_retval
  ;;

stop)
  log_info_msg "取消激活所有交换文件/分区..."
  swapoff -a
  evaluate_retval
  ;;

restart)
  $0 stop
  sleep 1
  $0 start
  ;;

status)
  log_success_msg "正在获取交换状态。"
  swapon -s
  ;;

*)
  echo "用法: $0 {start|stop|restart|status}"
  exit 1
  ;;
esac

exit 0
# 结束 swap
```

# D.7 /etc/rc.d/init.d/setclock

```bash
#!/bin/sh
################################################################
# 开始 setclock
# 描述 : 设置 Linux 时钟
# 作者 : Gerard Beekmans - gerard@linuxfromscratch.org
DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - dbubbs@linuxfromscratch.org
# 版本 : LFS 7.0
################################################################

### BEGIN INIT INFO
# Provides:
# Required-Start: modules
# Should-Start:
# Required-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 从硬件时钟存储并恢复时间
# Description: 在启动时，系统时间从 hwclock 获取。
# 硬件时钟也可以在关机时设置。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions

[ -r /etc/config/clock ] && . /etc/config/clock

case "$UTC" in
  true)
    CLOCKPARAMS="utc"
  ;;
  false)
    CLOCKPARAMS="localtime"
  ;;
esac

case "$1" in
  start)
    hwclock ${CLOCKPARAMS} >/dev/null
    ;;

  stop)
    log_info_msg "设置时钟..."
    hwclock ${CLOCKPARAMS} >/dev/null
    ;;

  *)
    echo "用法: $0 {start|stop}"
    exit 1
    ;;
esac

exit 0
```

# D.8 /etc/rc.d/init.d/checkfs

```bash
#!/bin/sh
############################################################
# 开始 udev
# 描述 : Udev 热插脚本
# 作者      : Zack Winkles, Alexander E. Patrakov
#              DJ Lucas - dj@linuxfromscratch.org
# 更新      : Bruce Dubbs - dbububs@linuxfromscratch.org
# 版本      : LFS 7.0
############################################################

### BEGIN INIT INFO
# Provides:          udev $time
# Required-Start:    modules
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:     S
# Default-Stop:
# Short-Description: 在 /dev 中填充设备节点。
# Description:       将 temps 挂载到 /dev 并启动 udev 守护进程。
                    设备节点根据 udev 的定义创建。
# X-LFS-Provided-By:  LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions
case "$1" in
  start)
  log_info_msg "正在 /dev 中填充设备节点..."
  if grep -q '[[[:space:]]*sysfs/proc/modules'; then
    log_failure_msg2
    msg="失败:\n\n无法创建 SysFS 文件系统\n\n"
    msg="${msg}缺少没有 SysFS 文件系统的设备\n\n"
    msg="${msg}在你按下回车后，此系统"
    msg="${msg}将停止并关机。\n\n"
    log_info_msg "$msg"
    log_info_msg "按回车键继续..."
    wait_for_user
    /etc/rc.d/init.d/halt stop
fi

# 启动 udev 守护进程以持续监控并处理
# uevents
/sbin/udevd --daemon

# 现在遍历 /sys 以“冷插拔”已经发现的设备
/sbin/udevadm trigger --action=add --type=subsystems
/sbin/udevadm trigger --action=add --type=devices
/sbin/udevadm trigger --action=change --type=devices

# 等待 udevd 处理我们触发的更改
if ! is_true "$OMIT_UDE_SETTLE"; then
  /sbin/udevadm settle
fi

# 如果系统上有任何 LVM 分区，确保它们
# 已被激活以供使用。
if [ -x /sbin/vgchange ]; then /sbin/vgchange -a y >/dev/null; fi

log_success_msg2
;;

*)
echo "用法 $0 {start}"
exit 1
esac

exit 0

# 结束 udev
```



# D.10. `/etc/rc.d/init.d/udev_retry`

## `checkfs` 初始化脚本

```bash
#!/bin/sh
################################################
# 开始 checkfs
# 描述 : 文件系统检查
# 作者 : Gerard Beekemans - gerard@linuxfromscratch.org
DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - dbububs@linuxfromscratch.org
# 版本 : LFS 7.0
################################################

### BEGIN INIT INFO
# Provides: checkfs
# Required-Start: modules
# Should-Start:
# Required-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 在挂载前检查文件系统。
# Description: 在启动时，通过 fsck 检查文件系统。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions

case "$1" in
  start)
    if [ -f /fastboot ]; then
      msg="fastboot 已启用，跳过文件系统检查。"
      log_info_msg "$msg"
      exit 0
    fi

    log_info_msg "以只读模式挂载根文件系统..."
    mount -o remount,ro /

    if [ $? -ne 0 ]; then
      _retval
      msg="无法挂载根文件系统 "
      msg="${msg}因为它处于只读模式。\n\n"
      msg="${msg}在你按下回车后，此系统"
      msg="${msg}将停止并关机。\n\n"
      log_failure_msg "${msg}"

      log_info_msg "按回车键继续..."
      wait_for_user
      /etc/rc.d/init.d/halt stop
    else
      log_success_msg

      if [ -f /forceck ]; then
        msg="/forceck 已启用，强制进行文件系统检查。"
        log_success_msg="${msg}"
        options="-f"
      else
        options=""
      fi

      log_info_msg "检查文件系统..."
      # 注意：使用 -p 参数但在 fsck 中会失败
      if is_true "VERBOSE_FSCK"; then
        fsck (${options}) -a -C
      else
        fsck (${options}) -A -C >/dev/null
      fi

      error_value=$?

      if [ "${error_value}\ -eq 0 ]; then
        log_success_msg2
      fi

      if [ "${error_value}\ -eq 1 ]; then
        msg="\n警告：发现并修复了 "
        msg="${msg}文件系统错误。\n"
        msg="${msg}你可能需要双检查 "
        msg="${msg}是否修复正确。"
        log_warning_msg "${msg}"
      fi

      if [ "${error_value}" -gt 3 -a "${error_value}" -lt 16 ]; then
        msg="${FAILURE:遇到了无法自动修复的 "
        msg="${msg}文件系统。此系统无法继续启动，"
        msg="${msg}将由系统管理员手动修复"
        msg="${msg}。\n\n"
        msg="${msg}在你按下回车后，此系统将"
        msg="${msg}停止并关机。\n\n"
        log_failure_msg "${msg}"

        log_info_msg "按回车键继续..."
        wait_for_user
        reboot -f
      fi

      if [ "${error_value}" -ge 16 ]; then
        msg="${FAILURE:\n运行 fsck 时发生意外故障。"
        msg="${msg}退出错误代码: ${error_value}"
        log_failure_msg $msg
        exit "${error_value}"
      fi
    fi
  fi
esac

exit 0
```

## 本地文件系统挂载脚本

```bash
### BEGIN INIT INFO

# Provides:              $local_fs
# Required-Start:       udev checks
# Should-Start:         swap
# Required-Stop:        
# Should-Stop:          S
# Default-Start:        
# Default-Stop:         0
# Short-Description:     挂载在 /etc/fstab 中定义的本地文件系统。
# Description:           在启动时重新挂载根文件系统为读写模式，并
                        挂载 /etc/fstab 中定义的所有文件。
                        停止时重新挂载根文件系统为只读并卸载
                        剩余的文件系统。

# X-LFS-Provided-By:    LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions

case "$1" in
start)
    log_info_msg "正在以读写模式挂载根文件系统..."
    mount -o remount,rw / >dev/null
    evaluate_retval

    # 移除 fsck 相关的文件系统标记。
    rm -f /fastboot /forcefsck

    # 确保 /dev/pts 存在
    mkdir -p /dev/pts

    # 这将挂载所有没有 _netdev 选项的文件系统
    # 它们的选项列表：_netdev 表示网络文件系统。

    log_info_msg "正在挂载剩余文件系统..."
    mount -a -o no_netdev /dev/null
    evaluate_retval
    exit $failed
    ;;

stop)
    # 不要卸载如 /run 等虚拟文件系统
    log_info_msg "正在卸载所有已挂载的文件系统..."
    umount -a -r -t notmpfs,nosysfs,nodevmpfs,nproc,nodevpts >dev/null
    evaluate_retval

    # 确保 / 为只读（除非 um 忙碌）
    mount -o remount,ro /

    # 在适当的情况下将所有 LVM 卷组设为不可用
    # 如果 swap 或 / 在 LVM 分区上，则会失败
    #if [ -x /sbin/vgchange ]; then /sbin/vgchange -an > /dev/null; fi
    ;;

*)
echo "用法: ${0} {start|stop}"
exit 1
;;
;;
esac
# End mountfs
```



```
#!/bin/sh
################################################################
# 开始 udev_retry
# 描述 : Udev 热插拔脚本（重试）
# Authors : Alexander E. Patrakov
# DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubce - bdbubms@linuxfromscratch.org
# Bryan Kadzban -
# Version : LFS 7.0
################################################################

### BEGIN INIT INFO
# Provides: udev_retry
# Required-Start: udev
# Should-Start: $local_fs
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 重试失败的 uevents 并创建额外的设备。
# Description: 重试由于硬件初始化较慢而跳过的失败 uevents，
# 并创建所需的
# 设备节点
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```
. /lib/lsb/init-functions
case "${1}" in
start)
  log_info_msg "正在重试失败的 uevents（如果有）..."

  # 从 udev-186 开始，--run 选项已不再有效
  # rundir=$1/sbin/udevadm info --run
  rundir=/run/udev
  # get Debian：“复制在 / 挂载为
  # 读写之前 生成的规则：”

  for file in ${${file##*tmp-rules--}}\; do
    dest=${${file##*tmp-rules--}}
    [ "$dest" = '*' ] && break
    cat $file >> /etc/udev/rules.$dest
  rm -f $file
done
# 重新触发可能失败的 uevents，
# 期望它们现在可以成功
#/bin/sed -e 's/.*$/' /etc/sysconfig/udev_retry | /bin/grep -v '^$' | \
while read line; do
  for subsystem in $line; do
    /sbin/udevadm trigger --subsystem=$subsystem --action=add
  done
done

# 等待 udev 处理我们触发的 uevents
if ! is_true "$OMIT_UDEV_RETRY_SETTLE"; then
  /sbin/udevadm settlen

evaluate_retval

;;

*)
echo "用法 ${0} {start}"
  exit 1
;;

esac

exit 0

# End udev_retry
```

# D.11./etc/rc.d/init.d/cleanfs

```
#!/bin/sh
################################################################
# 开始 cleanfs
# 描述 : 清理文件系统
# Authors : Gerard Beekmans - gerard@linuxfromscratch.com
# DJ Lucas - dj@linuxfromscratch.com
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.com
# Version : LFS 7.0

################################################################################**
```

```
### BEGIN INIT INFO
# Provides: cleanfs
# Required-Start: $local_fs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:
# Default-Stop: S
# Short-Description: 在启动过程中早期清理临时目录。
# Description: 清理 /var/run, /lock 以及可选的 /tmp。
# cleanfs 也会创建 /run/utmp 和 /etc/sysconfig/createfiles 中定义的任何文件。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

`. /lib/lsb/init-functions`

# 启动时创建文件/目录的函数

`create_files()`

`{`

    # 输入到文件描述符 9，输出到 stdin（重定向）
    exec 9>/etc/sysconfig/createfiles

while read name type grp min
    # 忽略注释和空行
    case "$name" in
        |"*) continue ;;
    esac

    # 忽略已存在的文件
    if [ ! -e "$name" ]; then
        # 根据类型创建
        case "$type" in
            dir)
                mkdir "$name"
                ;;
            file)
                :>"$name"
                ;;
            dev)
                case "$type" in
                    char)
                        mkn "$name" c ${maj}${min}
                        ;;
                    block)
                        mkn "$name" b ${maj}${min}
                        ;;
                    pipe)
                        mkn "$name" p
                        ;;
                    *)
                        log_warning_msg "未知设备类型: $type"
                esac
        fi
    esac
)

    log_warning_msg "未知设备类型: $type"
    continue
done

# 设置权限
chown "${grp}" "$name"
chmod "$perm" "$name"

# 关闭文件描述符 9（重定向）
exec 0>&-
return 0

case "$1" in
start)
  log_info_msg "正在清理文件系统:"
  if [ "${INFO_CLEAN}" = "" ]; then
    log_info_msg "/tmp"
    cd /tmp && find -name found -delete || failed=1
  fi
  ) > /var/run/utmp
  if grep -q '^utmp' /etc/group ; then
    chmod 664 /var/run/utmp
    chgrp utmp /var/run/utmp
  fi
  (exit $failed))
  evaluate_retval
  if grep -q '^1' /etc/sysconfig/createfiles 2>/dev/null; then
    log_info_msg "正在创建文件和目录..."
    create_files # 始终返回 0
    evaluate_retval
  fi
  exit $failed
;;
*)
  echo "用法: $(0) (start)"
  exit 1
;;
esac

# End cleanfs
```

# D.12./etc.init.d/console

```
#!/bin/sh
```



################################################################

# 开始 console

# 描述 : 设置键映射和屏幕字体

#

# Authors : Gerard Beekmans - gerard@linuxfromscratch.org

# Alexander E. Patrakov

# DJ Lucas - dj@linuxfromscratch.org

# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org

#

# Version : LFS 7.0

################################################################

### Linux From Scratch - Version 8.0

```
### BEGIN INIT INFO
# Provides: console
# Required-Start: 
# Required-Start: $local_fs
# Should-Start: 
# Required-Stop: 
# Should-Stop: 
# Default-Start: S
# Default-Stop: 
# Short-Description: 为用户设置本地化控制台。
# Description: 根据 /etc/sysconfig/console 设置字体和语言。
# X-LFS-Provided-By: LFS
### END INIT INFO

. /lib/lsb/init-functions

# 英语母语者完全没有 /etc/sysconfig/console
[ -r /etc/sysconfig/console ] && . /etc/sysconfig/console
nis_true() {
  case "$1" in
    "1" | "yes" | [ "$1" = "true" ]
  esac
}

failed=0
case "$1" in
start)
  # 查看是否需要 ${KEYMAP} 执行什么
  if [ -z "${KEYMAP}" ] && -z "${KEYMAP_CORRECTIONS}" ] &&
      [ -z "${FONT}" ] && -z "${LEGACY_CHARSET}" ] &&
      ! is_true "${UNICODE}"; then
    exit 0
  fi

  # 此行之后不应有错误的失败！
  log_info_msg "正在设置 Linux 控制台..."
  # 确定是否使用了帧控制台
  [ -d /sys/class/graphics/fb0 ] && use_fb=1 || use_fb=0

  # 确定设置控制台的命令
  is_true "${UNICODE}"; then
    MODE_COMMAND="echo -e '\033%G' && kb_mode -u"
    MODE_COMMAND="echo -e '\033%033 (K' && kb_mode -a"

   在帧控制台上，UTF-8 模式下必须为每个 vt 设置字体。这在非 UTF-8 模式下没有影响。

  is_true "${use_fb}" && [ -z "${FONT}" ] &&
    MODE_COMMAND="${MODE_COMMAND}" && setfont "${FONT}"

  # 将命令应用到 /etc/inittab 中提到的所有控制台。重要：在 UTF-8 模式下，
  # 这应该在 setfont 之前发生，否则会出现内核错误，
  # 字体的 unicode 映射将无法显示。
```

303

```bash
# 设置字体（如果上方未设置）和键映射
"$${use_fb}" == "1" || [ -z "${FONT}" ] || setfont $FONT || failed=1

[ -z "${KEYMAP}" ] || \
  loadkeys ${KEYMAP} >dev/null 2>&1 || \
  failed=1

[ -z "${KEYMAP_CORRECTIONS}" ] || \
  loadkeys ${KEYMAP_CORRECTIONS} >dev/null 2>&1 || \
  failed=1
```

```bash
# 将键映射从 ${LEGACY_CHARSET} 转换为 UTF-8
[ -z "${LEGACY_CHARSET}" ] || \
  dumpkeys "${LEGACY_CHARSET}" | loadkeys -u >dev/null 2>&1 || \
  failed=1
```

```bash
# 如果上述任何命令执行失败，顶部的 trap 将
# 将 $failed 设置为 1
exit $failed
evaluate_retval

exit $failed
;;
*)
echo "Usage: ${0} (start)"
exit 1
;;
esac
```

## D.13. /etc/rc.d/init.d/localnet

```bash
#!/bin/sh
################################################################
# 开始 localnet
# 描述 : 回环设备
# 作者 : Gerard Beekmans - gerard@linuxfromscratch.com
#        DJ Lucas - dj@linuxfromscratch.com
# 更新 : Bruce Dubbs - bdubbs@linuxfromscratch.com
# 版本 : LFS 7.0
################################################################
```

```bash
### BEGIN INIT INFO
# Provides:          localnet
# Required-Start:    $local_fs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start:\    S
# Default-stop:      0
# Short-Description:  启动本地网络。
# Description:        设置机器主机名并启动回环接口。
# X-LFS-Provided-By:  LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions && .
[ -r /etc/sysconfig/network ] && . /etc/sysconfig/network
[ -r /etc/hostname ] && HOSTNAME=`cat /etc/hostname`
case "$1" in
start)
    log_info_msg "正在启动回环接口..."
    ip addr add 127.0.0.1/8 label dev lo
    ip link set lo
    evaluate_retval

    log_info_msg "正在设置主机名为 ${HOSTNAME}..."
    hostname=${HOSTNAME}
    evaluate_retval
    ;;

stop)
    log_info_msg "正在关闭回环接口..."
    ip link set lo down
    evaluate_retval
    ;;

restart)
    $($0) stop
    sleep 1
    $($0) start
    ;;

status)
    echo "Hostname is: ${hostname}"
    ip link show lo
    ;;

)
    echo "Usage: $($0) {stop|restart|status}"
    exit 1
    ;;
esac

exit 0
```

## D.14. /etc/rc.d/init.d/sysctl



```bash
#!/bin/sh
######################################################################
# 开始 sysctl
# 描述 : 使用 /etc/sysctl.conf 设置内核运行时
#               参数
# 作者 : Nathan Coulson (nathan@linuxfromscratch.org)
          Matthew Burgess (matthew@linuxfromscratch.org)
          DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本 : LFS 7.0
######################################################################
```

```bash
### BEGIN INIT INFO
# sysctl
# Provides:
# Required-Start: mountvirtfs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: 对 proc 文件系统进行更改
# Description: 按照 /etc/sysctl.conf 定义对 proc 文件系统进行更改。
#               参阅 'man sysctl(8)'。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
./lib/lsb/init-functions

case "$1" in
start)
  if [ -f "/etc/sysctl.conf" ]; then
    log_info_msg "正在设置内核运行时参数..."
    sysctl -q p
    evaluate_retval
  fi
  ;;

status)
  sysctl -a
  ;;

)
  echo "Usage: $0 {start|status}"
  exit 1
  ;;
esac

exit 0
```

Linux From Scratch - Version 8.0

```bash
#  sysctl
```

## D.15. /etc/rc.d/init.d/syslogd

```bash
#!/bin/sh

# 描述 : Syslogd 加载器
# 作者 : Gerard Beekmans - gerard@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本 : LFS 7.0

### BEGIN INIT INFO

# Provides: $syslog
# Required-Start: localnet
# Should-Start: 
# Required-Stop: $local_fs
# Should-Stop:
# Default-Start: 3
# Default-Stop: 0
# Short-Description: 启动内核和系统守护进程。
# Description: 启动 /etc/fstab 中定义的内核和系统守护进程。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
# 注意：由于远程日志配置，syslogd 不运行级别 2 下启动。

/sbin/logd
evaluate_retval
;;

reload)
log_info_msg "正在重新加载日志守护进程..."
pid=`cat /var/run/logd.pid`
kill -H "$pid"
evaluate_retval
;;

restart)
$($0) stop
sleep 1
$($0) start
;;

status)
status /sbin/logd
;;

*)
echo "Usage: $0 {start|restart|status}"
exit 1
esac

exit 0
```

## D.16. /etc/rc.d/init.d/network

```bash

#!/bin/sh

################################################################

# 开始 network

# 描述 : 网络控制脚本

# 作者: Gerard Beekmans - gerard@linuxfromscratch.org

#          Nathan Coulson - nathan@linuxfromscratch.org

#          Kevin Fleming - fleming@linuxfromscratch.org

#          DJ Lucas - dj@linuxfromscratch.org

# 更新 : Bruce Dubbs - bdubbs@linuxfromscratch.org

# 版本 : LFS 7.0

################################################################

```

```bash

### BEGIN INIT INFO

# Provides: $network

# Required-Start: $local_fs

# Should-Start: $syslog

# Required-Stop: $local_fs

# Should-Stop: $syslog

# Default-Start: 3

# Default-Stop: 0

# Short-Description: 启动并配置网络接口。

# Description: 启动并配置网络接口。

# X-LFS-Provided-By: LFS

### END INIT INFO

```

```bash

case "$1" in

start)

  # 启动所有网络接口

  for file in /etc/sysconfig/ifconfig*;

  do

    interface=${file*/}

    # 如果没有找到接口，则跳过

    if [ "${interface}" = "*" ]; then

      continue

    fi

    /sbin/ifup ${interface}

  done

  ;;

stop)

  # 反转列表

  net_files=""

  for file in /etc/sysconfig/ifconfig*;

  do

    net_files="${file} ${net_files}"

  done

  # 停止所有网络接口

  for file in $net_files;

  do

    interface=${file*/}

    # 如果没有找到接口，则跳过

    if [ "${interface}" = "*" ]; then

      continue

    fi

    /sbin/ifdown ${interface}

  done

  ;;

restart)

  $($0) stop

  sleep 1

  $($0) start

  ;;

*)

  echo "Usage: $0 {start|stop|restart}"

  exit 1

  ;;

esac

exit 0

# 结束 network
```

## D.17. /etc/rc.d/init.d/sendsignal

```bash
#!/bin/sh
######################################################
# 开始 sendsignal
# 描述 : sendsignal 脚本
# 作者 : Gerard Beekmans - gerard@linuxfromscratch.org
          DJ Lucas - dj@linuxfromscratch.org
# 更新 : Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本 : LFS 7.0
######################################################
```



### BEGIN INIT INFO
# Provides: sendsignal
# Required-Start:
# Should-Start:
# Required-Stop: $local_fs localnet
# Should-Stop:
# Default-Start: 6
# Default-Stop:
# Short-Description: 尝试杀死剩余进程。
# Description: 尝试杀死剩余进程。
# X-LFS-Provided-By: LFS
### END INIT INFO

```bash
/lib/lsb/init-functions

case "$1" in
stop)
  log_info_msg "正在向所有进程发送 TERM 信号..."
  killall5 -15
  error_value=${?}

  sleep ${KIDLLEAY}

  if [ "${error_value}" = 0 || "${error_value}" = 2 ]; then
    log_success_msg
  else
    log_failure_msg
  fi

  log_info_msg "正在向所有进程发送 KILL 信号..."
  killall5 -9
  error_value=${?}

  sleep ${KIDLLEAY}
  if [ "${error_value}" = 0 -o "${error_value}" = 2 ]; then
    log_success_msg
  else
    log_failure_msg
  fi
  ;;

*)
  echo "Usage: $(0) {stop}"
  exit 1
;;
esac

exit 0

# 结束 sendsignal
```

## D.18. /etc/rc.d/init.d/reboot

```bash
#!/bin/sh

################################################

# 开始 reboot

# 描述 : 重启脚本

# 作者 : Gerard Beekmans - gerard@linuxfromscratch.org

#          DJ Lucas - djlj@linuxfromscratch.org

# 更新 : Bruce Dubbs - dbubbs@linuxfromscratch.org

# 版本 : LFS 7.0

################################################
```

### BEGIN INIT INFO
# Provides:              reboot
# Required-Start:       
# Should-Start:
# Required-Stop:       
# Should-Stop:
# Default-Start:        6
# Default-Stop:        
# Short-Description:    重启系统。
# Description:          重启系统。
# X-LFS-Provided-By:    LFS
### END INIT INFO

```bash
/lib/sb/init-functions

case "$1$" in

stop)

    log_info_msg "正在重启系统..."

    reboot -d -f -i

    ;;

```

```bash
*)
echo "Usage: ${0} stop"
exit 1
;;
esac
case "${1}" in
stop)
halt -d -f -i -p
;;
*)
echo "Usage: ${0} stop"
exit 1
;;
esac
# End reboot
# End reboot
```

## D.19. /etc/rc.d/init.d/halt

```sh
#!/bin/sh
################################################################################
# Begin halt
# Description : 停机脚本
# Authors : Gerard Beekemans - gerard@linuxfromscratch.org
#          DJ Lucas - djlucas@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
# Version : LFS 7.0
################################################################################
```

```
### BEGIN INIT INFO
# Provides: halt
# Required-Start:
# Should-Stop:
# Required-Stop:
# Should-Stop:
# Default-Start: 0
# Default-Stop:
# Short-Description: 停止系统。
# Description: 停止系统。
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```sh
case "${1}" in
stop)
  halt -d -f -i -p
;;
*)
  echo "Usage: ${0} stop"
  exit 1
;;
esac

# End halt
```

## D.20. /etc/rc.d/init.d/template

```sh
#!/bin/sh

################################################################################

# Begin scriptname

# Linux From Scratch - 版本 8.0

#

# Description :

#

# Authors :

#

# Version : LFS x.x

#

# Notes :

###############################################################################
```

### BEGIN INIT INFO
# Provides: template
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

```sh
. /lib/lsb/init-functions

case "$1" in

start)

  log_info_msg "Starting..."

  start_daemon fully_qualified_path

  ;;

stop)

  log_info_msg "Stopping..."

  killproc fully_qualified_path

  ;;

restart)

  $0 stop

  sleep 1

  $0 start

  ;;

*)

  echo "Usage: $0 {start|stop|restart}"

  exit 1

  ;;

esac

exit 0

# End scriptname
```

## D.21. /etc/sysconfig/modules

```sh
###############################################################################
# Begin /etc/sysconfig/modules
# Description : 模块自动加载配置
# Authors :
# Version : 00.00
# Notes : 该文件的语法如下：
#   <module> {arg1} <arg2> [...]

# 每个模块应该独占一行，任何你想要传递给模块的选项
# 都应该跟随其后。行分隔符可以是空格或制表符。
################################################################

# End /etc/sysconfig/modules
```

## D.22. /etc/sysconfig/createfiles



```sh
################################################################
# Begin /etc/sysconfig/createfiles
# Description : createfiles 脚本配置文件
# Authors :
# Version : 00.00
# Notes : 该文件的语法如下：
#   如果 type 等于 "file" 或 "dir"
#     <filename> <type> <permissions> <user> <group>
#   如果 type 等于 "dev"
#     <filename> <permissions> <user> <group <devtype>
#     <major><minor>

#   <filename> 是要创建的文件名
#   <type> 为 file、dir 或 dev 之一
#     file 创建新文件
#     dir 创建新目录
#     dev 创建新设备
#   <devtype> 为 block、char 或 pipe 之一
#     block 创建块设备
#     char 创建字符设备
#     pipe 创建管道，这将忽略 <major> 和
#     <minor> 字段
#   <major> 和 <minor> 是用于
#设备的主设备号和次设备号。
################################################################

# End /etc/sysconfig/createfiles
```

## D.23. /etc/sysconfig/udev-retry

# Begin /etc/sysconfig/udev_retry

```sh
# Description : udev_retry 脚本配置
# Authors : :
# Version : 00.00
# Notes : 在 mountfs 之后可能需要重新触发的子系统
# 都应该列在此文件中。可能需要列出的子系统有
# rtc（由于 /var/lib/hwclock/adjtime）和 sound
#（由于 /var/lib/alsa/asound.state 和 /usr/sbin/isactl）。
#
#################################################################
# 条目之间用空格分隔。
```

```sh
rtc

# End /etc/sysconfig/udev_retry
```

## D.24. /sbin/ifup

```sh
#!/bin/sh
#################################################################
# Begin /sbin/ifup
# Description : 接口启动
# Authors : Nathan Coulson nathan@linuxfromscratch.org
# Kevin P. Fleming - kpfleming@linuxfromscratch.org
# Update : Bruce Dubce - dbdudu@linuxfromscratch.org
# Version : LFS 7.7
# Notes : IFCONFIG 变量被传递给 /lib/services 目录
下的 SERVICE 脚本
################################################################

up()
{
  link_status=$(ip link $1 2>/dev/null)
  if [ -z "$link_status" ]; then
    echo "Interface $1 does not exist."
    return 1
  fi

  if echo "$link_status" | grep -q UP; then
    echo "Interface $1 is already up."
    return 0
  fi

  echo "Bringing up $1..."
  ip link set $1 up
}

down()
{
  if ip link $1 2>/dev/null | grep -q DOWN; then
    echo "Interface $1 is already down."
    return 0
  fi

  echo "Bringing down $1..."
  ip link set $1 down
}

case "$1" in
  up)
    up "$2"
    ;;
  down)
    down "$2"
    ;;
  *)
    echo "Usage: $0 {up|down} <interface>"
    exit 1
    ;;
esac
```

# Linux From Scratch - 版本 8.0

```bash
if [ -z "${IFACE}" ]; then
  log_failure_msg "${file} does not define an interface [IFACE]."
  exit 1
fi
```

```bash
# 我们只需要第一个服务来关闭接口
S=$(echo "${SERVICE}" | cut -f1 -d " ")

if link show ${IFACE} >/dev/null 2>&1; then
  if [ -n "${S}" -a x - /lib/services/${S} ]; then
    IFONFIG(${IFACE}) /lib/services/${S} down
  else
    MSG="无法处理 ${file}要么 "
    MSG="${S} SERVICE 变量未设置"
    MSG="${MSG}或指定的服务无法执行。"
    log_failure_msg "${MSG}"
    exit 1
  fi
else
  log_warning_msg "接口 ${IFACE} 不存在。"
```

```bash
# 如果设备中还有其他接口，则保持接口开启状态
link_status=$(ip link show ${IFACE} 2>/dev/null)

if [ -n "${link_status}" ]; then
  if [ $(echo "${link_status}" | grep UP) != "" ]; then
    if [ "$(ip addr show ${IFACE} | grep 'inet')" != "" ]; then
      log_info_msg "正在关闭 ${IFACE} 接口..."
      ip link set ${IFACE} down
    fi
  fi
  evaluate_retval
```

```bash
# 结束 /sbin/ifdown
```

## D.26. /lib/services/ipv4-static

```bash
#!/bin/sh
################################################################################
# 开始 /lib/services/ipv4-static
# 描述：IPv4 静态启动脚本
# 作者：Nathan Coulson - nathan@linuxfromscratch.org
# Kevin P. Fleming - kpfleming@linuxfromscratch.org
# 更新：Bruce Dubbs - bdbubbs@linuxfromscratch.org
# 版本：LFS 7.0
################################################################################

./lib/sh/init-functions
.${IFCONFIG}

```

```bash
if [ -z "${IP}" ]; then
  log_failure_msg "${IFCONFIG} 中缺少 IP，无法继续。"
  exit 1
fi
```

```bash
if [ -z "${PREFIX}" -a -z "${PEER}" ]; then
  log_warning_msg "${IFCONFIG} 中缺少 PREFIX，假设为 24。"
  PREFIX=24
  args=${args} ${IP}/${PREFIX}"
```

```bash
elif [ -n "${PREFIX}" -a -n "${PEER}" ]; then
  log_failure_msg "${IFCONFIG} 中同时指定的 PREFIX 和 PEER，无法继续。"
  exit 1
fi
```



```bash
elif [ -n "${PREFIX}" ]; then
  args=${args} ${IP}/${PREFIX}"
```

```bash
elif [ -n "${PEER}" ]; then
  args=${args} ${IP} peer ${PEER}"
```

```bash
if [ -n "${LABEL}" ]; then
  args=${args} label ${LABEL}"
fi
```

```bash
if [ -n "${BROADCAST}" ]; then
  args=${args} broadcast ${BROADCAST}"
fi
```

```bash
case "${2}" in
  up)
    if [ "$(ip addr show ${1} 2>/dev/null | grep "${IP}")" = "" ]; then
      # 装饰性输出
      if [ echo "${SERVICE}" | grep -q "" ]; then
        log_info_msg "" 终止之前的消息
      fi

      log_info_msg "正在向 ${1} 接口添加 IPv4 地址 ${IP}..."
      ip addr add ${args} dev ${1}
    else
      log_warning_msg "无法向 ${1} 添加 IPv4 地址 ${IP}。已存在。"
    fi
    ;;

  down)
    if [ "$(ip addr show ${1} 2>/dev/null | grep "${IP}")" != "" ]; then
      log_info_msg "从 ${1} 接口移除 IPv4 地址 ${IP}..."
      ip addr del ${args} dev ${1}
    fi

    if [ -n "${GATEWAY}" ]; then
      # 只有在没有剩余 ipv4 地址时才删除网关
      if [ "$(ip addr show ${1} 2>/dev/null | grep 'inet ')" != "" ]; then
        log_info_msg "正在移除默认网关..."
        ip route del default
        evaluate_retval
      fi
    fi
    ;;
  *)
    echo "用法: $0 [interface] (up|down)"
    exit 1
    ;;
esac
# 结束 /lib/services/ipv4-static
```

## D.27. /lib/services/ipv4-static-route

```bash
#!/bin/sh
################################################################################
# 开始 /lib/services/ipv4-static-route
# 描述：IP4 静态路由脚本
#
# 作者
    Kevin P. Fleming - kpfleming@linuxfromscratch.org
    DJ Lucas - djlucas@linuxfromscratch.org
# 更新
    Bruce Dubbs - bdubbs@linuxfromscratch.org
# 版本
    : LFS 7.0
################################################################################
. /lib/sh/init-functions
. ${IFCONFIG}
case "$TYPE" in
  ""|"network")
    need_ip=1
    need_gateway=1
    ;;

  ("default")
    need_gateway=1
    args="${args} default
    desc="default"
    ;;

  ("host")
    need_ip=1
    ;;

  ("unreachable")
    need_ip=1
    args="${args} unreachable
    desc="unreachable"
    ;;

  *)
    log_failure_msg "${IFCONFIG} 中存在未知路由类型 (${TYPE}),无法继续。"
    exit 1
    ;;
esac
if [ -n "${GATEWAY}" ]; then
  MSG="静态路由无法在 ${IFCONFIG} 中设置 GATEWAY。"
  log_failure_msg "${MSG}无法继续"
  exit 1
fi

if [ -n "${need_ip}" ]; then
  if [ -z "${IP}" ]; then
    log_failure_msg "${IFCONFIG} 中缺少 IP，无法继续。"
    exit 1
  fi
  if [ -z "${PREFIX}" ]; then
    log_failure_msg "${IFCONFIG} 中缺少 PREFIX，无法继续。"
    exit 1
  fi
  args="${args} ${IP}/${PREFIX}"
  desc="${desc} ${IP}/${PREFIX}"
fi

if [ -n "${need_gateway}" ]; then
  if [ -z "${GATEWAY}" ]; then
    log_failure_msg "${IFCONFIG} 中缺少 GATEWAY 变量，无法继续。"
    exit 1
  fi
  args="${args} via ${GATEWAY}"
fi

if [ -n "${SOURCE}" ]; then
  args="${args} src ${SOURCE}"
fi

case "${2}" in
  up)
    log_info_msg "正在向 ${1} 接口添加 ${desc} 路由..."
    ip route add ${args} dev ${1}
    evaluate_retval
    ;;

  down)
    log_info_msg "正在从 ${1} 接口移除 ${desc} 路由..."
    ip route del ${args} dev ${1}
    evaluate_retval
    ;;
  *)
    echo "用法: $0 [interface] {up|down}"
    exit 1
    ;;
esac
# 结束 /lib/services/ipv4-static-route
```

## 附录 E. Udev 配置

本附录中的规则是为了方便而列出的。安装通常通过第 6.2.1 节完成。

### E.1. 55-lfs.rules

```bash
# /etc/udev/rules.d/55-lfs.rules: LFS 的规则定义

# 内核设备

# 当 /dev/rtc 可用时立即设置系统时钟
SUBSYSTEM="rtc", ACTION="add", MODE="0644", RUN="/etc/rc.init.d/setclock"
KERNEL="rtc", ACTION="add", MODE="0644", RUN="/etc/rc.init.d/setclock"

# 通信设备

KERNEL="ppp[0-9]*", GROUP="dialout"
KERNEL="isdn[0-9]*", GROUP="dialout"
KERNEL="isdnctrl[0-9]*", GROUP="dialout"
KERNEL="dbri[0-9]*", GROUP="dialout"
```

## 附录 F. LFS 许可

本书根据知识共享署名-非相同相同 2.0 许可。

计算机指令可以根据 MIT 许可从书中提取。

### F.1. 知识共享法律代码

知识共享署名-非相同相同 2.0

> **重要** 知识共享组织不是法律实体，且不提供法律服务。分发本许可并不建立律师与客户的关系。知识共享按“原样”提供此类信息。知识共享不对所提供的信息承担任何保证，并对其使用造成的损害免责。

许可

作品根据知识共享通用许可（“CCPL”或“许可”）的条款提供。该作品受版权和/或其他适用法律的保护。禁止在本许可或版权法授权之外对作品进行任何使用。

通过行使此处提供的对作品的任何权利，您接受并同意受本许可条款的约束。考虑到您接受这些条款和条件，许可方授予您此处包含的权利。

1. 定义

a“集体作品”是指一种作品，如期刊、选集或百科全书，其中作品以完整且未修改的形式出现，并将若干其他本身构成独立作品的贡献汇编成一个整体。构成集体作品的作品在本许可目的下不被视为衍生作品（下文定义）。



b“衍生作品”是指基于作品或作品及其他现有作品的作品，例如翻译、音乐改编、戏剧化、虚构化、电影版本、录音或复制、删节、压缩或作品可能进行重排、转换或改编的任何形式，但构成集体作品的作品在本许可目的下不被视为衍生作品。为了避免疑问，当作品为音乐作品或录音时，作品与动态图像在时间关系上的同步（“同步”）在本许可目的下将被视为衍生作品。

c“许可方”是指根据本许可条款提供作品的个人或实体。

d“原作者”是指创建作品的个人或实体。

e“作品”是指根据本许可条款提供的受版权保护的作者作品。

f“您”是指根据本许可行使权利且此前未针对该作品违反过本许可条款的个人或实体，或尽管之前的之前的版本但已获得许可方明确许可根据本许可行使权利的个人或实体。

g. “许可元素”是指许可方提供的以下高级许可属性，并在本许可的标题中注明：署名（Attribution）、非商业（Noncommercial）、相同方式（ShareAlike）。

## 2. 公平使用权
本许可中的任何内容均不减少、限制或约束由于公平使用、首次销售或其他根据版权法或其他适用法律对版权所有者专有权利所作的限制而产生的任何权利。

## 3. 许可授予
在遵守本许可条款和条件下，许可方授予您一个全球范围内的、免版税的、非独的、永久的（在适用版权有效期内）许可，以行使下述对作品的权利：

- a. 复制作品，将作品纳入一个或多个集体作品中，并复制已并入集体作品中的作品；
- b. 创作并复制衍生作品；
- c. 分布作品的副本或录音制品，公开展示、公开表演以及通过数字音频传输公开表演作品（包括包含在集体作品中的作品）；
- d. 分布衍生作品的副本或录音制品，公开展示、公开表演以及通过数字音频传输公开表演衍生作品；

上述权利可以在现在或以后开发的任何媒体和格式中行使。上述权利包括为了在其他媒体和格式中行使权利而技术上必要的修改权利。许可方未明确授予的所有权利均保留，包括但不限于第 4(e) 节和 4(f) 节规定的权利。

## 4. 限制
第 3 节授予的许可明确受以下限制的约束：

- a. 您仅可以在在本许可的条款下分发、公开展示、公开表演或数字表演作品，并且在分发、公开展示、公开表演或数字表演作品的每份副本或录音制品中，必须包含本许可的副本或其统一资源标识符（URI）。您不能对作品提供或施加任何更改或限制本许可条款或受收者行使本许可下授予权利的条款。您不能对作品进行分许可。您必须完整保留所有引用本许可及免责声明的通知。您不能使用任何与本许可协议条款不一致的技术措施来控制对作品的访问或使用进行分发、公开展示、公开表演或数字表演。上述适用于并入集体作品的作品，但并不要求作品之外的集体作品本身也受本许可的约束。如果您创建了集体作品，在收到任何许可方的通知后，在可行范围内根据要求从集体作品中删除对该许可方或原作者的任何引用。如果您创建了衍生作品，在收到任何许可方的通知后，在可行范围内从衍生作品中删除对该许可方或您的任何引用。

- b. 您仅可以在在本许可的条款、与本许可具有相同许可元素的本许可的后续版本许可，或知识共享许可协议（CC-NonCommercial-ShareAlike 2.0）的条款下分发、公开展示、公开表演或数字表演衍生作品。在您分发、公开展示、公开表演或数字表演的每份衍生作品的副本或录音制品中，必须包含本许可或前述指定的其他许可的副本或其统一资源标识符。您不能对衍生作品提供或施加任何更改或限制本许可条款或收者行使本许可下授予权利的条款，并且您必须完整保留所有引用本许可及免责声明的通知。您不能使用任何与本许可协议条款不一致的技术措施来控制对作品的访问或使用进行分发、公开展示、公开表演或数字表演。上述适用于并入集体作品的作品，但并不要求衍生作品之外的集体作品本身也受本许可的约束。

- c. 您不能以任何主要用于商业利益或私人报酬的方式行使上述第 3 节授予给您的任何权利。通过文件共享或其他方式以作品交换其他版权作品不应被视为用于商业利益或私人报酬的。

- d. 如果您分发、公开展示、公开出版或公开表演衍生作品或作品，您必须完整保留作品的所有版权声明，并根据使用的媒介或手段注明原作者署名（或笔名），如指定的；使用的作品标题；在可行范围内注明许可方指定的与作品相关的统一资源标识符（如有），除非该 URI 指向作品的版权声明或许可信息；在衍生作品的情况下，注明在衍生作品中使用作品（例如：“原作者的法语译本”或“原作者编剧”）。此类说明可以以任何合理方式实施；但前提是在衍生作品或集体作品中，此类说明至少应出现在其他署名处，且显著程度至少与其他类似的署名相当。

- e. 免经确认，若作品为音乐作品：
    - i. 毯式许可下的表演权。许可方保留单独或通过表演权组织（例如 ASCAP、BMI、SESAC）收取作品的公开表演或公开数字表演（例如网络广播）版税的专有权利，前提是该表演主要用于商业利益或私人报酬。
    - ii. 机械复制和法定版税。许可方保留单独或通过音乐代理机构或指定代理（例如 Harry Fox Agency）收取作品的任何录音制品（“翻唱版本”）版税并分发的专有权利，但须遵守美国版权法第 115 节（或其他适用法律的等效规定）创建的强制许可，前提是您分发此类翻唱版本主要用于商业利益或私人报酬。

- f. 网络广播权和法定版税。免经确认，若作品为录音制品，许可方保留单独或通过表演权组织（例如 SoundExchange）收取作品的公开数字表演（例如网络广播）版税的专有权利，但须遵守美国版权法第 114 节（或其他适用法律的等效规定）创建的强制许可，前提是您的公开数字表演主要用于商业利益或私人报酬。

## 5. 陈述、保证与免责声明
除非双方另有书面约定，否则许可方按“原样”提供作品，且不对作品不任何任何形式的陈述或保证，无论是明式的、隐含的、法定的或其他，包括但不限于对标题、可销性、特定用途的适用性、不侵权，或对不存在潜在或其他缺陷、准确性或是否存在或不存在错误的保证，无论这些错误是否可被发现。某些管辖区不允许排除隐含的保证，因此此类排除可能不适用于您。

## 6. 责任限制
在适用法律要求的范围内，在任何情况下，许可方均不对基于任何法律理论的因使用本作品而产生的任何特殊、间接、后果性、惩罚性或示例性损害向您承担责任，即使许可方已被告知发生此类损害的可能性。

## 7. 终止
a. 如果您违反本许可的条款，本许可及在此授予的权利将自动终止。根据本许可从您处获得衍生作品或集体作品的个人或实体，只要此类作品完全符合所有章节，其许可就不会终止。第 1、2、5、6、7 和 8 条在任何终止后继续有效。

b. 在上述条款和条件的基础上，所授予的许可是永久的（在作品适用版权的有效期内）。尽管如此，许可方保留在随时以不同的许可条款发布作品或停止分发作品的权利；但只要，任何此类选择均不会撤销本许可（或根据本许可条款已授予或被要求授予的任何许可），且本许可将继续完全有效，除非如上述所示终止。

## 8. 杂项
a. 每当您分发或公开表演本作品或集体作品时，许可方均向接收者提供一份与根据本许可授予您的许可具有相同条款和条件的作品许可。

b. 每当您分发或公开表演一份衍生作品时，许可方均向接收者提供一份与根据本许可授予您的许可具有相同条款和条件的原始作品许可。

c. 如果本许可的任何规定在适用法律下无效或不可执行，则该规定不影响本许可其余条款的有效性或可执行性，且在本协议双方不采取进一步行动的情况下，该规定应修订至必要的最小限度以使该规定有效且可执行。

d. 本许可的任何条款或规定均不应视为放弃，除非此类放弃或同意以书面形式做出并由承担此类放弃或同意的一方签署。

e. 本许可构成了双方就此处许可的作品之间达成的完整协议。对于未在此处说明的作品，双方没有其他理解、协议或陈述。许可方不受您提供的通信中可能出现的任何附加条款的约束。经许可方和您双方共同书面同意，不得对本许可进行修改。

# 重要提示
知识共享组织（Creative Commons）并非本许可的方，且对作品不提供任何形式的保证。知识共享组织在任何法律理论下均不对您或任何方对任何损害负责，包括但不限于与本许可相关的任何一般、特殊、间接或后果性损害。尽管有上述两（2）句的规定，如果知识共享组织明确标识自己为许可方，则其应拥有许可方的所有权利和义务。

出于向公众说明作品根据 CCPL 许可的有限目的外，未经知识共享组织的事先书面许可，任何一方均不得使用“Creative Commons”商标或其任何相关商标或标志。任何许可的使用都应符合知识共享组织当时有效的使用指南，该指南可能会发布在我们的网站上，或根据要求随时提供。

可以通过 `http://creativecommons.org` 联系知识共享组织。

# F.2. MIT 许可证
版权所有 © 1999-2017 Gerard Beekmans

特此允许任何获得本软件及相关文档文件（下称“软件”）副本的人员不受限制地对软件进行处理，包括但不限于使用、复制、修改、合并、发布、分发、分许可和/或销售软件副本的权利，并允许向提供软件的人员也这样做，但须符合以下条件：

上述版权声明和本许可声明应包含在软件的所有副本或主要部分中。



软件按“原样”提供，不提供任何形式的保证，无论是明式的还是隐含的，包括但不限于对可销性、特定用途的适用性和不侵权的保证。在任何情况下，作者或版权持有者均对因合同、侵权或其他诉讼引起的、源于软件或与软件的使用或其他处理有关的任何索赔、损害或其他责任不负责。

# 索引

## 软件包

| 软件包 | 页码 |
| :--- | :--- |
| Acl | 125 |
| Attr | 123 |
| Autoconf | 156 |
| Automake | 158 |
| Bash | 142 |
| tools | 60 |
| Bc | 144 |
| Binutils | 105 |
| tools, pass 1 | 37 |
| tools, pass 2 | 48 |
| Bison | 137 |
| tools | 61 |
| Bootscripts | 216 |
| usage | 226 |
| Bzip2 | 117 |
| tools | 62 |
| Check | 58 |
| Coreutils | 170 |
| tools | 63 |
| DejaVu | 57 |
| Diffutils | 175 |
| tools | 64 |
| E2progs | 167 |
| Udev | 197 |
| configuring | 198 |
| Expat | 148 |
| Expect | 55 |
| File | 104 |
| tools | 65 |
| Findutils | 177 |
| tools | 66 |
| Flex | 138 |
| Gawk | 176 |
| tools | 67 |
| GCC | 112 |
| tools, libstdc++ | 46 |
| tools, pass 1 | 39 |
| tools, pass 2 | 50 |
| GDBM | 146 |
| Gettext | 163 |
| tools | 68 |
| Glibc | 94 |
| tools | 43 |
| GMP | 108 |
| Gperf | 147 |
| Grep | 139 |
| tools | 69 |
| Groff | 179 |
| GRUB | 182 |
| Gzip | 185 |
| tools | 70 |
| Iana-etc | 135 |
| Inutools | 149 |
| Intool | 155 |
| IProute2 | 187 |
| Kbd | 161 |
| Kmod | 184 |
| Libcap | 127 |
| Libpipeline | 191 |
| Libtool | 145 |
| Linux | 243 |
| API headers | 92 |
| M4 | 136 |
| Make | 192 |
| Man-DB | 204 |
| Man-pages | 93 |
| MPC | 111 |
| MPFR | 110 |
| Nurses | 120 |
| Patch | 193 |
| Perl | 151 |
| Pkgconfig | 119 |
| Procs-ng | 165 |
| Psmisc | 134 |
| rc.site | 233 |
| Readme | 140 |
| Tcl-core | 53 |
| Texinfo | 208 |
| Udev usage | 218 |
| Vim | 210 |
| XML::Parser | 154 |
| Zlib | 103 |

## 程序

| 程序 | 页码 |
| :--- | :--- |
| accessdb | 204, 206 |
| aclocal | 158, 158 |
| aclocal-1.15 | 158, 228 |
| addftinfo | 179, 179 |
| addpart | 199 |
| addr2 | 105, 106 |
| asid | 179, 179 |
| aspos | 199, 200 |
| attr | 123, 123 |
| autoconf | 156, 156 |
| automake | 158, 158 |
| automate-1.15 | 158, 228 |
| autoheader | 156, 156 |
| autinfo | 156, 156 |
| autopipe | 156, 156 |
| author | 156, 156 |
| autdate | 156, 156 |
| autf | 156, 156 |
| bash | 142, 142 |
| bc | 144, 144 |
| binutils | 105, 105 |
| bison | 137, 137 |
| bootscripts | 216, 216 |
| bzip2 | 117, 117 |
| cal | 199, 200 |
| check | 58, 58 |
| coreutils | 170, 170 |
| dejavu | 57, 57 |
| diffutils | 175, 175 |
| e2progs | 167, 167 |
| udev | 197, 197 |
| expat | 148, 148 |
| expect | 55, 55 |
| file | 104, 104 |
| findutils | 177, 177 |
| flex | 138, 138 |
| gawk | 176, 176 |
| gcc | 112, 112 |
| gdbm | 146, 146 |
| gettext | 163, 163 |
| glibc | 94, 94 |
| gmp | 108, 108 |
| gperf | 147, 147 |
| grep | 139, 139 |
| groff | 179, 179 |
| grub | 182, 182 |
| gzip | 185, 185 |
| iana-etc | 135, 135 |
| inutools | 149, 149 |
| intool | 155, 155 |
| iproute2 | 187, 187 |
| kbd | 161, 161 |
| kmod | 184, 184 |
| libcap | 127, 127 |
| libpipeline | 191, 191 |
| libtool | 145, 145 |
| linux | 243, 243 |
| m4 | 136, 136 |
| make | 192, 192 |
| man-db | 204, 204 |
| man-pages | 93, 93 |
| mpc | 111, 111 |
| mpfr | 110, 110 |
| nurses | 120, 120 |
| patch | 193, 193 |
| perl | 151, 151 |
| pkgconfig | 119, 119 |
| procs-ng | 165, 165 |
| psmisc | 134, 134 |
| rc.site | 233, 233 |
| readme | 140, 140 |
| tcl-core | 53, 53 |
| texinfo | 208, 208 |
| udev usage | 218, 218 |
| vim | 210, 210 |
| xml::parser | 154, 154 |
| xz | 159, 159 |
| zlib | 103, 103 |

## Linux 从 Linux - 版本 8.0

| 命令 | 页码范围 |
| :--- | :--- |
| dc | 144, 144 |
| dd | 170, 172 |
| deallocvct | 189, 190 |
| debugfs | 167, 168 |
| delpart | 199, 200 |
| depmod | 161, 161 |
| df | 170, 172 |
| diff | 175, 175 |
| diff3 | 175, 175 |
| dir | 170, 172 |
| diricolors | 170, 172 |
| dirname | 170, 172 |
| dmesg | 199, 200 |
| dnsdomainname | 149, 150 |
| du | 170, 172 |
| dumpe2fs | 167, 168 |
| dumpekeys | 189, 190 |
| d2freefrag | 167, 168 |
| d2fsk | 167, 168 |
| d2image | 167, 168 |



| `d2label` | 167, 169 |
| `d2undo` | 167, 169 |
| `d4defrag` | 167, 169 |
| `echo` | 170, 172 |
| `degrep` | 139, 139 |
| `deject` | 199, 200 |
| `elferit` | 105, 106 |
| `enc2xs` | 151, 152 |
| `encguss` | 151, 152 |
| `denv` | 170, 172 |
| `envsubst` | 163, 163 |
| `eqqn` | 179, 179 |
| `eqqn2graph` | 179, 179 |
| `ex` | 210, 212 |
| `expand` | 170, 172 |
| `expect` | 55, 56 |
| `expiry` | 129, 132 |
| `expr` | 170, 172 |
| `factor` | 170, 172 |
| `faillog` | 129, 132 |
| `fallocate` | 199, 201 |
| `file` | 170, 172 |
| `fdformat` | 199, 201 |
| `fdisk` | 199, 201 |
| `fgconsole` | 189, 190 |
| `fgrep` | 139, 139 |
| `file` | 104, 104 |
| `filefrag` | 167, 169 |
| `find` | 177, 177 |
| `findfs` | 199, 201 |
| `findmt` | 199, 201 |
| `flex` | 138, 138 |
| `flex++` | 138, 138 |
| `flock` | 199, 201 |
| `fmt` | 170, 172 |
| `fold` | 170, 172 |
| `free` | 165, 165 |
| `fsck` | 199, 201 |
| `fsckramfs` | 199, 201 |
| `fsckext2` | 167, 169 |
| `fsfext3` | 163, 169 |
| `fsfext4` | 169, 169 |
| `fsfextd4` | 127, 169 |
| `fsminix` | 199, 201 |
| `fsree` | 199, 201 |
| `stab-decode` | 196, 196 |
| `fstrim` | 199, 201 |
| `ftp` | 149, 150 |
| `fuser` | 134, 134 |
| `gff++` | 112, 115 |
| `gawk` | 176, 176 |
| `gaw-4.1.4` | 176, 176 |
| `gcc` | 112, 115 |
| `gc-ar` | 112, 115 |
| `gc-nm` | 112, 115 |
| `gc-ranlib` | 112, 115 |
| `cov` | 112, 116 |
| `dgbmttool` | 146, 146 |
| `dgbm_dump` | 146, 146 |
| `dgbm_load` | 146, 146 |
| `dgifmk` | 179, 179 |
| `gencat` | 94, 99 |
| `genl` | 187, 187 |
| `getcap` | 127, 127 |
| `getconf` | 94, 99 |
| `getent` | 94, 99 |
| `getfacl` | 125, 126 |
| `getattr` | 123, 123 |
| `getkeycodes` | 189, 190 |
| `getopt` | 199, 201 |
| `getcaps` | 127, 127 |
| `gettext` | 163, 163 |
| `gettext.sh` | 163, 163 |
| `getgetextize` | 163, 163 |
| `gll ypond` | 179, 179 |
| `gpassword` | 129, 132 |
| `gperf` | 147, 147 |
| `perl` | 179, 179 |
| `gpinyin` | 179, 179 |
| `gprof` | 105, 106 |
| `graph2` | 179, 180 |
| `grep` | 139, 139 |
| `grn` | 179, 180 |
| `grodvi` | 179, 180 |
| `groff` | 179, 180 |
| `groffer` | 179, 180 |
| `grog` | 179, 180 |
| `golbp` | 179, 180 |
| `grolj4` | 179, 180 |
| `gropdf` | 179, 180 |
| `grops` | 179, 180 |
| `grotty` | 179, 180 |
| `groupadd` | 129, 132 |
| `groupdel` | 129, 132 |
| `groupmems` | 129, 132 |
| `groupmod` | 179, 132 |
| `groups` | 170, 172 |
| `gprck` | 129, 132 |
| `gprconv` | 129, 132 |
| `gprunconv` | 129, 132 |
| `grub-setup` | 182, 182 |
| `grub-edit` | 182, 182 |
| `grub-file` | 182, 182 |
| `grub-fstest` | 182, 182 |
| `grub-glue-efi` | 182, 182 |
| `grub-install` | 182, 182 |
| `grub-kbdcomp` | 182, 182 |
| `grub-macless` | 182, 182 |
| `grub-menist` | 182, 182 |
| `grub-mkconfig` | 182, 182 |
| `grub-mkimage` | 182, 182 |
| `grub-mklayout` | 182, 182 |
| `grub-mknetdir` | 182, 182 |
| `grub-mkpasswd` | 182, 182 |
| `grub-mkrel` | 182, 182 |
| `grub-mkrescue` | 182, 182 |
| `grub-mkstandalone` | 182, 182 |
| `grub-ofpathname` | 182, 182 |
| `grub-probe` | 182, 182 |
| `grub-reboot` | 182, 182 |
| `grub-render-label` | 182, 182 |
| `grub-script-check` | 182, 182 |
| `grub-set-default` | 182, 182 |
| `grub-syslinux` | 182, 182 |
| `gzip` | 185, 185 |
| `gzexe` | 185, 185 |
| `gzip` | 185, 185 |
| `h2f` | 151, 152 |
| `h2xs` | 151, 152 |
| `halt` | 196, 196 |
| `head` | 170, 172 |
| `hexdump` | 199, 201 |
| `hostid` | 170, 172 |
| `hostname` | 149, 150 |
| `hpftid` | 179, 180 |
| `hwclock` | 199, 201 |
| `i386` | 199, 201 |
| `iconv` | 94, 99 |
| `iconvconfig` | 94, 99 |
| `ido` | 170, 172 |
| `ifcfg` | 187, 187 |
| `ifconfig` | 149, 150 |
| `ifnames` | 156, 156 |
| `ifstat` | 187, 187 |
| `igawk` | 176, 176 |
| `ndxbib` | 179, 180 |
| `info` | 208, 209 |
| `infomp` | 120, 122 |
| `infotac` | 120, 122 |
| `init` | 196, 196 |
| `insmod` | 161, 162 |
| `install` | 170, 172 |
| `install-info` | 208, 209 |
| `instmod` | 151, 152 |
| `intltool-extract` | 155, 155 |
| `intltool-merge` | 155, 155 |
| `intltool-prepare` | 155, 155 |
| `intltool-update` | 155, 155 |
| `intltoolize` | 155, 155 |
| `ionice` | 199, 201 |
| `ip` | 187, 187 |
| `ipcmk` | 199, 201 |
| `iprm` | 199, 201 |
| `ipcs` | 199, 201 |
| `nisosize` | 199, 201 |



| `join` | 170, 172 |
| `json_pp` | 151, 152 |
| `kbdinfo` | 189, 190 |
| `kbdrate` | 189, 190 |
| `bd_mode` | 189, 190 |
| `kill` | 199, 201 |
| `killall` | 134, 134 |
| `killall5` | 196, 196 |
| `klogd` | 194, 194 |
| `kmod` | 161, 162 |
| `last` | 199, 201 |
| `lastb` | 199, 201 |
| `lastlog` | 129, 132 |
| `ld` | 105, 106 |
| `ld.bfd` | 105, 106 |
| `ldatch` | 199, 201 |
| `config` | 94, 99 |
| `ld` | 94, 99 |
| `dlibc4` | 94, 99 |
| `less` | 184, 184 |
| `lessecho` | 184, 184 |
| `lesskey` | 184, 184 |
| `tex` | 138, 138 |
| `lexgrog` |  |
| `lfskernel-4.9.9` | 243, 246 |
| `libasan` | 112, 116 |
| `libnetcfg` | 151, 152 |
| `libtool` | 145, 145 |
| `libtool2` | 145, 145 |
| `link` | 170, 173 |
| `linux32` | 199, 201 |
| `linux64` | 199, 201 |
| `lkbib` | 179, 180 |
| `In` | 170, 173 |
| `Instat` | 187, 188 |
| `loadkeys` | 189, 190 |
| `loadunimap` | 189, 190 |
| `locale` | 94, 99 |
| `localedef` | 94, 99 |
| `locate` | 177, 177 |
| `logger` | 199, 201 |
| `login` | 129, 132 |
| `logname` | 170, 173 |
| `logout` | 129, 132 |
| `logsave` | 167, 169 |
| `look` | 199, 201 |
| `lookbib` | 179, 180 |
| `losetup` | 199, 201 |
| `is` | 170, 173 |
| `lsattr` | 167, 169 |
| `lsblk` | 199, 201 |
| `lsc` | 199, 201 |
| `locks` | 199, 201 |
| `lslogins` | 199, 201 |
| `lismod` | 161, 162 |
| `lzcat` | 159, 159 |
| `lzdiff` | 159, 159 |
| `lzfg` | 159, 159 |
| `lzgrep` | 159, 159 |
| `lzless` | 159, 159 |
| `lzma` | 159, 159 |
| `lzmadec` | 159, 159 |
| `lzmainfo` | 159, 159 |
| `lzmore` | 159, 159 |
| `m4` | 136, 136 |
| `make` | 192, 192 |
| `makedby` | 94, 99 |
| `makeinfo` | 208, 209 |
| `mand` | 204, 206 |
| `manpath` | 204, 206 |
| `mapscrn` | 189, 190 |
| `mookie` | 199, 202 |
| `mmesg` | 199, 200 |
| `mk2fs` | 167, 169 |
| `mkifto` | 170, 173 |
| `mkfs` | 199, 202 |
| `mkfs.bfs` | 199, 202 |
| `mkfs.crams` | 199, 202 |
| `mkfs.ext2` | 167, 169 |
| `mkfs.ext3` | 163, 169 |
| `mkfs.ext4` | 169, 169 |
| `mkfs.ext4dev` | 167, 169 |
| `mkfs.minix` | 199, 201 |
| `mknod` | 170, 173 |
| `mktemp` | 170, 173 |
| `mk_cmds` | 167, 169 |
| `mkswap` | 199, 202 |
| `mmroff` | 179, 180 |
| `modinfo` | 161, 162 |
| `modprobe` | 161, 162 |
| `more` | 199, 202 |
| `mount` | 199, 202 |
| `mountpoint` | 199, 202 |
| `msgattrib` | 163, 164 |
| `msgcat` | 163, 164 |
| `msgcnp` | 163, 164 |
| `msgcomm` | 163, 164 |
| `msgconv` | 163, 164 |
| `msgeec` | 163, 164 |
| `msgfilter` | 163, 164 |
| `msgft` | 163, 164 |
| `smsggnit` | 163, 164 |
| `smmergege` | 163, 164 |
| `msgfunmt` | 163, 164 |
| `msguniq` | 163, 164 |
| `mvo` | 170, 173 |
| `namei` | 199, 202 |
| `new6-config` | 120, 122 |
| `neqtp` | 179, 180 |
| `newgidmap` | 129, 132 |
| `newgrp` | 129, 132 |
| `newduidmap` | 129, 132 |
| `newusers` | 129, 132 |
| `gettest` | 163, 164 |
| `nice` | 170, 173 |
| `nl` | 105, 106 |
| `nohup` | 170, 173 |
| `nologin` | 129, 132 |
| `nproc` | 170, 173 |
| `nnroff` | 179, 180 |
| `nscd` | 94, 99 |
| `senter` | 199, 202 |
| `numfmt` | 170, 173 |
| `objectij` | 105, 106 |
| `objectump` | 105, 106 |
| `ood` | 170, 173 |
| `oldfind` | 177, 178 |
| `openvent` | 189, 190 |
| `partx` | 199, 202 |
| `paste` | 170, 173 |
| `patch` | 193, 193 |
| `pathch` | 170, 173 |
| `pdfmom` | 179, 180 |
| `pdfroff` | 179, 180 |
| `pdftextdvi` | 208, 209 |
| `peekfd` | 134, 134 |
| `perl` | 151, 152 |
| `perl5.24.1` | 151, 152 |
| `perlbug` | 151, 152 |
| `perdoc` | 151, 152 |
| `perliv` | 151, 152 |
| `perthanks` | 151, 152 |
| `pfops` | 179, 180 |
| `pg` | 199, 202 |
| `pgrep` | 165, 166 |
| `pic` | 179, 180 |
| `picgraph` | 179, 180 |
| `pidof` | 165, 166 |
| `ping` | 149, 150 |
| `pink6` | 149, 150 |
| `pivot_root` | 199, 202 |
| `pkg-config` | 119, 119 |
| `pkill` | 165, 166 |
| `pmap` | 165, 166 |
| `pldd` | 94, 99 |
| `pl2m` | 151, 152 |
| `pod2html` | 151, 152 |
| `pod2man` | 151, 152 |
| `pod2text` | 208, 209 |
| `pod2usage` | 151, 153 |
| `post-grohtml` | 179, 180 |
| `pre-grohtml` | 179, 180 |
| `preconv` | 129, 132 |
| `poweroff` | 196, 196 |
| `pr` | 170, 173 |
| `referfer` | 180, 190 |
| `printv` | 170, 173 |
| `printenv` | 170, 173 |
| `printf` | 170, 173 |
| `prlimit` | 199, 202 |
| `prove` | 151, 153 |
| `prstat` | 134, 134 |



# Linux 从头 - 版本 8.0

| `ps` | 165, 166 |
| `psaddtable` | 189, 190 |
| `psgettable` | 189, 190 |
| `psistable` | 189, 190 |
| `pstree` | 134, 134 |
| `ptarg` | 151, 153 |
| `struct` | 151, 153 |
| `raw` | 199, 202 |
| `ranlib` | 112, 115 |
| `readelf` | 105, 107 |
| `readlink` | 170, 173 |
| `readprofile` | 199, 202 |
| `readpath` | 170, 173 |
| `reboot` | 196, 196 |
| `rename` | 199, 202 |
| `renice` | 199, 202 |
| `reset` | 129, 132 |
| `resize` | 199, 201 |
| `resizefs` | 167, 169 |
| `resizepart` | 199, 202 |
| `resize` | 199, 202 |
| `rm` | 170, 173 |
| `rmid` | 170, 173 |
| `rmmod` | 161, 162 |
| `rpc` | 94, 99 |
| `route` | 187, 187 |
| `rtcack` | 94, 99 |
| `rtcwake` | 199, 202 |
| `rtmon` | 187, 187 |
| `rtat` | 187, 187 |
| `runcon` | 170, 173 |
| `runlevel` | 196, 196 |
| `runtest` | 57, 57 |
| `runuser` | 210, 212 |
| `rvim` | 210, 212 |
| `runscript` | 199, 202 |
| `runreplay` | 199, 202 |
| `sdiff` | 175, 175 |
| `sed` | 128, 128 |
| `seq` | 170, 173 |
| `setac` | 125, 126 |
| `setarch` | 199, 202 |
| `setattr` | 123, 123 |
| `setcap` | 127, 127 |
| `setfont` | 189, 190 |
| `setkeycodes` | 189, 190 |
| `setleds` | 189, 190 |
| `setmetode` | 189, 190 |
| `ssetsid` | 199, 202 |
| `setterm` | 199, 202 |
| `setvgb` | 189, 190 |
| `sfdisk` | 199, 202 |
| `sg` | 129, 143 |
| `sh` | 142, 143 |
| `sha1` | 170, 173 |
| `sha224sum` | 170, 173 |
| `sha256sum` | 170, 173 |
| `sha384sum` | 170, 173 |
| `sha512sum` | 170, 173 |
| `shashum` | 151, 153 |
| `showconsole` | 189, 190 |
| `showkey` | 189, 190 |
| `shred` | 170, 174 |
| `shuf` | 170, 174 |
| `shutdown` | 196, 196 |
| `size` | 105, 107 |
| `slabtop` | 165, 166 |
| `sleep` | 170, 174 |
| `sln` | 94, 99 |
| `soelim` | 179, 181 |
| `sort` | 170, 174 |
| `sotruss` | 94, 99 |
| `splain` | 151, 153 |
| `split` | 170, 174 |
| `sprof` | 94, 99 |
| `ss` | 187, 188 |
| `stat` | 170, 174 |
| `stuf` | 170, 174 |
| `strings` | 105, 107 |
| `strip` | 105, 107 |
| `stty` | 170, 174 |
| `su` | 129, 133 |
| `sulogin` | 199, 202 |
| `sum` | 170, 174 |
| `swaplabel` | 199, 202 |
| `swappoff` | 199, 202 |
| `swapon` | 199, 202 |
| `switch_root` | 199, 202 |
| `sync` | 170, 174 |
| `syscl` | 165, 166 |
| `syslogd` | 194, 195 |
| `tabs` | 120, 122 |
| `tac` | 170, 174 |
| `tail` | 170, 174 |
| `tail` | 199, 202 |
| `talk` | 149, 150 |
| `tar` | 207, 207 |
| `taskset` | 199, 203 |
| `tbl` | 179, 181 |
| `tc` | 187, 188 |
| `tclsh` | 53, 54 |
| `tclsh8.6` | 53, 54 |
| `te` | 170, 174 |
| `telinit` | 196, 196 |
| `telnet` | 149, 150 |
| `test` | 170, 174 |
| `text2di` | 208, 209 |
| `text2pdf` | 208, 209 |
| `text2any` | 208, 209 |
| `textindex` | 208, 209 |
| `tfmodit` | 179, 181 |
| `tflip` | 149, 150 |
| `tic` | 120, 122 |
| `timeout` | 170, 174 |
| `tload` | 165, 166 |
| `toe` | 120, 122 |
| `top` | 165, 166 |
| `touch` | 170, 174 |
| `tputut` | 120, 122 |
| `tr` | 170, 174 |
| `traceroute` | 149, 150 |
| `troff` | 179, 181 |
| `true` | 170, 174 |
| `truncate` | 170, 174 |
| `tset` | 120, 122 |
| `tsort` | 170, 174 |
| `tty` | 170, 174 |
| `tune2fs` | 167, 169 |
| `tzselect` | 94, 99 |
| `udevam` | 197, 198 |
| `udev` | 197, 198 |
| `ul` | 199, 203 |
| `umount` | 199, 203 |
| `uname` | 170, 174 |
| `uname26` | 199, 203 |
| `uncompress` | 185, 185 |
| `unexpand` | 170, 174 |
| `unicode_start` | 189, 190 |
| `unicode_stop` | 189, 190 |
| `uniq` | 170, 174 |
| `unlink` | 170, 174 |
| `unlzma` | 159, 160 |
| `unshare` | 199, 203 |
| `unxz` | 159, 160 |
| `updatedb` | 177, 178 |
| `nuptime` | 165, 166 |
| `useradd` | 129, 133 |
| `userdel` | 129, 133 |
| `usermod` | 129, 133 |
| `users` | 170, 174 |
| `utmpdump` | 199, 203 |
| `nuuid` | 199, 203 |
| `uidigen` | 199, 203 |
| `vdir` | 170, 174 |
| `vio` | 210, 212 |
| `view` | 210, 212 |
| `vigr` | 129, 133 |
| `vvvim` | 210, 212 |
| `vimdiff` | 210, 212 |
| `vimutor` | 210, 212 |
| `vipw` | 129, 133 |
| `vstat` | 165, 166 |
| `w` | 165, 166 |
| `wall` | 199, 203 |
| `watch` | 165, 166 |
| `wc` | 170, 174 |
| `wdcl` | 199, 203 |
| `whatwhis` | 204, 206 |
| `whereis` | 199, 203 |
| `who` | 170, 174 |
| `whoami` | 170, 174 |
| `wpefs` | 199, 203 |
| `x86_64` | 199, 203 |
| `libcap` | 127, 127 |
| `xargs` | 177, 178 |
| `libcheck` | 58, 58 |
| `xgettext` | 163, 164 |
| `libcidr` | 94, 100 |
| `xmlwe` | 148, 148 |
| `libcom-err` | 167, 169 |
| `xubpp` | 151, 153 |
| `libcrypt` | 94, 100 |
| `xtrace` | 94, 100 |
| `libcursesw` | 120, 122 |
| `xxd` | 210, 212 |
| `libdl` | 94, 100 |
| `xz` | 159, 100 |
| `lib2p` | 167, 169 |
| `xzcat` | 159, 160 |
| `libater` | 148, 148 |



- `xzcmmp`: 159, 160
- `lib-5.45`: 55, 56
- `xzdecc`: 159, 160
- `libext2fs`: 167, 169
- `xdiff`: 159, 160
- `libdfsk`: 199, 203
- `xzegrep`: 159, 160
- `libbfl`: 138, 138
- `xzgrep`: 159, 160
- `libformw`: 120, 122
- `xzless`: 159, 160
- `libg`: 94, 100
- `zmore`: 159, 160
- `libgcc`: 112, 116
- `yacc`: 137, 174
- `libgcov`: 112, 116
- `yes`: 170, 174
- `libdbm`: 146, 146
- `zcat`: 185, 185
- `libdbm_compat`: 146, 164
- `zcmpmp`: 185, 185
- `libgettext`: 163, 164
- `zdiff`: 185, 185
- `libgetextpo`: 163, 164
- `zdump`: 94, 94
- `libgetextsr`: 163, 164
- `zgrep`: 185, 185
- `libbmp`: 108, 109
- `zfgrep`: 185, 185
- `libgmpx`: 108, 109
- `zforce`: 185, 185
- `libgomp`: 112, 116
- `zgrep`: 185, 185
- `libhistory`: 140, 140
- `z`: 94, 94
- `libliberty`: 112, 116
- `zipdetails`: 151, 153
- `libweee`: 94, 100
- `zless`: 185, 185
- `libkmod`: 161, 161
- `zmore`: 185, 186
- `libtdld`: 145, 145
- `znew`: 185, 186
- `liblto_plugin`: 112, 116
- `zramctl`: 199, 203
- `liblzma`: 159, 160

- `libm`: 94, 100
- `Expat`: 154, 154
- `libmagic`: 104, 104
- `ld-2.25.so`: 94, 100
- `libman`: 204, 206
- `libac`: 125, 126
- `libmandb`: 204, 206
- `libnl`: 94, 100
- `libmemusage`: 94, 100
- `libbprint`: 163, 164
- `libmenwu`: 120, 122
- `libattr`: 123, 124
- `libmount`: 199, 203
- `libbdf`: 105, 107
- `libmpc`: 111, 111
- `libbkid`: 199, 203
- `libmpfr`: 110, 110
- `libcursesw`: 120, 122
- `libBrokenLocale`: 94, 94
- `libnsl`: 94, 100
- `libbz2`: 117, 118
- `libbss`: 94, 100
- `libc`: 94, 100
- `libopcodes`: 105, 107
- `libpanelw`: 120, 122
- `libpipeline`: 191
- `mountfs`: 216, 216
- `libpropcs`: 155, 166
- `mountvirtfs`: 216, 216
- `libthread`: 94, 100
- `network`: 216, 216
- `libquadmath`: 112, 116
- `libreadline`: 140, 141
- `libresv`: 94, 100
- `librpscv`: 94, 100
- `libSegFault`: 94, 94
- `libsmartcols`: 199, 203
- `libss`: 167, 169
- `libsp`: 212, 212
- `libstdbuf`: 170, 174
- `libupc++`: 112, 112
- `libtel6.so`: 53, 54
- `libtelstub6.a`: 53, 54
- `libthread_db`: 94, 100
- `libudev`: 197, 198
- `libutil`: 94, 100
- `libuuid`: 199, 203
- `liby`: 137, 137
- `libz`: 103, 103
- `preload_libintl`: 163, 164
- `libudev_retry`: 216, 217

## 脚本

- `checkfs`: 216, 216
- `cleansfs`: 216, 216
- `console`: 216, 216
- `/boot/config-4.9.9`: 243, 246
- `/boot/System.map-4.9.9`: 243, 246
- `/dev/*`: 83
- `/etc/fstab`: 241
- `/etc/group`: 89
- `/etc/inittab`: 227
- `/etc/inputrc`: 238
- `/etc/ld.so.conf`: 98
- `/etc/lfs-release`: 249
- `/etc/localtime`: 96
- `/etc/lsb-release`: 249
- `/etc/modprobe.d/usb.conf`: 246
- `/etc/nwitch.conf`: 96
- `/etc/profile`: 236
- `/etc/protocols`: 135
- `/etc/resolv.conf`: 225
- `/etc/services`: 135
- `/etc/syslog.conf`: 194
- `/etc/udev`: 197, 198
- `/etc/udev/hwdb.bin`: 198
- `/etc/vimrc`: 211
- `/usr/include/asm-generic/*.h`: 92, 92
- `/usr/include/asm/*.h`: 92, 92
- `/usr/include/drm/*.h`: 92, 92
- `/usr/include/linux/*.h`: 92, 92
- `/usr/include/mtd/*/*.h`: 92, 92
- `/usr/include/rdma/scsi/*.h`: 92, 92
- `/usr/include/scsi/*.h`: 92, 92
- `/usr/include/sound/*.h`: 92, 92
- `/usr/include/video/*.h`: 92, 92
- `/usr/include/xen/*.h`: 92, 92
- `/var/log/btmp`: 89
- `/var/log/lastlog`: 89
- `/var/log/wtmp`: 89
- `/var/run/utmp`: 89
- `/etc/shells`: 240

`man页`: 93, 93
