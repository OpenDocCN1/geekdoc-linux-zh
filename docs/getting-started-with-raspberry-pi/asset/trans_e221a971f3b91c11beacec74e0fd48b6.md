

## 进程文件系统

进程文件系统（procfs）是一个虚拟文件系统，它为内核的内部结构提供了访问窗口。当你浏览 procfs 时看到的数据是由内核动态生成的。procfs 中的文件用于配置内核参数、查看内核结构、从设备驱动程序中获取统计数据，以及获取通用系统信息。

Procfs 是一个伪文件系统。这意味着驻留在 procfs 中的文件不与诸如硬盘等物理存储设备关联。相反，这些文件中的数据是由内核中对应的入口点按需动态创建的。因此，procfs 中的文件大小显示为零。在内核启动期间，Procfs 通常挂载在 /proc 目录下；你可以通过调用 mount 命令来查看这一点。

为了初步了解 procfs 的功能，请检查 /proc/cpuinfo、/proc/meminfo、/proc/interrupts、/proc/tty/driver/serial、/proc/bus/usb/devices 和 /proc/stat 的内容。某些内核参数可以通过写入 /proc/sys/ 下的文件在运行时进行修改。例如，你可以将一组新值回显到 /proc/sys/kernel/printk 来更改内核 printk 日志级别。许多实用工具（如 ps）和系统性能监控工具（如 systat）内部都是从驻留在 /proc 下的文件中获取信息的。

序列文件（Seq files）是在 2.6 内核中引入的，它们简化了大型 procfs 操作。它们在第 C 章“序列文件”中有详细描述。

## 内存分配

一些设备驱动程序必须意识到*内存区域*的存在。此外，许多驱动程序还需要内存分配函数的服务。在本节中，我们将简要讨论这两者。

内核将物理内存组织成*页*。页大小取决于架构。在基于 x86 的机器上，它是 4096 字节。物理内存中的每个页都关联有一个 struct page（定义在 include/linux/mm_types.h 中）：

```
struct page {
    unsigned long flags;     /* Page status */
    atomic_t _count;        /* Reference count */
    /* ... */
    void * virtual;         /* Explained later on */
};
```

在 32 位 x86 系统上，默认的内核配置将可用的 4GB 地址空间划分为用于用户进程的 3GB 虚拟内存空间和用于内核的 1GB 空间，如 图 2.5 所示。这给内核可处理的物理内存量施加了 1GB 的限制。实际上，限制是 896MB，因为地址空间的 128MB 被内核数据结构占用。你可以通过在内核配置期间更改 3GB/1GB 的分割来增加这个限制，但如果你减少用户进程的虚拟地址空间，将会引起对内存密集型应用程序的不满。

![](img/07cc6f9c8c74622020874f66bfb53dc4_59_0.png)

映射低 896MB 的内核地址与物理地址相差一个常量偏移量，被称为*逻辑地址*。借助“高内存”支持，内核可以通过使用特殊映射为那些区域生成*虚拟地址*来访问 896MB 以外的内存。所有逻辑地址都是内核虚拟地址，但反之并不成立。

这导致我们得到以下内核内存区域：

1. `ZONE_DMA` (<16MB)，用于*直接内存访问*（DMA）的区域。由于传统 ISA 设备具有 24 位地址线且只能访问前 16MB，内核试图将此区域专门分配给此类设备。
2. `ZONE_NORMAL`（16MB 到 896MB），通常可寻址的区域，也称为低内存。低内存页的 `struct page` 中的 "virtual" 字段包含对应的逻辑地址。
3. `ZONE_HIGH` (>896MB)，内核只有在将驻留页映射到 `ZONE_NORMAL` 中的区域（使用 `kmap()` 和 `kunmap()`）后才能访问的空间。对应的内核地址是虚拟地址而不是逻辑地址。如果页未被 kmapped，高内存页的 `struct page` 中的 "virtual" 字段指向 `NULL`。

