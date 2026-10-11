
| **Flag** | **Description** |
| :--- | :--- |
| WA_READ | Read access |
| WA_WRITE | Write access |
| WA_EXEC | Execution access |
| WA_TRAPAF TER | Trap after the instruction completes |

When a watchpoint is triggered, a traced process makes a memory reference that covers at least one byte of a watched area and the memory reference that covers a bit mask is as specified in pr_wflags. When a watchpoint is triggered, it triggers a watchpoint trap. The trap occurs before the instruction completes unless WA_trapafter was specified. If WA_trapafter was specified, the trap will occur after the instruction completes. When the trap occurs before completion, the memory is not modified. If it occurs after completion, the memory is modified if the access permission is a write access. The /proc process information file, pr_info, contains information pertinent to the watchpoint trap and can be read into a struct pr_info. The s1_addr field contains the virtual address of the memory reference that triggers the watchpoint.

## Pages

Pages are units of physical memory. Active pages in the kernel are mappings between a vnode and memory. A page can be identified with a vnode pointer and the page size offset within the vnode, or the vnode/offset pair, which is the backing store for the page and represents the file and offset that the page is mapping. The HAT and address space layers manage the mapping between the physical page and its virtual address space. The vnode/offset pair is reusable by other tasks because it synchronizes its contents in RAM with its backing store before reuse. A global hash list is an array of pointers to linked lists of pages. The virtual memory system hashes pages with a valid vnode/offset pair onto a global hash list so that they can be located by vnode and offset. There are three functions that search the global hash list: page_find(), page_lookup(), and page_lookup_nowait(). These functions use vnode and offset as arguments and return a pointer to a page structure if it finds one.

The Solaris kernel also uses a segmented global physical page list. This is made up of segments in contiguous physical memory. These segments are added during the system boot. They are also added and deleted dynamically when physical memory is added or removed while the system is running. A free list and cache list hold pages that are not mapped into any address space and have been freed by page\_free(). Although they may be reported as free pages by vmstat, they can still contain a valid page from a vnode/offset and are still part of the global page cache. Caching pages can appear on the free list. Memory on the cache list is not really free either, but it is a valid cache of a page from a file. The cache list demonstrates how the file systems use memory as a file system cache.

If a page has been destroyed and removed from a vnode\'s hash list, it will appear on the free list. The free list is usually small because most pages used by a process still keep their vnode/offset information intact. When a process exits, pages are put on the free list. This frees anonymous memory pages such as heap, stack, and copy-on-write pages.

Page sizes may vary depending upon the hardware. The Solaris kernel uses a page size that is usually 8KB. The MMU page size causes somewhat of a trade-off of performance and memory size efficiency. A larger page gives better performance because of less memory management overhead, but a smaller page size wastes less memory.

Solaris 8 controls many page-related activities with the use of algorithms. Although there are too many to delve into, suffice it to say that algorithms to fine-tune the page coloring, page scanner page-out, and scan rate operations are all as efficient as any operating system can make them. Shared libraries have been optimized to prevent stolen pages. Demand paging allows the file system cache to grow and shrink as required by "stealing pages" not recently used by other subsystems. Solaris 8 is capable of sustaining much higher I/O rates because of this. Memory is conserved through various means. The CPU scheduler/dispatcher can swap out entire processes to conserve memory.

## POSIX

Portable Operating System Interface (POSIX) standards are used with Solaris 8. They were implemented with the System V IPC (Interprocess Communication) set: shared memory, semaphores, and message queues. The implementation in Solaris 8 is different from that in System V. The POSIX name convention provides abstraction, as well as a file descriptor to enable the use of the file memory mapping interface, mmap(2), on which all the POSIX IPC mechanisms are built. The IPC facilities need not be files in a file system, but they must look like they are. The old key values used by System V have been done away with in Solaris 8. With POSIX, the processes acquire the desired resource by using filename conventions. The POSIX interfaces require linking with the libposix4 .20 shared object library when running code that uses any POSIX IPC facilities on Solaris.

All of the POSIX IPC functions are directly or indirectly based on memory-mapped files. The message queue and semaphore functions make direct calls to the mmap(2). This creates a memory-mapped file based on the file descriptor returned from the xs\_open(3R) call. If you use the POSIX shared memory, you must make the mmap(2) call from the application code. The mmap(2) system call maps a file directly from the code.

## Summary

In this chapter, you learned how Solaris 8 was developed. Multics, which was developed by AT&T and designed for an in-house system, was the grandparent of Solaris 8. Solaris 8 has been refined and the operating environment includes all of the tools, applications, and services that make use of SunOS, the Sun Operating System. The C programming language, which was written specifically for the Unix system, is used by Solaris 8.

Solaris 8 employs the modular or layered design made popular by Unix. Sun developed a new operating system kernel, which is used by Solaris today. Solaris 8 uses multiple threads of execution. The hierarchical structure of Solaris 8 is followed through each module of the operating system, making for a uniform structure. Buses and devices can be installed and configured by dynamically loadable devices and bus drivers.

This chapter also covered schedulers. You learned that each scheduler has its own algorithms and priority levels to optimize operations and that the virtual file system framework implements multiple file system types. The proc file system provides all programs with a uniform interface into the kernel. Solaris recognizes two distinct processor execution modes: a privileged mode called kernel mode and a nonprivileged mode called user mode.

In addition to schedulers, this chapter covered interrupts and traps. An interrupt is a signal that a device sends to the kernel indicating that something needs immediate attention. The kernel can send an interrupt to another processor when required. A trap is a vectored transfer of control into the kernel initiated by the processor. Software traps are used for system calls in the Solaris kernel.

This chapter also showed how Solaris employs shared memory architecture, which implements a single kernel shared by all processors and a single memory address space. You read how data threads are prioritized and high-priority threads can interrupt lower-priority threads upon execution and how the virtual memory system provides a programming model with larger size.

Finally, you learned that memory is managed by page size rather than by bytes.

# CHAPTER **3**

# **Installing Solaris 8**

+   **FEATURING:**
+   *   *The different Solaris distributions* 62
+   *   *The SPARC installation* 71
+   *   *Solaris on Intel installation* 83
+   *   *StarOffice and additional component installations* 85
+   *   *Patches* 87

![](img/256e02a6afce528d264a8d911fa0ff20_81_0.png)
