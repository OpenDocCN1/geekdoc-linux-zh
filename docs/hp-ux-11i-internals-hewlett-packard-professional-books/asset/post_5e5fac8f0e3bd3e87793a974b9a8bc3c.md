
that they did not disturb the view of their neighbors. The kernel maintained peace in the community and made each process feel as if it were king of the hill. This type of process management required heavyweight context-switching system calls.

A threaded process is one in which there may be several threads of execution simultaneously contending for system resources. Unlike in the older multiprocess environment, a single process may have one or more concurrent threads. Multiple threads of the same process (called siblings) share the same system resource view. They share the same code, most of the same data space (each thread does have its own stack space and user area), and the same libraries and system resources. Since all the threads of a process are playing in the same sandbox, it becomes the responsibility of the programmer to develop strategies to assure that siblings don’t step on each other. To help in this task, many programming aids and libraries have been developed. The thread has become the schedulable entity and working incarnation of the program’s instructions and logic.

Today many operating system kernels (including HP-UX) operate in a multiprocess and multithreaded environment. The kernel must manage many different process contexts and also must manage processes with multiple threads. To accomplish this, the kernel considers individual threads, not processes, for scheduling. The thread becomes the active, working, schedulable entity for kernel management. This change in behavior between the process-centric and the thread-centric view of running a program is a seminal point in the evolution of operating system design.

In HP-UX, the kernel must keep track of all active processes and each of their individual threads. This is accomplished by the creation of what many feel are the two most fundamental data structures in the operating system kernel: the process table and the kernel thread table.

## Threading Models and HP-UX

Several threading models are utilized in modern operating systems (see Figure 4-3).

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_122_0.png)

**M x 1** threading allows for a single kernel-level thread per process. In the user space, a user-level scheduler may be employed to approximate the actions of a multi-threaded environment. Programmers use user-space library routines to accomplish pseudo-scheduling and resource coordination. The library routines must monitor the individual user threads and context-switch if the current active thread is about to make a system call that would result in a blocking action. Once any of a process’s user threads blocks on a call, the entire process is placed in a wait state. Keep in mind that from the perspective of the kernel, this is a single-threaded model (ergo the 1 in the M x 1 label). All of the scheduling is done by the user model, which results in a fairly low cost because the pseudo-scheduler does not encounter the additional overhead of system calls. While this is a plus, a big negative is that this model does not allow a process to take advantage of multiple CPU configurations.

**1 x 1** threading does allow for multiple threads per process. In this model, there is a one-to-one relationship between kernel and user threads, and no user-space scheduler is allowed. The kernel scheduler works only with kernel threads and has no knowledge of what goes on in the user space. A process’s user threads are bound one-on-one to a kernel thread, which in turn is scheduled on a specific CPU. The scheduler runs in kernel space and requires heavyweight system calls to manage each processor’s run-queue. Processor run-queues are built by creating a linked list of kernel threads, *kthreads*, that share the same priority queue and processor affinity. The thread at the head of the list of the strongest active priority queue will be the next one scheduled. Once a kernel thread is scheduled, it may pass control to its user thread. We return to a kernel thread only when the user thread makes a system call or to the kernel proper upon receipt of a system interruption. While this model makes extensive use of system calls, it allows a process to take advantage of parallel execution on SMP systems.

**M x N** threading brings together both of the previous models. In this environment, the programmer may choose to employ a user-space scheduler or simply rely on the kernel scheduler, or use a combination of both. On SMP systems, user threads may be multiplexed to several kernel threads or simply bound in a one-to-one fashion at the discretion of the application programmer. This gives the programmer the greatest degree of control when trying to optimize process performance.

**Hewlett Packard is using a phased introduction of threading to the HP-UX kernel.**

**Phase 1** occurred with the release of HP-UX 10.10. This involved modifying the kernel's scheduling system to work with the newly created `kthread` table entries. For this release, only one thread of execution could exist per `proc` table entry. One could argue that this was not truly a threaded kernel; in effect, we were at the time merely “prepping the kernel for threads.” A limited form of threading known as user threads, or the M x 1 model (making use of the DCE libpthread library), was also available to programmers at this time.

**Phase 2** came with HP-UX release 10.30/11.00, which adopted a threading model called 1 x 1 threading: for each thread spawned by a user process, there is a single unique kernel thread. This new capability allowed a process to spawn multiple sibling threads and, for the first time on an HP-UX system, allowed a process to take full advantage of SMP system parallelism. To facilitate this model, the POSIX kernel threads library, `libpthread`, was implemented.

The release of HP-UX 10.30 (an early developers' release for workstations) provided for compliance with the POSIX 1003.1b API for multithreaded application development. With the full HP-UX 11.00 release, more thread features were added to make it POSIX 1003.1c compliant.

**Phase 3** will be implemented in a future release. This phase will adopt the M x N threading model. In this model a single kernel thread may be associated with one or more individual user threads. This is a very flexible model, but along with flexibility comes an added cost in the complexity of the programming. M x N threads should be available on HP-UX in the near future.

## The System Call Interface

Each process thread consists of a bound user/kernel thread pair (unless a user-space scheduler is used). This thread is executing instructions from either the process's user memory space or from the privileged memory space of a legitimate kernel system call at any one instance of time. In addition to the many process-based threads, at times the system is required to halt the execution of the currently scheduled thread and switch to a specific kernel-only thread for the performance of interrupt handling, scheduling, or a host of other operating system-related tasks.

The transition between these various modes of operation is the study of the system call interface and the interrupt system (see Figure 4-4). We discussed the occurrence and handling of internal system-level interruptions in Chapter 1, “HP PA-RISC Architecture,” and we explore external interrupts in detail in Chapter 10, “I/O and Device Management.”

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_124_0.png)

### Figure 4-4 User-to-Kernel Thread Transitions

For now, consider that there are only two means by which a processor’s current execution mode may be changed from user mode to kernel mode. The first is as the result of some type of system interruption that results in an immediate switch into the kernel context. The second is the direct result of the current user thread making a request to use one of the many provided kernel routines known as system calls, syscall().

The return to the most deserving user thread is controlled by the same kernel-level mechanism, syscall(), regardless of which event caused the switch to kernel mode. This kernel routine is responsible for the delivery and notification of process-to-process signals and the handling of user-level context-switching, returning from a user-defined signal-handling routine, returning from a system-level interruption handler, and returning from a user thread-requested system call. It therefore must be able to deal with several different user and kernel stacks for the recovery of the user thread’s context (a thread’s run state context is stored in a process control block, or PCB, structure).

Reference Figure 4-5 as we describe the various tasks performed by a thread during the execution of a system call.
