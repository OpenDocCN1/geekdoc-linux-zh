
here it is observed that next stepper over function is in line

```
(gdb) c
number 33
not a prime
program exited with code 0.
```

```
(gdb) break isprime
break point 1 at 0x008086; File gdbex.c, line 5
(gdb) r
starting program: /root/a.out
enter number 54
breakpoint 1, isprime (x=54) at gdbex.c:5
5 for (i =2; i<=x/2; i++)
```

here break point is given for a function

```
(gdb) break main
break point 2 at 0x8048369: File gdbex.c, line 13
(gdb) r
starting program: /root/a.out
breakpoint 2 main () at gdbex.c:13
13 For (i = 1; i<=3; i++)
```

# GNU 调试器

```
(gdb) break 5
breakpoint 5, at 0x8048362: File gdbex.c Line 5
(gdb) delete
delete all breakpoints/y or n
(gdb) break 5
breakpoint 1, at 0x8048362: File gdbex.c, line 5
(gdb) r
starting program: /root/a.out
enter number 34
breakpoint, isprime (x=34) at gdbex.c:5
for (i=2; i<=x/2; i++)
(gdb) bt
# 0 isprime (x=34) at gdbex.c: 5
# 1 0x0004887 in main () at gdbex.c:17
# 2 0x004215574 in __libc_start_main () from /lib/tls/libc.so.
```

# 示例 4

下面的程序也被用于解释如何使用 gdb 调试程序。下面列出了示例 `gdb-example.c`。这是一个简单但有错误的程序，可以在 gdb 下运行。

```c
#include <stdio.h>

void print_scrambled(char *message) {
  int i = 3;
  do {
    printf("%c", (*message)+i);
  } while (*++message);
  printf("\n");
}

int main() {
  char * bad_message = NULL;
  char * good_message = "Hello, world.";
  print_scrambled(good_message);
  print_scrambled(bad_message);
}
```

# Linux 简介：安装与编程

通过 gdb 输出，`list`、`info locals` 和 `info args` 命令可以获取当前选栈帧的信息。除了使用 `up` 命令选择之前的帧外，你也可以使用 `down` 命令选择后续的帧，或者使用 `frame` 命令（带有数字参数）选择要切换到哪个栈帧。

## 获取更多信息

gdb 还可以允许你在程序运行时逐行执行，这样你就可以仔细跟踪它的步骤。下面的 gdb 会话演示了如何进行这些操作。

```
gdb -q gdb-example
This GDB was configured as "i386-redhat-linux-gnu"...Using host libthread_db library "/lib/tls/libthread_db.so.1".
Breakpoint 1 at 0x0804839c: file gdbex.c, line 16.
(gdb) run
Starting program: /root/a.out
Breakpoint 1, main () at gdb.c:16
16 char * bad_message = NULL;
(gdb) print bad_message
$1 = 0x0
(gdb) print good_message
$2 = "Hello, world."
(gdb) next
17 char * good_message = "Hello, world.";
(gdb) print bad_message
$3 = 0x0
(gdb) next
19 print_scrambled(good_message);
(gdb) next
20 print_scrambled(bad_message);
(gdb) step
print_scrambled(message=0x0) at gdbex.c:5
4 void print_scrambled(char *message)
5 {
6     int i = 3;
7     do {
8         printf("%c", (*message)+i);
9     while (*++message);
10    printf("\n");
11  }
12 }
(gdb) info locals
i = 3
(gdb) info args
message = 0x0
(gdb) up
#1 0x000483c3 in main () at gdb.c:20
20     print_scrambled(bad_message);
(gdb) next
8         printf("%c", (*message)+i);
(gdb) next
9         while (*++message);
(gdb) next
10    printf("\n");
(gdb) next
11  }
(gdb) next
12 }
(gdb) info locals
i = 3
(gdb) info args
message = 0x0
(gdb) up
#1 0x000483c3 in main () at gdb.c:20
20     print_scrambled(bad_message);
```

## GNU 调试器 (GDB)

## 关于设置断点的更多

## 示例 6

