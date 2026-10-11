# vfork()

The vfork() system call has the same effect as fork(), except that the page table entries of the parent process are not copied. Instead, the child executes as the sole thread in the parent's address space, and the parent is blocked until this child either calls exec() or exits. The child is not allowed to write to the address space. This was a welcome optimization in the old days of 386BSD when the call was introduced because at the time copy-on-write pages were not used to implement fork(). Today, with copy-on-write and child-runs-first semantics, the only benefit to vfork() is not copying the parent page tables entries. If Linux one day gains copy-on-write page table entries, there will no longer be any benefit. Because the semantics of vfork() are tricky (what, for example, happens if the exec() fails), ideally systems would not need vfork() and the kernel would not implement it. It is entirely possible to implement vfork() as a normal fork()—this is what Linux did until version 2.2.

The vfork() system call is implemented via a special flag to the clone() system call:

+   1. In copy_process(), the task_struct member vfork_done is set to NULL.
+   2. In do_fork(), if the special flag was given, vfork_done is pointed at a specific address.
+   3. After the child is first run, the parent—instead of returning—waits for the child to signal it through the vfork_done pointer.
+   4. In the mm_release() function, which is used when a task exits a memory address space, vfork_done is checked to see whether it is NULL. If it is not, the parent is signaled.
+   5. Back in do_fork(), the parent wakes up and returns.

If this all goes as planned, the child is now executing in a new address space, and the parent is again executing in its original address space. The overhead is lower, but the implementation is not pretty.

# The Linux Implementation of Threads

Threads are a popular modern programming abstraction. They provide multiple threads of execution within the same program in a shared memory address space. They can also share open files and other resources. Threads enable concurrent programming and, on multi-processor systems, true parallelism.

Linux has a unique implementation of threads. To the Linux kernel, there is no concept of a thread. Linux implements all threads as standard processes. The Linux kernel

> * Patches are available to add this functionality to Linux. In time, this feature will most likely find its way into the mainline Linux kernel.