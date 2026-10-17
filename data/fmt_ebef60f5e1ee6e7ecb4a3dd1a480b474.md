
`semid` 和 `semnum` 参数标识要设置值的信号量集合及其内部元素。如果失败，`semelement` 返回 `-1` 并设置 `errno`（由 `semctl` 设置 `errno`）。

## 示例 15.6 removesem.c

`removesem` 函数删除 `semid` 标识的信号量。

```c
#include <sys/sem.h>

int removesem(int semid) {
  return semctl(semid, 0, IPC_RMID);
}
```

如果成功，`removesem` 返回 `0`。如果失败，`removesem` 返回 `-1` 并设置 `errno`（由 `semctl` 设置 `errno`）。

## 15.2.3 POSIX 信号量集合操作

`semop` 原子地对与标识符 `semid` 关联的信号量集合执行一组信号量操作。`sops` 参数指向元素操作数组，`nsops` 参数指定 `sops` 数组中的操作数量。

```c
语法概要 (SYNOPSIS)
#include <sys/sem.h>
int semop(int semid, struct sembuf *sops, size_t nsops);
```

POSIX:XSI

如果成功，`semop` 返回 `0`。如果失败，`semop` 返回 `-1` 并设置 `errno`。下表列出了 `semop` 的强制性错误。

| errno | cause |
|---|---|
| E2BIG | nsops 值太大 |
| EACCES | 调用者拒绝操作 |
| EAGAIN | 操作将阻塞进程但 (sem_flg & IPC_NOWAIT) != 0 |
| EBIG | sops 条目之一的 sem_num 值小于 0 或大于信号量集合中的元素数量 |
| EIDRM | 信号量标识符 semid 已从系统中移除 |
| EINTR | semop 被信号中断 |
| EINVAL | semid 值无效，或用于 SEM_UNDO 的信号量数量超过限制 |
| ENOSPC | 请求 SEM_UNDO 的进程限制已超过 |

### ERANGE 操作会导致 semval 值溢出

`semop` 函数在单个信号量集合上原子地执行 `sops` 数组中指定的所有操作。如果任何单个元素操作会导致进程阻塞，则进程将阻塞且不执行任何操作。

指定信号量元素操作的 `struct sembuf` 结构体包含以下成员：

- `short sem_num` 信号量元素的索引
- `short sem_op` 要执行的特定元素操作
- `short sem_flg` 用于指定操作选项的标志

`sem_op` 元素操作是指定信号量值变化量的。

- 如果 `sem_op` 是大于 `0` 的整数，`semop` 将该值加到相应的信号量元素值，并唤醒所有等待元素增加进程。
- 如果 `sem_op` 为 `0` 且信号量元素值不是 `0`，`semop` 阻塞调用进程（等待 `0`）并增加等待该元素零值的进程数计数。
- 如果 `sem_op` 是负数，只要结果不是负数，`semop` 就将 `sem_op` 值加到相应的信号量元素值。`semop` 在信号量元素增加事件上阻塞进程。如果结果值为 `0`，`semop` 唤醒等待 `0` 的进程。

`semop` 的描述假设所有元素操作 `sem_flg` 均为 `0`。如果 `sem_flg & IPC_NOWAIT` 为真，元素操作永远不会导致 `semop` 阻塞。如果 `semop` 返回会在该操作上阻塞，则它返回 `-1` 并设置 `errno` 为 `EAGAIN`。如果 `sem_flg & SEM_UNDO` 为真，函数还会修改进程的调整值。这种调整允许进程在退出时撤销其对信号量的影响。你应该仔细阅读手册页中关于 `semop` 与各种标志设置交互的内容。

## 示例 15.7

以下声明 `myopbuf` 并初始化使其 `sem_num` 为 `1`、`sem_op` 为 `1` 且 `sem_flg` 为 `0` 的代码哪里错误？

```c
struct sembuf myopbuf = {1, -1, 0};
```

答案：

直接赋值假设 `struct sembuf` 的成员按照 `sem_num`、`sem_op` 和 `sem_flg` 的顺序出现。你可能会在旧代码中看到这种写法，它在你的系统上可能有效，但请尽量避免。尽管 POSIX:X 扩展规定了 `struct sembuf` `sem_num`、`sem_op` 和 `sem_flg`，但标准并没有规定这些成员在定义中出现的顺序，也没有限制 `struct sembuf` 仅包含这些成员。

