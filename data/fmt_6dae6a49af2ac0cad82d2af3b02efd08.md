
```
(gdb) run < testtabs
Starting: /home/mark/book/10/tabs < testtabs
Breakpoint 1, findstop(col=0xfffffc0) at tabs.c:41
41 retval = (TABSIZE) - (*col % TABSIZE);
(gdb) print *col
$1 = 3
(gdb) backtrace
#0 findstop(col=0xfffffc0) at tabs.c:41
#1 0x804843a in main () at tabs.c:20
(gdb)
```

你可以检查当前作用范围内的任何内容——激活函数中的变量和参数以及全局变量。在下一个示例中，在断点 1 检查变量`pos`的请求会导致错误。产生错误的原因是变量`posn`是在`main`函数中局部定义的，而不是在`findstop`函数中：

```
(gdb) print posn
No symbol "posn" in current context.
```

`up`命令将函数切换到当前激活函数的调用者。因为`main`调用了函数`findstop`，所以当给出`up`命令时，`main`变为激活函数。（`down`命令执行相反的操作）。`up`命令可以接受一个整数参数，指定在函数栈中回溯的层数，`up 1`的意义与`up`相同。（你可以使用`backtrace`命令来确定用于`up`的参数。）

```
(gdb) up
#1 0x808483a in main () at tabs.c:20
20 inc = findstop(&posn);
$2 = 3
(gdb) print posn
(gdb) print *col
No symbol "col" in current context.
(gdb)
```

`cont`（继续）命令使进程从停止的地方继续运行。`testtabs`文件只有单行，执行结果显示在屏幕上。

## 调试 C 程序

`gdb`支持许多让调试变得简单的命令。输入`help`后跟命令：

- `call`
- `delete display`
- `disabled display`
- `dassemble`
- `display`
- `enable display`
- `inspect`
- `output`
- `print`
- `printf`
- `type`
- `set`
- `set variable`
- `undisplay`
- `whatis`
- `x`

```
(gdb) cont

Continuing.

(gdb)
-
-
- x/FMT ADDRESS

输入 "help" 加上命令名称获取完整文档。以下是对 `whatis` 命令的信息，它接受一个变量名或其他表达式作为参数：

(gdb) help whatis

Print data type of expression.
```

## 图形符号调试器

存在多个`gdb`的图形界面。`gdb`的图形版本`xgdb`提供了多个窗口，包括源代码窗口、一个包含常用命令组的命令窗口以及一个用于查看变量值的显示窗口。左鼠标键在命令窗口中进行选择。你可以点击源代码窗口中的所需行来设置断点，并通过点击源代码窗口中的变量来选择变量。在源代码窗口中选择变量并点击命令窗口中的`print`将显示窗口中显示变量的值。你可以通过滚动和（调整）源代码窗口查看代码行。

`GNU ddd`调试器 (www.gnu.org/software/ddd) 也为`gdb`提供了图形用户界面。与`xgdb`不同，`ddd`可以图形化地显示复杂的 C 结构以及链接：

`![](img/c0494f8f1ebc7cc234d912ea2765b44e_455_0.png)`

在它们之间。这种显示使得查看这些结构中的错误变得容易。否则，`ddd`界面与`xgdb`非常相似。

与`xgdb`不同，`ups` (ups.sourceforge.net) 从设计之初就是为了作为一个图形化调试器而设计的；图形界面并不是在调试器完成后添加的。生成的界面简单而强大。例如，当你点击一个变量时，`ups`会自动显示该变量的值，并提供了一个内置的 C 解释器，允许你将 C 代码附加到正在调试的程序中。由于这些附加代码可以访问程序中的变量和值，你可以使用它们来执行复杂的检查，例如跟踪并显示复杂数据结构中的链接（见第 87 页）。

# 系统调用 47

线程是进程内部的单一顺序控制流。线程是多线程程序的基础，多线程程序允许单个程序控制并发运行的线程，每个线程执行不同的任务。多线程程序通常使用重入代码（多个线程可以同时使用的代码），并且在多 CPU 机器上运行时最有价值。在 Linux 环境下，多线程服务器（如`NFS`）可以提供更清晰的接口，并且可能比多个服务器进程更容易编写。当适当地应用时，多线程还可以作为传统的`fork-exec`进程创建范式的低开销替代方案。请参阅位于`/tldp.org/FAQ/Threads-FAQ`的`FAQ`。

# 线程并非越多越好

