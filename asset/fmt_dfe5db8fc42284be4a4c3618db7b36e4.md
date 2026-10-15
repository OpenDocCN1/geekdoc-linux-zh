
# Linux 内存管理器（早期访问）

## 反向映射遍历：`page_vma_mapped_walk`

### 结构体定义

`struct page_vma_mapped_walk` 用于遍历页面的反向映射。定义如下（列表 7-43）：

```c
struct page_vma_mapped_walk {
    unsigned long pfn;
    unsigned long nr_pages;
    pgoff_t pgoff;
    struct vm_area_struct *vma;
    unsigned long address;
    pmd_t *pmd;
    pte_t *pte;
    spinlock_t *ptl;
    unsigned int flags;
};
```

**字段说明：**

- **pfn** (必填)：要检查映射的 folio 的页帧号 (PFN)。可通过 `folio_pfn()` 获取。
- **nr_pages** (必填)：从 PFN 开始要遍历的基页数。对于巨页或 `folio_mkclean_range()` 等范围操作，通常为 1。
- **pgoff** (必填)：folio 的偏移量。非巨页时等于 `folio->index`。
- **vma** (必填)：正在遍历其页表映射的 `struct vm_area_struct` (VMA)。
- **address** (必填)：在 VMA 中检查的虚拟地址。通常由 `vma_address()` 确定。
- **pmd** (输出)：指向相关 PMD 条目的指针。
- **pte** (输出)：指向相关 PTE 条目的指针。
- **ptl** (输出)：发现映射后获取的页表锁。
- **flags** (必填，可为 0)：修改遍历行为的标志。
  - `0`：无特殊要求。
  - `PWMW_SYNC`：避免可能导致竞态的同步检查。
  - `PWMW_MIGRATION`：查找迁移条目而非 PTE。

这些参数通常由宏 `DEFINE_FOLIO_VMA_WALK` 初始化（列表 7-44）：

```c
#define DEFAULT_FOLIO_VMA_WALK(name, _folio, _vma, _address, _flags) \
    struct page_vma_mapped_walk name = {                             \
        .pfn       = folio_pfn(_folio),                              \
        .nr_pages  = folio_nr_pages(_folio),                         \
        .pgoff     = folio_pgoff(_folio),                            \
        .vma       = _vma,                                           \
        .address   = _address,                                       \
        .flags     = _flags,                                         \
    }
```

### 核心函数

#### `page_vma_mapped_walk()`

接受 `struct page_vma_mapped_walk *pmw` 参数。若找到有效映射，返回 `true` 并设置 `pmd`、`pte` 及锁定 `ptl`；否则返回 `false` 并释放 `ptl`。

通常在循环中调用以处理各种页面情况。若需提前退出，调用 `page_vma_mapped_walk_done()`。

#### `page_vma_mapped_walk_done()` (列表 7-45)

```c
static inline void page_vma_mapped_walk_done(struct page_vma_mapped_walk *pmw)
{
    /* HugeTLB pte 指向相关的页表条目但不 pte_mapped. */
    if (pmw->pte && !is_vm_hugetlb_page(pmw->vma))
        pte_unmap(pmw->pte);
    if (pmw->pte)
        spin_unlock(pmw->ptl);
}
```

> **注意**：在现代系统中 `pte_unmap()` 为空操作，因此本质上仅释放 PTE 表锁 `ptl`。

#### `page_vma_mapped_walk()` 实现逻辑 (列表 7-46，省略巨页与 devmap 逻辑)

```c
bool page_vma_mapped_walk(struct page_vma_mapped_walk *pmw)
{
    struct vm_area_struct *vma = pmw->vma;
    struct mm_struct *mm = vma->mm;
    unsigned long end;
    unsigned long pfn = pmw->pfn;
    unsigned long nr_pages = pmw->nr_pages;
    pgoff_t pgoff = pmw->pgoff;
    unsigned long address = pmw->address;
    unsigned int flags = pmw->flags;
    pmd_t *pmd = pmw->pmd;
    pte_t *pte = pmw->pte;
    spinlock_t *ptl = pmw->ptl;

    if (unlikely(!vma || !mm || !pfn))
        return false;

    end = vma->vm_end - (pgoff << PAGE_SHIFT);

    while (address < end) {
        pmd = pmd_offset(mm, vma, address);
        if (unlikely(!pmd_present(*pmd)))
            break;

        if (flags & PWMW_SYNC) {
            if (ptl) {
                spin_lock(ptl);
            }
        }

        pte = pte_offset_map(pmd, address);
        if (pte_present(*pte)) {
            pmw->pmd = pmd;
            pmw->pte = pte;
            if (ptl) {
                spin_unlock(ptl);
            }
            return true;
        }

        if (ptl) {
            spin_unlock(ptl);
        }

        address += PAGE_SIZE;
    }

    return false;
}
```

