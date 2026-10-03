
# VMA 合并与调整

## 5.1.1 VMA 合并逻辑

注意，该函数的调用者将持有 `struct mm_struct->mmap_lock` 的写锁。该函数的调用者保证由 `addr` 和 `end` 指定的地址范围符合以下标准之一：

- `addr` 将跨越一个空洞，即未映射的内存（如果可以合并，这将是情况 1-3 之一）。
- `addr` 将跨越 `prev` 的部分（如果 `end` 等于 `prev->end`，那么如果另一个 VMA 紧邻相接，则可能适用情况 4）。
- 在所有其他情况下，`addr` 将等于 `area->vm_start`（如果可以合并，这将是情况 5-8 之一）。

我们使用 `vma_next()` 获取 `prev` 之后的 VMA。如果 `prev` 为 NULL，则输入内存范围跨越了地址空间中的第一个 VMA 或第一个 VMA 之前的内存，此时它直接通过 `mm_struct->mmap` 获取第一个 VMA。

我们将 `addr` 分配给该 VMA，只有当 `addr` 和 `end` 跨越了整个 VMA 时，才会更新 `next` 指向其之后的 VMA（情况 6-8）。

最后，在检查可合并性之前，我们评估了一些基础情况——如果输入的 `addr` 起于 `prev` 之前、在 `end->vm_end` 之后且不代表有效的内存范围，那么发生了严重的错误。

我们首先检查是否可以与 `prev` 合并——这涵盖了情况 1, 2, 5-7。`prev` 的通用合并性由 `mpol_equal()` 决定，它判断内存策略是否相等（内存策略见 NUMA 章节），并将其他可合并性检查推迟到 `can_vma_merge_after()`。

我们通过检查 `next` 是否可合并来区分情况 1 和 6（`prev` 和 `next` 都已合并）以及所有其他情况，这次是通过 `can_vma_merge_before()` 进行。

区别在于，`prev` 和 `next` 之间的 `anon_vma` 合并性是通过 `is_mergeable_anon_vma()` 检查的。我们将详细检查该函数（你可以在第 7 章阅读关于 `anon_vma` 对象和反向映射的内容），但在 `prev` 和 `next` 都确定与输入地址范围合并时，这是唯一无法保证的标准。

最后，合并的核心工作被推迟到 `vma_adjust()`。我们也将检查该函数及其参数化。

内存映射 321

如果在调整时发生错误，我们返回 NULL 表示无法合并，由于我们将地址范围折叠到了 `prev` 中，我们返回这个合并后的 VMA。

让我们查看列表 5-33 所示无法与 `prev` 合并的情况。

```c
/*
 * 这个新请求可以合并到 next 之前吗？ */
if (next->start && end == next->vm_end &&
    mpol_equal(policy, vm_policy_before(next)) &&
    can_vma_merge_before(next, vm_flags,
        anon_vma, file, pgoff+pglen,
        vm_userfaultfd_ctx, anon_name)) {
    if (prev && addr < prev->vm_end) /* 情况 4 */
        err = __vma_adjust(prev, prev->vm_start,
            addr, prev->vm_goff, NULL, next);
    else { /* 情况 3, 8 */
        err = __vma_adjust(area, next->vm_end,
            next->vm_goff - pglen, next);
        /*
         * 在情况 3 下 area 已经等于 next
         * 这是一个空操作，但在情况 8 中 "area"
         * 被移除并由 next 扩展。
         */
        area = next;
    }
    if (err)
        return NULL;
    khugepaged_enter_vm(area, vm_flags);
    return area;
}
return NULL;
```

列表 5-33: mm/map.c: vma_merge() 后继合并

我们首先通过上方式检查是否可以与 `next` 合并——如果没有合并则返回 NULL。

否则，我们检查地址范围是否跨越了 `prev` 的末尾（情况 4），此时我们返回与 `next` 合并的 `area`，完成了从 `prev` 末尾切出的新 VMA。否则，在情况 3 下，我们已经将 `area` 分配给 `next` 并调整 `next` 以包裹它，因此两种情况下返回 `next`。

