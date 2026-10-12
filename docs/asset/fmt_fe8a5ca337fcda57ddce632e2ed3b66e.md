
`do_wp_page`负责创建页副本并将其插入进程的页表中——并赋予硬件写权限。这种机制被称为写时复制（简写为 COW），在第 1 章中进行了讨论。当进程进行 `fork` 时，页面不会立即复制，而是以“只读”副本的形式放入进程的地址空间中，以免在（浪费的）信息复制上花费过多时间。在进程发生访问之前，不会创建页面的独立副本。

下文将详细查看在页异常修复期间调用的异常处理程序的实现。这些部分没有涵盖 `do_swap_page` 中如何将页面换入交换区的方法，因为该主题在第 18 章有专门讨论，并且需要对交换管理器的结构和组织的额外知识。

## 4.11.1 需需分配/分页

页分配被委托给定义在 `mm/memory.c` 中的 `do_linear_fault`。在经过一些参数转换后，内核被交给 `__do_fault`，其代码流程如图 4–19 所示。

首先，内核必须确保数据被读取到发生异常的地址空间，处理方式取决于映射的文件，特定方法会被调用以获取数据。通常，它存储在 `vm->mm_ops->fault` 中。由于早期的内核版本使用不同调用约定的方法，对于某些代码尚未更新以使用新方法的情况，引入了新约定。因此，如果没有注册异常方法，则会调用旧的变体 `vm->mm_ops->nopage`。

大多数文件使用 `filemap` 来读取所需数据。该函数不仅读取所需数据，还实现了预读（`readahead`）功能，即会提前读取未来可能需要的页面。实现此目的机制在第 16 章中介绍，该章更详细讨论了该函数。目前，我们只需要知道内核使用 `address_space` 对象中的信息将数据从存储（backing store）读取到物理内存页。

### 第 4 章：进程虚拟内存

![](img/a80e0e530e25bf9e2df2fc130fff42a2_370_0.png)

考虑到涉及的 `vm_area_struct` 区域，内核如何选择使用哪种方法读取页面？

1. 使用 `vm_area_struct->vm_file` 找到映射的文件。
2. 可以在 `file->f_mapping` 中找到映射本身的指针。
3. 每个地址都有特殊的空间操作，可以从中选择 `readpage` 方法。数据通过 `mapping->a_ops->readpage(file, page)` 从文件传输到 RAM。

如果需要访问，内核必须区分共享映射和私有映射。对于私有映射，必须准备页面的副本。

```c
mm/memory.c

static int __do_fault(struct mm_struct *mm, struct vm_area_struct *vma,
    unsigned long address, pmd_t *pmd,
    pgoff_t pgoff, unsigned int flags, pte_t *orig_pte)
```

...

### 第 4 章：进程虚拟内存

```c
/*
* 我们应该进行早期的 C-O-W 破坏吗？
*/

if (flags & FAULT_FLAG_WRITE) {
    if (!(vma->flags & VM_SHARED)) {
        anon = i;
        if (unlikely(anon_vma_prepare(vma))) {
            ret = VM_FAULT_OOM;
            goto out;
        }
        page = alloc_page_vma(GFP_HIGUSHER_MOVABLE, vma, address);
    }
}

...

copy_user_highpage(page, vmf.page, address, vma);
```

一旦通过 `anon_vma_prepare` 为区域创建了新的 `anon_vma` 实例，必须分配新页（在 `anon_vma_prepare` 中，旧区域的指针被重定向到新区域）。此目的优先使用高内存（high memory area），因为它对用户态没有问题。`copy_user_highpage` 创建数据的副本（内核和用户态之间拷贝数据的例程在第 4.13 节中描述）。

现在页面的位置已知，必须将其添加到进程的页表中并整合反向映射数据结构。在此之前，会创建一个缓存以通过 `flush_icache_page` 更新缓存来确保页面内容可见（处理器不需要执行此操作，执行空操作即可）。

通常指向只读页面的页表是使用第 3.3.2 节讨论的 `mk_pte` 函数生成的。如果发生了写访问，则使用 `mk_pte` 生成指向只读页面的页表。

根据类型，通过 `lru_cache_add_active` 将页面添加到活跃区域（第 16 章详细讨论了缓存机制），然后通过 `page_add_anon_rmap` 整合到反向映射中。`page_add_new_rmap` 处理写访问的函数在第 4.8 节中讨论。

## 4.11.2 匿名页

`do_anon_page` 被调用以映射存储支持。除了需要将数据读入页外，该过程与映射文件支持数据的方式无异。在活跃区域创建一个新页，然后将其添加到进程的页表中，并更新缓存/MMU。

请注意，早期的内核区分读取和写匿名映射：在第一情况下，使用零页来满足请求。在内核 2.6.24 开发期间，这种行为被弃用了，因为测量显示性能提升微乎其微，而共享映射会出现很多问题，我在这里不想讨论。

### 第 4 章：进程虚拟内存

## 4.11.3 写时复制

写时复制在 `do_wp_page` 中处理，其代码流程如图 4-20 所示。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_372_0.png)

图 4-20：`do_wp_page` 代码流程。

让我们查看一个稍微简化的版本，我省略了与交换缓存的潜在干扰，因为这会使情况复杂而无法揭示机制本身。

内核首先调用 `vm_normal_page` 通过页表项找到页的 `struct page` 实例——该函数基于 `cte_pfn` 和 `pfn_to_page`，后者在所有架构上必须定义。前者查找关联页表项的页码，后者根据页码确定页实例。这是可能的，因为 COW 机制仅针对位于内存中的页面调用（否则它们将首先由其他页异常机制自动加载）。

通过 `page_cache_get_anon` 获取页引用后，`anon_vma_prepare` 准备反向映射数据结构以接受新的匿名区域。由于异常源自必须拷贝到新页的有用数据，内核调用 `alloc_page_vma` 分配新页。`cow_user_page` 将异常页的数据拷贝到新页中，进程随后向新页写入。

然后使用 `page_remove_rmap` 移除指向原始只读页的反向映射。新页被添加到页表中，此时必须同时更新 CPU 缓存。

最后的操作包括使用 `lru_cache_add_active` 将新分配的页放入 LRU 缓存列表中，并并通过 `page_add_anon_rmap` 将其插入反向映射数据结构中。此后，用户态进程可以尽情地向该页写入。

# 第 4 章：虚拟进程内存

## 4.11.4 获取非线性映射

非线性映射的页处理程序比上述描述的方法要短得多：

```c
## memory.c

static int do_nonlinear_fault(struct mm_struct *mm, struct vm_area_struct *vma,
    unsigned long address, pte_t *page_table, pmd_t *pmd,
    int write_access, pte_t *orig_pte)
{
    pgoff = pte_to_pgoff(orig_pte);
    return _do_fault(mm, vma, address, pmd, pgoff, flags, orig_pte);
}
```
