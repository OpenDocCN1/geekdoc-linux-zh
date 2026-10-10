
# 开发环境 IV

这一次，`gdb`的状态消息稍有不同。它显示如下：

```
GNU gdb 4.8

Copyright 1998 Free Software Foundation, Inc.

GDB 是免费软件，受 GNU 公共许可证保护，你可以在特定条件下修改并分发副本。输入 "show"
```

## 开发环境

### 第四部分

`gdb`的输出。这可以使调试界面变得显著整洁，特别是对于产生大量输出的程序。

- 可以在需要的地方仅挂载。

让我们逐步通过这种挂载示例。首先，是用于这些示例的样例代码：

```c
#include <stdio.h>
#include <string.h>

void dostuff(char *baz);
void crashme(char *bar);

int main(void) {
    char *foo = strdup("Welcome!");
    printf("Hi!\n");
    dostuff(foo);
    printf("Hi: %s\n", foo);
}

void gostuff(char *baz) {
    char quux[80];
    sprintf(quux, "%s; %s", baz, baz);
    crashme(quux);
}

void crashme(char *bar) {
    printf("Enter greeting: %s");
    fgets(bar, 20, stdin);
    printf("I didn't like that one. Try again: %s");
    bar = 0;
    fgets(bar, 20, stdin);
}
```

注意，这是之前导致段错误的代码的修改版本。现在，像往常一样编译代码：

```
gcc -g3 -o test.c
```

在此时，你可能想直接运行程序看看它做了什么：

```
./test
```

```
Hi!

I didn't like that one. Try again: Hi

Segmentation fault
```

现在，重新启动程序。这次，在它请求第一个问候语后，不要立即输入。相反，打开另一个 xterm 或虚拟控制台。你将使用另一个终端运行 `gdb`。

# C/C++ 开发环境

## 第 24 章

要做的第一件事是找到测试程序的进程。这个 `ps` 命令可能会有所帮助：

```
ps x | grep test
```

你会得到一个类似这样的结果：

```
1100 pts/3    S    0:00 ./test
```

该行中的第一个数字；它是测试程序的进程 ID（PID），你需要将其传递给 `gdb`。现在，是启动 `gdb`。告诉它使用测试程序并挂载到已运行的进程：

```
gdb test 1100
```

当然，用你通过 `ps` 得到的结果替换 `1100`。

这次，`gdb` 在启动时显示以下内容：

```
/home/username/foo/1100: No such file or directory.
Attaching to program: /home/username/foo/test, process 1100
Reading symbols from /lib/libc.so.6...\done.
Reading symbols from /lib/ld-linux.so.2...\done.
0x040bd784 in read () from /lib/libc.so
```

等一下，让我重读一遍。它按照指定挂载到了进程 `1100`。它加载了适当的库符号并告诉你当前执行点的位置：在 C 库内部，在 `read()` 系统调用中，正在等待输入。

现在，弄清楚这相对于代码其他部分的位置是有用的。这样做将向你显示已调用的函数，以便你理解到当前进程的执行情况：

```
(gdb) info stack
#0 0x040bd784 in read () from /lib/libc.so.6
#1 0x0481774c in crash () from /lib/libc.so.6
#2 0x006e791 in _io_new_file_overflow () from /lib/libc.so.6
#3 0x006ef9d5 in _default_uflow () from /lib/libc.so.6
#4 0x006fd00 in _uflow () from /lib/libc.so.6
#5 0x006b885 in _get_info () from /lib/libc.so.6
#6 0x006bd2d in _get_line () from /lib/libc.so.6
#7 0x04cafe2 in fgets () from /lib/libc.so.6
#8 0x0848551 in crashme (bar=0xbffffcd8 "Welcome! Welcome!") at test.c:22
#9 0x0848528 in dostuff (baz=0x08484900 "Welcome!") at test.c:17
#10 0x0848d4e in main () at test.c:10
```

`gdb` 显示了大量看起来并不完全奇怪的信息。它正在向你显示 C 库内部的堆栈帧；这是被调用的 `gets()` 函数。这可能是可以忽略的，因为这不是你的代码；关键在第 8 帧，那里执行正处于所编写的代码中。

![](img/f36419c0b225d12fa66de83fa271829b_800_0.png)

让我们设置一个断点，以便 C 库函数可以完成，当测试代码中还有其他要执行的操作时跳回调试器：

```
(gdb) break test.c:23
Breakpoint 1 at 0x0848554: test.c, line 23.
```

告诉 `gdb` 继续执行程序直到到达断点：

```
(gdb) continue
Continuing.
```

此时，`gdb` 将会一直坐在那里，显然什么也没做。切换到另一个终端并按回车，显示已完成的内容。`gdb` 指出已命中断点并显示信息，然后是提示符：

```
Breakpoint 1, crashme(bar=0xffffc8) at test.c:23
printf('I didn't like that one. Try again: ');
```

注意与程序的交互在一个窗口中进行，而与 `gdb` 的交互在另一个窗口进行。现在，单步执行 `printf()`：

```
(gdb) s
bar = 0
```

你可能会惊讶地发现提示符实际上还没有出现在程序窗口中。原因是输出在内部缓冲的，直到遇到换行符或尝试从终端读取。这是 C 库出于性能考虑而做的。继续再次按 `s`：

```
(gdb) s
gets(bar, 20, stdin);
```

检查 `bar` 和 `stdin` 的内容，以防万一：

```
(gdb) print bar
$1 = 0x0
(gdb) print stdin
$2 = 0x7ffff74560
```

看起来很奇怪。`stdin` 是指向文件句柄的指针，因此它很大并不意外。现在，`gdb` 执行了 `gets()` 调用：

```
(gdb) s
```

注意另一个终端中执行的程序显示了等待中的提示符，因为有输入请求。然后它等待输入。在这一切过程中，`gdb` 暂停了，等待 `gets()` 返回。输入一些简单的问候并按回车。`gdb` 恢复了运行并提到

```
Program received signal SIGSEGV, Segmentation fault.
0x00406b8d3 in _getline_info () from /lib/libc.so.6
```

现在显而易见，段错误发生在调用 `fgets()` 处，并且是因为 `bar` 为 0。剩余的分析是学术性的，但我们继续进行以演示更多几项：

```
(gdb) bt
#0 0x0046b8d3 in _getline_info () from /lib/libc.so.6
#1 0x00468b2d in _getline_info () from /lib/libc.so.6
#2 0x0046afae2 in fgets () from /lib/libc.so.6
#3 0x0848579 in crash (bar=0x0) at test.c:25
#4 0x0848528 in dostuff (baz=0x08499e0 "Welcome!") at test.c:17
#5 0x0848a4de in main () at test.c:10
```

堆栈回溯结果在很大程度上符合预期；崩溃前测试代码中执行的最后一行是 `test.c` 的第 25 行，崩溃发生在 C 库的 `fgets()` 实现内部。此时，可以切换帧并分析其内容，就像分析核心文件时一样；然而，过程是相同的，所以我们继续退出程序：
