turnstiles are not used for semaphores—turnstiles are an implementation of sleep queues specifically for mutex and RW locks. Kernel threads blocked on any-thing other than mutexes and RW locks are placed on sleep queues.

Sleep queues are discussed in more detail in Chapter 6, "Kernel Memory." Briefly though, sleep queues are organized as a linked list of kernel threads, and each linked list is rooted in an array representing the sleepq_head kernel pointer. Some changes were made in Solaris 7 to facilitate faster sleep queue operations: insertion, removal, and traversal. In Solaris prior to Solaris 7, an entry in the sleepq_head array begins a linked list of kernel threads waiting on the same object. The list is singly linked by the kernel thread's t_link pointer. In Solaris 7, several additional pointers were added to the kernel thread to support a doubly linked sublist of threads at the same priority. Figure 3.16 illustrates how sleep queues are organized.

![](bbox=[0.188, 0.40355, 0.876, 0.7635])

# Sleep Queues in Solaris 2.5.1 and 2.6

# Sleep Queues in Solaris 7

Figure 3.16 Sleep Queues in Solaris 2.5.1, 2.6, and 7

In all pre and post-Solaris 7 implementations, a hashing function indexes the sleepq_head array, hashing the address of the object. In the pre-Solaris 7 implementations, kernel threads are inserted on the list in descending order based on their priority. In Solaris 7, the singly linked list that establishes the beginning of the doubly linked sublists of kthreads at the same priority is also in ascending order based on priority. The sublist is implemented with a t_priforw (forward