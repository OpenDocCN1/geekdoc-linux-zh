
最后，如果既没有指定 `MAP_SHARED` 也没有指定 `MAP_PRIVATE`，我们会报错。注意 `MAP_SHARED_VALIDATE` 不是匿名映射的有效标志。查看列表 5-13 中 `do_mmap()` 的最后部分。

> * 某些架构可能会指定 `VM_GROWSUP` 标志来表示向上增长的堆栈，然而我们不考虑此类架构。

内存映射 291

# Linux 内存管理器（早期访问版）© 2025 Lorenzo Stoakes

```c
1526
1527
/* 如果我们不应该计算此映射的
1528
* 内存使用，设置 'VM_NORESERVE'
1529
*/
1530
if (flags & MAP_NORESERVE) {
1531
/* 如果允许内存过度提交，我们尊重 MAP_NORESERVE */
1532
    if (sysctl_overcommit_memory != OVERCOMMIT_NEVER)
1533
        vm_flags |= VM_NORESERVE;
1534
1535
/* 除非指定 MAP_NORESERVE，否则 hugetlb 采用严格的过度提交 */
1536
    if (file && is_file_hugepages(file))
1537
    vm_flags |= VM_NORESERVE;
1538
}
1539
1540
addr = mmap_region(file, addr, len, vm_flags, pgoff, us);
1541
if (!IS_ERR(addr) &&
1542
(vm_flags & VM_LOCKED) ||
1543
(flags & (MAP_POPULATE | MAP_NONBLOCK)) == MAP_POPULATE)
1544
/* populate = len; */
1545
return addr;
1546
```

列表 5-13: do_mmap().c

我们首先处理 `MAP_NORESERVE` 情况。如果过度提交模式（第 4.1 节）不是 `OVERCOMMIT_NEVER`，或者这是一个大页，则设置 `VM_NORESERVE` 标志（关于此点的更多讨论，请参见映射标志的讨论）。

在设置所有标志并执行检查后，实际映射由 `mmap_region()` 执行，我们将检查它。

如果成功，则检查 `MAP_POPULATE` 语义——如果该区域未锁定（则已经填充过），且指定了 `MAP_POPULATE` 但没有指定 `MAP_NONBLOCK`，则执行填充。

我们从列表 5-4 开始检查 `mmap_region()`：

```c
1681 unsigned long mmap_region(struct file *file, unsigned long addr,
1682 signed long len, unsigned long vm_flags, unsigned long pgoff,
1683 struct list_head *up)
1684 {
1685 struct mm_struct *mm = current_mm;
1686 struct vm_area_struct *vma, *prev, *merge;
1687 int error;
1688 struct rb_node **rb_link, *rb_parent;
1689 signed long charged = 0;
1690
1691 /* 检查地址空间限制。 */
1692 if (!my_expand_vm(mm, vm_flags, len >> PAGE_SHIFT)) {
1693 signed long nr_pages;
1694
/* MAP_FIXED 可能会移除与请求映射相交的
* 映射的页面。计算它将卸载的页面 */
1695
1696
nr_pages = count_vma_range(mm, addr, addr + len);
1697
if (!may_expand_vm(mm, vm_flags,
1698 (len >> PAGE_SHIFT) - nr_pages))
1700 return -ENOM1;
1701
1702
1703
1704
1705
1706
1707
1709
1710
1711
1711
```

列表 5-14: mm/map.c: map_region() 初始化与早期退出

我们通过 `expand_vm()` 开始检查地址空间限制，这确保了 `RLIMIT_AS` 和 `RLIMIT_DATA` 被遵守。如果显然被违反，我们使用 `count_vma_range()` 对任何交叉映射进行昂贵的计数，并在重试之前减去这些计数。注意，区域内的任何 VMA 交叉都意味着指定了 `MAP_FIXED`，否则调用代码现在就会报错。为了方便起见，通过 `munmap_range()` 映射区域内的任何内存。调用 `find_vma()` 获取之前的 VMA、父节点以及新插入 VMA 的指针（即其父节点的左或右节点）。

内存映射 293

# Linux 内存管理器（早期访问版）© 2025 Lorenzo Stokes

查看第 5.6 节关于内存映射的详细说明。最后，如果我们简单将候选 VMA 与之前的 VMA 合并，我们通过 `vma_merge()` 实现，从而避免分配和设置新的 VMA。

