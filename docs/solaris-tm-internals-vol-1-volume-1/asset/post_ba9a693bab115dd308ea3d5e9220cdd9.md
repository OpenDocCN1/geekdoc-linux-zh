
Solaris 2.5.1 and 2.6 implement a dispatcher lock in the reader/writer (RW) lock structure to protect access to some fields in the structure. Solaris 7, with a reworking of the RW lock code, no longer requires a dispatcher lock in this area.

### 3.9 Kernel Semaphores

Semaphores provide a method of synchronizing access to a sharable resource by multiple processors or threads. A semaphore can be used as a binary lock for exclusive access or as a counter, allowing for concurrent access by multiple threads to a finite number of shared resources.

In the counter implementation, the semaphore value is initialized to the number of shared resources (these semaphores are sometimes referred to as counting semaphores). Each time a process needs a resource, the semaphore value is decremented to indicate there is one less of the resource. When the process is finished with the resource, the semaphore value is incremented. A 0 semaphore value tells the calling process that no resources are currently available, and the calling process blocks until another process finishes using the resource and frees it. These functions are historically referred to as semaphore P and V operations—the P operation attempts to acquire the semaphore, and the V operation releases it.

The Solaris kernel uses semaphores where appropriate, when the constraints for atomicity on lock acquisition are not as stringent as they are in the areas where mutex and RW locks are used. Also, the counting functionality that semaphores provide makes them a good fit for things like the allocation and deallocation of a fixed amount of a resource.

The kernel semaphore structure maintains a sleep queue for the semaphore and a count field that reflects the value of the semaphore, shown in Figure 3.15. The figure illustrates the look of a kernel semaphore for all Solaris releases covered in this book.

| Field | Description |
|---|---|
| `*s_slpq` | Sleep queue management of the semaphore; points to a kernel thread waiting on the semaphore. |
| `s_count` | The semaphore value |

**Figure 3.15** *Kernel Semaphore*

Kernel functions for semaphores include an initialization routine (`sema_init()`), a destroy function (`sema_destroy()`), the traditional P and V operations (`sema_p()` and `sema_v()`), and a test function (is the semaphore held? `sema_held()`). There are a few other support functions, as well as some variations on the `sema_p()` function, which we discuss later.

The `init` function simply sets the count value in the semaphore, based on the value passed as an argument to the `sema_init()` routine. The `s_slpq` pointer is set to `NULL`, and the semaphore is initialized. The `sema_destroy()` function is used when the semaphore is an integral part of a resource that is dynamically created and destroyed as the resource gets used and subsequently released. For example, the bio (block I/O) subsystem in the kernel, which manages buf structures for page I/O support through the file system, uses semaphores on a per-buf structure basis. Each buffer has two semaphores, which are initialized when a buffer is allocated by `sema_init()`. Once the I/O is completed and the buffer is released, `sema_destroy()` is called as part of the buffer release code. (`sema_destroy()` just nulls the `s_slpq` pointer.)

Kernel threads that must access a resource controlled by a semaphore call the `sema_p()` function, which requires that the semaphore count value be greater than 0 in order to return success. If the count is 0, then the semaphore is not available and the thread must block. If the count is greater than 0, then the count is decremented in the semaphore and the code returns to the caller. Otherwise, a sleep queue is located for the systemwide array of sleep queues, the thread state is changed to sleep, and the thread is placed on the sleep queue. Note that turnstiles are not used for semaphores—turnstiles are an implementation of sleep queues specifically for mutex and RW locks. Kernel threads blocked on anything other than mutexes and RW locks are placed on sleep queues.

Sleep queues are discussed in more detail in Chapter 6, “The Solaris Dispatcher.” Briefly though, sleep queues are organized as a linked list of kernel threads, and each linked list is rooted in an array referenced through a `sleepq_head` kernel pointer. Some changes were made in Solaris 7 to facilitate faster sleep queue operations: insertion, removal, and queue traversal. In Solaris releases prior to Solaris 7, an entry in the `sleepq_head` array begins a linked list of kernel threads waiting on the same object. The list is singly linked by the kernel thread's `t_link` pointer. In Solaris 7, several additional pointers were added to the kernel thread to support a doubly linked sublist of threads at the same priority. Figure 3.16 illustrates how sleep queues are organized.

![](img/220ae4af07df2fe8e5be69d27f885d1b_142_0.png)

**Figure 3.16** *Sleep Queues in Solaris 2.5.1, 2.6, and 7*

In all pre- and post-Solaris 7 implementations, a hashing function indexes the `sleepq_head` array, hashing on the address of the object. In the pre-Solaris 7 implementation, kernel threads are inserted on the list in descending order based on their priority. In Solaris 7, the singly linked list that establishes the beginning of the doubly linked sublists of threads at the same priority is also in ascending order based on priority. The sublist is implemented with a `t_priforw` (forward pointer) and `t_priback` (previous pointer) in the kernel thread. Also, a `t_sleepq` pointer added in Solaris 7 points back to the array entry in `sleepq_head`, identifying which sleep queue the thread is on and providing a quick method to determine if a thread is on a sleep queue at all; if the thread's `t_sleepq` pointer is `NULL`, then the thread is not on a sleep queue.

Inside the `sema_p()` function, if we have a semaphore count value of 0, the semaphore is not available and the calling kernel thread needs to be placed on a sleep queue. A sleep queue is located through a hash function into the `sleepq_head` array, which hashes on the address of the object the thread is blocking, in this case, the address of the semaphore. The code also grabs the sleep queue lock, `sq_lock` (see Figure 3.16), to block any further inserts or removals from the sleep queue until the insertion of the current kernel thread has been completed (that's what locks are for!).

The scheduling-class-specific sleep function is called to set the thread wakeup priority and to change the thread state from ONPROC (running on a processor) to SLEEP. The kernel thread's `t_wchan` (wait channel) pointer is set to the address of the semaphore it is blocking on, and the thread's `t_sobj_ops` pointer is set to reference the `sema_sobj_ops` structure. The thread is now in a sleep state on a sleep queue.

A semaphore is released by the `sema_v()` function, which has the exact opposite effect of `sema_p()` and behaves very much like the lock release functions we've examined up to this point. The semaphore value is incremented, and if any threads are sleeping on the semaphore, the one that has been sitting on the sleep queue longest will be woken up. Semaphore wakeups always involve waking one waiter at a time.

Semaphores are used in relatively few areas of the operating system: the buffer I/O (`bio`) module, the dynamically loadable kernel module code, and a couple of device drivers.

## KERNEL BOOTSTRAP AND INITIALIZATION

In the previous chapters, we provided a description of the Solaris kernel and an overview of the key features and facilities of the operating system. We emphasized the modular and dynamic nature of the kernel because the Solaris kernel does not originate on disk as a single, monolithic binary object. Rather, the kernel is constructed in memory, during system bootstrap, as major operating system components are loaded.

Kernel objects are loaded both at boot time and while the system is running. In this chapter, we take a look at the directory hierarchy that stores binary kernel objects. We then discuss the kernel bootstrap and initialization process, the dynamic module loading facility, and the kernel runtime linker.

### 4.1 Kernel Directory Hierarchy

The binary object modules that make up the Solaris kernel exist in a well-defined directory name space in the root and usr file systems. The system directory names are described in Table 4-1.
