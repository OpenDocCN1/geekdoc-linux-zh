
# Listing 14-34: 页表自省示例 [main]

## 14.6 内存可调参数 (Memory tunables)

有很多 VM 可调参数，位于 `/proc/sys/vm`，或者通过 `sysctl` 命令行通过 `vm.<tunable name>` 访问。关于此点的 procfs 文档非常详尽（sysctl 内核文档也是），我们将详细检查其中的一个核心子集：

- `admin_reserve_kbytes` - `sysctl_admin_reserve_kbytes` - 在 `OVERCOMMIT NEVER` 模式下，为管理员（即具有 `CAP_SYS_ADMIN` 权限的用户）保留的内存量。默认值为 8 MiB，且永远不会超过 8 MiB 和初始空页的 1/2，具体由 `init_admin_reserve()` 决定。这在 `_vm_memory()` 中检查，如果用户不具备系统管理权限，该值将从分配大小中减去。在其他 overcommit 模式下，此项无效。有关 overcommit 的更多细节请参见第 4.1 节。

- `user_reserve_kbytes` - 与 `sysctl_admin_reserve_kbytes` 参数类似，用于自定义 OVERCOMMIT NEVER 模式下的系统行为（有关内核中如何实现 overcommit 的详细检查请参见第 4.1 节）。此值指定了要保留的内存量，以防止任何用户导致系统停滞。该值在 `sysctl_user_reserve` 全局变量中指定，并在 `init_user_reserve()` 中初始设置，值为初始空页的 1/3 或 32 MiB 中的较者。

- `compact_memory`, `compact_victable_allowed`, `compact_proactiveness` - 前者在被写入时会触发 `sysctl_action_handler()` 函数，后两个参数的状态分别存储在 `sysctl_compact_victable_allowed` 和 `sysctl_proactiveness` 中。写入 `compact_memory` 会立即触发压缩，调用 `compact_nodes()` 压缩系统内所有节点的内存。`compact_victable_allowed` 参数决定是否可以压缩可驱逐内存，对于非实时内核，默认是允许的。`compact_proactiveness` 参数决定当压缩线程运行时，压缩内存的积极程度。该值以百分比表示，默认值为 20%。此值通过 `should_compact()` 影响压缩。如果设置为 0，则不会发生任何压缩。广义地说，该值越高，内核对页的压缩就越积极。当 `compact_proactiveness` 参数发生变化时，会调用 `compact_proactiveness_sysctl_handler()`，唤醒每个节点的压缩进程以应用更改。关于压缩整体的详细讨论请参见压缩章节。

- `dirty_background_bytes/dirty_background_ratio`, `dirty_bytes/dirty_ratio` – 这些值决定了回写（writeback）的行为（有关回写的详细讨论请参见第 ??），即修改数据何时返回磁盘。这些的字节和比例版本是互斥的——当设置其中一个，另一个会被清零。默认使用字节变体。这些参数的背景版本决定了每个节点后台回写何时开始写入磁盘。如果指定了字节，则该值是可以返回磁盘的脏数据字节数。如果指定了比例，该值表示为脏内存的百分比，即可变脏内存（在 `global_dirty_memory()` 中计算，包括现有文件页和空页）。非背景值决定了写入干净页时何时让进程进入睡眠直到回写成功完成。再次，关于后台和触发睡眠的回写算法的详细讨论请参见第 ??。脏页的数量等于 `global_node_page_state()` 中使用的 `NR_DIRTY` 统计值，即跨整个系统的 `/proc/zoneinfo` 中显示的 `nr dirty` 值，或者 `/proc/meminfo` 中显示的 `Dirty` 值。`dirty_background_bytes` 的状态存储在 `dirty_background_bytes` 全局值中，`dirty_background_ratio` 存储在 `dirty_background_ratio` 中，`dirty_bytes` 存储在 `vm_dirty_bytes` 中，`dirty_ratio` 存储在 `vm_dirty_ratio` 中。这些值每个在修改时分别由 `dirty_background_bytes_handler()`、`dirty_background_ratio_handler()`、`dirty_writeback_handler()` 和 `dirty_ratio_writeback_handler()` 函数处理。

- `dirty_expire_pages`, `page_refault_pages` – 这些值控制内存中页在内核尝试回收之前的寿命。这用于防止页的“抖动”。

- `vfs_cache_pressure` - 这控制内核回收内核缓存（inode 和 dentry 缓存）内存的倾向。值越大越倾向于回收 dentry/inodes 而不是页缓存。

- `swappiness` - 此参数调整内核交换匿名内存与回收页缓存之间的倾向。取值范围从 0 到 200，其中 0 表示尽可能避免交换，200 表示激进交换。

- `watermark_ratio` - 这控制在 kswapd 守护进程开始回收匿名页之前必须空闲的内存百分比。

