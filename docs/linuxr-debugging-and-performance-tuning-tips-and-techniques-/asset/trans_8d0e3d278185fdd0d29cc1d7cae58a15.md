

# 3.2.4 懒惰编程员的调用：alloca()

> > “危险，威尔·罗宾逊！危险！”
> > ——《机器人》

`brk()` 系统调用实际上会改变进程的地址空间。该地址是一个指针，代表数据段（实际上如前文图 3.1 所示，是堆区）的结束位置。它的参数是一个绝对逻辑地址，代表地址空间的新结束位置。成功时返回 0，失败时返回 -1。

`sbrk()` 函数则更易于使用；其参数是以字节为单位的地址空间增量。通过传入 0 作为增量，你可以确定地址空间当前结束的位置。因此，要将地址空间增加 32 字节，可以使用如下代码：

```c
char *p = (char *) sbrk(0);    /* 获取地址空间的当前末尾 */
if (sbrk(p + 32) < 0) {
    /* 处理错误 */
}
/* 否则，修改成功 */
```

从实际角度看，你不会直接使用 `brk()`。相反，你会专门使用 `sbrk()` 来增长（甚至缩减）地址空间。（我们将在 3.2.5 节“地址空间检查”，第 78 页中展示如何这样做。）

更实际地说，你绝不应该使用这些例程。使用了这些例程的程序就无法再使用 `malloc()`，这是一个大问题，因为标准库的许多部分都依赖于能够使用 `malloc()`。因此，使用 `brk()` 或 `sbrk()` 很可能导致难以排查的程序崩溃。

但了解底层机制是有价值的，事实上，`malloc()` 系列例程就是用 `sbrk()` 和 `brk()` 实现的。

还有一个额外的内存分配函数你应该知道。我们讨论它只是为了让你看到时能理解，但你不应该在新程序中使用它！这个函数名为 `alloca()`，其声明如下：

```c
/* GNU/Linux 的头文件，可能并非所有 Unix 系统都有 */  通用
#include <alloca.h>
void *alloca(size_t size);
```

`alloca()` 函数从 `栈` 分配 `size` 字节。其优点在于，分配的存储区域在函数返回时会自动消失。因为就像局部变量一样会自动消失，所以无需显式释放。

乍一看，`alloca()` 似乎是一种编程万能药：可以分配内存，且完全不需要管理。就像原力黑暗面一样，这确实具有诱惑力。但也同样应该避免，原因如下：

- 该函数非标准；它未包含在任何正式标准中，无论是 ISO C 还是 POSIX。
- 该函数不可移植。尽管它存在于许多 Unix 系统和 GNU/Linux 中，但在非 Unix 系统上并不存在。这是一个问题，因为代码往往需要在 Linux 和 Unix 之外的多平台上运行。
- 在某些系统上，甚至无法实现 `alloca()`。世界并不全是 Intel x86 处理器，也不全是 GCC。
- 引用 man 手册页（加粗部分为强调）：“`alloca` 函数依赖于机器和编译器。在许多系统上，其实现存在 bug。不推荐使用。”
- 再次引用 man 手册页：“在许多系统上，`alloca` 不能用于函数调用的参数列表中，因为 `alloca` 预留的栈空间会出现在栈中函数参数空间的中间。”
- 它鼓励随意编码。仔细且正确的内存管理并不难；你只需要思考自己在做什么并提前规划。

GCC 通常使用内置版本的函数，该函数通过内联代码来操作。因此，`alloca()` 还有其他后果。再次引用 man 手册页：

> 代码是内联的这一事实意味着，不可能获取该函数的地址，也不可能通过链接不同的库来改变其行为。内联代码通常由一条调整栈指针的指令组成，并且不检查栈溢出。因此，没有 `NULL` 错误返回值。

手动页对 GCC 内置 `alloca()` 的问题描述还不够彻底。如果发生栈溢出，返回值将是*垃圾数据*。而且你无从知晓！这个缺陷使得 GCC 的 `alloca()` 无法在健壮代码中使用。

以上所有内容应该足以说服你，在任何新编写的代码中都要远离 `alloca()`。反正如果你要编写使用 `malloc()` 和 `free()` 的可移植代码，就没有理由同时编写使用 `alloca()` 的代码。

# 3.2.5 地址空间检查

以下程序 `ch03-memaddr.c` 总结了我们看到的关于地址空间的所有内容。它做了一些在实践中你不应该做的事情，例如调用 `alloca()` 或直接使用 `brk()` 和 `sbrk()`：

