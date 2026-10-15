
```c
pthread_mutex_unlock(mutex);

ret = 0;

}

else {

    int status;

    waitpid(pid, &status, 0);

    printf("Child returned %d\n", WEXITSTATUS(status));

    pthread_mutex_lock(mutex);

    (*pcount)++;

    pthread_mutex_unlock(mutex);

    printf("Count = %d\n", *pcount);

    pthread_mutex_destroy(mutex);

}

munmap(mem, 1024*sizeof(int));

shm_unlink("/shm");

return ret;

}
```

父进程的第一要工作是设置一个父子进程之间共享的互斥锁。一旦完成，父进程就会 `fork` 出一个子进程。随后，父进程等待子进程完成。当子进程被 `fork` 时，它会接收父进程的副本。这使其能够访问共享内存段以及段中包含的互斥锁和变量。子进程获取互斥锁，增加共享变量，并在取消挂载和取消链接内存段之前释放互斥锁。

### 204 第5章 使用 POSIX 线程

## 消息队列

消息队列是线程或进程间传递消息的方法。消息可以放入队列中，并按优先顺序读取。

要挂载到消息队列，需要调用 `mq_open()` 函数，它将返回消息队列的句柄。消息队列应以 `/` 开头，后面最多 13 个字符。标志需要 `O_RDONLY`、`O_WRONLY` 或 `O_RDWR` 以产生只读、只写或读写的消息队列。

该 `open` 调用将打开现有的消息队列，如果队列不存在则失败。如果传递额外的标志 `O_CREATE`，则在队列不存在时创建它。额外的标志 `O_EXCL` 可以确保调用仅在队列不存在时才成功。如果传递了 `O_CREATE`，`mq_open()` 调用需要两个参数：用于设置消息队列访问权限的模式以及指向消息队列属性的指针；如果此指针为空，则对消息队列使用默认值。

消息队列的属性存储在 `mq_attr` 结构中，包含字段 `mq_maxmsg`（消息队列中可以包含的消息数）和 `mq_msgsize`（存储在消息队列中的消息的最大尺寸）。

传递给 `mq_open()` 的另一个标志是 `O_NONBLOCK`。如果设置了此标志，向满队列写入或从空队列读取将失败并立即返回。默认情况下会阻塞直到消息队列有空间发送消息，或有消息可读。

`mq_close()` 函数接收消息队列句柄作为参数，将关闭与消息队列的连接。消息队列将继续存在。要从系统移除消息队列，必须调用 `mq_unlink()`，它接收消息队列的名称作为参数。在调用 `mq_unlink()` 后，当所有对该消息队列的引用都关闭时，消息队列将被移除。

## 进程间的共享信号量

正如前面所述，信号量可以与其他进程共享。5.58 显示了命名的信号量。

### 命名的信号量

```c
#include <unistd.h>
#include <stdio.h>
#include <semaphore.h>
int main()
{
    int status;
    sem_t * semaphore;
    pid_t f = fork();
    semaphore = sem_open("/my_semaphore", O_RDWR|O_CREAT, 0777, 1);
    if (f == 0) {
        /* 子进程 */
        printf("Child process\n");
        sem_post(semaphore);
        sem_close(semaphore);
    }
    else {
        sem_wait(semaphore);
        printf("Parent process\n");
        sem_close(semaphore);
    }
    sem_unlink("/my_semaphore");
}
```

列表 5.59 打开和关闭消息队列

```c
#include <mqueue.h>
int main()
{
    mq_attr attr;
    mqd_t queue;
    attr.mq_maxmsg = 1000;
}
```

## 多进程编程 185

消息队列是优先级的先进先出（FIFO）队列。使用调用 `mq_send()` 将消息添加到队列中，如果队列是用 `mq_receive()` 创建的，则可以使用 `O_NONBLOCK` 属性从队列接收消息。这些这些函数无论执行成功都会立即返回。这些函数还有其他版本，如果执行失败，会在超时后返回：使用 `mq_timedsend()` 和 `mq_timedreceive()`，它们接受一个无符号整数；以及 `mq_retimedsend_np()` 和 `mq_retimedreceive_np()`，它们接受一个相对时间。

`mq_send()` 的参数是消息队列、指向包含消息大小的缓冲区指针以及优先级。高优先级消息将放在低优先级消息之前，放在具有相同或更高优先级消息之后。消息将从缓冲区拷贝到队列中。如果消息大小大于队列的 `mq_msgsize` 属性，则 `mq_send()` 调用将失败。

`mq_receive()` 调用接收消息队列、用于拷贝消息的缓冲区指针、缓冲区大小，以及一个空指针或一个用于写入消息优先级的无符号整数指针。如果缓冲区大小小于消息大小，则调用将失败。

注意，发送消息至少需要对消息执行两次拷贝操作——一次拷贝到队列中，一次从队列拷贝出来。因此，建议发送短消息并使用共享内存传递较长的信息。

列表 5.60 显示了父子进程之间发送消息的示例。在 Solaris 上，该代码需要使用编译器 `-lrt` 与实时扩展库进行链接。

### 列表 5.60 父进程与子进程之间传递消息

```c
#include <unistd.h>
#include <stdio.h>
#include <mqueue.h>
#include <string.h>
int main()
{
    int status;
    pid_t f = fork();
if ( f == 0 )
    /* 子进程 */
    mq_t queue;
    char message[20];
    queue = mq_open("/messages", O_WRONLY+O_CREATE, 0777, 0);
    strncpy(message, "Hello", 6);
    printf("send message %s\n", message);
    mq_send(queue, message, strlen(message)+1, 0);
    mq_close(queue);
    printf("Child process completed\n");
} else
{
    mq_t queue;
    char message[2000];
    queue = mq_open("/messages", O_RDONLY+O_CREATE, 0777, 0);
    mq_receive(queue, message, 2000, 0);
    printf("Receive message %s\n", message);
    mq_close(queue);
    mq_unlink("/messages");
    printf("Parent process completed\n");
}
```
