Whenever you write kernel code, you should ask yourself these questions:

+   Is the data global? Can a thread of execution other than the current one access it?
+   Is the data shared between process context and interrupt context? Is it shared between two different interrupt handlers?
+   If a process is preempted while accessing this data, can the newly scheduled process access the same data?
+   Can the current process sleep (block) on anything? If it does, in what state does that leave any shared data?
+   What prevents the data from being freed out from under me?
+   What happens if this function is called again on another processor?
+   Given the preceding points, how am I going to ensure that my code is safe from concurrency?

In short, nearly all global and shared data in the kernel requires some form of the synchronization methods, discussed in the next chapter.

# # Deadlocks

A *deadlock* is a condition involving one or more threads of execution and one or more resources, such that each thread waits for one of the resources, but all the resources are already held. The threads all wait for each other, but they never make any progress toward releasing the resources that they already hold. Therefore, none of the threads can continue, which results in a deadlock.

A good analogy is a four-way traffic stop. If each car at the stop decides to wait for the other cars before going, no car will ever proceed, and we have a traffic deadlock.

The simplest example of a deadlock is the self-deadlock.4 If a thread of execution attempts to acquire a lock it already holds, it has to wait for the lock to be released. But it will never release the lock, because it is busy waiting for the lock, and the result is deadlock:

```
acquire lock
acquire lock, again
wait for lock to become available
...
```

> 4 Some kernels prevent this type of deadlock by providing recursive locks. These are locks that a single thread of execution may acquire multiple times. Linux, thankfully, does not provide recursive locks. This is widely considered a good thing. Although recursive locks might alleviate the self-deadlock problem, they very readily lead to sloppy locking semantics.