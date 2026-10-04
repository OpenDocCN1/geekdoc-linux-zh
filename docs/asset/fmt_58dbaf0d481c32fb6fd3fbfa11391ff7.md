
本章解释了在 Linux/Unix 环境下编译 C 程序。书中逐步解释了编译阶段及其目标。此外，还解释了多文件编程。最后，还解释了如何在 Linux/Unix 下编译“c++”程序。同样，也逐步解释了如何混合 C、C++ 程序。此外，`main()` 实际上是如何启动的以及 Linux 操作系统如何协调它的，是本章的一个特别处理内容。

# 19 GNU 调试器

## 19.1 引言

GNU 调试器主要关注调试。它包含某些语言。

| 宏 | 描述 |
| :--- | :--- |
| `LINE` | 表示行号的十常量。 |
| `FILE` | 表示文件名的字符串。 |
| `DATE` | 格式为“mm:dd:yyyy”的字符串。 |
| `TIME` | 格式为“hh:mm:ss”的字符串。 |

### 19.1.1 Bug 与调试

Bug 是错误。调试意味着检测并消除 Bug。如果指定的程序错误，将导致失败。Bug 发生在设计阶段。调试有三种：

## 19.2 使用 gdb 调试

GDB 是 GNU 调试器的简称，是一个受 GNU 通用许可证（GPL）保护的免费软件。GDB 允许用户查看程序执行时的状态。GDB 可以完成以下工作：

- 启动你的程序，指定可能影响其行为的任何。
- 让你的程序在特定条件下停止。
- 查看程序停止时发生了什么。
- 修改你的程序，以便实验修正一个 Bug 并了解其他 Bug

如果加载了 Fortran 编译器，GDB 也可以用于调试 Fortran 程序通过通过 命令 `gdb` 调用。启动后，它从终端读取命令，直到我们按下退出。我们可以不带选项运行 `gdb` 命令。通常我们如下运行：

```bash
gdb program
```

这里 `program` 是要调试的可执行文件。使用 `-g` 选项编译。此选项将调试信息附加到原始可执行文件。如果我们想知道更多关于 gdb 的细节，可以像下面所示带有 `-help` 选项运行。

```
gdb -help
```

该命令将显示输出。用法：

```
gdb [options] [executable-file [core-file or process-id]]
gdb [options] --args executable-file [inferior-arguments ...]
```

选项：

- `--args` 可执行文件后的参数将传递给从进程
- `--[no]async` 启用（禁用）异步版本的 CLI
- `--b BAUDRATE` 设置远程调试使用的串口端口波特率。
- `--batch` 在处理选项后退出。
- `--cd=DIR` 将当前目录改为 DIR。
- `--command=FILE` 从 FILE 执行 GDB 命令。
- `--core=COREFILE` 分析转储文件 COREFILE。
- `--pid=PID` 连接到运行的进程 PID。
- `--dbx` DBX 兼容模式。
- `--directory=DIR` 在 DIR 中搜索源文件。
- `--epoch` 输出 epoch emacs-GDB 接口的信息。
- `--exec=EXECFILE` 使用 EXECFILE 作为可执行文件。
- `--fullname` 输出 emacs-GDB 接口使用的输出信息。
- `--help` 打印此消息。
- `--interpreter=INTERP` 选择特定的解释器 / 用户界面。
- `--mapped` 如果系统支持，则使用映射的符号文件。
- `--nw` 不使用窗口界面。
- `--nx` 不读取 `.gdbinit` 文件。
- `--quiet` 启动时不打印版本号。
- `--readnow` 在首次访问时完全读取符号文件。
- `--se=FILE` 使用 FILE 作为符号文件和可执行文件。
- `--symbols=SYMFILE` 从 SYMFILE 读取符号。
- `--tty=TTY` 使用 TTY 作为被调试程序的输入/输出控制台。
- `--version` 打印版本信息后退出。
- `--w` 使用窗口界面。
- `--write` 将输出写入可执行文件和核心转储文件（core files）。
- `--xdb` 进入 XDB 兼容模式。

## 示例 1

让我们考虑一个简单的程序 (`ex1.c`) 并看看我们如何使用 gdb 进行调试。

```c
#include <stdio.h>
int main()
{
  printf("Hello How are you?\n");
  return 23;
}
```

首先使用 `-g` 选项编译该程序。即执行以下命令。

```bash
gcc -g ex1.c
```

为了调试该可执行文件，执行以下命令，它会在显示 gdb 提示符（即 `(gdb)` ）之前显示许多详细信息：

