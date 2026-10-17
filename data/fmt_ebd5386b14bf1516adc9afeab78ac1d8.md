
`$ gcc -shared -fPIC -Wall libRoutine.so routine1.o routine2.o`

```
```

这将生成共享库 `libRoutine.so`。然后你可以像对待静态库一样通过在命令行使用 `(.so)` 共享对象或使用 `-l` 和 `-L` 选项生成可执行文件。

当你运行可执行文件时，可能会看到：

```bash
./BinaryName
```

`/BinaryName: error while loading shared libraries: libRoutine.so: cannot open shared object file: No such file or directory`
```

这是因为系统不知道哪里寻找共享库。你必须将包含共享对象的目录添加到 `LD_LIBRARY_PATH` 环境变量。为了添加 `/path/to/so`，你需要在 `csh` 或 `tsh` 中运行以下命令：

```csh
% setenv LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/path/to/so
```

如果你运行的是 `ksh` 或 `bash`，那么命令为：

```bash
$ export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/path/to/so
```

# 第五部分：工具与编程

如果你将此文件保存为 `makefile` 并将其与名为 `hello.c` 文件放在同一目录下，在 `include` 子目录下放置名为 `hello.h` 的头文件，然后运行 `make` 命令，

```
$ make
gcc -g -O -o /home/nate/bin/hello hello.c
```

它将显示并执行类似所示的内容并生成 `~/bin/hello`。如果你再次运行 **make** 命令，你将得到如下响应：

```
$ make
make: '/home/nate/bin/hello' is up to date.
```

因为你的可执行文件已经是最新的。如果你执行命令：

```
$ make clean
rm -f *.o /home/nate/bin/hello
```

那么它将删除此目录中的任何对象文件以及生成的程序文件。虽然生成一个 `Makefile` 比仅仅输入编译 `hello.c` 的命令要耗费得多，但随着项目的增长，这种时间投入是非常值得的。你还可以通过更改文件名来在新项目中复用你的 `makefiles`。

## Makefile 语法

`Makefile` 的语法与 shell 脚本相似。`Makefile` 可以包含注释、变量、依赖关系和命令。

### 注释

你可以使用 `#`（井号）在 makefile 中插入注释。行中 `#` 之后的所有内容都会被 **make** 忽略。

### 变量

**make** 程序允许你定义命名变量，类似于在 shell 中使用的变量。例如，如果你定义 `SOURCES=hello.c`，那么变量 `$(SOURCES)` 的值就是 `hello`。

你还可以在变量赋值中进行替换。赋值语句

```
OBJECTS=${SOURCES:.cpp=.o}
```

将从变量 `SOURCES` 获取文件列表，并将其赋值给 `OBJECTS`，同时将 `.cpp` 扩展名替换为 `.o`。

**make** 程序拥有程序开发的内置知识。你可以通过运行 **make -p** 来获取内置规则和变量值的列表。**make** 知道以 `.c` 后缀的文件应该被构建为 C 源文件，以 `.cpp`、`.cc` 或 `.C++` 结尾的文件是 C++ 源文件，以 `.o` 结尾的是对象文件，而以 `.a` 结尾的是汇编文件。虽然 **make** 允许你自定义变量名，但如果未定义 `CC` 和 `C` 等变量，它将使用它们的默认值。

# 第 24 章：C 和 C++ 编程工具

### 依赖关系

分配变量后，我们的示例指定了依赖关系。你通过将目标文件名放在左侧，后跟冒号，然后列出目标文件依赖的文件列表来指定依赖关系。在我们的示例中，

```
$ $(PRODUCT) $(SOURCES) $(INCLUDE)
```

“PRODUCT”变量依赖于“SOURCES”变量和“INCLUDE”变量。在替换变量后，这意味着文件 `$HOME/bin/hello` 依赖于 `hello.c` 和 `include/hello.h` 文件。如果目标文件不存在或比它所依赖的文件旧，那么 `make` 将尝试重新构建它。

