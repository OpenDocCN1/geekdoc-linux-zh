

## 10.7.4 条件属性

条件变量仅有的属性是进程共享属性和时钟属性。这些是高级主题，此处不涉及。有几个与条件属性相关的函数，具体用于获取和设置这些属性，它们由各自的手册页描述：

```
int pthread_condattr_destroy   ( pthread_condattr_t *attr);
int pthread_condattr_init      ( pthread_condattr_t *attr);
int pthread_condattr_getclock  ( const pthread_condattr_t *restrict attr,
                                 clockid_t *restrict clock_id);
int pthread_condattr_setclock  ( pthread_condattr_t *attr,
                                 clockid_t clock_id);
int pthread_condattr_getpshared( const pthread_condattr_t *restrict attr,
                                 int *restrict pshared);
int pthread_condattr_setpshared( pthread_condattr_t *attr,
                                 int pshared);
```

## 10.7.5 示例

清单10.8包含一个使用互斥锁和两个条件变量解决单生产者/单消费者问题的多线程方案。为简单起见，它被设计为在每个线程迭代固定次数后终止。它将输出消息发送到工作目录中名为`prodcons_mssges`的文件。缓冲区例程向共享的全局缓冲区添加一个整数，并从中移除一个整数。生产者和消费者中调用这些函数的代码位于由互斥锁`buffer_mutex`保护的区域内。

消费者逻辑稍微复杂一些，因为生产者在缓冲区为空时可能会退出。因此，消费者线程在阻塞于`data_available`条件之前，必须先检查生产者是否仍然存活；否则它将永远挂起而无法终止，`main()`也会如此。

生产者在退出时将标志`producer_exists`置零是不够的，因为消费者可能在生产者将其置零之前刚刚检查过该值，并且看到`producer_exists == 1`，从而阻塞在`data_available`条件上。这就是为什么生产者在退出时要执行以下代码行：

```
pthread_mutex_lock(&buffer_mutex);
producer_exists = 0;
pthread_cond_signal(&data_available);
pthread_mutex_unlock(&buffer_mutex);
```

它首先锁定`buffer_mutex`。如果消费者持有该锁，它将阻塞直到消费者释放该锁。这意味着要么消费者刚刚获得互斥锁并即将阻塞在`data_available`条件上，要么它正在从缓冲区获取数据并很快会解锁互斥锁。无论哪种情况，消费者都会释放锁，生产者会将`producer_exists`置零，然后发出`data_available`信号。如果消费者正要在`data_available`上阻塞自己，那么该信号会唤醒它，它将看到`producer_exists`为零，然后退出。如果它正在从缓冲区获取数据然后释放了互斥锁，之后生产者获得了该锁，那么当它再次获得该锁时，producer_exists 将为零，并且如果缓冲区为空，它也会退出。

### 清单10.8：单生产者/单消费者多线程程序。

```
#include <sys/time.h>
#include <sys/types.h>
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <errno.h>

/********************************************************************************
                              Global, Shared Data
********************************************************************************/
#define NUM_ITERATIONS 500   /* number of loops each thread iterates */
#define BUFFER_SIZE    20    /* size of buffer */
/* buffer_mutex controls buffer access */
pthread_mutex_t buffer_mutex = PTHREAD_MUTEX_INITIALIZER;

/* space_available is a condition that is true when the buffer is not full */
pthread_cond_t space_available = PTHREAD_COND_INITIALIZER;

/* data_available is a condition that is true when the buffer is not empty */
pthread_cond_t data_available = PTHREAD_COND_INITIALIZER;

int producer_exists;   /* true when producer is still running */
FILE *fp;              /* log file pointer for messages */

/********************************************************************************
                              Buffer Object
********************************************************************************/
int buffer[BUFFER_SIZE]; /* the buffer of data — just ints here */
int bufsize;             /* number of filled slots in buffer */

void add_buffer(int data)
{
    static int rear = 0;
    buffer[rear] = data;
    rear = (rear + 1) % BUFFER_SIZE;
    bufsize++;
}

int get_buffer()
{
    static int front = 0;
    int i;
    i = buffer[front];
    front = (front + 1) % BUFFER_SIZE;
    bufsize--;
    return i;
}
```

