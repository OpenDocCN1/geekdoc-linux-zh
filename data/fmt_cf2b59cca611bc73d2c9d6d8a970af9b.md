
在这个示例中，在使用 `rm` 删除 `shuffle.c` 的工作副本后，执行了 `cvs remove` 命令。同样，在文件从源仓库实际删除之前，你必须执行 `commit` 命令。

## 其他 CVS 命令

虽然前面描述的命令对于模块的大部分工作已经足够，但你可能会发现其他命令有用。

## 为发布版本标记

你可以对模块中当前存在的文件应用一个公共标签（tag）。一旦你对模块的文件进行了标记，即使这些文件自自标记以来被修改、添加或删除，你也可以以完全相同的格式重新创建它们。这种能力允许你冻结一个发布，同时允许在下一个发布上继续开发：

```
$ cvs rtag Release_1 Project1

cvs rtag: Tagging Project1
```

在这里，`Project1` 模块被标记了 `Release_1` 标签。你可以配合 `cvs export` 命令使用此标签来提取冻结时的文件。

## 提取发布版本

`cvs export` 命令允许提取冻结并标记的文件：

```
$ cvs export -r Release_1 -d R1 Project1

cvs export: Updating R1

R1/scm.txt
```

此命令的工作原理类似于 `cvs checkout` 命令，但不会创建 CVS 支持文件。你必须提供识别版本的选项（如上所示）或使用 `D` 选项指定日期。`d R1` 指示 `cvs` 将模块的文件放入目录 `R1` 中，而不是使用模块名作为目录。

## 删除工作文件

（注：原始 OCR 中的后续文本似乎是重复/损坏的，我已根据上下文清理了机械错误。）

大多数仓库都从一个 `modules` 文件开始，允许你使用以下命令检出该模块文件，而不是之前显示的命令：

`cvs checkout modules`

使用上述命令，CVS 会在工作目录下创建一个名为 `modules` 的子目录，而不是名为 `CVSROOT` 的目录。随后 `modules` 文件会被检出到此目录中。

以下示例了一个 `modules` 文件（以 `#` 开头的注释行和空行会被 CVS 忽略）：

```
# The CVS modules file

# 三种不同的行格式都是有效的：

# key a alias...

# key [options] directory

# key [options] directories...

# 其中 "options"由以下部分组成：

# i prog 在模块层级执行 "cvs commit" 时运行 "prog"。

# o prog 在模块执行 "cvs checkout" 时运行 "prog"。

# t prog 在模块执行 "cvs tag" 时运行 "prog"。

# u prog 在模块执行 "cvs update" 时运行 "prog"。

# d dir 将目录放置在 "dir" 而不是模块名。

# i Toplevel 仅执行顶层目录，不返回。

# 并且 "directory" 是相对于 $CVSROOT 的目录路径。

# "a" 选项指定别名。别名被解释为

# "a" 右侧的所有内容已在命令行中输入。

# 你可以使用特殊字符 '&' 在模块内部编码模块，

# 将另一个模块插入到当前模块中。这对于创建一个分布在整个源代码仓库中的多个目录模块非常有用。
```

```
# 便捷别名

world a .

# CVSROOT 支持：每次更改时运行 mkmodules。

CVSROOT i mkmodules CVSROOT

modules i mkmodules CVSROOT

loginfo i mkmodules CVSROOT login

commitinfo i mkmodules CVSROOT commitinfo

rcinfo i mkmodules CVSROOT rcinfo

editinfo i mkmodules CVSROOT editinfo

# 在此处添加其他模块...

testgen testgen

testdata testdata1

testdata2 testdata2

testdata3 testdata3

testdata4 testdata4

testcode testgen_code

cvs cvs
```

注释和空行之后的行定义了许多模块的符号名称。例如，下一行将 `world` 定义为 CVS 仓库根目录的别名：

`world a .`

你可以在 CVS 中使用此类名称作为模块名。例如，以下命令检出了整个仓库（这可能不是好主意）：

