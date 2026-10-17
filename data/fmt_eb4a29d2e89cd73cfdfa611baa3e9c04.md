
## make 选项

| `-e` | 允许环境变量覆盖 `makefile` 中同名变量的定义。 |
| `-f FILE` | 将 `FILE` 作为 `makefile` 读取。 |
| `-h` | 显示 `make` 选项列表。 |
| `-i` | 忽略构建目标时执行的命令中的所有错误。 |
| `-I DIR` | 在指定目录中搜索包含的 `makefile`。（在 `makefile` 中包含文件的能力是 `GNU make` 独有的。） |
| `-j NUM` | 指定 `make` 可以同时运行的作业数。 |
| `-k` | 即使在构建其中一个目标时发生错误，也继续构建不相关的目标。 |
| `-l LOAD` | 如果负载平均值至少为 `LOAD`（浮点数），则不启动新作业。 |
| `-m` | 忽略给定的变量但接受该变量以兼容 `make` 的其他版本。 |
| `-n` | 打印要执行的命令但不执行它们。 |
| `-o FILE` | 不重建名为 `FILE` 的文件，即使它比其依赖项旧。 |
| `-p` | 显示变量和隐式规则的 `make` 数据库。 |
| `-q` | 不运行任何内容，但如果所有目标都是最新的则返回 `0`（零），如果需要更新则返回 `1`，如果发生错误则返回 `2`。 |
| `-r` | 去除所有内置规则。 |
| `-R` | 去除所有内置变量和规则。 |
| `-s` | 静默工作（不显示命令的执行情况）。 |
| `-t` | 更改文件的時間戳。 |
| `-v` | 显示 `make` 的版本号、许可信息和版权声明。 |
| `-w` | 在处理 `makefile` 之前和之后显示工作目录的名称。 |
| `-W FILE` | 假定指定文件已被修改（与 `-n` 一起使用以查看修改该文件时会发生什么）。 |

## GNU 调试器

虽然 `make` 自动执行构建程序的过程，但在程序无法正常工作或程序突然因错误消息退出时，编程中最令人担忧的部分并不是构建。你需要一个调试器来查找程序错误的根源。Linux 包含 `gdb` —— 具有命令行界面的多功能 `GNU` 调试器。

像任何调试器一样，`gdb` 让你执行典型的调试任务，例如以下内容：

- 在指定行设置断点，使程序在该处停止。
- 查看程序中变量的值。
- 一行一行地逐步执行程序。
- 更改变量以尝试纠正错误。

`gdb` 调试器可以调试 `C` 和 `C++` 程序。

## 为调试程序做准备

如果你想使用 `gdb` 调试程序，必须确保编译器在可执行文件中生成并放置调试信息。调试信息包含程序中变量的名称以及可执行文件中地址到源文件中代码行的映射。`gdb` 需要这些信息来执行其功能，例如在执行源代码的指定行后停止。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_482_0.png)

为了确保可执行文件已正确准备好进行调试，请使用 `-g` 选项与 `GCC` 或 `G++`。你可以通过在 `makefile` 中定义变量 `CFLAGS` 来完成此任务，如下所示

```
CFLAGS= -g
```

## 运行 gdb

调试程序最常见的方法是使用以下命令运行 `gdb`：

```
gdb progname
```

`progname` 是程序可执行文件的名称。`progname` 运行后，`gdb` 会显示以下消息并提示你输入命令：

```
GNU gdb (GDB) 7.5.91.20130417-cvs-ubuntu
Copyright (c) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later ---<http://gnu.org/licenses/gpl.html>
This is free software: you are free to change it and redistribute it.
There is NO WARRANTY, to the extent permitted by law. Type "show copying" and
"show warranty" for details.
This GDB was configured as "i686--linux-gnu".
For bug reporting instructions, please see:
http://www.gnu.org/software/gdb/bugs/.
(gdb)
```

你可以在 `(gdb)` 提示符下输入 `gdb` 命令。一个有用的命令 `help` 会显示命令列表，如下一列表所示：

```
(gdb) help
List of classes of commands:
aliases -- Aliases of other commands
breakpoints -- Making program stop at certain points
data -- Examining data
files -- Specifying and examining files
internals -- Maintenance commands
obscure -- Obscure features
running -- Running the program
stack -- Examining the stack
status -- Status inquiries
support -- Support facilities
tracepoints -- Tracing of program execution without stopping the program
user-defined -- User-defined commands
Type "help" followed by a class name for a list of commands in that class.
Type "help all" for the list of all commands.
Type "help" followed by command name for full documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)
```

要退出 `gdb`，输入 `q` 然后按 Enter。

`gdb` 有大量命令，但你只需要少数几个就能快速找到错误的根源。表 3-4 列出了常用的 `gdb` 命令。

## 表 3-4 常用 gdb 命令

| 此命令 | 执行以下操作 |
|---|---|
| `break NUM` | 在指定的行号 `NUM` 处设置断点。（调试器会在断点处停止。） |
| `bt` | 显示所有栈帧的回溯。（此命令显示迄今为止的函数调用序列。） |
| `clear FILENAME: NUM` | 删除源文件 `FILENAME` 中特定行号 `NUM` 处的断点。例如，`clear xdraw.c:8` 会清除文件 `xdraw.c` 第 `8` 行的断点。 |
| `continue` | 继续运行正在调试的程序。（在程序因信号或断点而停止后使用此命令。） |
| `display EXPR` | 每次程序停止时显示表达式 `EXPR`（由程序中定义的变量组成）的值。 |
| `file FILE` | 加载指定的可执行文件 `FILE` 进行调试。 |
| `help NAME` | 显示名为 `NAME` 的命令的帮助信息。 |
| `info break` | 显示当前断点列表，包括每个断点被命中的次数信息。 |
| `info files` | 显示正在调试的文件的详细信息。 |
| `info func` | 显示所有函数名。 |
| `info local` | 显示当前函数的局部变量信息。 |
| `info prog` | 显示正在调试程序的执行状态。 |
| `info var` | 显示所有全局和静态变量名。 |
| `kill` | 结束正在调试的程序。 |
| `list` | 列出源代码的一部分。 |
| `make` | 在不离开 `gdb` 的情况下运行 `make` 工具重建可执行文件。 |
| `next` | 在不进入其他函数的情况下推进当前函数的一行源代码。 |
| `print EXPR` | 显示表达式 `EXPR` 的值。 |
| `quit` | 退出 `gdb`。 |
| `run` | 开始运行当前加载的可执行文件。 |
| `set variable VAR=VALUE` | 将变量 `VAR` 的值设置为 `VALUE`。 |
| `shell CMD` | 在不离开 `gdb` 的情况下执行 `shell` 命令 `CMD`。 |
| `step` | 在当前函数中推进一行，如果有则进入其他函数。 |
| `watch VAR` | 每当变量 `VAR` 的值发生变化时显示其值。 |
| `where` | 显示调用序列。使用此命令定位程序崩溃的位置。 |
| `x/F ADDR` | 以字母 `F` 指定的格式检查地址 `ADDR` 处的内存位置内容，`F` 可以是 `o`（八进制）、`x`（十六进制）、`d`（十进制）、`u`（无符号十进制）、`t`（二进制）、`f`（浮点）、`a`（地址）、`i`（指令）、`c`（字符）或 `s`（字符串）。你可以在格式字母后附加表示数据类型大小的字母。大小字母为 `b`（字节）、`h`（半字，2 字节）、`w`（字，4 字节）和 `g`（巨型，8 字节）。通常，`ADDR` 是变量或指针的名称。 |