> 内存管理器 (早期访问) © 2025 Lorenzo Stokes

- `mmap_min_addr` – 指定了进程中映射的最小地址。这很重要，因为如果允许在虚拟地址零进行分配，那么空指针处理将变得有问题。此值存储在 `mmap_min_addr` 中，但在 `dac_mmap_min_addr` 中进行保留。如果设置了 `CONFIG_LSM_MMAP_MIN_ADDR` 值，将为可以指定的值设置一个硬下限。更新在 `update_mmap_min_addr()` 中执行，由 `mmap_min_addr_handler()` 调用。

- `min_free_bytes` – 指定系统始终必须维持的最空空内存，用于计算区域水位线（zone watermarks）。这很重要，因为始终保持某些内存至关重要，否则内核或关键用户态可能无法运行，导致系统挂起或失效。默认值由 `calculate_free_bytes()` 决定，它尝试根据可用系统内存设置此值，计算为 $4\_j$，其中 $j$ 是超过每个区域高水位线的内存量（单位 KB）。在我的机器上，这产生了 67,584 KiB。每个区域的最小水位线通过将该值相对于每个区域管理的内存比例进行扩展来确定。这存储在 `min_free_bytes` 全局值中。

只有当用户拥有 `CAP_SYS_RAWIO` 权限时才允许更新。

- `oom_dump_tasks`, `oom_kill_allocating_task` - 如果 `oom_dump_tasks` 可调参数设置为非零值，则在调用内存杀手进程时转储所有任务；否则（这对于真正的大型系统有用）。默认值为 1。

- 如果指定了 `oom_kill_allocating_task`，则触发导致 OOM 杀手进程的任务，而不是被认为消耗内存最多的任务。

- 这通常不是一个好主意，因为触发 OOM 的任务往往不是导致问题的任务，而是一个无辜的旁观者。这默认值为 0。

- `overcommit_memory`, `overcommit_kbytes/overcommit_ratio` - 指定 `overcommit_memory` 中的过度提交策略——其中 0 表示 `OVERCOMMIT_GUESS`，1 表示 `OVERCOMMIT_ALWAYS`，2 表示 `OVERCOMMIT_NEVER`。在 GUESS 模式下，只要分配未超过安装的 RAM 和交换区的总和，就允许分配（切换 `MAP_NORESERVE` 会跳过此事件）。在 OVERCOMMIT_ALWAYS 模式下，没有任何检查，并允许任何有效范围的映射；在 OVERCOMMIT_NEVER 模式下，会跟踪已提交的内存并与限制进行比较。限制确定为交换区加上 `overcommit_bytes` 内存或所有安装 RAM 的 `overcommit_ratio`（以百分比表示，默认为 50%）。可以在 `/proc/meminfo` 的 `CommitLimit` 下观察该限制，总提交量记为 `Committed_AS`。关于过度提交的详细讨论，请参见第 4.1 节。这些值存储在全局变量 `sysctl_overcommit_memory`、`sysctl_overcommit_kbytes` 和 `sysctl_overcommit_ratio` 中。

- `page-cluster` - 确定一次从交换区检索的页数，以交换区内的连续页测量。实际值指定页顺序（page-order），即基础页数的 2 的幂，对于内存极小的机器，默认值为 3。该值存储在全局变量 `page_cluster` 中。

- `panic_on_oom` - 如果设置为 0，则 OOM 杀手执行其惯常工作，杀死最极端的内存大户（详情请参见它是如何做的）。如果设置为 1，则当系统内存耗尽时将触发恐慌（panic），或者在受内存策略或 cgroup 因素限制时照常进行（这两者超出本书讨论范围）。最后，如果设置为 2，Linux 在内存耗尽时将始终触发 panic。该值默认为 0。该值存储在全局变量 `sysctl_panic_on_oom` 中。

- `percpu_pagelist_high_fraction` - 这决定了每个区域中可以存储在每 CPU 页（Per-CPU-Pages，或 PCPs）中的页比例。PCP 是维护在每个 CPU 上的缓存，以避免释放和分配页时需要锁（有关此机制如何工作的更多细节请参见第 2.7.3 节）。该值本身指定每个区域页比例的分母，这将决定每个 PCP 的高值，即其中居住的最大页数。如果设置为 0（默认值），内核将根据区域的低水位（low watermark）和系统中的 CPU 数量启发式地确定此值。否则，如果指定了该值，则该值将将管理的页除以可调参数中的分母，并除以 CPU 数量。该值存储在全局变量 `percpu_pagelist_high_fraction` 中。PCP 高计数的计算在 `zone_highsize()` 中确定。当值改变时，会调用 `percpu_pagelist_high_fraction_sysctl_handler()` 函数，该函数执行合理检查并确保该值不会导致过度平衡。

