

```c
if ((key = ftok(name, 1)) == -1) {
    if (errno != ENOENT)
        EC_FAIL
} else {
    if ((semid = semget(key, 1, PERM_FILE)) == -1) {
        if (errno != ENOENT)
            EC_FAIL
    } else
        ec_negl(semctl(semid, 0, IPC_RMID));
}
return true;
EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

现在，让我们回到 System V。我们准备好介绍那个令人望而生畏的 `semop` 系统调用，它同时执行 `semwait` 和 `sempost` 操作：

### semop—对信号量集进行操作
```c
#include <sys/sem.h>

int semop(
    int semid,                  /* 标识符 */
    struct sembuf *sops,        /* 操作 */
    size_t nsops                /* 操作数量 */
);
/* 成功时返回 0，错误时返回 -1（设置 errno） */
```

### struct sembuf—用于 semop 的结构体
```c
struct sembuf {
    unsigned short sem_num;     /* 信号量编号 */
    short sem_op;               /* 信号量操作 */
    short sem_flg;              /* 操作标志 */
};
```

正如我所述，`semop` 不仅操作一个信号量，还可以操作任意多个，甚至整个集合。在进行调用之前，你需要构建一个操作数组（`struct sembufs`），尽管如果只有一个需要操作，单个 `struct sembuf` 就足够了——你只需传递其地址，并将 `nsops` 设为 1。

每个 `sem_op` 可以是正值、负值或零：

- **> 0** `sem_op` 的值加到信号量值上（*sempost*）。
- **< 0** `sem_op` 的绝对值从值中减去，除非这会使值变为负数；如果是这种情况，该调用将阻塞，直到整个值可以被减去（*semwait*）。
- **0** 该调用将阻塞，直到值变为零。

传递给 `semop` 的所有操作都是原子执行的，函数在全部完成之前不会返回。（除非它被线程取消、信号或信号量集的移除所中断。）

你可以通过在某个操作的 `sem_flg` 成员中设置 `SEM_UNDO` 标志来防止阻塞。如果数组中的任何操作会阻塞且设置了该标志，`semop` 将立即返回。由于 `semop` 总是原子性地执行，因此不会执行任何其他操作，即使它们出现在数组中更早的位置且本身不会阻塞。

还有一个特性：对于进程增加的或减少的每个信号量，都会维护一个调整值，与实际值一起保存。当增加操作设置了 `SEM_UNDO` 标志时，调整值会减少；对于减少操作则反之。当进程退出时，其调整值会被加到信号量的值上，从而撤销该进程对信号量所做的更改。例如，假设一个进程减少一个信号量（即 *semwait*）以锁定缓冲区，并在完成后增加它（*sempost*）。使用 `SEM_UNDO` 标志，它可以确保如果在异常退出时，缓冲区被解锁。

对于我们的简单信号量，我们只想一次操作一个，只增加或减少 1，并且不使用 `SEM_UNDO`。因此 `SimpleSemWait` 和 `SimpleSemPost` 确实很简单：

### SimpleSemWait—减少简单信号量
```c
#include "SimpleSem.h"

bool SimpleSemWait(
    struct SimpleSem *sem    /* 信号量 */
);
/* 成功时返回 true，错误时返回 false（设置 errno） */
```

### SimpleSemPost—增加简单信号量
```c
#include "SimpleSem.h"

