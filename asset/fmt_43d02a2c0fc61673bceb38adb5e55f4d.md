
| `trace fun1 in fun2` | 仅跟踪对 `fun1` 的调用 |
| `trace var` | 跟踪变量的变化 |
| `list line` | 列出行号 |
| `print exp` | 显示表达式 |
| `cont` | 继续执行 |
| `stop` | 在行处暂停 |
| `step` | 执行下一行源码 |
| `next` | 执行到下一行源码 |
| `delete` | 删除跟踪或断点 |
| `status` | 显示激活的跟踪和断点 |
| `help` | 显示帮助 |

### 表 10.6 跟踪命令

| 命令 | 描述 |
| :--- | :--- |
| `trace line` | 跟踪该行的执行 |
| `trace function` | 跟踪对函数的调用 |
| `trace fun1 in fun2` | 仅跟踪对 `fun1` 的调用 |
| `trace var` | 跟踪变量的变化 |
| `list line` | 列出行号 |
| `print exp` | 显示表达式 |
| `cont` | 继续执行 |
| `stop` | 在行处暂停 |
| `step` | 执行下一行源码 |
| `next` | 执行到下一行源码 |
| `delete` | 删除跟踪或断点 |
| `status` | 显示激活的跟踪和断点 |
| `help` | 显示帮助 |

### 表 10.7 断点命令

| 命令 | 描述 |
| :--- | :--- |
| `stop line` | 在行处暂停 |
| `stop function` | 在函数处暂停 |
| `stop var` | 在变量处暂停 |
| `list line` | 列出行号 |
| `print exp` | 显示表达式 |
| `cont` | 继续执行 |
| `step` | 执行下一行源码 |
| `next` | 执行到下一行源码 |
| `delete` | 删除跟踪或断点 |
| `status` | 显示激活的跟踪和断点 |
| `help` | 显示帮助 |

# 第 10 章

+   [3] `trace lower`

`(dbx) stop in lower`

[4] `stop in lower`（断点）

`(dbx) run <file1> file2`（运行程序）

`%2 calling read()) from function main`

`%2 returning 0 from read`

`%2 calling lower (buf = "Now Is The Time For\n", length = 20)`

`from function main`

`%2 Stopped at breakpoint 4 in lower at line 22`

`22 { while (length-- > 0)`

`(dbx) where`（display function stack）

`lower(buf = "Now Is The Time For\n", length = 20),`

`line 22 in "lowercase.c"`

`main(argc, 1, argv = 0xff314, 0xff31c), line 10 in "lowercase.c"`

`(dbx) whatis buf`

`char *buf;`

`(dbx) step`（单步执行）

`%2 Stopped after step in lower at line 23`

`23 { if (isupper(*buf))`

`(dbx) print *buf`（显示信息）

`'N'`

`(dbx) step`

`%2 Stopped after step in lower at line 24`

`24 *buf = tolower(*buf);`

`(dbx) step`

`%2 Stopped after step in lower at line 25`

`25 buf++;`

`(dbx) print *buf`

`'N'`

`(dbx) delete 4`（移除断点 4）

`(dbx) delete 3`（移除跟踪 3）

`(dbx) status`（查看哪些跟踪和断点）

`[1] trace read`

`[2] trace write`

`(dbx) cont`（继续执行）

`%2 returning 0 from lower`

`%2 calling write() from function main`

`%2 returning 20 from write`

`%2 calling read() from function main`

`%2 returning 0 from read`

`%2 Stopped by Exit in _exit at 0x13a5`

```
(dbx) quit (退出 dbx)
```

在 `trace` 输出行之前的前缀 `%2` 表示受 `dbx` 控制的子进程（`lowercase`）的进程编号，我们将在下一节中看到。

# 高级 dbx 使用

在了解基本命令后，你已经准备好探索 `dbx` 的全部威力。之前列出的任何 `trace` 和 `stop` 命令后面都可以跟上：

```
if condition
```

只有当用 C 语法给定的 `condition` 满足时，跟踪和断点操作才会生效。还可以设置与位置无关的断点：

```
stop if condition
```

它会在给定的条件变为真时立即暂停执行。例如

```
stop if queue_length > 100
```

可以用于在全局变量 `queue_length` 大于 100 时中断执行。

你还可以指定在特定条件为真时执行的 `dbx` 命令。以下命令：

```
when in function {command; ...}
when at line {command; ...}
when condition {command; ...}
```

在函数被调用、到达某行或条件为真时，会执行 `dbx` 命令（多个命令）。

在断点处，你可以直接调用任何函数来检查其行为。要做到这一点，使用命令：

```
call function (从 dbx 中调用函数)
```

