![](bbox=[0.194, 0.118, 0.889, 0.336])

**Figure 5.18** *Locating Pages by Their Vnode/Offset Identity*

`page_find()` locates a page as follows:

+   1. It calculates the slot in the `page_hash` array containing a list of potential pages by using the `PAGE_HASH_FUNC` macro, shown below.

```
```c
#define PAGE_HASHSZ        page_hashsz
#define PAGE_HASHHLEVEL    4
#define PAGE_HASHSHIFT     6
#define PAGE_HASH_FUNC(vp, off) \\
        ((((unsigned long long) (off) >> PAGE_HASHSHIFT) + \\
          ((unsigned long long) (vp) >> PAGE_HASHSHIFT)) & \\
          (PAGE_HASHSZ - 1))
```
```

**Header File** `<vm/page.h>`

+   2. It uses the `PAGE_HASH_SEARCH` macro, shown below, to search the list referenced by the slot for a page matching vnode/offset. The macro traverses the linked list of pages until it finds such a page.

```
```c
int PAGE_HASH_SEARCH(index, pp, vp, off) {
        for (pp = page_hash[index]; ((pp) = ((pp) -> p_hash)) \\
             && !((pp)->p_vnode == (vp) && ((pp)->p_offset == off)) \\
                break; \\
}
```
```

**Header File** `<vm/page.h>`

# 5.7.3 MMU-Specific Page Structures

The defined page structure is the same across different platforms and hence contains no machine-specific structures. We do, however, need to keep machine-specific data about every page, for example, the HAT information that describes how the page is mapped by the MMU. The kernel wraps the machine-independent page structure with a machine-specific page structure, struct machpage. The contents