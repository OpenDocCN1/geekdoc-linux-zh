
```
    772: ff 75 f8        pushl 0xffffff8(%ebx)

    77e: e8 d6 fe ff ff    call 650 <init+0x48>

    77a: 83 c4 10        add $0x10,%esp

    77d: 8b 5d fc        mov 0xfffffffc(%ebp),ebx

    780: c9              leave

    781: c3              ret

    782: 90              nop

    783: 90              nop
```

使用 `-g` 编译源码后，你现在就有了将源码映射到机器码的能力。`objdump` 提供了许多其他功能。GNU/Linux 手册列出了大量的选项。

## ranlib

`ranlib` 工具是创建静态库时最重要的工具之一。它为库创建一个索引并将其存储在库文件中。当库中存在此索引时，链接阶段可以大大加快。因此，每当创建一个静态库时都应该执行 `ranlib` 工具。这里有一个使用 `ranlib` 的示例：

```
$ ranlib libmyrand.a
```

注意，使用 `ar` 命令配合 `-s` 选项也可以执行相同的操作，如下所示：

```
$ ar -s libmyrand.a
```

打印归档可以通过这些选项中的任何一个完成：

```
$ nm -s libmyrand.a

$ nm -print libmyrand.a
```

## 总结

本章探讨了库的创建和使用。首先讨论了静态库，是共享库库最后是动态加载库。本章还研究了使用 `ar` 创建库的方法。最后讨论了若干基于库的工具，包括 `ldd`、`size` 和 `ranlib`。

## 动态库 API

```
#include <dlfcn.h>

void *dlopen(const char *filename, int flag);

const char *dlerror(void);

void *dlsym(void *handle, char *symbol);

int dlclose(void *handle);
```

### 8 使用 autoconf 构建软件包 13

Curtis Nottberg 著

# 在章中

- 复习
- GNU Autotools 简介
- 将项目转换为 Autotools
- automate 简介
- autoconf 简介

## 引言

标准的 GNU `make` 工具减轻了从多个文件构建可执行文件的许多负担。它实现了源码的增量构建，并允许维护软件包所需的命令收集在单一位置。然而，随着项目复杂性的增加，GNU `make` 开始变得复杂。导致 `Makefile` 维护复杂的因素有：

- 具有各种构建要求的大项目
- 对外部库的依赖
- 在多平台环境中构建的需求
- 在多个环境中安装软件
- 分发软件包

## GNU/Linux 编程

解决这些复杂性的方案是向上移动并自动生成构建项目的 `Makefile`。这让 GNU `make` 专注于它擅长的领域，同时仍然配置当前构建环境的能力。GNU Autotools 尝试在 GNU `make` 工具之上提供下一级构建功能。跨平台 GNU 构建系统（由 automate、autoconf 和 libtool 软件包组成）由自由软件基金会的 David Mackenzie 于 1991 年启动。

## 示例项目

本章示例展示了构建由四个源文件组成的项目的各种方法。两个源文件用于构建库，其他文件构建使用该库的应用程序（见图 8.1）。

![](img/f7bd35eb87a62f74c6f23c07df847dff_114_0.png)

### Makefile 解决方案 95

## 示例简单实现

列表 8.1 显示了一个构建库和使用该库的应用程序的简单 `Makefile`。此 `Makefile` 用于为比较 Autools 如何构建相同项目提供基础。请这里考虑的示例非常简单。在这个项目中应用 `automate/autoconf` 看起来投入多于收益，但随着项目的增长，使用 Autotools 的回报会增加。

**列表 8.1** 构建示例的简单 `Makefile`（位于 CD-ROM 的 `/source/ch8/Makefile.simple`）

```
1: VPATH= lib app

2:

3: LIBSRC= lib.c bar.c

4: LIBOBJ= $(LIBSRC):.o

5:

6: APPSRC= main.c app.c

7: APOBJ= $(APPSRC):.o

8:

9: CFLAGS=

10: INCLUDES=-I ./lib

11:

12: all: libexp.a appex

13:

14: %.o:%.c $(CFLAGS) $(INCLUDES) -o $$

15:

16:

17: libexp.a: $(LIBOBJ)

18: $(AR) cru $(LIBOBJ) libexp.a

19:

20: appex: $(APOBJ) libexp.a

21: $(CC) -o appex $(APOBJ) -lex -L
```

列表的第 1 行显示了 `VPATH` 变量。`VPATH` 变量指定了 `make` 工具查找构建源文件的路径。注意列表中没有包含路径，因为这是由 `VPATH` 变量处理的。第 9 行和第 10 行设置了执行构建所需的编译器标志。第 12 行设置了构建库和应用程序的默认目标。## 96 GNU/Linux 编程

简单的 `Makefile` 缺少了一些在实际构建系统中需要包含才能使其可用的功能：清理目标、对包含头文件的依赖跟踪、安装生成的二进制文件的方法等等。Autotools 实现提供了许多这些缺失的功能，与创建简单 `Makefile` 所需的工作相比，仅需要少量额外工作。

## 使用 Autotools 的简单实现

列表 8.1 使用了使用 Autotools 构建项目来替换简单 `Makefile` 的初始实现。尽管这看起来是用很多文件来替换一个文件，但每个替换文件通常更简单。图 8.2 阐明了图 8.1 的目录结构在增加 Autotools 文件后的目录结构。

![](img/f7bd35eb87a62f74c6f23c07df847dff_116_0.png)

图 8.2 带有 Autotool 文件的示例项目目录结构。

# 第 8 章 使用 automake/autoconf 构建软件包 97

支持简单的 Autotools 项目添加的额外文件有：

- autogen.sh: 用于运行 Autotools 生成构建环境的 shell 脚本
- configure.ac: autoconf 工具的输入文件
- Makefile.am: 顶层 Makefile 模板
- app/Makefile.am: appexp 可执行文件的 Makefile 模板
- lib/Makefile.am: 构建 libexp.a 库的 Makefile 模板

这些文件向 Autotools 描述了预期的构建产品和环境。Autotools 获取这些输入并生成一个构建环境模板，然后在构建系统上进一步进行配置，以生成最终的 Makefile Set。假设你在同一台机器上进行开发和构建，以下命令可以配置并构建示例项目：

```
## ./autogen.sh

## ./configure

## make
```

运行 `autogen.sh` 脚本会执行 Autotool 工具，将输入文件转换为可以在主机系统上配置的构建环境模板。执行 `configure` 脚本会针对该机器自定义构建环境模板。`configure` 脚本的输出是一组 GNU Makefiles，用于构建系统。在根目录下执行 `make` 命令会同时构建库和应用程序。

检查 `autogen.sh` 应该是理解此过程如何工作的起点。列表 8.2 显示了一个执行 Autools 工具的非常简单 `autogen.sh` 脚本。通常，在实际项目中，`autogen.sh` 脚本要复杂得多，首先要检查是否存在 Autotools 以及版本是否合适。要寻找复杂的 `autogen.sh` 脚本示例，你应该查看你喜欢的开源项目源码仓库中的此文件。

# 列表 8.2 简单的 autogen.sh 脚本（位于 CD-ROM 的 ./source/ch8/autogen.sh）

```
1: #!/bin/sh

2: # 运行此脚本生成所有初始 makefiles 等

3:

4: aclocal

5: libtoolize -automake

6: automake -a

7: autoconf
```
