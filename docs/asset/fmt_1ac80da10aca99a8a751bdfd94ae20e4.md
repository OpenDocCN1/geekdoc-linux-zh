
由于我们没有在命令行提供参数，当 `i` 值为 3 时，观察到 `argv[i]` 为 0。因此我们得到了段错误。另一个错误是没有检查 `malloc` 的返回值以确保系统内存已充足。此外，另一个错误是假设调用 `malloc` 的函数不会返回 NULL，即使它返回了 `malloc` 的结果。

# GNU 调试器

我们在 `create_memory` 中使用内存之前检查 `malloc` 是否成功，这是一项很好的做法，但我们没有检查 `create_memory` 是否返回了有效指针。这是一个错误，除非你显式地在低内存情况下测试代码，否则在你在真实系统上运行代码之前它是不会发现的。

# 解引用未初始化的指针

判断一个指针是否已初始化比判断指针是否为 NULL 要稍微困难一点。避免使用未初始化指针的最佳方法是在声明（或初始化）指针时将其设置为 NULL。如果你对一个已经分配了内存的指针进行操作，你会立即判断出来。

如果你在声明指针时没有将它们设置为 NULL，那么处理起来会很棘手（记住，在任何 C 或 C++ 中，非静态变量都不会被初始化为 NULL）。你可能需要判断 `0x0425e800` 是否为有效内存。在 GDB 中，你可以通过打印存储在其他可能正确分配内存的指针中的地址来感受这一点。当然，无法保证这条规则在所有系统上都适用。

在某些情况下，调试器可以根据指针中存储的值告诉你某个地址是无效的。例如，在下面的示例中，GDB 指出 `char* x`（我将其指向内存地址 "0"）是不可访问的。

```
(gdb) print x
$ 0xe1 <out of bounds>
(gdb) print *x
Cannot access memory address at 0xe1
```

通常，处理此类情况的最佳方法是避免依赖内存是否紧密或明显无效。从一开始就将变量设置为 NULL。

# 解引用已释放的内存

这是另一个难以发现的错误，因为你正在操作的内存地址看起来有效的。处理此类情况的最佳方法是预防性的：在释放指针后将其设置为 NULL。如果你以后尝试使用它，你将遇到另一个“解引用 NULL”错误，这应该容易跟踪得多。

这种错误的另一种形式是处理超出作用域的内存。如果你这样声明一个局部数组：

```c
char *return_buffer()
{
    char x[10];
    strncppy(x, "string", sizeof(x));
    return x;
}
```

那么数组 `x` 将不再有效，因为当你在 GDB 中打印它时，该内存地址看起来仍然是有效的。事实上，你的代码有时甚至可以运行（或者只是表现得很奇怪，打印出栈上曾经是数组 `x` 内存位置的任何内容）。通常情况下，你会知道这种错误是：尽管你知道它已经初始化，但在打印该变量时会得到垃圾数据。注意函数返回的指针。如果该指针引起了问题，请检查函数并查看指针是否指向函数中的局部变量。请注意，返回指向使用 `new` 或 `malloc` 在函数中分配内存的指针是完全可以的，但不要返回静态数组的指针（例如 `char x[10]`）。

# 越界写入

通常，如果你写出了数组边界，那么最初导致段错误（segment fault）的那行应该是一个数组访问语句。（在少数情况下并非如此——特别是，写越界数组会导致栈溢出——基本上是覆盖了存储函数完成后返回地址的指针。）

当然，有时写出数组末尾并不会真的引起错误。相反，你可能注意到某些变量值在定期且意料的情况下发生变化。这是一个很难破解的错误；一种方法是设置调试器监控一个变量并运行程序直到该变量的值发生变化。调试器会在该指令处断点，你可以查看以确定行为是否符合预期。

```
(gdb) watch [variable name]
(gdb) continue
...
Hardware watchpoint 1: [variable name]
...
Hardware watchpoint 1: [variable name]
Old value = [value1]
New value = [value2]
```

当你处理大量动态分配的内存且不清楚应该监控什么时，这种方法会变得复杂。为了简化问题，请使用简单的测试，保持使用相同的输入，如果你使用了随机数，请关闭随机种子！

# 栈溢出

栈溢出与其他指针相关问题不是同一类型。在这种情况下，你不需要在程序中有一个简单的显式指针；你只需要一个没有基准条件的递归函数。尽管如此，这是一个关于段错误的教程，在某些系统上，栈溢出会被报告为段错误。（这是合理的，因为栈内存耗尽会违反内存保护。）

要在 GDB 中诊断栈溢出，你只需要执行回溯（backtrace）：

# 以 GDB 方式解释普通递归和尾递归

在本节中，我们想展示普通递归（也称为直接递归或自递归）与尾递归之间的概念区别。为了这个目的，我们使用了两个版本的函数来计算整数的阶乘。查看程序 `fact1.c` 和 `fact2.c`。

# GNU 调试器 (GNU Debugger)