还可以创建不生成文件的目标名称。这些目标被称为伪目标（**phony**）。如果你将目标标记为 `.PHONY`，那么它将在不检查依赖关系的情况下运行。例如：

```
.PHONY: clean
```

即使目录中存在名为 `clean` 且已更新的文件，也会导致 `clean` 运行。

依赖关系结合后续章节中描述的命令，构成了规则。

### 命令

依赖行后面可以跟随一个或多个 shell 命令行，如果任何依赖发生变化，就会执行这些命令。这些命令通常用于重建目标。例如：

```
gcc -g -O -o hello.c
```

这是一个构建 `hello` 的命令。命令行必须相对于左边距缩进至少一个制表符（必须使用 Tab；多个空格的等效替换无效）。用空格缩进这些行会导致错误消息：

```
Makefile:8: *** missing separator (did you mean TAB instead of 8 spaces?). Stop.
```

一个规则由一条依赖行和随后的命令组成。这些通常用于重新制作目标文件，但也可以执行任意命令。例如：

clean:
```
rm -f *.o $(PRODUCT)
```

当运行 `make clean` 时执行 `rm` 命令。

### 具有多个依赖关系的 Makefile

如果你有多个源文件，可以通过在 `SOURCES` 行末尾添加额外的 `.c` 文件来扩展前面的示例。遗憾的是，这种方法会导致当任何源文件发生变化时都强制完全重新编译，即使你只修改了一个源文件。更有效的方法是让程序目标依赖于对象文件 `.o`，这样如果相应的源文件没有变化，`make` 就可以复用对象文件。

如果你省略解释如何从源 C 或 C++ 文件获取对象文件 `.o` 的规则，那么 `make` 将使用内置隐式规则自动构建你的对象文件。对于 C 文件，内置命令看起来如下：

```
$(CC) $(CFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -c
```

对于 C++ 文件，该行如下：

```
$(CXX) $(CXXFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -c
```

如果你想指定如何构建对象文件 `.o`，你可以手动为每对对象文件/源文件输入一个规则，或者可以在你的 makefile 中包含一个构建所有这些文件的显式规则。无论你使用隐式规则还是显式规则来生成对象文件 `.o`，你仍然需要列出头文件依赖关系。告诉 `make` 当头文件变化时应该重新构建 `hello.o`。由于手动输入头文件依赖关系耗时且容易出错，可以使用如 `makedepend` 这样的工具，它可以解析你的源文件并为你的 makefile 生成头文件依赖行。

| 变量 | 说明 |
| --- | --- |
| $@ | 目标文件名。 |
| $< | 依赖文件的名称。 |
| $* | 依赖文件名的主体部分（stem）。 |
| $? | 所有过期的文件列表。 |
| $^ | 所有唯一依赖文件的列表。 |
| $+ | 按给定顺序的依赖文件列表。 |
| $% | 仅适用于库存档。当目标是归档时，目标成员。 |

# 表 24-2 Makefile 自动变量

# 第五部分：工具与编程

## 一个复杂的 C++ Makefile

以下是一个更复杂的 C++ makefile 示例，它会生成一个名为 `Executable` 的程序。该程序包含两个源文件 `main.cpp` 和 `rest.cpp`；一个头文件 `private.h`，它位于名为 `include` 的子目录下；以及一个库 `libRoutines.a`，其包含源文件 `routine1.cpp` 和 `routine2.cpp`。

```
# 一个更复杂的 makefile，用于组合 c++ 源文件
# 私有头文件和库。
HEADERS=include/private.h
SOURCES=main.cpp rest.cpp
OBJECTS=$(SOURCES):.o
PRODUCT=Executable
LIB=libRoutines.a
LISOURCES=routine1.cpp routine2.cpp
LIBOBJECTS=$(LISOURCES):.cpp.o
INCLUDE=include
CXX=g++
CXXFLAGS = -g -Wall -O
all: $(PRODUCT)
$(PRODUCT): $(OBJECTS) $(LIB)
	$(CXX) $(CXXFLAGS) -o $(PRODUCT) $(OBJECTS) $(LIB)
.cpp.o:
	$(CXX) -c $(CXXFLAGS) -I$(INCLUDE) $<
$(LIB): $(OBJECTS)
	ar cr $ $(LIB) ^
$(OBJECTS): $(HEADERS)
.PHONY: clean
clean:
	rm -f *.o $(PRODUCT) $(LIB)
```

