
该结构体的三个成员`l_whence`、`l_start`和`l_len`，确定了要操作的区域。前两者类似于`lseek`的参数（`l_whence`可以是`SEEK_SET`、`SEEK_CUR`或`SEEK_END`），而`l_start`是相对于当前文件偏移量、相对于文件末尾的绝对位置或相对位置。区域的长度由`l_len`给出。

在`lockf`中只有一种类型的锁，但在`fcntl`中你可以同时拥有读锁和写锁，或者通常称为共享锁和排他锁。对某个区域的共享锁会阻止对该区域的排他锁；排他锁则阻止共享锁或排他锁。实际上，当你仅读取数据时设置共享锁，当你写入数据时设置排他锁。

你在`l_type`成员中指定锁类型；概要中显示的第三个选项用于解锁区域。

现在我们要解释`fcntl`的锁定操作，它们非常简单：

- `F_SETLK` 如果可能，执行结构体中指定的操作。如果无法立即设置锁，则返回-1并将`errno`设置为`EAGAIN`或`EACCES`；即不阻塞。
- `F_SETLKW` 类似于`F_SETLK`，但如果无法立即设置锁，则阻塞。
- `F_GETLK` 返回有关第一个会导致结构体中指定的锁阻塞的锁的信息（如果有）。传入结构体的所有成员都被结果覆盖，包括持有锁的进程的进程 ID。如果传入的锁不会阻塞，则结构体原样返回，除了第一个成员被更改为`F_UNLCK`。

因此，`fcntl`锁定可以做`lockf`能做的一切。此外，它区分共享锁和排他锁，并且可以检索有关现有锁的信息。通常，实现者将`lockf`实现为基于`fcntl`的库函数，但这并非必须。另外，`[SUS2002]`指出你不应该假设两个函数操作的锁是相同的。也就是说，如果你用`lockf`锁定，不要用`fcntl`解锁。事实上，不要期望`fcntl`甚至知道该锁。

与`lockf`锁一样，用`fcntl`设置的锁在关闭打开到该文件的文件描述符或进程终止时释放，并且当进程调用`fork`时不会被继承。

## 7.11.5 建议锁和强制锁

使用`lockf`和`fcntl`设置的锁通常仅影响那些函数调用，而不影响其他 I/O 操作。也就是说，如果你使用`lockf`对文件设置锁，然后另一个进程在不调用`lockf`的情况下写入该文件，该写入将照常进行。这被称为建议锁，显然，只有当所有进程都通过适当调用`lockf`或`fcntl`进行协作时，它才有效。

强制锁意味着一旦设置锁，它确实会禁止冲突的 I/O 操作。POSIX 和 SUS 标准完全没有规定强制锁，但它们也不禁止它。

在支持强制锁的系统中，你在调用`lockf`或`fcntl`时并不做任何不同的操作。相反，你用一组通常没有意义的权限标记文件本身：设置执行时设置组 ID 位（set-group-ID-on-execution bit），并关闭组执行位。下面是一个根据参数使用建议锁或强制锁的示例程序：

```c
int main(int argc, char *argv[])
{
    int fd;
    mode_t perms = PERM_FILE;

    if (fork() == 0) {
        sleep(1); /* wait for parent */
        ec_neg1( fd = open("tmpfile", O_WRONLY | O_NONBLOCK) )
        ec_neg1( write(fd, "x", 1) )
        printf("child wrote OK\n");
    }

    else {
        (void)unlink("tmpfile");

        if (argc == 2)
            perms |= S_ISGID; /* mandatory locking */

        ec_neg1( fd = open("tmpfile", O_CREAT | O_RDWR, perms) )
        ec_neg1( lockf(fd, F_LOCK, 0) )
        printf("parent has lock\n");

        ec_neg1( wait(NULL) )
    }

    exit(EXIT_SUCCESS);
}

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
```

当我在具有强制锁的 Solaris 上运行此程序时，得到以下结果：

```
$ lockftest
parent has lock
child wrote OK
$ lockftest x
parent has lock
ERROR: 0: main [/aup/c7/lockftest.c:11] write(fd, "x", 1)
*** EAGAIN (11: "Resource temporarily unavailable") ***
$
```

如果没有`O_NONBLOCK`标志，子进程中的写入将阻塞，等待锁释放。

## 7.11.6 高性能数据库锁定