我们查看在列表 5 中分配并初始化新 VMA 的代码：

```c
/* 确定被映射的对象并调用相应的映射器。地址已经过验证，
* 但尚未映射，不过映射已从列表中移除。 */

vma = vm_area_alloc(mm);

if (!vma) {
    error = -ENOMEM;
    vm_acct_error();
}

vma->vm_start = addr;
vma->vm_end = addr + len;
vma->vm_flags = vm_flags;
vma->vm_page_prot = vm_get_page_prot(vm_flags);
vma->vm_pgoff = pgoff;

if (file) {
    if (vma->flags & VM_SHARED) {
        error = mapping_map_writable(file->mapping);
        if (error)
            goto free_vma;
    }
}

vma->vm_file = get_file(file);
error = call_map(file, vma);
if (error)
    goto unmap_and_free_vma;

/* addr 可能改变？
+ 答：是的，多个设备驱动可以在它们
* f_op->mmap 方法中这样做。- Dave M
* Bug：如果 addr 改变，prev、rb_link、rb_parent
* 应为 vma_link() 更新 */
WARN_ON(addr != vma->vm_start);
addr = vma->vm_start;
```

```c
/* 如果 call_map() 之后 vm_flags 发生了变化，我们应该再次合并 vma
* 因为我们这次可能会成功。 */
if (unlikely(vm_flags != vm->vm_flags && prev)) {
    merge = vma->merge(mm, prev, vma->vm_start, vma->vm_end, vma->vm_flags,
        NULL, vma->vm_file, vma->vm_pgoff, NULL, NULL_VM_UFDX, NULL);
    if (merge) {
        /* vmap() 可能会改变 vma->vm_file，在这里释放原始文件
           * vma->vm_file，否则我们会增加额外的 fput
           * 并最终导致通用保护性异常。 */
        fput(vm_area_free(vma));
        vma = merge;
        /* 更新 vm_flags 以获取变化。 */
        vm_flags = vma->vm_flags;
        goto unmap_writable;
    }
    vm_flags = vma->vm_flags;
} else if (vm_flags & VM_SHARED) {
    error = shmem_zero_setup(vma);
    if (error)
        goto free_vma;
} else {
    vma_set_anonymous(vma);
}
```

```c
/* Allow_validate 对 vm_flags 进行合理性检查 */
if (arch_validate_flags(vma->vm_flags)) {
    error = -EINVAL;
    if (file)
        goto unmap_and_free_vma;
    goto free_vma;
}
```

```c
vma_link(mm, vma, prev, rb_link, rb_parent);
```

列表 5-15: mm/mmap.c: map_region() VMA 分配与初始化

我们通过 `vm_area_alloc()` 分配并初始化一个新的 VMA（关于本节的更多细节请参见 4.4.2 节），在输入参数分配 VMA 的 `vm_start`、`vm_end`、`vm_flags` 和 `vm_pgoff` 之前。

内存映射 295

# Linux 内存管理器（早期访问）©2025 Lorenzo Stokes

适用于 VMA（虚拟内存区域）的保护标志通过特定于架构的 `vm_get_page_prot()` 函数确定，该函数在虚拟内存章节的第 3.1.3 节中有详细描述。

按照惯例，文件映射比匿名映射更复杂——我们首先通过 `mapping_map_writable()` 指明我们有一个新的可写映射（内核合理地假设它是不可变的，但 `VM_SHARED` 意味着如果是共享的则映射是可写的）。

接下来，在通过 `call_mmap()` 调用系统自定义的 `struct file_operations` 处理句柄 `file->f_op->mmap` 之前，我们增加与映射相关的引用计数，如果调用失败则报错。

我们断言没有驱动程序对该地址进行异常操作，然后检查一个边缘情况——上述在 VMA 标志之前对文件系统内存映射钩子的调用可能更改了之前成功的合并，因此我们再次通过 `vma_merge()` 执行合并，如果发生了合并，则清理自身并退出。

跳过匿名共享的情况——如果 VMA 是私有的且匿名的，我们调用 `vma_set_anonymous()`，它会清空 `vm_area_alloc()->vm_ops` 字段，以明确指示该 VMA 是匿名的（注意，在分配时，VMA 的字段由 `vma_init()` 初始化，它将 `vm_ops` 默认指向一个静态的空 `dummy_vm_ops` 对象）。

