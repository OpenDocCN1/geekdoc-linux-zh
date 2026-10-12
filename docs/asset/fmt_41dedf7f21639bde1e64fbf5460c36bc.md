
```c
/*
 * mp1ex.c - 使用 select 从 pipe1 和 pipe2 读取输入
 *
 * 改编自 mpx-select.c，作者是 Michael Johnson 和 Erik Troan。经原作者
 * _Linux Application Development_ 的 authors Michael Johnson 和
 * Erik Troan 允许使用。
 */
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

#define BUFSZ 80

void err_quit(char *msg);

int main(void)
{
    int fds[2];
    char buf[BUFSZ];
    int i, rc, maxfd;
    fd_set watchset;              /* 读取此文件描述符集合 */
    fd_set inset;                 /* watchset 的副本，供 select 更新 */

    /* 打开管道 */
    if((fds[0] = open("pipe1", O_RDONLY | O_NONBLOCK)) < 0)
        err_quit("open pipe1");
    if((fds[1] = open("pipe2", O_RDONLY | O_NONBLOCK)) < 0)
        err_quit("open pipe2");

    /* 使用文件描述符初始化 watchset */
    FD_ZERO(&watchset);
    FD_SET(fds[0], &watchset);
    FD_SET(fds[1], &watchset);
    /* select 需要知道最大的文件描述符 */
    maxfd = fds[0] > fds[1] ? fds[0] : fds[1];

    /* 循环监视管道，以读取输出 */
    while(FD_ISSET(fds[0], &watchset) || FD_ISSET(fds[1], &watchset)) {
        /* 确保 select 有一个当前的描述符集合 */
        inset = watchset;
        if(select(maxfd + 1, &inset, NULL, NULL, NULL) < 0)
            err_quit("select");

        /* 哪个文件描述符准备好读取？ */
        for(i = 0; i < 2; ++i) {
            if(FD_ISSET(fds[i], &inset)) {
                rc = read(fds[i], buf, BUFSZ - 1);
                if(rc > 0) { /* 读取了一些数据 */
                    buf[rc] = '\0';
                    printf("read: %s", buf);
                } else if(rc == 0) { /* 此管道已关闭 */
                    close(fds[i]);
                    FD_CLR(fds[i], &watchset);
                } else
                    err_quit("read"); /* 糟糕 */
            }
        }
    }
    exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

图 8.1 展示了`mplex`运行时的样子。

这个程序有点复杂。在打开两个命名管道后，它使用`FD_ZERO`初始化一个文件描述符集合，然后添加两个管道的描述符。`mplex`的核心是`while`循环。在每次迭代中，它使用`FD_ISSET`查看任一管道是否有可读的数据。如果有，它首先将`watchset`复制到`inset`，因为`watchset`可能由于其中一个管道关闭而发生了变化。

![](img/be588b36b489136ce784030a08a1d3d4_203_0.png)

图 8.1：`mplex`复用来自两个管道的输入。

接下来是`select`调用，随后是一个`for`循环，用于确定哪个描述符准备好被读取（超时值为`NULL`，因此`select`会阻塞直到数据准备好被读取）。然后`for`循环读取管道并显示数据。如果`read`返回 0，表示管道已关闭，因此`mplex`关闭该文件并将其从监视集合中移除。当最后一个管道关闭时，`mplex`终止。

## 内存映射文件

`内存映射文件`是磁盘文件在内存中的相同副本。`inode`映像与磁盘文件逐字节对应。内存映射文件有两个主要优点。第一个优点是更快的文件 I/O。普通的 I/O，如`read`和`write`系统调用以及`fputs`和`fgets`库调用，会通过内核缓冲区复制数据。尽管 Linux 使用快速、复杂的磁盘缓存算法，但最快的磁盘访问始终会比最慢的内存访问慢。对内存映射文件的 I/O 操作绕过内核缓冲区，因此速度要快得多。它们使用起来也更简单，因为你可以使用指针而不是通常的文件操作函数来访问映射文件。

内存映射文件的第二个优点是数据共享。如果多个进程需要访问相同的数据，可以将数据存储在一个内存映射文件中。这实际上是一种共享内存模型（参见第 16 章“共享内存”），使数据独立于任何单个进程，可供任何进程访问，并将区域的内容存储在磁盘文件中。

管理内存映射的函数调用定义在`<sys/mman.h>`中。它们包括以下调用：

- `mmap`—将磁盘文件映射到内存

- `munmap`—解除文件映射，删除内存映像

- `msync`—使用内存映像中的数据更新磁盘文件

- `mprotect`—限制对内存映像的访问

- `mlock`—防止映射的一部分交换到磁盘

- `munlock`—移除之前设置的锁定

- `mlockall`—防止内存映像的任何部分交换到磁盘

- `munlockall`—移除由`mlockall`设置的锁定

这些函数调用将在下面的章节中详细讨论。

## 创建内存映射

要创建一个内存映射文件，请调用`mmap`。使用完毕后，调用`munmap`将映射从内存中删除并将内存返回给操作系统。

## 映射文件

`mmap`函数将磁盘文件映射到内存。其原型如下：

```c
void *mmap(void *start, size_t length, int prot, int flags,
       int fd, off_t offset);
```

`mmap`创建由文件描述符`fd`引用的文件的内存映像。内存映像将从文件的`offset`字节处开始。参数`length`指示应将文件的多少内容读取到内存中。为了限制对内存映射的访问，可以使用`prot`参数设置不同的保护级别。它可以是表 8.1 中一个或多个值的逻辑或。`flags`参数为内存映射设置若干额外属性。它可以是表 8.2 中列出的一个或多个值的逻辑或。`mmap`返回指向内存区域的指针，失败时返回 -1。

### 表 8.1：mmap 保护参数的值

| 保护 | 描述 |

| :--------- | :--------- |

| `PROT_NONE` | 不允许访问 |

| `PROT_READ` | 映射区域可读 |

| `PROT_WRITE` | 映射区域可写 |

| `PROT_EXEC` | 映射区域可执行 |

> **注意** 在 x86 架构上，`PROT_EXEC`隐含`PROT_READ`，因此`PROT_EXEC`等同于指定`PROT_EXEC|PROT_READ`。

### 表 8.2：mmap 标志参数的值

| 标志 | 描述 |

| :----- | :----- |

| `MAP_ANONYMOUS` | 创建匿名映射，忽略`fd` |

| `MAP_FIXED` | 如果地址无效或已被使用则失败 |

| `MAP_PRIVATE` | 对区域的写入是进程私有的 |

| `MAP_SHARED` | 对区域的写入会被复制到文件 |

| `MAP_DENYWRITE` | 禁止对文件进行正常写入 |

| `MAP_GROWSDOWN` | 内存向下增长 |

| `MAP_LOCKED` | 将页锁定在内存中 |
