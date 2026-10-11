# find_vma()

The kernel provides a function, find_vma(), for searching for the VMA in which a given memory address resides. It is defined in mm/mmap.c:

```
```c
struct vm_area_struct * find_vma(struct mm_struct *mm, unsigned long addr);
```
```

This function searches the given address space for the first memory area whose vm_end field is greater than addr. In other words, this function finds the first memory area that contains addr or begins at an address greater than addr. If no such memory area exists, the function returns NULL. Otherwise, a pointer to the vm_area_struct structure is returned. Note that because the returned VMA may start at an address greater than addr, the given address does not necessarily lie inside the returned VMA. The result of the find_vma() function is cached in the mmap_cache field of the memory descriptor. Because of the probability of an operation on one VMA being followed by more operations on that same VMA, the cached results have a decent hit rate (about 30–40% in practice). Checking the cached result is quick. If the given address is not in the cache, you must search the memory areas associated with this memory descriptor for a match. This is done via the red-black tree:

```
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
        } if (vma)
            mm->mmap_cache = vma;
    }
}
```
```