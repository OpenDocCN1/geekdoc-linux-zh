# # Virtual Memory

**Sysctl Prefix:** `vm`

**/proc Prefix:** `/proc/sys/vm/`

| Parameter | Description |
|---|---|
| `max_map_count` | Maximum number of memory map areas per process |
| `max-readahead` | Maximum I/O read-ahead size |
| `min-readahead` | Minimum I/O read-ahead size |
| `vm.heap-stack-gap` | Enforces a gap between heap and stack |

The `vm.heap-stack-gap` parameter allows a gap to be enforced between the heap and the stack. Any access to memory in the gap area causes a segmentation fault. This action avoids silent corruption that could occur when allocating on stack runs over the heap. The gap enforced is in number of pages.

| Parameter | Description |
|---|---|
| `pagetable_cache` | Cache size per processor for page tables |

The `pagetable_cache` parameter specifies low and high cache size per processor to be used for page tables. On SMP systems, this parameter allows the system to do fast pagetable allocations without having to acquire the kernel memory lock. On a single-CPU system, these values can be set to 0 to avoid wasting memory.

| Parameter | Description |
|---|---|