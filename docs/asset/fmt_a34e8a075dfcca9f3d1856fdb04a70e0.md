
```
[rootserver1]# cat /etc/dumpdates
/dev/hda2 0 Sat Jul 23 16:43:09 2005
[rootserver1]# _
```

要执行首次增量备份并查看 `/etc/dumpdates` 文件的内容，你可以在 SCSI 驱动器中放入一条新磁带并执行以下命令：

```
[rootserver1]# dump -luf /dev/st0 /dev/hda2
DUMP: Date of this level 1 dump: Sat Jul 23 16:50:57 2005
DUMP: Date of last level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Dumping /dev/hda2 (/boot) to /dev/st0
DUMP: Exclude ext3 journal inode 8
DUMP: Label: /boot
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 21 tape blocks.
DUMP: Volume 1 started with block 1 at: Sat Jul 23 16:50:58 2005
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/st0
DUMP: Volume 1 completed at: Sat Jul 23 16:50:58 2005
DUMP: Volume 1: 20 tape blocks (0.02MB)
DUMP: 20 tape blocks (0.02MB) on 1 volume(s)
DUMP finished in less than a second
DUMP: Date of this level 1 dump: Sat Jul 23 16:50:57 2005
DUMP: Date of this dump completed: Sat Jul 23 16:50:58 2005
DUMP: Average transfer rate: 0 kB/s
DUMP: IS DONE
```

```
[rootserver1]# cat /etc/dumpdates
/dev/hda2 0 Sat Jul 23 16:43:09 2005
/dev/hda2 1 Sat Jul 23 16:50:57 2005
[rootserver1]# _
```

要查看归档的内容，你可以在 `restore` 命令中指定 `-t` 选项并后跟归档信息。要查看之前执行的全备份内容，你可以将相应的磁带放入磁带驱动器并执行以下命令：

```
[rootserver1]# restore -tf /dev/st0
Dump: Date: Sat Jul 23 16:43:09 2005
Dumped from: the epoch
Level 0 dump of /boot on localhost.localdomain:/dev/hda2
Label: /boot
2
11
./root+found
4033 /grub
4035 /grub/grub.conf
4034 /grub/splash.xpm
```

```
4036 /grub/menu.lst
4037 /grub/device.map
4038 /grub/stagel
4039 /grub/stage2
4040 /grub/e2fs_stage1_5
4041 /grub/fat_stage1_5
4042 /grub/ffs_stage1_5
4043 /grub/reiserfs_stage1_5
4044 /grub/vstafs_stage1_5
4045 /grub/xfs_stage1_5
12 /boot.b
13 /chain.b
14 /config-2.6.5-1.358
15 /init2rd-2.6.5-1.358.img
17 /memtest86+-1.11
19 /os2_d.b
22 /System.map-2.6.5-1.358
20 /vmlinuz-2.6.5-1.358
```

要提取上述输出中显示的全备份，你可以在 `restore` 命令中指定 `-r` 选项并后跟归档信息。此外，你可以指定 `-v` 选项来列出恢复的文件名，如下所示：

```
[root@server1 ~]# restore -vrf /dev/st0
Verify tape and initialize maps
Input from file/pipe
Input block size is 32
Dump date: Sat Jul 23 16:43:09 2005
Dumped from: the epoch
Level 0 of /boot on localhost.local:/dev/hda2
Label: /boot
Begin level 0 restore
Initialize symbol table.
Extract directories from tape
Calculate extraction list.
restore: /lost-found: File exists
restore: ./grub: File exists
Extract new leaves.
Check pointing to the restore file
extract file /boot.b
extract file /chain.b
extract file /config-2.6.5-1.358
extract file /init2rd-2.6.5-1.358.img
extract file /memtest86+-1.11
extract file /os2_d.b
extract file /System.map-2.6.5-1.358
extract file /vmlinuz-2.6.5-1.358
extract file /grub/grub.conf
extract file /grub/splash.xpm
```

```
extract file ./grub/menu.lst
extract file ./grub/device.map
extract file ./grub/stage1
extract file ./grub/stage2
extract file ./grub/e2fs_stage1_5
extract file ./grub/fat_stage1_5
extract file ./grub/ffs_stage1_5
extract file ./grub/reiserfs_stage1_5
extract file ./grub/vstafs_stage1_5
extract file ./grub/xfs_stage1_5
```

## 源码编译程序

将源码编译为二进制程序的方法在 Linux 系统中是标准化的。源码通常以 tar 格式提供，你必须先解压并提取文件。这会在当前目录下创建一个包含源码的目录。此外，该目录通常包含一个关于程序的 README 文件和一个包含安装说明的 INSTALL 文件。

在源码目录内，安装的第一步是运行 `configure` 程序。它会执行系统要求的初步检查，并在当前目录下创建一个名为 `Makefile` 的文件。接下来，你可以输入 `make` 命令，它会查找 `Makefile` 并使用其中的信息通过 GNU 编译器 `gcc` 将源码编译为二进制程序。编译完成后，二进制文件仍存储在源码目录中。要将文件复制到文件系统的相应位置，例如 `PATH` 变量列出的目录，你必须输入 `make install`。

> 大多数 Linux 程序安装在 `/usr/local` 目录下。

在程序被编译并复制到文件系统的正确位置后，源码目录及其内容可以从系统中删除。

假设，你从网上下载了 rdesktop（远程桌面协议客户端）1.3.1 源码。

