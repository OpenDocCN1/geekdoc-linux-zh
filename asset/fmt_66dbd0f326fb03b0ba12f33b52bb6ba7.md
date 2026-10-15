
```c
void *thread_function(void *arg) {
    char message[] = "Hello World";
    int thread_finished = 0;

int main() {
    int res;
    pthread_t a_thread;

    pthread_attr_t thread_attr;
    res = pthread_attr_init(&thread_attr);
    if (res != 0) {
        perror("Attribute creation failed");
        exit(EXIT_FAILURE);
    }

    res = pthread_attr_setdetachstate(&thread_attr, PTHREAD_CREATE_DETACHED);
    if (res != 0) {
        perror("Setting detached attribute failed");
        exit(EXIT_FAILURE);
    }

    res = pthread_create(&a_thread, &thread_attr, thread_function, (void *)message);
    if (res != 0) {
        perror("Thread creation failed");
        exit(EXIT_FAILURE);
    }
    pthread_thread_destroy(&a_thread);
    while (!thread_finished) {
        printf("Waiting for thread to say it's finished...\n");
        sleep(1);
    }

    printf("Other thread finished, bye!\n");
    exit(EXIT_SUCCESS);
}

void *thread_function(void *arg) {
    printf("thread_function is running. Argument %s\n", (char *)arg);
    sleep(4);
    printf("Second thread setting finished flag, and exiting now\n");
    thread_finished = 1;
    pthread_exit(NULL);
}
```

输出结果并没有意外：

```
$ ./threads
Waiting for thread to say it's finished...
thread_function is running. Argument was Hello World
Waiting for thread to say it's finished...
```

## POSIX 线程

```
Waiting for thread to say it's finished...
Waiting for thread to say it's finished...
Second thread setting finished flag, and exiting now
Other thread finished, bye!
```

正如你所见，设置分离状态（`detached state`）允许辅助线程独立完成，而无需主线程等待它。

## 工作原理

代码中两个重要的部分是：

```c
pthread_attr_t thread_attr;

res = pthread_attr_init(&attr);
if (res != 0) {
    perror("Attribute creation failed");
    exit(EXIT_FAILURE);
}
```

这声明了一个线程属性并对其进行了初始化：

```c
res = pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
if (res != 0) {
    perror("Setting detached attribute failed");
    exit(EXIT_FAILURE);
}
```

将属性值设置为分离状态。

其他的细微差别在于创建线程时传递属性地址：

```c
res = pthread_create(&a_thread, &attr, thread_function, (void*)message);
```

以及，为了完整性，在我们在使用属性后销毁它们：

```c
pthread_attr_destroy(&attr);
```

## 线程属性—调度

让我们来看看我们想要更改的第二个线程：调度。更改调度属性与设置分离状态非常相似，但我们可以多可以使用两个函数来查找可用的优先级级别，`sched_priority_max` 和 `sched_priority_min`。

## 尝试一下—调度

由于这个 `thread.c` 与之前的示例非常相似，我们将查看差异。

1. 首先，我们需要一些额外的变量：

```c
int max_priority;
int min_priority;
struct sched_param scheduling_value;
```

2. 在设置了分离属性后，我们设置调度策略。

```c
res = pthread_attr_setschedpolicy(&thread_attr, SCHED_OTHER);
if (res != 0) {
    perror("Setting scheduling policy failed");
    exit(EXIT_FAILURE);
}
```

3. 接下来，我们找到允许的优先级范围：

```c
max_priority = sched_get_priority_max(SCHED_OTHER);
min_priority = sched_get_priority_min(SCHED_OTHER);
```

4. 并设置其中一个：

```c
scheduling_value.sched_priority = min_priority;
res = pthread_attr_setschedparam(&thread_attr, &scheduling_value);
if (res != 0) {
    perror("Setting scheduling priority failed");
    exit(EXIT_FAILURE);
}
```

## 工作原理

这与设置分离状态属性类似，不同在于设置的是调度策略。

## 取消线程

有时，我们希望一个线程能够请求另一个线程终止，就像向它发送信号一样。线程有办法做到，并且与信号处理并行，线程获得了一种修改其在请求终止时行为的方法。

让我们先看看请求线程终止的函数：

```c
#include <pthread.h>

int pthread_cancel(pthread_t thread);
```

这非常直接：给定一个线程标识符，我们可以请求取消它。在接收到取消请求时，线程的情况稍微复杂一点，但并不多。线程可以使用 `pthread_cancel` 取消它的取消状态。

```c
#include <pthread.h>

int pthread_cancelstate(int state, int *oldstate);
```

第一个参数是 `PTHREAD_CANCEL_ENABLE`（允许其接收取消请求）或 `PTHREAD_CANCEL_DISABLE`（导致这些请求被忽略）。`oldstate` 指针允许你获取之前的状态。

```c
#include <pthread.h>

int pthread_canceltype(int type, int *oldtype);
```

类型可以取两个值：`PTHREAD_ASYNCHRONOUS`（立即执行）或 `PTHREAD_DEFERRED`（让取消请求等待到取消点）。

```c
#include <pthread.h>

int pthread_canceltype(int type, int *oldtype);
```

根据标准，如果你对状态感兴趣，可以传递 `NULL`。

## POSIX Threads

在创建的线程中，我们首先将取消状态设置为允许取消。

```c
res = pthread_setcancelstate(PTHREAD_CANCEL_ENABLE, NULL);
if (res != 0) {
    perror("Thread pthread_setcancelstate failed");
    exit(EXIT_FAILURE);
}
```

然后，我们将取消类型设置为延迟。
