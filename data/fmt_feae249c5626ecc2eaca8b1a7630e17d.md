
列表 4.14 再次显示了之前的示例，现在使用条件变量来保护线程标志。注意，在 `thread_function` 中，在检查 `thread_flag` 的值之前持有互斥锁的锁。该锁会在 `pthread_cond_wait` 阻塞前自动释放，并在阻塞后自动重新获取。此外，注意 `set_thread_flag` 在设置 `thread_flag` 的值并发送信号之前会锁定互斥锁。

# 第 4 章 线程

## 列表 4.14 `condvar.c` 使用条件变量控制线程

```c
#include <pthread.h>

int thread_flag;
pthread_cond_t thread_flag_cv;
pthread_mutex_t thread_flag_mutex;

void initialize_flag () {
    /* 初始化互斥锁和条件变量。 */
    pthread_mutex_init(&thread_flag_mutex, NULL);
    pthread_cond_init(&thread_flag_cv, NULL);
    /* 初始化标志值。 */
    thread_flag = 0;
}

/* 当线程标志为真时，反复调用 do_work；
   如果标志为假则阻塞。 */

void* thread_function (void* thread_arg) {
    /* 无限循环。 */
    while (1) {
        /* 在访问标志值之前锁定互斥锁。 */
        pthread_mutex_lock(&thread_flag_mutex);
        while (!thread_flag) {
            /* 标志为假。等待条件变量的信号，
               表示标志已更改。当信号
               到达且此线程解除阻塞时，循环并再次检查
               标志。 */
            pthread_cond_wait(&thread_flag_cv, &thread_flag_mutex);
            /* 当我们到达这里时，标志必须为真了。 */
            // 解锁互斥锁。
        }
        pthread_mutex_unlock(&thread_flag_mutex);
        /* 执行一些工作。 */
        do_work();
    }
    return NULL;
}

void set_thread_flag (int flag_value) {
    /* 在访问标志值之前锁定互斥锁。 */
    pthread_mutex_lock(&thread_flag_mutex);
    /* 设置标志，然后发送信号，以防 thread_function
       处于阻塞状态等待标志被设置。然而，
       thread_function 在互斥锁解锁之前实际上无法检查标志。 */
    thread_flag = flag_value;
    pthread_cond_signal(&thread_flag_cv);
    /* 解锁互斥锁。 */
    pthread_mutex_unlock(&thread_flag_mutex);
}
```

由条件变量保护的条件可以任意复杂。然而，在执行任何可能使条件产生意义的操作之前，应该需要互斥锁，并在之后对条件变量发送信号。

条件变量可以在没有条件的情况下使用，仅作为一种阻塞线程的机制，直到另一个线程“唤醒”它。信号量也可用于目的。主要区别在于，信号量会“记住”唤醒调用，即使当时没有线程在阻塞；而条件变量除非实际上有线程在阻塞，否则会丢弃唤醒调用。此外，信号量每次发布（post）只交付一次唤醒；而使用 `pthread_cond_broadcast` 可以同时唤醒任意数量的未知线程。

### 4.4.7 两个或多个线程的死锁

当两个（或多个）线程被阻塞，等待一个只有另一个线程才能发生的条件时，就会发生死锁。例如，如果线程 A 阻塞在条件变量上等待线程 B 发送信号，而线程 B 阻塞在条件变量上等待线程 A 发送信号，则发生了死锁。

导致死锁的一个常见错误涉及多个线程以不同的顺序锁定相同的资源。这是一个更一般的死锁问题，涉及的不只是互斥锁等同步对象，还有其他资源，如文件或设备。解决方法是确保所有线程以相同的顺序锁定资源。

# 线程实现

GNU/Linux POSIX 线程实现与许多 Unix 类系统的实现有重要不同：GNU/Linux 将线程实现为进程。当你调用 `pthread_create` 创建新线程时，Linux 会创建一个运行线程的新进程。然而，这个进程与你通过 `fork` 创建的进程不同；特别是它与原始进程共享地址空间和资源，而不是接收副本。

