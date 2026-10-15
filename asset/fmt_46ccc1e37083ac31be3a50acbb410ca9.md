
```bash
$ xscale-ldd busybox
linux.so.2 => (0xb0b870)
libm.so.6 => /lib/tls/i686/cmov/libm.so.6 (0xb7b4d00)
libc.so.6 => /lib/tls/i686/cmov/libc.so.6 (0xb7efe00)
/lib/ld-linux.so.2 => (0xb08800)
```

注意，使用默认配置编译的 BusyBox 需要所示的四个库。如果我们选择将 BusyBox 构建为静态二进制文件，`ld` 只会提示该二进制不是动态执行文件。换句话说，它不需要共享库。静态链接产生更小的文件系统占用，因为不需要共享库。然而，在没有共享库的情况下构建嵌入式应用程序意味着您的应用程序无法使用 C 函数。为了让您了解静态链接的 BusyBox 与链接共享库的 BusyBox 之间的相对大小差异，对于最近版本，静态链接的 busybox 约为 1.5MB，而动态链接镜像为 778KB。

## 11.2.1 交叉编译 BusyBox

正如本章开头提到的，BusyBox 的作者打算将该软件包用于交叉开发环境，因此在类环境中构建 BusyBox 非常容易。在早期的 BusyBox 版本中，唯一的要求是通过选择使用交叉编译器构建的选项来指定交叉编译的前缀。这已被更标准的方法取代，类似于构建其他 Linux 内核软件包。要在您的开发工作站上使用特定的交叉编译器进行交叉编译，只需在环境中定义 `CROSS_COMPILE`。`CROSS_COMPILE` 值的示例有 `arm5vt_le-`、`xscale_be-` 和 `ppc_linux-`。注意，您也可以在描述的编译工具中指定交叉编译器前缀。我们在下一章检查嵌入式开发环境时，将更详细地涵盖交叉编译相关的编译器前缀。

构建 BusyBox 后，就会得到一个二进制文件——你猜对了——BusyBox。BusyBox 可以通过二进制文件本身进行调用，但它通常通过一个符号链接（symlink）调用。当不带命令行参数直接调用 BusyBox 时，它会生成一个通过配置启用的函数列表。列表 11-3 显示了输出（已根据页面宽度进行格式化）。

### 列表 11-3 BusyBox 使用方法

```
root@coyote # busybox
BusyBox v1.13.2 (2010-02-24 16:04:14 EST) multi-call binary
Copyright (C) 1998-2008 Erik Andersen, Rob Landley, Denys Vlasenko and others. Licensed under GPLV2.
See source distribution for full notice.
```

用法: busybox [function] [arguments]...

或: function [arguments]...

BusyBox 是一个多功能二进制文件，它将许多 Unix 工具合并到单个可执行文件中。大多数人会为想要使用的每个函数创建一个指向 busybox 的链接，而 BusyBox 会像任何被调用的方式一样工作！

已定义的函数：

```json
{
  "functions": [
    "{addgroup, addgroup, adduser, ar, sh, awk, basename, blkid, bunzip2, bzcat, chat, chattr, chrpg, chmod, chpass, chvt, clear, cp, cpio, cryptpw, cut, date, dd, deallocvt, delgroup, deluser, df, dhcprelay, diff, echo, egrev, expr, false, fbset, fdisk, fdisk, fgrep, find, free, freerandisk, fck, fckdm.minix, dumpmangle, fewer, fuser, getopt, grep, gzip, gunzip, halt, head, hexdump, hostname, hwdock, id, ifconfig, ifdown, ifup, less, linuxc, insmod, ip, kill, killall, klog, last, ln, loadfont, logger, login, logread, logger, legetop, ls, lmad, madedevs, dmsum, medcv, micron, mdir, mkfifo, mkfinis, mknod, mkswap, mktap, mdprobe, mount, mv, nc, netstat, nice, nohup, nlookup, od, openv, passwd, patch, pidof, ping, ping6, pivot_root, preprocess, ps, pw, rdate, rdev, reahead, readlink, readprofile, reabth, renice, reset, rm, rmdir, rmmod, rtwc, run-parts, sed, seq, setconsole, setfont, sh, showkey, sleep, sort, start-stop-daemon, strings, stty, su, sulogin, swapon, switch_root, sync, sysctl, syslog, tail, tee, telnet, telnetd, tftp, time, top, touch, traceroute, true, try, udhcpc, udhcpd, umount, uname, uniq, unzip, uptime, usleep, vi, vlock, watch, wget, which, whoami, xargs, yes, zcat"
  ]
}
```

从列表 11-3 中，你可以看到此 BusyBox 构建中启用的函数列表。它们按字母顺序（忽略 shell 脚本的 `[` 和 `[[` 运算符）从 `addgroup` 到 `zcat` 排列，`zcat` 是用于解压压缩文件内容的工具。此列表代表该特定 BusyBox 构建中启用的工具集。

