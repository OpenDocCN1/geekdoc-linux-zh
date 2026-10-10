

例如，假设你从 Internet 上的 www.sourceforge.net 下载了 rdesktop（远程桌面协议客户端）版本 1.8.2 的源代码：

```
[root@server1 ~]# ls -f
Desktop/ rdesktop-1.8.2.tar.gz
[root@server1 ~]# _
```

安装此程序的第一步是解压并提取 tarball，如下面的输出所示。这将创建一个名为 rdesktop-1.8.2 的目录，其中包含源代码和支持文件。

```
[root@server1 ~]# tar -zxvf rdesktop-1.8.2.tar.gz
rdesktop-1.8.2/COPYING
rdesktop-1.8.2/README
rdesktop-1.8.2/configure
rdesktop-1.8.2/configure.ac
rdesktop-1.8.2/config.sub
rdesktop-1.8.2/config.guess
rdesktop-1.8.2/bootstrap
rdesktop-1.8.2/install-sh
rdesktop-1.8.2/Makefile.in
rdesktop-1.8.2/rdesktop.spec
rdesktop-1.8.2/asn.c
rdesktop-1.8.2/bitmap.c
rdesktop-1.8.2/cache.c
rdesktop-1.8.2/channels.c
rdesktop-1.8.2/cliprdr.c
rdesktop-1.8.2/cssp.c
rdesktop-1.8.2/ctrl.c
rdesktop-1.8.2/disk.c
rdesktop-1.8.2/ewmhints.c
rdesktop-1.8.2/iso.c
rdesktop-1.8.2/licence.c
rdesktop-1.8.2/lspci.c
rdesktop-1.8.2/mcs.c
rdesktop-1.8.2/mppe.c
rdesktop-1.8.2/orders.c
rdesktop-1.8.2/parallel.c
rdesktop-1.8.2/printer.c
rdesktop-1.8.2/printer/cache.c
rdesktop-1.8.2/pskcache.c
rdesktop-1.8.2/rdesktop.c
rdesktop-1.8.2/rdp5.c
rdesktop-1.8.2/rdp.c
rdesktop-1.8.2/rdpdr.c
rdesktop-1.8.2/rdpsnd_alSa.c
rdesktop-1.8.2/rdpsnd.c
rdesktop-1.8.2/rdpsnd_disp.c
rdesktop-1.8.2/rdpsnd_libao.c
rdesktop-1.8.2/rdpsnd_oss.c
rdesktop-1.8.2/rdpsnd_sgi.c
rdesktop-1.8.2/rdpsnd_sun.c
rdesktop-1.8.2/scard.c
rdesktop-1.8.2/sc.c
rdesktop-1.8.2/seamless.c
rdesktop-1.8.2/secure.c
rdesktop-1.8.2/serial.c
rdesktop-1.8.2/ss1.c
rdesktop-1.8.2/tcp.c
rdesktop-1.8.2/utils.c
rdesktop-1.8.2/xclip.c
rdesktop-1.8.2/xkeymap.c
rdesktop-1.8.2/xwin.c
rdesktop-1.8.2/constants.h
rdesktop-1.8.2/disk.h
rdesktop-1.8.2/orders.h
rdesktop-1.8.2/parse.h
rdesktop-1.8.2/proto.h
rdesktop-1.8.2/rdesktop.h
rdesktop-1.8.2/rdpsnd_dsp.h
rdesktop-1.8.2/rdpsnd.h
rdesktop-1.8.2/scancodes.h
rdesktop-1.8.2/scard.h
rdesktop-1.8.2/seamless.h
rdesktop-1.8.2/ss1.h
rdesktop-1.8.2/types.h
rdesktop-1.8.2/xproto.h
rdesktop-1.8.2/proto.head
rdesktop-1.8.2/proto.tail

<Additional contents omitted here>

rdesktop-1.8.2/doc/HACKING
rdesktop-1.8.2/doc/AUTHORS
rdesktop-1.8.2/doc/TODO
rdesktop-1.8.2/doc/ChangeLog
rdesktop-1.8.2/doc/keymapping.txt
rdesktop-1.8.2/doc/keymap-names.txt
rdesktop-1.8.2/doc/ipv6.txt
rdesktop-1.8.2/doc/licensing.txt
rdesktop-1.8.2/doc/patches.txt
rdesktop-1.8.2/doc/redirection.txt
rdesktop-1.8.2/doc/rdesktop.1
[root@server1 ~]# _
```

接下来，你可以移动到该目录并查看文件内容，如下面的输出所示：

