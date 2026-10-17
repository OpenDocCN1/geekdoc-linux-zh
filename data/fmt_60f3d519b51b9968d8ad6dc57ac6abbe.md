
在这个示例中，`CXX` 和 `CXXFLAGS` 是变量。GNU make 倾向于将它们称为变量，但大多数 UNIX 系统将它们称为宏。

要在 Makefile 的任何地方使用变量，请以美元符号 (`$`) 开头，后跟括号内的变量。GNU make 将变量的所有出现处替换为其定义；因此，它会将所有 `$(CXXFLAGS)` 的出现处替换为字符串 `-O2 -g -m486`。

GNU 有几个具有特殊含义的预定义变量。表 23-2 列出了这些变量。除了表 23-2 中列出的变量外，GNU make 还认为所有的环境变量都是预定义的。

| 表 23-2 GNU make 中的一些预定义变量 |
| 变量 | 含义 |
| `$%` | 归档目标的成员名称。例如，如果目标是 `libDisp.(image.o)`，则 `$%` 是 `image.o`，而 `%@` 是 `libDisp.` |
| `$*` | 不带扩展名的目标文件名 |
| `$+` | 所有具有重复依赖的依赖文件名称，按其出现顺序列出 |
| `$<` | 第一个依赖文件的名称 |
| `??` | 比目标新的所有依赖文件名称（名称之间用空格） |
| `$@` | 目标的完整名称 |
| `$^` | 所有依赖文件的名称，名称之间用空格。文件名中的重复项移除 |
| `AR` | 归档维护程序的名称（默认值: `ar`） |
| `ARFLAGS` | 归档维护程序的标志（默认值: `rv`） |
| `AS` | 将汇编语言转换为目标代码的汇编程序名称（默认值: `as`） |

### 第 23 章：Linux 下的软件开发

| 变量 | 含义 |
| --- | --- |
| `ASFLAGS` | 汇编器的标志 |
| `CC` | C 编译器的名称。（默认值: `cc`） |
| `CFLAGS` | 传递给 C 编译器的标志 |
| `CO` | 从 RCS 提取文件的程序名称（默认值: `co`） |
| `COFLAGS` | RCS `co` 程序的标志 |
| `CPP` | C 预处理器的名称（默认值: `$(CC) -E`） |
| `CPPFLAGS` | C 预处理器的标志 |
| `CXX` | C++ 编译器的名称（默认值: `g++`） |
| `CXXFLAGS` | 传递给 C++ 编译器的标志 |
| `FC` | FORTRAN 编译器的名称（默认值: `f77`） |
| `FFLAGS` | FORTRAN 编译器的标志 |
| `GET` | 从 SCCS 提取文件的程序名称（默认值: `get.`） |
| `GFLAGS` | SCCS `get` 程序的标志 |
| `LDFLAGS` | 编译器调用链接器时的标志 1 |
| `LEX` | 将 Lex 语法转换为 C 程序的程序名称（默认值: `lex`） |
| `LFLAGS` | Lex 的标志 |
| `MAKEINFO` | 将 Texinfo 源文件转换为 info 文件的程序名称（默认值: `makeinfo`） |
| `RM` | 删除文件的命令名称（默认值: `rm -f`） |
| `TEX` | 从 TeX 源文件生成 TeX DVI 文件的程序（默认值: `tex`） |
| `TEXI2DVI` | 从 Texinfo 源生成 TeX DVI 文件的程序（默认值: `texi2dvi`） |
| `YACC` | 将 YACC 语法转换为 C 程序的程序名称（默认值: `yacc -r`） |
| `YFLAGS` | `yacc` 的标志 |

#### 隐式规则

GNU make 还包含内置的、或隐式的规则，这些规则定义了如何从各种依赖项创建特定类型的目标。隐式规则的一个示例是 make 执行的从 C 源文件生成对象文件的命令。

`make` 支持两种类型的隐式规则：

- 后缀规则（Suffix rules）——后缀规则定义了 make 的隐式规则。后缀规则定义了如何将具有某种扩展的文件转换为具有另一种扩展的文件。每个后缀规则由一对后缀定义。例如，将 `.c` 文件转换为 `.o`（对象）文件的后缀规则可能写成：
```make
$(CC) $(CFLAGS) -c -o
```
此规则使用了预定义变量 `CC`、`CFLAGS` 和 `CPPFLAGS`。该规则使用了（目标的完整名称）和（第一个文件名）。

