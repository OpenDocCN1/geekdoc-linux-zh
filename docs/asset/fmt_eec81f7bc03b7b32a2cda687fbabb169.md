
root@imx6qsabsred:~# `/sys/bus/platform/drivers/intkey# echo 0 > led` /* 关闭 led */

root@imx6qsabsred:~# `/sys/bus/platform/drivers/intkey# echo 1 > led` /* 开启 led */

root@imx6qsabsred:~# `ls /sys/class/gpio` /* 检查 gpio2 和 gpio5 文件是否已创建 */

```
root@imx6qsabsred:~# /sys/class/gpio/ ls /sys/class/gpio/
export gpio28 gpio9 gptchip128 gptchip192 gptchip32 gptchip96
gpio2 gpio5 gptchip0 gptchip160 gptchip250 gptchip64 export the led
root@imx6qsabsred:~# echo 0 > /sys/class/gpio/gpio2/value /* 关闭 led */
root@imx6qsabsred:~# echo 1 > /sys/class/gpio/gpio2/value /* 开启 led */
root@imx6qsabsred:~# rmmod led_sysfs_key_platform.ko /* 移除模块 */
root@imx6qsabsred:~# ls /sys/class/gpio /* 检查 gpio2 和 gpio5 文件是否已移除 */
```

root@imx6qsabsred:~# `ls /sys/class/gpio/`

export gpio9 gptchip128 gptchip192 gptchip32 gptchip96

gpio200 gptchip0 gptchip160 gptchip250 gptchip64 export

“多次按下 SW 按钮。切换按钮”

# 第 7 章 内存管理

Linux 是虚拟内存系统，这意味着用户程序看到的地址并不直接对应硬件使用的物理地址。内核和用户进程使用虚拟地址，地址转换在硬件 MMU（内存管理单元）中完成。有了虚拟内存，运行在系统上的程序可以分配比物理可用得多的内存；事实上，单个进程的地址空间可以比物理内存大。

当程序在计算机上实例化时，操作系统将可执行文件移动到内存中，处理器开始执行。这些指令可能用于准备程序的初始环境，内存可能包含非活跃代码。程序执行期间活跃部分的观察为内存系统的基础，而非活跃部分被移动到辅助存储（例如 Nand Flash、eMMC、RAM DDR2、 DDR3）。

以下是 Linux 中使用的地址类型：

- 1. 用户虚拟地址：用户程序看到的普通地址。地址长度为32 位或 64 位，取决于底层架构，每个进程都有自己的虚拟空间。虚拟地址空间被分为：低部用于用户空间，高部用于内核。在 32 位处理器上，分界在 `0xC0000000`。

- 2. 物理地址：处理器与系统内存之间的地址。物理地址为 32 位或 64 位；某些情况下，32 位系统可以使用更大的物理地址。

- 3. 总线地址：外设总线与内存之间的地址。通常与处理器使用的物理地址相同，但不一定。某些架构可以提供 I/O 管理单元 IOMMU，用于重映射总线与主内存之间的地址。在设置 DMA 操作时，必须额外编程 IOMMU。NXP iMX6 处理器不使用 IOMMU。

- 4. 内核逻辑地址：构成内核的正常地址空间。这些是 `CONFIG_PAGE_OFFSET` 之虚拟地址。在大多数架构上，逻辑地址与其相关的物理地址仅差一个常量偏移，这使得物理地址和虚拟地址之间的转换变得简单。`kmalloc()` 函数返回指向连续物理页的内核逻辑地址指针。内核逻辑内存空间不能被交换。可以使用宏 `__pa(x)` 和 `__va(x)` 在物理地址和逻辑地址之间转换。

- 5. 内核虚拟地址：内核虚拟地址与逻辑地址相似，它们都是从内核空间到物理地址的映射。然而，内核虚拟地址并不具有逻辑空间所特征的到物理地址的一对一线性映射。所有的逻辑地址都是内核虚拟地址，但许多内核虚拟地址并不是逻辑地址。例如，`vmalloc()` 函数将返回一个虚拟内存块，但内存仅在虚拟空间连续，在物理空间可能不连续。`vmap()` 返回的内存也会动态放置在该区域。机器特定的静态映射也通过 `early_init()` 位于此处。

## 用户进程虚拟到物理内存映射