第 5 章 322

## 5.1.2 可合并性

在两种情况下，我们都在 `__vma_adjust()` 中执行核心工作，我们在 5.1 节中检查它。一旦确定 VM 是相邻的，我们在检查候选 VMA 是否能合并 `prev` 时，通过 `can_vma_merge_after()` 判断是否与另一个合并；在检查候选 VMA 是否能合并 `next` 时，通过 `can_vma_merge_before()` 判断，如列表 5-34 所示。

```c
/*
 * 如果可以将 (vm_flags,anon_vma,file,vm_goff)
 * 合并到 vma 之后（更高的虚拟地址和文件偏移量）。
 * 如果两个 vmas 拥有不同的（非空）anon_vmas，
 * 或者 anon_vma 的偏移量分配不兼容，则我们无法合并。
 */
static int
can_vma_merge_after(struct vm_area_struct *vma, unsigned long vm_flags,
	struct anon_vma *anon_vma, struct file *file,
	pgoff_t vm_goff,
	struct userfaultfd_ctx *userfaultfd_ctx) {
	if (is_mergeable_vma(vma, file, vm_flags, userfaultfd_ctx,
		anon_name) &&
		is_mergeable_anon_vma(anon_vma, vma->anon_vma)) {
		pgoff_t pglen;
		pglen = vm_pages(vma);
		if (vma->vm_goff + pglen == vm_goff)
			return 1;
	}
}
```

列表 5-34: mm/map.c: can_vma_merge_after()

这把核心工作推迟给了辅助函数 `is_mergeable_vma()` 和 `is_mergeable_anon_vma()`，我们稍后将检查。除了这些检查之外，我们还执行最后的检查——候选 VMA 的虚拟页偏移必须等于上一个（作为 `vma` 传入）的偏移。`can_vma_merge_before()` 类似，但是一个简化的 `vm_goff` 检查，因为我们只检查列表 5-35 所示的相等性。

```c
/*
 * 如果可以将 (vm_flags,anon_vma,file,vm_goff)
 * 合并到 vma 之前（较低的虚拟地址和文件偏移）。
 * 如果两个 vmas 拥有不同的（非空）anon_vmas，
 * 或者 anon_vma 的偏移量分配不兼容，则我们无法合并。
 */
static int
can_vma_merge_before(struct vm_area_struct *vma, unsigned long vm_flags,
	struct anon_vma *anon_vma, struct file *file,
	pgoff_t *vm_goff,
	struct vm_userfaultfd_ctx *userfaultfd_ctx,
	struct anon_vma_name *anon_name) {
	if (is_mergeable_vma(vma, file, flags, userfaultfd_ctx,
	anon_name) &&
	is_mergeable_anon_vma(anon_vma, vma->anon_vma)) {
		if (vma->vm_goff == *vm_goff)
		return 1;
	}
}
```

列表 5-35: mm/mmap.c: can_vma_merge_before()

VMA 的合并性根本上由 `is_mergeable_vma()` 函数决定，如列表 5-36 所示。

```c
/*
* 如果 vma 有 ->close 操作，那么驱动程序可能需要释放
* 每-vma 资源，因此我们不尝试合并那些。
*/
static inline int is_mergeable(struct vm_area_struct *vma,
	struct file *file, unsigned long vm_flags,
	struct vm_userfaultfd_ctx *vm_userfaultfd_ctx,
	struct anon_vma_name *anon_name) {
	/*
* VM_SOFTDIRTY 应该防止 VMA 合并，如果我们
* 匹配标志但防止了脏位——调用者应该标记
* 合后的 VMA 为脏。如果脏位不从比较中
* 排除，我们将增加内存系统的压力，迫使内核
* 在可以扩展时生成新的 VMA。
*/
	if ((vma->vm_flags ^ vm_flags) & ~VM_SOFTDIRTY)
      return 0;
	if (vma->vm_file != file)
      return 0;
	if (vma->vm_ops && vm_ops->close)
      return 0;
	if (!is_mergeable_vm_userfaultfd_ctx(vma, vm_userfaultfd_ctx))
      return 0;
	if (!anon_vma_name_eq(anon_vma_name(anon), anon_name))
      return 0;
      return 1;
}
```

