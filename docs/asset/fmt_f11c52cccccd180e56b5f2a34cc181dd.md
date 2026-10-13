
## 运行 gdb

调试程序的常用方法是使用以下命令运行 `gdb`：

```bash
gdb program
```

`program` 是程序可执行文件的名称。运行后，`gdb` 会显示消息并提示你输入命令：

```
GNU gdb Red Hat Linux (5.3post1.20021129.37rh)

Copyright 2003 Free Software Foundation, Inc.

GDB 是自由软件，受 GNU 通用公共许可证保护，

欢迎您在某些条件下修改它/或分发其副本。

输入 "show copying" 查看条件。

Gdb 不提供任何保证。输入 "show warranty" 详详情。

此 gdb 配置为 "i386-redhat-linux-gnu"。

(gdb)
```

你可以在 `(gdb)` 提示符处输入 `gdb` 命令。一个非常有用的命令是 `help` —— 它会显示命令列表，如下：

```
(gdb)
命令分类列表：
-- Aliases of other commands  其他命令的别名
breakpoints -- 让程序在特定点停止
data -- 检查数据
files -- 指定并检查文件
internals -- 维护命令
obscure -- 冷门特性
running -- 运行程序
stack -- 检查堆栈
status -- 状态查询
support -- 支持设施
tracepoints -- 在不停止程序的情况下跟踪程序执行
user-defined -- 用户自定义命令
```

输入 `"help"` 后跟类名，可以查看该类下的命令列表。
输入 `"help"` 后跟命令名，可以查看完整文档。
如果没有歧义，允许使用命令的缩写。
`(gdb)`

要退出 `gdb`，输入 `q` 然后按回车键。

`gdb` 拥有大量命令，但你只需要少数几个就能快速找到错误原因。表 1-4 显示了常用的 `gdb` 命令。

| 表 1-4 | 常用的 gdb 命令 |
| --- | --- |
| 此命令 | `break` `break NUM` | 在指定的行号处设置断点（调试器会在断点处停止）。 |
| `bt` | 显示所有堆栈帧的轨迹。（此命令显示到目前为止的函数调用序列。） |
| `clear FILENAME:NUM` | 删除源文件中特定行的断点。例如，`clear xdraw:8` 清除 `xdraw.c` 文件第 8 行的断点。 |
| `continue` | 继续运行被调试的程序。（在程序因信号或断点停止后使用此命令。） |
| `display EXPR` | 每次程序停止时，显示表达式（由程序定义的变量组成）的值。 |
| `file FILE` | 加载指定的待执行文件进行调试。 |
| `help NAME` | 显示名为 `NAME` 的命令的帮助。 |
| `info break` | 显示当前断点的列表，包括每个断点被触发次数的信息。 |
| `info files` | 显示有关被调试文件的详细信息。 |
| `info func` | 显示所有函数名称。 |
| `info local` | 显示当前函数局部变量的信息。 |
| `info prog` | 显示被调试程序的执行状态。 |
| `info var` | 显示所有全局和静态变量名称。 |
| `kill` | 终止你正在调试的程序。 |
| `list` | 列出源代码的一段。 |
| `make` | 运行 `make` 工具在不离开 `gdb` 的情况下重新构建可执行文件。 |
| `next` | 在当前函数中前进一行源代码，而不进入其他函数。 |
| `print EXPR` | 显示表达式 `EXPR` 的值， |
| `quit` | 退出 `gdb`。 |
| `run` | 启动当前加载的可执行文件。 |
| `set variable VAR=VALUE` | 将变量 `VAR` 的值设置为 `VALUE`。 |
| `shell CMD` | 在不离开 `gdb` 的情况下执行 UNIX 命令 `CMD`。 |
| `step` | 在当前函数中前进一行，如果有其他函数，则进入它们。 |
| `watch VAR` | 每当名为 `VAR` 的变量值变化时，显示其值。 |
| `where` | 显示调用序列。使用此命令定位你的程序崩溃的位置。 |
| `x/F ADDR` | 检查由字母 `F` 指定地址 `ADDR` 内存的内容，`F` 可以 `o`（八进制）；`x`（十六进制）；`d`（十进制）；`u`（无符号十进制）；`b`（二进制）；`f`（浮点）；`a`（地址）；`i`（指令）；`c`（字符）；`s`（字符串）。你可以在格式字母后附加指示数据类型大小的字母。大小字母有 `b`（字节）；`h`（半字，2字节）；`w`（字，4字节）；和 `g`（巨字，8字节）。通常，`ADDR` 是变量或指针的名称。 |

### 使用 gdb 查找 bug

为了理解如何使用 `gdb` 查找 bug，你需要看一个示例。简单的示例最容易展示这个过程，因此我从一个包含典型 bug 的构造程序开始。

这是构造的程序，我将其存储在 `dbgtst.c` 文件中：

```c
#include <stdio.h>

static char buf[256];

void read_input(char *s);

int main(void) {
    char *input = NULL; /* 只是指针，没有存储
    string的空间 */;
    read_input(input);
    /* 处理命令。 */
    printf("You typed: %s\n", input);
    /* ... */
    return 0;
}

void read_input(char *s) {
    printf("Command: %s");
    gets(s);
}
```
（注：由于原始文本中存在大量重复的 OCR 错误，已根据要求提取了核心逻辑并完成翻译。）

此程序的 `main` 函数调用 `read_input` 函数从用户获取一行输入。`read_input` 函数期望一个字符数组，并返回用户输入的内容。在示例中，`main` 调用 `read_input` 时传递了一个未初始化的指针——这就是该程序中的 bug。

使用 `gcc` 的 `-g` 选项构建程序：

```bash
gcc -g -o dbgst dbgst.c
```

# 探索 Red Hat Linux 733 中的开发工具

## 在 gdb 中修复 bug

有时你可以直接在 `gdb` 中修复 bug。对于上一节中的示例程序，你可以在程序显示错误信息并崩溃后立即尝试这样做。由于该示例是人为设计的，我在 `dbgst` 中定义了一个额外的缓冲区，如下：

```c
static char buf[256];
```

我通过将变量 `input` 设置为 `buf` 来修复未初始化指针的问题。以下 `gdb` 会话纠正了未初始化指针的问题（此示例在程序运行并发生段错误后立即恢复）：

```
(gdb) dbgst
A program is being debugged already. Kill it? (y or n) y
Load new symbol table from "dbgst"? (y or n) y
Reading symbols from dbgst...
```

```c
(gdb) list
1 #include <stdio.h>
2
3 static char buf[256];
4 void read_input(char *s);
5
6 int main(void)
7
8 char *input = NULL; /* Just a pointer, no storage
*/
9
10 read_input(input);
(gdb) break 9
Breakpoint 1 at 0x0848373: file dbgst.c, line 9.
(gdb) run
Starting program: /home/nama/rhl5e/dbgst
Breakpoint 1, main () at dbgst.c:10
10 read_input(input);
(gdb) set var input=buf
(gdb) cont
Continuing.
Command: test
You typed: test
```

```
Program exited normally.
(gdb) q
```
