
# 由 configure 从 Makefile.in 自动生成。

# GNU tar 程序的 Unix Makefile。

# 版所有 (C) 1991 Free Software Foundation, Inc.

```
```

# 此程序是自由软件；你可以根据 GNU

# 通用公共许可证的条款重新发布

# 或/或修改它

...
```

```
SHELL = /bin/sh

#### 系统配置部分开始。 ####

srcdir =

# 如果你使用 gcc，你应该运行

# 随附的 fixincludes 脚本，或者使用

# 带 -traditional 选项的 gcc。否则内联

# 调用将在某些系统上被错误编译。

CC = gcc -O

YACC = bison -y

INSTALL = /usr/local/bin/install -c

INSTALLDATA = /usr/local/bin/install -c -m 644

```

```
# 你可能添加到 DEFS 的内容：

```

```
# -DSTC_HEADERS

如果你有 ANSI C 头文件和库。

# -POSIX

如果你有 POSIX.1 头文件和库。

# -DBSDS42

如果你有 sys/dir.h（除非你使用 -DPOSIX）、sys/file.h，以及 'struct stat' 中的 st_blocks。

# -DUSG

如果你有 System V/ANSI C 字符串和内存函数头文件、sys/sysmacros.h、fcntl.h、getcwd、没有 valloc 以及 ndir.h（除非你使用 -DIRENT）。

# -DNO_MEMORY_H

如果你使用了 DSTC_HEADERS 但没有包含 memory。

# -DIRENT

如果你有 dirent.h 而不是 ndir.h。

# -DSIGTYPE=int

如果你的信号处理程序返回 int 而不是 void。

# -DMTIO

如果你缺少 sys/mtio.h (磁带 ioctls)。

# -DNO_REMTE

如果你没有远程 shell 或 rex。

# -DUSE_EXEC

使用 rex 进行远程磁带操作，而不是派生 rsh 或 remov。

# -DVPRINT_MISSING

如果你缺少 vprintf（但有 _doprint）。

# -DDOPR_MISSING

如果你缺少 _doprint 函数。还需要定义 DVPRINT_MISSING。

# -DFTIME_MISSING

如果你缺少 ftime 系统调用。

# -DSTR__MISSING

如果你缺少 strerror 函数。

# -DVALLOC_MISSING

如果你缺少 valloc 函数。

# -DMKDIR_MISSING

如果你缺少 mkdir 和 rmdir 系统调用。

# -DRENAME_MISSING

如果你缺少 rename 系统调用。

# -DFTRUNCATE_MISSING

如果你缺少 truncate 系统调用。

# -DV7

在 Version 7 Unix 上（很久未测试了）。

# -DEMUL_OPEN3

如果你缺少 3 参数版本的 open，并想用你已有的系统调用来模拟它。

# -DNO_OPEN3

如果你缺少 3 参数版本，并想通过禁用 tar -k 选项而不是模拟 open。

```

# 录 C：复杂的 Makefile 示例

```

# -DXENIX    如果你有 sys/inode.h

#           并且需要包含 st4。

```

```
DEFS = -DSIGYPE=int -DDIRENT -DSTR_MISSING \
-DVPRINT_MISSING -DBSD42

# 将此设置为 rtaplib，除非你定义了 NO_REMOTE，

# 在那种情况下将其为空。

RTAPELIB = rtaplib

LIBS =

DEF_AR_FILE = /dev/rmt8

DEFBLOCKING = 20

```

```
CDEBUG = -g

CFLAGS = $(CDEBUG) -I-$(scdir) $(DEFS) \
-DEF_AR_FILE="$(DEF_AR_FILE)" \
-DEFBLOCKING=$-g

```

```
LDFLAGS

prefix = /usr/local

# 每个安装程序的前缀，

# 通常为空或为 '.'。

prefix =

```

```
# 安装 tar 的目录。

bindir = $(prefix)/bin

```

```
# 安装 info 文件的目录。

infodir = $(prefix)/info

```

#### 系统配置部分结束。 ####

SRCS_C = tar.c extract.c buffer.c \
update.c gnu-mangle.c \
version.c diffarch.c \
port.c wildcat.c getopt.c \
SRCS_Y = getdate.y

SRCS = $(SRCS_C) $(SRCS_Y)

OBJS = $(SRCS_C:.o) $(SRCS_Y:.o)

AUX = README.pc configure.in \
tar.texinfo tar.*.tex \
port.h open.h \
rmt.c rtaplib alloc.c \
msd_dir.h msd_dir.c specs.c

GNU make

.PHONY: all

all:
    tar rmt.info

tar:
    $(OBJS)
    $(CC) $(LDFLAGS) -o $@ $(OBJS) $(LIBS)

rmt:
    rmt.c
    $(CC) $(CFLAGS) -o $@ rmt.c

tar.info: tar.texinfo
    make info tar.info

.PHONY: install

install:
    $(INSTALL) tar $(bindir)/$(prefix) \
    -f rmt || $(INSTALL) rmt /etc/
    $(INSTALLDATA) $(srcdir)/tar.info $(infodir)

$(OBJS): tar.h port.h regex.o buffer.o

# getdate.y has conflicts.

testpad:
    ./testpad

testpad: testpad.o
    $(CC) -o $@ testpad.o

TAGS:
    $(SRCS)
    etag $(SRCS)

.PHONY: clean

clean:
    rm -f *.o rmt testpad.h core

.PHONY: distclean

distclean: clean
    rm -f TAGS Makefile config.status

.PHONY: realclean

realclean: distclean
    rm -f tar.info*

# 录 C：复杂的 Makefile 示例

```
.PHONY: shar
shar: $(SRCS) $(AUX)
  shar $(SRCS) $(AUX) | compress \
  > tar-sed -e '/version_string/!d' \
  -e 's/[0-9].*\([0-9].*\)/\1/' \
  -e q
  version.c.shar.Z

```

.PHONY: dist

dist: $(SRCS) $(AUX)
  echo tar-sed \
  -e '/version_string/!d' \
  -e 's/[0-9].*\([0-9].*\)/\1/' \
  -e q
  version.c
  rm -rf 'cat-fame'
  mkdir 'cat-fame'
  ln $(SRCS) $(AUX) 'cat-fame'
  tar czf 'cat-fame'.tar.Z 'cat-fame'
  rm -rf 'cat-fame'

```

```
tar.zoo: $(SRCS) $(AUX)
  rm -rf tmp.dir
  mkdir tmp.dir
  rm tar.zoo
for X in $(SRCS) $(AUX); do \
  echo $$
  sed 's/\$/M$$' $$X \
  > tmp.dir/$$X; done
cd tmp.dir; zoo am ../tar.zoo *
  rm tmp.dir