如果你拥有所有文件并运行，输出将是：

```
$ make
g++ -c -g -Wall -Oinclude main.cpp
g++ -c -g -Wall -Oinclude rest.cpp
g++ -c -g -Wall -Oinclude routine1.cpp
```

g++ -C -Wall -O -Include routine2.cpp
ar crs libRoutines.a routine1.o routine2.o
g++ -g -Wall -O -o Executable main.o rest.o libRoutines.a

## 非编程类 Makefile

`make` 命令可以用于更新具有内部依赖的其他类型的项目，例如文档。这里有一个示例 Makefile，展示了在文本写作项目中使用 `make` 的基本结构：

```
# 用于书本版本的 Makefile
PRINTER = 1p
FILES = intro chap1 chap2 chap3 chap4 chap5 chap6 appendix glossary
```

book:
```
troff -Tpost -mm $(FILES) | $(PRINTER)
draft: $(FILES)
n1 -bt -p $? -? | pr -d | $(PRINTER)
```

要打印完整文档的当前版本，你只需输入 `make book` 或 `make draft`。

## gdb 调试器

大多数程序都存在 bug。你可以尝试通过迭代开发代码来防止它们的出现，并尝试通过代码检查、使用 `printf()` 或日志文件来追踪它们。然而，很多情况下，你除了查看崩溃或在调试器中单步执行代码外别无选择。`gdb` 是一个命令行调试器，允许你执行这些操作。

如果你想调试代码，需要在使用 `cc`、`gcc` 或 `g++` 时通过 `-g` 命令选项编译你的代码。如果你正在使用 Makefile，请编辑 `CFLAGS` 或 `CXXFLAGS` 以包含 `-g`。如果没有 `-g` 选项，编译器将不会包含 gdb 用于将你的可执行程序映射到源代码的调试符号。`-g` 选项会让你的二进制文件变得大得多且更容易被反向工程。`gdb` 和 `dbx` 是你可能在系统中找到两种替代 UNIX 调试器。它们的使用频率都较低，因此我们在这里重点关注 `gdb`。

### 启动 gdb

你有多种方法使用 `gdb` 调试你的程序。你可以启动 `gdb` 并在内部运行程序，可以将 `gdb` 附加到运行中的程序版本，也可以可以使用 `gdb` 调试从崩溃产生的核心文件（core file）。

### 在 gdb 内部启动程序

你可以将应用程序名称作为命令行参数启动 `gdb`。`gdb` 将加载你程序的符号信息并允许你启动程序。例如，命令

```
gdb debugprogram
```

# 第 24 章：C 和 C++ 编程工具 715

将启动 `gdb` 并加载 `debugprogram`。它会给你一个 `(gdb)` 提示符，表示它已准备好接受输入。如果你忘记使用 `-g` 标志编译 `debugprogram`，那么你将在输出中看到 `(no debugging symbols found)`。

如果你输入

```
(gdb) run
```

那么 `gdb` 将启动你的应用程序。在可能的情况下，`gdb` 会尝试为你减少一些输入工作；只要文本不产生歧义，你就可以省略命令。在 `run` 的情况下，你可以输入 `r` 或 `ru`，它仍然会运行你的程序。

你也可以不带命令行参数启动 `gdb`，并通过命令加载程序：

```
(gdb) file debugprogram
```

这将尝试从当前工作目录调试 `debugprogram`。你可以通过在文件名中包含路径来从单独目录加载文件。

### 附加到进程 gdb