列表 4.15 所示的程序演示了这一点。该程序创建了一个线程；原始线程和新线程都会调用 `getpid` 函数并打印各自的进程 ID，然后无限循环。

## 列表 4.15 `thread-pid` 为线程打印进程 ID

```c
#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

void* thread_function(void* arg) {
    fprintf(stderr, "child thread pid is %d\n", (int) getpid());
    /* 无限循环。 */
    while (1) {
        return NULL;
    }
}

int main () {
    pthread_t thread;
    fprintf(stderr, "main thread pid is %d\n", (int) getpid());
    pthread_create(&thread, NULL, thread_function, NULL);
    /* 无限循环。 */
    while (1) {
        return 0;
    }
}
```

在后台运行该程序，然后调用 `ps x` 显示正在运行的进程。之后不要忘记杀死 `thread-pid` 程序——它消耗大量的 CPU。输出可能如下：

```c
$ cc thread-pid.c -o thread-pid -lpthread
$ thread-pid &
[1] 14608
main thread pid is 14608
child thread pid is 14610
ps x
PID TTY      STAT COMMAND
14602 pts/9 S    0:00 bash
14608 pts/9 R    0:01 ./thread-pid
```

1469 pts/9 S 0:00 ./thread-pid

1460 pts/9 R 0:01 ./thread-pid

1461 pts/9 R 0:00 ps x

% kill 14608

[1]+ ./thread-pid

# Shell 中的作业控制 `Job Control`

以 `[1]` 开头的行来自 shell。当你在后台运行一个程序时，shell 会为其分配一个作业号——在本例中为 1——并打印程序的 pid。如果后台作业终止了，shell 会会在你下次调用命令时报告该信息。

请注意，有三个进程在运行 `thread-pid` 程序。其中第一个（pid 为 14608）是程序的主线程；第三个（pid 为 14610）是我们创建的执行 `thread_function` 的线程。

那么第二个（pid 为 14609）又是什么呢？它是“管理线程”，是 GNU/Linux 线程内部实现的一部分。当程序第一次调用 `pthread_create` 创建新线程时，就会创建管理线程。

### 4.5.1 信号处理 `Signal Handling`

假设一个多线程程序接收到一个信号。信号处理器在哪个线程中被调用？信号与线程之间的交互行为在不同的 UNIX 类系统之间存在。在 GNU/Linux 中，这种行为是由线程实现为进程这一事实决定的。

由于每个线程都是独立的进程，而且信号是传递给特定进程的，因此对于哪个线程接收信号并没有歧义。通常，来自程序外部的信号会被发送到程序主线程对应的进程。例如，如果一个程序进行了 fork 且子进程创建了一个多线程程序，父进程将持有子程序主线程的 pid，并使用该 pid 向子进程发送信号。在向多线程程序发送信号时，这通常是一个值得遵循的约定。

请注意，GNU/Linux 线程线程的这一方面与 POSIX 线程标准存在差异。在需要移植的程序中，不要依赖这种行为。

在多线程程序内部，一个线程可以专门向另一个线程发送信号。使用 `pthread_kill` 函数来实现这一点。它的第一个参数是线程号，第二个参数是信号号。

### 4.5.2 `clone` 系统调用 `The clone System Call`

尽管在同一个程序中创建的 GNU/Linux 线程被实现为独立的进程，但它们共享虚拟内存空间和其他资源。然而，通过 `fork()` 创建的子进程会获得这些项目的副本。那么第一类型的进程是如何创建的？

Linux `clone` 系统调用是 `fork` 和 `pthread_create` 的通用形式，它允许调用者指定调用进程与新创建进程之间共享哪些资源。此外，`clone` 要求你为新进程使用的执行栈指定内存区域。虽然我们在这里提到 `clone` 是为了满足好奇，但通常不应在程序中使用系统调用。使用 `fork` 创建新进程或使用 `pthread_create` 创建线程。

