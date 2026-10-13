

为整数 test 所占用的字节创建读写访问的监视点。

```c
#include <sys/types.h>
#include <sys/fcntl.h>
#include <sys/procfs.h>

typedef struct {
        long cmd;
        prwatch_t prwatch;
} ctl_t;

main(int argc, char **argv)
{
        int ctlfd;
        ctl_t ctl;
        int test;

        if ((ctlfd = open("/proc/self/ctl", O_WRONLY)) < 0) {
                perror("open /proc");
                exit (1);
        }

        ctl.cmd = PCWATCH;
        ctl.prwatch.pr_vaddr = (uintptr_t)&test;
        ctl.prwatch.pr_size = sizeof(int);
        ctl.prwatch.pr_wflags = WA_READ|WA_WRITE;

        if (write(ctlfd, &ctl, sizeof (ctl)) != sizeof (ctl)) {
                perror("Set PCWATCH");
                exit (1);
        }

        test = 0;
}
```

当我们试图写入整数 test 时，会触发一个监视点，默认情况下，进程会进行核心转储。

```text
$ ./watchpoint
Trace/Breakpoint Trap (coredump)
```

`/proc` 进程信息文件 `prinfo` 包含与监视点陷阱相关的信息，可以读入 `struct pr_info` 结构。特别是，`si_addr` 字段包含触发监视点的内存引用的虚拟地址，`si_code` 字段包含 `TRAP_RWATCH`、`TRAP_WWATCH` 或 `TRAP_XWATCH` 之一，分别表示读、写或执行访问。`si_trapafter` 字段为零，除非对该监视区域设置了 `WA_TRAPAFTER`；非零表示当前指令并非导致监视点陷阱的指令。`si_pc` 字段包含导致陷阱的指令的虚拟地址。图 5.16 展示了监视点的数据结构。

![](img/220ae4af07df2fe8e5be69d27f885d1b_208_0.png)

## 5.7 全局页面管理

页面是 Solaris 内存管理子系统中物理内存的基本单位。在本节中，我们讨论页面如何组织、如何定位，以及空闲列表如何在系统内管理页面池。

### 5.7.1 页面——Solaris 内存的基本单位

物理内存被划分为页面。Solaris 内核中的每一个活动（非空闲）页面都有一个文件（vnode）与内存之间的映射关系；该页面可以用一个 vnode 指针和该页面在该 vnode 中的偏移量来标识。页面的标识就是其 vnode/偏移对。vnode/偏移对是页面的后备存储，表示该页面所映射的文件和偏移量。

硬件地址转换（HAT）和地址空间层管理物理页面与其虚拟地址空间之间的映射（更多内容见第 190 页的“硬件地址转换层”）。vnode/偏移对的关键属性是复用性；也就是说，我们可以在页面被复用之前，通过简单地将其在 RAM 中的内容与其后备存储（vnode 和偏移量）同步，从而将每个物理页面用于另一项任务。

例如，我们可以通过简单地将内容复制到其 vnode 和偏移量来复用进程中的堆内存页面，在这种情况下，这会将内容复制到交换设备。同样的机制也用于缓存文件，我们只需使用 vnode/偏移对来引用正在缓存的文件。如果我们复用的是正在缓存常规文件的内存页面，那么我们只需将该页面与其后备存储同步（如果页面已被修改），或者直接复用它（如果页面未修改，且不需要与其后备存储重新同步）。

![](img/220ae4af07df2fe8e5be69d27f885d1b_209_0.png)

**图 5.17** *页面结构*

### 5.7.2 页面哈希列表

VM 系统将具有标识（有效的 vnode/偏移对）的页面哈希到全局哈希列表上，以便可以通过 vnode 和偏移量定位它们。有三个页面函数会搜索全局页面哈希列表：`page_find()`、`page_lookup()` 和 `page_lookup_nowait()`。这些函数以 vnode 和偏移量为参数，如果找到，则返回指向页面结构的指针。

全局哈希列表是一个指向页面链表的指针数组。这些函数使用哈希作为 `page_hash` 数组的索引，以定位包含具有匹配 vnode/偏移对的页面的链表。图 5.18 显示了 `page_find()` 函数如何索引到 `page_hash` 数组以定位匹配给定 vnode/偏移量的页面。

