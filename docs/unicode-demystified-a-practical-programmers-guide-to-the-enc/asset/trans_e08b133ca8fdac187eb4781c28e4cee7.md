
（通常是编译和/或链接）目标文件。当先决列表中一个或多个文件的修改时间比目标文件的修改时间新时，`make` 实用程序执行构建命令。

下面的示例显示了图 16-3 中文件名的依赖行和构建命令。该示例依赖先决文件 `size.o` 和 `length.o`。使用适当的 `gcc` 命令构建目标：

```
form: size.o length.o
TAB gcc -o form size.o length.o
```

每条依赖行中的每个先决文件都可以是另一个依赖行中的目标。例如，`size.o` 和 `length.o` 在其他依赖行中。虽然图 16-3 中的示例非常简单，但依赖规格的嵌套可以创建一个复杂的层次结构，指定许多文件之间的关系。

下面的 make（命名为 Makefile）与图 16-3 所示的完整依赖图对应。可执行文件 `form` 依赖于两个对象文件，而这些对象分别依赖于它们的源文件和一个头文件 `form.h`。反过来，`form` 依赖于另外两个头文件：

```
$ cat Makefile
form: size.o length.o
gcc -o form size.o length.o
size.o: size.c form.h
gcc -c size.c
length.o: length.c form.h
gcc -c length.c
form.h: num.h table.h
cat num.h table.h > form.h
```

虽然最后一行通常不会出现在 Makefile 中，但它说明了一个事实：你可以在构建行上放置任何 shell 命令。由于文件是由 shell 处理的，因此命令行应该是你可以在响应 shell 提示符时输入的命令。

如果其目标文件的先决文件更，或目标不存在，则下面的命令将构建默认目标 `form`：

```
$ make
```

因此，如果文件 `form` 被删除，`make` 将重新构建它，无论其先决文件的修改日期如何。Makefile 中的第一个目标是默认目标，并在你不带任何参数调用 `make` 时对它进行构建。

如果你想让 `make` 重新构建 Makefile 中第一个目标以外的目标，你必须将目标作为 `make` 的参数提供。下面的命令如果 `form.h` 不存在或其先决文件最新，则重新构建 `form.h`：

```
$ make form.h
```

## 隐式依赖

你可以依靠隐式依赖和构建命令来让你的编写 Makefile 的工作变得更简单。例如，如果你没有为对象文件包含依赖行，`make` 会假设它依赖于编译器或汇编器源文件。因此，如果目标文件的先决文件是 `xxx.o` 且没有以 `xxx.o` 为目标的依赖行，`make` 将通过查看扩展名来确定如何构建 `.o` 文件。如果它找到了合适的源文件，`make` 将提供一个默认的构建行，调用适当的编译器或汇编器来创建对象文件。表 16-1 列出了 `make` 识别的一些文件名扩展名以及与后缀对应的文件类型。

| 文件名扩展名 | 描述 |
| --- | --- |
| filename.c | C 语言源代码 |
| filename.C, filename.cc, filename.cxx, filename.c++, filename.cpp | C++ 语言源代码 |
| filename.f | FORTRAN 语言源代码 |
| filename.h | 头文件 |
| filename.l | flex, lex 分析器生成器源代码 |
| filename.o | 对象模块 |
| filename.s | 汇器脚本 |
| filename.y | bison, yacc 解析器生成器源代码 |

C 和 C++ 是 Red Hat 提供的传统编程语言。bison 和 flex 工具创建命令语言。下一个示例显示了一个保持名为 `compute` 的文件更新的 Makefile。`make` 实用程序忽略任何以井号 (`#`) 开头的行。下面的 Makefile 前三行是注释行。第一条依赖行显示 `compute` 依赖于两个对象文件：`compute.o` 和 `calcco`。对应的构建行给出了 `make` 生成 `compute` 需要的。下一条依赖行显示 `compute` 不仅依赖于它的 C 源文件，还依赖于头文件 `compute.h`。`compute.o` 的构建行使用了 C 编译器优化器（`-O3` 选项）。第三组依赖和构建行不是必需。

在缺少这些的情况下，`make` 推断出 `calc.o` 依赖于 `calc.c` 并产生编译所需的命令行：

```
$ cat Makefile
#
# Makefile for compute
#
compute: compute.o calc.o
gcc -o compute calc.o

compute.o: compute.c compute.h
gcc -c -O3 compute.c

calc.o: calc.c
gcc -c calc.c

clean:
rm *.o core* ~
```

在前面的 Makefile 中，最后一个目标 `clean` 没有先决文件。该目标通常用于丢弃可能已过期或不再需要的多余文件，例如 `.o` 文件。

以下是基于前面的 Makefile 对 `make` 的一些示例执行。如接下来的命令所示，`compute.o`、`calc.c` 和 `compute` 不是最新的。因此，`make` 运行了重新创建它们的构建命令。

```
$ ls -ltr
total 22
-rw-rw------ 1 alex pubs 311 Jun 21 15:56 makefile
-rw-rw------ 1 alex pubs 354 Jun 21 16:02 calc.o
-rwxr-xr-x 1 root 6337 Jun 21 16:04 compute
-rw-rw------ 1 alex pubs 311 Jun 21 15:56 makefile
```
*(注：此处由于原文文本中 `ls` 输出部分似乎存在重复或格式异常，翻译时已根据语境保持其逻辑结构)*

如接下来的命令所示，`compute.o`、`calc.c` 和 `compute` 不是最新的。因此，`make` 运行了重新创建它们的构建命令。

```
$ ls -ltr
total 22
-rw-rw------ 1 alex pubs 311 Jun 21 15:56 makefile
-rw-rw------ 1 alex pubs 354 Jun 21 16:02 calc.o
-rwxr-xr-x 1 root 6337 Jun 21 16:04 compute
-rw-rw------ 1 alex pubs 311 Jun 21 15:56 makefile
```
*(注：原文中存在大量重复文本块，已按要求要求处理)*