在共享匿名映射（即用户同时指定了 `MAP_ANONYMOUS` 和 `MAP_SHARED`）的情况下，需要特殊处理，因为内核不支持共享匿名映射，而是通过 RAM 支撑的文件映射处理来绕过。这在列表 5-16 所示，在 `shmem_zero_setup()` 中完成。

```c
/**

 * shmem_zero_setup - 设置共享匿名映射
 * @vma/ 要映射的 vma 由 do_mmap 准备
 */

int shmem_zero_setup(struct vma_area *vma)
{
    struct file *file;
    loff_t size = vma->vm_end - vma->vm_start;

    /*
     * 在 mmap_lock 下克隆新文件会导致 XFS 目录读取与 selinux
     * 之间的锁顺序冲突：由于该文件仅通过其映射对用户
     * 可用，使用 S_PRIVATE 标志绕过安全检查，
     * 与 shmem_kernel_file_setup() 相同
     */
    file = shmem_kernel_file_setup("dev/zero", size, vma->vm_flags);
    if (IS_ERR(file))
        return PTR_ERR(file);

    if (vma->vm_file)
        fput(vma->vm_file);

    vma->vm_file = file;
    vma->vm_ops = &shmem_vm_ops;
    return 0;
}
```

列表 5-16: mm/shmem.c: shmem_zero_setup()

这建立了一个指定大小的 `/dev/zero` 副本，作为一个未链接的 tmpfs 文件（即与一个新生成的 inode 绑定，该 inode 实际上已从文件系统中删除，但我们通过引用计数将其保留），并相应设置了 `vm_file` 和 `vm_ops`。这部分的重型工作由 `shmem_kernel_file_setup()` 完成，其描述不在本文讨论范围内。

一旦为每个文件映射、匿名共享和匿名私有用例建立了此设置；我们就调用 `arch_validate_flags()` 函数，该函数为那些在创建 VMA 时需要验证 VMA 标志的架构提供了钩子。

我们通过 `vma_link()` 将此新分配并设置的 VMA 链接到 VMA 链表和红黑树（参见列表 4-21）。

最后，让我们检查列表 5-17 中 `mmap_region()` 的错误处理和共享代码（省略了超出范围的大页逻辑、向上计数逻辑和性能事件逻辑）。

```c
/* 一旦 vma 拒绝写入，撤销我们的临时拒绝计数 */
unmap_writable:
    if (file & vm_flags & VM_SHARED)
        mapping_unmap_writable(file->f_mapping);
    file = vma->vm_file;

out:
    vm_stat_account(mm, vm_flags, len >> PAGE_SHIFT);
    if (vm_flags & VM_LOCKED) {
        if ((vm_flags & VM_SPECIAL) || vma_is_dax(vma) ||
            is_vm_hugetlb_page(vma)) ||
            vma = get_gate_vma(current->mm)
            vma->vm_flags &= VM_LOCKED_CLEAR_MASK;
    else
        mm->locked_vm += (len >> PAGE_SHIFT);
    }
```

列表 5-17: mm/mmap.c: mmap_region() 错误处理和共享

注意，“shmem”实现了基于 RAM 的文件系统，最著名的是 tmpfs。

```c
/*
1835 * 新（或扩展的）vma 总是获取脏状态。
1836 * 否则用户空间软脏页跟踪器将
1837 * 无法区分 vma 区域被取消映射的情况，
1838 * 然后新的映射在原地映射（这必须目标是
1839 * 一个完全全新的数据区域）。
*/
1841 vma->vm_flags = VM_DIRTY;
```

# Linux 内存管理器（早期访问）© 2025 Lorenzo Stoakes

```c
/* open 常程是否对保护属性做了某些
pgprot_modify
    * 无法保留的修改？ */
if (pgprot_val(vm_page_prot) != pgprot_val(vm_pgprot_modify(vm_page_prot, vm_flags)))
    return 0;

/*
    * 我们是否需要跟踪 softdirty？hugetlb 尚未支持
    * soft-dirty 追踪。 */
if (vm_soft_dirty_enabled(va) && !is_vm_hugetlb_page(vm))
    return 1;

/* 特殊映射？ */
if (vm_flags & VM_PFMAP)
    return 0;

/* 映射可以跟踪脏页吗？ */
return vma->vm_file && vma->wants_mapping &&
    mapping_can_writeback(vma->vm_file->f_mapping);
```
