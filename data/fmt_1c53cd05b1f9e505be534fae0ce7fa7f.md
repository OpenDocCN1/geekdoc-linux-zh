
```
39 void *
40 produce(void *arg)
41 { for { ; ; } {
42     pthread_mutex_lock(&shared->mutex);
43     if (shared->nput >= nitems)
44         pthread_mutex_unlock(&shared->mutex);
45         return (NULL); /* 数组满了，我们完成了 */
46     }
47     shared->buf[shared->nput] = shred->nval;
48     shared->nput++;
49     shared->nval++;
50     pthread_mutex_unlock(&shared->mutex);
51     *(int *)arg) += 1;
52 }
53 
54 void *
55 consume(void *arg)
56 {
57     int i;
58     for (i = 0; i < nitems; i++) {
59         if (shared->buf[i] != i)
60             printf("*buff[%d] = %d\n", i, shared->buf[i]);
61     }
62     return (NULL);
63 }
```

## 生成数据项

生产者的临界区域包括对是否完成的测试：

```c
if (shared->nput >= nitems)
shared->buf[shared->nput] = shred->nval;
shared->nput++;
shared->nval++;
```

随后是这三行：

使用互斥锁保护此区域，确保在完成后解锁互斥锁。注意，计数元素（通过指针 `arg`）不属于临界区域的一部分，因为每个线程都有自己的计数器（`ean` 函数中的 `count` 参数）。因此，我们没有将此行代码包含在互斥锁锁定的区域内，因为根据通用编程原则，我们应该尽量减少被互斥锁锁的代码量。

## 消费者验证数组内容

消费者验证数组中的每个项目是否正确，如果发现错误则打印消息。正如我们之前所说，该函数的实例只在所有生产者线程完成后运行，因此不需要任何同步。

# 锁定与等待

如果我们运行设计的程序，指定一百万个项目和五个生产者线程，我们得到：

```
solaris % prodcons2 1000000 5
count[0] = 167165
count[1] = 248991
count[2] = 194221
count[3] = 192185
count[4] = 190988
```

正如提到的，如果我们在 Solaris 2.6 中移除对 `set-concurrency` 的调用，则 `count [0]` 将变为 1000000，其余计数均为 0。

如果我们从这个示例中移除互斥锁锁定，它会失败，正如预期的。也就是说，消费者发现了许多 `buff[i]` 不等于 `i` 的情况。我们还可以验证，如果只运行一个生产者线程，移除互斥锁没有影响。

我们证明了互斥锁用于锁定而不能用于等待。我们修改上一节的生产者-消费者示例，在所有生产者线程启动后立即启动消费者线程。这让消费者线程在生产者线程生成数据时进行处理，而在图 7.2 中，我们直到所有生产者线程完成才启动消费者。但在这里我们同步消费者与生产者，以确保消费者只处理生产者已经存储的项目。

图 7.4 显示了 `main` 函数。所有声明行都没有更改。

```c
14 int
15 main(int argc, char **argv)
16 {
17     int i, nthreads, count[MAXTHREADS];
18     pthread_mutex_t tid_mutex[MAXTHREADS], tid_consumer;
19     if (argc < 3)
20         err("usage: prodcons <items> <threads>");
21     items = atoi(argv[1]);
22     nthreads = atoi(argv[2]);
23     /* 设置并发级别 */
24     Set_concurrency(nthreads);
25     for (i = 0; i < nthreads; i++) {
26         count[i] = 0;
27         pthread_mutex_init(&tid_mutex[i], NULL);
28     }
29     /* 创建所有生产者 */
30     for (i = 0; i < nthreads; i++) {
31         pthread_create(&tid_produce[i], NULL, produce, &count[i]);
32     }
33     /* 创建一个消费者 */
34     pthread_create(&tid_consumer, NULL, consume, NULL);
35     /* 等待所有生产者 */
36     for (i = 0; i < nthreads; i++) {
37         pthread_join(tid_produce[i], NULL);
38     }
39     /* 等待消费者 */
40     pthread_join(tid_consumer, NULL);
41     exit(0);
42 }
```

# 条件变量：等待与信号

根本问题是：当所需项目未准备绪时我们该怎么办？我们在 7.5 中做的只是再次循环，每次解锁并锁定互斥锁。这被称为自旋（spinning），是对 CPU 时间的浪费。

我们也可以睡眠一段时间，但我们不知道需要睡多久。我们需要的是另一种同步类型，允许线程（或进程）睡眠直到某些事件发生。

互斥锁始终与条件变量关联。当我们调用 `pthread_cond_wait` 等待某些条件为真时，我们指定条件变量的地址和关联互斥锁的地址。

我们通过上一节的示例解释条件变量的使用。图 7.6 显示了全局声明。

## 将生产者和互斥锁收集到结构中

变量 `nput` 和 `nval` 与互斥锁关联，我们将所有三个变量放入名为 `put` 的结构中。该结构被生产者使用。

## 将计数器、条件和互斥锁收集到结构中

下一个结构 `nready` 包含一个计数器、一个条件变量和一个互斥锁。我们将条件变量初始化为 `PTHREAD_COND_INITIALIZER`。

`main` 函数没有从图 7.4 变化。

### 互锁与条件变量

```c
#include "unpipc.h"

#define MAXITEMS             100000
#define MAXTHREADS            100

/* 线程共享的全局变量 */
int                                     /* 生产者和消费者只读 */
int                     buf[MAXITEMS];
struct {
    pthread_mutex_t mutex;
    int                               /* 下一个存储的索引 */
    int                               /* 下一个要存储的值 */
} put = {
    PTHREAD_MUTEX_INITIALIZER
};
struct {
    pthread_mutex_t mutex;
    pthread_cond_t cond;
    int                               /* 准备好给消费者数量 */
    nready;
} ready = {
    PTHREAD_MUTEX_INITIALIZER, PTHREAD_COND_INITIALIZER
};
```

*图 7.6 用于生产者-消费者模型的全局变量，使用了条件变量。*

`produce` 和 `consume` 函数发生了变化，我们在图 7.7 中展示了它们。

### 将下一个项放入数组

当生产者将新项放入数组时，我们使用互斥锁 `put.mutex` 来锁定临界区。

### 通知消费者

我们增加计数器 `ready.n`，它记录了准备好供消费者的项数。在递增之前，如果计数器的值为 0，我们会调用 `pthread_cond_signal` 来唤醒任何可能等待该值变为非零的线程（例如消费者）。现在我们可以看到与此计数器相关的互斥锁和条件变量的操作。该计数器在生产者和消费者之间共享，因此在关联的互斥锁（`ready.mutex`）锁定时，必须对其进行访问。条件变量用于等待和信号通知。

### 消费者等待 ready.n 非零