![](img/220ae4af07df2fe8e5be69d27f885d1b_210_0.png)

**图 5.18** *通过 vnode/偏移标识定位页面*

`page_find()` 按如下方式定位页面：

1. 它使用下面显示的 `PAGE_HASH_FUNC` 宏计算 `page_hash` 数组中的槽位，该槽位包含潜在页面列表。

```c
#define PAGE_HASHSZ        page_hashsz
#define PAGE_HASHHLEVEL    4
#define PAGE_HASHSHIFT     6
#define PAGE_HASH_FUNC(vp, off) \
        ((((unsigned long long) (off) >> PAGE_HASHSHIFT) + \
          ((unsigned long long) (vp) >> PAGE_HASHSHIFT)) & \
          (PAGE_HASHSZ - 1))
```

**头文件** `<vm/page.h>`

2. 它使用下面显示的 `PAGE_HASH_SEARCH` 宏，搜索该槽位引用的链表，以查找匹配 vnode/偏移量的页面。该宏遍历页面链表，直到找到这样的页面。

```c
#define PAGE_HASH_SEARCH(index, pp, vp, off) \
        for (pp = page_hash[index]; (pp) != NULL; (pp) = (pp)->p_hash) \
                if ((pp)->p_vnode == (vp) && (pp)->p_offset == (off)) \
                        break;
```

**头文件** `<vm/page.h>`

### 5.7.3 MMU 相关的页面结构

定义的页面结构在不同平台上相同，因此不包含任何机器相关的结构。然而，我们确实需要保存关于每个页面的机器相关数据，例如描述页面如何被 MMU 映射的 HAT 信息。内核用机器相关的页面结构 `struct machpage` 包装机器无关的页面结构。机器相关页面结构的内容对通用内核隐藏——只有 HAT 机器相关层可以看到或操作其内容。图 5.19 显示了每个页面结构如何嵌入到机器相关的 `struct machpage` 中。

![](img/220ae4af07df2fe8e5be69d27f885d1b_211_0.png)

**图 5.19** *机器相关的页面结构：sun4u 示例*

机器相关的页面包含一个指向 HAT 特定映射信息的指针，关于页面 HAT 状态的信息存储在机器相关的 machpage 中。存储的信息包括指示页面是否已被引用或修改的位，供页面扫描器使用（本章稍后介绍）。机器无关和机器相关的页面结构在内存中共享相同的起始地址，因此指向页面结构的指针可以强制转换为指向机器相关页面结构的指针（见图 5.19）。用于在机器无关页面和机器相关页面结构之间转换的宏完成了这种强制转换。

### 5.7.4 物理页面列表

Solaris 内核使用一个分段的全局物理页面列表，由连续的物理内存段组成。（许多硬件平台现在以非连续组的形式呈现内存。）连续的物理内存段在系统启动期间被添加。当系统运行期间物理内存被添加和移除时，它们也会被动态地添加和删除。图 5.20 显示了物理页面列表排列成连续段的情况。

![](img/220ae4af07df2fe8e5be69d27f885d1b_212_0.png)

**图 5.20** *连续的物理内存段*

#### 5.7.4.1 空闲列表和缓存列表

空闲列表和缓存列表保存那些未映射到任何地址空间且已由 `page_free()` 释放的页面。这些列表的总和在 `vmstat` 的 *free* 列中报告。即使 `vmstat` 将这些页面报告为空闲，它们仍然可能包含来自 vnode/偏移量的有效页面，因此仍然是全局页面缓存的一部分。在页面缓存中缓存文件的页面可能出现在空闲列表上。缓存列表上的页面并不是真正空闲的，它是来自文件的页面的有效缓存。缓存列表体现了文件系统如何将内存用作文件系统缓存。

空闲列表包含不再关联 vnode 和偏移量的页面——这种情况只有在页面已被销毁并从 vnode 的哈希列表中移除时才会发生。空闲列表通常非常小，因为大多数不再被进程或内核使用的页面仍然保留其完整的 vnode/偏移信息。当进程退出时，页面会被放到空闲列表上，此时所有匿名内存页面（堆、栈和写时复制页面）都会被释放。

缓存列表是一个页面的哈希列表，这些页面仍然具有到有效 vnode 和偏移量的映射。回想一下，页面可以通过

