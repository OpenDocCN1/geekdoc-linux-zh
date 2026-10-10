
## Virtual Mode Initialization

### Pre-Initialization Steps (continued)

- 8. Call `pa_memory_init()`, which scans the central bus for memory modules not yet initialized. Any memory modules found are initialized and added to the native module tree.
- 9. Create another resource map `real_free_map` to be used to track available pages now that we have initialized the rest of memory. The resource map we had been using is copied into this new one.
- 10. Create the 32-bit and 64-bit resource maps `sysmap_32bit` and `sysmap_64bit`.
- 11. Using the routines provided by HPUXBOOT, read the LVM configuration from `/stand/rootconf` and the stored I/O configuration from `/stand/ioconfig`.
- 12. Perform first-level I/O configuration. This calls `pa_module_init()` to scan the system's busses looking for modules. Each module is added to the `native_mod_tree`. If the module is a processor, it gets a crash table entry; if it is an I/O module, the module is reset and interrupt handlers are set up for the module.
- 13. The `fixed_mod_table` (from `/stand/ioconfig`) gets merged with the `native_mod_table`, which contains devices we've discovered.
- 14. The space used by HPUXBOOT is now freed—it is no longer needed.
- 15. Allocate and initialize a number of kernel data structures. These include:
    - The `pgclass` table, used by `crashconf(1m)` to mark which pages to dump in the event of a panic
    - `mproc_info` structures for non-monarch processors
    - `pdir` locks, the page directory, and the `pfn_to_virt` table
    - The I/O alias table
    - The space map
    - The inode table
    - The file table
    - The directory name lookup cache (DNLC)
    - The `proc` and `kthread` tables
    - Physo's private buffer pool
    - Processor save state areas
    - Callouts
    - Resource allocation maps for quadrants 2, 3, and 4
- 16. Handcraft `proc[0]`, the swapper. Assign it to `kthread[0]`. Create a virtual address space for it, and manually map it to a real address.
- 17. Allocate and initialize processor idle stacks and non-monarch interrupt stacks.
- 18. Map any extra I/O register sets into virtual space.
- 19. Each page we allocated so far while in real mode is inserted into the `pdir` and reserved in `sysmap_32bit`.

Let's have a look at where we are when `realmain()` completes:

- We have discovered all our I/O devices and reset them, but have not yet assigned drivers to them.
- The virtual memory system is initialized and ready to run.
- The monarch is still the only processor running, although we have initialized much of the data for the other processors.
- The file systems are initialized.
- The proc and thread tables are initialized, and the first entry in each is occupied by the swapper process.

When `realmain()` completes, it returns to its caller, `rdb_bootstrap()`. The next thing `rdb_bootstrap()` does is put us into virtual mode by setting the W, D, C, P, Q, and I bits. This gives us wide mode, data translation, code translation, protection identifier validation, interrupt state collection, and external interrupts enabled. The system is now running in virtual mode.

Once `rdb_bootstrap()` has placed the system into virtual mode, it has a couple of more steps to do. It flushes all the caches because the `realmain` routine does some code optimization. This act of having the kernel modify its own code can cause problems with the caches, so we flush them. We also create the kernel stack and switch to using that instead of the interrupt stack. Finally, `rdb_bootstrap` branches to `main()`, the virtual mode main program for the kernel.

`main()` is similar to `realmain()` in that it works from a calllist. This one is called `mainstreet_calllist`. One interesting difference in `main` is that it never returns. The thread that calls the `mainstreet_calllist` routines eventually become `proc 0`, the swapper. If `DoCalllist` ever returns in `main()`, we'll panic with the message `main: Road Ends.`

Like `realmain`, `calllist`, `mainstreet_calllist` has a lot of work to do. There are over 100 entries on the calllist. Rather than list them all, we just summarize the more important functions.

The first step is to initialize more systemwide data structures: semaphores, the per-processor run queues, `t_tss` data structures, and `clocks`. Then, we finish filling out `proc[0]`, `kthread[0]`, and the user area for that thread. All other proc table and kthread table entries are placed on the `freeproc_list` or `freekthread_list`. We set up the external clock interrupt handler and start the clock ticking.

At this point, we're finally ready to start up the non-monarch processors. They get started up one at a time. For each processor, the monarch does the following:

- Setup the `procinfo` structure and IVA for the particular processor.
- Set the global variable `boot_rendez_state` to `RS_RENDEZ_IN_PROGRESS`.
- Set the `MEM_RENDEZ` pointer in page zero of memory to point to `force_start()`.
- Send a rendezvous interrupt to the processor on EIRR bit 0.
- Monitor the value of `boot_rendez_state` for 10 seconds. If it changes to `RS_RENDEZ_ACK`, then the processor woke up. If it doesn't, then the processor is considered bad.

