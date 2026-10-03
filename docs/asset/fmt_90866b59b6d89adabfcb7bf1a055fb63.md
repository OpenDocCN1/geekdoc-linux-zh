
函数最后如果指定了（例如用户设置了 `MAP_POPULATE`），通过 `__mm_populate()` 填充（即预取）范围。这最终调用 `__mm_populate()`，该函数在第 8.1.9 节描述。

### 列表 5-6: mm/util.c: `__mmap_pgoff()`

```c
/*
* 调用者必须锁定 current->mmmap_lock。
*/
unsigned long do_map(struct file *file, unsigned long addr,
                      unsigned long len, unsigned long prot,
                      unsigned long flags, unsigned long pgoff,
                      unsigned long *populate, struct list_head *uf) {
    struct mm_struct *mm = current->mm;
    vm_flags_t vm_flags;
    int pkey = 0;

    *populate = 0;

    if (len)
        return -EINVAL;

    /*
* 应用是否期望 PROT_READ 意味着 PROT_EXEC？
* （异常是底层文件是以 noexec 模式挂载的，
* 在这种情况下我们添加 PROT_EXEC）。
*/
    if ((prot & PROT_READ) && (current->personality & PROT_IMPLIES_EXEC))
        if (!file && path_noexec(&file->f_path))
            prot = PROT_EXEC;

    /* 强制在 get_unmapped_area 中处理架构特定的 MAP_FIXED */
    if (flags & MAP_FIXED_NOREPLACE)
        flags = MAP_FIXED;
```

### 列表 5-7: mm/map.c: `do_map()` 参数过滤

我们从简单的初始化和参数过滤开始。如果没有指定长度，则返回错误，否则如果 `PROT_READ` 意味着 `PROT_EXEC`（正如在某些架构上如此）。

Linux 内存管理器（早期访问）© 2025 Lorenzo Stoakes

最后，我们确保如果设置了 `MAP_FIXED_NOREPLACE`，则始终设置 `MAP_FIXED`，以确保在 `get_unmapped_area()` 中运行特定架构的逻辑，该函数只有在在前一个标志被正确调用时才会执行。

我们查看列表 5-8 中该函数的实现。

```c
if (!(flags & MAP_FIXED))
    addr = round_hint_to_min(addr);

/* 注意溢出.. */
len = PAGE_ALIGN(len)
if (!len)
    return -ENOMEM;

/* offset 溢出? */
if ((pgoff + (len >> PAGE_SHIFT)) < pgoff)
    return -EEOVERFLOW;

/* 映射过多? */
if (mm->map_count > sysctl_max_map_count)
    return -ENOMEM;

/* 获取要映射的地址。我们验证（或选择）该地址并确保
 它代表地址空间的有效区域。 */
addr = get_unmapped_area(file, addr, len, pgoff, flags);
if (IS_ERR_VAL(addr))
    return addr;

if (flags & MAP_FIXED_NOREPLACE) {
    if (find_vma_intersection(mm, addr, addr + len))
        return -EEXIST;
}

/* 在此处进行一些检查，这样底层例程就不需要
* 了。我们假设权限已经通过打开内存对象
* 处理过，所以我们这里没有相关处理。 */
vm_flags = calc_vm_prot_bits(prot, pkey) | calc_vm_flag_bits(flags) |
    mm->def_flags | VM_MAYED | VM_WRITE | VM_MAXEXEC;

if (flags & MAP_LOCKED)
    if (!can_do_lock())
        return -EPERM;

if (mlock_future_check(mm, vm_flags, len))
    return -EAGAIN;
```

### 列表 5-8: mm/mmap.c: `do_mmap()` 初始检查与设置

我们首先确保任何指定的提示地址（即作为 `addr` 参数，且未指定 `MAP_FIXED` 标志）都经过了页对齐，并且通过 `round_hint_to_min()` 大于 `mmap_addr` 允许的最小值，如列表 5-9 所示。

```c
/*
 * 如果提示小于 mmap_addr，则更改提示使其
 * 尽可能低但仍大于 mmap_addr
 */
static inline unsigned round_hint_to_min(unsigned long long)
{
    hint &= PAGE_MASK;
    if ((void *)hint != NULL) &&
        (hint < mmap_addr))
            return PAGE_ALIGN(mmap_addr);
    return hint;
}
```

### 列表 5-9: mmap.c: `round_hint_to_min()`

随后，我们确保对 `len` 和 `pgoff` 参数进行检查，以确保它们没有接近其类型的最大值而可能导致溢出。