```
[server1 root]# ls -F
Desktop/  rdesktop-1.3.1.tar.gz
[server1 root]#
```

安装此程序的第一步是解压并提取 tar 包，如下输出所示。这将创建一个名为 `rdesktop-1.3.1` 的目录，其中包含源码和支持文件。

```
[server1 root]# tar -xvf rdesktop-1.3.1.tar.gz
rdesktop-1.3.1/COPYING
desktop-1.3.1/README
desktop-1.3.1/configure
desktop-1.3.1/Makefile
desktop-1.3.1/spec
desktop-1.3.1/bitmap.c
desktop-1.3.1/cache.c
desktop-1.3.1/channels.c
desktop-1.3.1/clipdr.c
```

# 软件安装

```
rdesktop-1.3.1/ewmhints.c
rdesktop-1.3.1/iso.c
rdesktop-1.3.1/licence.c
rdesktop-1.3.1/mcs.c
rdesktop-1.3.1/orders.c
rdesktop-1.3.1/printer.c
rdesktop-1.3.1/rdesktop.c
desktop-1.3.1/rdp.c
desktop-1.3.1/rdp5.c
desktop-1.3.1/rdpdr.c
desktop-1.3.1/rdpsnd.c
desktop-1.3.1/rdpsnd_oss.c
desktop-1.3.1/rdpsnd_sun.c
desktop-1.3.1/secure.c
desktop-1.3.1/serial.c
desktop-1.3.1/tcp.c
desktop-1.3.1/xclip.c
desktop-1.3.1/xkeymap.c
desktop-1.3.1/xwin.c
desktop-1.3.1/constants.h
desktop-1.3.1/orders.h
desktop-1.3.1/parse.h
rdesktop-1.3.1/proto.h
rdesktop-1.3.1/rdesktop.h
desktop-1.3.1/scancodes.h
desktop-1.3.1/types.h
desktop-1.3.1/xproto.h
desktop-1.3.1/crypto/md32_common.h
rdesktop-1.3.1/crypto/md5.h
rdesktop-1.3.1/crypto/md5_locl.h
rdesktop-1.3.1/crypto/rc4.h
rdesktop-1.3.1/crypto/sha.h
rdesktop-1.3.1/crypto/sha_locl.h
rdesktop-1.3.1/keymaps/common
desktop-1.3.1/keymaps/modifiers
desktop-1.3.1/keymaps/convert-map
desktop-1.3.1/doc/HACKING
desktop-1.3.1/doc/AUTHORS
desktop-1.3.1/doc/ChangeLog
desktop-1.3.1/doc/keymapping.txt
desktop-1.3.1/doc/keymap-names.txt
desktop-1.3.1/doc/ipv6.txt
rdesktop-1.3.1/doc/rdesktop.1
[root@server1]#
```

接下来，你可以进入该目录并查看文件内容，输出输出所示：

## 第 12 章 root、系统备份与软件安装

```
[root@server1]# cd rdesktop-1.3.1
[root@server1] rdesktop-1.3.1]# ls -F
bitmap.c      crypto/      mcs.c       rdesktop.h    rdpsnd_sun.c  xclip.c
cache.c       doc/        orders.c    rdesktop.spec README      xkeymap.c
channels      ewhmins.c  orders.h    rdp5.c       scancodes.h  proto.h
cliprdr.c                   parse       rdp.c        secure.c     xwin.c
configure*    keymaps/    printer.c    rdpdr.c      serial.c
constants.h  license.c   proto.h     rdpsnd.c      tcp.c
COPYING                      Makefile     rdesktop.c  rdpsnd_oss.c types.h
[root@server1 rdesktop-1.3.1]# _
```

从上一个输出可以看出，README 和 `configure` 文件是可执行的。要在不使用 `PATH` 变量的情况下执行此文件，你可以输入以下命令：

```
[root@server1 rdesktop-1.3.1]# /configure
rdesktop configuration script
```

X Window System:

includes /usr/X11R/include

libraries /usr/X11R/lib

OpenSSL:

includes /usr/include

libraries /usr/lib

Sound support enabled: Open Sound System

```
configure complete - now run make
[root@server1 rdesktop-1.3.1]# _
```

运行 `configure` 脚本后，当前目录下会存在一个 `Makefile`，输出如下：

```
[root@server1 rdesktop-1.3.1]# cat Makefile
# rdesktop: 一个远程桌面协议客户端
# Makefile
# Copyright (C) Matthew Chapman 1999-2004
# Configuration defaults
prefix = /usr/local
exec_prefix = $(exec_prefix)/bin
bindir = $(exec_prefix)/bin
mandir = $(prefix)/man
datadir = $(prefix)/share/rdesktop
VERSION = 1.3.1
KEYMAP_PATH = $(datadir)/keymaps/
```

RDPOBJ = tcp.o mcs secure licence rdp orders.o bitmap cache.o md5.o channels.o rdpdr.o serial.o printer.o

X11OBJ = rdesktop.o xwin.o xkeymap.o ewhmints.o xclip.o cliprdr.o

VNCOBJ = vnc/rdp2vnc.o vnc/xkeymap.o vnc/x1ll.o

```

## 550 第 12 章 压缩、系统备份与软件安装

```bash

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o mcs.o -cc mcs.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o secure.o -cc secure.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o licence.o -cc licence.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o rdp.o -cc rdp.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o orders.o -cc orders.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o bitmap.o -cc bitmap.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o cache.o -cc cache.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o rdp5.o -cc rdp5.c
```
