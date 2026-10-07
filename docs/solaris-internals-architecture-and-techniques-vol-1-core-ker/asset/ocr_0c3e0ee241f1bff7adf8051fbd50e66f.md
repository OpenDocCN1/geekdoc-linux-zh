# Kernel Semaphores

The calling process that no resources are currently available, and the calling process blocks until another process finishes using the resource and frees it. These functions are historically referred to as the semaphore P and V operations—the P operation attempts to acquire the semaphore, and the V operation releases it.

The Solaris kernel uses semaphores where appropriate, with the constraints for atomicity on lock acquisition not as stringent as they are in the areas where mutex and RW locks are used. Also, the counting functionality that semaphores provide makes them a good fit for things like the allocation and deallocation of a fixed amount of a resource.

The kernel semaphore structure maintains a sleep queue for the semaphore and a count field that reflects the value of the semaphore, shown in Figure 3.15. The figure illustrates the look of a kernel semaphore for all Solaris releases covered in this book.

| s_slipq | Sleep queue management of the semaphore; |
| s_count | points to a kernel thread waiting on the semaphore. |
| | The semaphore value |

Figure 3.15 Kernel Semaphore

Kernel functions for semaphores include an initialization routine (sema_init()), a destruction (sem_destroy()), the traditional P and V operations (sema_p() and sem_v()), and a test function (is the semaphore held? sem_held()). There are a few other support functions, as well as some variations on the sem_p() function, which we will discuss later.

The init function simply sets the count value in the semaphore, based on the value passed as an argument to the sem_init(). The s_slipq pointer is set to NULL, and the semaphore is initialized. The sem_destroy() is used when the semaphore is an integral part of a resource that is dynamically created and destroyed by the resource gets and subsequently released. For example, the bio (block I/O) subsystem in the kernel, which manages buf structures for I/O support through the file system, uses semaphores on a per-buffer basis. Each buffer has two semaphores, which are initialized when a buffer is allocated by sem_init(). The I/O is completed and the buffer is released, sem_destroy() is called as part of the buffer release code.{sem_destroy()} just null the s_slipq pointer.

Kernel threads that must access a resource controlled by a semaphore call the sem_p() function, which requires the semaphore count value be greater than 0 in order return success. If the count is 0, then the semaphore is unavailable and the calling thread must block. If the count is greater than 0, then the count is decremented in the semaphore and the code returns to the caller. Otherwise, a sleep queue is located from the systemwide array of sleep queues, and the thread state is changed to sleep, and the thread