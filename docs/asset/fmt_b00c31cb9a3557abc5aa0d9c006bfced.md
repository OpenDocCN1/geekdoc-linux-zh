
```c
#include <sys/ipc.h>
#include <sys/shm.h>
#include <stdio.h>
#include <unistd.h>

void(void)
/*
列表 3.4.c - 子进程更改父进程共享内存中的数据
*/
{
    struct area { /* 共享内存区域 */
    int value; /* (一个简单的示例) */ /
} area, *ap;

    int flag = (IPC_CREAT | IPC_EXCL | 0660);
    int size = sizeof(struct area);
    key_t key = 0x01020304; /* 示例 */
    int shmid; /* 共享内存区域 id */
    int pid; /* 子任务进程 id */

/* 获取共享内存区域 * */
shmid = shmget(key, size, flag);

/* 附加共享内存区域 * */
```

### 列表 3.4 续

```c
ap = (struct area *) shmat(shmid, 0, 0);

/* 初始化值 */
ap->value = 0;
printf("父进程：值为 %d\n", ap->value);

if((pid = fork()) == 0) { /* 子进程 */
    /* 更改共享内存 */
    ap->value = 100;
    printf("子进程：值为 %d\n", ap->value);
    sleep(2);
    exit(0);
} else { /* 父进程 */
    while(1) {
        printf("父进程值为 %d\n", ap->value);
        fflush(stdout);
        if(ap->value != 0) {
            break;
        }
        printf("继续中...\n");
        sleep(1);
    }
    printf("拜!\n");
}

/* 移除共享内存 */
shmdt(ap);

/* 再次修改 */
ap->value = 200;
printf("父进程值为 %d\n", ap->value);

/* 父进程等待子任务退出 */
waitpid(pid, NULL);

/* 释放共享内存区域 */
shmctl(shmid, IPC_RMID, (struct shmid_ds *) 0);

return;
```

## 在共享数据中使用信号

注意

注意添加 `sleep` 调用只是为了减慢速度。如果没有这些 `sleep` 调用，一切发生得太快，以至于事件的顺序可能并不明显。尝试在不带 `sleep` 的情况下运行它。实验得越多，学得越多，记得越深。

## 在共享数据中使用信号量

列表 3.4 中的共享数据示例并没有说明与共享变量相关的风险。考虑一个类似的示例，父账户创建了两个子任务：一个负责存款，另一个负责取款，每个在处理时都计算新余额。你能看到风险吗？

如果两个交易同时到达——一个存款，一个取款——存在一种很小的可能性，其中一个失效。假设取款进程从共享内存获取余额，减去取款金额并被存款进程中断。存款进程从共享内存获取余额（取款进程仍持有的），增加存款，将余额放回共享内存，并等待。取款进程继续处理，将其重新计算的余额放入共享内存，覆盖了存款进程设置的值。交易丢失了，因为存款进程的所有操作都被该中断抵消了。

这里感兴趣的研究概念是关键区：你如何确保进程在从共享内存获取余额开始处理后，在放入重新计算的余额时不会取消另一个交易？通过使用信号量保护共享数据的完整性。

什么是信号量？首先，考虑它不是什么：信号量并不阻止另一个进程修改共享数据，就像红灯并不阻止你进入路口一样。我们在绿灯通过，黄灯减速，红灯停止。信号量也是如此。

每个信号量与共享资源相关，不是直接相关，而是通过源码注释和其他文档间接相关。信号量要么已设置要么未设置，这就是操作系统关心的全部。如果你尝试设置一个信号量，操作系统将设置它。如果你尝试设置一个已设置的信号量，操作系统将导致你的进程等待，直到最后一个进程将其清除。

为了避免银行交易示例中的任何困难，两个进程（存款和取款）必须在从共享内存获取余额之前设置信号量，并在重新计算的余额放回后清除它（见列表 3.5）。

这有时被称为对资源序列化（serializing on a resource），意味着对资源执行的任何操作必须一次一次、按顺序进行。（你可以在本章末尾“扩展阅读”部分包含的文本中找到更多相关信息。）

# 列表 3.5 存款与取取的同步处理

```c
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/sem.h>
#include <stdio.h>
#include <unistd.h>

main(void)
/*
** Listing3.5.c - 存款与取取的同步处理
*/
    struct area {   /* 共享区域 */
        int balance;
        int deposit;
        int withdrawal;
    } area, *ap;
#if defined(__GNU_LIBRARY__) && !defined(__SEM_MUN_UNDEFINED)
/* union semun 通常通过包含 <sys/sem.h> 定义 */
#else
    /* 否则我们必须根据 <bits/sem.h> 自己定义它 */
union union
{
    int val;
    /* SETVAL 的值 */
    struct semid_ds *buf;    /* 用于 IPC_STAT, IPC_SET 的缓冲区 */
    unsigned short int *array; /* 用于 GETALL, SETALL 的数组 */
    struct seminfo *__buf;   /* 用于 IPC_INFO 的缓冲区 */
};
#endif
union semun; /* 信号量联合和缓冲区 */
struct sembuf buf;

    int flag = (IPC_CREATE | IPC_EXCL | 0660);
    int size = sizeof(struct area);
    key_t skey = 0x04030201; /* 示例键 */
    key_t mkey = 0x01020304;
```

### 列表 3.5 继续

```c
int semid; /* 信号量 id */
int shmid; /* 共享内存 id */
int pid0; /* 存款子任务 pid */
int pid; /* 取款子任务 pid */
int amount;
char inbuf[80];
```

```c
/* 获取共享内存区域 */
shmid = shmget(key, size, flag);

/* 挂载共享内存区域 */
ap = (struct area *) shmat(shmid, 0, 0);

/* 在共享内存中初始化账户信息 */
ap->balance = 1000; /* 初始化余额为 $1000 */
ap->withdrawal = 0;
ap->deposit = 0;
```

```c
/* 获取并初始化信号量 */
semid = semget(key, 1, flag);
/* 设置信号量可用 */
un.val = 1;
semctl(semid, 0, SETVAL, un);
/* 第一个唯一的信号量 */
nbuf.sem_num = 0;
/* 如果设置则等待 */
nbuf.sem_flg = 0;
```

```c
if((pidD == fork()) == 0) /* 存款 */
{
/* 挂载父进程的共享内存 */
ap = (struct area *) shmat(shmid, 0, 0);
/* 注意：shmid 仍然正确设置 */
```

```c
/* 处理存款 */
while(1)
{
sleep(1);

/* 设置信号量_op */
nbuf.sem_op = -1;
semop(semid, (struct sembuf *)&nbuf, 1);
```

# 第 3 章 进程间通信

### 列表 3.5 继续

```c
if(ap->deposit < 0)
    break; /* 退出请求 */
```

```c
if(ap->deposit > 0)
{
    /* 处理存款 */
    ap->balance += ap->deposit;
    ap->deposit = 0; /* 清空 */
}
```

```c
/* 清空信号量 */
buf.sem_op = 1;
semop(semid, (struct sembuf *) &buf);
```
