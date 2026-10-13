
其中 `a` 是主版本号，`b` 是次版本号，`c` 是补丁号。目前已经建立了一种惯例，奇数次次版本被认为是开发版本，偶数次次版本被认为是稳定的生产版本。

在编写本文时，Linux 内核的当前稳定生产版本是 `2.2.13`，而当前的开发版本是 `2.3.31`。虽然版本 `2.2.13` 是当前的内核版本，但大多数 Linux 发行版尚未发布该版本。

要确定系统使用的内核版本，可以使用 `-a` 选项。列表 2.7 显示了 Mandrake 6.0 使用该命令的示例。

### 列表 2.7 uname -a 输出

```
1 [rich@shadrach]$ uname -a
2 Linux shadrach.small.org 2.2.9-19mdk #1 Wed May 19 19:53:00 GMT 1999
- i586 unknown
3 [rich@shadrach]$
```

第 2 行显示了 `uname` 命令的输出。在本例中，使用的是专门为 Mandrake 发布版编译的 `2.2.9` 内核，因此带有 `-19mdk` 信息。

可以在运行的 Linux 系统中下载更新版本的内核。你必须拥有源代码文件，这些文件通常可以从 `http://www.kernel.org` 下载。编译和安装新内核并不适合初学者。如果你决定升级 Linux 内核，请阅读内核源代码带的所有文档以及特定 Linux 发行版支持小组提供的建议。

### 注意

安装新的 Linux 内核属于“没坏就修”的类别。如果你的 Linux 服务器没有遇到任何问题，不要仅仅因为有更新就尝试安装新内核。许多 Linux 发行版都针对特定内核进行了微调；只更改内核可能会导致不可预测的结果。

## Linux 库

Linux 操作系统严重依赖 C 语言。内核、许多设备驱动程序以及所有工具都是使用 C 语言编写的。大多数为 Linux 平台编写的应用程序使用 C 语言编写，这并不意外。

C 语言的一个特性是程序在运行时可以从库文件中加载代码段。大多数熟悉 Microsoft Windows 操作系统的计算机用户都熟悉 DLL。可以在多个程序之间共享程序代码可以编译成公共库（DLL 文件）。当程序执行时，如果需要使用文件中的库函数，它可以将 DLL 文件加载到内存中。

Linux 操作系统使用了类似的技术。在 Linux 中，`lib` 前缀表示库文件。库表跟踪系统上所有的共享库。Microsoft Windows 环境中的一个常见问题是，当一个程序更新 DLL 文件时，另一个需要旧版本 DLL 的程序会停止工作。在 Linux 中这不是问题，因为库表可以维护同一库的多个副本。

## Linux 简介

## 第 2 章

一段时间后，Linux 开发者认为旧的 C 库方法不再理想。这不仅是因为该库与 Linux 内核的关系过于紧密，而且它产生的是一种名为 `aout` 的旧版可执行文件格式。大多数较新的 POSIX 类型系统已经转换为可执行文件和链接格式（`ELF`），事实证明这种格式更快速、更高效。下一个版本的 C 库——`libc5`——实现了 `ELF` 格式。使用 `libc5` 编译的程序将无法在仍使用 `aout` 风格库的旧版 Linux 系统上运行。然而，在 `aout` 风格下编译的旧程序在新的 `libc5` 上可以正常执行。这在 Linux 应用世界中引发了第一轮混乱。

在开发和使用 `libc5` 库的同时，GNU 项目开发了自己的不依赖于特定内核的库。GNU 项目的 C 库是 `glibc`。由于 `libc5` 库当时已经可以良好工作，并没有没有人继续投入 `glibc` 库的工作。

在经历了一段沉寂后，程序员们重新审视了 `glibc` 代码。他们认为它可能比 `libc5` 好。`glibc` 的优势之一是它独立于任何特定的操作系统或内核。在这些程序员的努力下，诞生了 `glibc 2.0`。

许多 Linux 发行版决定将 `glibc 2.0` 代码与他们新的 Linux 发行版一起。遗憾的是，许多 Linux 发行版决定在新内核中保留 `libc5` 库。这很快变得扑朔。

使用 `glibc 2.0` 库的 Linux 发行版为了后兼容，也包含了 `libc5` 库。请记住 Linux 维护着一个库文件表，同时使用两个不同的 C 库是可能的。因为如此，许多 Linux 为了兼容性继续使用 `libc5` 库。

