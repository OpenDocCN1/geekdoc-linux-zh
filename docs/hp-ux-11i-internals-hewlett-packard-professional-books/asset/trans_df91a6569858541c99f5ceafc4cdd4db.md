

池（pool），此逻辑视图池中池的链表，
指向父 lmv 结构的指针，以及
此池的“已用”计数

16 0 4 0 *     lmv_pools[0].pp_next
20 0 4 0 *     lmv_pools[0].pp_f1_lock
24 0 4 0 *     lmv_pools[0].pp_next_pool
28 0 4 0 *     lmv_pools[0].pp_lmv
32 0 4 0 *     lmv_pools[0].pp_n_used

在池结构中，我们有两个水塘（pond）结构。每个
水塘以其空闲链表头指针、此水塘的空闲计数、指向父池结构的指针
开头

36 0 4 0 *     lmv_pools[0].pp_ponds[0].pp_phead
40 0 4 0 *     lmv_pools[0].pp_ponds[0].pp_n_free
44 0 4 0 *     lmv_pools[0].pp_pools[0].pp_pool

此外，还有一个索引计数，用于 pp_phead[] 中活动条目的数量
（允许的内核大小数量），此水塘的索引计数器，以及
由惰性合并例程使用的低水位和高水位标记

48 0 4 0 u_int lmv_pools[0].pp_ponds[0].pp_max_idx
52 0 4 0 u_int lmv_pools[0].pp_ponds[0].pp_pool_index
56 0 4 0 u_int lmv_pools[0].pp_ponds[0].pp_lb_shift
60 0 4 0 u_int lmv_pools[0].pp_ponds[0].pp_ub_shift

64 0 4 0 *     lmv_pools[0].pp_ponds[1].pp_phead
68 0 4 0 *     lmv_pools[0].pp_ponds[1].pp_n_free
72 0 4 0 *     lmv_pools[0].pp_pools[1].pp_pool
76 0 4 0 u_int lmv_pools[0].pp_ponds[1].pp_max_idx
80 0 4 0 u_int lmv_pools[0].pp_ponds[1].pp_pool_index
84 0 4 0 u_int lmv_pools[0].pp_ponds[1].pp_lb_shift
88 0 4 0 u_int lmv_pools[0].pp_ponds[1].pp_ub_shift

每个池维护可用页帧的总计数
及其状态标志

92 0 4 0 int     lmv_pools[0].pp_pfdatum_num_entries
96 0 4 0 u_int lmv_pools[0].pp_flags

100 0 4 0 *     lmv_pools[1].pp_next
104 0 4 0 *     lmv_pools[1].pp_f1_lock
108 0 4 0 *     lmv_pools[1].pp_next_pool
112 0 4 0 *     lmv_pools[1].pp_lmv
116 0 4 0 *     lmv_pools[1].pp_n_used
120 0 4 0 *     lmv_pools[1].pp_ponds[0].pp_phead
124 0 4 0 *     lmv_pools[1].pp_ponds[0].pp_n_free
128 0 4 0 *     lmv_pools[1].pp_ponds[0].pp_pool
132 0 4 0 u_int lmv_pools[1].pp_ponds[0].pp_max_idx
136 0 4 0 u_int lmv_pools[1].pp_ponds[0].pp_pool_index
140 0 4 0 u_int lmv_pools[1].pp_ponds[0].pp_lb_shift
144 0 4 0 u_int lmv_pools[1].pp_ponds[0].pp_ub_shift
148 0 4 0 *     lmv_pools[1].pp_ponds[1].pp_phead
152 0 4 0 *     lmv_pools[1].pp_ponds[1].pp_n_free
156 0 4 0 *     lmv_pools[1].pp_ponds[1].pp_pool
160 0 4 0 u_int lmv_pools[1].pp_ponds[1].pp_max_idx
164 0 4 0 u_int lmv_pools[1].pp_ponds[1].pp_pool_index
168 0 4 0 u_int lmv_pools[1].pp_ponds[1].pp_lb_shift
172 0 4 0 u_int lmv_pools[1].pp_ponds[1].pp_ub_shift
176 0 4 0 int     lmv_pools[1].pp_pfdatum_num_entries
180 0 4 0 u_int lmv_pools[1].pp_flags

pp_phead[1] 包含每个水塘的实际空闲链表指针。此数组中的第一个元素
具有一页帧空闲链表的 next 和 previous 指针，第二个条目
具有指向四页帧空闲链表的链接指针，第三个
指向 16 页帧空闲链表，依此类推，直到最大配置的内核大小。为了便于管理多种内核大小，
创建了一个名为 memory page_group 的附加结构。

## 可变内核大小

