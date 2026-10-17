
在这个示例中，`CXXFLAGS` 是变量。GNU make 倾向于称它们为变量，但大多数 UNIX 工具称它们为宏。

要在 makefile 的任何地方使用变量，以美元符号（`$`）开头，后跟括号内的变量名。GNU make 将变量的所有出现处替换为其定义；因此，它将 `$(CXXFLAGS)` 的所有出现替换为字符串 `-O2 -g -mcu=1686`。

# 734 第五部分：Linux 编程

GNU make 有几个具有特殊含义的预定义变量。表 23-2 列出了这些变量。除了表 23-2 列出的变量外，GNU make 还考虑所有的环境变量。

## 表 23-2：GNU make 中的一些预定义变量

| 变量 | 含义 |
| --- | --- |
| `$%` | 目标的成员名称。如果目标是 libdisp.a (image.o)， |
| `$*` | 不带扩展的目标名称。 |
| `$+` | 第一个依赖项的名称。 |
| `<` | 目标文件。 |
| `?` | 所有依赖项的名称。 |
| `@@` | 目标的完整名称。 |
| `^` | 所有依赖项的名称。 |
| `AR` | 归程序名称。 |
| `ARFLAGS` | 存档程序的标志。 |
| `AS` | 汇编器名称。 |
| `ASFLAGS` | 汇编器的标志。 |
| `CC` | 编译器名称。 |
| `CFLAGS` | 编译器的标志。 |
| `CO` | 对象文件名称。 |
| `COFLAGS` | 对象文件的标志。 |
| `CPP` | 预处理器名称。 |
| `CPPFLAGS` | 预处理器的标志。 |
| `CXX` | C++ 编译器名称。 |
| `CXXFLAGS` | C++ 编译器的标志。 |
| `FC` | Fortran 编译器名称。 |
| `FFLAGS` | Fortran 编译器的标志。 |
| `GET` | 获取程序。 |
| `GFLAGS` | 获取的标志。 |
| `L` | 链接器名称。 |
| `LDFLAGS` | 链接器的标志。 |
| `LEX` | 词法分析器名称。 |
| `LEXFLAGS` | 标志。 |
| `MAKEINFO` | 转换 Texinfo 的程序。 |
| `RM` | 删除文件的命令。 |
| `TEX` | 生成 DVI 的程序。 |
| `TEXDVI` | 生成 DVI 的程序。 |
| `YACC` | 转换 YACC 语法的程序。 |
| `YACCFLAGS` | 标志。 |

## 第 23 章：Linux 中的软件开发

| 变量 | 含义 |
| --- | --- |
| `MAKEINFO` | 转换 Texinfo 的程序。 |
| `RM` | 删除文件的命令。 |
| `TEX` | 生成 DVI 的程序。 |
| `TEXDVI` | 生成 DVI 的程序。 |
| `YACC` | 转换 YACC 语法的程序。 |
| `YACCFLAGS` | 标志。 |

## 查看隐式规则

GNU make 还包含了内置的（或隐式的）规则，这些规则定义了如何创建特定类型的目标。隐式规则的一个示例是从源文件生成对象文件的命令。GNU make 支持两种类型的隐式规则：

- 后缀规则：后缀规则为 make 定义了隐式规则。后缀定义了如何将具有一种扩展的文件转换为具有另一种扩展的文件。每个后缀通过一对后缀（文件扩展名）定义。例如，将 `.c`（C 源）文件转换为 `.o`（对象）文件的后缀规则可能写如下：
```make
.c:.o
$(CC) $(CFLAGS) $(CPPFLAGS) c -o $@ $<
```
使用了预定义的变量 `CC`、`CFLAGS` 和 `CPPFLAGS`。对于文件名，规则使用变量 `$@`（目标的完整名称）和 `$<`（第一个依赖项的名称）。
- 模式规则：这些规则更灵活，因为你可以使用模式指定更复杂的依赖。模式规则看起来和普通规则一样，只是目标名称中有一个百分号（`%`）。依赖项也使用 `%` 来指示名称与目标的关系。以下模式规则规定了如何将任何文件 X 转换为文件 Y：
```make
%.o:%.c
$(CC) $(CFLAGS) $(CPPFLAGS) c -o $@ $<
```