```
[root@server1 ~]# cd rdesktop-1.8.2
[root@server1 rdesktop-1.8.2]# ls -F
asn.c           disk.c          parallel.c      rdpsnd_alsa.c   seamless.c
bitmap.c        disph.h         parse.h         rdpsnd.c        seamless.h
bootstraps*     doc/            printer.c       rdpsnd_dsp.c    secure.c
cache.c         evmhints.c      printercache.c  rdpsnd_dsp.h    serial.c
channels.c      install.sh*     proto.h         rdpsnd.h        ssl.c
cliprdr.c       iso.c           proto.head      rdpsnd_libao.c  csli.h
config_gucess*  keymaps/        proto.tail      rdpsnd_oss.c    tcp.c
config_sub*     license.c       pscatcache.c    rdpsnd_ssh.c    types.c
configure*      lspeci.c        rdesktop.c      rdpsnd_sun.c    utils.c
configure.ac    Makefile.in     rdesktop.h      README          xclip.c
constants.h     mcs.c          rdesktop.spec   scandodes.h     xkeymap.h
COPYING         mppe.c         rdp5.c         scard.c         xproto.h
cssp.c          orders.c      rdp.c          scard.h         xwin.c
ctrl.c          orders.h      rdrp.c         sc.c
css.h           rdp9.h        sc.h
[root@server1 rdesktop-1.8.2]# _
```

在上面的输出中，你可以看到存在 README 和 configure 文件，并且 configure 文件是可执行的。要执行 configure 文件而不使用 PATH 变量，你可以输入以下命令：

```
[root@server1 rdesktop-1.8.2]# ./configure
checking build system type... x86_64-redhat-linux-gnu
checking host system type... x86_64-redhat-linux-gnu
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking for a BSD-compatible install... /usr/bin/install -c
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking whether byte ordering is bigendian... no
checking for X11 libraries, headers
checking for gethostbyname... yes
checking for connect... yes
checking for remove... yes
checking for shmat... yes
checking for IceConnectionNumber in -lICE... no
checking for pkg-config... /usr/bin/pkg-config
checking for library containing socket... none required
checking for library containing inet_aton... none required
checking sys/select.h usability... yes
checking sys/select.h presence... yes

<Additional checks omitted here>

checking for struct statvfs.f namemax... yes
checking for struct statfs.f namelen... yes
checking for struct statvfs.f namelen... no
checking for special C compiler options needed for large files... no
checking for _FILE_OFFSET_BITS value needed for large files... no
checking mntent.h usability... yes
checking mntent.h presence... yes
checking for mntent.h... yes
checking for setmntent... yes
configure: creating ./config.status
config.status: creating Makefile
[root@server1 rdesktop-1.8.2]# 
```

在 configure 脚本运行后，当前目录中存在一个 Makefile，如下面的输出所示：

```
[root@server1 rdesktop-1.8.2]# head Makefile
#
# rdesktop: A Remote Desktop Protocol client
# Makefile.in
# Copyright (C) Matthew Chapman 1999-2007
#
prefix = /usr/local
exec_prefix = ${prefix}
bindir = ${exec_prefix}/bin
mandir = ${datarootdir}/man
[root@server1 rdesktop-1.8.2]# 
```

该 Makefile 包含了编译程序所需的大部分信息和命令。你下载的一些程序源代码可能包含注释行，你需要取消这些行的注释以启用程序的某些功能，或允许程序在你的计算机架构上编译。这些注释区域的说明记录在 Makefile 本身中；因此，在运行 configure 脚本后阅读 Makefile 是一种好习惯。如果你想要更改程序安装的目的地，也可以编辑 Makefile。对于 rdesktop，只需将上面输出中显示的 `prefix=/usr/local` 行更改为反映新目录。

接下来，你必须在源代码目录中输入 `make` 命令，根据存储在 Makefile 中的设置来编译程序。这将使用 `gcc` 程序编译源代码文件，如下面的输出所示：

