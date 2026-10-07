

![](img/a86367b95bf21add858c99948ac951c_205_0.png)

# 图 5.13 匿名槽在页面换出前初始化为虚拟交换

只有当发生第一次页面换出请求时——因为页面扫描器必须想要将某个页面推送到交换区——才会分配真正的交换空间。此时，页面扫描器会查找该页面的 vnode 并调用其 `putpage()` 方法。该页面的 vnode 是一个 vnode，因此调用 `putpage()` 将此页面交换到交换设备中。`putpage()` 例程会分配一个与页面大小相等的物理交换块，然后设置匿名槽中的物理 vnode 偏移字段以指向交换设备。该页面被推送到交换设备。在此时，我们分配了交换空间。图 5.14 显示了页面被换出*之后*的匿名槽。

# 匿名内存

![](img/a86367b95bf21add858c99948ac951c_206_0.png)

图 5.14 页面换出后的物理交换

当我们耗尽交换空间时，简单地忽略对某个页面的 `putpage()` 请求，会导致难以分析的内存问题。当物理交换满时，不会发生错误；在预留期间，我们已经确保了足够的虚拟交换空间，其中包含了物理内存和交换空间。在这种情况下，`putpage()` 将页面留在内存中，而不将其推送到物理交换。由于这个原因，在 100% 交换分配的情况下运行（`swap -s` 显示为 0 空闲）通常是一个坏主意，因为我们可能开始锁定内存中错误的页面，而我们的工作集可能与我们想要留存在内存中的页面不匹配。

## 5.5.3 匿名计数

系统中的匿名内存数量由匿名计数结构记录。匿名层在下面的 `anon_info` 结构中跟踪匿名面的分配情况。

```c
struct anon_info {
    int ani_max;          /* 物理交换上可预留槽的总数 */
    int ani_free;         /* 未分配物理和内存槽的数量 */
    int ani_phys_res;     /* 已预留物理（磁盘）槽的数量 */
    int ani_mem_res;      /* 已预留内存槽的数量 */
    int ani_locked_swap;  /* 内存中锁定的交换槽数量 */
};
```

### 头文件 <sys/anon.h>

`anon_info` 结构记录了物理交换和内存上预留槽位的数量。这些信息用于填充 `swapctl` 系统调用的数据。`swapctl()` 为 `swap` 命令提供数据。交换系统调用使用了稍不同的数据结构，即下所示 `anoninfo` 结构。

```c
struct anoninfo {
    int ani_max;
    int ani_free;
    int ani_res;
};
```

### 头文件 <sys/anon.h>

`anoninfo` 结构以平台无关的方式导出交换分配信息。下面的 `swap` 命令输出总结了来自 `anoninfo` 结构的信息。

```bash
# swap -s
total: 108504k allocated + 13688k reserved = 122192k used, 114880k available
```

`swap -s` 的输出可能有点误导性，因为它混淆了交换定义的术语。输出实际上告诉我们，已经使用了 122,192 K字节的虚拟交换空间，108,504 K字节的交换空间分配给了已访问的页面，有 114,880 K字节是空闲的。这些信息反映了图 5.15 中的交换分配阶段。记住，我们在创建虚拟内存时会预留交换空间，当真实页面被分配到地址空间时，那部分交换空间会被分配。剩余的交换空间保持未使用。

![](img/a86367b95bf21add858c99948ac951c_208_0.png)

图 5.15 交换分配状态

你可以使用 MemTool 3.8.1 中的 `prtswap` 脚本（参见第 242 页的“MemTool: Unbundled Memory Tools”）来列出交换的状态并找出交换是从哪里分配的，如下所示。如果只需要交换分配摘要，请使用 `prtswap` 命令。

```bash
# prtswap -l
Swap Reservations:
Total Virtual Swap Configured:          767MB
RAM Swap Configured:                    255MB
Physical Swap Configured:               512MB

Virtual Swap Reserved Against:         513MB
RAM Swap Reserved Against:             1MB
Physical Swap Reserved Against:        512MB

Virtual Swap Unresv. & Avail. for Reservation:  253MB
Physical Swap Unresv. & Avail. for Reservations:  0MB
RAM Swap Unresv. & Avail. for Reservations:  253MB

Swap Allocations: (Reserved and Phys pages allocated)
Total Virtual Swap Configured:          767MB
Total Swap Allocated Against:          467MB

Physical Swap Utilization: (pages swapped out)
Swap Free (should not be zero):         232MB
```

# Solaris 内存架构

```bash
# swap -
Virtual Swap:
Total Virtual Swap Configured:          767MB
Virtual Swap Reserved Against:         513MB
Virtual Swap Unresv. & Avail. for Reservation:  253MB

Physical Swap Utilization: (pages swapped out)
Physical Swap Configured:               512MB
Physical Swap Reserved Against:        512MB
Physical Swap Unresv. & Avail. for Reservations:  0MB

RAM Swap Configured:                    255MB
RAM Swap Reserved Against:             1MB
RAM Swap Unresv. & Avail. for Reservations:  253MB
```

