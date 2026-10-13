![](bbox=[0.176, 0.12, 0.795, 0.412])

# Figure 3.7 *Solaris 2.5.1 Adaptive Mutex*

The implementation of the mutex code in Solaris 2.5.1 is quite different from the other releases, although algorithmically the behaviour is essentially the same. Solaris 2.5.1 defines a mutex operations vector. Each element in the array is a mutex_ops structure, one structure for each type of mutex defined in Solaris 2.5.1. The array is indexed according to the lock type and the function called. The design is such that specific functions handle lock operations for each of the different types of mutex locks. Common entry points into the mutex code pass control to the lock-specific functions by switching through the operations array, as determined by the lock type and function offset. This is illustrated in Figure 3.8.

![](bbox=[0.212, 0.659, 0.853, 0.831])

# Figure 3.8 *Solaris 2.5.1 Mutex Operations Vectoring*

Solaris 2.5.1 implements a wakeup method similar to that of Solaris 2.6 when an adaptive mutex is released with waiting threads; the highest priority waiter is