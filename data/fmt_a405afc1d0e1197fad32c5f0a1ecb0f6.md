
![](img/bc86631e65e541c1c58ec0ab72a978e0_334_1.png)

在 Linux 内核启动过程的 CPU/平台特定初始化阶段，内核设置特定平台的硬件和软件环境。这涉及初始化 CPU、内存管理、中断处理以及其他低层硬件细节。

内核入口点通常是一个汇编语言程序，位于特定架构的文件 `arch/kernel/head.S` 中。该程序执行几项重要任务，包括：

1. 启用 MMU（如果尚未启用）并设置内存管理单元，初始化页表并启用虚拟内存。
2. 执行缓存初始化，设置缓存控制器和缓存大小。
3. 通过清零 BSS 段来设置 BSS，BSS 是内核二进制文件中包含未初始化数据的段。
4. 设置堆栈以便调用第一个 C 语言程序，即 `init/main.c` 中的 `start_kernel()` 函数。

`start_kernel()` 是一个执行大量初始化任务的函数，直到它进入进程 ID 为 0 的空闲任务。这些任务包括：

1. 启动 CPU：初始化每个 CPU 数据结构，例如每个 CPU 的定时器和调度器。
2. 平台和 CPU 特定初始化：涉及识别处理器、识别板、分析传递给内核的命令行参数、识别内存磁盘、调用 `bootmem` 函数以及调用分页初始化函数。
3. 内存管理器初始化：涉及初始化内存管理器，设置页分配器和虚拟子系统。
4. 调度器初始化：涉及初始化调度器。
5. 中断初始化：涉及初始化中断控制器并注册中断处理程序。
6. 定时器初始化：涉及初始化系统定时器并维护时间。
7. 控制台初始化：涉及初始化控制台。
8. 剩余初始化：初始化系统的其他部分，如驱动程序、文件系统和网络。

![](img/bc86631e65e541c1c58ec0ab72a978e0_335_0.png)

总的来说，`init/main.c` 中的 `start_kernel()` 函数是 Linux 内核启动的关键组件，负责初始化内核子系统并启动系统服务。

### 内核的主函数

```c
start_kernel() {
    /* 激活第一个处理器 
    boot_cpu_init();
    setup_arch(command_line); /* 处理设备树 */
    page_tables_init();
    prctl_kernel(command_line);
    init_mm(); /* 设置页表并启动 */
    sched_init(); /* 虚拟内存 */
    init_timer(2, timekeeping_init);
    console_init(); /* 之前的所有时间 */
    rest_init();
    return 0;
    user_spaces
}
```

![](img/bc86631e65e541c1c58ec0ab72a978e0_337_0.png)

### `setup_arch()` 函数

`setup_arch()` 函数是一个特定于架构的函数，内核启动期间由 `start_kernel()` 函数调用。该函数定义在 `arch/` 目录下，负责执行内核执行之前所需的特定架构的初始化任务。

以下是 `setup_arch` 函数通常执行的某些任务：

- 初始化中断控制器。
- 初始化内存管理单元 (MMU)。
- 设置初始页表。
- 配置时钟和定时器设备。
- 设置虚拟文件系统 (VFS)。
- 如果架构使用了设备树，则初始化设备树。

`setup_arch()` 函数在 Linux 内核支持的每个架构中都实现在不同的文件中。例如，在 ARM 架构上，`setup_arch()` 函数定义在 `arch/arm/kernel/setup.c` 中。

总的来说，`setup_arch()` 函数是 Linux 内核启动过程的关键组件，负责执行内核开始执行之前所需的特定架构的初始化任务。

![](img/bc86631e65e541c1c58ec0ab72a978e0_337_1.png)

# 第 12 章：嵌入式 Linux 简介

此函数执行特定于平台和 CPU 的初始化，以便安全地调用其余的初始化工作。

它负责：

- 识别处理器。
- 识别主板。
- 分析传递给内核的命令行参数。
- 识别内存磁盘（ram disk）。
- 调用启动内存（bootmem）函数。
- 调用分页初始化函数。

![](img/bc86631e65e541c1c58ec0ab72a978e0_338_0.png)

![](img/bc86631e65e541c1c58ec0ab72a978e0_338_1.png)

```c
#include <linux/sched.h>
#include <linux/mm.h>
#include <linux/interrupt.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/module.h>
#include <linux/string.h>
#include <linux/delay.h>
#include <linux/version.h>
#include <linux/elf.h>
#include <linux/fs.h>
#include <linux/file.h>
#include <linux/capability.h>
#include <linux/slab.h>
#include <linux/page.h>
#include <linux/uapi.h>
#include <linux/uaccess.h>
#include <linux/gdt.h>
#include <linux/id.h>
#include <linux/task.h>
#include <linux/process.h>
#include <linux/signal.h>
#include <linux/timer.h>
#include <linux/hrtimer.h>
#include <linux/event.h>
#include <linux/workqueue.h>
#include <linux/worklist.h>
#include <linux/list.h>
#include <linux/spinlock.h>
#include <linux/atomic.h>
#include <linux/mutex.h>
#include <linux/semaphore.h>
#include <linux/rqueue.h>
#include <linux/completion.h>
#include <linux/wait.h>
#include <linux/vm_map.h>
#include <linux/mmap.h>
#include <linux/io.h>
#include <linux/procfs.h>
#include <linux/sysfs.h>
#include <linux/kdev.h>
#include <linux/pci.h>
#include <linux/dev.h>
#include <linux/platform.h>
#include <linux/bus.h>
#include <linux/usb.h>
#include <linux/video.h>
#include <linux/audio.h>
#include <linux/net.h>
#include <linux/if.h>
#include <linux/block.h>
#include <linux/gen.h>
#include <linux/random.h>
#include <linux/ext4.h>
#include <linux/b2fs.h>
#include <linux/xfs.h>
#include <linux/jfs.h>
#include <linux/crypt.h>
#include <linux/aes.h>
#include <linux/sha.h>
#include <linux/md5.h>
#include <linux/sha1.h>
#include <linux/zlib.h>
#include <linux/lz4.h>
#include <linux/lzma.h>
#include <linux/zstd.h>
#include <linux/xz.h>
#include <linux/bz2.h>
#include <linux/snappy.h>
#include <linux/btrfs.h>
#include <linux/trtrfs.h>
#include <linux/f2fs.h>
#include <linux/ext3.h>
#include <linux/ext2.h>
#include <linux/ext1.h>
```

![](img/bc86631e65e541c1c58ec0ab72a978e0_338_2.png)
