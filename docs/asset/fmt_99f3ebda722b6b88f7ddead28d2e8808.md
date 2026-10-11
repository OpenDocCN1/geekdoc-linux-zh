
`make` 如何知道如何从 `aux.c` 变成 `aux.o`？毕竟 `aux.c` 并不在 Makefile 中。答案是 `make` 遵循了它的内置规则。它知道当你想要 `.o` 文件时对应的 `.c` 文件，而且它还知道对 `.c` 文件运行 `cc -c` 来实现创建 `.o` 文件的目标。

获取 `myprog` 的最后一步有点复杂，但思路很清楚。一旦你在 `$(OBJ3)` 中有了两个对象文件，你就可以根据以下行运行 `cc` 编译器，其中 `$(CC)` 展开为编译器名称：

```
$(CC) - myprog $(OBJ3)
```

特别注意 `$(CC)` 之前的空格。这是一个制表符（tab）。在任何实际命令之前你必须放置一个制表符，并且它必须单独成一行。注意这个：

```
Makefile:7: *** missing separator. Stop.
```

类似这样的错误意味着 Makefile 损坏了。制表符是分隔符，如果没有分隔符或其他其他干扰，你就会看到这个错误。

## 保持更新

`make` 的基本原理之一是目标与其依赖项保持同步。如果你对前面的示例连续输入两次 `make`，第一个命令会构建 `myprog`，但第二个命令产生以下输出：

```
make: Nothing to be done for `all`.
```

对于这个特定的过程，`make` 查看了它的规则并发现 `myprog` 已经存在。具体来说，`make` 没有构建 `myprog` 是因为自上次构建 `myprog` 以来，没有任何依赖项发生过变化。你可以尝试实验：

- 1. 运行 `touch aux.c`。
- 2. 再次运行 `make`。这次，`make` 发现 `aux.c` 比目录中已 `aux.o` 新，它必须重新编译 `aux.o`。
- 3. `myprog` 依赖于 `aux.o`，现在 `aux.o` 比预存 `myprog` 新，所以 `make` 必须创建 `myprog`。

这种链式反应非常典型。

## 命令行选项

如果你知道 `make` 的命令行选项是如何工作的，就可以让它发挥巨大的作用。

最常见的 `make` 选项是在命令行上指定单个目标。对于前面的 Makefile，如果你只需要 `aux.o` 文件，可以运行 `make aux.o`。

你还可以在命令行上定义宏。假设你想使用一个名为 `my_bad_cc` 的不同编译器。尝试一下这个：

```
make CC=my_bad_cc
```

在这里，`make` 使用你对 `CC` 的定义，而不是它的默认编译器 `cc`。当你测试自己的预处理器定义和库时，命令行宏会非常有用，特别是稍后会解释的 `CFLAGS` 和 `LDFLAGS` 宏。

你甚至不需要运行一个 Makefile。如果内置的 `make` 匹配到一个目标，你只需要要求 `make` 创建该目标即可。例如，如果你有一个非常简单的程序 `blah.c` 的源码，尝试运行 `make blah`。`make` 的运行会尝试执行命令：

```
cc blah.o -o blah
```

这种 `make` 的用法仅适用于最基本的 C 程序；如果你的程序需要库或特殊的包含目录，编写一个 Makefile 可能更好。

在没有 Makefile 的情况下运行 `make` 在在你处理的不是 C 程序，而是像 Fortran、x、yacc 等东西时实际上有用。弄清楚编译器或工具的工作原理可能非常痛苦，为什么不让 `make` 尝试为你弄清楚呢？即使 `make` 未能创建目标，它可能仍然给你一个相当不错的提示，告诉你可能如何使用该工具。还有两个 `make` 选项脱颖而出：

- `-n` 打印构建所需的命令，但防止 `make` 实际运行任何命令。
- `-f file` 告诉 `make` 从文件而不是 Makefile 或 makefile 读取。

## 标准宏和变量

`make` 拥有特殊的宏和变量。很难区分宏和变量之间的区别，因此本书使用“宏”一词指代在 `make` 开始构建目标后通常不会改变的内容。正如你之前所看到的，你可以在 Makefile 的开头设置宏。以下列表包括：

