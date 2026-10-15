

## 阅读文档

尽管本书教会了你使用 Ubuntu 的基础知识，但要掌握和排查 Linux 操作系统及其发行版的更复杂方面，你仍需要时间和实践。与任何操作系统一样，随着你继续使用 Linux，你可能会遇到一些问题或令人困惑的问题。寻求这些问题帮助的第一个地方是系统自带的文档；如果在那里找不到所需的信息，请查看 Ubuntu 的网站。

Linux 与 Unix 一样，是一个自文档化系统，可通过 man 命令访问手册页。Linux 还提供了许多其他有用的命令来访问其文档。你可以使用 apropos 命令——例如，使用 partition 这样的关键词——来查找与分区相关的命令，如下所示：

```
$ apropos partition
diskdumpfmt      (8) - format a dump device or a partition
fdisk            (8) - Partition table manipulator for Linux
GNU Parted [parted] (8) - a partition manipulation program
m partition       (1) - partition an MSDOS hard disk
MPI_Cart_sub     (3) - Partitions a communicator into subgroups which form lower-dimensional cartesian subgrids
partprobe        (8) - inform the OS of partition table changes
pvcreate         (8) - initialize a disk or partition for use by LVM
sfdisk           (8) - Partition table manipulator for Linux
```

要查找命令及其文档，你可以使用 whereis 命令。例如，如果你正在寻找 fdisk 命令，可以这样做：

```
$ whereis fdisk
fdisk: /sbin/fdisk /usr/share/man/man8/fdisk.8.gz
```

## 使用手册页

要了解有关某个命令或程序的更多信息，请使用 man 命令，后跟命令的名称。Linux 和 X Window 命令的手册页位于 /usr/share/man、/usr/local/share/man 和 /usr/X11R6/man 目录中；因此，例如，要阅读 rm 命令的手册页，请这样使用 man 命令：

```
$ man rm
```

按下 Enter 后，less 命令（一种被称为分页器的 Linux 命令）会显示手册页。less 命令是一个文本浏览器，你可以用它向前和向后（甚至左右）滚动文档以了解有关该命令的更多信息。输入字母 h 以获取帮助，使用正斜杠输入搜索字符串，或按 q 退出。

### NOTE

尽管 Linux 附带的数百个 GNU 命令几乎都有手册页，但你必须使用 info 命令来阅读有关如何使用 GNU 命令的详细信息。例如，要了解有关 bash 的更多信息（它有一个相当详尽的手册页），请这样使用 info 命令：

```
$ info bash
```

按 n 和 p 键在文档中导航，或向下滚动到屏幕上的菜单项并按 Enter 以阅读有关特定功能的介绍。按 q 退出阅读。

## 相关 Ubuntu 和 Linux 命令

以下程序和内置 shell 命令在命令行工作时常用。这些命令按类别组织，以帮助你理解命令的目的。如果需要查找使用命令的完整信息，可以在该命令的手册页下找到该信息。

- ► 管理用户和组 — chage, chfn, chsh, edquota, gpasswd, groupadd, groupdel, groupmod, groups, mkpasswd, newgrp, newusers, passwd, umask, useradd, userdel, usermod
- ► 管理文件和文件系统 — cat, cd, chattr, chmod, chown, compress, cp, dd, fdisk, find, gzip, ln, mkdir, mkfs, mount, mv, rm, rmdir, rpm, sort, swapoff, tar, touch, umount, uncompress, uniq, unzip, zip
- ► 管理运行中的程序 — bg, fg, kill, killall, nice, ps, pstree, renice, top, watch
- ► 获取信息 — apropos, cal, cat, cmp, date, diff, df, dir, dmesg, du, env, file, free, grep, head, info, last, less, locate, ls, lsattr, man, more, pinfo, ps, pwd, stat, strings, tac, tail, top, uname, uptime, vdir, vmstat, w, wc, whatis, whereis, which, who, whoami
- ► 控制台文本编辑器 — ed, jed, joe, mcedit, nano, red, sed, vim
- ► 控制台 Internet 和网络命令 — ping, elm, ftp, host, hostname, ifconfig, links, lynx, mail, mutt, ncftp, netconfig, netstat, pine, ping, pump, rdate, route, scp, sftp, ssh, tcpdump, traceroute, whois, wire-test

