
## `buffer_init` 函数

在 `buffer_init` 函数中，从内核端和缓冲区区域终端同时向相反方向生长以产生 `buffer_head`、缓冲区块，直到 `buffer_head` 和缓冲区块的配对少于一对。在第二章中，内存起始处设置了约 3000 对 `buffer_head`，`buffer_head` 在低地址，缓冲区块在高位地址（图 2.23）。

设置设备头成员：设备头、缓冲区块的配对。

设置 `buffer_head` 成员：
直到 `buffer_head` 和缓冲区块的配对少于一对。

## 2.11 初始化硬盘

图 2.26 显示了初始化过程。

![](img/f661d64b7eb54840fcb4d65765a4e933_93_0.png)

图 2.26 初始化硬盘。

![](img/f661d64b7eb54840fcb4d65765a4e933_93_1.png)

代码如下：

```c
// 代码路径: init/main.c

void main(void)
{
    hd_init();
}
```

```c
// 代码路径: kernel/blk_dev/hd.c: 与 rd_init 类似，参见 rd_init 的注释

void hd_init(void)
{
    blk_dev[MAJOR_NR].request_fn = DEVICE_REQUEST; // 链接 do_hd_request
    set_int_prq(0x2E, hd_interrupt); // 设置硬盘中断
    outb(0x20, 0x61); // 允许 PIO 硬盘发送中断请求
    outb(0x64, 0xA1); // 允许硬盘发送中断请求
}
```

## 2.12 初始化软盘

软盘和软盘驱动器是分离的。在书中，为了方便起见，“软盘”代表软盘驱动器和软盘整体。

软盘的初始化与硬盘初始化类似。区别在于链接函数 `do_fd_request()`，它初始化了与软盘相关的中断。详见第 2.1 节。

代码如下：

```c
// 代码路径: init/main.c:

void main(void)
{
    floppy_init(); // 与 hd_init() 类似
}
```

```c
// 代码路径: kernel/floppy.c:

void init(void)
{
    blk_dev[MAJOR_NR].request_fn = DEVICE_REQUEST; // 链接 do_fd_request()
    set_trap_gate(0x26, &floppy_interrupt); // 设置软盘中断
    outb(in_p(0x21) & 0x00, 0x21); // 允许软盘发送中断
}
```

图 2.27 给出了初始化软盘的主要步骤。

![](img/f661d64b7eb54840fcb4d65765a4e933_95_0.png)

图 2.27 初始化软盘。

## 2.13 开启中断

现在，所有的中断服务程序和 IDT（中断描述表）都已链接；这意味着中断服务系统已经完成。系统可以在 32 位保护模式下处理中断。重要的是，这意味着可以使用系统调用了。

现在我们可以开启中断！

代码如下：

```c
// 代码路径: include/asm/system.h:

#define sti() asm("sti"::)
```

```c
// 代码路径: init/main.c:

void main(void)
{
    sti();
    ....
}
```

## 2.14 进程 0 从特权级 0 移动到 3 并成为真实进程

Linux 要求所有进程都由特权级 3 的现有进程创建，进程 0 除外。在 Linux 0.11 中，进程 0 的代码和数据写在系统的内核中。它处于特权级 0；此时严格来说，进程 0 并不是一个真实的进程。为了符合规则，在进程 0 创建进程 1 之前，必须将进程从特权级 0 移动到 3。具体方法是调用函数 `move_to_user_mode()`，模仿中断返回的方法，将进程的特权级从 0 移动到 3。

图 2.28 给出了开启中断后的效果。注意 EFlags 的变化。

![](img/f661d64b7eb54840fcb4d65765a4e933_96_0.png)

### 开启中断前后 EFLAGS 对比

| 位 | 30 | 29 | 28 | 27 | 26 | 25 | 24 | 23 | 22 | 21 | 20 | 19 | 18 | 17 | 16 | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **开启中断前** | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | I | I | Y | A | V | R | N | O | O | D | I | T | S | Z | 0 | F | P | C | F |   |   |
| **开启中断后** | 30 | 29 | 28 | 27 | 26 | 25 | 24 | 23 | 22 | 21 | 20 | 19 | 18 | 17 | 16 | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |

> **注**：原文表格数据行似乎重复或有误，此处保留结构并标注前后状态。

# 第 3 章 进程 1 的创建与执行

## 3.1 进程 1 的创建

现在，进程 0 处于特权级 3，这是一个进程状态。作为父进程，它的首要任务是调用 `fork()` 创建第一个子进程——进程 1，这是父子进程创建机制的首次实现。在此机制的基础上，后续所有的进程都由父进程创建。

### 3.1.1 创建进程 1 的准备

在 Linux 中，任何新进程都是通过调用 `fork()` 创建的。该过程如图 3.1 所示。

```c
// code path: init/main.c:

....

static inline _syscall10(int, fork) // 对应 fork
static inline _syscall10(int, pause)
static inline _syscall11(int, setup, void *, BIOS)

void main(void)
{
    sti();
    move_to_user_mode();

    if (!fork()) {
        /* 我们指望此这里能够正常运行 */
        init();
    }

    /*
     * 注意！！对于任何其他任务，'pause()' 意味着我们必须接收
     * 一个信号来唤醒（参见 'schedule()'），
     * 因为 task0 在每个空闲时刻（当没有其他任务
     * 可以运行时）都会被激活。对于 task0，'pause()' 仅仅意味着检查是否有其他
     * 任务可以运行，如果我们不返回这里。
     */

    for(;;) pause();
}
```

`main.c` 中的 `fork()` 表明执行实际上被转移到了 `unistd.h` 中的 `syscall` 宏。代码如下：

```c
// code path: include/unistd.h

#define NR_setup 0      /* 供 init 使用，用于启动系统 */
#define NR_exit   1
#define NR_fork   2
#define NR_read   3
#define NR_write  4
#define NR_getopt 5
#define NR_close  6

#define _syscall(type, name) \
    type name (void) { \
    long volatile *res; \
```