- 模式规则（Pattern rules）——这些规则更灵活，因为你可以使用模式规则指定复杂的依赖关系。模式规则看起来像普通规则，只是目标名称中出现了百分号 (`%`)。依赖使用 `%` 来指示它们与目标的关系。以下模式规则指定了如何将任何文件 X 转换为文件 X.o：
```make
%:o
$(CC) $(CFLAGS) -c -o
```

GNU make 拥有大量的隐式规则，分为后缀规则和模式规则。要查看所有变量和规则，请通过以下命令运行：

```
make -p
```

```
# GNU Make 版本 3.9 由 Stallman 和 Roland McGrath 编写
# 为 i386-linux 编译
# Copyright (C) 1989-2000 Free Software Foundation, Inc.
# 这是自由软件；用于复制。
# 即使对于 FITNESS 也没有保证。
make: *** targets. Stop.
* Make 数据，打印于 11 月 25 日 16:28:56
# 变量
（已删除）
# 默认
CC = cc
# 默认
COMPILE = $(CC) $(CFLAGS) $(CPPFLAGS) -c
（已删除）
# 默认
OUTPUT_OPTION = -o
MAKE_VERSION := 3.9
（已删除）
# 隐式规则
%.o:
# 执行的命令（内置）：
$(COMPILE) $(OUTPUT_OPTION)
（已删除）
```

列表显示了当你使用 `-p` 选项时 GNU make 显示的部分输出。输出包含了变量名称以及隐式规则。

#### 示例 Makefile

使用 GNU make 的预定义变量和内置规则，你可以轻松创建一个 Makefile。例如，一个由三个 C 源文件（`xdraw.c`、`xiewobj.c` 和 `shapes.c`）和两个头文件（`xdraw.h` 和 `shapes.h`）生成可执行文件 `xdraw` 的 Makefile。假设每个源文件都包含一个头文件。给定这些事实，示例 Makefile 可能如下：

```make
############################################
# 示例 Makefile
# 注释以 '#' 开头
#
############################################
```

```make
# 使用标准变量定义编译和链接标志
CFLAGS= -g -O2
# 定义目标 "all"
all: xdraw
```

```make
OBJS=xdraw.o xiewobj.o shapes.o
xdraw: $(OBJS)
```

```make
# 对象文件
xdraw.o: Makefile xdraw.c xdraw.h
```

```make
xiewobj.o: Makefile xiewobj.c shapes.h
```

此 Makefile 依赖于 GNU make 的隐式规则。.c 文件到 .o 文件的转换使用了内置规则。定义变量 `CFLAGS` 将标志传递给 C 编译器。

将名为 `all` 的目标定义为第一个目标有一个原因——如果你不在指定目标的情况下运行 GNU make（见下节的 make 语法），它将构建在 Makefile 中找到的第一个目标。通过将第一个目标定义为 xdraw，你可以确保 make 构建此可执行文件，即使你没有显式地指定它。UNIX 程序员传统上使用 `all` 作为第一个目标的名称，但目标的名称并不重要；重要的是它是 Makefile 中的第一个目标并最终退出。

如果你有一个包含相应源文件和头文件的目录，你可以尝试该 Makefile。以下是我尝试示例 Makefile 时发生的情况：

```
make
cc -g -O2 -c xdraw.c -o xdraw.o
cc -g -O2 -c xiewobj.c -o xiewobj.o
cc -g -O2 -c shapes.c -o shapes.o
cc xdraw.o shapes.o -o xdraw
```

如 make 的输出所示，它使用了 `cc` 命令（在你的 Linux 系统中是 GCC 的符号链接）配合适当选项来编译源文件，最后链接对象创建 xdraw 可执行文件。

#### 如何运行 make

通常，你在命令行中通过单个命令运行 make；即你通过输入 `make` 来运行 make。运行时，GNU make 会寻找名为 `GNUmakefile`、`make` 或 `Makefile` 的文件——按顺序找到其中一个 Makefile 后，它构建该 make 中指定的第一个目标。然而，如果 make 没有找到合适的 Makefile，它会显示以下错误消息并退出：

