
## 此命令行允许 `ld.so`（以及 `ldd`）在标准的 `/usr/lib` 之外，搜索可执行文件所需的 `/lib` 和 `/usr/X11R6/lib`。

编译器在链接时需要看到共享库，以确保所需的函数和程序如头文件（`.h`）所承诺的那存在。使用 `-L` 选项告诉编译器-链接器在 `mylib` 目录中查找共享或静态库：`-L mylib`。与搜索不同，当程序构建自己的共享库时，`-L` 可以使用相对路径，例如 `-L..`。库在构建时可以在一个位置（`-L`），但在安装后可能位于另一个位置（`-rpath`）。`-L` 前的空格是可选的，且通常会被省略；`-r` 后面不能有空格。你可以在链接行上多次重复 `-L` 和 `-r` 选项。

## 修复损坏的二进制文件

命令行搜索路径是一个相当新的概念。传统的搜索路径是通过使用 `LD_LIBRARY_PATH` 路径创建的，最近使用了 `LD_RUN_PATH` 环境变量。这些变量的格式与 `PATH` 相同（见第 284 页）。

`LD_LIBRARY_PATH` 中的目录通常会在常规库位置之前搜索。较新的版本扩展了 `LD_LIBRARY_PATH` 的功能，指定在正常位置之前或之后搜索的目录。`LD_RUN_PATH` 变量的行为与 `LD_LIBRARY_PATH`。然而，如果你使用 `-r`，`LD_LIBRARY_PATH` 将覆盖 `LD_LIBRARY_PATH` 中的任何内容。

使用 `LD_LIBRARY_PATH` 引出了几个问题。由于只存在一个环境变量，它必须在所有程序之间共享。如果两个程序对库具有相同的名称，或使用同一库的不同不兼容版本，则只会找到第一个。结果是程序将无法运行，或者最糟糕的是——运行不正常。

### 安全：`LD_LIBRARY_PATH`

在某些情况下，恶意用户可以创建一个名为 `lib.so` 的特洛伊马并将其放在搜索 `/usr/lib` 的目录中（`LD_LIBRARY_PATH` 中任何出现在 `/usr/lib` 之前的目录）。伪造的 lib 将被替代真实的 lib。

## 包装器 (Wrappers)

`LD_LIBRARY_PATH` 在用于修复损坏二进制文件的脚本（称为包装器）中仍有一用之地。假设损坏的二进制文件 `bb` 使用共享库 `libbb.so`，根据 `bb` 程序员的请求，你想将其放在 `/opt/bb/lib` 而不是 `/usr/lib`。命令 `ldd bb` 会告诉你缺少哪些库。解决办法是：将 `bb` 重命名为 `bb.broken`，并在 `/bin` 创建一个名为 `bb` 的包装器。

```bash
#!/bin/sh

LD_LIBRARY_PATH=/opt/bb/lib

export LD_LIBRARY_PATH

exec bb.broken "$@"
```

（使用 `"$@"` 而不是 `$*` 可以保留参数中的空格；见第 482 页。）包装器还可以允许你在任意位置安装程序。

## 创建共享库

构建动态加载的共享库并非易事：它涉及可重入函数调用、定义库入口例程以及执行其他任务。当你想要创建一个共享对象库时，你至少必须使用 `gcc` 的 `-fPIC`（位置无关）选项编译源文件，并使用 `-shared -x -o libymlib.so` 将生成的对象文件与 `libxx.so` 文件链接（传递给链接器）。研究共享库构建和使用的最佳结果是互联网上的代码。例如，你可以查看 `zlib` 的源文件（`www.gzip.org/zlib`）。

## C++

C++ 有特殊需求，库（共享与否）通常必须由编译器而非 `ld` 生成。共享库可以依赖于其他共享库并有它们自己的搜索路径。如果你设置了 `LD_LIBRARY_PATH`，在编译时的链接阶段添加 `-f` 标志以忽略当前的 `LD_LIBRARY_PATH`，或者你在全局级别设置了它，但在需要时在包装器中使用。

## make: 保持一组程序更新

**提示：** 本节介绍 GNU make 程序

本节描述了 GNU make 程序。其他 make 工具（BSN make、GNUStep make、Borlandmake 等）以及类似的工具（如 ant，即 Apache 构建工具）也是可用的。为 GNU make 创建的 Makefile 通常与其他 make 工具不兼容，如果你正在尝试编译针对另一个平台的代码，这可能会产生问题。

在一个包含许多源文件和头文件的大型程序中，文件通常以复杂的方式相互依赖。当你更改一个文件时，其他依赖于它的文件时，你必须重新编译所有依赖文件。例如，你可能有几个源文件，它们都使用同一个头文件。当你更改头文件时，你必须重新编译每个源文件。头文件可能依赖于其他头文件，依此类推。图 10-3 显示了依赖关系的简单示例。图中的每个箭头从一个文件指向依赖它的另一个文件。

图 10-3. 目标形式依赖图

![](img/bf98da8888128a6a4235ca4c80ee1f24_520_0.png)