列表 5-36: mm/mmap.c: is_mergeable_vma()

请注意，此检查本质上是在确定两个 VMA 是否实际上完全相同的。我们在每个 VMA 中维护此状态，以便能够使用尽可能少的空间描述虚拟内存范围，这就是为什么我们首先要合并 VMA 的原因。

检查所有这些标准（超出范围的 userfault 处理除外）：

1. `vm_flags` 必须排除 `VM_SOFTDIRTY` 之外，正如注释描述，不值得为了将其作为相同 VMA 基础并将它们分离而增加额外的内存压力。例如，在最初通过 `mmap_region()` 或 `do_brk_flags()` 映射内存时，`VM_SOFTDIRTY` 标志是被无条件设置的，因此该标志被正确维护。
2. `vm_file` – 如果有文件支持，则 VMA 必须由同一个文件支持。
3. `vm_ops->close` – 如果提供了 VMA 操作（即为非匿名映射），则 `close()` 处理程序的存在意味着（正如注释所示），实现此点的驱动程序具有不同的每个 VMA 状态，因此合并是不安全的。
4. `anon_vma_name` – 当区域用于特定用途时，匿名 VMA 可以被特定命名，例如：栈、堆（在 `/proc/pid/maps` 和 `/proc/pid/maps` 中用方括号显示）。自然，如果名称不同，匿名 VMA 之间是不可合并的。

最后，我们有特定的处理方法来确保与每个 VMA 关联的反映射结构体 `anon_vma` 对象（见第 7 章）是等价，通过 `is_mergeable_anon_vma()`（见列表 7-19）。这在反映射章节 7.0.11 中进行了详细讨论。

## 5.1.3 VMA 调整

`__vma_adjust()` 函数的参数化如表 5-1 所示。

### 表 5-1: __vma_adjust() 参数

| 参数 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| vma | prev | next | Case | | | | area |
| start end | prev->vma_start next->vma_end | next->addr addr | prev->vma_start next->vma_end area->vm | next->vma_end | | | | |
| pgoff | | | * | | | | | | |
| insert | | | | NULL | | | | | |
| expand | | | | | | | next | | |
| * next->vma_pgoff - (end - addr) >> PAGE_SHIFT | | | | | | | | | |

检查每个参数：

- `vma` - 将被调整并成为合并 VMA 的 VMA。
- `start` - 新合并映射将开始的地址（即合并后 VMA 的 `vm_start`）。
- `end` - 新合并映射的排他边界（即合并后 VMA 的 `vm_end`）。
- `pgoff` - 合并后 VMA 的 `vm_pgoff`。
- `insert` - 要插入的 VMA。在合并逻辑中未使用。
- `expand` - 为了获得合并后的 VMA 而需要扩展（向前或向后）的 VMA。

`__vma_adjust()` 函数非常庞大，因此让我们逐部分查看（省略超出范围的用途和对大页的处理）。

我们首先确定在不插入 VMA 的情况下（即合并情况），对跟随 `vma` 之后的 VMA 执行什么。让我们先看一眼代码，然后我们将尽可能尝试并如列表 5-37 所示对其进行拆解。

```c
/*
* 我们无法在不调整树的情况下，调整已经存在于 inmap tree
* 中的 vma 的 vm_start, vm_end, vm_pgoff 字段。
* 当需要此类调整时，应使用以下辅助函数。
* "insert"（如果有）将在我们丢弃必要的
* 锁之前进行插入。
*/
int _vma_adjust(struct vma_area_struct *vma, unsigned long start,
    unsigned long end, pgoff_t pgoff, struct vma_area_struct *insert,
    struct vma_area_struct *expand)
{
    struct mm_struct *mm = vma->vm->mm;
    struct vma_area_struct *next = vma->vm_next, orig_vma = vma;
    struct address_space *mapping = NULL;
    struct rb_root_cached *root = NULL;
    struct anon_vma *anon_vma = NULL;
```
