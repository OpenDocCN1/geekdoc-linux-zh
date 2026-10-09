
- 它不仅能检测写入违规，还能检测读取违规。
- 它能精确定位导致错误的指令。
- 它重载了所有标准的内存分配函数，例如 `malloc()`、`calloc()`、`memalign()`、`sbrup()`，以及 C++ 的 `new` 和 `new[]` 运算符，还包括它们的对应释放函数，例如 `free()`，以及 `delete` 和 `delete[]` 运算符。
- 利用 CPU 的内存管理单元，它分配并保护一个额外的内存页，以检测超出缓冲区顶部（或根据用户选项，底部）的任何非法访问。
- 它会在请求访问受保护内存页的错误指令处停止程序，允许你在调试器中定位有缺陷的源代码。
- 在内存块释放过程中，它检测内存块非保护端的错误写入。
- 它检测分配和释放函数的不匹配；例如，使用 `malloc()` 分配却使用 `delete` 释放。
- 它检测内存泄漏：那些直到程序退出前都未释放的内存块。
- 在 Linux（和部分 Unix）系统上，它预加载其库，允许在不修改源代码或重新编译的情况下进行测试。

## Electric Fence（电围栏）

如前所述，Electric Fence 仍然广泛可用，因此我们将包含第一版中关于 2.1 版本的讨论，作者发现该版本使用起来更简单，尽管其源代码有点棘手。撰写本文时，作者的 Fedora 7 发行版是 2.2.2-23，作者发现它需要进行大量修改才能编译。这留作读者的练习。

下载该软件包并将其解压到 `$[PRJROOT]/debug` 目录。在安装的其余步骤中，请切换到该软件的目录：

```
$ cd $[PRJROOT]/debug/ElectricFence-2.1
```

在为目标系统编译 Electric Fence 之前，你必须编辑 `page.c` 源文件，并在以下代码段周围添加 `#if 0` 和 `#endif` 以注释掉该代码段：

```c
#if ( !defined(sgi) && !defined(AX) )
extern int              sys_nerr;
extern char *          sys_errlist[   ];
#endif
```

如果不以这种方式修改代码，Electric Fence 将无法编译。修改代码后，为目标系统编译并安装 Electric Fence：

```
$ make CC=architecture-linux-gc AR=architecture-linux-ar
$ make LIB_INSTALL_DIR=\$(TARGET_PREFIX)/lib \
> MAN_INSTALL_DIR=\$(TARGET_PREFIX)/man install
```

Electric Fence 库 `libefence.a`（包含内存分配替换函数）现已安装到 `$[TARGET_PREFIX]/lib`。要将应用程序与 Electric Fence 链接，必须将 `-lelfence` 选项添加到链接器的命令行中。以下是我们对命令模块的 Makefile 所做的修改：

```
CFLAGS      = -g -Wall
LDFLAGS     = -lelfence
```

如果你希望 GDB 能够打印出引起问题的行，`-g` 选项是必需的。编译并剥离后，Electric Fence 库会使你的二进制文件增加约 30 KB。构建完成后，像往常一样将二进制文件复制到目标系统以执行。

如果程序没有核心转储（core dumping）地运行——恭喜！你成功编写了一个没有内存访问故障的程序。但几乎总是，当你在目标系统上运行该程序时，你会得到类似以下内容的输出：

```
# command-daemon
    Electric Fence 2.0.5 Copyright (C) 1987-1998 Bruce Perens.
    Segmentation fault (core dumped)
```

由于核心文件是在不同架构的系统中生成的，因此无法将 `core` 文件复制回主机进行分析。因此，在目标系统上启动 GDB 服务器，并使用目标 GDB 从主机连接到它。作为一个例子，以下是我们如何在目标系统上启动命令守护进程以便进行 Electric Fence 调试：

```
# gdbserver
    host_ip_address::2345 command-daemon
```

并且在主机上我们输入：

```
$ architecture-linux-gcc command-daemon
(gdb) target remote 192.168.172.10::2345
Remote debugging using 192.168.172.10::2345
0x10000074 in start ( )
(gdb) continue
Continuing.
    Program received signal SIGSEGV, Segmentation fault.
    0x10000384 in main (argc=2, argv=0x7ffff94) at daemon.c:126
    126    input_buf[input_index] = value_read;
```

在这种情况下，非法引用是由文件 `daemon.c` 第 126 行对数组的越界写入引起的。有关使用 Electric Fence 的更多信息，请查看软件包中包含的大量手册页（manpage）。

## DUMA