`kmalloc()` 是一个内存分配函数，它从 `ZONE_NORMAL` 返回连续内存。原型如下：

```c
void *kmalloc(int count, int flags);
```

其中 `count` 是要分配的字节数，`flags` 是模式指定符。所有支持的标志都列在 *include/linux/gfp.h* 中（gfp 代表 *get free pages*），但以下是常用的标志：

1. `GFP_KERNEL` 由进程上下文代码使用以分配内存。如果指定了此标志，`kmalloc()` 被允许进入睡眠状态并等待页面释放。
2. `GFP_ATOMIC` 由中断上下文代码使用以获取内存。在此模式下，`kmalloc()` 不被允许睡眠等待空闲页面，因此使用 `GFP_ATOMIC` 成功分配内存的概率低于使用 `GFP_KERNEL`。

由于 `kmalloc()` 返回的内存保留其前一次使用的内存内容，如果暴露给用户空间可能存在安全风险。要获取清零的 kmalloced 内存，请使用 `kzalloc()`。

如果你需要分配大型内存缓冲区，并且不要求内存物理连续，请使用 `vmalloc()` 而不是 `kmalloc()`：

```c
void *vmalloc(unsigned long count);
```

这里 `count` 是请求的分配大小。该函数返回内核虚拟地址。

`vmalloc()` 比 `kmalloc()` 享有更大的分配大小限制，但速度较慢，且不能从中断上下文调用。此外，你不能使用 `vmalloc()` 返回的物理不连续内存来执行*直接内存访问*（DMA）。高性能网络驱动程序通常在设备打开时使用 `vmalloc()` 来分配大型描述符环。

内核提供了更复杂的内存分配技术。这些包括*旁路缓冲区*、*slabs* 和*内存池*，超出了本章的范围。

### 查看源代码

内核启动以执行位于 `arch/x86/boot/` 目录下的实模式汇编代码开始。查看 `arch/x86/kernel/setup_32.c` 以了解保护模式内核如何获取实模式内核获得的信息。

第一条启动消息由驻留在 `init/main.c` 中的代码打印。深入了解 `init/calibrate.c` 以了解 BogoMIPS 校准，并查看 `include/asm-your-arch/bugs.h` 以洞察架构相关的检查。

内核中的定时器服务包括位于 `arch/your-arch/kernel/` 中的架构相关部分和实现在 `kernel/timer.c` 中的通用部分。对于相关定义，请查看头文件 `include/linux/time*.h`。

`jiffies` 定义在 `linux/jiffies.h` 中。`HZ` 的值取决于处理器，可以在 `include/asm-your-arch/param.h` 中找到。

内存管理源位于顶层的 `mm/` 目录中。

**表 2.1** 总结了本章中使用的主要数据结构及其在源代码树中定义的位置。**表 2.2** 列出了本章中使用的主要内核编程接口及其定义的位置。

### 表 2.1. 数据结构摘要

| 数据结构 | 位置 | 描述 |
| :--- | :--- | :--- |
| HZ | `include/asm-your-arch/param.h` | 系统定时器每秒滴答的次数 |
| loops_per_jiffy | `init/main.c` | 处理器在 1 个 jiffy 内执行内部延迟循环的次数 |
| timer_list | `include/linux/timer.h` | 用于保存你希望在未来某个时间点执行的例程的地址 |
| timeval | `include/linux/time.h` | 时间戳 |
| spinlock_t | `include/linux/spinlock_types.h` | 一种自旋锁定机制，以确保只有一个线程进入临界区 |
| semaphore | `include/asm-your-arch/semaphore.h` | 一种睡眠锁定机制，允许预定数量的用户进入临界区 |
| mutex | `include/linux/mutex.h` | 替代 `semaphore` 的新接口 |
| rwlock_t | `include/linux/spinlock_types.h` | 读者-写者自旋锁 |
| page | `include/linux/mm_types.h` | 内核对物理内存页的表示 |

### 表 2.2. 内核编程接口摘要

