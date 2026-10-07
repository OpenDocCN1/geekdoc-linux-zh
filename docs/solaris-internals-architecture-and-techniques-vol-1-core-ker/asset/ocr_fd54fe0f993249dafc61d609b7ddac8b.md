The implementation of the mutex code in Solaris 2.5.1 is quite different from the other releases, although algorithmically the behavior is essentially the same. Solaris 2.5.1 defines a mutex operations vector array. Each element in the array is a mutex_ops structure, one for each type of mutex defined in Solaris 2.5.1. The array is indexed according to the lock type and the function call. The design is such that specific functions handle lock operations for each of the different types of mutex locks. Common entry points into the mutex code pass control to the lock-specific functions by switching through the operations, as determined by the lock type and function offset. This is illustrated in Figure 3.8.

![](bbox=[0.36355, 0.21334999999999998, 0.90355, 0.49335])

Figure 3.8 Solaris 2.5.1 Mutex Operations Vectoring

Solaris 2.5.1 implements a wakeup method similar to that of Solaris 2.6 when an adaptive mutex is released with waiting threads; the highest priority waiter is selected for wakeup and should get ownership of the lock. It is, of course, possible for another thread to come along and acquire the lock before the wakeup is completed, the newly awakened thread is not guaranteed to get the lock.

Finally, note that the lockstat utility was first implemented in Solaris 2.6 and thus is not part of the 2.5.1 release.

# 3.5.2.3 Why the Mutex Changes in Solaris 7

We wanted to avoid getting mired in subtle differences that would not add real value to the text, but at the same time we want to point out relevant differences in implementations. The subsections describing the implementation differences across releases serve two purposes. The first and most obvious is completeness, to meet our goal of covering multiple Solaris releases. Second, and even more compelling, we see the evolution and refinements that have gone into the lock code from release to release. What we see is something that is functionally similar but significantly scaled down in size. The actual lock manipulation and turnstiles code follow the same trend shown in the data structures—scaled down, leaner, and more efficient.