## 示例 15.8 sembuf.c

`sembuf` 函数以与实现无关的方式初始化 `struct sembuf` 结构成员 `sem_num` 和 `sem_flg`。

```c
#include <sys/sem.h>

void sembuf(struct sembuf *s, int num, int op, int flg) {
  s->sem_num = (short)num;
  s->sem_op = (short)op;
  s->sem_flg = (short)flg;
  return;
}
```

## 示例 15.9

以下代码使用示例 15.8 中的 `sembuf` 原子地将 `semid` 的零索引元素加 `1`，并将 `semid` 的另一个元素加 `2`。

```c
struct sembuf myop[2];
sembuf(myop, 0, 1, 0);
sembuf(myop + 1, 1, 2, 0);
if (semop(semid, myop, 2) == -1)
  perror("Failed to perform semaphore operation");
```

## 示例 15.10

假设一个包含两个元素的信号量集合 `S` 代表一个磁带驱动系统，其中进程 `1` 使用磁带 A，进程 `2` 使用磁带 B，进程 `3` 使用磁带 B。以下伪代码定义了信号量操作，允许进程以互斥的方式访问一个或两个驱动器。

```c
struct sembuf get_tapes[2];
struct sembuf release_tapes[2];
sembuf(&get_tapes[0], 0, 1, 0);
sembuf(&get_tapes[1], 1, -1, 0);
sembuf(&release_tapes[0], 0, 1, 0);
sembuf(&release_tapes[1], 1, 1, 0);
```

```c
Process 1:
  semop(S, get_tapes, 1);
  <use tape A>
  semop(S, release_tapes, 1);
Process 2: 
  semop(S, get_tapes, 2);
  <use tapes A and B>
  semop(S, release_tapes, 2);
Process 3: 
  semop(S, get_tapes + 1, 1);
  <use tape B>
  semop(S, release_tapes + 1, 1);
```

`S[0]` 代表磁带 A，`S[1]` 代表磁带 B。我们假设 `s_id` 的两个元素都初始化为 `1`。

如果 `semop` 被信号中断，它将返回 `-1` 并将 `errno` 设置为 `EINTR`。程序 15.2 显示了一个在 `semop` 被信号中断时重新启动操作的函数。

## 程序 15.2 r_semop.c

一个在信号后重新启动 `semop` 的函数。

```c
#include <errno.h>
#include <sys/sem.h>
int r_semop(int semid, struct sembuf *sops, int nsops) {
  while (semop(semid, sops, nsops) == -1)
    if (errno == EINTR)
      return -1;
  return 0;
}
```

程序 14.1 使用 POSIX:XI 信号量集合来保护关键区域。程序 15.3 调用了 `setsembuf`（示例 15.8）和 `removesemb`（示例 15.6）。即使程序没有捕获任何信号，如果在被信号中断，也会重新启动 `semop` 操作。你获得了重新启动可以将 `errno` 设置为 `EINTR` 的函数的好处。

一旦创建了信号量程序 15.3，它就会一直存在直到被删除。如果子进程产生错误，它将退出。如果父进程产生错误，它将跳过 `wait` 调用并删除信号量。为自己的使用创建信号量的程序应该确保在程序终止之前删除信号量。务必准确删除一次信号量。

## 程序 15.3 chainsemset.c

对程序 14.1 的修改，使用信号量集合来保护关键区域。