- `CFLAGS`: 编译器选项。在创建对象文件时，`make` 将其作为参数传递。
- `LDFLAGS`: 类似于 `CFLAGS`，但用于链接器。
- `CC`: 编译器。默认是 `cc`。
- `CPPFLAGS`: 预处理器选项。当 `make` 运行预处理器时，它将其作为参数传递。
- `CXXFLAGS`: GNU 用于 C++ 的标志。
- `$@` 展开为目标文件名。例如，如果你正在构建 `blah.o`，它展开为 `blah`。
- `$*` 展开为目标的所有前提条件。

Linux 上最完整的 make 变量列表见 make 页面。

> 注意 记住，make 有许多扩展、内置规则和功能是其他变体没有的。只要你运行的是 Linux 就没事，但如果你在一个 BSD 机器上，可能会大吃一惊。

## 组织 Makefile

尽管有许多 Makefile 风格，但大多数程序员仍然遵循一些通用原则。

在 Makefile 的第一部分（宏定义内部），你应该看到根据包分组的库和包含文件：

```
X_INCLUDES=-I/usr/X11R/include
X_LIB=-L/usr/X11R/lib -lX11 -Xt
```

```
PNG_INCLUDES=-I/usr/local/include
PNG_LIB=-L/usr/local/lib -png
```

每种编译器和链接器标志通常都有一个如下的宏：

```
CFLAGS=$(CFLAGS) $(X_INCLUDES) $(PNG_INCLUDES)
DFLAGS=$(LDFLAGS) $(X_LIB) $(PNG_LIB)
```

对象文件通常根据可执行文件进行分组。假设你有一个包，可以创建名为 boring 和 trite 的两个可执行文件。它们都有自己的 .c 源文件，并且需要 `util.c` 中的代码。你可能会看到这样的内容：

```
UTIL_OBJS=$util.o
```

```
BORING_OBJS=$$(UTIL_OBJS) boring
TRITE_OBJS=$$(UTIL_OBJS) trite
```

```
PROGS=$boring trite
```

Makefile 的其余部分可能如下：

```
all: $(PROGS)

boring: $(BORING_OBJS)
$(CC) -o $@ $(BORING_OBJS) $(LDFLAGS)

trite: $(TRITE_OBJS)
$(CC) -o $@ $(TRITE_OBJS) $(LDFLAGS)
```

你可以将两个可执行文件合并到一个规则中，但通常这不是良好的做法，因为你无法轻松为另一个 Makefile 编写规则、删除可执行文件或以不同的方式分组可执行文件。此外，依赖关系将是——如果你为 boring 和 trite 只写了一个规则，trite 将依赖于 boring.c，而 boring 将依赖于 trite.c，每当你更改其中一个源文件时，make 都会尝试重新构建这两个程序。

> 注意：如果你需要为对象文件定义特殊规则，请将对象文件的规则放在构建可执行文件的规则之上。如果多个可执行文件使用同一个对象文件，请将对象规则放在所有可执行文件规则之上。

## 8.2 调试器

Linux 系统上的标准调试器是 `gdb`，`DDD` 是图形界面。要在程序中启用完全调试，你必须使用 `-g` 选项运行编译器，将符号表和其他调试信息写入可执行文件。要对名为 `program` 的可执行文件启动 `gdb`，请运行此命令：

```
gdb program
```

你应该得到一个 `(gdb)` 提示符。要带有命令行参数运行程序，请在 `(gdb)` 提示符处输入：

```
run options
```

如果程序运行正常，它应该正常启动、运行并退出。然而，如果出现问题，`gdb` 会停止，打印堆栈跟踪和失败的源代码，并将你带回 `(gdb)` 提示符。因为代码片段通常会给你关于问题的提示，你通常想要打印与问题相关的特定变量的值（`print` 命令也适用于数组和 C 结构）：

```
print variable
```

如果你想让 `gdb` 在原始源代码的任何点停止程序，请使用以下命令。`file` 是源代码文件，`line_num` 是该文件中 `gdb` 应该停止的行号：

```
break file:line_num
```

要让 `gdb` 继续执行程序，请使用此命令：

```
continue
```

要清除断点，请输入：

```
clear file:line_num
```

本节仅提供对调试器的简要介绍。`gdb` 随附带有一份非常详尽的手册，你可以在线阅读、打印或购买《Debugging with GDB [Stallman/Pesch/Shebs]》。

> 注意：如果你对根源内存问题和运行性能测试感兴趣，请尝试 Valgrind (http://valgrind.kde.org/)。

## 8.3 Lex 和 Yacc

在编译读取配置文件或命令的程序时，你可能会遇到 `lex` 和 `yacc`。
