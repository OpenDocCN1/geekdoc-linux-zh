
多个线程共享同一个 CPU 通常会导致性能产生更大的线性下降，原因包括活跃线程之间切换的成本、缓存中用数据的驱逐以及在虚拟 CPU 之间迁移线程的成本。值得注意的是，每个线程都需要一些内存占用，线程的激增是导致内存短的原因之一。

需要观察的关键点是，活跃线程多于虚拟 CPU 只能降低每个线程的工作速率。有一种情况，线程多于虚拟 CPU 可能会获益。睡眠或阻塞等待资源的线程不消耗 CPU，并且不会影响活跃线程的性能。这的一个例子是有许多线程在等待磁盘或网络活动完成。

让许多线程等待磁盘 I/O 完成可能是很有用的。在这种情况下，改进具有等待 I/O 的应用程序性能是一个关键问题——主线程可以继续，而子线程等待 I/O 请求的完成。

列表 9.29 中的代码可以用于演示存在其他活跃线程时，单线程的性能如何受到损害。代码测量了

# 第 9 章 使用多核心处理器的扩展

主线程完成其工作需要很长时间。然而，在主线程开始计时区域之前，它会创建多个子线程，这些线程会在锁上自旋，直到主线程完成工作。

## 列表 9.29 展示过度订阅（Oversubscription）成本的代码

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <sys/time.h>

double now()
{
    struct timeval time;
    gettimeofday(&time, 0);
    return (double)time.tv_sec + (double)time.tv_usec / 1000000.0;
}

#define COUNT 100000000
volatile int stop = 0;

void *spin(void *id)
{
    while (!stop) { }
}

