
我们指定非阻塞标志（`-n`）和三个操作，每个操作都会减少集合中的一个值。第一个操作是成功的（我们可以减少值为 1 的第一个成员），第二个操作也是成功的（我们可以减少值为 2 的第二个成员），但第三个操作无法执行（我们无法减少值为 3 的第三个成员）。由于最后一个操作无法执行且我们指定了非阻塞，返回了 `EAGAIN` 错误。（如果我们没有指定非阻塞标志，程序将阻塞）。我们通过 `semvalues` 验证集合中的值没有变化。尽管前两个操作可以执行，由于最后一个操作无法执行，三个操作都没有执行。`semop` 确保要么全部执行，要么都不执行。

我们现在演示 System V 信号量的 `SEM-UNDO` 特性。

```bash
solaris % semvalues /tmp/rich 1 2 3
solaris % semop -u /tmp/rich -1 -2 -3
solaris % getvalues /tmp/rich
semval[0] = 0  semop 终止时更改已撤销
semval[1] = 2  未指定 SEM_UNDO
semval[2] = 3  更改未被撤销
```

我们使用 `semvalues` 将值重置为 1, 2 和 3，然后用 `semop` 程序指定 `-1`, `-2` 和 `-3` 操作。这会导致三个值变为 0，除非我们在 `semop` 程序中指定了 `-u` 标志，此时对三个操作都指定了 `SEM-UNDO`。这会导致三个成员的 `semadj` 值分别变为 1, 2 和 3。当 `semop` 程序终止时，这些 `semadj` 值会被加到三个成员的当前值（均为 0），导致它们的值变为 1, 2 和 3，我们通过 `getvalues` 程序验证这一点。然后我们再次执行 `semop`，但不使用 `-u` 标志，这在 `semop` 终止时会将值保持为 0。

# 11.6 文件锁

我们可以使用 System V 信号量提供图 10.19 中 `my_lock` 和 `my_unlock` 函数的版本。我们在图 11.7 中展示这一点。

## 首先尝试排斥

我们必须保证只有一个进程初始化信号量，因此我们指定 `IPC_CREAT | IPC_EXCL`。如果成功，进程调用 `semctl` 将信号量值初始化为 1。如果有多个进程同时尝试，每个进程调用我们的 `my_lock` 函数都会创建信号量（假设它不存在），然后初始化信号量。第一次 `semget` 会向其他进程返回 `EEXIST` 错误，它们再次调用 `semget` 但不带 `IPC_CREAT | IPC_EXCL` 标志。

## 等待信号量初始化

我们在第 11.2 节讨论过 System V 信号量初始化时的竞态条件。为了避免这种情况，任何发现信号量已存在的进程必须调用带有 `IPC_STAT` 命令的 `semctl` 查看

```c
#include    "unipipc.h"                                              lock/lockvssem.c
#define LOCK_PATH     "/tmp/svseml*"
#define MAX_TRIES      10

int                    semid, init_flag;
struct sembuf postop, waitop;

void
my_lock(int fd)
{
    int                    oflag, i;
    union sem_arg arg;
    struct sem_info de_seminfo;

    if (init_flag == 0) {
        oflag = IPC_EXCL | SVSEM_MODE;
        if ((sem = semget(ftok(LOCK_PATH), 0, oflag)) >= 0) {
            /* 成功，我们是第一个初始化的 */
            arg.val = 1;
            semctl(semid, 0, SETVAL, arg);
        }
    } else if (errno == EEXIST) {
        /* 别人创建并初始化了 */
        semid = semget(ftok(LOCK_PATH), 0, SVSEM_MODE);
        arg.buf = &de_seminfo;
        for (i = 0; i < MAX_TRIES; i++) {
            semctl(semid, 0, IPC_STAT, arg);
            if (arg.buf->sem_otime != 0)
                goto retry;
            sleep(1);
        }
retry:
        err_quit("semget OK, but semaphore not initialized");
    } else {
        err_sys("semget error");
    }
init:
    init_flag = 1;
    postop.sem_num = 0;      /* 以及两个 semop() 结构体 */
    postop.sem_op = 1;
    postop.sem_fl = SEM_UNDO;
    waitop.sem_num = 0;
    waitop.sem_op = -1;
    waitop.sem_fl = SEM_UNDO;
    semop(semid, &waitop, 1);  /* 减 1 */
}

void
my_unlock(int fd)
{
    semop(semid, &postop, 1);  /* 加 1 */
}
```

信号量的 `sem_otime` 值。一旦该值不为零，我们就知道创建信号量的进程已经初始化了它，并调用了 `semop`（`semop` 调用位于该函数的末尾）。如果该值仍为 0（这种情况极少发生），我们将睡眠 1 秒并重试。我们限制了尝试的次数，以避免无限睡眠。

## 初始化信号量

正如我们之前提到的，`sembuf` 结构中成员的顺序是没有保证的，因此我们无法对它们进行静态初始化。相反，我们分配了两个这样的结构，并在进程第一次调用 `my-lock` 时在运行时填充它们。我们指定了 `SEM_UNDO` 标志，这样如果进程在持有锁的情况下终止，内核将释放该锁（参见练习 10.3）。在首次使用时创建信号量（每个尝试创建它的进程如果发现信号量已存在，则会获得一个错误，但在所有进程完成后再删除它要困难得多）。对于一个使用序列号分配作业号的解析器守护进程来说，信号量将一直存在。但其他应用程序可能希望在文件删除时删除信号量。事实上，记录锁（record lock）可能比信号量更好。

# 11.7 信号量限制

与 System V 消息队列一样，System V 信号量也有系统限制，大部分源于其原始的 System V 实现（第 3.8 节）。这些限制如图 11.8 所示。第一列是限制该项目的变量传统 System V 名称。

| 名称 | 描述 | DUnix 4.0B | Solaris 2.6 |
|---|---|---|---|
| `semmni` | 全范围内唯一信号量的数量 | 16 | 10 |
| `semms` | 每个信号量的最大信号量数 | 25 | 25 |
| `semmnms` | 全范围内信号量的总数 | 400 | 60 |
| `semopmn` | 每次 `sem` 调用最大操作数 | 10 | 10 |
| `semmnu` | 全范围内 `undo` 结构的最大数量 |  | 30 |
| `semone` | 每个结构的最大 `undo` 条目数 | 10 | 10 |
| `semmax` | 任何信号量的最大值 | 32767 | 32767 |
| `semaeem` | 退出时的最大调整值 | 16384 | 16384 |

图 11.8 System V 信号量的典型限制。

显然，Digital Unix 没有 `semmnu` 限制。

## 示例

图 11.9 中的程序确定了图 11.8 所示的限制。
