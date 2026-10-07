
通过调用如下 `ResetEvent` 例程，可以将事件对象置于重置状态：

```
BOOL ResetEvent ( HANDLE event );
```

`PulseEvent` 函数提供了一个单一操作，它可以将指定事件对象的状态设置为（已信号）状态，并在释放相应数量的等待线程后将其重置（为（非信号）状态）。对于手动重置事件对象，所有可以立即释放的等待线程都将被释放。然后，该函数将事件对象的状态重置为非信号状态并返回。对于自动重置事件对象，函数在释放一个等待线程后会将状态重置为非信号状态并返回，即使有多个线程在等待。如果没有线程在等待，或者没有线程可以被释放，`PulseEvent` 仅会将事件对象状态设置为非信号状态并返回。注意，对于线程而言，使用 `WaitForMultipleObjects` 函数等待所有指定对象变为信号状态可以将事件对象的状态设置为信号状态并重置为非信号状态，而不会导致等待函数返回。这发生在并非所有指定对象都同时变为信号的情况下。`PulseEvent` 例程的调用方式如下：

```
BOOL PulseEvent ( HANDLE event );
```

## 临界区 (Critical Sections)

临界区是 Win32 API 另一种并发控制机制。临界区仅在单个进程内有效，涉及定义一个临界数据结构并使用四个例程：

```
CRITICAL_SECTION cs;
```

```
InitializeCriticalSection(&cs);
```

```
EnterCriticalSection(&cs);
```

```
LeaveCriticalSection(&cs);
```

```
DeleteCriticalSection(&cs);
```

参数 `cs` 是为临界数据结构选择的名称。临界数据结构的初始化在程序开始时完成。`EnterCriticalSection` 和 `LeaveCriticalSection` 调用放置在临界代码周围。`DeleteCriticalSection` 调用应在进程终止时执行。然而，`EnterCriticalSection` 和 `LeaveCriticalSection` 部分可以多次调用，但“进入”调用次数必须等于“离开”调用次数，否则会发生意外结果。示例 2-1 展示了临界区的使用。此示例与示例 2-2 相同，后者使用了互斥锁（mutexes）来强制执行互斥。

### 示例 2–4 临界区例程演示

```
#include <windows.h>
#include <stdlib.h>
#include <iostream.h>

volatile INT gblktr;
CRITICAL_SECTION critsect;

void ThreadKr(INT arg) {
    INT l1ktr;
    INT i;

    for (i=0; i<arg; i++) {
        EnterCriticalSection(&critsect);
        l1ktr=gblktr;
        l1ktr++;
        gblktr=l1ktr;
        LeaveCriticalSection(&critsect);
    }
}

void main(void) {
    HANDLE knthHandle[4];
    DWORD threadID[4];
    INT i;

    gblktr=0;
    InitializeCriticalSection(&critsect);

    // 创建三个线程
    for(i=0; i<=3; i++) {
        knthHandle[i]=CreateThread(0, 0, (LPTHREAD_START_ROUTINE) ThreadKr, (void*)0, 0, &threadID[i]);
        if (knthHandle[i]==0)
            cout << "Cannot create thread " << GetLastError() << endl;
    }

    WaitForMultipleObjects(4, knthHandle, TRUE, INFINITE);
    DeleteCriticalSection(&critsect);
    cout << "Global counter = " << gblktr << endl;
}
```

## UNIX 中的并发控制函数

UNIX 包含了一系列并发例程，允许创建以下机制：

- 信号量 (Semaphores)
- 条件变量 (Condition variables)
- 读写锁 (RW locks)

信号量分为两种类型：POSIX 和 System V。两者在 Solaris 和 Red Hat Linux 上可用。System V 信号量的工作方式与 POSIX 类型不同；它们使用起来不够直接，但提供了 POSIX 信号量不具备的功能。互斥锁和读写锁通过允许线程获取锁来控制对共享资源的访问。此处理解的协议是：一旦获取锁，线程即可继续执行临界区中的代码。此时任何其他尝试获取锁的线程将被挂起。当线程完成临界区操作后，它释放锁允许任何其他线程获取。互斥锁和读写锁都基于这一前提工作。然而，读写锁可以以读模式或写模式访问共享资源。（详情请参见“POSIX 条件变量”章节。）