```
[root@server1 rdesktop-1.8.2]# make
gcc -g -O2 -Wall -I/usr/include -I/usr/include/alsa \
-DPACKAGE_NAME="rdesktop" -DPACKAGE_TARNAME="rdesktop" -DPACKAGE_VERSION="1.8.2" \
-DPACKAGE_STRING="rdesktop\ 1.8.2" -DPACKAGE_BUGREPORT="" \
-DSTC8_HEADERS=1 -DHAVAL_SYS_TYPES_H=1 -DHAVAL_SYS_STAT_H=1 -DHAVAL_STDLIB_H=1 \
-DHAVAL_STRING_H=1 -DHAVAL_MEMORY_H=1 -DHAVAL_STRINGS_H=1 -DHAVAL_INTTYPES_H=1 \
-DHAVAL_STDINT_H=1 -DHAVAL_UNISTD_H=1 -DL_ENDIAN=1 -DHAVAL_SYS_SELECT_H=1 \
-DHAVAL_LOCALE_H=1 -DHAVAL_LANGINFO_H=1 -Dssldird="/usr/" \
-DEGD_SOCKET="/var/run/egd-pool" -DWITH_RDPSND=1 -DRDPSPND_ORDS=1 \
-DRDPSPND_ALSA=1 -DHAVAL_ENDIAN_H=1 -DHAVAL_DIRPFD=1 -DHAVAL_DECL_DIFF=1 \
-DHAVAL_ICONV_H=1 -DHAVAL_ICONV=1 -DICONO_FOAV_CONST= -DHAVAL_SYS_VFS_H=1 \
-DHAVAL_SYS_STATVFS_H=1 -DHAVAL_STATVS_H=1 -DHAVAL_SYS_PARAM_H=1 \
-DHAVAL_SYS_MOUNT_H=1 -DSTAT_STATVFS=1 -DHAVAL_SYS_STATVS_H=1 \
-DHAVAL_SYS_MOUNT_H=1 -DSTAT_STATVFS=1 -D_FILE_OFFSET_BITS=64 \
-DHAVAL_STRUCT_STATFS_F_NAMLEHLE=1 -D_FILE_OFFSET_BITS=64 \
-DHAVAL_MNTENT_H=1 -DHAVAL_SETMNTENT=1 \
-DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -o rdesktop.o -c rdesktop.c

gcc -g -O2 -Wall -I/usr/include -I/usr/include/alsa \
-DPACKAGE_NAME="rdesktop" -DPACKAGE_TARNAME="rdesktop" -DPACKAGE_VERSION="1.8.2" \
-DPACKAGE_STRING="rdesktop\ 1.8.2" -DPACKAGE_BUGREPORT="" \
-DSTC8_HEADERS=1 -DHAVAL_SYS_TYPES_H=1 -DHAVAL_SYS_STAT_H=1 -DHAVAL_STDLIB_H=1 \
-DHAVAL_STRING_H=1 -DHAVAL_MEMORY_H=1 -DHAVAL_STRINGS_H=1 -DHAVAL_INTTYPES_H=1 \
-DHAVAL_STDINT_H=1 -DHAVAL_UNISTD_H=1 -DL_ENDIAN=1 -DHAVAL_SYS_SELECT_H=1 \
-DHAVAL_LOCALE_H=1 -DHAVAL_LANGINFO_H=1 -Dssldird="/usr/" \
-DEGD_SOCKET="/var/run/egd-pool" -DWITH_RDPSND=1 -DRDPSPND_ORDS=1 \
-DRDPSPND_ALSA=1 -DHAVAL_ENDIAN_H=1 -DHAVAL_DIRPFD=1 -DHAVAL_DECL_DIFF=1 \
-DHAVAL_ICONV_H=1 -DHAVAL_ICONV=1 -DICONO_FOAV_CONST= -DHAVAL_SYS_VFS_H=1 \
-DHAVAL_SYS_STATVFS_H=1 -DHAVAL_STATVS_H=1 -DHAVAL_SYS_PARAM_H=1 \
-DHAVAL_SYS_MOUNT_H=1 -DSTAT_STATVFS=1 -DHAVAL_SYS_STATVS_H=1 \
-DHAVAL_SYS_MOUNT_H=1 -DSTAT_STATVFS=1 -D_FILE_OFFSET_BITS=64 \
-DHAVAL_STRUCT_STATFS_F_NAMLEHLE=1 -D_FILE_OFFSET_BITS=64 \
-DHAVAL_MNTENT_H=1 -DHAVAL_SETMNTENT=1 \
-DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -o xwin.o -c xwin.c

<Additional gcc commands omitted here>

gcc -g -O2 -Wall -I/usr/include -I/usr/include/alsa \
-DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -o rdesktop rdesktop.o xwin.o \
xkeymap.o ewmhints.o xclip.o cliprdr.o rdpsnd.o rdpsnd_dsp.o rdpsnd_oss.o \
rdpsnd_alsa.o tcp.o iso.o mcs.c secure.o license.o rdp.o orders.o bitmap.o \
cache.o rdpdr.o channels.o rdrp.o
```

