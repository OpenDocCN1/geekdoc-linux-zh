
`int pthread_cond_signal(pthread_cond_t *cond);`

`int pthread_cond_broadcast(pthread_cond_t *cond);`

`int pthread_cond_destroy(pthread_cond_t *cond);`

要创建一个条件变量，只需声明一个类型为 `pthread_cond_t` 的变量。使用 `PTHREAD_COND_INITIALIZER` 初始化它：

```c
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
```

条件变量需要关联一个互斥锁。通过以下代码演示：

```c
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
```

## POSIX 线程

让我们来看使用条件变量的示例。在这个示例中，有一个线程等待条件满足，另一个线程在条件满足时发送信号。条件是一个简单的标志位。

```c
#include <pthread.h>
#include <stdio.h>
#include <assert.h>
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
int ready = 0;
void *workerThread(void *arg) {
    pthread_mutex_lock(&mutex);
    while (!ready) {
        printf("工作线程等待条件...\n");
        pthread_cond_wait(&cond, &mutex);
    }
    printf("条件满足！处理中...\n");
    pthread_mutex_unlock(&mutex);
    return NULL;
}
int main() {
    pthread_t thread;
    pthread_create(&thread, NULL, workerThread, NULL);
    // 模拟工作
    pthread_mutex_lock(&mutex);
    ready = 1;
    pthread_cond_signal(&cond);
    pthread_mutex_unlock(&mutex);
    pthread_join(thread, NULL);
    return 0;
}
```

`pthread_cond_wait` 外围的 `while` 循环是关重要的，因为存在“虚假唤醒”，即使没有发送信号，线程也可能被唤醒。循环确保在继续执行之前条件已满足。

线程 API 还支持条件的超时等待版本。该函数 `pthread_cond_timedwait` 允许调用者指定一个放弃的绝对时间。返回值为 `TIMEDOUT`，表示函数是因为超时而不是成功返回的。以下代码段演示了其用法：

```c
struct timeval currentTime;
struct timespec expireTime;
int ret;
ssert(pthread_mutex_lock(&mutex) == 0);
gettimeofday(&currentTime);
expireTime.tv_sec = currentTime.tv_sec + 1;
expireTime.tv_nsec = currentTime.tv_usec * 1000; // 这是为了示例进行的简化
ret = 0;
while (!ready && (ret != TIMEDOUT)) {
    ret = pthread_cond_timedwait(&cond, &mutex, &expireTime);
}
if (ret == TIMEDOUT) {
    /* 超时 - 执行超时处理 */
} else {
    /* 条件满足 - 执行条件恢复处理 */
}
ssert(pthread_mutex_unlock(&mutex) == 0);
```

# POSIX 线程 (Pthreads) 编程 225

从我们的标准条件处理（在本例中为恢复）开始，然后需要互斥锁。

这里需要注意的最后一个函数是 `pthread_cond_destroy`。我们只需将条件变量传递给它，例如：

```c
pthread_mutex_destroy(&RecoveryCond);
```

需要注意的是，在 GNU/Linux 实现中，实际上没有资源附加到条件变量上，该函数仅仅是检查是否有任何线程正在等待该条件变量。

现在，让我们来看一个完整的示例，它结合了上面讨论的关于条件变量的所有元素。在这个示例中，我们将在生产者和消费者的语境下说明条件变量。我们将创建一个生产者线程来创建工作任务，并创建 `$N$` 个消费者线程来对这些（模拟的）工作进行操作。

我们的第一个代码列表（列表 14.8）显示了主程序。该代码列表与我们之前创建和连接线程的示例相似，但有几处变化。在这个列表中，我们创建了两种线程。在第 18–21 行，我们创建了若干消费者线程，在第 24 行，我们创建了一个单一的生产者线程。我们很快会查看这些。在创建最后一个线程后，我们连接生产者线程（这将导致主应用程序挂起，直到其完成）。然后我们等待工作完成（通过一个简单的计数器 `workcount` 来标识）。我们希望允许消费者线程完成它们的工作，因此我们一直等到该变量为零，表示所有工作均已消费。