## 信号量——POSIX 线程

POSIX 线程信号量例程在 Sun Solaris 和 Red Hat 环境中可用，并需要 `semaphore.h`。调用序列如下：

```
int sem_init(sem_t *sem, int pshared, unsigned int value);

int sem_wait(sem_t *sem);

int sem_trywait(sem_t *sem);

int sem_post(sem_t *sem);

int sem_getvalue(sem_t *sem, int sval);

int sem_destroy(sem_t *sem);
```

`sem_init()` 函数用于初始化由 `sem` 指代的无名信号量。参数 `value` 指有多少个资源需要同步访问。该信号量可以在后续调用的 `sem_wait()`、`sem_trywait()`、`sem_post()` 和 `sem_destroy()`中使用。该信号量一直有效直到被销毁。参数 `pshared` 在表 2.2 中解释。

### 2.2 信号量共享参数的影响

| pshared 的值 | 含义 |
|---|---|
| 0 | 无法与其他进程共享，仅供进程内的线程使用 |
| 1 | 可由其他进程的线程共享 |

一旦通过 `sem_init()` 初始化信号量，在临界区代码周围使用 `sem_wait()` 和 `sem_post()`：

```
sem_wait(sem_t *sem); /* P(S) 或 Wait(S)

// 临界区代码

sem_post(sem_t *sem); /* V(S) 或 Signal(S)
```

`sem_trywait()` 例程用于有条件的获取信号量。调用此例程时，如果信号量可用（其值大于 0），将获取信号量。如果信号量可用，其值小于或等于 0；此例程将返回 -1并将 `errno` 变量设置为 BUSY。

`sem_getvalue()` 例程返回信号量的当前值。此处建议谨慎，因为此值可能会由于其他并发的 `sem_wait()` 或 `sem_post()` 调用而改变。示例 2-5 是对示例 2-3 中 Microsoft Windows 下 Visual C/C++ 生产者/消费者场景的还原。

### 示例 2-5 使用 POSIX 信号量完成生产者/消费者

```
#include <pthread.h>
#include <stdlib.h>
#include <stdio.h>
#include <errno.h>
#include <semaphore.h>
#include <errno.h>

#define numBufs 10

extern void Producer();
extern void Consumer();
extern void error_rpt(int err, char *fp);

sem_t full, empty, mutex;

char pData, cData;
char Buffer[numBufs];
```

示例 2-5 使用 POSIX 信号量完成生产者/消费者（续）

```
char alphaBeta[] = {'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 
'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'W', 'X', 'Y', 'Z'};

pindexX=0, cindexX=0, i=0, oktr=0, rval;

pthread_t pHandle, cHandle;

void Producer()
{
    printf("Producer thread starting\n");
    while(i) {
        /* 生产数据 ... */
        pData = alphaBeta[i++];
        sem_wait(&empty);
        sem_wait(&mutex);
        /* 将数据加入缓冲区 ... */
        Buffer[pindexX++] = pData;
        pindexX = pindexX%numBufs;
        sem_post(&mutex);
        sem_post(&full);
    }
    printf("Producer thread exiting\n");
}
```

```
void Consumer()
{
    printf("Consumer thread starting\n");
    for(oktr=0; oktr < 26; oktr++) {
        sem_wait(&full);
        sem_wait(&mutex);
        /* 从缓冲区中移动数据 ... */
        cData = Buffer[cindexX++];
        cindexX = cindexX%numBufs;
        sem_post(&mutex);
        sem_post(&empty);
        /* ... 使用数据 ... */
        printf("%s\n", cData);
    }
    printf("\nConsumer thread exiting ... 终止生产者\n");
    pthread_exit(0);
}
```

```
void error_rpt(int errnum, char *api)
{
    char *errstr;
    errstr = dterror(errnum);
    fprintf(stderr, "%error: %s\n", api, errstr);
    exit(-1);
}
```

## UNIX 中的并发控制函数

59

### 示例 2-5 使用 POSIX 信号量完成生产者/消费者模型（继续）

