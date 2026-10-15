
请注意，使用默认配置编译的 BusyBox 实用程序需要列表 11-2 中的三个共享库。如果我们选择将 BusyBox 构建为静态二进制文件，`ldd` 只会发出一条消息，告诉我们 BusyBox 二进制文件不是一个动态可执行文件。换句话说，它不需要任何共享库来解决可执行文件中的未解析依赖项。由于不需要共享库，静态链接在根文件系统上产生的占用空间更小。然而，在没有共享库的情况下构建嵌入式应用意味着你的应用程序将无法使用任何熟悉的 C 库函数。

我们将在下一节中讨论列表 11-1 中的其他选项。

### 11.2.1 交叉编译 BusyBox

如本章开头所述，BusyBox 的作者打算让该软件包在交叉开发环境中使用，因此在此类环境中构建 BusyBox 非常简单。在大多数情况下，唯一的要求是指定开发工作站上交叉编译器的前缀。这是在 BusyBox 配置实用程序的 Build Options（构建选项）中通过选择“使用交叉编译器构建 BusyBox”选项来指定的。随后，你会看到一个用于输入交叉编译器前缀的选项。你输入的前缀取决于你的交叉开发环境。一些示例包括 `xscale_be-` 或 `ppc-linux`。我们将在下一章讨论嵌入式开发环境时更详细地介绍这一点。

列表 11-1 中的最后一个选项是用于你可能想要在编译器命令行中包含的任何额外标志。这可能包括生成调试信息的选项（`-g`）、设置优化级别的选项（例如 `-O2`），以及其他可能因你的特定安装和目标系统而异的编译器选项。

## 11.3 BusyBox 操作

当你构建 BusyBox 时，最终会得到一个名为 `busybox` 的二进制文件。BusyBox 可以通过二进制文件名本身调用，但更常见的是通过符号链接启动。当在不带命令行参数的情况下调用 BusyBox 时，它会列出通过配置启用的功能列表。列表 11-3 显示了这样的输出（格式已略微调整以符合页面宽度）。

### 列表 11-3

```text

BusyBox Usage

root@cayote # ./busybox

BusyBox v1.01 (2005.12.03-18:00+0000) multi-call binary

Usage: busybox [function] [arguments]...

   or [function] [arguments]...

BusyBox is a multi-call binary that combines many common Unix

utilities into a single executable.  Most people will create a

link to busybox for each function they wish to use and BusyBox

will act like whatever it was invoked as!

Currently defined functions:

i, ash, basenames, bunzip2, busybox, bzcat, cat, chgrp, chmod,

chown, chroot, chvt, clear, cmp, cp, cut, date, dd, dealioct,

df, dirname, dmesg, du, echo, egrep, env, expr, false, fpreg,

find, free, grep, gunzip, gzip, halt, head, hexdump, hostname,

id, iconfig, init, install, kill, killall, klogd, linuxrc, ln,

logger, ls, mkdir, mknod, mktemp, more, mount, mv, openvt, pidof,

ping, pivot_root, poweroff, ps, pwd, readlink, reboot, reset,

rm, rmdir, route, sed, sh, sleep, sort, strings, swapon, swapoff,

sync, syslogd, tail, tar, tee, test, time, touch, tr, true, tty,

ttyun, uname, uniq, unzip, uptime, usleep, vi, wc, wget, which,

whoami, xargs, yes, zcat

```

从列表 11-3 中，你可以看到这个 BusyBox 构建中启用的功能列表。它们按字母顺序排列，从 `ash`（一种针对小内存占用优化的 shell）到 `zcat`（一种用于解压缩文件内容的实用程序）。这是该特定 BusyBox 快照中默认启用的实用程序集。

要调用特定功能，请在命令行上执行 `busybox` 并传入一个已定义的功能。因此，要显示当前目录中的文件列表，请执行以下命令：

```bash

[root@coyote]# ./busybox ls

```

列表 11-3 中 BusyBox 使用说明消息的另一个重要内容是程序的简短描述。它将 BusyBox 描述为一个多调用二进制文件，将许多通用实用程序合并到一个可执行文件中。这就是之前提到的符号链接的用途。BusyBox 旨在通过以其将执行的功能命名的符号链接来调用。这消除了输入两个单词的命令来调用特定功能的负担，并向用户提供了一组与同名实用程序熟悉的命令。列表 11-4 和 11-5 应该能清楚地说明这一点。

### 列表 11-4

BusyBox 符号链接结构—顶层

```bash

[root@coyote]$ ls -l /

total 12

drwxrwxr-x 2 root  root  4096 Dec 3 13:38 bin

lrwxrwxrwx 1 root  root    11 Dec 3 13:38 linuxrc -> bin/busybox

drwxrwxr-x 2 root  root  4096 Dec 3 13:38 sbin

drwxrwxr-x 4 root  root  4096 Dec 3 13:38 usr

```

列表 11-4 展示了通过 `make install` 命令由 BusyBox 软件包构建的目标目录结构。可执行文件 `busybox` 位于 `/bin` 目录中，并且符号链接已填充到结构的其余部分，指回 `/bin/busybox`。列表 11-5 扩展了列表 11-4 中的目录结构。

### 清单 11-5

BusyBox 符号链接结构——树形详情

```
[root@coyote]$ tree

. bin
|-- ash -> busybox
|-- busybox
|-- cat -> busybox
|-- cp -> busybox
|-- ...
|-- zcat -> busybox
|-- linuxrc -> bin/busybox
. sbin
|-- halt -> ../bin/busybox
|-- ifconfig -> ../bin/busybox
|-- init -> ../bin/busybox
|-- klogd -> ../bin/busybox
|-- ...
|-- syslogd -> ../bin/busybox
. usr
|-- bin
|-- .. -> ../bin/busybox
|-- basename -> ../bin/busybox
|-- ...
|-- xargs -> ../bin/busybox
|-- yes -> ../bin/busybox
. sbin
|-- chroot -> ../../bin/busybox
```

为了易读性并避免三页长的清单，清单 11-5 的输出内容已被大幅截断。每一行包含省略号 (...) 的行表示该清单已被修剪，仅显示给定目录的前几条和后几条条目。实际上，根据您使用 BusyBox 配置工具启用的功能，这些目录中可以填充超过 100 个符号链接。

请注意 `busybox` 可执行文件本身，它是 `/bin` 目录中的第二项条目。同样在 `/bin` 目录中，还有指向 `busybox` 的符号链接，如 `ash`、`cat`、`cp` ... 一直到 `zcat`。再次说明，为了易读性，本清单中 `cp` 和 `zcat` 之间的条目已被省略。有了这种符号链接结构，用户只需输入工具的实际名称即可调用其功能。例如，要使用 `busybox` 的 `ifconfig` 工具配置网络接口，用户可能输入类似以下的命令：

```
$ ifconfig eth1 192.168.1.14
```