```bash
gdb a.out
GNU gdb Red Hat Linux (5.3post-0.20021129.18)
Copyright 2003 Free Software Foundation, Inc.
GDB 是免费软件，受 GNU 通用公共许可证保护，我们欢迎在某些条件下更改和/或分发其副本。
输入 "show copying" 查看条件。
GDB 不提供任何质保证。输入 "show warranty" 查看详情。
此 GDB 已配置为 "i386-redhat-linux-gnu"... 
(gdb) r
Starting program: /root/nav/a.out
Hello How are You?
Program exited with code 023.
(gdb) q
```

如果我们想启动 gdb 且不想看到所有这些消息，可以使用 `-q` 选项启动 gdb，例如：

```bash
gdb -q a.out
```

```bash
(gdb) r
Starting program: /root/a.out
Hello How are You?
Program exited with code 023.
(gdb) q
```

## 19.2.1 可在 gdb 提示符使用的命令

### Break（断点）

Break 命令用于在文件的任意行或任何函数处设置断点。

**语法概要：**

`Break [file : ] function`

这里的 `file` 是文件的文件名，`function` 是需要设置断点的函数名。如果我们想在某行上设置断点，执行将在该指令执行之前停止。如果我们为函数设置断点，执行将在函数的第一条语句处停止。

### Run（运行）

Run 命令用于运行正在调试的程序。如果我们在程序正在调试时输入此命令，系统会询问我们是否想从开始运行。

**语法概要：**

`Run [arglist]`

`Arglist` 是命令行参数列表。它是可选的。`run` 的简写形式为 `r`。

### Back trace（回溯）

Back trace 命令用于显示程序堆栈。这显示了程序的运行时状态。

**语法概要：**

`bt`

此命令允许我们了解当前激活的函数及其信息。`bt` 是 back trace 的简写。

### Print（打印）

Print 命令用于显示程序运行某一时刻变量和表达式的值。

**语法概要：**

`Print [expression ]`

表达式可以是一个单独变量，也可以是通用表达式。如果我们提供变量名并加上 `&` 符号作为表达式（expr），则会显示该值的地址。`print` 的简写形式为 `p`。

### Continue（继续）

Continue 命令从断点处继续执行程序，直到遇到下一个断点或程序结束。

**语法概要：**

`Continue`

Continue 有助于程序从从一个断点到另一个断点的流程，允许程序员检测 bug 所在的位置。`continue` 的简写形式为 `c`。

### Next（单步执行）

Next 命令用于执行被调试程序的下一行。它会跳过行中的函数调用。

**语法概要：**

`next`

此命令会跳过行中的任何函数调用，将带有函数调用的行视为单条指令。`next` 的简写形式为 `n`。

### Step（单步进入）

Step 命令与 next 相同，但它会进入行中出现的任何函数内部。

**语法概要：**

`step`

此命令有助于跟踪甚至是行中出现的函数，从而使得调试文件的过程比使用 next 清得多。

### Edit（编辑）

Edit 有助于找到执行停止的程序行。

**语法概要：**

`Edit [file : ] function`

### List（列出）

List 命令在当前停止的位置附近列出程序的文本。`function` 是函数名，`file` 是文件名。

### Help（帮助）

Help 命令显示关于命令名称的信息。

**语法概要：**

`Help [name]`

命令名称是可选的。如果没有未提供，则将显示关于 gdb 命令的信息。

### Quit（退出）

这用于退出 gdb。

**语法概要：**

`quit`

`quit` 的简写形式为 `q`。

## 示例 2

考虑另一个接收命令行参数的示例 (`ex2.c`)。

```c
#include<stdio.h>
int main(int N, char *a[])
{
  int i;
  for(i=0; i<N; i++) {
    printf("%s\n", a[i]);
  }
  return 0;
}
```

使用 `-g` 选项编译上述程序，然后启动 gdb。即：

```bash
gcc -g ex2.c
gdb -q a.out
```

```bash
(gdb) r
Starting program: /root/a.out
Hello How are You?
Program exited with code 023.
```

如果我们愿意，可以将所有想要传递给 gdb 的命令写在一个文件中，并要求 gdb 使用这些命令来调试我们的程序。例如，让文件 "abc" 包含以下 gdb 命令。

现在，如下方式启动 gdb：

```bash
gdb -x abc a.out
```

## 示例 3

使用以下示例解释了一些 gdb 命令。在接下来的 gdb 会话输出中，你可以看到在调试程序时如何使用 gdb 命令。