`fcntl`和`lockf`系统调用提供的文件锁定，即使有强制锁，也不适合高性能数据库，因为在操作锁时开销太大，并且很难实现复杂的死锁检测和修正算法。不过，这通常没问题，因为大型数据库系统通常在它们自己的进程中运行，因此它们作为数据库文件的网关。锁可以轻松保存在数据库进程的地址空间中，或保存在多个数据库进程之间的共享内存中。这样做的话，根本不需要使用系统调用来管理锁。

## 7.12 关于共享内存

回想第 5.17 节，进程内的线程共享所有静态数据——全局数据和函数内部的静态数据。另一方面，进程拥有完全独立的内存，即使执行了`fork`而没有`exec`，在这种情况下，子进程获得父进程地址空间的副本。

使用共享内存，你可以安排不同的进程拥有部分共同内存。与线程一样，它们通常需要使用互斥锁或信号量来协调对内存的访问。

共享内存既有 System V 版本，也有 POSIX 版本，就像消息和信号量一样。对于这两种机制，每个进程都“打开”一个共享内存段并获得指向该内存的指针，然后可以随意使用普通的 C 或 C++ 运算符对其进行操作，而无需使用系统调用。通常，每个进程的指针具有不同的值，仅在该进程内有意义，但底层的内存是相同的。像之前一样，我们先从 System V 共享内存开始，然后转向 POSIX。

## 7.13 System V 共享内存

到这时，你应该已经熟悉了 System V IPC 调用的工作方式。正如 7.4 节所解释的，你获取一个键（key），如果使用`ftok`的话，然后使用一个`Xget`调用（`shmget`）来获取标识符。你使用一个`Xctl`调用（`shmctl`）来控制它。对于共享内存，你使用`shmat`将其附加到你的进程，该函数返回一个指针，当你用完它时，使用`shmdt`将其分离。

### 7.13.1 System V 共享内存系统调用

以下是 System V 共享内存系统调用的摘要：

**`shmget`** — 获取共享内存段

```c
#include <sys/shm.h>

int shmget(
  key_t key,          /* key */
  size_t size,        /* size of segment */
  int flags           /* creation flags */
);

/* Returns shared-memory identifier or -1 on error (sets errno) */
```

**`shmctl`** — 控制共享内存段

```c
#include <sys/shm.h>

int shmctl(
  int shmid,          /* identifier */
  int cmd,            /* command */
  struct shm_ds *data /* data for command */
);

/* Returns 0 on success or -1 on error (sets errno) */
```

**`struct shm_ds`** — 用于`shmctl`的结构体

```c
struct shm_ds {
  struct ipc_perm shm_perm; /* permission structure */
  size_t shm_segsz;         /* size of segment in bytes */
  pid_t shm_lpid;           /* process ID of last shared memory op */
  pid_t shm_cpid;           /* process ID of creator */
  shmatt_t shm_nattach;     /* number of current attaches */
  time_t shm_atime;         /* time of last shmat */
  time_t shm_dtime;         /* time of last shmdt */
  time_t shm_ctime;         /* time of last change by shmctl */
};
```

**`shmat`** — 附加共享内存段

```c
#include <sys/shm.h>

void *shmat(
 int shmid, /* identifier */
 const void *shmaddr, /* desired address or NULL */
 int flags /* attachment flags */
);

/* Returns pointer or -1 on error (sets errno) */
```

**`shmdt`** — 分离共享内存段

```c
#include <sys/shm.h>

int shmdt(
 const void *shmaddr /* pointer to segment */
);

/* Returns 0 on success or -1 on error (sets errno) */
```

不出所料，`shmget`访问共享内存段，如有必要且存在`IPC_CREAT`或`IPC_PRIVATE`标志时，它会创建该段。只有当段被创建时，`size`参数才有意义。新创建的段初始化为零。

然后，要使用该段，你调用`shmat`，它会给你一个指向该段的指针。奇怪的是，`shmat`在出错时返回-1，而不是`NULL`。这是可行的，因为它永远不会返回一个可能被误认为-1的指针；事实上，在几乎所有的 UNIX 系统上，返回的指针都是偶数。

当你用完该段时，你调用`shmdt`，传入从`shmat`获取的指针，而不是标识符。该段会一直存在，直到被显式移除（通过`shmctl`或`ipc(1)`命令）或者机器重启，因此你可以自由地重新附加它。不过，你可能会得到一个不同的指针。

