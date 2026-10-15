
```bash
$ ls ptxconfigs
arm-1136jfs-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
arm-xscale-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
armeb-xscale-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.17.ptxconfig
arm-ep93xx-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
arm-iwmmx-linux-gnueabi gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
arm-wrt.hardfloat-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.18.ptxconfig
arm-v4t-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
arm-v4t-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.18.ptxconfig
arm-xscale.hardfloat-linux-gnu gcc-4.0.4 glibc-2.6.16 linux-2.6.17.ptxconfig
arm-xscale-linux-gnueabi gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
arm-xscale-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.17.ptxconfig
i586-unknown-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
i686-unknown-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
mips-r5000-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
powerpc64-603e-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
powerpc64-970-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
```

要构建示例工具链之一，您需要告诉 Ptxdist 您想要使用哪个配置文件，然后指示它根据配置文件中的说明构建工具链。

作为一个示例，我们将为 ARM Xscale EABI 构建一个交叉工具链，使用 `gcc` 4.1.2 和 `glibc` 2.5，并包含来自 2.6.18 版本的内核头文件，同时支持 NPTL。因此，你将使用的示例文件为 `ptxconfig/figs/arm-xscale-linux-gnueabi_gcc-4.1.2_glibc-2.5_linux-2.6.18.ptxconfig`。

然而，在使用之前，你必须对示例配置文件进行小幅修改，因为示例配置文件是使用较早版本的 Ptxdist 框架生成的。该较早版本的版本号嵌入在配置文件中，如果你直接尝试使用该示例配置，Ptxdist 将会报错并停止。

幸运的是，配置文件是简单的文本文件。你可以直接编辑配置文件，并将版本号更新为你使用的最新版本。虽然你可以轻松使用文本编辑器手动完成此操作，但以下 shell 小技巧也能很好地完成这项工作：

```bash
$ sed s/PTXCONF_CONFIGFILE_VERSION=.*/PTXCONF_CONFIGFILE_VERSION="1.0"/ \
ptxconfig/figs/arm-xscale-linux-gnueabi_gcc-4.1.2_glibc-2.5_linux-2.6.18.ptxconfig \
ptxconfig/figs/arm-xscale-linux-gnueabi_gcc-4.1.2_glibc-2.5_linux-2.6.18.ptxconfig.tmp \
$ mv ptxconfig/figs/arm-xscale-linux-gnueabi_gcc-4.1.2_glibc-2.5_linux-2.6.18.ptxconfig.tmp \
ptxconfig/figs/arm-xscale-linux-gnueabi_gcc-4.1.2_glibc-2.5_linux-2.6.18.ptxconfig
```

执行此命令后，通过以下命令指示 Ptxdist 使用你的“已修补”的配置文件：

```bash
$ $PR$ROOT/build-tools/bin/ptxdist select \
ptxconfig/figs/arm-xscale-linux-gnueabi_gcc-4.1.2_glibc-2.5_linux-2.6.18.ptxconfig
```

现在你可以自定义我们选定的示例工具链项目配置。输入以下命令：

```bash
$ ptxdist menuconfig
```

系统将会展示 Ptxdist 工具链项目菜单，如图 4-2 所示。该菜单包含以下选项和子菜单：

## 项目名称

一个用于输入项目长名称的文本框。如果你维护多个不同的 Ptxdist 工具链项目，这会非常有用。

## glibc

此子菜单允许你指定 `glibc` 版本、可能希望传递给包配置脚本的额外配置选项、文件列表、构建前应用于库源代码的一组补丁、最低支持的内核版本、可能希望传递给 `glibc` 配置脚本的额外环境变量、要使用的线程库（NPTL 或 LinuxThreads），以及生成的 `glibc` 是否支持线程本地存储。

## glibc-ports

此子菜单允许你列出来自 `glibc-ports` 存档的一组补丁，应用于 `glibc`。该存档包含来自 `glibc` 核心团队之外的 `glibc` 补丁。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_132_0.png)

图 4-2. Ptxdist 工具链菜单

## binutils

此子菜单允许你选择要包含在构建的工具链中的 `binutils` 包版本。

## kernel

此子菜单设置用于构建工具链所需的 Linux 内核头文件的内核版本和配置文件。它还允许你指定是否使用净化的头文件。有关内核配置的更多信息，请参见第 5 章中的“配置内核”。

## gcc（第一阶段）

此子菜单允许你指定用于第一阶段（自举）编译器的 `gcc` 版本，以及提供给 `gcc` 配置脚本的补丁系列文件和额外选项。

## gcc（第二阶段）

此子菜单允许你选择新创建的工具链将支持哪些编程语言。支持的编程语言取决于 `gcc` 版本，但所有版本都支持 C 和 C++。

## cross gdb

勾选此复选框可以请求 PTxdist 在工具链构建过程中构建一个交叉调试器。

## architectures

此下拉框允许你指定工具链的目标架构。目前支持 ARM、MIPS、PowerPC 和 x86。

