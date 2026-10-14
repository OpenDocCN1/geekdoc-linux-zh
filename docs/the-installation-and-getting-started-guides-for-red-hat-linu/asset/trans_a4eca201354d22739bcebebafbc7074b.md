

## /etc 目录

/etc 目录保留用于本地于本机的配置文件。/etc 中不应放置二进制文件。过去放在 /etc 中的二进制文件现在应放入 /sbin 或可能是 /bin。X11 和 skel 目录应为 /etc 的子目录：

```
/etc |- X11 +- skel
```

X11 目录用于 X11 配置文件，如 XF86Config。skel 目录用于“骨架”用户文件，这些文件在用户首次创建时用于填充其主目录。

## /lib 目录

/lib 目录应仅包含执行 /bin 和 /sbin 中的二进制文件所需的库。

## /proc 目录

/proc 目录包含特殊文件，这些文件要么提取信息要么向内核发送信息。它是使用 cat 命令访问操作系统信息的一种简便方法。

## /sbin 目录

/sbin 目录用于仅 root 用户使用的可执行文件，且仅限于启动和挂载 /usr 并执行系统恢复操作所需的那些可执行文件。FSSTND 说：

> "/sbin 通常包含启动系统所需的文件，除 /bin 中的二进制文件外。/usr 已知已挂载后执行的任何内容（当没有问题时）应放置在 /usr/sbin 中。仅本地使用的系统管理二进制文件应放置到 /usr/local/sbin。"

至少，以下程序应位于 /sbin 中：

```
clock, getty, init, update, mkswap, swapon, swapoff, halt, reboot, shutdown, fdisk, fsck.*, mkfs.*, lilo, arp, ifconfig, route
```

## /usr 目录

/usr 目录用于可在整个站点共享的文件。/usr 目录通常有自己的分区，并且应可只读挂载。以下目录应为 /usr 的子目录：

```
usr
  |- X11R6
  |- bin
  |- dict
  |- doc
  |- etc
  |- games
  |- include
  |- info
  |- lib
  |- local
  |- man
  |- sbin
  |- share
  +- src
```

X11R6 目录用于 X Window System（Red Hat Linux 上的 XFree86），bin 用于可执行文件，doc 用于随机非手册页文档，etc 用于全站配置文件，include 用于 C 头文件，info 用于 GNU info 文件，lib 用于库，man 用于手册页，sbin 用于系统管理二进制文件（不属于 /sbin 的），src 用于源代码。

## /usr/local 目录

FSSTND 说：

> "/usr/local 层次结构供系统管理员在本地安装软件时使用。它需要在系统软件更新时免受覆盖。它可用于在多台机器间共享但不在 /usr 中找到的程序和数据。"

/usr/local 目录的结构与 /usr 目录相似。它具有以下子目录，其用途与 /usr 目录中的类似：

/usr/local
  |- bin
  |- doc
  |- etc
  |- games
  |- include
  |- info
  |- lib
  |- man
  |- sbin
  +- src

## /var 目录

由于 FSSTND 要求你能够只读挂载 /usr，任何写入日志文件或需要 spool 或 lock 目录的程序可能应将它们写入 /var 目录。FSSTND 声明“/var 用于...可变数据文件。这包括 spool 目录和文件、管理及日志数据，以及临时和临时文件。”以下目录应为 /var 的子目录：

+   /var
+     |- log
+     |- catman
+     |- lib
+     |- local
+     |- named
+     |- nis
+     |- preserve
+     |- run
+     |- lock
+     |- tmp
+     +- spool
+       |- at
+       |- cron
+       |- lpd
+       |- mail
+       |- mqueue
+       |- rwho
+       |- small
+       |- uucp
+       +- news

系统日志文件如 wtmp 和 lastlog 放在 /var/log 中。/var/lib 目录还包含 RPM 系统数据库。格式化的手册页放在 /var/catman 中，锁文件放在 /var/lock 中。/var/spool 目录具有各种需要存储数据文件的系统的子目录。

