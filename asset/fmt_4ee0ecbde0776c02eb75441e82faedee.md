
图 18-20：`read_swap_cache_async` 的代码流程图。

如果未找到页面，则必须调用 `alloc_vma`（在 NUMA 系统上最终归结为 `alloc_page`）来分配一个空闲内存页，以存储来自交换区域的数据。通过 `alloc_pages` 发出的内存请求具有高优先级。例如，如果没有空闲空间，内核会尝试交换出其他页面以提供空闲内存。该函数的失败（由 `NULL` 指针指示）代价高昂，并会导致换入（swap-in）立即终止。在这种情况下，高层代码会指示 OOM 内核杀死系统中具有较多内存页且不重要的进程，以获取空闲内存。

如果页面被成功回收（这种情况很少发生，因为很少有用户能无意中将系统加载到 OOM 内核会失败的程度），内核使用 `add_to_swap_cache` 将页面添加到交换缓存中，并使用 `lru_cache_add_active` 将其添加到 LRU 缓存（活动页面）。然后，通过 `swap_readpage` 将页面数据从交换区域传输到 RAM 内存。

`swap_readpage` 在满足必要的先决条件后启动从磁盘到 RAM 内存的数据传输。它通过两个短步骤完成：`get_swap_bio` 向块设备层生成适当 BIO 请求，`submit_bio` 发送该请求。

有两点需要特别注意：

- `add_page_to_swap_cache` 会自动锁定页面。
- `swap_readpage` 指示块层在页面完全读取后调用 `end_swap_bio_read`。如果执行顺利，这会设置 `PG_update` 标记并解锁页面。这很重要，因为读取操作是异步的。然而，内核必须确保在页面被标记为最新并解锁时，该页面已填充了所需的数据。

### 18.8.3 交换预读 (Swap Readahead)

与读取文件一样，内核也使用重读机制从交换区域读取数据。这确保了预读数据，以便未来的页入（page-in）请求能够快速满足，从而提高系统性能。与相当复杂的读取预读方法相比，交换系统的相应机制相对简单，如下代码所示：

```c
### mm/memory.c

void swapin_readahead(swp_entry_t entry, unsigned long addr, struct vm_area_struct *vma)
{
    int i, num;
    struct page *new_page;
    unsigned long offset;
    /*
     * 获取我们应该进行预读的句数量。
     */
    num = valid_swandles(entry, offset);
    for (i = 0; i < num; offset++, i++) {
        /* 现在执行异步读取 - */
        new_page = read_swp_cache_async(swp_entry(entry), offset, vma, addr);
        if (!new_page) {
            break;
        }
        page_cache_release(new_page);
        lru_add_drain(); /* 现在将任何新页面推送到 LRU */
    }
}
```

内核调用 `valid_swandles` 来计算预读页面的数量。通常读取 `2page_cluster` 个页面，其中 `page_cluster` 是一个全局变量，对于内存小于 16 MB 的系统设置为 2，对于其他系统设置为 3。这提供了一个四个或八个页面的预读窗口（`/proc/sys/vm/page-cluster` 允许从用户空间调整该变量，并通过设置为 0 来禁用交换预读）。然而，在以下情况下，必须减少 `valid_swandles` 计算出的值：

- 如果请求的页面接近交换区域的末尾，则必须减少预读页数，以防止读取到边界之外。
- 如果预读包含空闲或未使用的页面，内核只读取*这些页面之前*的有效数据。

`read_swp_cache_async` 连续向块设备层提交所选页面的读取请求。如果该函数因为没有分配内存页而返回 `NULL` 指针，内核将进行交换出，因为没有可用内存供后续页面使用，因此预读机制不如系统中盛行的内存存储重要。

### 18.9 启动内存回收

在本章开头的概述中，我演示了页面选择和交换出程序受更深层的控制，该层决定*何时*以及回收*多少*页面。这一决策被回溯到两个地方——首先是 `kswapd` 守护进程，它在没有内存密集型应用运行时尝试维持系统中的最佳内存平衡；另一个是当内核认为内存几乎完全耗尽时触发的紧急机制。

### 18.9.1 使用 kswapd 进行周期性回收

`kswapd` 是一个内核守护进程，每次系统启动时都会由 `kswapd_init` 激活，并在机器运行期间一直执行：

```c
mm/vmscan.c

int kswapd_run(int nid)
{
    pg_data_t *pgdat = NODE_DATA(nid);
    int ret = 0;
    pgdat->kswapd = kthread_run(kswapd, pgdat, "kswapd%d", nid);
    return ret;
}

static int __init kswapd_init(void)
{
    pg_data_t *pgdat;
    swap_setup();
    for_each_node(nid, HIGH_MEMORY)
        kswapd_run(nid);
    return 0;
}
```

代码显示，每个 NUMA 区域都会激活一个单独的 `kswapd` 实例。在某些机器上，这有助于增强系统性能。非 NUMA 系统只使用一个 `kswapd`。

有趣的是在 `mm/vmscan.c` 中实现的 `kswapd` 守护进程的执行：

```c
mm/vmscan.c

static int kswapd(void *p)
{
    unsigned long order;
    pg_data_t *pgdat = (pg_data_t*)p;
    struct task_struct *tsk = current;
    DEFINE_WAIT(wait);
    current->reclaim_state = &reclaim_state;
    tsk->flags |= PF_MEMALLOC | PF_SWAP | PF_KSAPD;
    order = 0;
    for ( ) {
        unsigned long new_order;
        prepare_to_wait(&pgdat->kswapd, &wait, TASK_INTERIBLE);
        new_order = pgdat->kswapd_max_order;
        pgdat->kswapd_max_order = 0;
        if (order < new_order) {
            /* 如果有人想要更大的分配，不要睡眠 */
            order = new_order;
        } else {
            schedule();
            order = pgdat->kswapd_max_order;
            finish_wait(&pgdat->kswapd, &wait);
            balance_pgdat(pgdat, 0, order);
            return 0;
        }
    }
}
```
