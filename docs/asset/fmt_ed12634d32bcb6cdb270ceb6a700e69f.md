
Gentoo 团队还维护着名为 `Hardened Gentoo` 的子项目，该项目致力于将 `SELinux`、`RSBAC` 和 `PaX/Grsecurity` 等项目（我们稍后将讨论所有这些）集成到发行版中。

## Debian (http://www.debian.org)

Debian 面向经验丰富的 Linux 用户，它缺乏其他发行版的一些美观之处（例如，更倾向于基于文本的安装程序），但其卓越的稳定性声誉完全弥补了这一点。尽管这种稳定性是以操作系统不够尖端为代价的，但许多管理员认为这是一个可以接受的折中方案。Debian 的另一个流行特性是它的软件包系统 `Dpkg`，它允许用户毫不力地获取和安装二进制文件。由于 Debian 软件包由一个中央小组维护，它们往往具有良好的集成性，极少彼此之间产生冲突。

## Mandrake™ (http://www.linux-mandrake.com)

Mandrake 通过强调创建强大的 GUI 赢得了最易用发行版之一的声誉。尽管这让它在家庭桌面用户（Mandrake 的目标受众）中拥有了庞大的粉丝群，但在没有安装 `X Windows` 的服务器上运行时，GUI 几乎没有用处。Mandrake 还倾向于向用户隐藏系统的内部运行机制。简而言之，它对于经验较少的家庭用户非常优秀，但不特别适用于服务器环境。

# 专用发行版

Linux 存在针对各种任务的专用发行版，但我们的重点是针对服务器市场的那些（这通常意味着对安全更高的关注）。这些安全发行版提供的多数功能都是开源的，并且可以同样轻松安装在任何其他版本的 Linux 上——你（在大多数情况下）不会因为其提供的功能而被绑定到特定的发行版。

## Openwall Linux (http://www.openwall.com)

Openwall Linux 并没有重点放在新技术上（正如漏洞本身可能是新的来源），它专注于通过安全的默认配置和主动性的代码审查来加固现有应用程序。

# Linux 网络安全

正如我们在第 2 章所看到的，不安全的服务是攻击者的常见点，允许他们以运行服务的用户权限在系统中执行命令。在许多情况下，这会导致攻击者获得 `root` 权限。

## SmoothWall Express® (http://www.smoothwall.org)

面向那些希望快速安装防火墙/路由器且不需要 Linux 知识的新用户，SmoothWall Express 是 Debian 的一个加固版本。系统的管理通过 Web 界面进行，且不需要预先的 Linux 知识。

## Adamantix (http://www.adamantix.org)

曾名为 `Trusted Debian`（由于商标问题更改了名称），Adamantix 本质上是 Debian 的加固版本，将 `RSBAC`（基于规则的访问控制）深度集成到系统中。其他功能包括通过 `PaX` 进行缓冲区溢出保护、磁盘分区加密以及内置病毒扫描。

## 8.2 chroot 环境

理想情况下，服务应该在沙箱环境中运行，限制它们可以的操作以及与系统其他部分的交互；这正是 `chroot` 所提供的。

正如其名所示，`chroot` 了进程对根目录（通常为 `/`）的视角；这是进程无法访问根之外任何区域的最高层级。本节涵盖了 `chroot` 监狱的理论；在第 10 章，我们将涵盖 `Apache` 和 `BIND` 等常用服务的实用方面。

`chroot` 监狱最常见的用途之一是匿名 FTP 服务器。允许匿名用户远程访问整个文件系统是不可思议的；相反，你希望将其限制在它的特定部分——最常见的 `/var/ftp/`。FTP 通过在匿名用户登录后立即执行 `chroot()` 系统调用来实现这一点，随后通过 `chdir()` 将其放入新定义的根。

## 系统加固 295

图 8.1 显示了典型 FTP 服务器上的文件系统部分，其中阴影区域代表匿名用户在机器上的范围。对于他来说，`/var/ftp` 看起来就像 `/`，而 `/var/ftp/bin` 看起来就像 `/bin`。

![](img/d90c7093221fd011adff06e7e1ff1ccd_314_0.png)

**图 8.1** 匿名 FTP 服务器文件系统的横截面。

## 监狱构建

`chroot` 监狱的一个重要后果是，被禁进程所需的任何文件（无论是普通文件还是设备）必须存在于监狱内部。参考之前的 FTP 示例，我们看到标准文件的一部分（非常小的一部分）被镜像到监狱中，包含了 `bin`、`lib` 和等 目录：

## 296 Linux 网络安全

```
# ls -1 /var/ftp/bin
total 364
-r--      1 root root       31 May  6 2003 bin.md5
-rwxr-xr-x 2 root root       19016 Feb 27 2002 compress
-rwxr-xr-X 2 root root.      64705 Feb 28 2002 cpio
-rwxr-xr-X 4 root root       63555 Mar 13 2002 gzip
-rwxr-xr-X 2 root root       46888 Jan 19 2003 ls
-rwxr-xr-X 2 root root     155560 Sep 10 2002 tar
lrwxrwxrw 1 root root             4 Jun 15 2003 zcat -> gzip
```

```
# ls -1 /var/ftp/lib
total 1484
-rwxr-xr-x 2 root root       89547 Mar  5 2003 ld-2.2.5.so
lrwxrwxrw 1 root root              11 Jun 15 2003 ld-linux.so--> id-2.2.5.so
-rwxr-xr-x 2 root root     126048 Mar  5 2003 libc-2.2.5.so
lrwxrwxrw 1 root root              13 Jun 15 2003 libdoc.so.6 -> libc-2.2.5.so
-rwxr-xr-x 2 root root       89424 Mar  5 2003 libns1-2.2.5.so
lrwxrwxrw 1 root root             15 Jun 15 2003 libns1.so.1 -> libns1-2.2.5.so
-rwxr-xr-x 2 root root       45415 Mar  5 2003 libns_files-2.2.5.so
lrwxrwxrw 1 root root             21 Jun 15 2003 libns_files.so.2 -> libns_files-2.2.5.so
-r--      1 root root             260 May  5 2003 libs.md5
lrwxrwxrw 1 root root             19 Jun 15 2003 libtermcap.so -2 -> libtermcap.so
# ls -1 /var/ftp/etc
total 12
-r--r--r-- 1 root root       53 Aug 22 2001 group
-rwxr-r--r-- 1 root root       409 May  5 2003 ld.so.cache
-rwxr-r--r-- 1 root root               0 May  5 2003 ld.so.conf
-r--r--r-- 1 root root               79 Aug 22 2001 passwd
```

### 发现库依赖

创建这个精简文件系统（`minifiles system`）简单；困难的部分在于确定需要哪些文件。我们将介绍的发现依赖的第一种方法是 `ldd` 命令，它显示给定文件的共享库依赖项：

```
$ ldd /bin/ls
librt.so.1 => /lib/librt.so.1 (0x40029000)
libc.so.6 => /lib/libc.so.6 (0x4003c000)
libthread.so.0 => /lib/libthread.so.0 (0x40172000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

从此可以看出，`ls` 命令在监狱（`jail`）中运行需要这四个库的存在。

### Strace

当然，库并不是进程可能需要访问的所有文件，这使得 `ldd` 的用途有限。确定所有依赖项的最有用方法之一是 `strace` 工具，它会列出进程执行的系统调用，因此包含了所有的文件操作。

要使用 `strace`，只需将要监控的应用程序名称作为参数执行它；`strace` 将显示该应用程序执行的所有系统调用，直到执行自然结束，或者通过 `Ctrl-D` 停止它：
