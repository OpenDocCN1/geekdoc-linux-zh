
`make` 实用工具通过读取和解释 Makefile（一个描述构建特定程序所需的文件以及如何编译和链接这些文件以构建程序的文本文件）来工作。每当你更改一个或多个文件时，`make` 会确定哪些文件需要重新编译——并发布适当的命令来编译这些文件并重建程序。

## Makefile 名称

默认情况下，GNU `make` 按以下顺序查找具有下列名称之一的 Makefile：

- `GNUMakefile`
- `makefile`
- `Makefile`

在 UNIX 系统中，使用 `Makefile` 作为 Makefile 的名称是一种惯例，因为在大写字母位于小写字母之前的目录列表中，它出现在列表的开头附近。

当你从互联网下载软件时，你通常会找到一个 `Makefile`，它伴随着源文件一起提供。要构建软件，你只需在 shell 提示符下输入 `make`，`make` 将处理构建软件所需的所有步骤。

如果你的 Makefile 没有标准名称（例如 `Makefile`），你必须使用 `make` 的 `-f` 选项来指定 Makefile 的名称。例如，如果你的 Makefile 名为 `myprogram.mak`，你必须使用以下命令行运行 `make`：

```bash
make -f myprogram.mak
```

## Makefile 文件

对于由多个源文件和头文件组成的程序，Makefile 指定以下内容：

- `make` 创建的项目——通常是目标文件和可执行文件。使用术语 `target`（目标）来指代 `make` 需要创建的任何项目是很常见的。
- 创建目标所需的文件或其他操作。
- 用于创建每个目标的命令。

假设你有一个名为 `form.C` 的 C++ 源文件，其中包含以下预处理器指令：

```cpp
#include "form.h" // Include header file
```

目标文件 `form.o` 显然依赖于源文件 `form.C` 和头文件 `form.h`。除了这些依赖项之外，你还必须指定 `make` 如何将 `form.C` 文件转换为目标文件 `form.o`。假设你希望 `make` 调用 `g++`（因为源文件是 C++）并使用以下选项：

- `-c`（仅编译）
- `-g`（生成调试信息）
- `-O2`（部分优化）

在 Makefile 中，你可以用以下规则表示这些选项：

```makefile
##### This is a comment in the makefile
# The following lines indicate how form.o depends
# form.C and form.h and how to create form.o.
form.o: form.C form.h
	g++ -c -g -O2 form.C
```

在此示例中，第一个非注释行将 `form.o` 显示为目标，将 `form.C` 和 `form.h` 显示为依赖文件。

依赖项后面的那一行指示如何从依赖项构建目标。这一行必须以制表符开头。

使用 `make` 的好处在于它防止不必要的编译。毕竟，你可以运行 shell 脚本中的 `g++`（或 `gcc`）来编译和链接组成你应用程序的所有文件，但 shell 脚本会编译所有内容，即使这些编译是不必要的。另一方面，GNU `make` 仅在其一个或多个依赖项自上次构建目标以来发生了变化时才构建目标。`make` 通过检查目标和依赖项的最后修改时间来验证此变化。

`make` 将目标视为要达成的目标名称；目标不一定是文件。你可以拥有如下的规则：

```makefile
clean:
	rm -f *.o
```

此规则指定了一个名为 `clean` 的抽象目标，它不依赖于任何内容。该依赖语句表示，为了创建目标 `clean`，GNU `make` 将调用命令 `rm -f *.o`，该命令删除所有具有 `.o` 扩展名的文件（即目标文件）。因此，创建名为 `clean` 的目标的净效果是删除目标文件。

### 变量（或宏）

除了基于依赖项构建目标的基本功能外，GNU `make` 还包含许多实用特性，使您能够轻松表达构建目标所需的依赖关系和规则。例如，如果您需要使用 GCC 以相同的选项编译大量 C++ 文件，为每个文件手动输入选项会非常繁琐。您可以通过在 `make` 中定义变量或宏来避免这种重复性任务，如下所示：

```
##### Define macros for name of compiler
CCXX= g++

##### Define a macro for the GCC flags
CXXFLAGS= -O2 -g -mcpu=i686

##### A rule for building an object file
form.o: form.C form.h
$ (CCXX) -c $ (CXXFLAGS) form.C
```

在这个示例中，`CXX` 和 `CXXFLAGS` 是 `make` 变量。（GNU `make` 更倾向于称它们为`变量`，但大多数 UNIX `make` 实用程序称它们为`宏`。）

要在 `makefile` 的任何位置使用变量，需以美元符号（`$`）开头，后跟括号内的变量名。GNU `make` 会用其定义替换变量的所有出现；因此，它会将 `$(CXXFLAGS)` 的所有出现替换为字符串 `-O2 -g -mcpu=i686`。

GNU `make` 具有几个具有特殊含义的预定义变量。表 1-2 列出了这些变量。除了表 1-2 中列出的变量外，GNU `make` 还将所有环境变量（例如 `PATH` 和 `HOME`）视为预定义变量。

#### 表 1-2 GNU make 中的一些预定义变量

| 变量 | 含义 |
| :--- | :--- |
| `$$` | 归档目标中的成员名称。例如，如果目标是 `libdisp.a`（`image.o`），那么 `$` 是 `image.o`，而 `$` 是 `libdisp.a` |
| `$*` | 不带扩展名的目标文件名。 |
| `$+` | 所有依赖项文件的名称，保留重复的依赖项，并按出现顺序列出。 |
| `$<` | 第一个依赖项文件的名称。 |
| `$?` | 所有比目标更新的依赖项文件的名称（名称之间用空格分隔）。 |
| `$@` | 目标的完整名称。 |
| `$^` | 所有依赖项文件的名称，名称之间用空格分隔。依赖项文件名中的重复项会被移除。 |
| `AR` | 归档维护程序的名称（默认值：`ar`）。 |
| `ARFLAGS` | 归档维护程序的标志（默认值：`rv`）。 |
| `AS` | 将汇编语言转换为目标代码的汇编程序的名称（默认值：`as`）。 |
| `ASFLAGS` | 汇编程序的标志。 |
| `CC` | C 编译器的名称（默认值：`cc`）。 |
| `CFLAGS` | 传递给 C 编译器的标志。 |
| `CO` | 从 RCS 提取文件的程序的名称（默认值：`co`）。 |
| `COFLAGS` | RCS co 程序的标志。 |
| `CPP` | C 预处理器程序的名称（默认值：`${CC} -E`）。 |
| `CPPFLAGS` | C 预处理器的标志。 |
| `CXX` | C++ 编译器的名称（默认值：`g++`）。 |
| `CXXFLAGS` | 传递给 C++ 编译器的标志。 |
| `FC` | FORTRAN 编译器的名称（默认值：`f77`）。 |
| `FFLAGS` | FORTRAN 编译器的标志。 |
| `LDFLAGS` | 编译器调用链接器 `ld` 时使用的标志。 |
| `RM` | 删除文件的命令名称（默认值：`rm -f`）。 |

### 示例 makefile

如果您使用 GNU `make` 的预定义变量及其内置规则，就可以轻松编写 makefile。例如，考虑一个 makefile，它从三个 C 源文件（`xdraw.c`、`xviewobj.c` 和 `shapes.c`）和两个头文件（`xdraw.h` 和 `shapes.h`）创建可执行文件 `xdraw`。假设每个源文件都包含其中一个头文件。鉴于这些事实，一个示例 makefile 可能如下所示：