通常，你并不关心`shmat`给你什么地址，所以将第二个参数设置为`NULL`。但是，如果你愿意，你可以尝试强制它给你指定通过`shmaddr`的地址。如果它做不到，因为该地址已经被使用或其他原因无效，它会失败并将`errno`设置为`EINVAL`。还有一个标志`SHM_RND`，用于将地址舍入到合适的边界，但我不会描述细节。另一个标志`SHM_RDONLY`，如果设置，则以只读方式附加该段。

使用`shmctl`时，你使用与其他`Xctl`系统调用相同的命令，`IPC_STAT`、`IPC_SET`和`IPC_RMID`。`IPC_SET`设置`shm_perm.uid`、`shm_perm.gid`以及`shm_perm.mode`的低 9 位。

这是一个简单的程序，展示了一个段（一个小段！）如何在两个进程之间共享：

```c
static int *getaddr(void)
{
    key_t key;
    int shmfd, *p;
    (void)close(open("shmeeg", O_WRONLY | O_CREAT, 0));
    ec_negl( key = ftok("shmeeg", 1) )
    ec_negl( shmfd = shmget(key, sizeof(int), IPC_CREAT | PERM_FILE) )
    ec_negl( p = shmat(shmfd, NULL, 0) )
    return p;

    EC_CLEANUP_BGN
        return NULL;
    EC_CLEANUP_END
}

int main(void)
{
    pid_t pid;
    if ((pid = fork()) == 0) {
        int *p, prev = 0;
        ec_null( p = getaddr() )
        while (*p != 99)
            if (prev != *p) {
                printf("child saw %d\n", *p);
                prev = *p;
            }
        printf("child is done\n");
    }

    else {
        int *p;
        ec_null( p = getaddr() )
        for (*p = 1; *p < 4; (*p)++)
            sleep(1);

        *p = 99;
    }

    exit(EXIT_SUCCESS);
    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

每个进程都调用`getaddr`；其中一个创建段，另一个只是访问它。以下是我们得到的输出：

```
$ shmem
child saw 1
child saw 2
child saw 3
$ child saw 99
child is done
```

有点奇怪，不是吗？为什么子进程报告它看到了 99，而 99 恰恰是终止其`while`循环的值？好吧，在行

```c
while (*p != 99)
```

中，`*p`在某个时刻等于 3，但等到到达行

```c
printf("child saw %d\n", *p);
```

时，`*p`已经是 99 了。（`$`提示符在那里是因为父进程在退出之前没有等待子进程。这不是缺陷，但在 UNIX 中是一种相当常见的现象。）

如果你第二次运行`shmem`，事情会变得甚至更奇怪：

```
$ shmem
child is done
$
```

它坏了！不，实际上唯一的错误是段在第一次`shmem`终止后留在那里——未分离——并且仍然保持值 99。在第二次运行中，子进程在父进程甚至到达其`for`循环之前就看到了 99。显然，我们可以通过在`shmem`终止时移除段来修复这个问题。但你明白了：共享内存是复杂的！

### 7.13.2 共享内存与信号量

上一节的示例由于另一个更微妙的原因是错误的：正如我们在线程中所看到的（5.17.3 节），我们不能假设对`*p`的引用是原子的。通常，你不能在没有某种形式的信号量控制的情况下在进程之间共享内存。因此，让我们加上它（`getaddr`不变）：

```c
int main(void)
{
    pid_t pid;
    ec_false( SimpleSemRemove("shmxsem") )
    if ((pid = fork()) == 0) {
        struct SimpleSem *sem;
        int *p, prev = 0, n;
        ec_null( sem = SimpleSemOpen("shmxsem") )
        ec_null( p = getaddr() )
        while (true) {
            ec_false( SimpleSemWait(sem) )
            n = *p;
            ec_false( SimpleSemPost(sem) )
            if (n == 99)
                break;
            if (prev != n) {
                printf("child saw %d\n", n);
                prev = n;
            }
        }
        printf("child is done\n");
        ec_false( SimpleSemClose(sem) )
    }

    else {
        struct SimpleSem *sem;
        int *p, i;
        ec_null( sem = SimpleSemOpen("shmxsem") )
        ec_null( p = getaddr() )
        *p = 0;
        ec_false( SimpleSemPost(sem) )
        for (i = 1; i < 4; i++) {
            ec_false( SimpleSemWait(sem) )
            *p = i;
```