## toolchain target

此文本框允许你设置你的工具链 GNU 配置字符串（例如，`powerpc64-970-linux-gnu`）。

## 可调试的工具链内部组件

此复选框允许你指定是否应为工具链的 `glibc` 和 `libstdc++` 库生成完整的调试信息。选中此复选框可以让你进入定义在这些基础库中的函数进行调试，但这会使你的工具链体积增加约 500 MB。（不过这不会影响目标文件系统的大小。）

## misc

`misc` 子菜单允许你指定与当前工具链项目兼容的 PTxdist 版本，以及设置生成的文件系统安装到的文件系统前缀。将第一个前缀设置为项目根目录下的 `tools` 目录，并将第二个前缀字段留空。

配置完这些项后，选择 `<Exit>` 按钮并按 `[Enter]`，然后选择 `<Yes>` 按钮以保存你的配置。

**构建工具链。** 最后，你可以让 PTxdist 构建你的工具链了。在此过程中，PTxdist 将自动下载、配置、打补丁、构建并安装所有必需的组件。要开始构建过程，输入以下命令：

```bash
$ ptxdist go
```

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_133_0.png)

构建完成后，新的工具链将位于项目根目录的 `tools/bin` 目录中，准备就绪。

## 使用工具链

前面章节中的步骤应该已经创建了一个功能完整的交叉开发工具链，你可以像使用本机 GNU 工具链一样使用它；你只需在每个命令前加上目标名称即可。例如，对于你的目标，不需要调用 `gcc` 和 `objdump`，而是需要调用类似 `i386-linux-gcc` 和 `i386-linux-objdump` 这样的命令。

以下是 DAQ 模块控制守护程序的 `Makefile`，这是交叉开发工具链用法的一个很好的示例：

```makefile
# Tool names
CROSS_COMPILE   = $(TARGET)-
AS              = $(CROSS_COMPILE)as
AR              = $(CROSS_COMPILE)ar
CC              = $(CROSS_COMPILE)gcc
CPP             = $(CC) -E
LD              = $(CROSS_COMPILE)ld
NM              = $(CROSS_COMPILE)nm
OBJCOPY         = $(CROSS_COMPILE)objcopy
OBJDUMP         = $(CROSS_COMPILE)objdump
RANLIB          = $(CROSS_COMPILE)ranlib
READELF         = $(CROSS_COMPILE)readelf
SIZE            = $(CROSS_COMPILE)size
STRINGS         = $(CROSS_COMPILE)strings
STRIP           = $(CROSS_COMPILE)strip

export AS AR CC CPP LD NM OBJCOPY OBJDUMP RANLIB READELF SIZE STRINGS STRIP

# Build settings
CFLAGS          = -O2 -Wall
HEADER_OPS      = 
LDFLAGS         = 

# Installation variables
EXEC_NAME       = command-daemon
INSTALL         = install
INSTALL_DIR     = $(PRJROOT)/rootfs/bin

# Files needed for the build
OBJS            = daemon.o

# Make rules
all: daemon

.c.o:
	$(CC) $(CFLAGS) $(HEADER_OPS) -c $<

daemon: $(OBJS)
	$(CC) -o $(EXEC_NAME) $(OBJS) $(LDFLAGS)

install: daemon
	test -d $(INSTALL_DIR) || $(INSTALL) -d -m 755 $(INSTALL_DIR)
	$(INSTALL) -m 755 $(EXEC_NAME) $(INSTALL_DIR)

clean:
	rm -f *.o $(EXEC_NAME) core

distclean:
	rm -f *.o ${EXEC_NAME} core
```

`Makefile` 的第一部分指定了我们用于构建程序的工具链实用程序名称。每个实用程序的名字前都加上了目标名称。因此，`CC` 的值将是 `i386-linux-gcc`，即我们之前构建的交叉编译器。除了定义实用程序的名称外，我们还导出这些值，以便此 `Makefile` 调用的后续 `Makefile` 使用相同的名称。这种构建架构在包含许多子目录的大型项目中非常常见。

`Makefile` 的第二部分定义了构建设置。`CFLAGS` 提供了在构建任何 C 文件时要使用的标志。

正如我们在上一节所见，编译器已经使用了目标库的正确路径。因此，链接器标志变量 `LDFLAGS` 为空。如果编译器没有指向正确的库，或者使用了宿主机的库（如果你按照之前提供的说明操作，这种情况不应该发生），你需要通过设置链接标志来告知编译器使用哪些库，如下所示：

```makefile
LDFLAGS    = -nostdlib -L${TARGET_PREFIX}
```

如果你希望静态链接应用程序，你需要在 `LDFLAGS` 中添加 `-static` 选项。这会生成一个不依赖任何共享库的可执行文件。但是，鉴于标准 GNU C 库相当大，这将导致非常大的二进制文件。例如，一个简单的使用 `printf()` 打印“Hello World!”的程序在动态链接时小于 12 KB，而在静态链接时（即使经过 `stripped` 处理）约为 350 KB。