```c
#include <errno.h>
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/sem.h>
#include <sys/stat.h>
#include <sys/wait.h>
#include "restart.h"
#define BUSIZE 1024
#define PERMS (S_IRUSR | S_IWUSR)
int itelement(int semid, int semnum, int semvalue);
int r_semop(int semid, struct sembuf *sops, int nsops);
int removevesem(int semid);
void semctl(struct sembuf *s, int num, int op, int flg);
void printerror(char *msg, int error) {
  fprintf(stderr, "[%d] %s: %s\n", getpid(), msg, strerror(error));
}
int main(int argc, char *argv[]) {
    char buffer[MAX_CANON];
    char *c;
    pid_t childpid;
    int delay;
    int error;
    int i, j;
    int semid;
    struct sembuf sembuf;
    struct sembuf sembuf[1];
    if ((argc != 3) || ((n = atoi(argv[1])) <= 0 || (delay = atoi(argv[2])) < 0) {
        fprintf(stderr, "Usage: %s\n", argv[0]);
        return 1;
    }
    /* 创建信号量 */
    if ((semid = semget(SEM_PRIVATE, 1, PERMS)) == -1) {
        perror("Failed to create semaphore");
        return 1;
    }
    semctl(semid, 0, -1, 0); /* 递减元素 0 */
    semctl(semid, 0, 1, 0); /* 增加元素 0 */
    if (itelement(semid, 0, 1) == -1) {
        perror("Failed to initialize semaphore to 1");
        if (removevesem(semid) == -1)
            perror("Failed to remove semaphore");
        return 1;
    }
    for (i = 1; i < n; i++) {
        if ((childpid = fork()) == 0)
            break;
        printf(buffer, BUSIZE, "%i:PID:%d child:%d\n", i, (long)getpid(), (long)childpid);
        c = buffer;
        /* 入口区域 */
        if ((error = r_semop(semid, sembuf, 1)) == -1 && (i > 1)) {
            printerror("Failed to load lock", error);
            return 1;
        } else if (!error) {
            /* 关键区域开始 */
            while (*c != '\0') {
                fputs(c, stderr);
                c++;
                for (j = 0; j < delay; j++) ;
            }
            /* 退出区域 */
            if ((error = r_semop(semid, sembuf, 1)) == -1)
                printerror("Failed to unlock semaphore", error);
            /* 剩余区域 */
            if ((wait(NULL) == -1) && (errno != ECHILD)) {
                printerror("Failed to wait", errno);
                if ((i == 1) && (error = removevesem(semid)) == -1) {
                    printerror("Failed to clean up", error);
                    return 1;
                }
            }
        }
    }
    return 0;
}
```

程序调用 `semget` 创建或访问信号量集合并调用 `semctl` 初始化它。一个进程创建并初始化信号量，另一个进程在创建和初始化之间调用 `semop`；执行结果是不可预测的。这种不可预测性是竞态条件的例子，因为错误的发生取决于不同进程之间的精确时机。程序 15.3 没有竞态条件，因为原始进程在 `fork` 之前创建并初始化了信号量。该程序避免了竞态条件，因为创建时只有原始进程可以访问信号量。信号量集合的主要问题之一是创建和初始化是分离的操作，不是原子的。记住，POSIX 命名和匿名信号量在创建时就会初始化，没有这个问题。

程序 15.4 可创建或访问包含单个信号量元素的信号量集合。它有三个参数：信号量键、初始值以及指向 `sig_atomic_t` 类型变量的指针，该变量初始化为 `0` 并在调用者之间共享。此函数用于单个进程的线程；`sig_atomic_t` 变量可以定义在块外部并进行静态初始化。在进程之间使用 `semctl` 需要共享内存。我们在章节后面使用程序 15.4 来保护共享内存段。`initsset` 中使用的忙等待并没有看起来那么无效，因为它只在创建信号量的线程在初始化之前丢失 CPU 时才使用。

## 程序 15.4 initsset.c

创建并初始化包含单个信号量的信号量集合的函数。

```c
#include <errno.h>
#include <signal.h>
#include <stdio.h>
#include <time.h>
#include <sys/sem.h>
#include <sys/stat.h>
#define PERMS (S_IRUSR | S_IWUSR)
#define TEN_MILLION 10000000L
int itelement(int semid, int semnum, int semvalue);
int initsset(key_t mykey, int value, sig_atomic_t *readyp) {
    int semid;
    struct timespec sleeptime;
    sleeptime.tv_sec = 0;
    sleeptime.tv_nsec = TEN_MILLION;
    semid = semget(mykey, 2, PERMS | IPC_CREATE | IPC_EXCL);
    if ((semid == -1) && (errno != EEXIST)) { /* 错误，返回 */
        return -1;
    }
    if (semid >= 0) { /* 我们创建了信号量，所以初始化它 */
        if (itelement(semid, 0, value) == -1)
            return -1;
        }
        *readyp = 1;
        return semid;
    }
    if ((semid = semget(mykey, 2, PERMS)) == -1) { /* 访问它 */
        return -1;
    }
    while (*readyp == 0) { /* 等待初始化 */
        nanosleep(&sleeptime, NULL);
    }
    return semid;
}
```