```bash
#1 0x08048418 in main () at fact1.c:15
(gdb) n
Factorial Value=24
main () at fact1.c:16
16 return 0;
(gdb) bt
#0 main () at fact1.c:16
(gdb) n
17 }
(gdb) n
0x004fbe33 in __libc_start_main()
from /lib/tls/libc.so.6
(gdb) n
Single stepping until exit from function __libc_start_main,
which has no line number information.
```

程序正常退出。

(gdb) q

# 示例 11

`cat fact2.c`

```c
#include <stdio.h>
int fact(int n, int a)
{
    if(n==0) return a;
    else
    return (fact(n-1,a*n));
}

int main ()
{
    int N;
    printf("Enter a Integer\n");
    scanf("%d", &N);

    printf("Factorial Value=%d\n", fact(N,1));
    return 0;
}
```

```bash
gcc -g fact2.c
gdb -q a.out
Using host libthread_db library "/lib/tls/libthread_db.so.1".
(gdb) break 6
Breakpoint 1 at 0x80483b0: file fact2.c, line 6.
(gdb) r
Starting program: /root/gdb/a.out
Enter Integer
4
Breakpoint 1, fact (n=4, a=1) at fact2.c:6
6 return (fact(n-1,a*n));
(gdb) n
Breakpoint 1, fact (n=3, a=4) at fact2.c:6
6 return (fact(n-1,a*n));
(gdb) n
Breakpoint 1, fact (n=2, a=12) at fact2.c:6
6 return (fact(n-1,a*n));
(gdb) n
Breakpoint 1, fact (n=1, a=24) at fact2.c:6
6 return (fact(n-1,a*n));
```

```bash
(gdb) bt
#0 fact (n=1, a=24) at fact2.c:6
#1 0x00483c5 in fact (n=2, a=12) at fact2.c:6
#2 0x00483c5 in fact (n=3, a=4) at fact2.c:6
#3 0x00483c5 in fact (n=4, a=1) at fact2.c:6
#4 0x0048481d in main () at fact2.c:15
(gdb) n
7
```

```bash
(gdb) bt
#0 fact (n=1, a=24) at fact2.c:7
#1 0x00483c5 in fact (n=2, a=12) at fact2.c:6
#2 0x00483c5 in fact (n=3, a=4) at fact2.c:6
#3 0x00483c5 in fact (n=4, a=1) at fact2.c:6
#4 0x0048481d in main () at fact2.c:15
(gdb) n
7
```

# GNU 调试器

```bash
#0 fact (n=2, a=12) at fact2.c:7
#1 0x080483c5 in fact (n=3, a=4) at fact2.c:6
#2 0x080483c5 in fact (n=4, a=1) at fact2.c:6
#3 0x0804841d in main () at fact2.c:15
(gdb) n
7
  }
(gdb) bt
#0 fact (n=3, a=4) at fact2.c:7
#1 0x080483c5 in fact (n=4, a=1) at fact2.c:6
#2 0x0804841d in main () at fact2.c:15
(gdb) n
7
  }
(gdb) bt
#0 fact (n=4, a=1) at fact2.c:7
#1 0x0804841d in main () at fact2.c:15
(gdb) n
Factorial Value=24
main () at fact2.c:16
16    return 0;
(gdb) bt
#0 main () at fact2.c:16
(gdb) n
17
  }
(gdb) n
0x004fbe33 in __libc_start_main()
from /lib/tls/libc.so.6
(gdb) n
Single stepping until exit from function __libc_start_main,
which has no line number information.

程序正常退出。
(gdb) q

gcc -g fact2.c
gdb -q a.out
Using host libthread_db library "/lib/tls/libthread_db.so.1".
(gdb) break 6
Breakpoint 1 at 0x80483b0: file fact2.c, line 6.
(gdb) r
Starting program: /root/gdb/a.out
Enter Integer
4
Breakpoint 1, fact (n=4, a=1) at fact2.c:6
6 return (fact(n-1,a*n));
(gdb) n
Breakpoint 1, fact (n=3, a=4) at fact2.c:6
6 return (fact(n-1,a*n));
(gdb) n
Breakpoint 1, fact (n=2, a=12) at fact2.c:6
6 return (fact(n-1,a*n));
(gdb) n
Breakpoint 1, fact (n=1, a=24) at fact2.c:6
6 return (fact(n-1,a*n));
```

```bash
(gdb) bt
#0 fact (n=1, a=24) at fact2.c:6
#1 0x00483c5 in fact (n=2, a=12) at fact2.c:6
#2 0x00483c5 in fact (n=3, a=4) at fact2.c:6
#3 0x00483c5 in fact (n=4, a=1) at fact2.c:6
#4 0x0048481d in main () at fact2.c:15
(gdb) n
7
```

```bash
(gdb) bt
#0 fact (n=1, a=24) at fact2.c:6
... (省略重复调试输出) ...
#4 0x0048481d in main () at fact2.c:15
(gdb) n
7
```