### 辅助函数：`vma_address_end()` (列表 7-48)

```c
unsigned long vma_address_end(struct page_vma_mapped_walk *pvmw)
{
    unsigned long address = pvmw->address + PAGE_SIZE;

    pgoff_t pgoff = pvmw->pgoff + pvmw->nr_pages;
    address = vma->vm_start + ((pgoff - vma->vm_pgoff) << PAGE_SHIFT);
    /* 检查地址是否超出 pvmw 范围（或通过它回绕？） */
    if (address < vma->vm_start || address > vma->vm_end)
        address = vma->vm_end;
    return address;
}
```

对于单页（非巨页），按基页大小返回地址；否则将返回值限制在 VMA 结束地址。

### PTE 映射与检查

#### `map_pte()` (列表 7-49)

```c
static bool map_pte(struct vma_mapped_walk *pvmw)
{
    pvmw->pte = pte_offset_map(pvmw->pmd, pvmw->address);
    if (!(pvmw->flags & PVMW_SYNC)) {
        if (pvmw->flags & PVMW_MIGRATION) {
            // 迁移条目处理逻辑
        } else if (pte_present(*pvmw->pte)) {
            return false;
        }
    }
    pvmw->ptl = pte_lockptr(pvmw->vma->mm, pvmw->pmd);
    spin_lock(pvmw->ptl);
    return true;
}
```

PTE 通过 `pte_offset_map()` 获取，锁通过 `pte_lockptr()` 获取并存入 `ptl`。

#### `check_pte()` (列表 7-50)

```c
/**
 * check_pte - 检查 @pvmw->page 是否已映射到 @pvmw->pte
 * @pvmw: vma_mapped_walk 结构体，包含用于检查的 pte 和 page
 *
 * page_vma_mapped_walk() 发现 @pvmw->page *可能* 映射了。
 * check_pte() 必须验证此点。
 *
 * pvmw->pte 可能指向空 PTE、交换 PTE 或指向任意页的 PTE。
 * 如果设置了 PVMW_MIGRATION 标志，当 @pvmw->pte 包含指向
 * @pvmw->page 或 THP 情况下任意子页的迁移条目时返回 true。
 * 如果未设置 PVMW_MIGRATION 标志，当 pvmw->pte 指向
 * pvmw->page 或 THP 情况下任意子页时返回 true。
 * 否则返回 false。
 */
static bool check_pte(struct vma_mapped_walk *pvmw)
{
    unsigned long pfn;

    if (pvmw->flags & PVMW_MIGRATION) {
        // 迁移条目检查逻辑
    } else if (is_swap_pte(*pvmw->pte)) {
        // 交换条目检查逻辑
    } else {
        if (!pte_present(*pvmw->pte)) {
            return false;
        }

        pfn = pte_pfn(*pvmw->pte);
        return (pfn == pvmw->pfn);
    }
}
```

> 由于本节省略了迁移和交换情况，上述函数逻辑相对简化。

### `page_vma_mapped_walk()` 遍历流程总结

1. 通过 PGD 确定 PGD 条目并确认已设置，否则进入下一个 PGD。
2. 通过 P4D 确定 P4D 条目并确认已设置，否则进入下一个 P4D。
3. 通过 PUD 确定 PUD 条目并确认已设置，否则进入下一个 PUD。
4. 通过 PMD 确定 PMD 条目并确认已设置，否则进入下一个 PMD。
5. 若可映射，通过 PMD 调用 `check_pte()`。
6. 若映射失败，返回 `false`。

### 相关 TLB 操作示例

```c
unmap_vmas(&tlb, vma, start, end);

free_pgtables(&tlb, vma,
              prev ? prev->vm_end : FIRST_USER_ADDRESS,
              next ? next->vm_start : USER_PGTABLES_CEILING);

tlb_finish_mmu(&tlb);
```