```
$ cvs checkout world
```

在示例 `modules` 文件中，管理文件包含类定义，这些定义为文件关联了符号名称以及每个文件检入仓库时执行的操作（`mkmodules`）。`mkmodules` 操作会导致 CVS 在文件被检入时运行 `mkmodules` 程序。该程序会确保被检出文件的副本存在于 CVS 可以找到的位置。

紧随操作之后的是 `CVSROOT` 中持有具有符号名称字段的子目录名称。行中剩余的任何参数都是该目录内特定文件的名称。

以下行将 `CVSROOT` 标识为目录 `$CVSROOT/CVSROOT` 的名称，即用于所有 CVS 的管理文件：

```
CVSROOT -i mkmodules CVSROOT
```

同样，下一行将 `modules` 模块与 `CVSROOT` 目录下的 `modules` 文件关联：

```
modules -i mkmodules CVSROOT modules
```

现在，命令可以找到并检出 `modules` 文件了：

```
$ cvs checkout modules
```

示例 `modules` 文件的最后一组行将符号模块名称与仓库中的目录和文件关联。

## 使用 TkCVS

`cvs` 工具非常实用，因此人们编写了一个使用 Tcl 编程语言（`tcl.sourceforge.net`）的 Tk 扩展的图形化界面——TkCVS。TkCVS 是 `tkcv` 软件包的一部分。它为 CVS 提供了一个（见图 27-6）方便的点击式界面。在下载并安装 TkCVS (`www.twobarleycorns.net/tkcvs.html`) 后，可以通过切换到想要的工作目录并输入以下命令来启动该工具：

```
$ tkcvs &
```

图 27-6. TkCVS 工具

## TkCVS 工作目录

| 文件 | CVS | SVN | RCS | 报告 | 选项 | 用户定义 | Go |
|---|---|---|---|---|---|---|---|
| `COPYING` | | | | | | | 2006/01/02 19:21 |
| `CREDITS` | | | | | | | 2006/02/21 23:31 |
| `Documentation` | | | | | | | | |
| `Kbuild` | | | | | | | 2006/02/21 23:31 |
| `MAINTAINERS` | | | | | | | 2006/02/21 23:31 |
| `Makefile` | | | | | | | 2006/02/21 23:51 |
| `Makefile.orig` | | | | | | | 2006/02/21 23:31 |
| `Module.symvers` | | | | | | | 2006/02/22 00:31 |
| `README` | | | | | | | 2006/02/21 23:31 |
| `REPORTING-BUGS` | | | | | | | 2006/02/21 23:31 |
| `System.symvers` | | | | | | | 2006/02/22 00:31 |
| `arch` | | | | | | | | |
| `block` | | | | | | | | |
| `configs` | | | | | | | | |
| `crypto` | | | | | | | | |
| `drivers` | | | | | | | | |
| `include` | | | | | | | | |
| `init` | | | | | | | | |
| `ipc` | | | | | | | | |
| `kernel` | | | | | | | | |
| `lib` | | | | | | | | |

## CVS

Linux 系统包含了几种实用程序，它们可以帮助跟踪那些经过多次修订的文件组，这些修订通常由多个开发人员完成。这些源代码管理系统之一是 CVS（并发版本系统）。CVS 构建在 `RCS` 之上，但提供了一套更广泛的操作集，用于管理可能被许多用户访问和修改的文件目录。它是管理大型项目以及维护在站点之间发送的软件发布版本的良好选择。

## 练习题

