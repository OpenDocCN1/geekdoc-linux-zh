
三种类型的互斥锁初始化器如表 15.1 所示。

| 类型 | 说明 |
| :--- | :--- |
| `PTHREAD_MUTEX_INITIALIZER` | 快速互斥锁 |
| `PTHREAD_RECURSIVE_MUTEX_INITIALIZER` | 递归互斥锁 |
| `PTHREAD_ERRORCHECK_MUTEX_INITIALIZER` | 错误检查互斥锁 |

递归互斥锁是一种特殊的互斥锁，允许同一线程多次锁定。注意 `_NP` 后缀表示它们不可移植。错误检查互斥锁可以帮助在线程尝试锁定它已持有的互斥锁时发现错误。

![](img/0b91ab9198b0fdfd5649d5d19571459e_284_0.png)

现在来看一个将这些函数结合的示例，以说明为什么互斥锁在多线程应用中很重要。在这个示例中，你基于之前提供任务创建和连接基础设施的应用程序进行构建。考虑列表 15.7 中的示例。在第 4 行，你创建互斥锁并将其初始化为快速互斥锁。在线程中，你的工作是增加受保护计数器的若干次数。这对于每个线程都会发生

# 第 15 章 POSIX 线程 (Pthreads) 编程 265

10)，所以你需要保护变量免受多次访问。你通过首先锁定互斥锁，然后在增加受保护的变量后解锁，将变量自增操作放置在临界区内。这确保了每个任务对执行自增的资源具有独占访问权限，并保护其免受损坏。最后，在第 52 行，你使用 `pthread_mutex_destroy()` 函数销毁互斥锁。

列表 15.7 使用互斥锁在临界区保护变量（位于 CD-ROM 中的 `./source/ch15/ptmutex.c`）

``` 
1: #include <pthread.h>

2: #include <stdio.h>

3: 

4: pthread_mutex_t cntr_mutex = PTHREAD_MUTEX_INITIALIZER;

5: 

6: long protVariable = 0;

7: 

8: void *myThread(void *arg)

9: {

10: int i, ret;

11: 

12: for (i = 0; i < 10000; i++) {

13: 

14: ret = pthread_mutex_lock(&cntr_mutex);

15: 

16: assert(ret == 0);

17: 

18: protVariable++;

19: 

20: ret = pthread_mutex_unlock(&cntr_mutex);

21: 

22: assert(ret == 0);

23: 

24: }

25: 

26: pthread_exit(NULL);

27: }

28: 

29: #define MAX_THREADS 10

30: 

31: int main()

32: {

33: int ret, i;

34: pthread_t threadIds[MAX_THREADS];

35:

36: for (i = 0; i < MAX_THREADS; i++) {

37: ret = pthread_create(&threadIds[i], NULL, myThread,

NULL);

38: if (ret != 0) {

39: printf("Error creating thread %d\n",

(int)threadIds[i]);

40: }

41:

42:

43: for (i = 0; i < MAX_THREADS; i++) {

44: ret = pthread_join(threadIds[i], NULL);

45: if (ret != 0) {

46: printf("Error joining thread %d\n",

(int)threadIds[i]);

47: }

48: 

49:

50: printf("The protected variable value is %ld\n",

protvariable);

51:

52: ret = pthread_mutex_destroy(&cntr_mutex);

53:

54: if (ret != 0) {

55: printf("Couldn't destroy the mutex\n");

56: }

57: 

58: return 0;

59: }

```

使用互斥锁时，将临界区内执行的工作量减少到真正需要执行的部分是非常重要的。因为其他线程会在互斥锁解锁之前一直阻塞，因此缩短临界区的时间可以获得更好的性能。

## 线程条件变量

现在你已经处理了互斥锁，可以探索条件变量了。条件变量是一种特殊的线程结构，允许线程根据条件唤醒另一个线程。互斥锁提供了一种简单的同步形式（基于互斥锁的锁定状态），而条件变量是一个线程等待事件而另一个线程信号该事件发生的手段。在这里，事件可以意味着任何内容。线程可以在互斥锁上阻塞，但可以在任何条件变量上等待。将它们想象成等待队列，这正是 GNU/Linux 中的实现方式。

考虑这样一个线程等待特定条件被满足的问题。如果你使用互斥锁，线程必须轮询以获取互斥锁、检查条件，如果没有发现有工作要做（条件不满足），则释放互斥锁。那种种忙循环会导致应用程序性能低下，并且需要避免。

pthreads API 提供了许多支持条件变量的函数。这些函数提供了变量的创建、等待、信号和销毁。条件变量 API 函数所示如下：

```
int pthread_cond_wait(pthread_cond_t *cond,pthread_mutex_t * mutex);
int pthread_cond_timedwait(pthread_cond_t *cond,pthread_mutex_t * mutex,const struct timespec *absime);
int pthread_cond_signal(pthread_cond_t *cond);
int pthread_cond_broadcast(pthread_cond_t *cond);
int pthread_cond_destroy(pthread_cond_t *cond);
```

要创建一个条件变量，你只需要创建一个类型为 `pthread_cond_t` 的变量。你通过将其设置为 `PTHREAD_COND_INITIALIZER` 来初始化它（类似于互斥锁的创建和初始化）。演示如下：

```
pthread_cond_t recoveryCond = PTHREAD_COND_INITIALIZER;
```

条件变量需要一个与其关联的互斥锁，你可以像之前学过的那样创建它：

```
pthread_mutex_t recoveryMutex = PTHREAD_MUTEX_INITIALIZER;
```

现在来看一个等待条件的线程。在这种情况下，你在调用条件变量之前锁定互斥锁。演示如下：

```
pthread_mutex_lock(&recoveryMutex);
// ... check condition ...
pthread_cond_wait(&recoveryCond, &recoveryMutex);
pthread_mutex_unlock(&recoveryMutex);
```

如果满足条件，则向线程发送信号。要向一个线程发送信号，你调用以下代码：

```
pthread_mutex_lock(&recoveryMutex);
pthread_cond_signal(&recoveryCond);
pthread_mutex_unlock(&recoveryMutex);
```

如果你需要唤醒所有线程，则使用广播。演示如下：

```
pthread_mutex_lock(&recoveryMutex);
pthread_cond_broadcast(&recoveryCond);
pthread_mutex_unlock(&recoveryMutex);
```

pthreads API 还支持条件变量的超时等待版本。该函数 `pthread_cond_timedwait` 允许调用者指定一个表示何时放弃并返回的绝对时间。返回 `TIMEDOUT` 值表示函数是因为超时而不是成功返回的。以下代码片段说明了它的用法：

```
struct timeval currentTime;
struct timespec expireTime;
int ret;
assert(pthread_mutex_lock(&recoveryMutex) == 0);
gettimeofday(&currentTime, NULL);
expireTime.tv_sec = currentTime.tv_sec + 1;
expireTime.tv_nsec = currentTime.tv_usec * 1000;
ret = 0;
while (workload <= MAX_NORMAL_THREADS) && (ret != TIMEDOUT) {
```