| 行号 | 文本 |
| :--- | :--- |
| 1 | `#include <stdio.h>` |
| 2 | `int isprime(int x)` |
| 3 | `{` |
| 4 | `int i;` |
| 5 | `for(i=2; i<=x; i++)` |
| 6 | `if (x % i == 0)` |
| 7 | `return 0;` |
| 8 | `return 1;` |
| 9 | `}` |
| 10 | `int main()` |
| 11 | `{` |
| 12 | `  int i, x;` |
| 13 | `  for(i=0; i<=3; i++)` |
| 14 | `    printf("Enter a number: ");` |
| 15 | `    scanf("%d",&x);` |
| 16 | `    if (!isprime(x))` |
| 17 | `      printf("not a prime number\n");` |
| 18 | `    else` |
| 19 | `      printf("a prime number\n");` |
| 20 | `  }` |
| 21 | `  return 0;` |
| 22 | `}` |

现在在命令提示符处为此程序 `gdb.c` 执行这些命令。

```bash
gcc -g gdb.c
gdb -q a.out
```

```bash
(gdb) r
Starting program: /root/a.out
Enter a number: 23
It is a prime number.
Enter a number: 44
Not a prime number.
Enter a number: 31
A prime number.
Program exited with code 0
```

这里程序一直执行到结束，因为没有断点。我们保留断点。

```bash
(gdb) break 18
Breakpoint 1 at 0x080483fe in main at gdb.c:18
在这里在 18 处创建了一个编号为 1 的断点。
现在运行程序。
```

```bash
(gdb) r
Starting program: /root/a.out
Enter a number: 23
It is a prime number.
Enter a number: 44
Not a prime number
Breakpoint/main () at gdb.c:18
printf("not a prime")
```

这里观察到程序停止在第18行。我们可以打印变量的值：

```bash
(gdb) print x
$1 = 44
(gdb) print &x
$2 = (int *) 0xffffeb4
这里显示了 x 的地址。
(gdb) print i
$3 = 2
(gdb) print &i
$4 = (int *) 0xfffffc0
```

`Info locals` 需要特殊说明。

上述提供了程序局部变量的信息。

```bash
(gdb) info registers
eax 0x0
cx 0x0
edx 0x0
ebx 0x42130a14 1708544020
esp 0xffffffec 0xffffec0
ebp 0xbffff8 0xbffff8
esi 0x40015360 1073828704
edx 0x804845c 134513756
eip 0x80483fe 0x80483fe
efl 0x243 582
ss 0x2b 43
es 0x2b 43
fs 0x0
gs 0x33 51
```

上述提供了寄存器值的信息。

```bash
(gdb) info args
no arguments
这是关于命令行参数的。
(gdb) info functions
All defined Functions
File gdbx .c
int isprime (int)
Non-debugging symbols
0x08048254 - init
0x0804827c - scanf
```

上述提供了函数的信息。

```bash
(gdb) info breakpoints
Num Type Disp Enb Address What
1 breakpoint lay 0x080483fe in main at gdb.c;8
breakpoint已命中 1 次。
```

上述提供了当前激活的断点的信息。

本地执行文件

```
/root/a-out, filetype ELF32-i386
entry point: 0x80482ac.
...
(gdb) info proc
process 2077
cmdline = a.out
cmd = /root
exe = /a.out.
(gdb) list
13 for (i = 1; i<=3; i++)
14 {
15 printf("Enter a number");
16 scanf("%d", &x)
17 if (isprime(x))
18 printf("not a prime number");
19 else
21 }
22 }
```

此阶段的回溯轨迹如下：

```bash
(gdb) bt
# 0 main () @ libc.c:18
# 1 0x004215574 in __libc_start_main () from /lib/tls./libc.so.6
```

```bash
(gdb) break 5
break point 2 at 0x8048362: File gdbex.c:line 5
(gdb) c
continuing
not a prime number
enter a number 7
'breakpoint 2, i<=x/2; isprime(x=7) gdbex.c:5
5 for (i=2; i<=x/2; i++)
(gdb) info locals
i = 110854420
contains garbage as it is not initialized
(gdb) step
6 if (x % i == 0)
(gdb) info locals
i = 2
is initialized.
(gdb) s
continuing
Is a prime number
program exited with code 0
This ends the program
```

```bash
(gdb) delete 1
```

```bash
(gdb) delete
Delete all breakpoints? 1 y or n 2 y
The first deletes 1 and second deletes all breakpoints.
```

```bash
(gdb) break 16
break 3 at 0x80483d5: file gdbex.c, line 10.
```

```bash
(gdb) step 2
isprime (x = 23) at gdbex.c:5
5 for (i = ; i<=x/2; i++) this step made 2 steps forward (one into the function isprime)
```

```bash
(gdb) c
continuing
it is prime
break point 3, main () at gdbex.c:16
16 scanf("%d", &x);
(gdb) step
enter number 56
```

```bash
17 if (f, isprime (x ))
(gdb) next
18 printf "not a prime";
```