DUMA 软件包位于 http://duma.sourceforge.com。它显然比 Electric Fence 更强大，但这种力量也带来了复杂性。作者在进行构建流程的实验后，发现将该软件包移动到与目标板共享的构建分区上更容易、更简单。然后，使用目标板上的本地 gcc、g++ 和 ar 来构建该软件包。如果你向目标系统导出一个 NFS 分区，构建 DUMA 并不难，也不会花费太长时间。请始终记住，“采用本地编译（go native）”往往比花数小时去弄清楚为什么 Makefile 或交叉编译的其他特殊性无法生成你可以从主机移植到目标的二进制文件，是一个更好的解决方案。

DUMA 的操作方式与 Electric Fence 类似，并且有自己的文档。

## MEMWATCH

与 Electric Fence 和 DUMA 一样，MEMWATCH 用跟踪分配和释放的版本替换了通常的内存分配函数，例如 `malloc()` 和 `free()`。MEMWATCH 在检测内存泄漏和违规方面非常有效，例如当你忘记释放内存区域或尝试多次释放同一内存区域时。然而，与 Electric Fence 相比，MEMWATCH 在检测迷失指针方面效率较低。例如，我们无法检测到前一节中展示的错误数组写入。

MEMWATCH 可在其项目站点 http://www.lindata.se/source code.html 上获取。下载软件包并将其解压到你的 `${PRJROOT}/debug` 目录中。

MEMWATCH 由一个头文件和一个 C 文件组成，两者都必须与你的应用程序一起编译。要使用 MEMWATCH，请通过将这些文件复制到你的应用程序源目录开始：

```
$ cd ${PRJROOT}/debug/memwatch-2.71
$ cp memwatch.c memwatch.h ${PRJROOT}/project/command-daemon
```

修改 `Makefile`，将新的 C 文件作为要编译和链接的对象的一部分添加进去。例如，对于我的命令守护进程，我使用了以下 `Makefile` 修改：

```
CFLAGS		= -O2 -Wall -DMEMWATCH -DWN_STDIO
.\
OBJ5		= daemon.o memwatch.o
```

你还必须将 MEMWATCH 头文件添加到你的源文件中：

```
#define MEMWATCH
#include "memwatch.h"
#endif /* #ifdef MEMWATCH */
```

现在你可以像平常一样交叉编译二进制文件；MEMWATCH 没有特殊的安装说明。构建并剥离后，memwatch.c 和 memwatch.h 文件会使你的二进制文件增加约 30 KB。

程序运行时，它会生成关于程序行为的报告，并将其放入二进制文件运行目录中的 memwatch.log 文件中。以下是目标机器上的测试程序生成的 memwatch.log 摘录：

```
=========== MEMWATCH 2.71 Copyright (C) 1992-1999 Johan Lindh ===========

Started at Sun Jan 11 12:55:04 1970

Modes: __STDC__ 32-bit mMORD= (unsigned long)
mROUNDALLOC=4 sizeof(mmData)=32 mmDataSize=-32

statistics: now collecting on a line basis

Hello world

underflow: <5> test.c(62), 200 bytes alloc'd at <4> test.c(60)
relink: <7> test.c(66) attempting to repair MM-0x1b2c8c...
relink: MM-0x1b2c8c is the head (first) allocation
relink: successful, no allocations lost
assert trap: <8> test.c(69), 1==2
breakout: MEMWATCH: assert trap: test.c(69), 1==2

Stopped at Sun Jan 11 12:58:22 1970

unfreed: <3> test.c(59), 20 bytes at 0x1b194 {FE FE FE FE FE FE FE FE FE FE FE F

 - memwatch.log 1/89 1%
```

`unfreed` 行告诉你源代码中的哪一行分配了从未被释放的内存。在这种情况下，test.c 第 59 行分配了 20 字节，且从未被释放。

有关使用 MEMWATCH 及其提供输出的更多信息，请查看软件包中包含的 FAQ、README 和 USING 文件。

## 关于硬件工具

本书的第一版曾提及调试中硬件的使用，并指出了工具的丰富性。如今情况亦是如此。对该主题进行一次粗略的 Google 搜索会产生超过 36,000 个结果，而且到你读完这本书时，这个数字还会更多。硬件和软件工具的价格从免费到数千美元不等。

板卡开发者已经意识到，调试的便利性是一项真正的资产，并取得了巨大进步，以提供对硬件的访问支持以及对硬件调试的支持。许多板卡，特别是 JTAG 板卡，都有连接器或原理图，显示如何连接板卡进行调试。最好的起点是你的硬件供应商的网站和技术支持。他们很有可能提供一个低成本选项来支持硬件调试工具。

这里的工具讨论将因嵌入式系统中变化之快而受到限制，这对调试尤为敏感。例如，许多
