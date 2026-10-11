
> 关于竞态条件的详细讨论，请参阅“使用 fork”一章，第 78 页。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_214_0.png)

此程序创建一个锁文件，然后尝试再次锁定它。第二次尝试将会失败。该程序旨在说明使用锁文件的正确逻辑。

```c
"""
 * lockit.c - 使用锁文件
 */
#include <unistd.h>
#include <fcntl.h>
#include <errno.h> /* for EEXIST */
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char *argv[])
{
    int fd, newfd;

    /* Open the lockfile */
    fd = open(argv[1], O_CREAT | O_EXCL, 0644);
    if(fd < 0 && errno == EEXIST) { /* lockfile exists */
        puts("file already locked");
        close(fd);
    } else if(fd < 0) /* some other error we don't test */
        puts("unknown error");
    else { /* file is now locked */
        puts("lock established");

        /* Additional processing would take place here */

        /* repeat the process, this time it will fail */
        newfd = open(argv[1], O_CREAT | O_EXCL, 0644);
        if(newfd < 0 && errno == EEXIST) {
            puts("file already locked");
            close(newfd);
        } else if(newfd < 0)
            puts("unknown error");
    }
    close(fd);
    unlink(argv[1]);
    exit(EXIT_SUCCESS);
}
```

运行 lockit 示例的输出如下：

```bash
$ ./lockit lockit.c.lck
lock established
file already locked
```

除非发生意外，否则 lockit 会在第一个 open 语句中成功锁定文件（文件名作为唯一的命令行参数传入）。然后，在第二个 open 语句中，lockit 通过创建相同的锁文件尝试第二次锁定该文件。在 open 调用中指定 O_CREAT 以及 O_EXCL，意味着如果文件已经存在，open 调用将失败。换句话说，使用所示语法创建或打开锁文件等同于锁定文件；删除锁文件等同于解锁文件。由于该测试失败，程序报告该文件已被锁定。返回到外层代码块，程序关闭文件描述符并取消链接（删除）该文件，从而移除锁。

## 记录锁定

虽然锁文件易于使用，但它们存在显著缺点：

- 当文件被锁定时，对于仅希望读取该文件的其他进程来说，该文件不可用。
- O_EXCL 标志仅在本地文件系统中可靠，在网络文件系统（如 NFS）上则不可靠。
- 这些锁仅是建议性的；进程可以忽略它们。
- 如果进程在移除锁文件之前终止，锁文件将保留在原处，其他进程没有可靠的方法来判定该文件是否为陈旧锁，即由过早死亡的进程遗留下来的锁。

这些缺点促成了记录锁定的发展，它赋予程序员锁定文件特定区域（称为记录）的能力。记录锁，有时称为 POSIX 锁，允许多个进程锁定同一文件的不同部分，甚至读取同一文件的相同片段。记录锁在 NFS 及其他网络文件系统中也能正常工作。最后，由于记录锁由内核持有，当进程终止时，其锁会自动释放。

POSIX 锁有两种类型：*读锁或共享锁* 以及 *写锁或排他锁*。读锁被称为共享锁，因为许多进程可以持有同一文件区域的读锁。然而，排他锁在写锁生效期间防止对锁定区域的访问。此外，当同一文件区域存在读锁时，无法创建写锁。

> **注意**
> 回顾第 4 章“进程”中的内容，子进程在 *fork* 后不会继承文件锁，尽管通过 exec 的进程会继承其父进程的文件锁。

*fcntl* 调用在 `<fcntl.h>` 中声明，用于管理记录锁。它有以下原型：

```c
int fcntl(int fd, int cmd, struct flock *lock);
```

*fd* 是要锁定的文件描述符。*cmd* 必须是 *F_GETLK*、*F_SETLK* 或 *F_SETLKW* 之一。*F_GETLK* 检查文件是否可以被锁定。如果可以锁定，*struct flock* 的 *l_type* 成员将被设置为 *F_UNLCK*；如果不能锁定，*struct flock* 的 *l_pid* 成员将被设置为持有锁的进程的 PID。*F_SETLK* 设置锁。*F_SETLKW* 也设置锁，但 *fcntl* 会等待直到成功设置锁后才返回。

*lock* 是指向 *flock* 结构的指针，该结构描述锁及其行为。*struct flock* 定义如下：

```c
struct flock {
    short l_type; /* Type of lock */
    short l_whence; /* Beginning of lock */
    off_t l_start; /* Starting offset of lock */
    off_t l_len; /* Number of bytes to lock */
    pid_t l_pid; /* Process holding lock */
};
```

*l_type* 可以是 *F_RDLCK*（读锁）、*F_WRLCK*（写锁）或 *F_UNLCK*（释放锁）。*l_whence* 是 *SEEK_SET*、*SEEK_CUR* 或 *SEEK_END* 之一，其语义与 *lseek* 调用相同。*l_start* 指示相对于 *l_whence* 的锁起始偏移量，而 *l_len* 指定要锁定的字节数。最后，*l_pid* 是持有锁的进程的 PID。

> * lseek 系统调用在第 143 页的“定位文件指针”一节中有介绍。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_217_0.png)

下面的程序 _reclck_ 在文件的一部分设置写锁，在另一部分设置读锁。如果在两个终端窗口中运行此程序，你可以清楚地看到记录锁是如何工作的。

```c
/*
 * reclck.c - 设置读写锁
 */
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>
#include <errno.h>

int main(void)
{
    int fd;
    struct flock lock;

    if ((fd = open("test.dat", O_RDWR)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    /*
     * Set up a write lock on the last 100
     * bytes of the file
     */
    lock.l_type = F_WRLCK;
    lock.l_whence = SEEK_END;
    lock.l_start = 0;
    lock.l_len = 100;

    /* set the lock */
    if (!fcntl(fd, F_SETLK, &lock))
        puts("write lock established");
    else {
        fcntl(fd, F_GETLK, &lock);
        printf("write locked by PID %d\n", lock.l_pid);
    }

    /* Now do a read lock */
    lock.l_type = F_RDLCK;
    lock.l_whence = SEEK_END;
    lock.l_start = 0;
    lock.l_len = 100;

    if (!fcntl(fd, F_SETLKW, &lock))
        puts("read lock established");
    else {
        fcntl(fd, F_GETLK, &lock);
        printf("read locked by PID %d\n", lock.l_pid);
    }

    getchar();
    exit(EXIT_SUCCESS);
}
```

该程序在两个 xterm 窗口中运行的输出如图 8.2 所示。

![](img/be588b36b489136ce784030a08a1d3d4_218_0.png)

写锁是排他的；读锁是共享的。

首先，`reclck` 在文件的最后 100 字节上设置写锁。如果无法建立锁，它会调用 `fcntl` 并使用 `F_GETLK` 命令来获取锁定进程的 PID。下一个锁是文件前 100 字节上的读锁。读锁是共享的，因此多个进程可以锁定文件的同一区域，如图 8.2 所示。

## 接下来是什么？

本章扩展了关于文件 I/O 的讨论，重点关注目录操作、内存映射和文件锁定等高级特性。下一章“守护进程”将介绍如何创建后台进程，从而完成对系统编程的综述。

## 9—守护进程

在本章中，你将学习如何创建*守护进程*，发音类似 *demon*。守护进程是非交互式运行的后台进程。它们通常提供某些服务，要么服务于整个系统，要么服务于用户程序。特别是，本章涵盖以下内容：

- 守护进程的特性
- 创建守护进程的规则
- 编程守护进程时使用的函数调用
- 如何使用 syslog 设施
- 守护进程应如何处理运行时错误