安装部分的变量指示要安装什么、安装到哪里以及如何安装生成的二进制文件。在这种情况下，二进制文件被安装到目标 `root` 文件系统的 `bin` 目录中。

就控制守护程序而言，目前我们只有一个文件需要构建。因此，程序的编译只需要这一个文件，但如果你在 `LDFLAGS` 中使用了 `-nostdlib` 选项（通常你不需要这样做），你还需要更改描述构建所需文件的段落以及生成二进制文件的规则：

```makefile
STARTUP_FILES = ${TARGET_PREFIX}/libc/crt1.o \ 
                ${TARGET_PREFIX}/libc/crti.o \ 
                ${PREFIX}/libc/gcc-1-lib/${TARGET}/7.9.5.3/crtbegin.o \ 
                ${PREFIX}/libc/gcc-1-lib/${TARGET}/7.9.5.3/crtend.o \ 
                ${TARGET_PREFIX}/libc/crtn.o
END_FILES     = -lc
LDBS          = daemon.o
OBJS          = ${STARTUP_FILES} ${OBJS} ${LDBS} ${END_FILES}


daemon:  ${OBJS}
	${CC}    -o  ${EXEC_NAME}  ${LINKED_FILES}  ${LDFLAGS}
```

前面的 `Makefile` 片段向由其自身 C 文件生成的目标文件添加了五个额外的目标文件：`crt1.o`、`crtbegn.o`、`crti.o` 和 `crtn.o`。这些文件分别对应特殊的启动、初始化、构造、析构和最终化文件，通常会自动链接到应用程序中。例如，正是通过这些文件，应用程序的 `main()` 函数才会被调用。由于我们在此处指示编译器不使用标准链接过程，因此需要显式地提及这些文件。如果你禁用了标准链接但忘记显式提及这些文件，链接器会因缺少 `_start` 符号而报错并失败。提供给编译器的目标文件的顺序很重要，因为编译器会自动调用 GNU 链接器来链接目标文件，而 GNU 链接器是一个单遍链接器。

`make` 规则本身与你通常会在标准本地 `Makefile` 中看到的规则非常相似。我们添加了安装规则以自动化安装过程。你也可以选择不使用这样的规则，而是手动将可执行文件复制到正确的目录。

在你的本地目录中有 `Makefile` 和源文件后，你只需要输入 `make` 即可为目标平台构建你的程序。例如，如果你想为宿主机的本地执行环境构建程序以测试你的应用程序，可以使用以下命令：

```
$ make CROSS_COMPILE=""
```

## C 语言库的替代方案

鉴于嵌入式系统的约束和限制，标准 GNU C 库的体积使其不太可能作为目标平台上的使用候选者。相反，我们需要寻找一个功能足够且相对较小的 C 语言库。随着时间推移，许多库在考虑到这些优先事项后得以实现。在本节中，我们将讨论两个最重要的 C 语言库替代方案：`uClibc` 和 `diet libc`。对于每个库，我们将提供背景信息、如何为目标平台构建该库的说明，以及如何使用该库构建应用程序的说明。

### uClibc

`uClibc` 库起源于 `uClinux` 项目，该项目提供可在缺乏内存管理单元（MMU）的处理器上运行的 Linux 系统。² 然而，该库后来成为一个独立项目，并支持多种处理器，包括那些拥有 MMU 的处理器。事实上，在撰写本文时，`uClibc` 支持第 3 章中深入讨论的所有处理器架构。

> ² 没有 MMU 的处理器属于低端处理器，而 Linux 越来越多地用于带有 MMU 的嵌入式系统。通过特殊处理，它可以在无 MMU 的系统上运行，缺点是某些功能将无法正常工作（例如内存保护）。

虽然 `uClibc` 不依赖 GNU C 库，但它提供了大多数相同的功能。当然，它不像 GNU 库那样完整，也不试图遵守 GNU 库遵守的所有标准。例如，那些极少使用的功能和函数特性在 `uClibc` 中被省略了。即便如此，大多数能针对 GNU C 库编译的应用程序也能使用 `uClibc` 进行编译和运行。为此，`uClibc` 开发人员专注于维护与 C89、C99 和 SUSV3 的兼容性。他们定期运行广泛的测试套件以确保 `uClibc` 符合这些标准。

`uClibc` 可以从其网站 `http://uclibc.org` 下载为 `tar-zip` 或 `tar-bzip2` 归档，或者通过 `CVS` 获取。该库根据 `LGPL` 条款分发。项目网站上提供有常见问题解答（FAQ），如果需要帮助，你可以订阅 `uClibc` 邮件列表或浏览邮件列表存档。在下文中的描述中，我们将使用 `uClibc` 的 0.9.29 版本，但解释也应适用于后续版本。早于 0.9.16 的版本依赖于不同的配置系统，因此不在下文讨论范围内。

### Buildroot