```
make: *** targets. Stop.
```

如果你的 make 名称恰好与默认名称不同，你必须使用 `-f` 选项来指定 Makefile。该 make 选项的语法如下：

```
make -f filename
```

其中 `filename` 是 Makefile 的名称。

即使你有一个默认名称（如 `Makefile`）的 Makefile，你可能也想从多个目标中构建特定的目标。在这种情况下，你可以使用以下语法运行 make：

```
make target
```

如果 Makefile 中包含名为 `clean` 的目标，你可以通过此命令构建该目标：

```
make clean
```

```
make CFLAGS="-g -O2"
```

除了这些选项外，GNU make 还接受其他几个命令行选项。表 23-3 列出了 GNU make 的选项。

| 选项 | 含义 |
|---|---|
| `-b` | 忽略但为了与其它版本的 make 兼容而接受。 |
| `-C DIR` | 在读取 makefile 之前切换到指定的目录。 |
| `-d` | 打印调试信息。 |
| `-e` | 环境变量覆盖 makefile 中同名变量的定义。 |
| `-f FILE` | 读取 makefile。 |
| `-h` | 显示 make 选项列表。 |
| `-i` | 忽略构建目标时执行的命令中的所有错误。 |
| `-I DIR` | 在指定目录搜索包含的makefile（在 makefile 中包含文件的功能是 GNU make 特有的）。 |
| `-j NUM` | 指定可以同时运行的命令数。 |
| `-k` | 即使在构建某个目标时发生错误，也继续构建无关的目标。 |
| `-l LOAD` | 如果负载平均至少达到 LOAD（浮点数），不启动新作业。 |
| `-m` | 忽略但为了与其它版本的 make 兼容而接受。 |
| `-n` | 打印将执行的命令，但不执行它们。 |
| `-o FILE` | 即使指定的 FILE 比其依赖项旧，也不重新构建。 |
| `-p` | 显示变量和隐式规则的 make 数据库。 |
| `-q` | 不运行任何操作，但如果所有目标都是最新的则返回零；如果有需要更新的返回一；发生错误则返回二。 |
| `-r` | 移除所有内置规则。 |
| `-R` | 移除所有内置变量和规则。 |
| `-s` | 静默工作（不显示执行的命令）。 |
| `-t` | 修改文件的时间戳。 |
| `-v` | 显示 make 版本号和版权声明。 |
| `-w` | 在处理 makefile 前后显示工作目录的名称。 |
| `-W FILE` | 假设指定文件已修改（配合 -n 使用查看修改该文件会发生什么）。 |

### GNU 调试器

虽然 make 自动化了程序的构建，但当程序运行不正常或带有错误消息突然退出时，这并不是你最担心的问题。你需要一个调试器来找到程序错误的原因。这本书的附带 CD-ROM 包含了 `gdb`——一个具有命令行界面的通用 GNU 调试器。CD-ROM 还包含 `xdb`，这是一个基于 Windows 系统的 `gdb` 图形化前端。

与任何调试器一样，`gdb` 允许你执行典型的调试任务，如下：

- 设置断点，使程序执行在指定行停止。
- 观察程序中变量的值。
- 逐行执行程序。
- 尝试更改变量以修复错误。

`gdb` 调试器可以调试 C 和 C++ 程序。

#### 为调试准备程序

如果你想使用 `gdb` 调试程序，就必须确保编译器生成并将调试信息放置在可执行文件中。调试信息包含了程序中变量的，以及可执行文件中的地址与源文件中代码行之间的映射。`gdb` 需要这些信息来执行其功能，例如在执行指定的源代码行后停止。

为了确保可执行文件已为调试准备就，请使用 GCC 的 `-g` 选项。你可以通过在 Makefile 中定义变量 `CFLAGS` 来：

```
CFLAGS=-g
```

#### 运行 gdb

调试程序最常用的方法是使用以下命令运行 `gdb`：

```
gdb progname
```

**`progname`** 是程序可执行文件的名称。运行它后，`gdb` 会显示以下消息并提示你输入命令：

