
这种形式（等宽字体）显示了执行命令后的屏幕输出。这种格式也用于显示文件名，例如 `/etc/ld.so.conf`。

这种形式在书中有几种用途。它的主要目的是强调重要的要点或项目。

`http://www.linuxfromscratch.org/`

这种格式用于 PFS 社区内部和外部页面的超链接。它包含了 HOWTO、下载位置和网站。

```
cat > $LFS/etc/group << "EOF"
root:x:0:
bin:x:1:
...\EOF
```

这种格式用于创建配置文件。第一条命令告诉系统从后续行中输入的任何内容创建 `$LFS/group` 文件，直到遇到结束文件（EOF）序列。因此，整个部分通常按照所示内容输入。

```
<REPLACED TEXT>
```

这种格式用于封装不需要按所示内容输入的文本，或用于复制粘贴操作。

`[OPTIONAL TEXT]`

Linux From Scratch - Version 9.0

这种格式用于封装可选文本。

`password(5)`

这种格式用于引用特定的手册（man）页。括号内的数字表示手册中的特定章节。例如，`password` 有两个 man 页。对于 LFS 安装说明，那两个 man 页将位于 `/usr/share/man/man1/password.1` 和 `/usr/share/man/man5/password.5`。当书使用 `password(5)` 时，它特指 `/usr/share/man/man5/password.5`。`man password` 将打印它找到的第一个匹配 "password" 的 man 页，即 `/usr/share/man/man1/password.1`。在本示例中，你需要运行 `man 5 password` 来引用所指的页面。需要注意的是，大多数 man 页在不同章节中没有重名的页名。因此，`man <program name>` 通常足够了。

## 结构

本书分为以下部分。

### 第一部分 - 引言

### 第二部分 - 为构建准备

### 第三部分 - 构建 LFS 系统

### 错误说明 (Errata)

## Syslog

此包包含了记录系统消息的程序，例如内核或守护进程在发生异常事件时提供的消息。

- Sysvinit

此包提供了 `init` 程序，它是 Linux 系统上所有其他进程的父进程。

- Tar

此包为 LFS 中使用的几乎所有软件包提供了归档和提取能力。

- Tcl

此包包含了 Tool Command Language（工具命令语言），它用于 LFS 软件包中的许多测试套件。它仅安装在临时工具链中。

- Texinfo

此包包含了读取、写入和转换 info 页的程序。它被用于许多 LFS 软件包的安装程序。

- Util-linux

此包包含了各种杂用程序。其中包含处理文件系统、控制台、分区和消息的工具。

- Vim

此包包含一个编辑器。选择它是因为它与经典编辑器的兼容性以及它拥有大量强大的功能。对于许多用户来说，编辑器是一个非常个人的选择，如果需要，可以用任何其他编辑器代替。

- XML::Parser

此包是一个与 Expat 接口的 Perl 模块。

- XZ Utils

此包包含了压缩和解压文件的程序。它提供了通常可用的最高压缩率，对于解压 XZ 或 LZMA 格式的软件包很有用。

- Zlib

此包包含了某些程序使用的压缩和解压程序。

## 前提条件

构建一个 LFS 系统并不是一项简单的任务。它要求你具备某种 Unix 系统管理现有知识，以便解决问题并正确执行列出的命令。特别是，至少你应该已经具备了使用命令行（shell）复制或移动文件和目录、查看目录文件内容以及更改当前目录的能力。预计你对使用和安装 Linux 软件有合理的了解。

由于 LFS 教程假设你至少具备这种基础水平，因此相关的 LFS 论坛可能无法在这些方面为你提供太多帮助。你会发现，关于此类基础知识的问题可能得不到回答，或者简单地引向 LFS 核心预读列表。

在构建 LFS 系统之前，我们建议阅读以下内容：

- Software-Building-HOWTO `http://www.tldp.org/HOWTO/Software-Building-HOWTO.html`

这是一个关于在 Linux 下构建和安装“通用”Unix 软件包的综合指南。虽然它编写于很久以前，但它仍然对构建和安装软件所需的基础技术提供了良好的总结。

- Beginner's Guide to Installing Source `http://mol.vonos.net/linux/beginners-installing-from-source/`

该指南对从源代码构建软件所需的基础技能和技术进行了良好的总结。

## 排版

为了方便阅读，本书通处使用了一些排版规范。本节包含了在 Linux From Scratch 各处可见的一些排版格式示例。

```
/configure --prefix=/usr
```

这种形式应按照所示的内容完全输入，除非周围文字另有说明。它也被用于解释部分，以识别引用的是哪一个命令。

在某些情况下，一行通过行尾的反斜杠扩展到两行或多行。

```
gcc -B/usr/bin/" ... /binutils-2.18/configure \
--prefix=/tools --disable-nls --disable-werror
```

注意，反斜杠后面必须紧跟回车。其他空白字符（如空格或制表符）会导致错误的结果。

```
install-info: unknown '--dir-file=/mnt/lfs/usr/info/dir'
```

这种形式（等宽字体）显示了执行命令后的屏幕输出。这种格式也用于显示文件名，例如 `/etc/ld.so.conf`。

强调

这种形式在书中有几种用途。它的主要目的是强调重要的要点或项目。

`http://www.linuxfromscratch.org/`

这种格式用于 PFS 社区内部和外部页面的超链接。它包含了 HOWTO、下载位置和网站。

```
cat > $LFS/etc/group << "EOF"
root:x:0:
bin:x:1:
...\EOF
```

这种格式用于创建配置文件。第一条命令告诉系统从后续行中输入的任何内容创建 `$LFS/group` 文件，直到遇到结束文件（EOF）序列。因此，整个部分通常按照所示内容输入。

```
<REPLACED TEXT>
```

这种格式用于封装不需要按所示内容输入的文本，或用于复制粘贴操作。

`[OPTIONAL TEXT]`

Linux From Scratch - Version 9.0

这种格式用于封装可选文本。

`password(5)`

这种格式用于引用特定的手册（man）页。括号内的数字表示手册中的特定章节。例如，`password` 有两个 man 页。对于 LFS 安装说明，那两个 man 页将位于 `/usr/share/man/man1/password.1` 和 `/usr/share/man/man5/password.5`。当书使用 `password(5)` 时，它特指 `/usr/share/man/man5/password.5`。`man password` 将打印它找到的第一个匹配 "password" 的 man 页，即 `/usr/share/man/man1/password.1`。在本示例中，你需要运行 `man 5 password` 来引用所指的页面。需要注意的是，大多数 man 页在不同章节中没有重名的页名。因此，`man <program name>` 通常足够了。
