
## 7. 常规启动顺序

常规启动顺序（例如调用 `/sbin/init`）是在根文件系统上执行的。

请注意，将 `initrd` 从 `/` 移动到 `/initrd` 并不涉及通过 `umount()` 调用将其卸载。因此，在此过程中，仍可能有进程在 `initrd` 上运行（或者仍可能有文件系统处于挂载状态，但请参见下文）。然而，如果 `/initrd` 不存在，只有当没有其他进程使用 `initrd` 时，才能将其卸载。如果无法卸载，它将保留在内存中。

还需注意的是，挂载在 `initrd` 下的文件系统仍然可访问，但其 `/proc/mounts` 条目将不再更新。此外，如果 `/initrd` 不存在，`initrd` 无法卸载，它会“消失”，并随之带走那些文件系统，从而阻止它们被正确重新挂载。因此，强烈建议在从 `initrd` 切换到“常规”根文件系统之前，一般性地卸载所有文件系统（当然，根文件系统除外，但包括 `/proc`）。要释放用于初始 RAM 磁盘的内存，必须在卸载 `/initrd` 后执行 `freeramdisk`（参见下文“资源”部分）。

### 启动时内核表的创建顺序

在启动时，内核必须创建并正确填充系统正常运作所需的所有表。它们几乎都在数据段中静态分配并在编译时初始化。位于数据结构中的 `task_struct`、`init_mm` 和 `pg_data_t` 数组包含了机器内存状态的所有信息。在先前的内核中（2.2.x 及更早版本），这些信息存储在内核全局变量中。如今，在使用集群 Linux 服务器中，这些变量是每节点（per node）的。

在 2.3.49 版本的 `/include/linux/mzone.h` 中，IA32（Intel x86）非 NUMA 机器的唯一节点被称为 `contig_page_data`。`contig_page_data->node_mem_map` 是 2.2.x 中的旧 `mem_map_t` 数组，其中包含所有 `struct page *`。`node_mem_map` 数组在启动时动态分配，一旦系统中页数的数量被确定即进行分配。

### 启动时的硬件识别

在 2.2.x 版本中，内核被用于回忆每个配置在内核中的子系统的初始化回调。然后，每个子系统针对配置在内核中的每个底层驱动程序调用设备初始化代码。此过程被称为*分层初始化*（hierarchical initialization），对于设备数量有限的简单系统运行良好。

在 2.3.x 中，硬件识别过程发生了相当大的变化。以前，为了添加某些内容，需要修改高层的 *init* 回调，例如：

```c
#ifdef CONFIG_MY_DRIVER
    init_my_driver();
#endif
```

这不再必要了，因为我们在一个特殊的 ELF 段中包含了指向 *init_my_driver()* 的指针，而高层会解析每个特殊文件（设备驱动程序）的 *init* 段，并回忆所有的 *init* 回调，而无需在底层驱动程序的 `.c` 文件之外编写代码。这简化了启动时的初始化。

值得注意的是，采用这种新的硬件识别策略或顺序后，设备驱动程序编译时的链接顺序变得重要起来，因为信息位于目标文件的 ELF 头中。因此，在某些特殊情况下，可能仍然需要显式调用初始化函数。然而，对于大多数情况，这是不必要的。在早期阶段（例如，在设置控制台或虚拟内存管理器时），动态内核结构是通过一个新的 *bootmem* 分配器分配的，该分配器可以返回大的物理连续内存块。在 2.2.x 中，我们过去使用一个指针来跟踪早期阶段手动分配的内存，但随着较新机器可以在内存中间分配表，因此需要一个分配器（*bootmem*），它也能感知启动过程早期阶段的内存空洞。*bootmem* 分配器还确保在可能的情况下返回非 DMA 内存。这样，我们就避免了用不需要在那里的内核结构浪费前 16MB 内存。

一旦虚拟内存管理器启动并初始化，且 *get_pages* 和 *get_free_pages* 从 *bootmem* 获取适当的指针，所有进一步的内存分配都由 VM 直接处理。

### 关机

所有繁重的工作都在用户空间完成。*halt -f* 只是通过 *SIGSTP* 通知 *init* 进程机器即将关机。然后，shutdown 执行 *sys_reboot(SYS_HALT)*，并在 IA32 计算机上稍后调用 *exit(2)*。事实上，如果你运行 `halt -f`，你的机器仍然可以正常运行；然而 `init` 将停止 fork 登录会话，因为它收到了来自 `halt` 进程的 SIGSTP。

关机时的通用代码会回忆一个称为 `machine_halt()` 的每架构函数。在 IA32 上，此函数是一个空操作（noop）。例如，在 Alpha 上，它会向所有 CPU 发送 IPI，使它们都调用 palcode HALT 函数，以便 SRM 稍后可以获取对它们的控制。