最后，如上述，gdb 有多种设置断点的方法。下面的示例演示了如何在特定的行号以及程序使用的库函数中设置断点。

```
gdb -q gdb-example
This GDB was configured as "1386-redhat-linux-gnu"...Using host libthread-db library /lib/tls/libthreaddb.so.1.
(gdb) break gdb-example.c:19
Breakpoint 1 at 0x80483d2: file gdb-example.c, line 19.
(gdb) break printf
Function "printf" not defined.
Make breakpoint pending on future shared library load? (y or [n]) y
Breakpoint 2 (printf) pending.
(gdb) run
Starting program: /data/home/newren/floss-development/developing-with-gnome/examples/debugging/gdb/gdb-example
Breakpoint 1, main () at gdb-example.c:19
19 print_scrambled(good_message);
(gdb) where
#0 main () at gdb-example.c:19
(gdb) cont
Continuing.
Breakpoint 3, 0x004692a6 in printf () from /lib/tls/libc.so.6
(gdb) where
#0 0x004692a6 in printf () from /lib/tls/libc.so.6
#1 0x08048394 in print_scrambled(message=0x80484c99 "Hello, world.") at gdb-example.c:8
#2 0x080483dd in main () at gdb-example.c:19
(gdb) cont
Continuing.
Breakpoint 3, 0x004692a6 in printf () from /lib/tls/libc.so.6
(gdb) where
#0 0x004692a6 in printf () from /lib/tls/libc.so.6
#1 0x08048394 in print_scrambled(message=0x804844ca "ello, world.") at gdb-example.c:8
#2 0x080483dd in main () at gdb-example.c:19
(gdb) delete 3
(gdb) cont
Continuing.
Program received signal SIGSEGV, Segmentation fault.
0x08048383 in print_scrambled (message=0x0) at gdb-example.c:8
8 printf("%c", (*message)+1);
(gdb) quit
The program is running. Exit anyway? (y or n) y
```

`continue` 命令（"continue" 的简写形式）指示 gdb 继续运行，直到遇到另一个断点或程序结束。`where` 命令与回溯（traceback）功能相同（它仅仅是一个别名）。`delete` 命令根据指定的断点编号移除断点（可以使用 `info breakpoints` 命令来配合 `delete` 使用）。

## 段错误 (Segment Violations)

什么是段错误？

段错误是指你的程序尝试使用未为程序保留的内存位置。在 C 中通过使用 `malloc` 为程序保留内存位置，在 C++ 中通过使用 `new`。

导致段错误的常见错误包括：

- 对 `NULL` 指针进行解引用
- 对未初始化的指针进行解引用
- 对已释放（在 C++ 中为已 `delete`）或超出作用域（函数中声明的数组的作用域）的指针进行解引用
- 在数组末尾写入
- 使用所有栈空间的递归函数。在某些系统上，这将会导致“栈溢出”报告，而在另一些系统上，它仅仅表现为另一种类型的段错误。

调试所有这些问题的策略是相同的：将核心文件（core file）加载到 GDB 中，进行回溯，进入你的代码作用域，并列出导致段错误的代码行。

## 示例 7

例如，在 Linux 系统上运行，这是一个使用 `example.c` 文件的会话示例。

```c
#include<stdio.h>

void foo() {
  char *x = 0;
  *x = 3;
}

int main() {
  foo();
  return 0;
}
```

```
gcc -g -o example.c
./example
```

上述程序如果执行会产生段错误，因为它试图在地址 0 处存储 3。有时也会出现 core dumped 消息，并在当前工作目录下看到一个以进程 PID 为后缀的 `core` 文件。如果你的配置文件（如 `/etc/profile`）中提到的 `core size` 为零，则不会创建核心文件。因此，如果你想为分析程序崩溃创建核心文件，可以在 shell 提示符处运行以下命令，然后运行你的程序，例如 example。

```
ulimit -S -c 100000
./example
```

现在配合核心文件调试你的程序（另见 bug-buddy⁴），请运行以下命令。

```
gdb -q example corefile
```

