
Please enter a name: Robert

The name you entered is Robert

Do you wish to continue? no

Good-bye

# for-in

`for-in` 结构设计用于顺序引用值列表。它接受两个操作数——一个变量和一个值列表。列表中的值逐一分配给 `for-in` 结构中的变量。就像 `while` 命令一样，`for-in` 结构是一个循环。每次循环，列表中的下一个值被分配给变量。当到达列表结束时，循环停止。就像 `while` 循环一样，`for-in` 循环体以关键字 `do` 开始，以关键字 `done` 结束。这是 `for-in` 循环的语法：

```
for variable in list of values

do

commands

done
```

在 `mylistfor` 脚本中，用户只需输出每个项目的列表。由 `for-in` 循环读取的列表项连续地分配给 `grocery` 变量。

## mylistfor

```
date='date +D'

for grocery in $list

do

    echo "$grocery"
```

这是 `mylistfor` 脚本的运行示例：

```
$ mylistfor

milk

cookies

apples

cheese
```

`for-in` 循环非常便于管理文件。你可以使用特殊字符生成当前目录下的所有文件列表。例如，`*` 字符列出所有 `.c` 扩展的文件。`backup` 脚本对每个文件进行备份并将其放在 `sourcebak` 目录中。注意使用 `*` 字符生成。

```
for backfile in *.c

do

    cp backfile sourcebak/$backfile

done
```

## backup

`backup` 脚本的运行示例：

```
$ backup

io.c

lib.c

main.c
```

# for

命令行上指定的参数变成一个值列表。`for` 命令中使用的变量自动设置为列表中的每个值。第一次循环时，变量设置为第一个参数 `$1`。第二次循环时，它设置为第二个参数 `$2`。没有指定列表的 `for` 结构等于 `$@`。在下一个示例中，调用了 `backuparg`，`backfile` 是 `for` 循环使用的变量。第一次循环时，`backfile` 持有第一个参数 `$1`。第二次循环时，它持有第二个参数 `$2`。

```
for backfile

do

  cp backfile sourcebak/$backfile

  echo "$backfile"

done
```

这是 `backuparg` 脚本的运行示例：

```
$ backuparg

main.c

lib.c

io.c
```

# 第 42 章：编译器、库和工具

## 概述

应用程序是程序员使用几种编程语言之一创建的可执行程序。Linux 提供了几种工具，程序员可以使用它们控制应用程序开发。其中包括 `gcc` 工具，它调用 C 和 C++ 编程语言的编译器，生成程序的可执行版本。大多数 Linux 应用是用 C 或 C++ 编写的。

应用程序开发大量使用库。你可以创建自己的库，也可以从专门库中选择。你可以使用 X Windows 库来编写窗口显示，以及 `gdbm` 库，你可以通过它访问数据库。库变得更加灵活，现在可以被共享或动态加载。

其他工具允许你更好地管理应用程序开发。`gdb` 符号调试器帮助你定位运行时错误，`indent` 帮助你准备源代码。`Autoconf` 和 `RPM` 帮助你对软件进行分发。`RCS` 和 `CVS` 等版本控制系统帮助你在开发软件应用时维护记录。表 1 列出了本章的开发工具。

## 表 1：编程工具

| 工具 | 说明 |
| :--- | :--- |
| gcc, g++ | GNU C 和 C++ 编译器，www.gnu.org/software/gcc |
| gdb | GNU 调试器，www.gnu.org/software/gdb |
| RCS | 版本控制系统，www.gnu.org/software/rc |
| CVS | 版本控制系统，www.cvhome.org |
| Man | 在线手册文档 |
| Autoconf | 源代码编译自动配置，www.gnu.org/software/autoconf |

## 获取信息：info

尽管所有编译器及其工具都有页面，但通过 GNU info 系统可以获得更详细的信息。这些文件位于 `/usr/info` 目录，包含 GNU 工具的详细描述和示例。它们等同于紧凑的在线手册。`gcc` 编译器、C 和 C++ 库以及 `Autoconf` 工具都有 info 文档。其他可能有自己的包含 info 文件的目录，例如 `/usr/tex/info` 目录存放了 LaTeX 文件。你通过输入命令 `info` 来调用 info 文档的主菜单。

```
$ info
```

你使用空格键向下翻页菜单。当你找到感兴趣的主题时，按下 `m` 键。这会在屏幕底部打开一行，你可以在其中输入菜单名称。当你按下回车键时，该文档就会出现。按 `b` 返回开头，`U` 回到上一个菜单。`info` 命令将带你进入关于如何使用 info 的教程。

## C 编译器：gcc

Unix 操作系统与 C 编程语言之间存在特殊的关系。C 编程语言是专门为编程 Unix 操作系统而开发的。使用操作系统的代码实际上是用 C 语言编写的。Linux 具有类似的特殊关系。大多数 Linux 系统都包含了 GNU 版本的 C 编译器 `gcc`。本节简要描述了 C 编程语言的基本组件，并利用它们构建了一个实用的编程示例。通过示例程序，我们可以检查编译 C 程序的不同方式。

注意：与其使用命令行界面编译应用程序，你也可以使用带有 Gnome 或 KDE 界面的集成开发环境（IDE）来编译和编辑应用程序源文件。在 Gnome 上，你可以使用 `gbuilder`、`Anjuta` 和 `Titano`。在 KDE 上，你可以使用 `Gideon`、`KDevelop` 和 `KDEStudio`。

你通过 `gcc` 命令在 Linux 系统上调用 GNU C 编译器，该命令反过来调用了其他四个命令。第一个是预处理器。C 程序包含特殊的预处理器命令，这些命令会在代码发送到编译器之前对其进行修改。第二个命令是编译器本身。编译器将处理代码并生成程序的汇编代码版本。第三个命令是汇编器。汇编器将使用程序的汇编代码版本生成目标代码版本。第四个命令是链接器。链接器使用程序的代码生成可执行文件。该可执行文件的默认名称为 `a.out`。通常情况下，你应该为可执行文件指定一个自定义名称。`-o` 选项接受文件名作为参数。该文件名将作为可执行文件的名称，而不是默认的 `a.out`。表 2 提供了 `gcc` 选项列表。在下一个示例中，`gcc` 命令编译了程序 `greet.c`。用户将可执行文件命名为 "`greet`"。

```
$ gcc greet.c -o greet

$ greet
```