```
GNU Red Hat Linux 7.x (5.0-15) (MI_OUT)
Copyright 2001 Free Software Foundation, Inc.
GDB 是免费软件，受 GNU 通用公共许可证保护，欢迎在特定条件下修改它并分发其副本。
输入 "show copying" 查看条件。
GDB 不提供任何保证。输入 "show warranty" 详情。
此 GDB 配置为 "i386-redhat-linux"。
(gdb) help
```

命令类别列表：

- aliases -- 其他命令的别名
- breakpoints -- 让程序在某些点停止
- data -- 检查数据
- files -- 指定和检查文件
- internals -- 维护命令
- obscure -- 晦涩特性
- running -- 运行程序
- stack -- 检查栈
- status -- 状态查询
- support -- 支持设施
- tracepoint -- 在不停止程序的情况下跟踪程序执行
- user-defined -- 用户定义命令

输入 "help" 后跟类名可查看该类别的命令列表。
输入 "help" 后跟命令名可查看完整文档。
如果没有歧义，允许使用命令缩写。
```
(gdb) q
```

**初始消息显示了 `gdb` 命令的类别。** 你可以按照指令获取特定类别命令或特定命令的进一步帮助。要查看用于运行你正在调试的程序的命令列表，请在 `gdb` 提示符处输入 `help running`。
要退出 `gdb`，输入 `q` 并按回车。

`gdb` 有大量命令，但你只需要少数几个快速找到错误原因。表 23-4 列出了常用的 `gdb` 命令。

| 表 23-4 常用的 gdb 命令 | 描述 |
|---|---|
| `break` | 在行处设置断点。 |
| `bt` | 显示帧轨迹。 |
| `clear` | 删除行处的断点。 |
| `continue` | 继续运行程序。 |
| `display` | 每当表达式变化时显示。 |
| `file` | 加载指定的文件。 |
| `help` | 显示命令的帮助。 |
| `info` | 显示信息。 |
| `info break` | 显示断点列表。 |
| `info files` | 显示文件信息。 |
| `info func` | 显示函数名。 |
| `info local` | 显示局部变量。 |
| `info prog` | 显示程序状态。 |
| `info var` | 显示全局变量。 |
| `kill` | 结束程序。 |
| `list` | 列出源代码段。 |
| `make` | 运行 make 工具。 |
| `next` | 进一行代码。 |
| `print` | 显示表达式的值。 |
| `quit` | 退出 gdb。 |
| `shell` | 执行 UNIX 命令。 |
| `set variable` | 设置变量的值。 |
| `step` | 进入其他函数。 |
| `watch` | 观察变量。 |
| `where` | 定位程序位置。 |

#### 使用 gdb 寻找漏洞

为了理解如何使用 `gdb` 寻找漏洞，你需要一个示例。这个过程通过简单的示例更容易展示，因此我从一个包含漏洞的构造程序开始。

这是构造程序，我将其存储在 `dbgtest.c` 文件中：

```
#include <stdio.h>
static char buf[256];
void read_input(char *s);
int main(void) {
    char *input = NULL; /* 只是指针，没有存储空间 */
    read_input(input);
    /* 处理命令。 */
    printf("You typed: %s\n", input);
    /* ... */
    return 0;
}
void read_input(char *s) {
    printf("Command: ");
    gets(s);
}
```

该程序的 `main` 函数调用 `read_input` 函数来从用户处获取行输入。`read_input` 函数期望一个字符数组来返回用户输入的内容。然而，在这个示例中，`main` 使用未初始化的指针调用了 `read_input`——这就是这个简单程序的漏洞。

使用带有 `-g` 选项的 `gcc` 构建程序：

```bash
gcc -o dbgtest dbgtest.c
```

忽略关于 `gets()` 函数危险的警告信息；我们正试图通过利用该函数的缺点来展示如何使用 `gdb` 跟踪错误。

要查看此程序的问题，运行它：

```
./dbgtest
Command: test
Segmentation fault
```

程序在显示段错误（Segmentation fault）消息后崩溃。对于这个小程序，你可以通过检查源代码找到原因。在现实世界的应用程序中，你可能无法立即知道是什么导致了错误。这就是你使用 `gdb` 找到问题原因的时候。

要使用 `gdb` 定位错误，请遵循以下步骤：

- 1. 在 `gdb` 中加载程序。若要在 `gdb` 中加载一个名为 `dbgtst` 的程序，请输入以下命令：
```