When a processor gets the rendezvous interrupt, it branches to the interrupt handler at `MEM_RENDEZ—force_start()`. This is an assembly language routine that does many of the things that `rdb_bootstrap()` does—the processor goes into wide mode, clears and enables interrupts, and sets up its IVA, stack, and data pointers. It then calls `non_monarch_init()` to do real mode initialization. `non_monarch_init()` sets up the TLB for the processor and fills in the rest of the `procinfo` structure. It then sets `boot_rendez_state` to `RS_RENDEZ_ACK` to indicate to the monarch that it has started.

Once it has done this, the processor begins to spin, watching the global value `mp_sync_after_rendez`. As long as this value is `WAIT_FOR_ALL_PROCESSORS`, it continues spinning. We'll see how that happens shortly.

Back on the monarch, once all the non-monarchs have been started, we continue with system initialization by initializing the scheduler. Next, we perform second-level I/O configuration, as described in detail in Chapter 10, “I/O and Device Management.” When this process is complete, we'll have the I/O tree completely filled out with drivers mapped to each device. Now we're ready for more Subsystem initialization! We set up buffer hash queues and allocate the buffer cache, initialize System V semaphores and shared memory, and initialize LVM.

Finally, we're ready to start some disk activity—starting with mounting the root file system. We go through every file system that was registered during the second level I/O configuration, looking for one with an empty point for `vfs_mountroot`. When we find one, that entry point is called, causing the file system to be mounted read-only on `/`.

Next, we fork some system daemon processes—`vhand`, `stataemon`, `unhashdaemon`, and `ttsr`. The process is very similar to the use of the `fork()` system call in a user program. We first have to call `prepare_newproc()`, which initializes a proc structure and a `kthread` structure, and gives us back pointers to those new structures. When we call `newproc()`, passing it the pointers to the new proc and kthread. Just like `fork()`, `newproc()` returns twice: once in the parent and once in the child. We check for a return value of `FORKRN_CHILD` to indicate that we are the new child process. If we are the child, then we call the appropriate routine—`vhand`, `stataemon`, `unhashdaemon`, or `ttsr_daemon`—to perform the daemon function. These calls never return; they run as long as the system is up.

Up to this point, all of the processes we've launched have been kernel processes. They run in kernel address space; use the kernel stack; and have access to all the kernel functions. The next step is to launch the first user space process—the pre_init_rc process. pre_init_rc is a script found in /etc/pre_init_rc and is responsible for performing an fscok on the root file system. We start out as before, calling prepare_newproc() and newproc() to fork a new process and kernel thread. Then we handcraft a small data space—three pages—and attach it to the thread. The first page gets a fixed preamble, coded in assembly, which contains some simple support routines. These include a version of strlen(), a version of bcopy(), and an interface to allow system calls. We need this preamble because we don't have direct access to the kernel's system call handlers or to routines like bcopy(), since the process is a user space process. At the same time, we don't have access to libc or any of the other usual C libraries because the kernel doesn't know where those are yet. We've only got the root file system mounted. Immediately following this, the code we want to run gets copied into the page. The second page is reserved for data for the process, and the third is used for stack.

Three pages isn't much space to operate in, but it doesn't have to do much. The code that gets placed into the first page opens stdin, stdout, and stderr, then does an execve() system call. For the pre_init_rc script, we tell execve() to run sh out of /sbin and pass pre_init_rc as argv[1]. The execve() syscall takes care of loading the shell and expanding memory regions as required, and then the shell runs the pre_init_rc script.

After the pre_init_rc script has run, we unmount the root file system, then mount it again, this time writable. Now we're ready to fork the init process.

Init gets forked essentially in the same way as pre_init_rc—by creating a process, creating a three-page user space for it, then using that space to make an execve() system call to get init running.

We're on the home stretch now. Once init is up and running, it starts forking off the user processes. We still need to get the rest of the processors going—we left them spinning, looking at the mp_sync_after_rendez global. The monarch processor now sets that global to CONTINUE_EXECUTION. All of the other processors now continue with their startup, much as the monarch did—they go into virtual mode, start their clocks ticking, and eventually call idle(), where they loop, looking for processes to run.

The last thing that the monarch does in the boot process is call sched(). This causes that thread of execution to become the sched process. Note that this isn't like the other daemons, where we forked first and the child became the daemon. We don't fork for sched, so the thread of execution that has done all the work for us so far becomes sched.

## Summary

We've looked at the boot process from the time that the system is powered on to the time it's running and ready to launch user processes. Most of the process is fairly routine—the creation and initialization of systemwide data structures. Some of the steps are described in more detail in other chapters, particularly the I/O configuration process. We've seen too that there are some unusual things that have to happen during boot, such as handcrafting processes and making the leap into user space to launch user-level processes. There's a lot of work that has to get done to get from power off to running, particularly in a multiprocessor system.