# 4.6 进程对比线程 `Processes Vs. Threads`

对于受益于并发的程序，决定使用进程还是线程可能是困难的。以下是一些指南，可以帮助你决定哪种并发模型最适合你的程序：

- 程序中的所有线程必须运行相同的可执行文件。相反，子进程可以通过 `exec` 函数运行不同的可执行文件。
- 一个错误的线程可能会损害同一进程中的其他线程，因为线程共享相同的虚拟内存空间和其他资源。例如，一个线程中通过未初始指针进行的内存写入可能会损坏另一个线程可见的内存。
- 反之，一个错误的进程不能这样做，因为每个进程都有程序内存空间的副本。
- 与创建新线程相比，为新进程拷贝内存会增加额外的开销。然而，只有在内存更改时才会执行复制，因此如果子进程只读取内存，这种代价是极微的。
- 需要细粒度并发的程序应使用线程，因为线程共享数据（然而，在线程间共享数据必须非常小心以避免竞态条件）。需要粗粒度并发的程序应使用进程，因为进程间共享数据是复杂的。

# 5.1 共享内存

由于内核不会对共享内存的访问进行同步，你必须提供自己的同步机制。例如，在数据写入内存之前，进程不应从其中读取数据，且两个进程不能同时向同一个内存位置写入。下一节将讨论避免这些竞态条件的常用策略。我们的示例程序仅展示了单个进程访问内存，以便关注共享内存机制，并避免示例代码中充斥着同步逻辑。

#### 5.1.2 内存模型

要使用共享内存段，必须由一个进程分配该段。然后，每个想要访问该段的进程都必须挂载（attach）。在完成对该段的使用后，每个进程都会释放该段。在某个时刻，必须由一个进程释放该段。

分配新的共享内存段会导致虚拟内存页的创建。对于所有想要访问该共享段的进程，应该只有一个进程去分配一个新的共享段。分配已有的段不会创建新页，但它会返回现有页的标识符。为了允许进程使用共享内存段，进程对其进行挂载，这会将从其虚拟内存到段页的映射条目加入其中。完成任务后，这些映射将被移除。当不再有进程想要访问这些共享内存段时，恰好有一个进程必须释放这些虚拟内存页。

所有共享内存段按系统大小的整数倍分配，系统大小是指一个内存页的字节数。在 Linux 系统上，页大小为 4KB，你应该通过调用 `getpagesize` 函数来获取该值。

#### 5.1.3 分配

进程使用 `shmget`（“获取共享内存”）来分配共享内存段。互不相关的进程可以通过指定相同的键值（key value）来访问同一个共享段。遗憾的是，其他进程可能也选择了相同的固定键值，这可能导致冲突。使用特殊常量 `IPC_PRIVATE` 作为键值可以保证创建一个新的内存段。

它的第二个参数指定段中的字节数。由于段是使用页分配的，实际分配的字节数会向上取整为页大小的整数倍数。

第三个参数是标志位值的按位或（bitwise or），用于指定 `shmget` 的选项。标志位值包括：

- `IPC_CREAT`——此标志表示将创建一个新段。在指定键值的同时创建一个新段。
- `IPC_EXCL`——此标志始终与 `IPC_CREAT` 一起使用，如果指定的段已存在，会导致 `shmget` 失败。因此，它要求进入的进程拥有一个“独占”段。如果没有给出现有段的键，`shmget` 将返回现有段而不是创建新段。
- 标志位——该值为 9 位，表示授予所有者、组以及控制对段访问的权限。执行位被忽略。任何指定权限的方法都是使用 `<sys/stat.h>` 中定义并在 `stat` 手册页第 2 节中记录的常量。例如，`S_IRUSR` 和 `S_IWUSR` 指定共享内存所有者的读、写权限，`S_IROTH` 和 `S_IWOTH` 指定其他用户的读、写权限。

