| **Flag** | **Description** |
| :--- | :--- |
| WA_READ | Read access |
| WA_WRITE | Write access |
| WA_EXEC | Excecution access |
| WA_TRAPAF TER | Trap after the instruction completes |

When a watchpoint is triggered, a traced process makes a memory reference that covers at least one byte of a watched area and the memory reference that covers a bit mask is as specified in pr_wflags. When a watchpoint is triggered, it triggers a watchpoint trap. The trap occurs before the instruction completes unless WA_trapafter was specified. If WA_trapafter was specified, the trap will occur after the instruction completes. When the trap occurs before completion, the memory is not modified. If it occurs after completion, the memory is modified if the access permission is a write access. The /proc process information file, pr_info, contains information pertinent to the watchpoint trap and can be read into a struct pr_info. The s1_addr field contains the virtual address of the memory reference that triggers the watchpoint.

# Pages

Pages are units of physical memory. Active pages in the kernel are mappings between a vnode and memory. A page can be identified with a vnode pointer and the page size offset within the vnode, or the vnode/offset pair, which is the backing store for the page and represents the file and offset that the page is mapping. The HAT and address space layers manage the mapping between the physical page and its virtual address space. The vnode/offset pair is reusable by other tasks because it synchronizes its contents in RAM with its backing store before reuse. A global hash list is an array of pointers to linked lists of pages. The virtual memory system hashes pages with a valid vnode/offset pair onto a global hash list so that they can be located by vnode and offset. There are three functions that search the global hash list: page_find(), page_lookup(), and page_lookup_nowait(). These functions use vnode and offset as arguments and return a pointer to a page structure if it finds one.

The Solaris kernel also uses a segmented global physical page list. This is made up of segments in contiguous physical memory. These segments are added during the system boot. They are also added and deleted dynamically when physical memory is added or removed while the system is running. A free list and cache list hold pages