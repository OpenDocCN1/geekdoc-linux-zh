the first thread in the pidhash. Linux threads don’t use CLONE_PID so there is no such problem if you are using the pthreads.h thread API.

When a signal is sent to a user task, for example when a user-space program accesses an illegal page, the following happens:

+   1.  page_fault( entry.S) —Low-level pagefault handler.
+   2.  do_page_fault() (fault.c) —Fetches i386-specific parameters of the fault and does basic validation of the memory range involved.
+   3.  handle_mm_fault() (memory.c) —Generic MM code (i386-independent), gets called. The MM reads the page table entry and uses the VMA to find out whether the memory access is legal.

The following case details an illegal access—a write was attempted to a read-only mapping. handle_mm_fault() returns 0 to do_page_fault() in this case:

```
```
{
    int fault = handle_mm_fault (tsk, vma, address, write);
    if (fault < 0)
        goto out_of_memory;
    if (!fault)
        goto do_sigbus;
}
... 
```

```

```
```
do_sigbus:
    up ( &mm->mmap_sem );


    /*
     * Send a sigbus, regardless of whether we were in kernel
     * or user mode.
     */
    tsk->thread.cr2 = address;
    tsk->thread.error_code = error_code;
    tsk->thread.trap_no = 14;
    force_sig (SIGBUS, tsk);
```

```

As you can see, locking of the MM is very fine grained (and it better be!), the mm->mmap_sem is per-MM semaphore used (which typically varies from process to process).

force_sig (SIGBUS, current) is used to “force” the SIGBUS signal on the faulting task. force_sig() delivers the signal even if the process has attempted to ignore SIGBUS.

force_sig fills out the signal event structure and queues it into the process’s signal queue (current->sigqueue and current->sigqueue_tail)