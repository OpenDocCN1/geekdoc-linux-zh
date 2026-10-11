

08049000 (4 KB)  rw-p (03:03 439029)  /home/slove/src/example
40000000 (84 KB)  r-xp (03:01 80276)  /lib/ld-2.5.1.so
40015000 (4 KB)  rw-p (03:01 80276)  /lib/ld-2.5.1.so
4001e000 (4 KB)  rw-p (00:00 0)  
1bffee00 (8 KB)  rwzp (00:00 0)  [stack]
mapped: 1340 KB  writable/private: 40 KB  shared: 0 KB

前三行是 libc.so（C 库）的文本段、数据段和 bss 段。接下来两行是我们可执行对象的文本段和数据段。随后的三行是 ld.so（动态链接器）的文本段、数据段和 bss 段。最后一行是进程的堆栈。

注意文本段都是可读且可执行的，这正符合我们对目标代码的预期。另一方面，数据段和 bss（两者都包含全局变量）被标记为可读且可写，但不可执行。堆栈当然是可读、可写且可执行的——否则没什么用。

整个地址空间约占 1340KB，但只有 40KB 是可写且私有的。如果内存区域是共享的或不可写的，内核在内存中只保留底层文件的一个副本。对于共享映射，这似乎是常识，但不可写的情况可能让人感到意外。如果你考虑到不可写映射永远不会被更改（映射只被读取），那么将映像仅加载到内存中一次显然是安全的。因此，C 库在物理内存中只需要占用 1212KB，而不是每个使用该库的进程都占用 1212KB。由于该进程可以访问大约 1340KB 的数据和代码，但仅消耗约 40KB 的物理内存，这种共享带来的空间节省是巨大的。

注意那些没有映射到设备 0:00 上 inode 为零的内存区域。这是零页，它是由全零组成的映射。通过将零页映射到可写内存区域上，该区域实际上被“初始化”为全零。这在 bss 中是重要的，因为它提供了预期的已清零内存区域。由于映射不是共享的，一旦进程向这些数据写入，就会制作一份副本（采用写时复制机制），并将值从零更新。

与进程相关的每个内存区域都对应于一个 `vm_area_struct` 结构。因为该进程不是线程，所以它有一个唯一的 `mm_struct` 结构，该结构由其 `task_struct` 引用。

## 操纵内存区域

内核经常需要对内存区域执行操作，例如判断给定地址是否存在于给定 VMA 中。这些操作非常频繁，构成了 `mmap()` 例程的基础，该例程将在下一节中介绍。定义了一组辅助函数来协助这些任务。

这些函数都在 `<linux/mm.h>` 中声明。

### find_vma()

内核提供了一个函数 `find_vma()`，用于查找给定内存地址所在的 VMA。它定义在 `mm/mmap.c` 中：

```c
struct vm_area_struct * find_vma(struct mm_struct *mm, unsigned long addr);
```

此函数在给定地址空间中搜索第一个 `vm_end` 字段大于 `addr` 的内存区域。换句话说，此函数找到包含 `addr` 或起始地址大于 `addr` 的第一个内存区域。如果不存在这样的内存区域，则函数返回 `NULL`。否则，返回指向 `vm_area_struct` 结构体的指针。请注意，由于返回的 VMA 可能从大于 `addr` 的地址开始，因此给定地址并不一定位于返回的 VMA 内部。`find_vma()` 函数的结果缓存在内存描述符的 `mmap_cache` 字段中。由于对一个 VMA 执行操作后紧接着对该相同 VMA 执行更多操作的可能性很大，因此缓存结果具有不错的命中率（实际上约为 30–40%）。检查缓存结果很快。如果给定地址不在缓存中，则必须搜索与该内存描述符关联的内存区域以查找匹配项。这是通过红黑树完成的：

```c
struct vm_area_struct * find_vma(struct mm_struct *mm, unsigned long addr)
{
    struct vm_area_struct *vma = NULL;

    if (mm) {
        vma = mm->mmap_cache;
        if (!( (vma && vma->vm_end > addr && vma->vm_start <= addr)) {
            struct rb_node *rb_node;

            rb_node = mm->mmap.rb_root.rb_node;
            vma = NULL;
            while (rb_node) {
                struct vm_area_struct * vma_tmp;

                vma_tmp = rb_entry(rb_node,
                                    struct vm_area_struct, vm_rb);
                if (vma_tmp->vm_end > addr) {
                    vma = vma_tmp;
                    if (vma_tmp->vm_start <= addr)
                        break;
                    rb_node = rb_node->rb_left;
                } else
                    rb_node = rb_node->rb_right;
            }
        }
        if (vma)
            mm->mmap_cache = vma;
    }
    return vma;
}
```