```c
main()
{
    sem_init(&full, 0, 0);
    sem_init(&empty, 0, numBufs);
    sem_init(&mutex, 0, 1);
    /* create the threads */
    rval=pthread_create(&pHandle, (pthread_attr_t *)NULL,
        (void (*)() Producer, (void *)NULL);
    if (rval != 0)
        error_rpt(rval, "pthread_create()");
    pthread_create(&cHandle, (pthread_attr_t *)NULL,
        (void (*)() Consumer, (void *)NULL);
    if (rval != 0)
        error_rpt(rval, "pthread_create()");
    /* wait for consumer thread to finish execution first */
    pthread_join(cHandle, (void **)NULL);
    printf("Main thread detected consumer thread termination\n");
    /* Now wait for the producer thread to finish */
    pthread_join(pHandle, (void **)NULL);
    printf("Main thread detected producer thread termination\n");
    exit(0);
}
```

## 信号量——System V 版本

System V 信号量是 UNIX IPC（进程间通信）例程的一部分，涉及三个例程：`semctl()`、`semop()` 和 `semget()`。这些例程并不容易使用，本节将讨论一种特定的实现。这些例程在信号集已建立的基础上运行。本章的讨论将仅说明包含单个信号量的信号集。在示例 2-6 中，System V 例程将通过整合到一个服务库中，提供经典信号量函数 WAIT(S) 和 SIGNAL(S) 的效果。这些例程创建的信号量仅对单个进程的线程可见。这些例程的调用序列如下：

```c
int semget(key_t key, int nsems, int flags);
```

# 第2章 控制并发活动

此例程用于返回信号量 ID。该 ID 在其他 System V 信号量例程中表示这组信号量。参数 `key` 包含一个使信号量 ID 唯一的数值。在示例 2-6 中，`key` 将被设置为 `IPC_PRIVATE`。参数 `nsems` 代表信号集中的信号量数量。对于任何用户来说，一个信号量通常足够了。`flags` 参数用于控制各种选项，例如访问权限和创建控制。例程 `semop()` 用于对信号集执行操作，其调用方式如下：

```c
int semop(int sid, struct sembuf(*ops)[], int nops);
```

参数 `sid` 代表从调用 `semget` 获取的信号量 ID。参数 `ops` 是指向信号量操作结构数组的指针。最后一个参数 `nops` 是数组中此类结构的数量。信号量操作结构所示：

```c
short sem_num  /* 信号量编号 */
short sem_op   /* 信号量操作 */
short sem_flg   /* 操作标志位 */
```

基本上，如果 `sem_op` 被设为负值，则该值将从由 `sem_num` 参数指定的信号量值中减去。这类似于 WAIT(S) 或 P(S) 函数。如果 `sem_op` 是正值，则将其加到由 `sem_num` 参数指定的信号量值。这类似于 SIGNAL(S) 或 V(S) 函数。

例程 `semctl` 可用于查询或更改某些特性，例如所有者、最后使用时间以及权限。此例程还可以用于确定有多少进程正在等待特定的信号量，以及最后一个更改该信号量的进程 ID。`semctl` 的调用序列如下：

```c
int semctl(int sid, int semnum, int cmd, [semun]);
```

参数 `sid` 代表从调用 `semget` 获取的信号量 ID。参数 `semnum` 代表要执行 `cmd` 操作的信号量。表 2.3 表示了 `cmd` 参数可以设置的一些值。

| 表 2.3 semctl 命令参数 | 描述 |
| :--- | :--- |
| GETVAL | 返回此信号量的值 |
| SETVAL | 将信号量的值设置为 semnum 参数指定的值 |
| IPC_RMID | 从系统中移除指定的信号量标识符并销毁相关的信号集和数据结构 |

## 示例 2-6 System V 信号量例程演示

```c
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/sem.h>
#include <errno.h>
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
int semid, i;
pthread_t threadids[4];
int counter;
void *KTRead (void *arg) {
    int x, i;
    for(i=0; i<250000; i++){
        wait(semid);
        x = counter;
        x++;
        counter = x;
        signal(semid);
    }
}
main() {
    union semun {
        int val;
        struct sem_ds *buf;
        ushort *array;
        int arg;
    } arg;
    if((semid = semget(IPC_PRIVATE, 1, 0666|IPC_CREAT)) == -1)
        perror("semget error");
    arg.val = 1;
    if(semctl(semid, 0, SETVAL, arg) == -1)
```
