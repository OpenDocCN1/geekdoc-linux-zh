
这里的基本要求是语句中的值测试，以及随后的减1（如果它大于 0），必须相对于其他访问此信号量的线程或进程，以`原子操作`的方式完成。（也就是说，System V 信号量是在 20 世纪 80 年代中期在内核中实现的。由于信号量操作使用了内核内部调用，因此保证相对于其他进程的原子性是非常简单的）。

该操作还有其他常见名称：最初它被 Edsger Dijkstra 称为 P，源自荷兰语 *proberen*（意为“尝试”）。它也被称为

### 3. 信号量量（Post）

此操作增加信号量的值，可以用伪代码总结为：

```
semaphore_value++;
```

如果有任何进程因等待此信号量的值大于 0 而被阻塞，现在这些进程中的一个可以被唤醒。根据所所示的等待代码，此 post 操作相对于其他访问信号量的进程必须是原子的。

该操作还有其他常见名称：最初它被称为 V，源自荷兰语 *verogen*（意为“增加”）。它也被称为 up（因为信号量的值正在增加）、unlock 和 signal（信号）。我们在此处使用 Posix 术语 post。

显然，实际的信号量代码比 wait 和 post 操作的伪代码更多细节：即将所有等待给定信号量的进程排入队列，然后唤醒（可能多个中的）一个正正在等待给定信号量被 post 的进程。幸运的是，这些细节由实现处理。

注意，伪代码并没有假设值为 0 和 1 的二值信号量。该代码适用于初始化为任何负值的信号量。我们称这些**计数信号量**（Counting semaphores）。它们通常被初始化为值 N，表示可用资源（例如缓冲区）的数量。我们在整个章节中展示了二值信号量和计数信号量的示例。

我们区分了二值信号量和计数信号量，我们在我们的版本中是这样做的。在实现信号量的系统代码中，两者之间没有区别。

二值信号量可以用于互斥访问，就像互斥锁（mutex）一样。图 10.3 展示了一个。

```
initialize_mutex;
initialize_semaphore to 1;
```

```
pthread_mutex_lock(&mutex);
sem_wait(&sem);
critical region
pthread_mutex_unlock(&mutex);
sem_post(&sem);
```

图 10.3 使用互斥锁和信号量解决互斥的比较。我们将信号量初始化为 1。对 `sem_wait` 的调用等待值大于 0 并减少该值。对 `sem_post` 的调用增加该值。

## Posix 信号量

第10章

```
named               memory-based
semaphore           semaphore
sem_open()          sem_init()
            sem_wait()
            sem_trywait()
            sem_post()
            sem_getvalue()
```

图 10.6 Posix 信号量的函数调用。

```
sem_close()         sem_destroy()
sem_unlink()
```

图 10.7 进程内两个线程共享的基于内存信号量。

图 10.8 显示了共享内存（第4部分）中的 Posix 基于内存的信号量，它被两个进程共享。我们展示了共享内存属于这两个进程的地址空间。

图 10.8 共享内存中的基于内存信号量，由两个进程共享。

在本章中，我们首先描述了 Posix 命名信号量，然后是 Posix 基于内存的信号量。我们回到第 7.3 节的生产者-消费者问题，并将其扩展为允许多个生产者对应一个消费者，最后是多个生产者对应多个消费者。然后，我们展示了多缓冲常用的 I/O 技术是生产者-消费者问题的一个特例。

我们展示了 Posix 信号量的三种实现：第一种使用 FIFO，第二种使用内存映射 I/O 结合互斥锁和条件变量，最后使用 System V 信号量。

### 10.2 sem_open, sem_close 和 sem_unlink 函数

`sem_open` 函数创建一个新的信号量或打开一个现有信号量。信号量始终可以同步线程或进程。

```c
#include <semaphore.h>

sem_t *sem_open(const char *name, int flags, ...
    /* mode, unsigned int *value */);

返回值：成功时返回信号量指针，错误时返回 SEM_FAILED
```

我们在第 2.2 节中描述了关于名称参数的规则。
`flags` 参数指示它是 0、`O_CREAT` 还是 `O_CREAT | O_EXCL`，如第 2.3 节所述。如果指定了 `O_CREAT`，则第三个和第四个参数为：
`mode` 指定权限位（图 2.4），`value` 指定信号量的初始值。该初始值为 `SEM_VALUE_MAX`，必须至少为 32767。二进制信号量的初始值通常为1，而计数信号量的初始值通常大于此值。

如果指定了 `O_CREAT`（未指定 `O_EXCL`），则仅当信号量不存在时才对其进行初始化。如果信号量已存在，指定 `O_CREAT` 并不是错误。此标志仅意味着“如果信号量尚不存在，则创建并初始化它”。如果信号量已存在，指定 `O_CREAT | O_EXCL` 则是一个错误。

返回值是一个指向 `sem_t` 类型的指针。该指针随后被作 `sem_close`、`sem_wait`、`sem_trywait`、`sem_post` 和 `sem_getvalue` 的参数。

返回值 `SEM_FAILED` 表示错误。早期的草稿会使用空指针，这导致 Posix 标准返回 -1 来表示错误。

```c
sem = sem_open(name, flags, &value);
```

POSIX 对于通过 `sem_open` 创建或打开信号量时与信号量关联的权限描述较少。注意根据图 2.3 和我们的讨论，在打开命名信号量时，我们没有在标志参数中指定 `O_RDONLY`、`O_WRONLY` 或 `O_RDWR`。书中的示例使用了两个系统：Digital Unix 4 和 Solaris 26，它们都需要对现有信号量具有读和写权限才能成功。原因可能是因为这些信号量操作——post 和 wait——会读取并更改信号量的值。对现有信号量没有读或写权限会导致这些实现中的 `sem_open` 函数返回 `EACCES` 错误（“权限被拒绝”）。

一个通过 `sem_open` 打开的命名信号量由 `sem_close` 关闭。

```c
#include <semaphore.h>

int sem_close(sem_t *sem);
```
