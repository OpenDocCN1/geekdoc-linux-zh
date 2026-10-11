

$ sum d * h* i* s*
43651  1 diskstuff
37612  5 hardlink
37612  5 inodes
37612  5 symlink

你可以轻松编写一个脚本，比较关键文件的校验和，以查看是否有人访问过它们。如果有输出，说明这些文件已被访问过。

```shell
#!/bin/sh
# compare checksums of the files in the /etc directory from yesterday
# move the previous day's checksum data to yesterdaysum
mv todaysum yesterdaysum
sum /etc/* > todaysum
diff yesterdaysum todaysum
```

sum 命令无法处理目录。尝试在目录上运行该命令时，查看会发生什么。

```shell
$ sum more*
sum: moreinfo: Is a directory
sum: morestuff: Is a directory
```

## file 命令

要查看目录中文件类型，请使用 file 命令。从下面的 file 命令输出中可以看出，硬链接与 inode 文件之间没有差异。但是，你可以区分目录、文本文件和符号链接。

```shell
$ file *
diskstuff: ASCII text
hardlink: English text
inodes: English text
moreinfo: directory
morestuff: directory
symlink: symbolic link to inodes
```

这是来自 / 目录的另一个示例。你可以看到 /tmp 目录设置了粘性位（sticky bit），这允许其他用户向其写入数据。你还可以看到内核文件；它们被识别为 x86 引导扇区文件。

```shell
$ file /*
/bin: directory
/boot: directory
/bzImage: x86 boot sector
/cdrom: directory
/dev: directory
/etc: directory
/home: directory
/lib: directory
/lost+found: directory
/mnt: directory
/proc: directory
/root: directory
/sbin: directory
/shlib: directory
/tmp: sticky directory
/usr: directory
/var: directory
/vmlinuz: x86 boot sector
```

以下是系统中可能遇到的其他一些文件类型：

```shell
/sbin/agetty: ELF 32-bit LSB executable, Intel 80386, version 1, dynamically linked, stripped
/sbin/explodepkg: Bourne shell script text
/sbin/fsck.ext2: symbolic link to e2fsck
/sbin/initscript.sample: English text
/dev/XOR: symbolic link to null
/dev/apm_bios: character special
/dev/aio: block special
/dev/beep: character special
/dev/cdrom: broken symbolic link to cdrom
/dev/gpmdata: fifo (named pipe)
/dev/hdd12: block special
/dev/lsdev: character special
/dev/printer: socket
```

## Slackware Linux 存放文件的位置

与其他 UNIX 系统一样，Slackware Linux 将目录和文件存储在一个层级结构中。该层级结构以根目录 / 开头。在根目录中，有文件和子目录。以下列表显示了根目录中的目录。

```shell
$ ls -ld /*
drwxr-xr-x    2 root     bin        2048 Aug  6 03:53 /bin
drwxr-xr-x    2 root     root       1024 Aug  6 11:39 /boot
drwxr-xr-x   3 root     root       25600 Aug  6 19:05 /dev
drwxr-xr-x  10 root     root       2048 Aug  6 19:05 /etc
drwxr-xr-x   4 root     root       1024 Aug  6 15:28 /home
drwxr-xr-x   3 root     root       2048 Aug  6 03:51 /lib
drwxr-xr-x   2 root     root      12288 Aug  6 03:36 /lost+found
drwxr-xr-x   2 root     root       1024 Oct  6  1997 /mnt
dr-xr-xr-x   5 root     root          0 Aug  6 12:04 /proc
drwx--x--    3 root     root       1024 Aug  6 11:39 /root
drwxr-xr-x   2 root     bin        2048 Aug  6 03:53 /sbin
drwxr-xr-x   2 root     root       1024 Apr 27  1996 /shlib
drwxrwxrwt   3 root     root       1024 Aug  6 22:20 /tmp
drwxr-xr-x  23 root     root       1024 Jun  8  1994 /usr
drwxr-xr-x  16 root     root       1024 Jun  8  1994 /var
```

/bin 中包含操作系统的主要二进制文件。这些包括但不限于 cd、ls、rm、cat、ftp、login、mail、ln、kill、pwd 以及用户 shell（bash、csh、zsh 等）。/sbin 目录包含系统管理员使用的二进制文件。这些包括 cardmgr、fdisk、halt、kernel、liio、mkfs 和 sologin。

/boot 中包含各种用于 LOADLlO 或 LILO 的文件，以启用启动功能。

你的设备，包括鼠标和终端，都保存在 /dev 中。这是设备目录。它还包括调制解调器、打印机、硬盘以及连接到计算机的任何其他设备。

/etc 目录是所有系统所需但确切归属不明的文件的杂项目录。/etc 目录最初可能是这样形成的——但现在它被期望包含某些特定文件，例如 /etc/hosts 和 /etc/services。

