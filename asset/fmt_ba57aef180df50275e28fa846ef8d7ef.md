
```makefile
# 为编译器名称定义宏
CXX=g++

# 为 GCC 标志定义一个宏
CXXFLAGS=-O2 -g

# 构建对象文件的规则
form.o: form.C form.h
$(CXX) -c $(CXXFLAGS) form.C
```

在这个示例中，`CXX` 和 `CXXFLAGS` 是变量（GNU make 倾向于将变量称为宏）。要在 makefile 的任何地方使用变量，以美元符号（`$`）开头，后跟括号内的变量。GNU make 将变量的所有出现处替换为其定义；因此，它将所有 `$(CXXFLAGS)` 替换为字符串 `-O2 -g`。GNU make 有若干个具有特殊含义的预定义变量。除了表 1-2 中列出的变量外，GNU make 还认为环境变量（如 `PATH` 和 `HOME`）也是预定义变量。

| 表 1-2 某些预定义变量 |

| :--- | :--- |

| GNU make 中的一些预定义变量 |

| 变量 | 含义 |

| CC | 编译器的名称 |

| CFLAGS | 编译标志 |

| CP | 复制命令名称 |

| CPFLAGS | 复制标志 |

| CPP | C++ 编译器的名称

| CPPFLAGS | C++ 编译标志 |

| FC | Fortran 编译器的名称

| FFLAGS | Fortran 编译标志 |

| LD | 链接器名称

| LDFLAGS | 链接标志 |

| RM | 删除命令名称

| RMFLAGS | 删除标志 |

| AS | 汇编器名称

| ASFLAGS | 汇编标志 |

| CXX | C++ 编译器的名称

| CXXFLAGS | C++ 编译标志 |

| EXE | 可执行文件命令

| EXEFLAGS | 可执行文件标志 |

| SIZE | 查看文件大小命令

| SIZEFLAGS | 查看文件大小标志 |

| TAG | 标签命令

| TAGFLAGS | 标签标志 |

| $ | 变量前符 |

| $@ | 目标名称 |

| $^ | 所有依赖项名称

| $< | 第一个依赖项名称 |

| $+ | 最后一个依赖项名称 |

| | | 匹配的依赖项 |

| ? | 匹配第一个依赖项 |

| * | 匹配所有依赖项 |

| | | 匹配模式的依赖项 |

| % | 匹配模式的依赖项 |

# 如何运行 make

通常，你通过在 shell 提示符下输入以下命令来运行 `make`：

```
make
```

运行时，GNU make 会查找名为 `GNUmakefile`、`makefile` 或 `Makefile` 的文件 —— 按照该顺序。如果 `make` 找到了其中一个 makefile，就会构建该 makefile 中的第一个目标。然而，如果 `make` 没有找到合适的 makefile，它会显示以下错误消息并退出：

```
make *** No targets specified and no makefile found. Stop.
```

如果你的 makefile 名称与默认名称不同，你必须使用 `-f` 选项来指定 makefile。带有选项的 `make` 命令语法为：

```
make -f filename
```

其中 `filename` 是 makefile 的名称。

即使你有一个默认名称如 `Makefile` 的 makefile，你可能也想构建 makefile 中定义的多个目标中的某一个。在这种情况下，运行 `make` 时必须使用以下语法：

```
make target
```

![](img/fb03f7f944c69a481f34f490e877a2b9_674_0.png)

## 648 探索 Linux 中的软件开发工具

例如，如果 makefile 中包含一个名为 `clean` 的目标，你可以使用此命令构建该目标：

```
make clean
```

另一种语法可以覆盖 `make` 变量的值。例如，GNU make 使用 `CFLAGS` 变量来存储编译 C 文件时使用的标志。你可以在调用 `make` 时覆盖此变量的值。以下是一个如何将 `CFLAGS` 定义为选项 `-g -O2` 的示例：

除了这些选项外，GNU make 还可以接受其他几个命令行选项。表 1-3 列出了 GNU make 的选项。

| 表 1-3 GNU make 选项 |

| 选项 | 含义 |

| -b | 忽略但接受，以与其他版本的 make 兼容。 |

| -C DIR | 在读取 makefile 之前切换到指定的目录。 |