当你处理大型程序时，根据依赖关系确定哪些模块需要重新编译可能是困难、耗时且乏味的。make 工具自动化了这一过程。

## 依赖行：目标文件和前提文件

简单来说，make 查看工作目录中名为 `Makefile` 或 `make` 的文件中的依赖行。依赖行指示了文件之间的关系，指定了依赖于一个或多个前提文件的目标文件。如果你修改任何前提文件的时间晚于它们的目标文件，make 将根据位于依赖行后面的构建命令更新目标文件。如果 make 工具在构建过程中遇到错误，通常会停止。

包含供 make 工具更新信息的文件称为 makefile。（见第 388 页的简单示例。）一个简单的 makefile 具有以下语法：

```make
target: prerequisite-list

TAB construction-commands
```

依赖行由目标和前提文件列表组成，用冒号分隔。每一行 `construction-commands`（你可能有多个）必须以一个 TAB 开头，并紧跟在依赖行之后。长行可以使用反斜杠（`\`）作为行的最后一个字符继续。

目标是依赖于 `prerequisite-list` 中文件的名称。`construction-commands` 是普通的 shell 命令（通常用于编译或链接目标文件）。当 `prerequisite-list` 中一个或多个文件的修改时间比目标文件新时，make 工具会执行 `construction-commands`。

下面的示例显示了图 10-3 所示 `form` 文件的依赖行和构建命令。`form` 依赖于前提 `size.o` 和 `length.o`。适当的 `gcc` 命令构建了目标：

```make
form: size.o length.o

TAB gcc -o size.o length.o
```

一个依赖行中的每个前提文件都可以另一个依赖行中的目标。例如，`size.o` 和 `length.o` 都是其他依赖行的目标。虽然图 10-3 中的示例很简单，但依赖规范的嵌套可以创建一个复杂的层次结构，规定了许多文件之间的关系。

下面的 makefile（命名为 `Makefile`）对应图 10-3 所示的完整依赖结构。可执行文件 `form` 依赖于两个对象文件，而对象文件分别依赖于它们的源文件和一个头文件 `form.h`。反之，`form.h` 依赖于另外两个头文件。

```make
$ cat Makefile

form: size.o length.o
  gcc -o form size.o length.o

size.o: size.c form.h
  gcc -c size.o

length.o: length.c form.h
  gcc -c length.h

form.h: num.h table.h
  cat num.h table.h > form.h
```

虽然最后一行通常不会出现在 Makefile 中，但它说明了你可以在构建行上放置任何 shell 命令。因为 shell 会处理 makefiles，所以命令行应该是你可以在响应 shell 提示符时输入的命令。

如果其默认目标 `form` 的任何先决文件比其对应的目标文件新，或者任何目标不存在，则以下命令将构建目标 `form`：

```make
$ make
```

如果文件 `form` 被删除，make 将重新构建它，无论其先决文件的修改日期如何。makefile 中的第一个目标是默认目标，并且在你不带任何参数调用 make 时构建该目标。

如果你想重新构建 makefile 中第一个目标以外的其他目标，必须将该目标作为参数传递给 make。以下命令如果在 `form.h` 不存在或其任何先决文件已更新，则重新构建它：

```make
$ make form.h
```

## 隐式依赖

你可以依靠隐式依赖和构建命令来简化编写 makefile 的工作。例如，如果你没有为对象文件包含依赖行，make 会假设它依赖于编译器或汇编器的源代码。因此，如果目标文件的先决文件是 `xxx.o`，make 将查看扩展名来确定如何构建 `.o`。如果它找到了合适的源文件，make 将提供一个构建命令行，调用相应的编译器或汇编器创建对象文件。表 10-1 列出了 make 识别的一些文件扩展名以及每个后缀对应的文件类型。

### 表 10-1. 文件扩展名

| 带扩展名的文件名 | 文件类型 |
| --- | --- |
| `filename.c` | C 语言源代码 |
| `filename.C`, `filename.cc`, `filename.cxx`, `filename.c++`, `filename.cpp` | C++ 语言源代码 |
| `filename.f` | Fortran 语言源代码 |
| `filename.h` | 头文件 |
| `filename.l` | flex, lex 词法分析生成器源码 |
| `filename.o` | 对象模块 |
| `filename.s` | 汇编代码 |
| `filename.sh` | Shell 脚本 |
| `filename.y` | bison, yacc 解析器生成器源码 |

C 和 C++ 是许多 Linux 发行版中提供的传统编程语言。bison 和 flex 工具用于创建 makefile 命令语言。

在下一个示例中，make 保持名为 `compute` 的文件是最新的。make 实用忽略任何以井号（#）开头的行。以下 makefile 的前三行是注释行。第一个依赖行显示 `compute` 依赖于两个对象：`compute.o` 和 `calc.o`。相应的构建行告诉 make 需要生成 `compute`。第二行依赖行显示 `compute` 不仅依赖于它的源文件，还依赖于 `compute.h` 头文件。`compute` 的构建行使用了 C 编译器优化器（`-O3` 选项）。第三组依赖和构建行不是必须的。在缺少它们的情况下，make 推断出 `calc.o` 依赖于 `calc.c` 并生成编译的命令行：

#### $cat Makefile

```make
#
# Makefile for compute
#

