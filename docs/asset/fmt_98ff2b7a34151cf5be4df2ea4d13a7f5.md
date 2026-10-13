
# 非操作系统特定的编译配置选项

最新的 Samba 版本具有更高的移植性，因为 Samba 使用 GNU 自动配置进行自配置，这结束了安装 Samba 的人员配置 Makefile 的需求。

在源码目录下，现在通过运行 `./configure` 然后运行 `make` 来配置并构建 Samba。更多细节，请参阅本书的光盘或最新 Samba 发行版的 `docs/textdocs/UN_INSTALL.txt` 文件。`./configure` 前后的源码目录列表分别在列表 3.7 和 3.8 中所示。

## 列表 3.7 `./configure` 之前的源码目录列表

```
Linuxserver1:/downloads/samba/samba-2.0.2/source# ls -l M

-rw-r--r-- 1002 1002 19676 Feb 6 22:51 Makefile.in
```

## 列表 3.8 `./configure` 之后的源码目录列表

```
Linuxserver1:/downloads/samba/samba-2.0.2/source# ls -l M*

total 45

-rw-r--r-- 1 root root 19517 Mar 1 20:13 Makefile
```

`Makefile` 的头部内容在列表 3.9 中显示。

## 列表 3.9 Makefile

```
# 由 configure 自动从 Makefile.in 生成

####################################################################################
# Samba 的 Makefile.in - 为支持 autoconf 重写
# 版所有 Andrew Tridgill 1992-1998
####################################################################################

prefix=/usr/local/samba

exec_prefix=$(prefix)

mandir=$(prefix)/man

LIBS=

CC=gcc

CFLAGS--0

CPPFLAGS=

LDFLAGS=

AWK=gawk

INSTALLCMD=//usr/bin/ginstall -c

ssrcdir-=

buildldir=/downloads/samba/samba-2.0.2/source

SHELL=/bin/sh

BASEDIR = /usr/local/samba

BINDIR = $(exec_prefix)/bin

# 我们没有使用 sbir，因为我们希望与
# 之前的 Samba 版本保持完全兼容

SBINDIR = $(exec_prefix)/bin

LIBDIR = $(exec_prefix)/lib

VDIR = $(prefix)/var

MANDIR = $(prefix)/man

# 给可执行文件赋予的权限

INSTALLPERMS = 0755

# 设置这些路径以找到各种文件
# 这些可以通过命令行开关覆盖（参见 smbd(B)）
# 或在 smb.conf 中覆盖（参见 smb.conf(5)）

SMBFILE=$(VARDIR)/log.smb

NMBLOGFILE=$(VARDIR)/log.nmb

CONFIGFILE=$(LIBDIR)/smb.conf

LMHOSTSFILE=$(LIBDIR)/lmhosts

DRIVERFILE=$(LIBDIR)/printers.def
```

### 直接解决方案

```
PASSWD_PROGRAM = /bin/passwd

# 这里是 smbpasswd 等文件的存放位置

PRIVATEDIR = $(prefix)/private
```

```
SMB_PASSWD_FILE = $(PRIVATEDIR)/smbpasswd

# 这里是 SWAT 和帮助文件的存放位置

SWATDIR = $(prefix)/swat
```

```
# 存放锁文件的目录

LOCKDIR = $(VARDIR)/locks
```

```
# 存放代码页定义文件的目录

CODEPAGED = $(LIBDIR)/codepages
```

```
# 当前的代码定义列表。

CODEPAGELIST = 437 737 850 852 861 932 866 949 950
```

![](img/166cd29830b01a9e3eceb33240be1bcf_160_0.png)

```
# 你可以在这里找到 smbrun 二进制文件。默认路径是
# 安装目录。此二进制文件对于正确的打印
# 和魔法脚本执行是所需的。这应该是一个绝对路径！
# 此外，文件名结尾应包含 "smbrun"
# 可执行文件的名称

SMBRUN = $(BINDIR)/smbrun
```

```
PASSWD_FLAGS = DPASS_PROGRAM="$(PASSWD_PROGRAM)"

DSMB_PASSWD_FILE="$(SMB_PASSWD_FILE)"

FLAGS1 = $(FLAGS) -include-I$(srcdir)/include -I$(srcdir)/ubiq

I$(srcdir)/smwrapper="$(CPFLAGES)" -DMBLOGFILE="$(SMBLOGFILE)"

DMBLOGFILE="$(NMBLOGFILE)"

FLAGS2 = -DCONFIGFILE="$(CONFIGFILE)" -DLMHOSTFILE="$(LMHOSTSFILE)"

FLAGS3 = -DSWATDIR="$(SWATDIR)" -DBINDIR="$(BINDIR)"

DLOCKDIR="$(LOCKDIR)" -DSMBRUN="$(SMBRUN)"

CODEPAGED="$(CODEPAGED)"

FLAGS4 = -DDRIVERFILE="$(DRIVERFILE)" -DBINDIR="$(BINDIR)"

FLAGS5 = $(FLAGS1) $(FLAGS2) $(FLAGS3) $(FLAGS4) -DHAVE_INCLUDES_H

FLAGS = $(ISA) $(FLAGS5) $(PASSWD_FLAGS)

FLAGS32 = $(ISA32) $(PASSWD_FLAGS)
```

```
SPROG5 = bin/smbd bin/nmbd bin/swat

SPROG1 = bin/smbclient bin/termpart/testprns bin/smbrun bin/smbstatus

SPROG2 = bin/rcpcient/smbpasswd bin/make_smbcodepage

MPROGS = 

PROGS = $(SPROG1) $(SPROG2) $(MPROGS) bin/nmblook bin/make_printerdef
```

# 第 3 章 获取与安装

```
SCRIPTS = $(srcdir)/script/smbtar $(srcdir)/script/addtosmbpass $(srcdir)/
script/convert_smbpasswd
```

`QUOTADBJS=noquotas.`

## 了解你的安装选项

你仍然可以针对特定系统编辑 `Makefile`。在运行 `Jconfigure` 之后和 `make` 之前编辑此文件允许允许根据你对基础目录或其他处的偏好安装 Samba。

在这种情况下，安装的默认目录是 `BASEDIR=/usr/local/samba`；
`prefix=/usr/local/samba` 是设置 `Makefile` 中其他目录的变量。

Samba 及其相关程序通常安装在替代位置；这些位于 `/usr/local/bin`, `/usr/local/sbin`, `/usr/bin`, `/usr/sbin`, `/opt/samba`, `/usr/lib` 以及 `/usr/local/main`。

## 默认配置选项

默认配置选项设置了 Samba 可执行文件使用的各种文件的位置。这些可以通过命令行开关或在 `smb.conf` 中如下覆盖：

```
SMBLOGFILE = $(VARDIR)/log.smb

NMLOGFILE = $(VARDIR)/log.nmb

CONFIGFILE = $(LIBDIR)/smb.conf

LMHOSTFILE = $(LIBDIR)/lmhosts

DRIVERFILE = $(LIBDIR)/printers.def

PASSWD_PROGRAM = /bin/passwd

# 这里是 smbpasswd 等文件的存放位置

PRIVATEDIR = $(prefix)/private

SMB_PASSWD_FILE = $(PRIVATEDIR)/smbpasswd
```
