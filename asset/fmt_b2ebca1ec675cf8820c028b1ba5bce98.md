
LSB 规范分为两部分——一个在所有类型处理器中保持相同的通用规范，以及一组特定硬件的规范，每种架构类型一套。例如，LSB 1.2 拥有针对 Intel 32 位 (`IA32`) 和 PowerPC 32 位 (`PPC32`) 处理器的特定架构规范。LSB 1.3 在 `IA32` 和 `PPC32` 规范的基础上，增加了 Intel 64 位 (`IA64`) 以及 IBM zSeries 32 位 (`s390`) 和 64 位 (`z390`) 处理器的规范。LSB 2.0 增加了 AMD 64 位 (`AMD64`) 和 `x86_64` 处理器的规范。当前的规范 LSB 2.1 支持多种架构：`IA32`、`IA64`、`PPC32`、`PPC64`（64 位 PowerPC）、`s390`、`z390` 和 `x86_64`。到目前，若干 Linux 发行版已通过 LSB 1.3、LSB 2.0、LSB 3.1、Mandriva Server、Red Hat Enterprise Linux 5、SUSE Linux Enterprise 10 和 Ubuntu 1.0。要了解更多关于 LSB 的信息，请访问 `www.linuxbase.org/LSB_Distribution`。

Linux 发行版带有 Linux 内核以及大量的软件。这些软件包包含了从图形桌面到创建新软件的编程工具等所有内容，并适用于典型的 Linux 发行版。如果没有这些软件，Linux 不会有今天这样流行。

Linux 发行版的核心是来自 GNU 项目的软件集合。如果你通过终端（一种在提示符处输入命令的交互命令行界面）使用 Linux 系统，那么你可能需要了解这些 GNU 工具。作为 Linux 用户，你可能没有意识到你在 Linux 系统中执行的所有任务在多大程度上涉及一个或多个 GNU 软件包。例如，GNOME 图形用户界面 (`GUI`) 和 `bash` shell 都是 GNU 软件程序。屏幕上的窗口模仿文本终端。如果你使用 `ed` 或 `emacs` 编辑器编辑文件，你又在使用 GNU 软件。如果你重新构建内核或使用 C 和 C++ 编译器（它是随 Linux 提供的 GNU 软件的一部分）开发软件，你是通过 `bash` 命令解释器完成的，它接受你输入的命令并响应这些命令运行程序。列表以此类推。

### 什么是 GNU 项目？

GNU 是一个递归缩写，代表 "GNU's Not Unix"（GNU 不是 Unix）。GNU 项目由 Richard Stallman 于 1984 年启动，旨在开发完整操作系统所需的除内核外的所有内容。所有 GNU 软件都以源代码的形式分发。然而，用户可能不需要为 GNU 软件的副本付费。GPL 打印在本书的末尾。

所有 GNU 软件根据通用公共许可证 (`GPL`) 分发，该许可证本质上要求软件以源代码形式分发，并规定任何用户都可以复制、修改和开发该软件。自由软件基金 (`FSF`) 是一家免税慈善机构，为 GNU 项目的工作筹集资金。要了解更多关于 GNU 的信息，请访问其主页 `GNU.org`。

表 1-2 | 知名软件包

| 软件包 | 描述 |
| :--- | :--- |
| `autoconf` | 生成自动配置软件包的脚本 |
| `automake` | 配合 `autoconf` 生成 `Makefile.in` |
| `bash` | Linux 中的默认 shell（命令解释器） |
| `bc` | 具有任意精度的交互式计算器 |
| `Binutils` | 包含一组处理二进制文件的工具：`ar`, `as`, `gas`, `gprof`, `ld`, `nm`, `objcopy`, `objdump`, `readlib`, `size`, `strings`, 和 `strip` |
| 表 1-2 | 续 |
| 软件包 | 描述 |
| :--- | :--- |
| `Coreutils` | 包含三个独立软件包 Fileutils、Shellutils 和 Textutils 的包，并实现了如 `chgrp`, `chmod`, `chown`, `cp`, `dd`, `df`, `dir`, `color`, `du`, `install`, `ln`, `mkdir`, `mkfifo`, `rm`, `rmdir`, `sync`, `touch` 等工具 |
| `GNUChess` | 国际象棋游戏 |
| `GNU C Library` | 用于所有 Linux 程序 |
| `cpio` | 将文件归拷贝到磁盘或文件系统的其他部分 |
| `diff` | 比较文件，以多种不同格式显示行差异 |
| `ed` | 行文本编辑器 |
| `emacs` | 可扩展、自定义的全屏文本编辑器和计算环境 |
| `Findutils` | 包含 `find`, `locate` 和 `xargs` 工具的包 |
| `finger` | 旨在让互联网上的用户获取其他信息的实用程序 |
| `awk` | GNU 项目对 `awk` 编程语言的实现 |
| `gcc` | C、C++、Objective C 以及其他语言的编译器 |
| `gdb` | C、C++ 和 Fortran 的源码调试器 |
| `gbm` | 传统 dbm 和数据库库的替代品 |
| `gettext` | 一组工具，允许软件维护人员对软件包的用户消息进行国际化（使其支持英语、法语和西班牙语等不同语言） |
| `ghostscript` | PostScript 和便携文档格式 (`PDF`) 语言的解释器 |
| `ghostview` | 一个 X 应用程序，通过 GUI 访问 `ghostscript`，能够在窗口中查看 PostScript 或 PDF 文件 |

