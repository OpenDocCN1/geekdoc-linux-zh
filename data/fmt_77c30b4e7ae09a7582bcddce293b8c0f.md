
打开、关闭、删除、读取和写入 FIFO 的过程分别使用你之前已经见过的 `open`、`close`、`unlink`、`read` 和 `write` 系统调用——这是 Linux “一切皆文件” 抽象的一个优点。由于打开和关闭 FIFO 与打开和关闭管道相同，你可能需要回顾本章前面列出的“打开和关闭管道”中的程序。

然而，在读取和写入 FIFO 时，你必须牢记一些细微之处。首先，FIFO 的两端都必须打开后才能使用。其次，更重要的是，如果 FIFO 使用 `O_NONBLOCK` 标志打开时的行为。回想一下，`O_WRONLY` 或 `O_RDONLY` 标志可以逻辑或与 `O_NONBLOCK`。如果 FIFO 使用 `O_NONBLOCK` 和 `O_RDONLY` 打开，调用会立即返回；但如果它使用 `O_NONBLOCK` 和 `O_WRONLY` 打开，如果该 FIFO 尚未同时被打开用于读取，则 `open` 返回错误并将 `errno` 设置为 `ENXIO`。

另一方面，如果 `open` 的标志中没有指定 `O_NONBLOCK`，`O_RDONLY` 会导致 `open` 阻塞（不返回），直到另一个进程以写模式打开该 FIFO。同样，`O_WRONLY` 会阻塞，直到该 FIFO 被打开用于读取。

与管道一样，向未打开用于读取的 FIFO 写入数据会向写入进程发送 `SIGPIPE`，并将 `errno` 设置为 `EPIPE`。在最后一个写入者关闭 FIFO 后，读取进程在其下一次读取时会检测到文件末尾。如前关于管道所述，为了确保多个进程向单个 FIFO 写入时的原子性写入，每个进程的写入大小必须小于 `PIPE_BUF` 字节。

## 读取和写入 FIFO

在考虑了上一节末尾讨论的事项后，读取和写入 FIFO 与读取和写入管道及常规文件类似。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_372_0.png)

此示例稍显复杂。一个程序 `rdfifo` 创建并打开一个 FIFO 用于读取，并将 FIFO 的输出显示到 `stdout`。另一个程序 `wrffifo` 打开该 FIFO 用于写入。特别有趣的是运行多个写入者实例在不同窗口中，并在运行读取者的窗口中观察它们的输出的过程。

```c
/*  rdfifo.c  Create a FIFO and read from it */
#include <sys/types.h>
#include <sys/stat.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <limits.h>

int main(void)
{
    int fd;                                      /* Descriptor for FIFO */
    int len;                                     /* Bytes read from FIFO */
    char buf[PIPE_BUF];
    mode_t mode = 0666;

    if ((mkfifo("fifo1", mode)) < 0) {
        perror("mkfifo");
        exit(EXIT_FAILURE);
    }
    /* Open the FIFO read-only */
    if ((fd = open("fifo1", O_RDONLY)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }
    /* Read and display the FIFO's output until EOF */
    while ((len = read(fd, buf, PIPE_BUF - 1)) > 0)
        printf("rdfifo read: %s", buf);
    close(fd);

    exit(EXIT_SUCCESS);
}

/*
 * wrfifo.c - Write to a "well-known" FIFO
 */
#include <sys/types.h>
#include <sys/stat.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <limits.h>
#include <time.h>

int main(void)
{
    int fd;                       /* Descriptor for FIFO */
    int len;                     /* Bytes written to FIFO */
    char buf[PIPE_BUF];          /* Ensure atomic writes */
    mode_t mode = 0666;
    time_t tp;                   /* For time call */

    /* Identify myself */
    printf("I am %d\n", getpid());

    /* Open the FIFO write-only */
    if ((fd = open("fifo1", O_WRONLY)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }
    /* Generate some data to write */
    while (1) {
        /* Get the current time */
        time(&tp);
        /* Create the string to write */
        len = sprintf(buf, "wrfifo %d sends %s",
                      getpid(), ctime(&tp));

        /*
         * Use (len + 1) because sprintf does not count
         * the terminating null
         */
        if ((write(fd, buf, len + 1)) < 0) {
            perror("write");
            close(fd);
            exit(EXIT_FAILURE);
        }
        sleep(3);
    }
    close(fd);
    exit(EXIT_SUCCESS);
}
```

这些程序的输出如图 15.5 所示。读者 `rdfifo` 运行在大型 `xterm` 中。三个较小的 `xterm` 各自运行写入者 `wrfifo` 的一个实例。每个写入者的 PID 都显示在它们的屏幕上。每隔三秒钟，写入者会将一条包含其 PID 和当前时间的消息推送到命名管道 `fifo1` 中。如你所见，读者显示收到的消息，并在其前面加上 `rdfifo read` 前缀，以将其输出与从命名管道读取的输入区分开来。

![](img/be588b36b489136ce784030a08a1d3d4_375_0.png)

图 15.5：多个进程向同一个命名管道写入。

值得注意的是，这些程序构成了一个原始的，尽管相对无用的，客户端/服务器应用程序。服务器是 `rdfifo`；它处理通过命名管道发送给它的数据。客户端是每个 `wrfifo` 进程，其唯一目的是向服务器发送消息。

更复杂的客户端/服务器应用程序会对接收到的数据执行某种处理，并向客户端发送某种通知或数据。关于客户端/服务器应用程序的深入讲解远远超出了本书的范围，但请感到满意，因为你刚刚编写了一个！

## 接下来是什么？

本章介绍了最简单形式的进程间通信：管道和命名管道。下一章将继续讨论进程间通信方法，重点讲解共享内存。虽然共享内存 IPC 比管道和命名管道更复杂，但它功能更强大且更灵活，常用于更大、更复杂的应用程序，如 RDBMS（关系数据库管理系统），例如 `Informix` 和 `Oracle`。

## 16— 共享内存

共享内存是你将要学习的三种进程间通信（IPC）类型中的第一种。其他两种风格是信号量和消息队列，它们是下一章的主题。综合起来，这三种类型通常被称为 `System V IPC`，因为它们源自 `System V UNIX`，最初由 `AT&T` 发布。基于 `BSD` 的 `UNIX` 实现以及其他类 `UNIX` 操作系统，包括 `Linux`，也支持它们。

> 关于信号量和消息队列的全面讲解将在第 17 章“信号量和消息队列”中提供。

本章涵盖的主题包括：

- `System V IPC` 的一般描述
- `System V IPC` 的问题
- 共享内存的使用