在 Linux 中，内核空间无处不在并在所有进程中映射相同的物理内存。内核代码和数据始终可访问，随时准备处理中断或系统调用。相比之下，每当发生进程切换时，地址空间用户模式部分的映射就会改变。

每个用户空间进程都有自己的虚拟内存布局，包含四个逻辑区域：

- 1. 代码段（Text segment）：程序代码，存储进程的二进制镜像（`/bin/app`）。

- 2. 数据段（data+bss+heap）：在程序启动或运行期间创建并初始化的各种数据结构（例如堆）。堆提供运行时内存分配，类似于栈，但与栈不同的是，它用于必须存活于执行分配的函数的数据。在 C 语言中，堆分配的主要接口是 `malloc()` 函数。数据段存储静态初始化变量，BSS 段存储全零的未初始化静态变量。

- 3. 内存映射段（Memory mapping segment）：内核在此将文件内容直接映射到内存。任何应用程序都可以通过 Linux `mmap()` 系统调用请求此类映射（例如动态库 `/lib/libc.so`）。也可以创建一个不对应任何文件的匿名内存映射，用于程序数据。在 Linux 中，如果你通过 `malloc()` 请求大块内存，C 库将创建此类匿名映射而不是使用堆内存。

- 4. 栈段（Stack segment）：位于进程可用区域的尾部并向下生长：在大多数编程语言中存储局部变量和函数参数。调用方法或函数会在栈上推入新帧。函数返回时，栈帧被销毁。

## 内核虚拟到物理内存映射

内核虚拟地址空间从 `0xc000000` 开始。你可以进入内核配置设置（Kernel config），允许内核访问更多的物理内存：

![](img/739a35b59067f8a55eff80a58765146f_278_0.png)

内核虚拟地址空间在启动期间打印在内核消息缓冲区中：

```
Virtual kernel memory layout:
vector : 0xfffff000 - 0xfffffff0 ( 4 KB)
fixmap : 0xffff0000 - 0xfffe0000 ( 896 KB)
vmalloc : 0xc0000000 - 0xff000000 (1000 MB)
lowmem : 0x80000000 - 0xc0000000 (1024 MB)
pkmap : 0x87fe0000 - 0x80000000 ( 2 MB)
modules : 0x87ff0000 - 0x87fe0000 ( 14 MB)
  .text : 0x80d20000 - 0x80d1fccd (13408 KB)
  .init : 0x80d20000 - 0x80d2c2c0 ( 329 KB)
  .data : 0x80d74000 - 0x80dd5280 ( 389 KB)
  .bss  : 0x80d5d280 - 0x80e4061c ( 429 KB)
```

你可以将内核物理分为分为区域：

- 1. **ZONE_DMA** - 映射到内核虚拟地址空间（HIGHMEM）。在 ARM® 32 位 CPU 中，映射到内核虚拟地址的范围从 `ffc00000` 到 `ffffffff`。映射的虚拟 DMA 内存区域由 `dma_alloc_xxx` 函数返回。

- 2. ZONE_NORMAL 映射到内核逻辑地址空间（LOWMEM）。内核内核用于内部数据结构以及其他系统和用户空间分配。

- 3. ZONE_HIGHMEM 映射到内核虚拟地址空间（HIGHMEM）。专门用于系统分配（文件系统缓冲区、用户空间分配等）。映射到由 `vmalloc` 函数返回的内核虚拟地址。

- 4. 内存映射 I/O（Memory-Mapped I/O）映射到内核虚拟地址空间（HIGHMEM）。通过 `ioremap()` 返回的内存也将动态地放置在此内核虚拟区域中。

在下面的图中你可以看到内核内存映射布局：

虚拟地址空间

![](img/739a35b59067f8a55eff80a58765146f_279_0.png)

## MMU 管理

NXP i.MX6 Cortex-A9 处理器使用虚拟地址运行。内存管理单元（MMU）将代码和数据的地址从内存的虚拟视图转换为真实系统中的物理地址。

几乎所有的虚拟内存实现都会将虚拟地址空间划分为连续的虚拟地址块，称为页（pages）。为了将进程的虚拟地址转换为硬件实际处理指令时使用的物理地址，MMU 利用了页表（page tables）。页表包含一系列条目，每个条目描述了内存映射的物理地址翻译。页表项按虚拟地址组织。除了描述该虚拟页到物理页的翻译外，它们还提供了该页的访问权限和内存属性。