compute: compute.o calc.o
    gcc -o compute compute.o calc.o

compute.o: compute.c compute.h
    gcc -c -O3 compute.c

calc.o: calc.c
    gcc -c calc.c

clean:
  rm *.o *core*
```

`clean` 是最后一个目标，没有先决文件。该目标通常用于清除可能已过期或不再需要的冗余文件（如 `.o` 文件）。

以下是基于之前的 makefile 的 make 示例执行。如 `ls` 命令所示，`compute.o`、`calc.o` 和 `compute` 都不是最新的。因此，make 命令运行了重新创建它们的构建命令。

```make
$ ls -ltr
total 22
-rw-rw--r alex pubs 311 Jun 21 15:56 makefile
-rw-rw--r alex pubs 354 Jun 21 16:02 calc.c
-rwx-rw-x alex pubs 6337 Jun 21 16:04 compute
-rw-rw--r alex pubs 49 Jun 21 16:04 compute.h
-rw-rw--r alex pubs 880 Jun 21 16:04 compute.o
-rw-rw--r alex pubs 780 Jun 21 18:20 calc.c
-rw-rw--r alex pubs 179 Jun 21 18:20 calc.c
```

```make
$ make
gcc -c -O3 compute.c
gcc -c calc.c
gcc -o compute compute.o calc.c
```

如果你运行一次 make，然后在不对先决文件任何更改的情况下运行它，make 会指示程序是最新的并且不执行任何命令：

```make
$ make
make: 'compute' is up to date.
```

下一个示例使用 `touch` 实用程序来更改先决文件的修改时间。此模拟显示了当你更改文件时会发生什么。make 实用程序只执行使过时目标变为新的所需的命令：

```make
$ touch calc.c
$ make
gcc -c calc.c
gcc -o compute compute.o calc.o
```

在下一个示例中，touch 更改了 `compute.h` 的修改时间。make 实用程序重新创建了 `compute.o`，因为它依赖于 `compute.h`，并重新创建了执行文件，因为它依赖于 `compute.o`。

```make
$ touch compute.h
$ make
gcc -c -O3 compute.c
gcc -o compute compute.o calc.o
```

### `-n`

如果你想看到运行会做什么，请带有 `-n`（不执行）选项运行 make。`-n` 选项显示 make 将执行的命令，但它不会实际执行它们。

### `-t`

正如这些示例所示，下一个示例多次使用 `make -n` 来查看在你提供 make 命令时 make 会做什么。第一条命令显示目标 **`compute`** 是最新的。接下来，**`touch`** 让所有 **`c`** 文件的修改日期比其目标更新，**`make -n`** 显示了如果你在不带 **`-n`** 的情况下调用它 make 会做什么。**`-t`** 命令确保所有目标是最新的。

```make
$ make -n
make: 'compute' is up to date.

$ touch *.c

$ make -n
gcc -c -O3 compute.c
gcc -c calc.c
gcc -o compute compute.o calc.o

$ make -t
touch compute.o
touch calc.o
touch compute

$ make -n
make: 'compute' is up to date.
```

**-`j`**（作业）选项并行执行任务；`-j` 的数值参数指定作业数量。大多数 **`make`** 任务会命中磁盘然后是 CPU，导致编译之间出现下降。在多处理器系统中，你可以使用 **`make -jn`** 来减少 CPU 使用，其中 *`n`* 是 CPU 的数量。并行运行任务可以显著减少项目的构建时间。

一旦对创建的程序满意，可以使用 makefile 冗余文件。在编写和调试需要重新构建程序时，保留中间文件是有用的。当你一段时间不处理程序时，可以释放磁盘空间。在 makefile 中使用 **`clean`** 目标意味着不需要记住所有可以删除的部分。下一个示例简单地删除所有对象文件：

```make
$ make clean
rm *.o
```

## 可选：宏

make 实用程序的宏功能允许你在 makefile 中创建和使用宏。宏定义的语法是

```make
ID=list
```

将 `ID` 替换为标识符，将 `list` 替换为文件名列表。在此宏定义之后，`$(ID)` 在 makefile 中代表 `list`。

使用宏可以使用多个 C 编译器编译程序，只需对 makefile 进行细微更改。通过使用 `CC` 宏并将第 402 页 makefile 中所有的 `gcc` 替换为 `$(CC)`，例如，你只需要为 `CC` 赋值以使用你选择的编译器：

```make
$ cat Makefile

#
# Makefile for compute
#

CC=gcc

compute: compute.o calc.o
    $(CC) -o compute compute.o calc.o

compute.o: compute.c compute.h
    $(CC) -c -O3 compute.c

calc.o: calc.c
    $(CC) -c calc.c

clean:
    rm *.o
```
