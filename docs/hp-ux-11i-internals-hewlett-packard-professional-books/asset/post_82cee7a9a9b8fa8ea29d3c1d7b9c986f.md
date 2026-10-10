
# Calling exec() Immediately After vfork()

In the `vfork()` / `exec()` case (where `vfork_state = VFORK_CHILD_RUN`), we first need to request the creation of a new uarea for the thread along with minimal vareas, pre region, and region structures. Next, the content of the parent’s uarea (the one we are currently using) is copied to the new one, and another routine is called to switch the thread’s execution trace to the new uarea and kernel stack.

The `vfork_state` is changed to `VFORK_CHILD_EXIT`, and we initiate the cleanup of the parent’s context. Once the parent uarea and stack have been restored, the parent wakes up and releases the `vfork_info` buffer as it resumes.

# Calling exec() after a fork()

Following a call to `fork()`, the newly created child has vareas, pre regions, private and shared regions, and an initial thread and uarea. In this case `getxfile()` must dispose of most of the existing pre regions and regions. This function is performed by the kernel procedure `dispreg()`. Figure 9-5 shows the state of a process’s memory view after the disposition of its old image.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_296_0.png)

# Removing pre regions, regions, and b-trees

The first step in removing pre regions, regions, and b-trees is to acquire a write lock for the process and terminate any existing sibling threads. Next, we walk the pre region list and dispose of all except our thread's `p_type=PT_UAREA`. If we are attempting to perform an `exec_self` (defined as a process attempting to execute itself with another copy of the same program image), we also save the `p_type=PT_TEXT` and `p_type=PT_NULLDREF` pre region/region to save time when we reconstruct the new logical view.

Disposing of a pre region involves several steps. First, it must be removed from the active list. If vhand's `agenda` or `sealand` are currently pointing to it, we move to `p_next` so vhand won't waste time. Next, we follow the `p_reg` pointer to its associated region structure.

If we are the last pre region to reference the region (`r_refcnt=1`), we schedule its cleanup (if others are still referencing an `RT_SHARED` region, we simply decrement its `r_refcnt`). After dealing with the region, each pre region structure is also freed and returned to the kernel memory arenas.

The actual cleanup of a region requires that we wait for any pending I/O operations to its pages to complete. We then walk the b-tree and delete all virtual address translations, purging them from the processor TLBs and freeing the associated `pd_dir` entries. If the virtual-to-physical `pde` was allocated from an alias or sparse `pd_dir` entry, it is returned to the appropriate free list. If it was located in a machine-visible hashable, it is simply marked as invalid (`pde_valid` is cleared). If this is the only virtual reference to a physical page (`pf_use=1` in the page's `pfd`), we must free the physical page and adjust the system's available page count. `freemem` (if any process threads are currently blocked, waiting on a memory page, we wake them). The page entry in `pdat_ptr` and `virt_to_virt_ptr` is updated, and appropriate adjustments to the swap reservation and allocation structures are also made.

Finally, we release any reserved or allocated swap and physical pages used to hold the region's `pgs` list (the pages needed to hold the b-tree nodes and chunks). The region is unlinked from the forward and backward pointers to the systemwide region list, and we return its structure to the kernel memory arena.

### Building the New Logical View

At this point, regardless of which path we followed, `getxfile()` sets up the new logical view and maps it within the system's virtual address space (see Figure 9-6). To take stock, we have a new `proc` and `kthread` structure and a minimal `proc` with `a urea`.

The `exec` routine opens the program file and passes its `vnode` to `getxfile()` along with its attributes and load-specific information from the header. If the program file is a text file, the `vnode` points to the executable image of the interpreter program, which is to be run to process the script.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_298_0.png)

Figure 9-6 getxfile() Rebuilds the Memory View

Now it’s finally time to build the new image map! The compiler magic type tells us what type of mapping (`DEMAND_MAGIC`, `EXEC_MAGIC`, `SHMEM_MAGIC`, `SHARE_MAGIC`) to use as we locate the regions in quadrants. First, the null dereference and text regions are configured and mapped (if we are doing an `exec` self, then these regions will have been retained). Private regions for data (initialized, BSS, and heap) and user stack are added next. Additional regions are added as required for shared memory objects and memory-mapped files (both private and shared varieties).

The transformation is now complete, and we return from the `exec()` call wearing our new image and ready to run its code. Before we examine the final call in a process’s life cycle, `exit()`, let’s take a closer look at the way shared memory objects are mapped into the system’s virtual space and attached to a process’s logical view.

# Shared Memory Objects Revisited

When a program filename is passed to `exec()`, it must find the file (also called the front store) and open it. If the file is already open, there will be an existing `vnode` for the file in the kernel memory. If not, a new `vnode`, pseudo `varea`, a single `pre_region`, and a `region` are created, as illustrated in Figure 9-7. In most cases, a `varea` structure is pointed to by a `proc` structure (`p_vas`), but in the case of an executable or memory-mapped file, it is a `vnode` (`v_vas`) that references it. In turn, the `varea` (`va_fp`) points back to the `vnode` for which it was created.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_299_0.png)

When a process needs to attach a text region or a memory-mapped file to its virtual view, it simply copies the file's `region` structure and increments the associated `region` reference count.

# Shared Memory, System-V, and POSIX

In a very similar manner, System-V shared memory regions are also maintained by first allocating an entry from the system’s shared memory descriptor table, `shmem[]`. An active table entry points to a pseudo `varea`, `pre_region`, and `region` created to manage the shared memory space (see Figure 9-8). The System-V shared memory allocation, attach, detach, and deallocation requests are mapped through this table and its related structures.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_300_0.png)

Figure 9-8 Shared Memory Objects

The following kernel-tunable parameters are used to size and configure System-V shared memory capabilities.

- **shmni** sets the maximum number of shared memory regions the kernel may manage.
- **shmmax** sets the maximum size in bytes for a shared memory region.
- **shms** sets the maximum number of shared memory regions a single process may attach to its virtual view at one time.

System-V shared memory regions are managed as independent kernel resources; that is, they may continue to exist even if there are no current processes attached to them. If a programmer decides to use shared memory regions, he or she is responsible for their allocation and eventual cleanup. The administrative commands **ipcs** and **ipcrm** may be used to check the status of shared memory regions and, if necessary, to remove them from the system.

Note that some programmatic schemes involve creating a shared memory region and having it persist as various daemons or agents are launched and momentarily attach to and detach from it. In a production environment, just because a shared memory region has no processes currently attached does not necessarily mean that you should remove it!

The POSIX system definition also has a set of shared memory calls. The calls are implemented on HP-UX as shared memory mapped files. Programmers are encouraged to use the System-V shared memory calls over the POSIX calls, but both will function.
