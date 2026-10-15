
PPC 的 `mem_init()` 代码查找并初始化所有区：

```c
arch/ppc/mm/init.c
void __init mem_init(void)
{
    unsigned long addr;
    unsigned int _va_mem = 0;
    int codepages = 0;
    int datapages = 0;
    int initpages = 0;
    #ifdef CONFIG_HIGHMEM
    unsigned long highmem_mapnr = mapnr;
#endif
    highmem_mapnr = total_lowmem >> PAGE_SHIFT;
    highmem_start_page = mem_map + highmem_mapnr;
#endif /* CONFIG_HIGHMEM
    max_mapnr = total_memory;
    high_memory = (void *)_va(PPC_MEMSTART + total_lowmem);
    num_physpages = mapnr; /* RAM 假设是连续的 */
    totalram_pages += free_allocmem(0);
#ifdef CONFIG_BLK_DEV_INIT
    /* 如果带有初始 ramdisk 启动，确保 ramdisk 页未被预留。 */
    if (init_start) {
    for (addr = init_start; addr < init_end; addr += PAGE_SIZE)
        ClearPageReserved(virt_to_page(addr));
    }
}
#endif /* CONFIG_BLK_DEV_INIT */

#ifdef CONFIG_PPC_OF
    /* 将 RTAS 页标记为预留 */
    if (rt_data) {
    for (addr = (unsigned long)_va(rt_data);
         addr < PAGE_ALIGN((unsigned long)_va(rt_data)+rtas_size);
         addr += PAGE_SIZE)
        SetPageReserved(virt_to_page(addr));
    }
    elseif (agp_special_page)
    SetPageReserved(virt_to_page(agp_special_page));
#endif
if (sysmap) {
    for (addr = (unsigned long)sysmap;
         addr < PAGE_ALIGN((unsigned long)sysmap+sysmap_size);
         addr += PAGE_SIZE)
        SetPageReserved(virt_to_page(addr));
}
#endif /* CONFIG_PPC_OF
for (addr = PAGE_OFFSET; addr < (unsigned long)high_memory;
    addr += PAGE_SIZE) {
    if (!PageReserved(virt_to_page(addr)))
        continue;
    if (addr < (unsigned long)etext)
        codepages++;
    else if (addr >= (unsigned long)&init_begin
        && addr < (unsigned long)&init_end)
        initpages++;
    else if (addr < (unsigned long)klimit)
        datapages++;
}

#ifdef CONFIG_HIGHMEM
{
    unsigned long pfn;
    for (pfn = himem_mapnr; pfn < max_mapnr; ++pfn) {
        struct page *page = mem_map + pfn;

        ClearPageReserved(page);
        set_bit(PG_highmem, page->flags);
        set_page_count(page, 1);
        __free_page(page);
        totalhigh_pages++;
    }
    totalram_pages += totalhigh_pages;
}
#endif

printf("Memory: %lu available (%dk kernel code, %ld data, %ld reserved, %ld init, %ld highmem)\n",
(unsigned long)nr_free_pages<< (PAGE_SHIFT-10),
codepages<< (PAGE_SHIFT-10), datapages<< (PAGE_SHIFT-10),
initpages<< (PAGE_SHIFT-10), (unsigned long)totalhigh_pages<< (PAGE_SHIFT-10));
if (sysmap)
    printf("System map loaded at 0x%x for debugger, size: %ld bytes\n",
    (unsigned long)sysmap, sysmap_size);
#ifdef CONFIG_PPC_PMAC
if (agp_special_page)
    printf("KERN_INFO AGP special page: 0x%08lx\n", agp_special_page);
#endif
```

# 8.5 起始：`start_kernel()`

```c
491     }
492     }
493     mem_init_done = 1;
494 )
```

第 399–410 行

这些行查找可用内存量。如果使用了 `HIGHMEM`，这些页面也会被计入内。全局变量 `totalram_pages` 被修改以反映这一点。

第 412–419 行

如果已使用，清除启动 RAM 磁盘已使用的任何页面。

第 421–432 行

根据启动环境，在需要时，为实时抽象服务（Real-Time Abstraction Services）和 AGP（视频）预留页面。

第 433–450 行

如果需要，为系统映射（`system map`）预留一些页面。

第 452–467 行

如果使用 `HIGHMEM`，清除所有预留的页面并修改全局变量 `totalram_pages`。

第 469–480 行

向控制台打印内存信息。

第 482–492 行

遍历页目录并初始化每个 `mm_struct` 和索引。

## 8.5.21 调用 `late_time_init()`

第 459–460 行

函数 `late_time_init()` 使用 HPET（参见“对 `time_init` 的调用”章节下的讨论）。该函数仅在 Intel 架构并配合 HPET 使用。该函数的代码与 `time_init()` 基本相同；它只是在内存初始化之后被调用，以便将 HPET 映射到物理内存。

## 8.5.22 调用 `calibrate_delay()`

第 461 行

`init/main.c` 中的函数 `calibrate_delay()` 计算并打印最著名的“BogoMips” 的值，这是一个衡量处理器在一个时钟周期（`clock tick`）内可以执行 `delay()` 迭代次数的指标。`calibrate_delay()` 使得不同速度下的延迟保持大致相同。得到的值——最多只是处理器运行快慢的指标——被存储在 `loop_pre_jiffy` 中，`udelay()` 和 `mdelay()` 函数使用它设置执行的 `delay()` 迭代次数：
