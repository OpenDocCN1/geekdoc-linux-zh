
```
############################################
##### Sample makefile
##### Comments start with '#'
############################################

##### Use standard variables to define compile and link flags

CFLAGS= -g -O2
##### Define the target "all"

all: xdraw

OBJJS=xdraw.o xvviewobj.o shapes.o
xdraw: $(OBJJS)
##### Object files
xdraw.o: Makefile xdraw.c xdraw.h

xvviewobj.o: Makefile xvviewobj.c shapes.h
shapes.o: Makefile shapes.c shapes.h
```

![](img/9f89727199836b0f871f1745838aa8b2_749_0.png)

此 `makefile` 依赖于 GNU `make` 的隐式规则。`.c` 文件到 `.o` 文件的转换使用内置规则。定义变量 `CFLAGS` 会将标志传递给 C 编译器。

名为 `all` 的目标被定义为第一个目标是有原因的——如果在命令行中不指定任何目标运行 GNU `make`（参见下一节中描述的 `make` 语法），该命令将构建在 `makefile` 中找到的第一个目标。通过将第一个目标 `all` 定义为 `xdraw`，您可以确保即使未显式将其指定为目标，`make` 也会构建此可执行文件。UNIX 程序员传统上使用 `all` 作为第一个目标的名称，但目标名称无关紧要；重要的是它是 `makefile` 中的第一个目标。

### 如何运行 make

通常，您只需在 shell 提示符下输入以下命令来运行 `make`：

```
make
```

以这种方式运行时，GNU `make` 会按顺序查找名为 GNU`makefile`、`makefile` 或 `Makefile` 的文件。如果 `make` 找到这些 `makefile` 之一，它将构建该 `makefile` 中指定的第一个目标。然而，如果 `make` 找不到合适的 `makefile`，它将显示以下错误消息并退出：

```
make: *** No targets specified and no makefile found. Stop.
```

如果您的 `makefile` 名称与默认名称不同，您必须使用 `-f` 选项来指定 `makefile`。带有此选项的 `make` 命令语法如下：

```
make -f filename
```

其中 `filename` 是 `makefile` 的名称。

即使您有一个具有默认名称（例如 `Makefile`）的 `makefile`，您可能仍然想要构建 `makefile` 中定义的多个目标中的特定目标。在这种情况下，运行 `make` 时必须使用以下语法：

```
make target
```

例如，如果 `makefile` 包含名为 `clean` 的目标，您可以使用以下命令构建该目标：

```
make clean
```

另一种特殊语法用于覆盖 `make` 变量的值。例如，GNU`make` 使用 `CFLAGS` 变量来存储编译 C 文件时使用的标志。您也可以在调用 `make` 时覆盖此变量的值。以下是如何将 `CFLAGS` 定义为选项 `-g -O2` 的示例：

```
make CFLAGS="-g -O2"
```

除了这些选项外，GNU`make` 还接受其他几个命令行选项。表 I-3 列出了 GNU`make` 选项。

#### 表 I-3 GNU make 选项

| 选项 | 含义 |

| :--- | :--- |

| -b | 忽略但接受，以与其他版本的 `make` 兼容。 |

| -C DIR | 在读取 `makefile` 之前更改到指定目录。 |

| -d | 打印调试信息。 |

| -e | 允许环境变量覆盖 `makefile` 中同名变量的定义。 |

| -f FILE | 读取 `FILE` 作为 `makefile`。 |

| -h | 显示 `make` 选项列表。 |

| -i | 忽略构建目标时执行命令中出现的所有错误。 |

| -I DIR | 在指定目录中搜索包含的 `makefile`（在 `makefile` 中包含文件的能力是 GNU`make` 独有的）。 |

| -j NUM | 指定 `make` 可以同时运行的命令数量。 |

| -k | 即使构建某个目标时发生错误，也继续构建无关的目标。 |

| -l LOAD | 如果负载平均值至少为 `LOAD`（一个浮点数），则不要启动新作业。 |

| -m | 忽略但接受，以与其他版本的 `make` 兼容。 |

| -n | 打印要执行的命令，但不执行它们。 |

| -o FILE | 即使文件 `FILE` 比其依赖项旧，也不重新构建它。 |

### GNU 调试器

尽管 `make` 自动化了程序构建过程，但当程序运行不正确或突然带有错误消息退出时，编程的这一部分是您最少需要担心的事情。您需要一个调试器来查找程序错误的原因。Fedora Core 包含 `gdb`——功能强大的具有命令行界面的 GNU 调试器。

像任何调试器一样，`gdb` 允许您执行典型的调试任务，例如：

- 设置断点，以便程序在指定行停止。
- 监视程序中变量的值。
- 逐行单步执行程序。
- 修改变量以尝试修复错误。

`gdb` 调试器可以调试 C 和 C++ 程序。

#### 准备调试程序

如果您想使用 `gdb` 调试程序，必须确保编译器生成调试信息并将其放置在可执行文件中。调试信息包含程序中变量的名称以及可执行文件中地址到源文件中代码行的映射。`gdb` 需要此信息来执行其功能，例如在执行指定的源代码行后停止。

为了确认可执行文件已为调试做好准备，请在 GCC 中使用 `-g` 选项。你可以在 `Makefile` 中通过定义变量 `CFLAGS` 来完成此任务，如下所示：

```
CFLAGS= -g
```

#### 运行 `gdb`

调试程序最常见的方式是使用以下命令运行 `gdb`：

```
gdb `progname`
```

`progname` 是程序可执行文件的名称。运行后，`gdb` 会显示以下信息并提示您输入命令：

```
GNU gdb Red Hat Linux (6.0post-0.20031117.7rh)
Copyright 2003 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
Type "Show copying" to see the conditions.
There is absolutely no warranty for GDB. Type "show warranty" for details.
This GDB was configured as "i386-redhat-linux-gnu".
(gdb)
```

您可以在 `(gdb)` 提示符后输入 `gdb` 命令。一个有用的命令是 `help` —— 它会显示一个命令列表，如下所示：

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
```