接下来，我们测试 `struct mm->map_count` 参数（计算进程地址空间中虚拟映射的数量）是否超过了 `vm.max_map_count` 可调参数。如果是，则报错。

该映射在虚拟内存中的具体位置由关键函数 `get_unmapped_area()` 决定。由于该函数是一个大主题，我们将讨论推迟到第 5.0.5 节。

如果指定了 `MAP_FIXED_NOREPLACE`，我们通过 `find_vma_intersection()` 确定是否存在现有的 VMA 与输入地址范围相交，如果是则报错。

VMA 标志始终默认为 `VM_READ`、`VM_WRITE`、`VM_MAKEY`——如果确定这些标志不适用，则取消这些标志。此外，`prot` 和 `flags` 隐含了进一步的 VMA 标志，这通过 `calc_vma_prot_bits()`（简单将 `PROT_xxx` 转换为 `VM_xxx`）和 `calc_vma_flags_bits()`（如上述列表 5-3 所示）结合 `struct mm_struct->def_flags` 中指定的故障进程地址空间来实现。

应用了两个针对 `lock()` 的检查。第一个是 `can_do_mlock()`，它检查 `RLIMIT_MEMLOCK` 是否不为零（或线程拥有 `CAP_IPC_LOCK` 权限*，它可以覆盖此限制）。第二个是 `mlock_future_check()`，如果设置了 `VM_LOCK`（即通过 `MAP_LOCK`），它确保对此映射的锁定不会导致超过 `RLIMIT_MEMLOCK` 用户限制（同样，除非线程拥有 `CAP_IPC_LOCK` 权限）。

* * Capabilities（能力）是基于线程的细粒度权限分配。*

一旦完成这些操作，我们继续检查 `flags` 字段是否有效并根据需要调整 VMA。针对文件映射和匿名映射有单独的逻辑，从列表 5-10 所示的文件映射情况开始。

```c
if (file) {
    struct inode *inode = file_inode(file);
    unsigned long flags_mask;

    if (!file_map_ok(file, inode, pgoff, len))
        return -EOVERFLOW;

    flags_mask = LEGACY_MAP_MAP | file->f_op->
    mmap_supported_flags;

    switch (flags & MAP_TYPE) {
        case MAP_SHARED:
            /*
             * 强制使用非旧标志使用 MAP_SHARED_VALIDATE。
             * 例如，在 MAP_SHARED 上使用 MAP_SYNC 是危险的，
             * 因为你并不知道其一致性。
             */
            flags &= LEGACY_MAP_MASK;
            fallthrough;
        case MAP_SHARED_VALIDATE:
            if (flags & ~flags_mask)
                return -EOPS;
            if (prot & PROT_WRITE) {
                if (!file->f_mode & FMODE_WRITE)
                        return -EACCES;
                if (IS_SWAP_FILE(file))
                        return -EBUSY;
            }
            /* 确保我们不允许对只追加
             * 文件写入 */
            if (IS_APPEND(inode) && !(file->f_mode & FMODE_WRITE))
                return -EACCES;

            vm_flags |= VM_SHARED | VM_MAYSHARE;
            if (!file->f_mode & FMODE_WRITE))
                vm_flags &= ~(VM_MAYWRITE | VM_SHARED);
            fallthrough;
        case MAP_PRIVATE:
            if (!(file->f_mode & FMODE_READ))
                return -EACCES;
            if (path_noexec(&file)) {
                if (vm_flags & VM_EXEC)
                    return -EPERM;
                vm_flags &= ~VM_MAYEXEC;
            }
            if (!file->f_op->mmap)
                return -ENODEV;
            if (vm_flags & (VM_WRITE|VM_SHARED))
                return -EINVAL;
            break;
        default:
            return -EINVAL;
    }
}
```

### 列表 5-10: mmap() do: 文件支持标志检查

我们首先通过 `file_mmap_ok()` 检查映射文件的大小是否合理，如列表 5-11 所示。

```c
static inline bool file_mmap_ok(struct file *file, struct inode *inode,
    unsigned long pgoff, unsigned long len)
{
    u64 maxsize = file_mmap_size_max(inode);
    if (maxsize && len > maxsize)
        return false;
    maxsize -= len;
    if (pgoff > maxsize >> PAGE_SHIFT)
        return false;
    return true;
}
```

### 列表 5-11: mm/mmap.c: `file_mmap_ok()`

此检查映射的长度（`len` 参数）小于或等于允许的大小，并且映射内的偏移（`pgoff` 参数，以页为单位）不会导致超出最大大小。最大大小由 `file_mmap_size_max()` 决定。该函数的关键目的是避免 32 位系统的溢出，因为文件大小可能是 64 位的，但我们必须确保可能无法正常工作的驱动索引是正确的。此逻辑添加于 commit be83bbf062: mmap: 引入合理的 mmap 限制。