这只是加载了被调用的 example 示例以及核心文件，核心文件包含了 GDB 重构无效操作导致段错误时执行状态所需的所有信息。一旦加载了 gdb，我们得到：Program terminated with signal 11, Segmentation fault. 关于加载符号的一些信息：

```
#0 0x080483c in foo() at t.cpp:4
4 *x = 3;
```

所以，执行停止在 `foo()` 函数的第 4 行，正好是将 3 赋值给 `x` 指向的位置。只需打印指针的值通常就能解决问题。在这种情况下：

```
(gdb) print x
$1 = 0x0
```

打印 x 显示它指向内存地址 0x0（打印地址传统的十六进制表示）。地址 0x0 是无效的——事实上，它是 `NULL`。如果引用一个存储 0x0 位置的指针，就会像我们做的那样定义段错误。如果遇到更复杂的情况，例如系统调用或库函数（可能是因为传递了未初始化的指针），我们需要找出是哪个函数调用了它以及发生了什么。这是另一个调试会话：bug-buddy 在 Fedora 版本中可用。

## 示例 8

```c
#include <stdio.h>
#include <string.h>

void foo() {
    char *x = 0;
    strcpy(x, "Hello");
}

int main() {
    foo();
    return 0;
}
```

```
gcc -g -o example1 example1.c
./example
0x4019f3 in strcpy () from /lib.so
```

这次段错误是因为 `strcpy` 内部的某些操作。这意味着库函数出了问题吗？不！这意味着可能向函数传递了坏值。为了调试这一点，我们需要看到向 `strcpy` 传递了什么。

```
(gdb) bt
#0 0x4019f3 in strcpy () from /lib/tls/libc.6
#1 0x080483c in foo () at t.cpp:6
#2 0x3e3 in main () at t.cpp:11
```

回溯显示了崩溃时进行的函数调用。每个函数都在调用它的函数上方。所以在这种情况下，`foo` 是由 `main` 调用的。数字（#0, #1, #2）指示了从最近到最远的调用顺序。要在栈帧内移动（这与栈的打印方式相反），我们可以使用 `up` 和 `down` 命令。现在我们知道自己在栈帧中，它包含了 `strcat` 的所有局部变量，因为它是栈顶函数。我们想要“向上”（向更大的数字移动）；这与栈的打印方式相反。

```
(gdb) up
#1 0x080483c in foo () at t.cpp:6
6      strcpy(x, "Hello");
```

这有一点帮助——我们知道有一个变量 `x` 和一个常量字符串。我们应该在此处查找函数，以确保参数顺序是正确的。既然是正确的，问题出在 `x` 上。

```
(gdb) print x
$1 = 0x0
```

又又是 `NULL` 指针。`strcpy` 函数必须引用了我们给它的 `NULL` 指针，尽管它是一个库函数，但并没有做任何魔法。

## 示例 9

下面的示例由于上述原因也产生段错误。

```c
#include <stdio.h>

int main (int argc, char **argv) {
    int i;
    printf("Hello, world!\n");
    /* 打印命令行参数的首字符 */
    for (i=0; i<argc; i++) {
        printf("%c", argv[i][0]);
    }
    printf("\n");
    return 0;
}
```

```
./a.out ram rama
Hello, world!
Segmentation fault (core dumped)
ls -l core.*
-rw------- 1 root 118624 Apr 29 12:04 core.4969
gdb -q a.out core.4969
Using host libthread_db library `/lib/tls/libthread_db.so.1`.
Core was generated by `./a.out rama`.
Program terminated with signal 11, Segmentation fault.
Reading symbols from `/lib/tls/libc.so.6...done.
Loaded symbols for /lib/tls/libc.so.6
Reading symbols from `/lib/id-linux.so.2...done.
Loaded symbols for /lib/id-linux.so.2
#0 0x08048b6 in main (argc=3, argv=0xffff4f94) at a.c:11
11
(gdb) print printf("%c", argv[i]);
$1 = 3
(gdb) print argv[i]
$2 = 0x0
(gdb) q
```
