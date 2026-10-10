
`ret = pthread_cond_timedwait(&recoveryCond, &recoveryMutex, &expireTime);`

}

if (`ret == TIMEDOUT`) {

    /* Timeout - 执行超时处理 */

} else {

    /* Condition met - 执行条件恢复处理 */

}

assert(`pthread_mutex_unlock(&recoveryMutex) == 0`);

```
这里需要的最后一个函数是 `pthread_cond_destroy`。你只需将条件变量传递给该函数，如下：
```

```
pthread_cond_destroy(&recoveryCond);
```

需要注意的是，在 GNU/Linux 实现中，没有任何资源实际上挂载到条件变量上，因此此函数简单地检查当前是否有线程正在等待该条件变量。

现在是时候看一个完整的示例了，它汇聚了我们讨论的关于条件变量的所有元素。这个示例在生产者和消费者的语文中阐述了条件变量。你创建一个生产者线程来创建工作，然后创建 N 个消费者线程对这些（模拟的）工作进行操作。

第一个列表（Listing 15.8）显示了主程序。该列表与之前创建和连接线程的示例相似，但有几处变化。你在此中创建了两种类型的线程。在第 18–21 行，你创建了若干消费者线程，在第 24 行，你创建了一个生产者线程。我们很快就会查看它们。在创建完最后一个线程后，你连接（join）了生产者线程（导致主应用程序挂起，直到它完成）。你等待工作完成（通过一个简单的计数器 `workCount` 来标识）。你希望消费者线程完成它们的工作，因此你等待该变量变为零，表示所有工作均已消费。

第 33-36 行的代码块显示了消费者线程的连接，但有一处有趣的变化。在这个示例中，消费者线程永远不会退出，因此你可以使用 `pthread_cancel` 函数来取消它们。该函数的原型如下：

```c
int pthread_cancel(pthread_t thread);
```

这允许你在完成某个线程的任务后将其终止。在这个示例中，你已经生产了消费者需要处理的工作，因此你可以顺序取消每个线程（第 34 行）。最后，你分别在第 37 和 38 行销毁了你的条件变量和互斥锁。

+ 列表 15.8 生产者/消费者示例初始化和 main（位于 CD-ROM 上的 `/source/ch15/pthread.cond`）

```c
1:  #include <pthread.h>
2:  #include <stdio.h>

4:  pthread_mutex_t cond_mutex = PTHREAD_MUTEX_INITIALIZER;
5:  pthread_cond_t condition = PTHREAD_COND_INITIALIZER;

7:  int workCount = 0;

9:  #define MAX_CONSUMERS  10

int main(void())
{
    int i;
    pthread_t consumers[MAX_CONSUMERS];
    pthread_t producer;
    /* 产生消费者线程 */
    for ( i = 0; i < MAX_CONSUMERS; i++) {
        pthread_create(&consumers[i], NULL,
            consumerThread, NULL);
    }
    /* 产生单个生产者线程 */
    pthread_create(&producer, NULL,
        producerThread, NULL);
    /* 等待生产者线程 */
    pthread_join(producer, NULL);
    while (workCount > 0) {
        /* 取消并连接消费者线程 */
        for ( i = 0; i < MAX_CONSUMERS; i++) {
            pthread_cancel(consumers[i]);
        }
        pthread_mutex_destroy(&cond_mutex);
        pthread_cond_destroy(&condition);
    }
    return 0;
}
```

接下来，你可以查看生产者线程函数（Listing 15.9）。生产者线程的目的是生产工作，通过增加 `workCount` 变量来模拟。非零的 `workCount` 表示有工作可做。如第 8–22 行所示，循环若干次创建工作。正如条件变量示例所示，首先在第 10 行锁定你的互斥锁，然后在第 14 行使用 `pthread_cond_broadcast` 函数通知消费者（工作者）线程。这会通知任何等待中的消费者线程，现在有工作可以做了。接下来，在第 15 行，你解锁互斥锁，允许消费者线程锁定互斥锁并执行它们的工作。

在第 20–22 行，你只是进行一些忙碌工作以允许内核调度另一个任务（为了说明目的，这避免了同步行为）。
当所有工作生产完成后，你允许生产者线程退出（在 Listing 15.8 的第 28 行于主函数中被连接）。

# 列表 15.9 条件变量的生产者线程示例（位于 CD-ROM 上的 `/source/ch15/ptcond.c`）

```c
void *producerThread(void *arg) {
    int i, j, ret;
    double result=0.0;
    printf("Producer started\n");
    for (i = 0; i < 30; i++) {
        ret = pthread_mutex_lock(&cond_mutex);
        if (ret == 0) {
            printf("Producer: Creating work %d\n", workCount);
            workCount++;
            pthread_cond_broadcast(&cond_mutex);
            pthread_mutex_unlock(&cond_mutex);
        } else {
            assert(0);
        }
    }
    for (j = 0; j < 60000; j++) {
        result = result + (double)random();
    }
    printf("Producer finished\n");
    pthread_exit(NULL);
}
```

现在是时候看消费者线程了（见 Listing 15.10）。你的第一个任务是分离（第 5 行），然后进入循环（第 8–22 行）。你首先在第 9 行锁定互斥锁，并在第 11 行等待条件。然后你在第 12 行检查是否有工作。如果是，你递减计数（第 13 行），执行你的工作（第 14 行），并在第 15 行释放互斥锁。注意，因为你正在广播（第 14 行），你可能没有工作要做（在情况下，在第 19 行递减计数），你释放互斥锁（第 20 行）并正常终止线程（第 25 行）。

# 列表 15.10 消费者线程示例（位于 CD-ROM 上的 `/source/ch15/ptcond.c`）

```c
void *consumerThread(void *arg) {
    int i, ret;
    printf("Consumer started\n");
    while (1) {
        ret = pthread_mutex_lock(&cond_mutex);
        if (ret == 0) {
            while (workCount == 0) {
                pthread_cond_wait(&condition, &cond_mutex);
            }
            workCount--;
            printf("Consumer: Performed work %d\n", workCount);
            pthread_mutex_unlock(&cond_mutex);
        } else {
            assert(0);
        }
        // 忙碌工作
        for (i = 0; i < 60000; i++) {
            // 无
        }
    }
}
```