在本示例中，`shmget` 创建一个新的共享内存段（或如果 `shm_key` 已使用，则访问现有段），该段对所有者可读可写，但对用户不可。

```c
int segment_id = shmget(shm_key, pagesize(), IPC_CREAT | S_IRUSR | S_IWUSR);
```

如果调用成功，`shmget` 返回一个段标识符。如果共享内存段存在，则会验证权限并确保该段未被标记为删除。

#### 5.1.4 挂载与卸载

为了使共享内存段可用，进程必须使用 `shmat`（“挂载共享内存”）。向其传递由 `shmget` 返回的共享内存标识符 `SHMID`。第二个参数是一个指针，指定你想在进程地址空间的何处映射共享内存；如果为 `NULL`，Linux 将选择一个可用地址。第三个参数是一个标志，可以包含以下内容：

- `SHM_RND` 表示第二个参数指定的地址应向下取整为页大小的倍数。如果你没有指定此标志，必须对传递 `shmat` 的第二个参数进行页对齐。
- `SHM_RDONLY` 表示该段将只读不写。
- 1. 权限位与文件使用的权限相同。它们在第 10.3 节“文件系统权限”中描述。

如果调用成功，它返回所挂载共享段的地址。通过调用 `fork` 创建的子进程会继承挂载的共享段；如果需要，它们可以卸载这些共享内存段。

当你完成对共享内存段的使用后，应使用 `shmdt`（“卸载共享内存”）卸载段。传递由 `shmat` 返回的地址。如果该段已被释放且是最后一个使用它的进程，则它会被移除。调用 `exit` 和 `exe` 族的任何函数会自动卸载段。

#### 5.1.5 控制与释放共享内存

`shmctl`（“控制共享内存”）调用返回有关共享内存段的信息并可以对其进行修改。第一个参数是共享内存标识符。

要获取有关共享内存段的信息，使用 `IPC_STAT` 作为第二个参数，并指向 `shmid_ds` 结构体的指针。

要移除一个段，将 `IPC_RMID` 作为第二个参数，并将 `NULL` 作为第三个参数。当挂载该段的最后一个进程最终卸载时，该段会被移除。

在完成共享内存段的使用后，应显式地使用 `shmctl` 释放它。查看 `shmctl` 手册页以了解对共享内存段可以执行的操作。

#### 5.1.6 示例程序

程序 5.1 展示了共享内存的使用。

```c
#include <stdio.h>
#include <sys/shm.h>
#include <sys/stat.h>

int main () {
    int segment_id;
    char* shared_memory;
    struct shmid_ds shmbuf;
    int segment_size;
    const int shared_segment_size = 0x6400;

    /* 分配一个共享内存段。 */
    segment_id = shmget(IPC_PRIVATE, shared_segment_size, IPC_CREAT | IPC_EXCL | S_IRUSR | S_IWUSR);

    /* 挂载段。 */
    shared_memory = (char*) shmat (segment_id, 0, 0);
    printf("shared memory attached at %p\n", shared_memory);

    /* 确定段的大小。 */
    shmctl(segment_id, IPC_STAT, &shmbuf);
    segment_size = shmbuf.shm_segs;
    printf("segment size: %d\n", segment_size);

    /* 向共享内存写入字符串。 */
    sprintf(shared_memory, "Hello, world.");

    /* 卸载共享内存段。 */
    shmdt(shared_memory);

    /* 在不同的地址重新挂载共享内存段。 */
    shared_memory = (char*) shmat (segment_id, (void*) 0x05000000);
    printf("shared memory reattached at address %p\n", shared_memory);

    /* 从共享内存打印字符串。 */
    printf("%s\n", shared_memory);

    /* 卸载共享内存段。 */
    shmdt(shared_memory);

    /* 释放共享内存段。 */
    shmctl(segment_id, IPC_RMID, 0);

    return 0;
}
```

#### 5.1.8 优点与缺点