> 如果你为单 CPU 系统编写了一个没有明确目标或没有工作分工的多线程程序（例如，并行服务器进程），那么生成的程序运行速度可能会比相同系统上的非线程程序更慢。

# 系统调用

Linux 内核的三个基本职责是控制进程、管理文件系统和操作外围设备。作为程序员，你通过系统调用和库函数访问这些内核操作。本节从宏观层面讨论系统调用；详细的处理超出了本书的范围。

正如其名所示，系统调用指示系统（内核）直接代表你执行某些工作。请求是一个消息，告诉内核需要执行什么工作，并包含了必要的参数。例如，打开文件的系统调用包含了文件名。库例程是间接的；它代表你执行系统调用。库例程的优势在于，它可以让你免受内核操作低级细节的干扰，并且它经过了仔细编写，以确保执行得完美。

例如，使用标准 I/O 库函数`fprintf()`向标准输出或标准错误发送文本是非常简单的。如果没有这个函数，你需要使用多个系统调用来实现相同的结果。第 390 页图 10-1 中对库例程`putchar()`和`getchar()`的调用最终使用`write()`和`read()`系统调用执行 I/O 操作。

# strace: 跟踪系统调用

`strace`实用程序是一个调试工具，显示进程或程序所执行的所有系统调用的跟踪。由于你不需要重新编译想要跟踪的程序，因此你可以对没有源码的二进制文件使用`strace`。

系统调用是发生在用户代码和内核代码界面（边界）之间的事件。检查这一边界可以帮助你定位错误、追踪竞态条件并进行完整性检查。Linux 内核并没有完全配合`strace`。请参阅`strace`主页 (www.liacs.nl/~wichert/strace) 获取改进内核与`strace`配合补丁。

# 控制进程

当你在提示符输入命令行时，shell 进程调用`fork`系统来创建自身的一个副本（产生子进程），然后使用`exec`系统调用用不同的程序（你要求它执行的命令）覆盖内存中的该副本。表 10-3 列出了影响进程的系统调用。

| 系统调用 | 功能 |
| --- | --- |
| `fork()` | 创建进程的副本 |
| `exec()` | 用另一个程序覆盖内存中的程序 |
| `getpid()` | 返回调用进程的 PID 数 |
| `wait()` | 使父进程等待子进程运行结束恢复执行 |
| `exit()` | 使进程退出 |
| `nice()` | 修改进程的优先级 |
| `kill()` | 向进程发送信号 |

# 访问文件系统

当你读写文件时，会发生许多操作。文件系统提供了存储和检索数据的主要手段。文件系统将数据组织成目录和文件的层次结构。导航文件系统通过路径完成。内核管理各种磁盘设备上数据的物理存储。表 10-4 列出了文件系统常用的系统调用：

| 系统调用 | 功能 |
| --- | --- |
| `stat()` | 获取状态信息 |
| `seek()` | 移动到文件的某个位置 |
| `create()` | 创建新文件 |
| `open()` | 打开现有文件 |
| `read()` | 读取文件 |
| `write()` | 写入文件 |
| `close()` | 关闭文件 |
| `unlink()` | 取消文件链接（删除） |
| `chmod()` | 修改访问权限 |
| `chown()` | 更改所有者 |

# 内置 CVS 帮助

`CVS`使用单一工具`cvs`来实现所有功能。要显示获取信息的说明，请使用`--help`选项：

```
$ cvs --help

用法: cvs [options] command [command-options-and-arguments]

where cvs-options 为 -a, -d 等等。

  (指定 --help-options 获取选项列表)

  where command 为 add, admin 等等。

  (指定 --help-synonyms 获取命令同义词列表)

  或使用 --help-synonyms 获取命令同义词列表

where command-options-and-arguments 取决于特定命令

  (指定 -H 后跟命令名称以获取特定命令的帮助)

  指定 --help 以接收此消息
```

并发版本系统（Concurrent Versions System，简称`CVS`）是一个用于版本控制工具。
有关`CVS`更新和更多信息，请参阅`CVS`主页`http://www.cvs.org/`或`Pascal Molli`的`CVS`站点`http://www.loria.org/~molli/cvs-index.html`

要获取`cvs`命令的帮助，请使用`--help`选项后跟工具名称。以下示例显示了`log`命令的用法：

```
$ cvs --help log

用法: cvs log [-R1htnb] [-revisions] [-d dates] [-s states]

  [-w][logins]] [files...]
```