int main(int argc, char *argv[]) {
    pthread_t threads[256];
    int nthreads = 1;
    if (argc > 1) { nthreads = atoi(argv[1]); }
    nthreads--;
    for(int i=0; i<nthreads; i++) {
        pthread_create(&threads[i], 0, spin, (void*)0);
    }

    double start=now();
    int total = 0;
    for(int h=0; h<COUNT; h++) {
        total += (total << 2) ^ (total | 33556);
        if (total == 0) printf("total==0\n");
    }
    double end=now();
    printf("Time %f a\n", end - start );
    stop = 1;
    for(int i=0; i<nthreads; i++)
    {
        pthread_join(threads[i], 0);
    }
    return 0;
}
```

图 9.6 显示了代码在具有四个虚拟 CPU 的系统上的运行时间。该代码的运行时间取决于每个 CPU 的软件线程数量。如果有八个或更多软件线程，运行运行时间至少是四个或更少线程时的两倍。图了两线：一条表示如果运行时间随线程数线性扩展，代码将如何运行；另一条线显示了代码的实际运行时间。在 64 个线程之后，显然过度订阅导致运行时间超过了基于线性扩展的预期值。换句话说，在约 64 个线程之后，系统性能受到过度订阅的影响。

![](img/9337ae7b0be66cc11725becaa009908f_392_0.png)

图 9.6 过度订阅系统的扩展

## 使用处理器绑定改进内存局部性

线程迁移是指线程在一个虚拟处理器上启动，但最终迁移到另一个虚拟处理器的情况。如果新的虚拟处理器与原始虚拟处理器共享同一个核心，或者与它共享缓存，则这种迁移的成本就很低。对于多核心处理器，如果线程的新位置与旧位置共享相近级别的缓存，那么线程迁移的影响往往是微小的。然而，如果迁移是从一个物理芯片到另一个物理芯片，成本可能会非常高。

线程迁移的成本之一与线程正在使用的数据现在位于旧处理器的缓存中有关。数据需要被获取到新进程的缓存中。重要的是，这可能是一种缓存传输，类似于伪共享（false sharing）的情况。对于某些系统，从另一个处理器的缓存中获取数据的成本可能比从内存中获取更低。然而，在某些系统中，从另一个缓存中获取数据的成本可能比从内存中获取更高。典型原因是数据在新处理器获取它之前需要先进行存储。

然而，在多处理器系统中，线程迁移还有一个额外的潜在成本。现代操作系统对内存子系统的拓扑结构有一定的了解。因此，操作系统可以为线程提供延迟最低的内存。遗憾的是，如果线程被迁移，它可能会位于一个内存延迟高得多的处理器上。这个问题导致系统尝试将线程保留——尽管不一定是在它们原始的位置，也要保持在共享相同内存延迟的虚拟 CPU 组内。

这引发了局部性组（locality groups）的概念，即共享相同内存访问延迟的线程组。如果线程在局部性组内移动，内存延迟成本不会发生变化；迁移成本只是线程移动到可能冷缓存缓存的微小代价。

Linux 提供了 `numactl` 工具，既可以查询硬件拓扑结构，又允许用户指定应用程序运行的虚拟处理器。列表 9.30 显示了 `numactl` 的输出，表明系统有两个节点、处理器以及每个节点关联的内存量。

### 9.30 来自 Linux 的 NUMA 特性

```
$ numactl --hardware
available: 2 nodes (0-1)
node 0 size: 2047 MB
node 0 free: 88 MB
node 1 size: 1983 MB
node 1 free: 136 MB
```

Solaris 提供了 `lgprinfo` 工具报告拓扑结构。对于某些系统，从另一个处理器的缓存中获取数据的成本可能比从内存中获取更低。然而，在某些系统中，从另一个缓存中获取数据的成本可能比从内存中获取更高。典型原因是数据在新处理器获取它之前需要先存储。

然而，在多处理器系统中，线程迁移还有一个额外的潜在成本。现代操作系统对内存子系统的拓扑结构有一定的了解。因此，操作系统可以为线程提供延迟最低的内存。遗憾的是，如果线程被迁移，它可能会位于一个内存延迟高得多的处理器上。这个问题导致系统尝试将线程保留——尽管不一定是在它们原始的位置，也要保持在共享相同内存延迟的虚拟 CPU 组内。

Solaris 提供了 `lgprinfo` 工具报告拓扑。对于某些系统，从另一个处理器的缓存中获取数据的成本可能比从内存中获取更低。然而，在某些系统中，从另一个缓存中获取数据的成本可能比从内存中获取更高。典型原因是数据在新处理器获取它之前需要先存储。

# 扩展到操作系统的限制

```c
printf("Time %14.2f ns Binding %i/s\n",
    (end - start) * 1000000000.0 / ((double)SIZE), (int)param);
} else { perror("Error"); }
```

```c
int main(int argc, char* argv[])
{
    pthread_t thread;
    int nthreads = 1;
    int i;
    if (argc > 1) { nthreads = atoi(argv[1]); };
    setup();
    for(i=0; i<nthreads; i++) {
        pthread_create(&thread, 0, use, (void*)i);
        pthread_join(thread, 0);
    }
    return 0;
}
```

该代码可以运行，但需要提供两个关键例程。简单的方法是提供 `now()` 例程，它以双精度类型返回当前时间（秒）。系统函数 `gettimeofday()` 在 *NIX* 上提供了一种可移植的方法，用于获取自系统启动以来的秒和微秒。9.33 显示了将此封装为返回双精度 类型的代码。

## 列表 9.33 返回当前秒数时间的代码

```c
double now()
{
    struct timeval time;
    gettimeofday(&time, 0);
    return (double)time.tv_sec + (double)time.tv_usec / 1000000.0;
}
```

控制线程运行的位置不是可移植的。列表 9.34 中的代码显示了如何使用 Solaris 的 `processor_bind()` 来控制线程到虚拟处理器的绑定。变量 `P_LWPID` 和 `P_MYID` 将调用线程绑定到特定的虚拟处理器。

## 列表 9.34 在 Solaris 上控制处理器绑定
