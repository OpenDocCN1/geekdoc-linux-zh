
- 仅使用来自最高区域的内存。对于内存较大的 32 位系统，这通常位于 `ZONE_HIGHMEM`，但对于 64 位系统，将使用 `ZONE_NORMAL` 或 `ZONE_DMA32`。

实际计算过程相当冗长，但并不有趣，因此我不再详细考虑它。重要的是结果：

- 存储在全局变量 `movable_zone` 中的虚拟 `ZONE_MOVABLE` 对应的物理区域。
- 对于每个节点，可移动区域中从何之后属于 `ZONE_MOVABLE` 的页帧位于 `zone_movable_pfn[node_id]` 中。

```c
mm/page/alloc.c
unsigned long __initdata zone_movable_pfn[MAX_NUMNODES];
```

内核确保这些页面将用于满足属于 `ZONE_MOVABLE` 责任范围的分配。

## 实现

这些数据结构是如何被投入使用的？与页面迁移方法一样，分配标志（allocation flags）起着至关重要的作用。它们在第 3.5.4 节中进行了更详细的讨论。在这里，只需说明所有可移动分配必须指定 `__GFP_HIGHMEM` 和 `__GFP_MOVABLE`。

由于内核通过分配标志来确定满足分配的区域，因此当标志被设置时，它可以选择 `ZONE_MOVABLE`。这是将 `ZONE_MOVABLE` 集成到伙伴系统（buddy system）中所需的唯一更改！其余部分由在所有区域运行的通用例程完成，见下文。

## 3.5.3 初始化区域和节点数据结构

到目前，我们只看到了内核如何在特定架构的代码中检测系统中的可用内存。与高级结构——区域（zones）和节点（nodes）的关联需要根据这些信息来构建。回想，架构要求在启动期间建立以下信息：

- 系统各种区域的页帧边界，存储在 `max_zone_pfn` 数组中。
- 作为节点分布的页帧，存储在全局变量 `early_node_map` 中。

### 管理数据结构的创建

从内核 2.6.10 开始，提供了一个通用框架来将这些信息传输到伙伴系统建立的节点和区域数据结构中；在此之前，每个架构必须自己设置这些结构。今天，只需使用上述简单结构并将艰性工作留给 `free_area_init_nodes` 即可。图 3-27 显示了该过程的概述，图 3-28 显示了 `free_area_init_nodes` 的代码图。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_242_0.png)

图 3-27：特定架构代码与通用内核代码设置节点和区域内存数据结构的相互作用概述。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_242_1.png)

图 3-28：`free_area_init_nodes` 的流程图。

`free_area_init_nodes` 必须分析并重写由特定架构代码的信息。，可以使用每个区域的最低和最高页帧数量——与 `zone_max_pfn` 和 `zone_min_pfn` 中的物理边界不同——来获取。使用了两个全局数组来存储这些信息：

```c
mm/page_alloc
static unsigned long __meminitdata arch_lowest_possible_pfn[MAX_NR_ZONES];
static unsigned long __meminitdata arch_highest_possible_pfn[MAX_NR_ZONES];
```

但是，`free_area_init_nodes` 首先按照其第一个页帧起始 `start_pfn` 排序 `early_zone_map` 中的条目。

```c
mm/page_alloc
void __init free_area_init_nodes(unsigned long *max_zone_pfn)
{
    unsigned long nid;
    enum zone_type i;

    /* 假设 early_node_map 初始化时是已排序的 */
    sort_node_map();
}
```

排序条目让后续任务变得更容易，但并不特别复杂，因此不需要进一步检查 `sort_node_map`。注意，内核在 `lib/sort.c` 中提供了一个通用的堆排序实现，该函数正是使用了它。

传递给 `free_area_init_nodes` 的 `zone_max_pfn` 返回了包含在每个区域的最大页帧号。`free_area_init_nodes` 通过为上述全局变量中的每个区域提供 `[low,high]` 形式的页帧区间，提供了这些信息的方便表示（我省略了值为零的变量）：

```c
mm/page_alloc.c
arch_lowest_possible_pfn[0] = find_min_pfn_with_active_regions();
arch_highest_possible_pfn[0] = max_zone_pfn[0];

for (i = 1; i < MAX_NR_ZONES; i++) {
    if (i == ZONE_MOVABLE)
        continue;
    arch_lowest_possible_pfn[i] =
        arch_highest_possible_pfn[i-1];
    arch_highest_possible_pfn[i] =
        max(max_zone_pfn[i], arch_lowest_possible_pfn[i]);
}
```

辅助函数 `find_min_pfn_with_active_regions` 用于寻找最低区域的最小页帧。这必须是 `ZONE_DMA`，但如果机器不需要 DMA，可以是 `ZONE_NORMAL`。最低区域的最大页帧可以直接从 `max_zone_pfn` 提供的信息中。

其他区域的区间是以直接构建的：第 $n$ 个区域的最小页帧是上一个 $(n-1)$ 区域的最大页帧。当前区域的最大页帧已经在 `max_zone_pfn` 中。

```c
mm/alloc.c
arch_lowest_possible_pfn[ZONE_MOVABLE] = 0;
arch_highest_possible_pfn[ZONE_MOVABLE] = 0;
```

```c
/* 找到每个节点 MOVABLE 开始的 PFN */
find_movable_pfn_for_nodes(zone_movable);
```

由于 `MOVABLE` 是虚拟区域且不与真实硬件关联，区域边界始终设置为零。如果之前指定了命令行参数 `kernelcore` 或 `movablecore`，则并非如此。每个节点的可移动区域从每个节点的某个特定页帧开始。相应的数字在 `find_movable_pfn_for_nodes` 中计算。

关于确定的页帧区间的一些信息广泛呈现给用户。例如，4 GiB 内存的 AMD64 系统上的输出：

```
root# dmesg
Zone PFN ranges:
DMA 0 -> 4096
DMA32 4096 -> 1048576
Normal 1048576 -> 1245184
```

`free_area_init_nodes` 的剩余部分遍历所有节点以设置每个节点的数据结构。

```c
mm/alloc.c
/* 打印区域信息 */

/* 初始化每个节点 */
for_each_online_node(nid) {
    NODE_DATA(nid);
    pg_data_t *pgdat =
        free_area_init_node(nid, pgdat, NULL);
    find_min_pfn_for_node(nid, NULL);

    /* 该节点上的任何内存 */
    if (pgdat->present_pages)
        node_set_state(nid, N_HIGH_MEMORY);
        check_for_regular_memory(pgdat);
}
```

代码遍历所有活动节点，并将每个节点的设置委托给需要第一个可用页帧作为参数的函数 `find_min_pfn_for_node` 从 `early_node_map` 中提取此信息。

如果根据 `node_present_pages` 字段节点配备内存，则通过设置 `N_HIGH_MEMORY` 标志反映在内存位图中。回想第 3.2.2 节，该标志尽管命名如此，仅信号节点上存在普通内存或高内存，因此 `check_for_regular_memory` 检查 `ZONE_HIGHMEM` 以下的任何区域，并在内存位图中设置 `N_NORMAL_MEMORY` 标志。

### 创建每个节点的数据结构

一旦确定了边界，`free_area_init_nodes` 通过调用 `free_area_init_node` 创建各个区域的数据结构。为此需要几个辅助函数。