来执行命名的函数。当然，你必须提供正确的参数，`dbx` 可以将它们传递给函数。指定参数时，可以使用作为常量的表达式、程序中的变量，或通过运算符组合这些值（当然是使用 C 语法）。取决于你版本的 `dbx` 的复杂程度，可能还允许其他表达式。

可以使用

```
dump function (显示与函数相关的值)
```

来显示当前或指定函数局部变量和参数的名称和值。在函数 `lower` 处停止后，你可以进入 `dump` 并类似：

```
lower(buf="Abcd EFGH\nIj kL\n", length = 16), line 22 in "lowercase.c"
```

可以使用

```
set var = expression
```

# 第 10 章 C 语言 UNIX 程序

为了以后使用，在变量中记住表达式的值。同样在 `lower` 断点处。

```
set n = length
set string = buf
print string
```

可以输入这些。稍后可以使用变量 `length` 和 `string`，例如在 `call` 命令中。

`dbx` 还提供了一项类似于 shell 中作业控制的功能。在断点处，你可以启动程序的另一个运行，从而创建一个可以以相同方式控制的另一个进程。`ps` 命令显示 `dbx` 下的所有活动进程及其分配的编号。你也可以使用 `/i` 命令在这些子进程之间切换，其中 `i` 是子 ID。

# 10.7 检查核心储（CORE DUMPS）

在我们之前的示例中，没有错误。当你的可执行程序遇到错误时，通常会产生一个核心储文件。该文件默认命名为 `core`，是你的运行程序在错误发生后内存镜像的副本。检查核心储就像调查犯罪现场——如果你能弄明白它们的含义，线索都在那里。例如，你可以通过键盘上的退出字符（^）来产生核心储。

`core` 文件的创建也可能受到你 shell 中设置的限制控制。输入 `csh` 命令

```
limit
```

显示该 shell 下设置的任何限制。不会产生大于 `coreumpsize` 的核心储。特别是

```
limit coreumpsize 0
```

*会阻止产生任何核心储。*

如果 `core` 文件位于你调用 `dbx` 执行可执行文件的当前目录，该核心文件提供的信息也将被读取供你检查。产生核心文件的可执行文件不需要使用 `-g` 标志编译，只要传递给 `dbx` 的可执行文件即可。

此外，核心储中还保留了两个重要信息：最后执行的行以及核心储产生时的函数调用。在调用 `dbx` 之后，你应该发布 `list` 命令来查看最后一行是什么。此外，通过给出 `where` 命令查看导致错误之前的函数调用。

> *此功能可能在所有的 csh shell 上不可用。*

# 10.7 检查核心储 325

让我们来看一个例子。取 `sample.c` 文件中的以下代码。

```
#include <stdio.h>

int main() {
    int i = 0;
    int a[10];
    while (i <= -1) {
        a[i++] = -1;
        printf("after while\n");
    }
}
```

如果你编译并运行此文件，你会发现它需要很长的时间，程序很可能陷入了某种无限循环中。但唯一的循环是 `while`，它看起来并没有明显的错误。所以你按下 `\` 产生一个核心文件，并使用 `dbx` 查看问题，

```
cc -g sample.c
dbx a out
```

并进行如下调试会话：

```
dbx version 5.10 of 7/15/88 18:13
Type 'help' for help.
reading symbolic information...
[using memory image in core]
dbx list
    7        a[i++] = -1;
    8        printf("after while\n");
    }
dbx print i
0
dbx trace 7
    7        a[i++] = -1;
    8        printf("after while\n");
    }