第 33–36 行的代码块显示了对消费者线程的连接（join），但有一个有趣的改变。在这个示例中，消费者线程永远不会退出，因此我们使用 `pthread_cancel` 函数来取消它们。该函数的原型为：

```c
int pthread_cancel(pthread_t thread);
```

这允许我们在完成对某个线程的操作后终止它。在这个示例中，我们已经了消费者需要处理的工作，因此我们按顺序取消每个线程（第 34 行）。最后，我们分别在第 37 和第 38 行销毁我们的条件变量。

- **列表 14.8** 生产者/消费者示例初始化和 main 函数（位于光盘的 `/source/ch14/ptcond.c`）

```c
1: #include <pthread.h>
2: #include <stdio.h>
3:
4: pthread_mutex_t cond_mutex = PTHREAD_MUTEX_INITIALIZER;
5: pthread_cond_t condition = PTHREAD_COND_INITIALIZER;
6:
7: int workCount = 0;
8:
9: #define MAX_CONSUMERS 10
10:
11: int main()
12: {
13:     int i;
14:     pthread_t consumers[MAX_CONSUMERS];
15:     pthread_t producer;
16:
17:     /* 产生消费者线程 */
18:     for ( i = 0; i < MAX_CONSUMERS ; i++ ) { { 
19:         pthread_create(&consumers[i], NULL,
20:             consumerThread, NULL );
21:     }
22:
23:     /* 产生单一生产者线程 */
24:     pthread_create(&producer, NULL,
25:             producerThread, NULL );
26:
27:     /* 等待生产者线程 */
28:     pthread_join(producer, NULL );
29:
30:     while ((workCount > 0));
31:
32:     /* 取消并连接消费者线程 */
33:     for ( i = 0; i < MAX_CONSUMERS ; i++ ) { 
34:         pthread_cancel(consumers[i]);
35:     }
36:
37:     pthread_mutex_destroy(&cond_mutex);
38:     pthread_cond_destroy(&condition);
39:
40:     return 0;
41: }
```

接下来，让我们来看生产者线程函数（列表 14.9）。生产者的目的是产生工作，通过增加 `workCount` 变量来模拟这一点。非零的 `workCount` 表示有工作可做。正如第 8–22 行所示，我们循环若干次来创建工作。正如条件变量示例所示所示，我们首先在第 10 行锁定互斥锁，然后创建要执行的工作（增加 `workCount`）。随后，我们在第 14 行使用 `pthread_cond_broadcast` 函数通知等待中的消费者（工作）线程。这将通知任何等待中的消费者线程，现在有工作可以做了。接下来，在第 15 行，我们解锁互斥锁，允许消费者线程锁定互斥锁并执行它们的工作。

在第 20–22 行，我们只需做一些忙工作以允许内核调度另一个任务（为了说明，这避免了同步行为）。

当所有工作产生完成后，我们允许生产者线程退出（它将在列表 14.8 的第 28 行的主函数中被连接）。

```c
1:  void *producerThread(void *arg)
2:  {
3:      int i, j, int ret;
4:      double result=0.0;
5:      
6:      printf("Producer started\n");
7:      
8:      for (i = 0; i < 30; i++) {
9:      
10:         ret = pthread_mutex_lock(&cond_mutex);
11:         if (ret == 0) {
12:             printf("Producer: Creating work %d\n", workCount);
13:             workCount++;
14:             pthread_cond_broadcast(&condition);
15:             pthread_mutex_unlock(&cond_mutex);
16:         } else {
17:             pthread_mutex_unlock(&cond_mutex);
18:         }
19:         
20:         for (j = 0; j < 1000; j++) {
21:             result = (double)rand();
22:         }
23:     }
24:     
25:     printf("Producer finished\n");
26:     pthread_exit(NULL);
27: }
```