重启的工作方式基本上相同，但不是调用 `machine_halt`，而是回忆另一个函数（`machine_restart`）。在 IA32 上，它通过向所有 CPU 发送停止信号并在 SMP 中禁用 I/O-APIC，然后向 I/O 地址写入一个特殊值来重启。如果这还不够，我们向 CPU 的中断表描述符（ITD）加载一个虚假的中断表。然后我们调用 int3（软中断），这将导致三重故障；CPU 将重启机器。

也有内核参数选项，强制内核使用 BIOS 函数而不是上述技术进行重启。

### 数据结构—linux/reboot.h

```c
 1 #ifdef _LINUX_REBOOT_H_
 2 #define _LINUX_REBOOT_H_
 3
 4 /*
 5 * Magic values required to use _reboot() system call.
 6 */
 7
 8 #define LINUX_REBOOT_MAGIC1  0xfee1dead
 9 #define LINUX_REBOOT_MAGIC2  672274793
10 #define LINUX_REBOOT_MAGIC2A 85072278
11 #define LINUX_REBOOT_MAGIC2B 369367448
12
13
14 /*
15 * Commands accepted by the _reboot() system call.
16 *
17 * RESTART    Restart system using default command and mode.
18 * HALT       Stop OS and give system control to ROM monitor, if any.
19 * CAD_ON     Ctrl-Alt-Del sequence causes RESTART command.
20 * CAD_OFF    Ctrl-Alt-Del sequence sends SIGINT to init task.
21 * POWER_OFF  Stop OS and remove all power from system, if possible.
22 * RESTART2   Restart system using given command string.
23 */
24
25 #define LINUX_REBOOT_CMD_RESTART  0x01234567
26 #define LINUX_REBOOT_CMD_HALT     0xCDEF0123
27 #define LINUX_REBOOT_CMD_CAD_ON   0x89ABCDEF
28 #define LINUX_REBOOT_CMD_CAD_OFF  0x00000000
29 #define LINUX_REBOOT_CMD_POWER_OFF 0x4321FEDC
```

```c
30    #define LINUX_REBOOT_CMD_RESTART2      0x01B2C3D4
31
32
33    #ifdef KERNEL
34
35    #include <linux/notifier.h>
36
37    extern struct notifier_block *reboot_notifier_list;
38    extern int register_reboot_notifier (struct notifier_block *);
39    extern int unregister_reboot_notifier (struct notifier_block *);
40
41
42    /*
43     * Architecture-specific implementations of sys_reboot commands.
44     */
45
46    extern void machine_restart(char * cmd) ;
47    extern void machine_halt(void);
48    extern void machine_power_off(void);
49
50    #endif
51
52    #endif  /* _LINUX_REBOOT_H  */
```

### 数据结构—linux/mmzone.h

```c
1    #ifndef _LINUX_MMZONE_H
2    #define _LINUX_MMZONE_H
3
4    #ifdef KERNEL
5    #ifndef __ASSEMBLY__
6
7    #include <linux/config.h>
8    #include <linux/spinlock.h>
9    #include <linux/list.h>
10
11    /*
12     * Free memory management - zoned buddy allocator.
13     */
14
15    #define MAX_ORDER 10
16
17    typedef struct free_area_struct {
18       struct list_head free_list;
19       unsigned int * map;
20    } free_area_t;
21
22    struct pglist_data;
23
```

```c
typedef struct zone struct {
    /*
     * Commonly accessed fields:
     */
    spinlock_t lock;
    unsigned long offset;
    unsigned long free_pages;
    int low_on_memory;
    unsigned long pages_min, pages_low, pages_high;

    /*
     * free areas of different sizes
     */
    free_area_t free_area[MAX_ORDER];

    /*
     * rarely used fields:
     */
    char * name;
    unsigned long size;
    /* Discontig memory support fields.
     */
    struct pglist_data *zone_pgd;
    unsigned long zone_start_paddr;
    unsigned long zone_start_paddr;
    struct page * zone_mem_map;
} zone_t;

#define ZONE_DMA        0
#define ZONE_NORMAL     1
#define ZONE_HIGHMEM    2
#define MAX_NR_ZONES    3

/*
 * One allocation request operates on a zonelist. A zonelist
 * is a list of zones, the first one is the 'goal' of the
 * allocation, the other zones are fallback zones, in decreasing
 * priority.
 *
 * Right now a zonelist takes up less than a cacheline. We never
 * modify it apart from boot-up, and only a few indices are used,
 * so despite the zonelist table being relatively big, the cache
 * footprint of this construct is very small.
 */
typedef struct zonelist struct {
    zone_t * zones [MAX_NR_ZONES+1]; // NULL delimited
    int gfp_mask;
} zonelist_t;

#define NR_GFPINDEX     0x100

struct bootmem_data;
typedef struct pglist data {
```