dbx trace i
0
dbx run
%2 calling read()) from function main
%2 returning 0 from read
%2 calling lower (buf = "Now Is The Time For\n", length = 20)
from function main
%2 Stopped at breakpoint 4 in lower at line 22
22 { while (length-- > 0)
(dbx) where (display function stack)
lower(buf = "Now Is The Time For\n", length = 20),
line 22 in "lowercase.c"
main(argc, 1, argv = 0xff314, 0xff31c), line 10 in "lowercase.c"
(dbx) whatis buf
char *buf;
(dbx) step (single stepping)
%2 Stopped after step in lower at line 23
23 { if (isupper(*buf))
(dbx) print *buf (display info)
'N'
(dbx) step
%2 Stopped after step in lower at line 24
24 *buf = tolower(*buf);
(dbx) step
%2 Stopped after step in lower at line 25
25 buf++;
(dbx) print *buf
'N'
(dbx) delete 4 (移除断点 4)
(dbx) delete 3 (移除跟踪 3)
(dbx) status (查看哪些跟踪和断点存在)
[1] trace read
[2] trace write
(dbx) cont (继续执行)
%2 returning 0 from lower
%2 calling write() from function main
%2 returning 20 from write
%2 calling read() from function main
%2 returning 0 from read
%2 Stopped by Exit in _exit at 0x13a5
```

`(dbx) quit`（退出 `dbx`）

在 `trace` 输出行之前的前缀 `%2` 表示受 `dbx` 控制的子进程（`lowercase`）的进程编号，我们将在下一节中看到。

# 高级 dbx 使用

在了解基本命令后，你已经准备好探索 `dbx` 的全部威力。之前列出的任何 `trace` 和 `stop` 命令后面都可以跟上：

```
if condition
```

只有当用 C 语法给定的 `condition` 满足时，跟踪和断点操作才会生效。还可以设置与位置无关的断点：

```
stop if condition
```

它会在给定的条件变为真时立即暂停执行。例如

```
stop if queue_length > 100
```

可以用于在全局变量 `queue_length` 大于 100 时中断执行。

你还可以指定在特定条件为真时执行的 `dbx` 命令。以下命令：

```
when in function {command; ...}
when at line {command; ...}
when condition {command; ...}
```

在函数被调用、到达某行或条件为真时，会执行 `dbx` 命令。

在断点处，你可以直接调用任何函数来检查其行为。要做到这一点，使用命令：

```
call function (从 dbx 中调用函数)
```

来执行命名的函数。当然，你必须提供正确的参数，`dbx` 可以将它们传递给函数。指定参数时，可以使用作为常量的表达式、程序中的变量，或通过运算符组合这些值（当然是使用 C 语法）。取决于你版本的 `dbx` 的复杂程度，可能还允许其他表达式。

可以使用

```
dump function (显示与函数相关的值)
```

来显示当前或指定函数局部变量和参数的名称和值。在函数 `lower` 处停止后，你可以进入 `dump` 并类似：

```
lower(buf="Abcd EFGH\nIj kL\n", length = 16), line 22 in "lowercase.c"
```

可以使用

```
set var = expression
```

# 第 10 章 C 语言 UNIX 程序

为了以后使用，在变量中记住表达式的值。同样在 `lower` 断点处。

```
set n = length
set string = buf
print string
```

可以输入这些。稍后可以使用变量 `length` 和 `string`，例如在 `call` 命令中。

`dbx` 还提供了一项类似于 shell 中作业控制的功能。在断点处，你可以启动程序的另一个运行，从而创建一个可以以相同方式控制的另一个进程。`ps` 命令显示 `dbx` 下的所有活动进程及其分配的编号。你也可以使用 `/i` 命令在这些子进程之间切换，其中 `i` 是子 ID。

# 10.7 检查核心储（CORE DUMPS）

在我们之前的示例中，没有错误。当你的可执行程序遇到错误时，通常会产生一个核心储文件。该文件默认命名为 `core`，是你的运行程序在错误发生后内存镜像的副本。检查核心储就像调查犯罪现场——如果你能弄明白它们的含义，线索都在那里。例如，你可以通过键盘上的退出字符（^）来产生核心储。

`core` 文件的创建也可能受到你 shell 中设置的限制控制。输入 `csh` 命令

```
limit
```

显示该 shell 下设置的任何限制。不会产生大于 `coreumpsize` 的核心储。特别是

```
limit coreumpsize 0
```

*会阻止产生任何核心储。*

如果 `core` 文件位于你调用 `dbx` 执行可执行文件的当前目录，该核心文件提供的信息也将被读取供你检查。产生核心文件的可执行文件不需要使用 `-g` 标志编译，只要传递给 `dbx` 的可执行文件即可。

此外，核心储中还保留了两个重要信息：最后执行的行以及核心储产生时的函数调用。在调用 `dbx` 之后，你应该发布 `list` 命令来查看最后一行是什么。此外，通过给出 `where` 命令查看导致错误之前的函数调用。

> *此功能可能在所有的 csh shell 上不可用。*

# 10.7 检查核心储 325

让我们来看一个例子。取 `sample.c` 文件中的以下代码。

```
#include <stdio.h>

int main() {
    int i = 0;
    int a[10];
    while (i <= -1) {
        a[i++] = -1;
        printf("after while\n");
    }
}
```

如果你编译并运行此文件，你会发现它需要很长的时间，程序很可能陷入了某种无限循环中。但唯一的循环是 `while`，它看起来并没有明显的错误。所以你按下 `\` 产生一个核心文件，并使用 `dbx` 查看问题，

```
cc -g sample.c
dbx a out
```

并进行如下调试会话：

```
dbx version 5.10 of 7/15/88 18:13
Type 'help' for help.
reading symbolic information...
[using memory image in core]
dbx list
    7        a[i++] = -1;
    8        printf("after while\n");
    }
dbx print i
0
dbx trace 7
    7        a[i++] = -1;
```