- 1. 每个 C 程序都具有什么函数？为什么你应该将大程序拆分成几个函数？
- 2. 你可以使用什么命令将 `prog.c` 和 `func.c` 编译成一个可执行文件 `cprog`？
- 3. 展示两种指示 C 预处理器在你的 C 程序中包含 `/usr/include/math.h` 头文件的方法。假设 `decl.h` 头文件位于子目录 `nameheaders` 中，请描述两种指示 C 预处理器在你的 C 程序中包含该头文件的方法。
- 4. 系统库的名称在 `gcc` 命令行上是如何缩写的？`gcc` 在哪里搜索以这种方式命名的库？描述如何在 `gcc` 命令行上指定你自己的库。
- 5. 编写一个反映以下关系的 makefile：
    a. 源文件 `transactions.c` 和 `reports.c` 编译生成名为 `accts` 的可执行文件。
    b. `transactions.c` 和 `reports.c` 都包含一个名为 `accts.h` 的头文件。
    c. 头文件 `accts.h` 由另外两个头文件组成：`trans.h` 和 `reps.h`。
- 6. 如果你获取 4.1 版本的 `answer` 进行编辑，然后尝试再次获取同一版本，你会做什么？为什么 CVS 要这样设置？

## 高级练习题

- 7. 修改 `badtabs` 程序（第 851 页），使其能够正常退出（带有特定的返回值）。编译程序并使用 `gdb` 或其他调试器运行它。当程序执行结束时，调试器报告什么值？
- 8. 对于 `Makefile`：

```
$ cat Makefile

leads: menu.o users.o resellers.o prospects.o

gcc -o leads menu.o users.o resellers.o prospects.o
```

```
menu.o: menu.h dialog.h

users.o: menu.h dialog.h

prospects.o: dialog.h
```

识别：

    a. 目标（Targets）。
    b. 构建命令（Construction commands）。
    c. 先决条件（Prerequisites）。

- 9. 参考练习 8 中的 `Makefile` 回答以下问题：
    a. 如果目标 `leads` 是新的且你更改了 `users.c`，再次运行 `make` 会发生什么？请具体说明。
    b. 重写 `Makefile` 以包含以下宏：

```
OBJECTS = menu.o users.o resellers.o prospects.o

HFILES = menu.h dialog.h
```

- 10. 查看 info 页面回答以下问题：
    a. `t` 选项的作用是什么？
    b. 如果你在工作目录中有名为 `make` 和 `Makefile` 的文件，你如何指示 `make` 使用 `Makefile`？
    c. 两种定义变量的方法，以便你可以在 makefile 中使用它。

- 11. 参考第 846 页关于 `compute` 的 makefile。

    a. 假设工作目录中的一个文件名为 `clean`。执行以下命令的影响是什么？请解释。

```
$ make clean
```

    b. 第 844 页的讨论指出，在 makefiles 中通常不会看到以下命令：

```
cat numh.h table.h > form.h
```

    在保留依赖行同时，从 makefile 中删除此构建命令会有什么影响？

    c. 先前的构建之所以起作用，是因为文件 `form.h` 是 `numh.h` 和 `table.h` 组成的。通常情况下，目标中的 `#include` 指令定义了依赖。建议一种更通用的技术，每当 `num.h` 或 `table.h` 有更新的修改日期时，都会更新 `form.h`。

## 28. 编写 Bourne Again Shell 编程

| 本章内容 | |
|---|---|
| 控制结构 | 878 |
| 文件描述符 | 911 |
| 参数与变量 | 914 |
| 数组变量 | 914 |
| 变量局部性 | 916 |
| 特殊参数 | 918 |
| 位置参数 | 920 |
| 内建命令 | 926 |
| 表达式 | 940 |
| Shell 程序 | 948 |
| 递归 Shell 脚本 | 949 |
| 测验 Shell 脚本 | 952 |

第 7 章引入了 shell，第 9 章详细介绍了 Bourne Again Shell。本章介绍了 Bourne Again Shell 命令以及将 shell 编程提升到实用水平的概念。本章的第一部分涵盖了编程控制结构，也称为控制构造。这些结构允许编程控制流程，支持条件判断和循环逻辑。

本章引入了 Bourne Again Shell 命令以及将 shell 编程提升到实用水平的概念。本章的第一部分涵盖了编程控制结构，也称为控制构造。