Netscape 的 Communicator 和 Core 的 WordPerfect 是两个继续使用 `libc5` 库编写的应用程序，几乎可以在每个 Linux 发行版上运行。一些 Linux 应用程序员决定利用新 `glibc 2.0` 库的功能，并为该平台发布了软件版本。Star Division 的 StarOffice 5.0 和 Oracle 的 Oracle8 数据库软件是两个使用 `glibc 2.0` 库的应用程序。这些应用程序无法在仅使用 `libc5` 库的 Linux 发行版上运行。

如果故事到此结束那也够糟糕了。最近，GNU 项目发布了 `glibc 2.1` 库。让事情复杂化的是，`glibc 2.0` 中的某些函数发生了变化，导致使用 `glibc 2.0` 库编写的一些应用程序（如 StarOffice 5.0）在运行使用 `glibc 2.1` 库的 Linux 系统运行时崩溃。

![](img/4af9afea53463095bafc6057b1f7b908_59_0.png)

## Linux 库

如果你在读完本节后对你的 Linux 系统感到担心，不必。对于以源码分发的应用程序（例如本书中讨论的所有邮件服务器程序），使用你系统中的任何 C 库来编译代码，代码就能运行良好良好。对于以二进制格式分发的应用程序，只需记住使用为你系统发布的 C 库版本（`libc5`、`glibc 2.0` 或 `glibc 2.1`）即可。

如果你不知道正在使用哪种 Linux 发行版，可以通过查看 `/lib` 目录下的库来确定。表 2.7 显示了 Linux 系统可能存在的不同 C 库。

### 表 2.7 Linux C 库列表

| 库 | 描述 |
| --- | --- |
| `libc.so` | libc1 a.out library |
| `libc.so.2` | libc2 a.out library |
| `libc.so.3` | libc3 a.out library |
| `libc.so.4` | libc4 a.out library |
| `libc.so.5` | libc5 ELF library |
| `libc.so.6` | glibc 库的符号链接 |
| `libc-2.0.x.so` | glibc 2.0 ELF library |
| `libc-2.1.x.so` | glibc 2.1 ELF library |

## GNU 项目

GNU 项目创建于 1984 年，旨在创建一个自由的类 UNIX 操作系统。它负责维护许多常用 UNIX 工具的开源版本。没有 GNU 项目，Linux 操作系统将不会非常有趣。Linux 操作系统的核心大部分都是 GNU 项目的产物。本节描述了三个对 Linux 邮件服务器运行至关重要的程序：`bash` shell、`gcc` 编译器和 `make` 工具。

## Linux 简介

## 第 2 章

### GNU bash

内核需要某种宏处理器来使用户户能够在系统上执行命令（程序）。在 UNIX 世界中，宏处理器被称为 shell。UNIX 环境中最常见的 shell 是 Bourne shell，以其创建者 Stephen Bourne 命名。Bourne shell 是一个在系统上作为进程运行的程序，并有一个活动会话允许使用户在命令提示符处输入命令。命令可以是可执行程序、shell 内部命令，或包含 shell 命令的程序文件（脚本文件）。shell 通过创建一个新进程并在该新进程中运行程序来启动可执行程序。这使得从 shell 运行的每个程序在系统中都有它们自己的进程。

GNU 项目的开发者知道，对于开源类 UNIX 操作系统来说，有一个良好的开源 shell 是至关重要的。他们开发的 shell 是 `bash`，即 Bourne-Again Shell。`bash` 兼容原始的 Bourne shell（称为 `sh`）。`bash` shell 还包含了在 UNIX 环境开发的其他 shell 的功能，如 C shell (`csh`) 和 Korn shell (`ksh`)。`bash` 已成为系统的默认 shell。在编写时 `bash` 版本为 `2.0`。

当用户 登录时，`bash` 有几个不同的配置文件可以修改其 特性。当 `bash` 作为 shell 被调用时，`/etc/profile` 文件中的命令会被执行。这发生在所有在密码文件中指定 `bash` 为默认 shell 的用户身上。![](img/4af9afea53463095bafc6057b1f7b908_61_0.png)

### 图 2.9 /etc/profile