GNU make 有大量的隐式规则，以后缀和模式规则定义。要查看已知变量和规则的列表，请使用命令行运行 make：
```
make -p -f /dev/null
```
输出包含了变量的名称，以及隐式规则。

## 编写示例 myfile

如果你使用 GNU make 的预定义变量和内置规则，可以轻松地编写 Makefile。例如，这个 Makefile 可以根据三个 C 源文件（`xdraw.c`、`xviewobj.c` 和 `shapes.c`）以及两个头文件（`xdraw.h` 和 `shapes.h`）创建一个可执行文件 `xdraw`。假设每个源文件都包含其中一个头文件。基于这些事实，一个示例 myfile 可能如下：
```
################################################
# 示例 myfile
# 注释以 '#' 开头
################################################
# 使用标准变量定义编译和链接标志
CFLAGS= -g -O2
# 定义目标 "all"
all: xdraw
OBJS=xdraw.c xviewobj.c shapes.o
xdraw: $(OBJS)
# 目标文件
xdraw.o: Makefile xdraw.c xdraw.h
xviewobj.o: Makefile xviewobj.c shapes.h
shapes.o: Makefile shapes.c
```
此 myfile 依赖于 GNU make 的隐式规则。`.c` 文件到 `.o` 文件的转换使用了内置规则。定义 `CFLAGS` 会将标志传递给编译器。

> 命名为 `all` 的目标定义为 Makefile 中的第一个目标是有原因的——如果你在命令行中不指定任何目标就运行 `make`（见下节），它将构建在 Makefile 中找到的第一个目标。通过将第一个目标定义为 `xdraw`，你可以确保即使你没有指定它为目标，`make` 也会构建这个可执行文件。UNIX 程序员传统使用 `all` 作为第一个目标的名称，但目标的名称并不重要；重要的是它是 Makefile 中的第一个目标。

如果你有一个包含适当源文件和头文件的目录，你可以可以尝试运行该 makefile。以下是我输入 `make` 来尝试运行示例 myfile 时执行的命令：
```
cc -g -O2 -c xdraw.c -o xdraw
cc -g -O2 -c xviewobj.c -o xviewobj.o
cc -g -O2 -c shapes.c -o shapes.o
cc xdraw.o xviewobj.o shapes.o -o xdraw
```
![](img/3b3329dddbc9c0857ad4f2ef1c0db305_770_0.png)

## 第 23 章：Linux 下软件开发

如 `make` 的输出所示，`make` 使用 `cc` 命令（这在你的 Linux 系统中恰好是一个符号链接）配合适当选项编译源文件并链接对象文件，最后将对象链接以创建 `xrd` 可执行文件。

## 运行 make

通常，你在命令行中通过单个命令运行 `make`；即通过输入 `make` 来运行。运行时，GNU make 会查找名为 `Makefile`、`makefile` 或 `Makefile` 的大写的文件——一旦 `make` 找到这些 makefile 之一，它就会构建该数据文件中指定的第一个目标。然而，如果 `make` 没找到合适的 makefile，它将显示以下错误信息并退出：
```
make: *** No targets. Stop.
```
如果你的 makefile 名称与默认名称不同，你必须使用 `-f` 选项来指定 makefile。该 `make` 选项的语法如下：
```
make -f filename
```
其中 `filename` 是 makefile 的名称。

即使你有一个具有默认名称（如 `Makefile`）的 makefile，你可能也想从 makefile 中定义的多个目标中构建某一个特定的目标。在这种情况下，你必须使用以下语法运行 `make`：
```
make target
```
如果 makefile 包含目标名称 `clean`，你可以使用此命令构建该目标：
```
make clean
```
另一种特殊语法可以覆盖 `make` 变量的值。例如，GNU make 使用 `CFLAGS` 来存储编译 C 文件时使用的标志。在调用时你可以覆盖此变量的值。如下：
```
make CFLAGS="-g -O2"
```