对 `mmap_cache` 的初始检查测试缓存的 VMA 是否包含所需的地址。请注意，仅检查 VMA 的 `vm_end` 字段是否大于 `addr` 并不能确保这是大于 `addr` 的第一个此类 VMA。因此，为了使缓存在此处有用，给定的 `addr` 必须位于 VMA 内部——幸运的是，这正是在对同一 VMA 执行连续操作时会出现的情景。

如果缓存中不包含所需的 VMA，则函数必须搜索红黑树。如果当前 VMA 的 `vm_end` 大于 `addr`，则函数遵循左子节点；否则，遵循右子节点。一旦找到包含 `addr` 的 VMA，函数就会终止。如果未找到这样的 VMA，函数将继续遍历树，并返回它找到的第一个起始位置在 `addr` 之后的 VMA。如果从未找到 VMA，则返回 `NULL`。

### find_vma_prev()

`find_vma_prev()` 函数的工作方式与 `find_vma()` 相同，但它还返回 `addr` 之前的最后一个 VMA。该函数也定义在 `mm/mmap.c` 中，并在 `<linux/mm.h>` 中声明：

```c
struct vm_area_struct * find_vma_prev(struct mm_struct *mm, unsigned long addr,
                                       struct vm_area_struct **prev);
```

`prev` 参数存储指向 `addr` 之前 VMA 的指针。

### find_vma_intersection()

`find_vma_intersection()` 函数返回与给定地址区间重叠的第一个 VMA。该函数定义在 `<linux/mm.h>` 中，因为它是内联的：

```c
static inline struct vm_area_struct *
find_vma_intersection(struct mm_struct *mm,
                      unsigned long start_addr,
                      unsigned long end_addr)
{
    struct vm_area_struct *vma;

    vma = find_vma(mm, start_addr);
    if (vma && end_addr <= vma->vm_start)
        vma = NULL;
    return vma;
}
```

第一个参数是要搜索的地址空间，`start_addr` 是区间的起始位置，`end_addr` 是区间的结束位置。

显然，如果 `find_vma()` 返回 `NULL`，那么 `find_vma_intersection()` 也会返回 `NULL`。然而，如果 `find_vma()` 返回一个有效的 VMA，那么 `find_vma_intersection()` 仅当该 VMA 没有从给定地址范围结束之后的位置开始时，才返回相同的 VMA。如果返回的内存区域确实从给定地址范围结束之后的位置开始，则函数返回 `NULL`。

## mmap() 和 do_mmap()：创建地址区间

`do_mmap()` 函数用于内核创建新的线性地址区间。说该函数创建一个新的 VMA 在技术上并不完全准确，因为如果创建的地址区间与现有的地址区间相邻，并且它们共享相同的权限，则这两个区间将合并为一个。如果这不可能，则创建一个新的 VMA。无论如何，`do_mmap()` 是将地址区间添加到进程地址空间的函数——无论是扩展现有内存区域还是创建新区域。

`do_mmap()` 函数在 `<linux/mm.h>` 中声明：

```c
unsigned long do_mmap(struct file *file, unsigned long addr,
            unsigned long len, unsigned long prot,
            unsigned long flag, unsigned long offset)
```

此函数将 `file` 指定的文件映射在偏移量 `offset` 处，长度为 `len`。`file` 参数可以为 `NULL`，且 `offset` 可以为零，在这种情况下，映射将没有底层文件支持。在这种情况下，这被称为*匿名映射*。如果提供了文件和偏移量，则该映射被称为*文件映射*。

`addr` 参数可选地指定开始搜索空闲区间的初始地址。

`prot` 参数指定内存区域中页面的访问权限。可能的权限标志定义在 `<asm/mman.h>` 中，并且对每个支持的架构都是独特的，尽管在实践中，每个架构都定义了表 15.2 中列出的标志。

| 标志 | 对新区间内页面的影响 |
| :--- | :--- |
| PROT_READ | 对应 VM_READ |
| PROT_WRITE | 对应 VM_WRITE |
| PROT_EXEC | 对应 VM_EXEC |
| PROT_NONE | 无法访问页面 |

