

# 使用 Red Hat Linux 提供的 C 语言管理工具

请记住，`gcc` 是你用来调用 GNU 编译器的命令。（本章稍后的“使用 GNU C 编译器”部分解释了 `-c` 和 `-o` 的含义。）

## 调试工具

调试既是一门科学，也是一门艺术。有时，简单的工具——代码列表——最好的调试工具。但在其他情况下，你可能需要使用其他的调试工具。其中三个是 `splint`、`gprof` 和 `gdb`。

### 使用 splint 检查源代码
`splint` 命令与传统的 UNIX `lint` 命令类似；它检查源代码中可能存在的问题，并且具有许多额外功能。即使你的 C 代码符合 C 标准并且能够编译通过，它仍然可能包含错误。`splint` 执行许多不同类型的检查，并可以提供详尽的错误信息。例如，这个简单的程序可能可以编译通过并运行：

```
$ gcc tux.c -o tux
$ ./tux
```

但 `splint` 命令可能会指出源码中的一些问题：

```
$ splint tux.c
splint 3.0.1.6 --- 27 May 2002
```

```
tux.c:(in function main)
tux.c:2:19: Return value (type int) ignored: putchar(t[++j]) ...
函数调用的返回值未被使用。如果这是刻意为之，可以将结果转换为 (void) 以消除该消息。（使用 -retvalint 抑制警告）
Finished checking --- 1 code warning
```

你可以像这样使用 `splint` 命令的 `-strict` 选项来获取更详细的报告：

```
$ splint -strict tux.c
```

GNU 编译器还支持通过使用大量的警告来提供诊断（通过 `-Wall` 和 `-pedantic` 选项：）：

```
$ gcc -Wall tux.c
tux.c:1: warning: return type defaults to `int`
tux.c: In function `main`
tux.c:2: warning: implicit declaration of function `putchar`
```

# 第 21 章 C/C++ 编程工具介绍

> 注意
如果你想探索各种 C 语法检查程序，请访问 http://www.biblio.org/pub/Linux/devel/lang/c/。`splint` 程序源自 `lint`，你可以在网站的 lclint-2.2a-src.tar.gz 文件中找到它。

# 使用 gprof 跟踪函数时间

你使用 `gprof`（分析）命令来研究程序是如何消耗时间的。如果程序在编译和链接时带有 `-p` 标志，在执行时会创建一个 `mon.out` 文件，其中包含每个函数被调用的频率以及在函数中花费时间的数据。`gprof` 会解析并显示这些数据。对 `gprof` 生成的输出进行分析可以帮助你确定性能瓶颈在哪里。使用优化编译器可以加快程序，但花时间使用 `gprof` 的分析并修改瓶颈函数可以显著提高程序性能。

# 使用 gdb 进行符号调试

`gdb` 工具是一个符号调试器。当程序使用 `-g` 标志编译时，会保留符号表，并可以使用符号调试器来跟踪程序错误。基本技术是在产生核心转储（core dump，一个包含崩溃程序所用用内存快照的文件）后调用 `gdb` 并获取栈回溯。栈回溯指示了发生核心转储的源代码行以及调用到该行的函数。通常，这就足够识别问题了。不过并不是 `gdb` 的极限。

`gdb` 还提供了一个交互式调试程序的环境。调用 `gdb` 运行程序允许你设置断点、检查变量的值并监控变量。如果你怀疑某行代码附近有问题，可以在该行设置断点并运行 `gdb`。当你遇到断点时，执行会被停止。你可以检查变量的值，单步执行程序并观察变量。

> 注意
如果你想探索各种 C 语法检查程序，请访问 http://www.biblio.org/pub/Linux/devel/lang/c/。`splint` 程序源自 `lint`，你可以在网站的 lclint-2.2a-src.tar.gz 文件中找到它。

# 使用 gprof 跟踪函数时间

（此处内容重复，根据指令要求不重复原文）

# 使用 gdb 进行符号调试

（此处内容重复）

# 使用 使用

  使用 C 语言编译器

> 注意
如果你想
http://www.biblio.org/pub/Linux/devel/lang/c/。` 编译器

# 22.1 选项

| 选项 | 说明 |
| :--- | :--- |
| -x | 指定语言 |
| -c | 仅编译 | |
| -S | 仅汇编 |
| -E | 仅预处理 |
| -o | 指定输出文件名 |
| -l | 指定库 |
| -I | 搜索目录 |
| -w | 抑制警告 |
| -pedantic | 要求 ANSI 标准 |
| -Wall | 打印额外的警告 |
| -g | 生成调试信息 |
| -p | 为 gprof 生成 |
| -pg | 为 gprof 生成 |

> 注意
你可以用 C 编写大型程序。C 程序可以拆分成任意数量的文件，只要没有一个函数跨越超过一个文件即可。

当你使用 `gcc` 构建 C 程序时，编译过程分为几个步骤：

- 第一，C 预处理器解析代码。在此过程中，它包含头文件并执行宏替换。
- 编译器解析代码。在此过程中，它构建符号表并创建目标文件。
- 最后的编译阶段是链接，通过解决尚未解析的符号将文件和库连接在一起。

> 注意
如果你遵循 ANSI 规则，你可以用 C++ 编译器编译。例如，你通常将文件命名为 hello.cc、hello.C、hello.cpp 或 hello.cxx。GNU 编译器接受这些名称。

#简单的 C 程序

本节提供了一个如何在 Linux 上创建可执行程序的简单示例。用 C 编写的最短程序之一是经典的“Hello World”程序（由 Brian W. Kernighan 和 Dennis M. Ritchie 在 1978 年的著作《C 语言》中推广）。

开始之前，使用你喜欢的 Linux 编辑器输入以下文本：```
main() {
    printf("hello, world.\n");
}
```

完成后，将文件保存为 hello.c，然后使用 gcc 编译器系统编译该程序：

```
$ gcc -o hello hello.c
```

该命令创建了一个名为 hello 的可执行程序，使用 hello.c 作为输入。然后你可以这样运行程序：

```
$ ./hello
hello, world.
```

该 C 程序只包含一个函数，名为 `main()`。gcc 命令行通过 `-o` 选项指定了输出程序的名称以及输入文件 hello.c。注意，为了运行新的 hello 命令，你必须显式指定它（使用点和斜杠字符），因为该程序没有安装在标准的命令目录（例如 /usr/bin 或 /usr/local/bin）。