## Linux 发行版包含的内容

| 软件包 | 描述 | 第一本书 |
| --- | --- | --- |
| `GNOME` | 为 Linux 用户可能执行的各种任务提供图形用户界面 (`GUI`) | 第 1 章 |
| `gnumeric` | 一个在 GNOME 中运行的表格程序（类似于 Microsoft Excel） | | |
| `grep package` | 包含 `grep`、`egrep` 和 `fgrep` 命令，用于查找匹配指定文本的行 | | |
| `groff` | 一种类似于 `troff` 的文档格式化系统 | | |
| `gtk+` | 用于 X 窗口系统的 GUI 工具包（用于开发 GNOME 应用） | | |
| `gzip` | 一个用于压缩和解压缩文件的 GNU 工具 | | |
| `indent` | 通过以几种不同风格中的一种缩进对 C 源代码进行格式化 | | |
| `less` | 一个逐页显示内容的程序，与 `more` 类似，但具有额外功能 | | |
| `libpng` | 用于便携网络图形 (`PNG`) 格式图像文件的库 | | |
| `m4` | 传统 UNIX 处理器的实现 | | |
| `make` | 一种用于确定大型软件包中哪些文件需要重新编译，并使用命令建议这些文件的工具 | | |
| `mtools` | 一组程序，允许使用户在 DOS 文件系统（通常是软盘）上读取、写入和操纵文件 | | |
| `curses` | 一个用于在纯文本终端上显示和更新文本的包 | | |
| `patch` | Larry Wall 程序的 GNU 版本，用于区分差异并将这些差异应用到原始文件中以生成修改后的版本 | | |
| `rcs` | (版本控制系统)：用于软件项目中源文件的版本控制和管理 | | |
| `sed` | `ed` 编辑器的流导向版本 | | |
| `Sharutils` | 一个包含 `shar`（将多个文件创建为存档）和 `unshar`（解压这些存档）的包 | | |
| `tar` | 一种磁带存档程序，支持多卷；具有存档稀疏文件（包含全零数据块）、处理压缩和解压缩以及创建远程存档的能力；以及用于增量和全量备份的其他功能 | | |
| `texinfo` | 一组实用程序，生成打印手册、纯 ASCII 文本和在线超文本文档（称为 `info`），并允许用户查看和阅读在线 `info` | | |
| `time` | 一种报告进程使用的用户时间、系统时间和实际时间的工具 | | |

## 20 Linux 发行版包含的内容

### GUI 和应用程序

面对现实吧——在终端上输入晦涩的 Linux 命令是无聊的。对于普通人来说，通过图形用户界面（`GUI`，读音为 GOOee）使用系统——即一个提供可以点击的图标和可以打开的小窗口窗口的界面——要容易得多。这就是 X 窗口系统（或 X）大显身手的地方。

X 类似于 Microsoft Windows，但 X 的工作原理细节与 Windows 完全不同。（与 Microsoft Windows 不同）它没有为图形应用程序提供任何特定的外观和操作感觉。这种外观和感觉来自 GUI，例如 `GNOME` 和 `KDE`，它们利用了 X 窗口系统。

大多数发行版都以 `XFree86` 或 `XOrg X11` 的形式附带 X 窗口系统——这些是针对 `x86` 系统的 X 窗口系统实现。`XFree86` 和 `XOrg` 兼容当今 PC 上的各种显卡。
