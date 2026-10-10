This leads us to the following kernel memory zones:

+   1.  `ZONE_DMA` (<16MB), the zone used for *Direct Memory Access* (DMA). Because legacy ISA devices have 24 address lines and can access only the first 16MB, the kernel tries to dedicate this area for such devices.
+   2.  `ZONE_NORMAL` (16MB to 896MB), the normally addressable region, also called low memory. The "virtual" field in `struct page` for low memory pages contains the corresponding logical addresses.
+   3.  `ZONE_HIGH` (>896MB), the space that the kernel can access only after mapping resident pages to regions in `ZONE_NORMAL` (using `kmap()` and `kunmap()`). The corresponding kernel addresses are virtual and not logical. The "virtual" field in `struct page` for high memory pages points to `NULL` if the page is not kmapped.

`kmalloc()` is a memory-allocation function that returns contiguous memory from `ZONE_NORMAL`. The prototype is as follows:

```
```c
void *kmalloc(int count, int flags);
```
```

Where `count` is the number of bytes to allocate, and `flags` is a mode specifier. All supported flags are listed in *include/linux/gfp.h* (gfp stands for *get free pages*), but these are the commonly used ones:

+   1.  `GFP_KERNEL` Used by process context code to allocate memory. If this flag is specified, `kmalloc()` is allowed to go to sleep and wait for pages to get freed up.
+   2.  `GFP_ATOMIC` Used by interrupt context code to get hold of memory. In this mode, `kmalloc()` is not allowed to sleep-wait for free pages, so the probability of successful allocation with `GFP_ATOMIC` is lower than with `GFP_KERNEL`.

Because memory returned by `kmalloc()` retains the contents from its previous incarnation, there could be a security risk if it’s exposed to user space. To get zeroed kmalloced memory, use `kzalloc()`.

If you need to allocate large memory buffers, and you don’t require the memory to be physically contiguous, use `vmalloc()` rather than `kmalloc()`:

```
```c
void *vmalloc(unsigned long count);
```
```

Here `count` is the requested allocation size. The function returns kernel virtual addresses.

`vmalloc()` enjoys bigger allocation size limits than `kmalloc()` but is slower and can’t be called from interrupt context. Moreover, you cannot use the physically discontinuous memory returned by `vmalloc()` to perform *Direct Memory Access* (DMA). High-performance network drivers commonly use `vmalloc()` to allocate large descriptor rings when the device is opened.

The kernel offers more sophisticated memory allocation techniques. These include *look aside buffers*, *slabs*, and *memory pools*, which are beyond the scope of this chapter.