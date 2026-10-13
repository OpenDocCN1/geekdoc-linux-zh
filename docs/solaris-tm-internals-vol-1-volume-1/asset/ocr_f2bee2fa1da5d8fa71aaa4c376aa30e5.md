processor when the lock is acquired. Interrupts are covered in more detail in “Kernel Traps and Exceptions” later in this chapter.

```
```c
struct kernel_data {
    mutex_t klock;
    char *fow_ptr;
    char *back_ptr;
    long data;
    int data2;
} kdata;

void function()
{
    mutex_init(&kdata.klock);

    mutex_enter(&kdata.klock);
    klock.data1 = 1;
    mutex_exit(&kdata.klock);
}
```
```

The preceding block of pseudocode illustrates the general mechanics of mutex locks. A lock is declared in the code; in this case, it is embedded in the data structure it is designed to protect. Once declared, the lock is initialized with the kernel mutex_init() function. Any subsequent reference to the kdata structure requires that the klock mutex be acquired with mutex_enter(). Once the work is done, the lock is released with mutex_exit(). The lock type, spin or adaptive, is determined in the mutex_init() code by the kernel. Assuming an adaptive mutex in this example, any kernel threads that make a mutex_enter() call on klock will either block or spin, depending on the state of the kernel thread that owns klock when mutex_enter() is called.

# 3.5.2 Solaris 7 Mutex Lock Implementation

The implementation description in this section is based on Solaris 7. Algorithmically, Solaris 2.5.1 and Solaris 2.6 are very similar but have some implementation differences, which we cover in the sections that follow.

The kernel defines different data structures for the two types of mutex locks, adaptive and spin, as shown in Figure 3.5.

![](bbox=[0.211, 0.741, 0.735, 0.856])

**Figure 3.5** *Solaris 7 Adaptive and Spin Mutex*