你也可以将 `gdb` 附加到运行中的进程。如果你在程序运行时发现了一个问题，你可能想这样做。你可以使用 `ps -u username` 获取运行进程的列表。它看起来可能像这样

```
$ ps -u nate
PID TTY             CMD
7240 pts/34    00:00:00 bash
9033 pts/34    00:00:04 debugprogram
9238 pts/34    00:00:00 ps
```

第一列告诉你 `debugprogram` 是进程 ID 9033。然后你可以通过运行程序名和进程 ID 来运行 `gdb` 从而附加到你的进程。例如，

```
$ gdb debugprogram 9033
```

只要没有名为 9033 的文件，该命令就会附加到运行的进程。它将进程的执行停止在源代码的当前行。当你退出 `gdb` 时，只要你没有杀死程序，`gdb` 就会将调试器从进程中分离。

### 使用 gdb 调试核心文件

你可以配置 UNIX 环境在应用程序崩溃时转储核心文件（dump core）。核心文件是一个核心映像——一个包含失败进程映像的文件，包括发生故障瞬间的堆栈和堆。“核心映像”（core image）这一术语可以追溯到计算机主内存被称为核心内存的时代，因为它是由称为电感器芯的圆环形磁铁制成的。`gdb` 等调试器可以使用核心映像来确定程序在产生核心文件时所在的位置，以及它是如何到达那里的（即通过函数调用序列）。`gdb` 还可以确定程序失败时变量的值、正在执行的语句以及每个调用的参数![](img/e13cd5886a91d372a0d9c24f7d0_754_0.png

由于核心文件会占用大量的磁盘空间，大多数 UNIX 系统默认不会在程序崩溃时转储核心文件。如果你想启用它，你需要在你的 `shellrc` 中添加该行。例如：

```
ulimit -c unlimited
```
这将允许系统在程序崩溃时生成核心文件。一旦生成了核心文件，你就可以使用 `gdb` 调试它。

由于核心文件会占用大量的磁盘空间，大多数 UNIX 系统默认不会在程序崩溃时转储核心文件。如果你想启用它，你需要在你的 `shellrc` 中添加该行。例如：

```
ulimit -c unlimited
```
这将允许系统在程序崩溃时生成核心文件。一旦生成了核心文件，你就可以使用 `gdb` 调试它。

由于核心文件会占用大量的磁盘空间，大多数 UNIX 系统默认不会在程序崩溃时转储核心文件。如果你想启用它，你需要在你的 `shellrc` 中添加该行。例如：

```
ulimit -c unlimited
```
这将允许系统在程序崩溃时生成核心文件。一旦生成了核心文件，你就可以使用 `gdb` 调试它。

由于核心文件会占用大量的磁盘空间，大多数 UNIX 系统默认不会在程序崩溃时转储核心文件。如果你想启用它，你需要在你的 `shellrc` 中添加该行。例如：

```
ulimit -c unlimited
```
这将允许系统在程序崩溃时生成核心文件。一旦生成了核心文件，你就可以使用 `gdb` 调试它。

由于核心文件会占用大量的磁盘空间，大多数 UNIX 系统默认不会在程序崩溃时转储核心文件。如果你想启用它，你需要在你的 `shellrc` 中添加该行。例如：

```
ulimit -c unlimited
```
这将允许系统在程序崩溃时生成核心文件。一旦生成了核心文件，你就可以使用 `gdb` 调试它。

由于核心文件会占用大量的磁盘空间，大多数 UNIX 系统默认不会在程序崩溃时转储核心文件。如果你想启用它，你需要在你的 `shellrc` 中添加该行。例如：

```
ulimit -c unlimited
```
这将允许系统在程序崩溃时生成核心文件。一旦生成了核心文件，你就可以使用 `gdb` 调试它。

由于核心文件会占用大量的磁盘空间，大多数 UNIX 系统默认不会在程序崩溃时转储核心文件。如果你想启用它，你需要在你的 `shellrc` 中添加该行。例如：

```
ulimit -c unlimited
```
