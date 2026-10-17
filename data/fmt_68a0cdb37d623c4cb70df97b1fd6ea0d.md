
维基百科 Python 编程语言：http://en.wikipedia.org/wiki/Python_(programming_language)。

Python 在线文档：http://docs.python.org。

# GNU/Linux 管理基础

## 本章内容

- 导航 Linux 文件系统
- 在 GNU/Linux 中管理包
- 管理你的内核

## 引言

本章从开发者的视角探索 GNU/Linux 系统管理。这意味着将不会涵盖基本配置、用户管理等主题。相反，本章将探索如何导航 Linux 文件系统、包管理、内核管理以及主题。

# 导航 Linux 文件系统

对于许多 UNIX 和 Linux 发行版，它们很容易发生分支，从而变得不兼容。文件系统是可能导致不兼容的主要区域之一（包括其结构和文件存储的位置）。幸运的是，文件系统层次结构标准（FHS）的创建是为了解决这一问题（不仅针对大量的 Linux 发行版，还针对 BSD 和其他类 Unix 操作系统）。你可以在其主页 http://www.pathname.com/fhs/ 找到更多关于 FHS 的信息。

FHS 定义了出现在根 (`/`) 文件系统中的子目录以及它们应该的内容（见表 28.1）。

## 542 GNU/Linux 应用程序编程

### 表 28.1 FHS 的标准子目录

| 目录 | 目的 |
|---|---|
| `/` | 原始根层次结构（用于整个根文件系统） |
| `/bin` | 单用户模式下使用的主要命令 |
| `/sbin` | 系统二进制文件 |
| `/dev` | 设备文件（用户空间到内核叶节点） |
| `/etc` | 局级配置文件 |
| `/home` | 本地用户的家目录 |
| `/lib` | `/bin` 和 `/sbin` 中二进制文件所需的库 |
| `/mnt` | 临时挂载文件系统的目录 |
| `/opt` | 可选软件包的目录 |
| `/proc` | 虚拟文件系统（内核状态和用户进程状态） |
| `/tmp` | 临时文件目录 |
| `/usr` | 用户相关层次结构（`/usr/bin`, `/usr/sbin`, `/usr/include` 等） |
| `/var` | 可变文件（如邮件和打印队列、电子邮件、日志等） |

FHS 提供了更详尽的细节，但这个初级介绍为根文件系统的内容提供了一些视角。该标准实际上对文件位置（包括其原理）进行了非常详细的阐述，值得查阅。

# 包管理

包管理是维护软件包（安装、升级或卸载）的过程。软件软件包通常分发在单个文件中（为了简单起见），但可能会在系统中的多个位置安装许多文件。软件包不仅包含软件本身（源码或二进制形式），还包含关于如何以及何处安装该包的自动化指令。

本节探索了一些包管理的可能性，从最基础的开始。

## 第 28 章 GNU/Linux 管理基础 543

# TARBALL 分发

分发软件包最常见且平台无关的方法是通过压缩的 tarball（压缩包）。tarball 是一种使用 `tar` 命令创建和处理的文件格式。tarball 通常需要更多的工作，但由于它非常常见，因此理解它是很有用的。

`tar` 命令的名字源于它最初作为磁带备份格式的使用。该名称本身源于“tape archive”（磁带存档），但在 POSIX 框架下被标准化。`tar` 工具保留了其旧磁带使用时代的传统。例如，访问（像磁带一样）是顺序的。使用 `tar` 时，如果要提取最后一个文件，将扫描整个存档以获取该文件（就像在磁带硬件的情况下一样）。

![](img/f7bd35eb87a62f74c6f23c07df847dff_563_0.png)

许多软件软件包以 tarball 的形式分发，因为 tarball 是通用的，并且可以压缩到便于存储和传输的大小。分发软件 tarball 通常意味着一组其他工具（如 `automake`、`configure` 等），这些工具将在第 8 章“使用 autoconf 构建包”中描述。

![](img/f7bd35eb87a62f74c6f23c07df847dff_563_1.png)

Tarball 通常遵循标准的命名规范，因此很容易知道文件是如何创建的。标准的 tarball 命名为 `file.tar`，表示未压缩的 tarball。如果 tarball 是压缩过的，则命名为 `file.tar.gz`（gzip 压缩）或 `file.tar.bz2`（bzip2 压缩）。正如我们在本章后面看到的，tarball 可以通过 `tar` 命令自动压缩或解压。

下载 tarball 后，常用的处理位置是 `/usr/local/src`。回想一下，该位置存储了特定此主机的本地数据。如果在安装软件包后删除 tarball，更好的地方是 `/tmp`。该位置是理想的，因为机会定期和自动清理。但有时保留源码是有必要的，因此在示例中，使用了前一个目录。接下来（见列表 28.1），下载要安装的特定 tarball（在本示例中，为了演示目的，使用了 Ruby 的最新版本）。

使用压缩的 Ruby tarball，你通过三个选项对 tarball 运行 `tar` 命令。第一个选项 `x` 表示你正在提取一个存档（而不是使用 `c` 创建一个）。接着，你指定命令行上后面跟着一个文件名（不使用 `c`）。最后，你指定 `z` 表示它是一个 gzip 压缩的存档并解压 tarball。结果是一个名为 `ruby-1.8.6-p111` 的新目录，包含了该面向对象语言的源码。

## 544 GNU/Linux 应用程序编程

### 列表 28.1 下载 Tarball 到工作目录

```
root@camus:~# cd /usr/local/src
root@camus:/usr/local/src# wget http://xyz.lcs.mit.edu/ruby/
ruby-1.8.6-p111.tar.gz
       18:35:21 (218.6 KB/s) `ruby-1.8.6-p111.tar.gz` saved
Length: 4,547,579 (4.3M) [application/x-tar]
18:35:41
root@camus:/usr/local/src# tar xzf ruby-1.8.6-p111.tar.gz
root@camus:/usr/local/src#
```

下一步是构建你的源码，你可能进入子目录。如果子目录包含 Makefile（make 工具的规范），你只需要输入 `make` 来构建源码。如果没有 Makefile，则你需要通过配置过程。该过程会自动创建构建源码的 Makefile。该过程是必要的，因为系统有许多不同之处。例如，工具可能存储在不同的地方。你运行的 shell 可能与预期的不同。编译器可能不支持软件包的先决条件，或者缺少先决包（需要下载额外的模块）。配置过程会自动检查你的系统并相应地构建 Makefile。

接下来的过程通常非常简单（见列表 28.2）。首先，运行工作目录（即刚刚安装源码的地方）中的 configure 脚本。接着，输入配置指令——例如，安装到何、启用哪些选项等。你通常可以通过输入 `./configure --help` 查看可用选项的列表。

### 列表 28.2 configure 和 make 过程

```
root@camus:/usr/local/src/ruby-1.8.6-p111# ./configure
checking build system... i686-pc-linux-gnu
checking host system type... i686-pc-linux-gnu
checking target system type... i686-pc-linux-gnu
checking for gcc... gcc
checking for C compiler default output file name... aout
checking whether the C compiler works... yes
```

## 第 28 章 GNU/Linux 管理基础 545

```
checking whether we are cross compiling... no
...
creating config.h
configure: creating ./config.status
config.status: creating Makefile
root@camus:/usr/local/src/ruby-1.8.6-p111# make
root@camus:/usr/local/src/ruby-1.8.6-p111# array array
gcc -g02 -DRY_EXPORT -D_GNU_SOURCE=1 -I. -I. -c array.c
gcc -g02 -DRY_EXPORT -D_GNU_SOURCE=1 -I. -I. -c bignum.c
```