执行此检查后，我们通过结合 `LEGACY_MAP_MASK` 与文件额外支持的标志（由 `struct file->f_op->mmap_supported_flags` 确定）来建立接受的标志掩码。

`LEGACY_MAP_MASK` 包含关键映射标志。排除弃用和重建的标志，包括 `MAP_SHARED`、`MAP_PRIVATE`、`MAP_FIXED`、`MAP_ANONYMOUS`、`MAP_UNINITIALIZED`、`MAP_GROWNSDOWN`、`MAP_LOCKED`、`MAP_NOSERVE`、`MAP_POPULATE` 和 `MAP_32BIT`。

映射类型由 `MAP_TYPE` 掩码，它涵盖了 `MAP_PRIVATE`、`MAP_SHARED` 和 `MAP_VALIDATE`，我们按如下方式处理这些标志：

* `MAP_SHARED` - 出指定此标志的原因，我们防止指定未识别或无效的标志，通过简单的与 `LEGACY_MAP_MASK` 取掩码将其忽略。这样做维持了不验证标志的行为，同时防止了无意中使用可能危险的标志（例如 `MAP_SHARED`）。

由于 `flags` 现在是有效子集，我们可以直接进入 `MAP_SHARED_VALIDATE` 情况，并在情况之间共享后续逻辑。

* `MAP_SHARED_VALIDATE` - 已经确立了有效标志集为 `LEGACY_MAP_MASK` 和 `file->f_op->mmap_supported_flags` 指定的，因此如果标志指定了这些以外的任何标志，则报错。

如果映射是读/写的（即指定了 `PROT_WRITE`），则我们确保文件是以写权限打开的且该文件未被指定为交换文件，如果任一不符合，我们返回错误。此外，如果文件是只追加的，我们不允许调用者以写模式内存映射文件，因为这显然不是只追加的，所以如果尝试，我们将抛出错误。

最后，我们指定映射特定的 VMA 标志 - `VM_MAYSHARE` 和文件是可写的 `VM_SHARED`，否则清除 `VM_MAYWRITE` 标志。

* `MAP_PRIVATE` - 如果文件不是以读模式打开，则我们自然报错。与文件挂载在不允许执行的文件系统上的情况不同（通过 `path_noexec()` 检查），如果 `VM_EXEC` 被设置了（由 `PROT_EXEC` 隐含），我们报错，否则清除 `VM_MAYEXEC` 标志。

然后我们执行一个绝对至关重要的检查 - 如果 `struct file->f_op->mmap` 中的 `struct file_operations` 句柄未指定（这必须由文件系统提供），那么该文件不支持内存映射，因此我们必须报错。

Linux 内存管理器（早期访问版）© 2025 Lorenzo Stokes

最后，这部分内存将被映射为堆栈（由 `VM_GROWSDOWN` 暗示），然后我们报错，因为将文件支持的内存映射为堆栈完全没有意义。

在检查了文件支持的逻辑后，让我们考虑列表 5-12 中远简单的匿名映射逻辑：

```c
 } else {
    switch (flags & MAP_TYPE) {
    case MAP_SHARED:
        if (vm_flags & (VM_GROWSDOWN|VM_GROWSUP))
            return -EINVAL;
        /*
         * 忽略 pgoff.
         */
        pgoff = 0;
        vm_flags |= VM_SHARED | VM_MAYSHARE;
        break;
    case MAP_PRIVATE:
        /*
         * 根据 addr 为 anon_vma 设置 pgoff。
         */
        pgoff = addr >> PAGE_SHIFT;
        break;
    default:
        return -EINVAL;
    }
}
```

### 列表 5-12: mmap.c: `do_mmap()` 匿名标志检查

如果映射是共享的，我们检查确保此映射不是堆栈（共享堆栈没有意义）。如果是共享的，我们就会重置由 `pgoff` 指定的映射偏移量，因为匿名映射实际上是通过映射 `/dev/zero` 的 `tmpfs` 副本的已删除 inode 实现的，因此进行偏移操作是有意义的。

我们额外设置了 `VM_SHARED` 和 `VM_MAYSHARE` 来指示这是一个共享映射。

如果映射是私有的，重要的是，我们指定了一个虚拟页偏移（再次忽略用户可能错误指定的任何偏移量）——这简单来说按基页大小位移后的虚拟地址。这对于伪造（forging）很有用，关于如何利用它的更多讨论，请参见反向映射（第 7 章）。
