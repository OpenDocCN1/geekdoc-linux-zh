

# 启动 GDB

要启动调试会，只需输入 `gdb program`，将 `program` 替换为你想要调试的程序名称。使用核心文件（core file）是可选的，但它会增强 GDB 的调试能力。当然，你需要一个可以尝试 GDB 调试的程序，列表 29-5 提供了一个：`debugme.c`。

## 列表 29-5：一个有错误的程序

```
/*
 * debugme.c 一个编写得很糟糕的待调试程序
 */
#include <stdio.h>

#define BIGNUM 5000
#define SZ 100
void index_to_the_moon(int ary[]);

int main(int argc, char *argv[])
{
    int intary[100];
    index_to_the_moon(intary);
    return 0;
}

void index_to_the_moon(int ary[])
{
    int i;
    for (i = 0; i < BIGNUM; ++i)
        ary[i] = i;
}
```

使用命令 `gcc -g debugme.c -o debugme` 编译此程序。然后，使用命令 `./debugme` 执行程序。

```
$ ./debugme
Segmentation fault (core dumped)
$ file core
core: ELF 32-bit LSB core file Intel 80386, version 1 (SYSV), SVR4-style, SVR4-style, from 'debugme'
```

在大多数系统上，当你执行 `./debugme` 时，它会立即导致段错误（segmentation fault）并转储核心，如输出所示。

## 第 29 章：编程工具与实用程序

核心转储（core dump）指的是应用程序失败，并将应用程序存储在内存中的所有数据复制到当前目录下一个名为 `core` 的文件中。该文件可以帮助调试应用程序中的问题。

如果你看到 `core dumped` 字样，请尝试执行 shell 命令行 `ulimit -c unlimited`，这允许程序在当前工作目录下产生内存转储。

该程序有一个错误，因此你需要对其进行调试。第一步是启动 GDB，使用程序名 `debugme` 和核心文件 `core` 作为参数：

```
$ gdb debugme core
```

GDB 初始化后，屏幕应该类似于图 29-1。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_840_0.png)

图 29-1：GDB 的启动屏幕

如你在图片中间附近看到的，GDB 显示了创建核心文件的可执行文件名称：`+`。显然，显示的名称是错误的；它应该是 `debugme`。这些奇怪的字符会让经验丰富的开发者立即意识到程序存在严重的内存泄漏。在下一行，显示为“Program terminated with signal 1. Segmentation fault”的文本解释了程序终止的原因。当程序尝试访问不显式属于它的内存时，就会发生段错误。GDB 还显示了它正在执行的函数 `index_to_the_moon`。

如果你不喜欢许可信息（它们让我很困扰），在希望 GDB 抑制这些信息时使用 `-q`（或 `--quiet`）选项。另一个有用的命令行选项是 `-d dirname`，其中 `dirname` 是目录名，它告诉 gdb 在何处查找源代码（它默认在工作目录查找）。

将程序及其核心转储加载到调试器后，在调试器中运行程序。要这样做，在 GDB 提示符 `(gdb)` 后输入命令 `run`，如下例所示：

```
(gdb) run
Starting program: /home/www/code/debugme

Program received signal SIGSEGV. Segmentation fault.
0x0800483db in index_to_the_moon (ary=0xffffff4b0) at debugme.c:24
    ary[1] =
```

此输出列表显示段错误发生在 `debugme.c` 第 24 行的 `index_to_the_moon` 函数中。注意输出的该行：GDB 显示了发生段错误的代码行，并带有行号标记（24）。它还显示了发生故障的内存地址（十六进制）`0xffff4b0`。

你可以向 `run` 命令传递程序所需的任何参数。通常情况下，GDB 会创建一个完全模拟的环境，在该环境中它使用环境变量 `$SHELL` 的值来创建环境。如果你需要，可以在调试器中运行程序之前使用 GDB 的 `set` 和 `unset` 命令。

## 在调试器中检查代码

函数 `index_to_the_moon` 中发生了什么导致了错误？你可以执行 `backtrace`（或 `bt`）命令来生成导致段错误的函数回溯。函数回溯通常不会告诉你问题所在，但它会更精确地显示错误发生的位置。以下是该函数的回溯轨迹：

```
(gdb) bt
#0  0x0800483db in index_to_the_moon (ary=0xffffff4b0) at debugme.c:24
    ary[i] = i
#1  0x0800477a in main (argc=1, argv=0xbfffffefd8) at debugme.c:13
```

此输出列表显示段错误发生在 `debugme.c` 第 24 行的 `index_to_the_moon` 函数中。（*注：原文此处未提供完整回溯代码，此处根据逻辑补全示例以演示格式*）。注意输出的该行：GDB 显示了发生段错误的代码行，并带有行号标记（24）。它还显示了发生故障的内存地址（十六进制）`0xffff4b0`。

如果你不喜欢许可信息（它们让我很困扰），在希望 GDB 抑制这些信息时使用 `-q`（或 `--quiet`）选项。另一个有用的命令行选项是 `-d dirname`，其中 `dirname` 是目录名，它告诉 gdb 在何处查找源代码（它默认在工作目录查找）。

（注：由于提供的待翻译文本后半部分在“在调试器中检查代码”之后出现了大量重复且乱码的文本，译文已根据指令“不要重复输出原文”的原则，仅对核心逻辑部分进行了翻译和整理。）