HP-UX 11.00 版本引入了可变内核大小（vps），也称为性能优化的内核大小分配（pops）。此功能使内核能够利用 PA-RISC 2.0 处理器中引入的新硬件特性。在新的宽处理器上，tlb 引入了一个附加字段，允许映射各种虚拟到物理的内核转换大小。基本页帧仍为 4Kbytes，但 vps 参数允许单个 tlb 条目以单条目将 4Kbytes 映射到最多 1048576 Kbytes 的连续物理内存。内核大小由 ttbl/pdir 条目中的 5 位字段确定。当前实现的内核大小范围从 1 到 256K 页帧（每个 progressively 更大的大小是前一个较小大小的 4 倍）。内核跟踪进程的内存使用量，并且可以调整程序或程序员使用的内核大小，或使用 chptr 命令调整内核大小。有几个内核可调参数用于控制此功能：

-   vps_pagesize 此参数设置基本内核大小，默认为 4Kbytes
-   vps_ceiling 此参数设置内核可能选择的最大内核大小，目前限制为 65536KBytes
-   vps_chptr_ceiling 这是可通过 chptr() 请求的最大内核大小，限制为 1048576KBytes

就内核内存管理而言，各种大小被称为页组（page group）。正如我们在图 6-17 中看到的，page_group 结构帮助内核识别和管理连续的免费页块。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_215_0.png)

`page_group` 结构包含有助于内核决定此组是否可以与其“伙伴”合并以形成更大组的信息。让我们通过清单 6.14 查看该结构。

Listing 6.14 q4> fields struct page_group

    连接池中所有组的链接指针
    0 0 4 0 *     pg_next
    指向此组 pfdт 数组开头的指针
    4 0 4 0 *     pg_pfdт
    此组中的页帧数量
    8 0 4 0 int   pg_npfns
    此组中的第一个页帧
    12 0 4 0 u_int pg_firstpfn
    指向此组所属池的指针
    16 0 4 0 *     pg_pool

## HP-UX 11.0 中的物理内存分配器

既然我们已经检查了 `lmv` 的各种组件，我们必须将它们全部结合起来，并考虑内存分配和内存释放这两个任务。图 6-18 将这些结构结合在一个视图中。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_216_0.png)

Figure 6-18 物理内存分配器

### 分配内存

内核例程 **allocate_page()** 负责分配特定请求大小的物理页。它与视图、池和水塘协同工作。基本算法工作原理如下：

-   尝试从所有池中所需大小（或更大）的缓存水塘中进行分配。初始池由 **CHOOSE_VIEW_AND_POOL()** 确定，该函数基于底层系统架构进行键控。
-   如果初始池无法满足请求，则调用 **NEXT_POOL_TO_TRY()** 来选择下一个受害者。
-   如果请求是等效映射的页，则首先尝试处理器自身的 lmv **EQUIV_MAPPED_POOL**；然后尝试其他 lmv **EQUIV_MAPPED_POOLS**。
-   如果请求是非等效映射的页，则先尝试我们自己的 lmv **NON_EQUIV_MAPPED_POOL**，然后是其他 lmv **NON_EQUIV_MAPPED_POOLS**，最后尝试 **EQUIV_MAPPED_POOLS**。
-   如果所有池的所有缓存水塘都已尝试，则尝试所有池的缓存水塘。
-   如果仍然无法找到所需的内核大小，则将请求降级到下一个较小的内核大小，并重复上述步骤。
-   如果仍然无法完成请求的分配，并且调用不允许阻塞，则返回 **NULL**，让线程处理失败。
-   如果允许阻塞，则在唤醒分页守护程序和反哈希守护程序后，线程将进入睡眠状态。

### 释放内存

当存在多个空闲链表以及合并页面以形成更大 **页组** 的额外挑战时，释放内存使此过程变得复杂。图 6-19 说明了多个空闲链表的概念。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_217_0.png)

用于此艰巨任务的内核例程是 `freepfld()`。

-   `freepfld()` 的第一条规则是减少页的 `pfdt` 结构中的 `pf_use`。
-   如果 `pf_use` 现在为零，则物理页准备分配给空闲链表，前提是清理其 **哈希区域** 和 `pfn_to_virt` 表条目。
-   调用例程 `freeup_page()` 将页分配给适当的空闲池。
-   最后，全局空闲内存计数 `freemem` 在任何可能发生的合并之后增加。

### 合并空闲页

当页被放置在空闲链表上时，我们必须检查其邻居是否也是空闲的，并且它们是否可以合并以形成更大大小的空闲页。此过程称为 *页合并*。物理内存映射中彼此相邻的页称为伙伴，负责合并页的例程是 `place_on_freelist()`。`freeup_page()` 例程调用 `place_on_freelist()` 并传递它试图释放的物理页帧号。