... (此处省略重复的调试过程，保持逻辑一致) ...

# 附加到已经在运行的进程

我们想要调试一个无法从命令行启动的程序。这可能是因为程序是由某些系统守护进程启动的（例如 Web 的 CGI 程序）。或者程序运行初始化代码需要很长时间，我们可以通过附加调试器继续运行它来捕获这段更长的启动时间。还有其他原因，但希望你理解了这一点。为了实现，我们将如下方式启动调试器：

```bash
gdb debug_me=9561
```

我们假设 "debug_me" 是执行的程序名称，而 9561 是我们要调试的进程标识 ID (PID)。

发生的情况是，gdb 首先尝试寻找名为 "9561" 的 "core" 文件（我们将在下一节查看什么是 core 文件），当它找不到文件时，它会假设提供的数字是进程 ID 并尝试附加到它。如果进程执行的程序与提供给 gdb 的路径完全相同（不是文件的副本，而是进程运行的完全相同的文件），它将附加到程序并暂停其执行，我们就可以像从调试器内部启动程序一样继续调试它。在获取 gdb 提示符时立即执行 "where" 将显示进程的堆跟踪，我们可以从那里继续。一旦退出调试器，它将从进程中脱离，进程将从它离开的地方继续执行。

为了演示这一点，我们使用以下程序，它每隔 5 秒打印一个从 0 开始的自然数：

# 示例 12

```c a7.c
#include<stdio.h>

int N=0;

void f() {
  printf("%d\n",N++);
}
```

```c
void ff() {
  f();
  sleep(5);
}
```

```c
int main() {
  while(1) {
    ff();
    return 0;
  }
}
```

```bash
gcc -g a7.c
./a.out & [1] 567
0
```

```bash
gdb -q a.out 567
2
Using host libthread_db library "/lib/tls/libthread_db.so.1".
(gdb) break 6
Breakpoint 1 at 0x80483b0: file fact2.c, line 6.
... (此处省略重复的调试输出) ...
```

# File b.c

```c
void ff()
{
printf("How are you?\n");
}
```

# File a.h

```c
void f();
void ff();
```

# File main.c

```c
#include<stdio.h>
#include "a.h"

int main()
{
f();
ff();
return 0;
}
```

对于上述示例，编写了以下 "makefile" 文件，它指示了文件之间的依赖关系。

```
myapp: main.o a.o main.o b.o
gcc -o myapp main.o a.o b.o
main: main.c a.h
gcc -c main.c
a.o: a.c
gcc -c a.c
b.o: b.c
gcc -c b.c
```

## 20.2.2 依赖

在上述示例中，`main.o` 受 `main.c` 和 `a.h` 变化的影响，如果这两个文件中的任何一个发生变化，都需要通过重新编译 `main.c` 来重新创建它。

同样，最终目标文件（可执行文件）"myapp" 依赖于 `main.o`、`a.o` 和 `b`；这些文件又具有上述的依赖关系。

在 make 中，我们通过编写目标名称、冒号、空格或制表符，然后是用空格或制表符分隔的文件列表来使用这些规则。我们示例的依赖列表为：

```
myapp: main a.o b.o
main.o: main.c a.h
a.o: a.c
b.o: b.c
```

我们可以很容易地看到，如果 `b` 发生了变化，我们需要重新编译 `b.o` 并且需要重建 `myapp`。

## 20.2.3 规则

makefile 的第二部分指定了描述如何创建目标的规则。在我们的示例中，当 make 命令确定 `a.o` 需要重新构建后，应该使用什么命令。

包含 makefile 的一种非常奇怪且不幸的语法：空格和制表符之间的区别。所有规则必须位于以制表符开头的行上；使用空格是不行的。

在命令行提示符处输入简单的 `make` 来运行命令。我们将在屏幕上看到以下消息。

```
gcc -c main.c
gcc -c a.c
gcc -c b.c
gcc -o myapp main.o a.o
```

现在，你只需要在命令行提示符处输入以下内容即可运行程序 "myapp"。

```
./myapp
```

如果 makefile 名称与默认文件名（如 makefile 或 Makefile）不同，我们使用 `-f` 配合文件名调用 make 命令。

如果我们在不包含源代码的目录中调用上述示例，将得到此 make 错误消息。

```
make: *** No rule to make target 'main.c', needed by 'main.o'. Stop. Stop.
```

此外，上面的 Makefile 可以像所示所示修改，因为 make 命令可以使用它自己的目标生成规则。

```
myapp: main.o a.o b.o
gcc -o myapp main.o a.o b.o
main.o: main.c a.h
a.o: a.c
b.o: b.c
```

在命令行提示符处输入 `make` 命令来运行上述（修改后的）makefile。我们在屏幕上看到以下消息。

```
cc -o a.o a.c
cc -o b.o b.c
cc -o main.c
gcc -o myapp main.o a.o b.o
```