| -d | 打印调试信息。 |

| -e | 允许环境变量覆盖 makefile 中同名变量的定义。 |

| -f FILE | 读取 FILE 作为 makefile。 |

| -h | 显示 make 选项列表。 |

| -i | 忽略构建目标时执行命令中的所有错误。 |

| -l DIR | 在指定目录中搜索包含的 makefiles。（在 makefile 中包含文件的功能是 GNU make 特有的。） |

| -j NUM | 指定可以同时运行的命令数。 |

| -k | 即使构建某个目标时发生错误，也继续构建无关的目标。 |

| -l LOAD | 如果平均负载至少为 LOAD（浮点数），则不启动新作业。 |

| -m | 忽略但接受，以与其他版本的 make 兼容。 |

| -n | 打印要执行的命令，但不执行它们。 |

| -o FILE | 不重新构建命名的 FILE，即使它比依赖项旧。 |

| -p | 显示变量和隐含规则的 make 数据库。 |

| -q | 不运行任何操作，但如果所有目标都是新的则返回 0；如果需要更新则返回 1；如果发生错误则返回 2。 |

| -r | 移除所有内置规则。 |

| -R | 移除所有内置变量和规则。 |

| -s | 静默工作（不显示执行过程中的命令）。 |

| -t | 修改文件的时间戳。 |

| -v | 显示 make 版本号和版权声明。 |

| -w | 在处理 makefile 之前之后显示工作目录的名称。 |

| -W FILE | 假设指定文件已修改（使用 -n 查看修改该文件会发生什么）。 |

## GNU 调试器 (GNU debugger)

尽管 `make` 自动化了程序的构建过程，但当程序因错误消息而突然停止正常运行时，编程的那部分并不是你最需要担心的。你需要一个调试器来找到程序错误的原因。Linux 包含了 `gdb` —— 一个具有命令行界面的多功能 GNU 调试器。

与任何调试器一样，`gdb` 允许你执行典型的调试任务，如下：

- 设置断点，使程序在指定的行停止。

- 监视程序中变量的值。

- 逐行执行程序。

- 尝试更改变量以修复错误。

`gdb` 调试器可以调试 C 和 C++ 程序。

### 准备调试程序

如果你想使用 `gdb` 调试程序，你必须确保编译器生成并放置了调试信息，其中包含程序中变量的名称，以及可执行文件地址到源文件中代码行的映射。

`gdb` 需要这些信息来执行其功能，例如在执行指定的源码行后停止。

为了确保可执行文件已为调试准备好，请在使用 GCC 时使用 `-g` 选项。你可以通过在 makefile 中定义变量 `CFLAGS` 完成此任务：

```
CFLAGS= -g
```

![](img/fb03f7f944c69a481f34f490e877a2b9_676_0.png)

### 运行 gdb

调试程序的常用方法是使用以下命令运行 `gdb`：

```
gdb programe
```

`programe` 是程序可执行文件的名称。运行后，`gdb` 显示以下消息并提示你输入命令：

```
GNU gdb 6.1-debian
Copyright 2004 Free Software Foundation, Inc.
GDB 是自由软件，受 GNU 通用公共许可证保护，欢迎在某些条件下修改和/或分发其副本。
输入 "show copying" 查看条件。
GDB 绝对没有任何保证。输入 "show warranty" 查看详情。
此 GDB 配置为 "i386-linux"。
(gdb)
```

你可以在 `(gdb)` 提示符处输入 `gdb` 命令。一个非常有用的命令是 `help` —— 它显示如下命令列表：

- `(gdb) help`

命令类别列表：

alias -- 其他命令的别名

breakpoints -- 让程序在某些点停止

data -- 检查数据

files -- 指定并检查文件

Internals -- 维护命令

obscure -- 冷门特性

running -- 运行程序

stack -- 检查栈

status -- 状态查询

nsupport -- 支持设施

tracepoints -- 在不停止程序的情况下跟踪程序执行

user-defined -- 用户定义命令

输入 "help" 后跟类名可以查看该类中的命令列表。输入 "help" 后跟命令名可以查看该命令的完整帮助。命令名允许缩写。

(gdb)

要退出 `gdb`，输入 `q` 然后按回车。
