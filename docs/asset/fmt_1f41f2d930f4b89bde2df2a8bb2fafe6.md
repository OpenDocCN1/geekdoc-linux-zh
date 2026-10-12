
```c
/*
 * main.c
 *
 * Created on: Nov 18, 2019
 * Author: Keroles Shenouda
 * //
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>

pthread_mutex_t fill_mutex;
int arr[20];
int flag=1;
pthread_cond_t cond_var=PTHREAD_COND_INITIALIZER;

void fill() {
    int i=0;
    for(i=0;i<4;i++) {
        pthread_mutex_lock(&fill_mutex);
        pthread_mutex_unlock(&fill_mutex);
        sleep(1);
    }
}

void read() {
    int i=0;
    printf("Values filled in array are:\n");
    for(i=0;i<4;i++) {
        pthread_mutex_lock(&fill_mutex);
        printf("%d\n", arr[i]);
        pthread_mutex_unlock(&fill_mutex);
    }
}

int main() {
    int tid;
    pthread_t thread_id1, thread_id2;
    int ret;
    void *arg;
    ret=pthread_create(&thread_id1,NULL,fill,NULL);
    ret=pthread_create(&thread_id2,NULL,read,NULL);
    printf("Created threads:\n");
    pthread_join(thread_id1,NULL);
    pthread_join(thread_id2,NULL);
    return 0;
}
```

![](img/bc86631e65e541c1c58ec0ab72a978e0_183_0.png)

## 第 13 章：嵌入式 Linux 简介

### Pthread 条件变量

`Pthread` 条件变量与互斥锁（mutexes）结合使用，实现线程之间的通信和同步。条件变量允许一个或多个线程等待，直到某个条件变为真，该条件由另一个线程信号。线程库提供了一个用于条件的原始语：`pthread_cond_t`。

要使用 `pthread` 条件变量，必须对其进行初始化。初始化 `pthread` 条件变量有两种方式：

1. 使用 `PTHREAD_COND_INITIALIZER`：

```c
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
```

2. 在运行时使用 `pthread_cond_init()`：

```c
pthread_cond_t cond;
pthread_cond_init(&cond, NULL);
```

为了等待条件变为真，线程可以调用 `pthread_cond_wait()`。该函数会原子性地释放第二个参数指定的互斥锁，并将调用线程置于睡眠状态。当条件被信号时，该线程将唤醒并重新获取互斥锁。

```c
pthread_cond_wait(&cond, &mutex);
```

要发送条件信号，线程可以调用 `pthread_cond_signal()` 来唤醒一个等待线程，或者调用 `pthread_cond_broadcast(&cond)` 来唤醒所有等待线程。请注意，这些函数可以在持有关联互斥锁时被调用。

```c
pthread_cond_signal(&cond); // 唤醒一个等待线程
pthread_cond_broadcast(&cond); // 唤醒所有等待线程
```

这是一个如何使用 `pthread` 条件变量实现生产者-消费者模型的示例：

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

#define BUFFER_SIZE 10

int buffer[BUFFER_SIZE];
int count = 0;
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

void* producer(void* arg) {
    int i;
    for (i = 0; i < 100; i++) {
      pthread_mutex_lock(&mutex);
      while (count == BUFFER_SIZE) {
        pthread_cond_wait(&cond, &mutex);
      }
      buffer[count++] = i;
      pthread_mutex_unlock(&mutex);
      pthread_cond_signal(&cond);
    }
    return NULL;
}

void* consumer(void* arg) {
    int i, data;
    for (i = 0; i < 100; i++) {
        pthread_mutex_lock(&mutex);
        while (count == 0) {
            pthread_cond_wait(&cond, &mutex);
        }
        data = buffer[--count];
        pthread_mutex_unlock(&mutex);
        printf("Consumed: %d\n", data);
        pthread_cond_signal(&cond);
    }
    return NULL;
}

int main() {
    pthread_t producer_thread, consumer_thread;
    pthread_create(&producer_thread, NULL, producer, NULL);
    pthread_create(&consumer_thread, NULL, consumer, NULL);
    pthread_join(producer_thread, NULL);
    pthread_join(consumer_thread, NULL);
    return 0;
}
```

在这个示例中，生产者线程用从 0 到 99 的整数填充缓冲区，而消费者线程负责移除并打印它们。`pthread_cond_wait()` 和 `pthread_cond_signal()` 函数用于确保消费者线程一直等待直到缓冲区中有数据。

### Socket 编程

```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, char *argv[]) {
    int sockfd;
    struct sockaddr_in addr;
    socklen_t len = sizeof(addr);

    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    addr.sin_family = AF_INET;
    addr.sin_port = htons(8080);
    addr.sin_addr.s_addr = INADDR_ANY;

    bind(sockfd, (struct sockaddr *)&addr, sizeof(addr));
    listen(sockfd, 3);

    while(1) {
        int client_fd;
        client_fd = accept(sockfd, (struct sockaddr *)&addr, &len);
        printf("Connection received\n");
        close(client_fd);
    }
    return 0;
}
```

![](img/bc86631e65e541c1c58ec0ab72a978e0_186_0.png)