要调用特定函数，请通过命令行传递一个定义的函数之一来执行 busybox。例如，要显示根目录下的文件列表，请执行此命令：

```
[root@coyote]# busybox ls /
```

列表 11-3 所示的 BusyBox 用法中的另一个重要信息是程序的简短描述。它将 BusyBox 描述为多功能二进制文件，将许多常用工具合并到单个可执行文件中。这就是前面提到的符号链接的目的。BusyBox 设计的目的是通过与其将执行的函数同名的符号链接来调用的。这消除了必须输入两个单词命令来调用给定函数的负担，并为用户提供了一组与同名工具类似的熟悉命令。列表 11-4 和 11-5 应该说明这一点。

列表 11-4 显示了由 BusyBox 软件包通过 busybox 源码树中的 `make install` 命令构建的目标目录结构。

### 列表 11-4 来自 make install 的 BusyBox 符号链接结构

```
[root@coyote]$ ls -l /
total 12
drwxr-xr-x 2 root 4096 Dec 3 13:38 bin
lrwxr-xr-x 1 root 11 Dec 3 13:38 linux -> busybox
drwxr-xr-x 2 root 4096 Dec 3 13:38 sbin
drwxr-xr-x 4 root 4096 Dec 3 13:38 usr
```

可执行文件 `busybox` 位于 `/bin` 目录中，在结构的其余部分填充了符号链接，指向 `/bin/busybox`。列表 11-5 扩展了列表 11-4 的目录结构。

### 列表 11-5 BusyBox 符号链接结构：树形细节

```
[root@coyote]$ tree
|-- bin
|   |-- addgroup -> busybox
|   |-- busybox
```

### 列表 11-5 继续

```
| -- cat -> busybox
| -- cp -> busybox
...
| -- zcat -> busybox
|-- linux -> /bin/busybox
|-- sbin
|   -- halt -> busybox
|   -- ifconfig -> busybox
|   -- init -> busybox
|   -- klog -> busybox
|   -- syslog -> busybox
|-- usr
|   -- bin
|   |-- xargs -> busybox
|   |-- yes -> busybox
```

这是一个 BusyBox 配置的目标，该操作执行成功，并且 busybox 通过我们根文件系统上的软链接 `/bin/sh` 启动。

第一个 BusyBox 会抱怨找不到 `/etc/init.d/rc`。这是 BusyBox 搜索的默认初始化脚本。与使用 `inittab` 相比，这是初始化基于 BusyBox 的嵌入式系统的首选方法。

当处于初始化状态时，BusyBox 会显示一个提示符，要求用户按回车键以激活控制台。当 BusyBox 检测到回车键时，它会执行一个等待用户输入的 shell。关于作业控制的最后信息是由于在这一特定的（以及典型的嵌入式系统）中，我们正在串口终端上创建系统控制台。Linux 内核包含代码，在检测到控制台位于串口终端上运行时禁用作业控制。

此示例产生了一个可以运行的系统，提供了近 100 个 Linux 实用程序，包括核心工具、文件工具、网络支持以及功能相当的 shell。你可以看到，这个简单的软件包提供了一个强大的平台，你可以在此基础上构建自己的应用程序。当然，需要注意的是，如果没有对 lib 和其他系统库的支持，你在实现应用程序时将面临一项艰巨的任务。你必须为典型 C 程序所依赖的所有标准 C 库调用和其他库函数提供支持。或者，你可以对应用程序与其依赖的库进行静态链接，但如果你有多个应用程序使用这种方法，你的应用程序总大小可能会超过动态链接并在目标机上放置共享库的总和。

## 11.3.2 示例 rc 初始化脚本

在 BusyBox 产生一个交互式 shell 之前，它会尝试从脚本 `/etc/init.d/rcS` 中执行命令，如列表 11-7 所示。你的应用程序在 BusyBox 系统正是在这里运行。列表 11-8 提供了一个简单的 rc 初始化脚本。

### 列表 11-8 简单的 rcS BusyBox 启动脚本

```sh
#!/bin/sh
echo "Mounting proc"
mount -t /proc /proc
echo "Starting system loggers"
syslogd
```

### 列表 11-8 继续

```sh
klogd

echo "Configuring loopback interface"
ifconfig lo 127.0.0.1

echo "Starting inetd"
xinetd

# start a shell
busybox sh
```

这个简单的脚本大部分是自述易懂的。首先，将 `/proc` 文件系统挂载到其预留的挂载点很重要。这是因为许多实用程序从 `/proc` 文件系统获取信息。这在第 9 章中有更详细的解释。接下来，我们尽早启动系统日志记录程序以捕捉任何启动问题。在系统日志守护进程之后，我们为系统配置了环回接口。再次，Linux 设施的传统做法假设存在环回接口，如果你的系统支持配置的 sockets，你应该启用此接口。在启动 shell 之前我们做的最后一件事是启动 Internet 服务器 `xinetd`。该程序在后台运行，监听任何已配置的网络接口上的网络请求。例如，要向开发板发起的 telnet 会话，`xinetd` 会拦截 telnet 连接请求并产生一个 telnet 服务器来处理该会话。