/etc 中有一些重要的子目录。它们包括 pcmcia、ppp、rc.d（包含启动和关闭脚本）、slip 以及 skel（包含在创建用户主目录时复制到其中的文件）。

用户的主目录默认为 /home。但是，如果你愿意，可以设置自己的目录来存储用户帐户。root 帐户的主目录是 /root。

系统库存储在 /lib 中。这些是 32 位 ELF 共享对象或 ELF 32 位可执行文件。还有 /lib/modules 目录，用于存储内核模块的目标文件。/shlib 目录用于 SCO 兼容文件。

/lost+found 目录是系统发送那些有数据但没有所属目录的 inode 的地方。这可能是由磁盘崩溃或系统突然关机引起的。

/mnt 和 /tmp 目录是临时目录。/mnt 目录是一个临时挂载点目录。/tmp 目录是临时文件存储区，特别是在启用了磁盘配额且用户临时需要磁盘空间时。/proc 目录用于启用文件系统进程。这些包括磁盘 I/O 进程、内存和 CPU 访问。

/usr 目录主要包含本地程序和文件。/usr 目录包含指向其他目录或子目录的链接。/usr/X11 和 /usr/X11R6 包含 Xwindow 系统和文件。本地二进制文件位于 /usr/bin 和 /usr/local/bin 中。手册页存储在 /usr/man 中。/usr 目录中还存在许多其他文件；因此它占用了大量空间。

```shell
$ ls -ld /usr/*
lrwxrwxrwx    1 root     root            5 Aug  6 03:55 /usr/X11 -> X11R6
drwxr-xr-x    9 root     root          1024 Apr 27 1994 /usr/X11R6
lrwxrwxrwx    1 root     root            8 Aug  6 03:48 /usr/adm -> /var/adm
drwxr-xr-x    2 root     root          9216 Mar 23 12:33 /usr/bin
drwxr-xr-x    2 root     root          1024 Nov  25 1993 /usr/dict
drwxr-xr-x  116 root     root          3072 Jun  8 1994 /usr/doc
drwxr-xr-x    2 root     root          1024 Nov 25 1993 /usr/etc
drwxr-xr-x    4 root     root          1024 Jun  8 1994 /usr/games
lrwxrwxrwx    1 root     root            9 Aug  6 03:50 /usr/i486-coff -> ix86-coff
lrwxrwxrwx    1 root     root           10 Aug  6 03:50 /usr/i486-linux -> ix86-linux
lrwxrwxrwx    1 root     root           14 Aug  6 03:50 /usr/i486-linuxaout -> ix86-linuxaout
drwxr-xr-x    3 root     root          1024 Aug 13 1995 /usr/i486-sysv4
lrwxrwxrwx    1 root     root           10 Aug  6 03:51 /usr/i586-pc-linux-gnu/libc1 -> ix86-i5linux
drwxr-xr-x   20 root     root          3072 Aug  6 03:58 /usr/include
drwxr-xr-x    2 root     root          5120 Jun 20 1997 /usr/info
drwxr-xr-x    4 root     root          1024 Feb 20 22:01 /usr/ix86-coff
drwxr-xr-x    5 root     root          1024 May 15 17:15 /usr/ix86-linux
drwxr-xr-x    4 root     root          1024 Jun 11 1995 /usr/ix86-linuxaout
drwxr-xr-x   29 root     root          4096 Aug  6 03:58 /usr/lib
drwxr-xr-x    4 root     root          1024 Nov  4 1996 /usr/libexec
drwxr-xr-x   13 root     root          1024 Aug  6 03:57 /usr/local
drwxr-xr-x    2 root     root         12288 Aug  6 03:38 /usr/lost+found
drwxr-xr-x   13 root     root          1024 Jun  4 17:59 /usr/man
drwxr-xr-x    8 root     root          1024 May 26 1994 /usr/openwin
lrwxrwxrwx    1 root     root           13 Aug  6 03:48 /usr/preserve -> /var/preserve
drwxr-xr-x    3 root     bin           3072 Aug  6 03:53 /usr/sbin
drwxr-xr-x   10 root     root          1024 Feb 14 11:55 /usr/share
lrwxrwxrwx    1 root     root           10 Aug  6 03:48 /usr/spool -> /var/spool
drwxr-xr-x    3 root     root          1024 Aug  6 03:52 /usr/src
lrwxrwxrwx    1 root     root            8 Aug  6 03:48 /usr/tmp -> /var/tmp
```

/var 目录包含各种系统管理文件。这些包括日志文件、邮件、cron、打印和其他应用程序的 spool 目录。它还包含进程 ID 信息（/var/pid）和其他系统信息。