- `stat_interval/stat_refresh` - VM 统计存储在每 CPU 缓存中，以避免更新节点和区域统计因需要锁而产生的影响。统计数据随后定期刷回全局状态。`stat_interval` 值指定此间隔，单位为秒。可以通过向 `stat_refresh` 写入值手动触发统计刷新。`stat_interval` 值存储在全局变量 `sysctl_stat_interval` 中，并转换为内核 jiffs（内核内部的时间度量）。调用手动统计刷新将触发 `vm_refresh()`。

- `swappiness` - 该值以一种更具启发式的方式表示在回收时将内存交换出磁盘与从页缓存中丢弃页的相对成本。取值范围从 0 到 200，值越小表示交换成本越高，值越大表示成本越低，100 表示两者的性能成本相等。这在真正意义上是可调的，因为需要通过经验确定一个值。默认设置为 60，明智地表明交换出/换入比丢弃页缓存的引用要贵得多。该值存储在全局变量 `vm_swappiness` 中。它被 `get_scan_count()` 在回收期间利用，以决定如何在两者之间做出选择。请参见回收章节，以详细检查其如何影响算法。

- `watermark_boost_factor`, `watermark_scale_factor` - 当页块（pageblocks）混合了不同的迁移类型（migrate types）时，可能会导致碎片化（迁移类型的详细说明请参见第 2.5 节）。为了抵消这种影响，当发生此类混合时，可以对区域的水水位应用一个提升因子（boost factor）。提升因子是区域高水位（high mark）的倍数，乘以 10000，默认值为 15（意味着默认是高水位的 1.5 倍）。`watermark_scale_factor` 决定每个区域内水位之间的距离，在 `setup_zone_watermarks()` 中确定，乘以 10000。默认值为 10，意味着可用内存的 0.1%。允许的最大值为 3000，即可用内存的 30%。`watermark_boost_factor` 可调参数存储在 `watermark_boost` 中，而 `watermark_scale_factor` 存储在 `scale_factor` 中。提升在 `boost_watermark()` 中应用。

- `reclaim_mode` - 此可调参数决定当区域低于分配所需的水位时是否尝试回收，而不是默认的直接尝试下一个区域。该可调参数还决定了在这种情况下如何回收。有趣的是，存储此值的全局变量是 `node_reclaim_mode`，可以设置为可组合标志：`RECLAIM_ZONE` (1) 在区域内存耗尽时回收，`RECLAIM_WRITE` (2) 在回收期间写出脏页，`RECLAIM_UNMAP` (4) 取消映射。此可调参数的交换页检查在 `get_page_from_freelist()` 中执行，由 `node_reclaim_enabled()` 决定是否启用了它。

## 查看一个简单的服务器/客户端架构

它仅仅建立了一个共享内存映射，且双方都对其写入权限：

### 列表 14-35：System V 共享内存服务器示例

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <unistd.h>

#define KEY (1234)
#define SIZE (4096)
#define NUM_LOOPS (10)

int main(void) {
    int i, shmid;
    char *shm;

    shmid = shmget(KEY, SIZE, IPC_CREAT | 0666);
    if (shmid < 0) {
        perror("shmget");
        return EXIT_FAILURE;
    }

    shm = shmat(shmid, NULL, 0);
    if (shm == (void *)-1) {
        perror("shmat");
        return EXIT_FAILURE;
    }

    memset(shm, 0, SIZE);

    for (i = 0; i < NUM_LOOPS; i++) {
        shm[i] = 'a' + i;
        printf("server: %s\n", shm);
        sleep(1);
    }

    return EXIT_SUCCESS;
}
```

使用 `shmget()` 建立键，指定 `IPC_CREAT` 表示该段应该被创建而非仅仅是访问。该区域的权限设置方式与 `chmod()` 指定的方式相同。

然后通过 `shmat()` 获取该区域的指针并将其附加到该区域，即将其映射到进程中。第二个参数指定所需的地址，这里在此使用 `NULL` 表示映射到何处并不重要，最后的标志位为 `none`，我们在这里不需要其中任何标志位。此时，我们已经创建了一个共享内存映射，可以通过客户端中指定相同的键来访问它：

### 列表 14-36：System V 共享内存客户端示例

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <unistd.h>

#define KEY (1234)
#define SIZE (4096)
#define NUM_LOOPS (10)

int main(void) {
    int i, shmid;
    char *shm;

    shmid = shmget(KEY, SIZE, 0666);
    if (shmid < 0) {
        perror("shmget");
        return EXIT_FAILURE;
    }

    shm = shmat(shmid, NULL, 0);
    if (shm == (void *) -1) {
        perror("shmat");
        return EXIT_FAILURE;
    }

    for (i = 0; i < NUM_LOOPS; i++) {
        shm[i] = 'a' + i;
        printf("client: %s\n", shm);
        sleep(1);
    }

    return EXIT_SUCCESS;
}
```