你的应用程序可以从 rc 初始化脚本启动，而不是启动 shell。列表 11-8 是一个支持 telnet 运行系统和内核日志记录器等基本服务的目标板的简单示例。

## 11.3.3 BusyBox 目标安装

只有当你理解了软链接的使用和目的后，才能继续讨论 BusyBox 的安装。BusyBox Makefile 包含一个名为 `install` 的目标。执行 `make install` 会创建一个包含 BusyBox 可执行文件和软链接树的目录结构。此环境需要迁移到你的目标嵌入式系统的根目录，并带有软链接树。如之前解释的那样，软链接消除了为每个命令输入 busybox 命令的需求。相反，要查看给定目录下的文件列表，用户只需输入 `ls`。软链接将如前所述执行 BusyBox 并调用 `ls` 功能。查看列表 11-4 和 11-5 以查看软链接树。注意，BusyBox 构建系统仅对你通过配置实用程序启用的功能创建链接。

向你的根文件系统填充必要的软链接群的最简单方法是让 BusyBox 构建系统为你完成工作。只需将你的根文件系统挂载到你的开发工作站上，并将 `CONFIG_PREFIX` 传递给 BusyBox make 文件。

### 列表 11-9 在根文件系统上安装 BusyBox

```bash
$ mount -o loop brootfs.ext2 /mnt/remote
$ make CONFIG_PREFIX=/mnt/remote install
 /mnt/remote/bin/ash -> busybox
 /mnt/remote/bin/cat -> busybox
 /mnt/remote/bin/chgrp -> busybox
 /mnt/remote/bin/chmod -> busybox
 /mnt/remote/bin/chown -> busybox

 /mnt/remote/usr/bin/xargs -> ../../bin/busybox
 /mnt/remote/usr/bin/yes -> ../../bin/busybox
 /mnt/remote/usr/bin/sh -> ../../bin/busybox
```

你可能需要将你的 busybox 二进制文件设置为 setuid root 以确保所有配置的 applet 正常工作。

```bash
$ chmod +s /mnt/remote/bin/busybox
$ ls -l /mnt/remote/bin/busybox
-rws-sr-x 1 root 552132 ... /mnt/remote/bin/busybox
```

首先，我们将根文件系统镜像挂载到我们指定的挂载点——在本例中为 `/mnt/remote`。然后向 BusyBox makefile 传递 `CONFIG_PREFIX`，指定我们希望 BusyBox 可执行文件和软链接树放置的位置。该脚本非常详细，它会为每个创建的软链接输出一行。为了简短，列表 11-9 只显示了开头和结尾。省略号代表被省略的内容。

安装脚本还会显示关于 setuid 的消息，提醒你可能需要让 BusyBox 可执行文件设置为 root。这允许由 root 用户调用的 BusyBox 函数正常工作。这并不是绝对必要的，特别是在只有一个 root 账户的嵌入式环境中。如果你的安装需要，列表 11-9 显示了所需的命令 `chmod +s`。

此安装步骤是在文件系统中得到的结果。

有用的是，BusyBox 还具有一个在运行时目标系统上创建此软链接树的选项。该选项在 BusyBox 配置中启用，并通过带有 `-install` 选项的运行时调用。你必须将 `/proc` 文件系统挂载到目标系统，该功能才能工作。

## 11.3.4 BusyBox Applet

在最近的 BusyBox 快照中，282 个命令（也称为 applet）在 man 页面中有记录。对于复杂的 shell 脚本提供了足够的支持，包括对 Bash shell 脚本的支持。BusyBox 支持 `awk` 和 `sed`，这些频繁出现在 Bash 脚本中。BusyBox 支持网络实用程序如 `ping`、`ifconfig`、`traceroute` 和 `netstat`。某些命令专门为脚本支持而包含，包括 `true`、`false` 和 `yes`。

> 花几分钟浏览附录 C.，“BusyBox 命令”，在其中你可以找到每个 BusyBox 命令的摘要。完成后，你将更好地理解 BusyBox 的功能以及它如何适用于你自己的嵌入式 Linux 项目。

正如本章开头提到的，与全功能版本相比，许多 BusyBox 命令包含的功能和选项是有限的。通常，你可以通过运行带有 `--help` 选项的命令在运行时获取任何给定 BusyBox 命令的帮助。这将产生一条用法消息，并对每个支持的命令选项进行简要描述。BusyBox `gzip` applet 是一个支持有限选项的 BusyBox 命令的有用示例。列表 11-10 显示了在 BusyBox 目标上执行 `gzip --help` 的输出。

## 11.4 总结

### 列表 11-10 BusyBox gzip Applet 使用

```
# gzip --help
BusyBox v1.13.2 (2010-02-24 16:04:14 EST) multi-call binary

Usage: gzip [OPTION]... [FILE]...

Compress FILEs (or standard input)

Options:
  -c    Write to standard output
  -d    Decompress
  -f    Force
```