```c
/*
 * ch03-memaddr.c  ---  显示代码、数据和栈部分，
 *                       以及 BSS 和动态内存的地址。
 */

#include <stdio.h>
#include <malloc.h>      /* 用于在 GLIBC 中定义 ptrdiff_t */
#include <unistd.h>
#include <alloca.h>      /* 仅用于演示 */

extern void afunc(void);  /* 用于展示栈增长的函数 */

int bss_var;             /* 自动初始化为 0，应在 BSS 中 */
int data_var = 42;       /* 初始化为非零值，应在数据段中 */

int
main(int argc, char **argv)  /* 参数未使用 */
{
    char *p, *b, *nb;

    printf("文本段位置:\n");
    printf("\tmain 的地址: %p\n", main);
    printf("\tafunc 的地址: %p\n", afunc);

    printf("栈位置:\n");
    afunc();

    p = (char *) alloca(32);
    if (p != NULL) {
        printf("\talloca() 数组的起始位置: %p\n", p);
        printf("\talloca() 数组的结束位置: %p\n", p + 31);
    }

    printf("数据段位置:\n");
    printf("\tdata_var 的地址: %p\n", &data_var);

    printf("BSS 位置:\n");
    printf("\tbss_var 的地址: %p\n", &bss_var);

    b = sbrk((ptrdiff_t) 32);   /* 增长地址空间 */
    nb = sbrk((ptrdiff_t) 0);
    printf("堆位置:\n");
    printf("\t堆的初始末尾: %p\n", b);
    printf("\t堆的新末尾: %p\n", nb);

    b = sbrk((ptrdiff_t) -16);   /* 缩减 */
    nb = sbrk((ptrdiff_t) 0);
    printf("\t堆的最终末尾: %p\n", nb);
}

void
afunc(void)
{
    static int level = 0;     /* 递归层级 */
    auto int stack_var;       /* 自动变量，位于栈上 */

    if (++level == 3)         /* 避免无限递归 */
        return;

    printf("\t栈层级 %d: stack_var 的地址: %p\n",
           level, &stack_var);   /* 递归调用 */
    afunc();
}
```

该程序打印了两个函数 `main()` 和 `afunc()` 的位置（第 22-23 行）。然后展示栈如何向下增长，让 `afunc()`（第 51-63 行）打印其局部变量 `stack_var` 的连续实例化地址。（`stack_var` 特意声明为 `auto`，以强调它位于栈上。）接着展示由 `alloca()` 分配的内存位置（第 28-32 行）。最后打印数据和 BSS 变量的位置（第 34-38 行），以及通过 `sbrk()` 直接分配的内存位置（第 40-48 行）。以下是该程序在 Intel GNU/Linux 系统上运行时的结果：

```text
$ ch03-memaddr
Text Locations:
    Address of main: 0x804838c
    Address of afunc: 0x80484a8
Stack Locations:
    Stack level 1: address of stack_var: 0xbffff864
    Stack level 2: address of stack_var: 0xbffff844
    Start of alloca()‘ed array: 0xbffff860
    End of alloca()‘ed array: 0xbffff870
Data Locations:
    Address of data_var: 0x80496b8
BSS Locations:
    Address of bss_var: 0x80497c4           BSS 位于数据变量之上
Heap Locations:
    Initial end of heap: 0x80497c8          堆位于 BSS 之上
    New end of heap: 0x80497e8             并且向上增长
    Final end of heap: 0x80497d8           地址空间可以缩减
```

# 3.3 总结

- 每个 Linux（以及 Unix）程序都有不同的内存区域。它们存储在可执行程序的磁盘文件的各个部分中。程序运行时会有一些段被加载到内存的同一部分。同一程序的所有运行副本共享可执行代码（文本段）。`size` 程序显示可重定位目标文件和完全链接的可执行文件中不同区域的大小。
- 运行中程序的地址空间可能存在空洞，并且随着内存的分配和释放，地址空间的大小会发生变化。在 modern 系统上，地址 0 不属于地址空间的一部分，因此不要尝试解除 NULL 指针的引用。
- 在 C 语言层面，使用 `malloc()`、`calloc()` 或 `realloc()` 之一来分配或重新分配内存。使用 `free()` 释放内存。（虽然 `realloc()` 可以做所有事情，但不建议那样使用它）。被释放的内存通常不会从地址空间中移除；相反，它会被复用用于后续的分配。
- 必须极度谨慎地做到以下几点：
  - 只释放来自分配例程的内存，
  - 只释放一次且仅释放一次此类内存，
  - 释放未使用的内存，并且
  - 不“泄露”任何动态分配的内存。
- POSIX 提供 `strdup()` 函数作为便利函数，而 GLIBC 提供 `getline()` 和 `getdelim()` 用于读取任意长度的行。

