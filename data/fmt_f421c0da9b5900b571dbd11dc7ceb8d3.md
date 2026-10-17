
除了这些选项外，GNU `make` 还接受若干命令行选项。表 3-3 列出了这些选项。

### 表 3-3：GNU make 的选项

| 选项 | 含义 |
| :--- | :--- |
| `-b` | 忽略给定的变量，但与其他版本的 `make` 兼容。 |
| `-C DIR` | 在读取 `makefile` 之前切换到目录。 |
| `-d` | 打印调试信息。 |
| `-e` | 允许环境变量覆盖 `makefile` 中的定义。 |
| `-f FILE` | 将 `FILE` 作为 `makefile`。 |
| `-h` | 显示 `make` 选项列表。 |
| `-i` | 构建目标时忽略所有错误。 |
| `-I DIR` | 在指定目录搜索包含的 `makefile`。（在 `makefile` 中包含文件是 GNU make 的特性。） |
| `-j NUM` | 指定 `make` 同时运行的作业数。 |
| `-k` | 在构建某个目标时发生错误时，继续构建无关的目标。 |
| `-l LOAD` | 如果负载至少为 *LOAD* 则不启动新作业（一个浮点数）。 |
| `-m` | 忽略给定的变量，但与其他版本的 `make` 兼容。 |
| `-n` | 打印将执行的命令但不执行它们。 |
| `-o FILE` | 即使文件比其依赖项旧，也不重新构建名为 *FILE* 的文件。 |
| `-p` | 显示 `make` 的变量和隐式规则数据库。 |
| `-q` | 不运行任何操作，但如果所有目标都是新的则返回 0，如果有更新返回 1，如果发生错误则返回 2。 |
| `-r` | 移除所有内置规则。 |
| `-R` | 移除所有内置变量和规则。 |
| `-s` | 静默工作（不显示执行的命令）。 |
| `-t` | 修改文件的时间戳。 |
| `-v` | 显示 `make` 版本版本、许可信息和版权声明。 |
| `-w` | 在处理 `makefile` 之前之后显示工作目录的名称。 |
| `-W FILE` | 假设指定的文件已修改（配合 `-n` 使用以查看修改该文件会发生什么）。 |

## GNU 调试器

尽管 `make` 自动化了程序的构建过程，但当程序运行异常或突然带有错误消息退出时，那部分工作并不是你最需要担心的。你需要一个调试器来找到程序错误的原因。Linux 包含了 `gdb` —— 这是一个带有命令行界面的多功能 GNU 调试器。

与其他任何调试器一样，`gdb` 允许你执行典型的调试任务，如下：

- 设置断点，使程序在指定的行停止。
- 观察程序中变量的值。
- 逐行执行程序。
- 尝试修改变量以纠正错误。

`gdb` 调试器可以调试 C 和 C++ 程序。

### 准备调试程序

如果你想使用 `gdb` 调试程序，你必须确保编译器生成并将调试信息放置在可执行文件中。调试信息包含了你程序中变量的名称，以及可执行文件中的地址到源文件中代码行的映射。`gdb` 需要这些信息来执行其功能，例如在执行完指定的源代码行后停止。

为了确保可执行文件已为调试做好良好准备，请在使用 GCC 或 G++ 时使用 `-g` 选项。你可以通过在 `makefile` 中定义变量 `CFLAGS` 来完成此任务：

`CFLAGS= -g`

### 运行 gdb

调试程序的常用方法是使用以下命令运行 `gdb`：

`gdb progname`

`progname` 是程序可执行文件的名称。在 `progname` 运行后，`gdb` 显示以下消息并提示你输入命令：

```
GNU gdb (GDB) 7.5.91.20130417-cvs-ubuntu
Copyright (c) 2013 Free Software Foundation, Inc.
License GPLv3`: `: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change it and redistribute it.
There is NO WARRANTY, to the extent permitted by law. Type "show copying" and "show warranty" for details.
This GDB was configured as "i686--linux-gnu".
For bug reporting instructions, please see:
http://www.gnu.org/software/gdb/bugs/.
(gdb)
```

你可以在 `(gdb)` 提示符下输入 `gdb` 命令。一个非常有用的命令 `help` 可以显示命令列表，如下列表所示：

```
(gdb) help
List of classes of commands:
- aliases -- 其他命令的别名
- breakpoints -- 让程序在某些点停止
- data -- 检查数据
- files -- 指定并检查文件
- internals -- 维护命令
- obscure -- 冷门特性
- running -- 运行程序
- stack -- 检查栈
- status -- 状态查询
- support -- 支持设施
- tracepoints -- 在不停止程序的情况下跟踪程序执行
- user-defined -- 用户定义的命令

输入 "help" 后跟类名可以获取该类命令的列表。
输入 "help all" 可以获取所有命令的列表。
输入 "help" 后跟命令名称可以查看完整文档。
如果没有产生歧义，允许使用命令缩写。
(gdb)
```

要退出 `gdb`，输入 `q` 然后按回车。

`gdb` 拥有大量的命令，但你只需要几个就能快速找到错误原因。表 3-4 列出了常用的 `gdb` 命令。

### 常用 gdb 命令

| 命令 | 功能 |
| :--- | :--- |
| `break NUM` | 在指定的行 *NUM* 处设置断点。（调试器会在断点处停止。） |
| `bt` | 显示所有栈帧的轨迹溯（此命令向你显示到目前为止的函数调用序列。） |
| `clear FILENAME: NUM` | 删除源文件 *FILENAME* 中特定行 *NUM* 处的断点。例如，`clear xdraw.c:8` 会清除 `xdraw.c` 第 8 行的断点。 |
| `continue` | 继续运行正在调试的程序（在程序因信号或断点停止后使用此命令）。 |
| `display EXPR` | 每次程序停止时显示表达式 *EXPR*（由程序中定义的变量组成）的值。 |
| `file FILENAME` | 加载指定的调试用可执行文件 *FILE*。 |
| `help NAME` | 显示命令 *NAME* 的帮助信息。 |
| `info break` | 显示当前断点的列表，包括每个断点被触发次数的信息。 |
| `info files` | 显示关于正在调试的文件的详细信息。 |
| `info func` | 显示所有函数名称。 |
| `info local` | 显示当前函数局部变量的信息。 |
| `info prog` | 显示程序的执行状态。 |
| `info var` | 显示所有全局和静态变量名称。 |
| `kill` | 结束程序调试。 |
| `list` | 列出源代码的一部分。 |
| `make` | 运行 `make` 工具在不离开 `gdb` 的情况下重新构建可执行文件。 |
| `next` | 在当前函数中前进一行源代码，且不进入其他函数。 |
| `print EXPR` | 显示表达式 *EXPR* 的值。 |
| `quit` | 退出 `gdb`。 |
| `run` | 运行加载的可执行文件。 |
| `set variable VAR=VALUE` | 将变量 *VAR* 设置为 *VALUE*。 |
| `shell CMD` | 在不离开 `gdb` 的情况下执行 shell 命令 *CMD*。 |

### 使用 gdb 查找错误

为了理解如何使用 `gdb` 查找错误，你需要看一个示例。最简单的方法是通过简单的示例来展示，下面的 `dbgtst.c` 是一个包含典型错误的程序：

```c
#include <stdio.h>

static char buf[256];

void read_input(char *s);

int main(void)
{
    char *input = NULL; /* 只是指针，没有存储空间 */
    read_input(input);
    /* 处理命令。 */
    printf("You typed: %s\n", input);
    /* ... */
    return 0;
}

void read_input(char *s)
{
    printf("Command: ");
    gets(s);
}
```
