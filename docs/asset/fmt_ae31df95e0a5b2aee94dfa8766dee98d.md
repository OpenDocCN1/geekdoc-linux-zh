
函数`pthread_cond_signal()`用于重新启动等待某个条件的其中一个（且仅一个）线程。函数`pthread_cond_broadcast()`类似，它会重新启动所有线程。两者都接受一个`cond_t`类型的条件来标识该条件。

函数`pthread_cond_wait()`解锁由`mutex`指定的互斥锁，并等待变量`cond`上的信号。函数`pthread_cond_timedwait()`类似，但它会等待到`abstime`指定的时间为止。该时间通常是自 1970 年 1 月 1 日以来的秒数，并与系统调用`time()`返回的值兼容。这些函数也是取消点，成功时返回 0，失败时返回错误代码。

## `pthread_equal()` 函数

如果`thread1`和`thread2`所指的线程实际上是同一个，函数`pthread_equal()`返回非零值；否则返回零。

```c
#include <pthread.h>
```

```c
int pthread_equal(pthread_t thread1, pthread_t thread2);
```

## 互斥锁

互斥锁是互斥锁，是信号量的一种。互斥锁是`mutex_t`类型的对象，使得只有一个线程可以持有给定互斥锁的锁。像任何形式的信号量一样，它们通常用于防止两个进程或线程同时使用共享资源。尝试锁定已锁定互斥锁的线程将被挂起，直到持有锁的线程释放它。

```c
#include <pthread.h>
pthread_mutex_t fastmutex = PTHREAD_MUTEX_INITIALIZER;
pthread_mutex_t recmutex = PTHREAD_RECURSIVE_MUTEX_INITIALIZER_NP;
pthread_mutex_t errchmutex = PTHREAD_ERRORCHECK_MUTEX_INITIALIZER_NP;
```

```c
int pthread_mutex_init(pthread_mutex_t *mutex,
const pthread_mutexattr_t *mutexattr);
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_trylock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```

函数`pthread_mutex_init()`和`pthread_mutex_destroy()`分别是互斥锁对象的构造函数和析构函数。`pthread_mutex_lock()`和`pthread_mutex_unlock()`分别用于锁定和解锁互斥锁。函数`pthread_mutex_trylock()`与`pthread_mutex_lock()`，不同在于如果互斥锁已被锁定，它不会阻塞（挂起）。这些函数成功时返回 0，否则返回错误代码；`pthread_mutex_init()`永远不会失败。

## 示例程序

本节介绍我编写的一个库，该库演示了许多进程控制功能以及使用该库的一些示例程序。

### 子进程库

列表 11.1 显示了头文件`child.h`，列表 11.2 显示了该库的实际实现`child.c`。该库包含了创建一组子进程、在这些进程死亡时替换这些进程以及向这些进程发送信号的函数。它还包含一个函数，作为标准库函数`system()`和`popen()`更安全、更灵活的替代。

`child_fp_t`类型定义了一个指向将在子进程中执行的函数指针。两个参数分别是指向`child_info_t`结构的指针（用于描述子进程）和一个任意（用户定义）`void`指针。

`child_info_t`数据结构包含有关特定进程的信息，包括其进程 ID (pid)、父进程 ID (ppid)、通过给定组中的进程数计算的进程编号，以及指向要执行函数的指针。

`child_group_t`数据结构包含一组子进程的信息。成员`children`定义了数组中列出的进程数量。成员`maxchildren`和`activechildren`定义了要维护的最少和最大数量以及当前维护的数量；目前，这三个值应该都相同。数组包含多个`child_info_t`实例。该数据结构维护了一组运行相同函数的子进程的信息。

`child_groups`数据结构定义了多个组；每个组可能在运行不同的函数。成员`groups`表示类型为`child_info_t`的数组中定义了多少个组。这允许函数等待不同的进程。`child_create()`函数创建一个单独子进程。第三个参数`private_p`是一个用户定义的指针，会被传递给创建的子进程。`child_group_create()`函数当一个或多个组因任何原因终止时，创建在“min”到“max”之间的子进程副本（目前创建的数量将是“min”）。`child_groups_alive()`函数通过向每个子进程发送`SIGTERM`来统计子进程数量，并等待所有进程都死亡或经过几分钟，此时它会发送`SIGKILL`终止它们。`child_pipe()`函数是`system()`和`popen()`的替代方案。前三个参数与`execve()`系统调用的参数相似，定义了要执行的程序、命令行参数及其环境。剩余参数是指向`stdin`、`stdout`和`stderr`文件描述符的指针；如果这些指针不为空，则为相应的流创建一个管道，并将相应端的文件描述符返回到引用的对象中。

### 列表 11.1 child.h
