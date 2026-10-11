
this mm_struct, and it is freed. When the kernel operates on an address space and needs to bump its associated reference count, the kernel increments mm_count. Having two counters enables the kernel to differentiate between the main usage counter (mm_count) and the number of processes using the address space (mm_users).

The mmap and mm_rb fields are different data structures that contain the same thing: all the memory areas in this address space. The former stores them in a linked list, whereas the latter stores them in a red-black tree. A red-black tree is a type of binary tree; like all binary trees, searching for a given element is an O(log n) operation. For further discussion on red-black trees, see "Lists and Trees of Memory Areas," later in this chapter.

Although the kernel would normally avoid the extra baggage of using two data structures to organize the same data, the redundancy comes in handy here. The mmap data structure, as a linked list, allows for simple and efficient traversing of all elements. On the other hand, the mm_rb data structure, as a red-black tree, is more suitable for searching for a given element. Memory areas are discussed in more detail later in this chapter. The kernel isn't duplicating the mm_struct structures; just the containing objects. Overlaying a linked list onto a tree, and using both to access the same set of data, is sometimes called a threaded tree.

All of the mm_struct structures are strung together in a doubly linked list via the mmlist field. The initial element in the list is the init_mm memory descriptor, which describes the address space of the init process. The list is protected from concurrent access via the mmlist_lock, which is defined in kernel/fork.c.

## Allocating a Memory Descriptor

The memory descriptor associated with a given task is stored in the mm field of the task's process descriptor. (The process descriptor is represented by the task_struct structure, defined in <linux/sched.h>.) Thus, current->mm is the current process's memory descriptor. The copy_mm() function copies a parent's memory descriptor to its child during fork(). The mm_struct structure is allocated from the data_cachep slab cache via the allocate_mm() macro in kernel/fork.c. Normally, each process receives a unique mm_struct and thus a unique process address space.

Processes may elect to share their address spaces with their children by means of the CLONE_VM flag to clone(). The process is then called a thread. Recall from Chapter 3, "Process Management," that this is essentially the only difference between normal processes and so-called threads in Linux; the Linux kernel does not otherwise differentiate between them. Threads are regular processes to the kernel that merely share certain resources.

In the case that CLONE_VM is specified, allocate_mm() is not called, and the process's mm field is set to point to the memory descriptor of its parent via this logic in copy_mm():

```c
if (!clone_flags & CLONE_VM) {
    /*
     * current is the parent process and
     * task is the child process during a fork()
     */
    atomic_inc(&current->mm->mm_users);
    task->mm = current->mm;
}
```

### Destroying a Memory Descriptor

When the process associated with a specific address space exits, the exit_mm(), defined in kernel/exit.c, function is invoked. This function performs some housekeeping and updates some statistics. It then calls mmput(), which decrements the memory descriptor's mm_users user counter. If the user count reaches zero, mm_drop() is called to decrement the mm_count usage counter. If that counter is finally zero, the free_mm() macro is invoked to return the mm_struct to the mm_cachep slab cache via kmem_cache_free(), because the memory descriptor does not have any users.

### The mm_struct and Kernel Threads

Kernel threads do not have a process address space and therefore do not have an associated memory descriptor. Thus, the mm field of a kernel thread's process descriptor is NULL. This is the *definition* of a kernel thread—processes that have no user context.

This lack of an address space is fine because kernel threads do not ever access any user-space memory. (Whose would they access?) Because kernel threads do not have any pages in user-space, they do not deserve their own memory descriptor and page tables. (Page tables are discussed later in the chapter.) Despite this, kernel threads need some of the data, such as the page tables, even to access kernel memory. To provide kernel threads the needed data, without wasting memory on a memory descriptor and page tables, or wasting processor cycles to switch to a new address space whenever a kernel thread begins running, kernel threads use the memory descriptor of whatever task ran previously.

Whenever a process is scheduled, the process address space referenced by the process's mm field is loaded. The active_mm field in the process descriptor is then updated to refer to the new address space. Kernel threads do not have an address space and mm is NULL. Therefore, when a kernel thread is scheduled, the kernel notices that mm is NULL and keeps the previous process's address space loaded. The kernel then updates the active_mm field of the kernel thread's process descriptor to refer to the previous process's memory descriptor. The kernel thread can then use the previous process's page tables as needed. Because kernel threads do not access user-space memory, they make use of only the information in the address space pertaining to kernel memory, which is the same for all processes.

## Virtual Memory Areas

The memory area structure, vm_area_struct, represents memory areas. It is defined in <linux/mm_types.h>. In the Linux kernel, memory areas are often called *virtual memory areas* (abbreviated *VMAs*).

The vm_area_struct structure describes a single memory area over a contiguous interval in a given address space. The kernel treats each memory area as a unique memory object. Each memory area possesses certain properties, such as permissions and a set of associated operations. In this manner, each VMA structure can represent different types of memory areas—for example, memory-mapped files or the process's user-space stack. This is similar to the object-oriented approach taken by the VFS layer (see Chapter 13). Here's the structure, with comments added describing each field:

```c
struct vm_area_struct {
    struct mm_struct *vm_mm; /* associated mm_struct */
    unsigned long vm_start; /* VMA start, inclusive */
    unsigned long vm_end; /* VMA end, exclusive */
    struct vm_area_struct *vm_next; /* list of VMA's */
    ppgrot_t vm_page_prot; /* access permissions */
    unsigned long vm_flags; /* flags */
    struct rb_node vm_rb; /* VMA's node in the tree */
    union {
        /* links to address_space->i_mmap or i_mmap_nonlinear */
        struct {
            struct list_head list;
            void *parent;
            struct vm_area_struct *head;
        } vm_set;
        struct prio_tree_node prio_tree_node;
    } shared;
    struct list_head anon_vma_node; /* anon_vma entry */
    struct anon_vma *anon_vma; /* anonymous VMA object */
    struct vm_operations_struct *vm_ops; /* associated ops */
    unsigned long vm_pgoff; /* offset within file */
    struct file *vm_file; /* mapped file, if any */
    void *vm_private_data; /* private data */
};
```

Recall that each memory descriptor is associated with a unique interval in the process's address space. The vm_start field is the initial (lowest) address in the interval, and the vm_end field is the first byte after the final (highest) address in the interval. That is, vm_start is the inclusive start, and vm_end is the exclusive end of the memory interval. Thus, vm_end − vm_start is the length in bytes of the memory area, which exists over the interval [vm_start, vm_end). Intervals in different memory areas in the same address space cannot overlap.

The vm_mm field points to this VMA's associated mm_struct. Note that each VMA is unique to the mm_struct with which it is associated. Therefore, even if two separate processes map the same file into their respective address spaces, each has a unique vm_area_struct to identify its unique memory area. Conversely, two threads that share an address space also share all the vm_area_struct structures therein.