bool SimpleSemPost(
    struct SimpleSem *sem    /* 信号量 */
);
/* 成功时返回 true，错误时返回 false（设置 errno） */
```

这是代码：

```c
bool SimpleSemWait(struct SimpleSem *sem)
{
    struct sembuf sop;

    sop.sem_num = 0;
    sop.sem_op = -1;
    sop.sem_flg = 0;
    ec_negl( semop(sem->sm_sm_semId, &sop, 1) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemPost(struct SimpleSem *sem)
{
    struct sembuf sop;

    sop.sem_num = 0;
    sop.sem_op = 1;
    sop.sem_flg = 0;
    ec_negl( semop(sem->sm_sm_semId, &sop, 1) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

在我们继续之前，我应该提到 System V 信号量的另一个用途：在进程之间传递整数。例如，假设客户端想要将其进程 ID 传递给服务器。它获取对一个信号量的访问权并将其值设置为其进程 ID。然后服务器可以通过查看该值来获取这个数字。由于信号量集可以包含一个信号量数组，因此可以以这种方式传递一个整数数组。

## 7.10 POSIX 信号量

这些信号量系统调用是 POSIX 标准的一部分，尽管是可选的，并且你需要检查 `_POSIX_SEMAPHORES` 特性测试宏来确定它们是否存在（参见第 1.5.4 节和第 7.6.3 节）。截至目前，它们在 FreeBSD、Darwin 或 Linux 中并不存在。

### 7.10.1 命名 POSIX 信号量

POSIX 信号量比 System V 信号量简单得多，也更容易使用。实际上，五个系统调用与上一节中 SimpleSem 接口完全对应：

### sem_open—打开命名信号量
```c
#include <semaphore.h>

sem_t *sem_open(
    const char *name,    /* POSIX IPC 名称 */
    int flags            /* 标志（不包括 O_CREATE） */
);
/* 成功时返回指向信号量的指针，错误时返回 SEM_FAILED（设置 errno） */

sem_t *sem_open(
    const char *name,    /* POSIX IPC 名称 */
    int flags,           /* 标志（包括 O_CREATE） */
    mode_t perms,        /* 权限 */
    unsigned value       /* 初始值 */
);
/* 成功时返回指向信号量的指针，错误时返回 SEM_FAILED（设置 errno） */
```

### sem_close—关闭命名信号量
```c
#include <semaphore.h>

int sem_close(
    sem_t *sem           /* 信号量 */
);
/* 成功时返回 0，错误时返回 -1（设置 errno） */
```

### sem_unlink—移除命名信号量
```c
#include <semaphore.h>

int sem_unlink(
    const char *name     /* POSIX IPC 名称 */
);
/* 成功时返回 0，错误时返回 -1（设置 errno） */
```

### sem_wait—减少信号量
```c
#include <semaphore.h>

int sem_wait(
    sem_t *sem           /* 信号量 */
);
/* 成功时返回 0，错误时返回 -1（设置 errno） */
```

### sem_post—增加信号量
```c
#include <semaphore.h>

int sem_post(
    sem_t *sem           /* 信号量 */
);
/* 成功时返回 0，错误时返回 -1（设置 errno） */
```

POSIX 信号量是计数信号量，与 System V 变体类似，但仅以 1 为步长。每个 `sem_t` 对象仅代表一个信号量，而不是像 System V 那样的一组信号量。

打开、关闭和解除链接的调用遵循我们在第 7.7.1 节中看到的 POSIX IPC 调用的模式，针对的是 POSIX 消息队列系统调用。特别是，传递给 `sem_open` 的名称必须遵循第 7.6.2 节中讨论的可移植性规则。不出所料，`sem_post` 将 1 加到信号量的值上，而 `sem_wait` 减去 1，如果值已经是零则阻塞。

你在 `sem_open` 中不使用 `O_RDONLY`、`O_WRONLY` 或 `O_RDWR`，因为它们是无意义的——除非 `sem_post` 和 `sem_wait` 都可以使用，否则信号量毫无用处。

我们需要为 System V 所做的那些繁琐的初始化过程已经消失了。我们只需将所需的值（通常是零）传递给 `sem_open`。

当 `sem_open` 失败时，要注意其返回值：它是 `SEM_FAILED`，而不是 `NULL`，后者是其他返回指针的函数的常规失败返回值。

POSIX 信号量的 SimpleSem 调用的实现是微不足道的：

```c
struct SimpleSem *SimpleSemOpen(const char *name)
{
    struct SimpleSem *sem = NULL;

    ec_null( sem = malloc(sizeof(struct SimpleSem)) );
    if ((sem->sm_sem = sem_open(name, O_CREAT, PERM_FILE, 0)) == SEM_FAILED)
        EC_FAIL;
    return sem;

EC_CLEANUP_BGN
    free(sem);
    return NULL;
EC_CLEANUP_END
}

bool SimpleSemClose(struct SimpleSem *sem)
{
    ec_neg1( sem_close(sem->sm_sm_sem) );
    free(sem);
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemRemove(const char *name)
{
    if (sem_unlink(name) == -1 && errno != ENOENT)
        EC_FAIL;
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemPost(struct SimpleSem *sem)
{
    ec_neg1( sem_post(sem->sm_sm_sem) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

bool SimpleSemWait(struct SimpleSem *sem)
{
    ec_neg1( sem_wait(sem->sm_sm_sem) );
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

10. 如果你不熟悉这个术语，我查阅的一本词典将其定义为“一套复杂而琐碎的程序”，这简直再合适不过了。

