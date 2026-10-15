
### 3.4 一个为其客户端创建唯一消息队列的服务器。哪种方法更优——使用某些常量路径（例如服务器的可执行文件）作为 `ftok` 的参数，还是使用 `IPC_PRIVATE`？

### 3.5 修改图 4.2 以仅打印 IPC 键和路径。运行 `find` 程序以打印所有映射到相同键的路径。

### 3.6 如果你的系统支持 `sar` 程序（“系统活动报告器”），运行命令 `sar -n 5 6`。这会打印每秒消息队列操作数和每秒信号量操作数，每 5 秒采样一次，共 6 次。

# 第二部分 消息传递

# 第 4 章 管道与 FIFO

## 4.1 引言

管道是 Unix IPC 的原始形式，可以追溯到 1973 年的 Unix 第三版。尽管它们对许多操作非常有用，但其根本局限性在于没有名称，因此只能由相关进程使用。这在 System III Unix (1982) 中通过增加 FIFO 得到了纠正。FIFO 也称为命名管道。管道和 FIFO 都使用普通的 `read` 和 `write` 函数进行访问。

> 从技术上讲，如果能够在进程之间传递描述符，则 FIFO 可以在无关进程之间使用（我们在本文的第 15.8 节中描述，对应 Unix V 的第 14.7 节）。但从实际目的考虑，管道通常用于具有祖先的进程之间。

本章描述了管道和 FIFO 的创建与使用。我们使用一个简单的文件服务器示例，并查看一些客户端-服务器设计问题：需要多少个 IPC 通道、迭代服务器与并发服务器，以及字节流与消息接口。

## 4.2 一个简单的客户端-服务器示例

图 4.1 所示的客户端-服务器示例贯穿本章和第 6 章，用于说明管道、FIFO 和 System V 消息队列。客户端从标准输入读取路径并写入 IPC 通。服务器从 IPC 通道读取该路径并尝试打开文件进行读取。如果服务器可以打开文件，服务器将通过读取文件并将其写入 IPC 通道来响应；否则，服务器用错误消息进行响应。

## 4.3 管道

所有的 Unix 版本都提供了管道。管道通过 `pipe` 函数创建，并提供单向（单边）数据流。

```c
#include <unistd.h>
int pipe(int fd[2]);
```

返回两个文件描述符：`fd[0]` 用于打开以读取，`fd[1]` 用于打开以写入。

> 某些 Unix 版本（特别是 SVR4）提供全双工管道，两端均可读写。另一种创建全双工 IPC 通道的方法是使用 `socketpair` 函数，这在大多数 Unix 系统上都有效。对于大多数管道用途，半双工管道就足够了。

Posix-1999 只需要半双工管道，我们在本章中假设如此。

`S_ISFIFO` 宏可以用于判断描述符是管道还是 FIFO。它的唯一参数是 `stat` 结构中的 `st_mode` 成员，其求值结果（非零）假(0)。对于管道，该结构由 `fstat` 函数填充。对于 FIFO，该结构由 `fstat`、`lstat` 或 `statat` 函数填充。

图 4.2 显示了单个进程中的管道的貌。

尽管管道是由一个进程创建的，但很少在单个进程内使用。（我们在图 5.14 中展示了单个进程内的管道示例。）管道通常以以下方式在两个不同进程（父进程和子进程）之间进行通信。首先，一个进程（将作为父进程）创建一个管道并 `fork` 创建它自身的副本，如图 4.3 所示。

![](img/1541bd224d292c30573e864db3959d59_59_0.png)

图 4.2 单个进程中的管道。

![](img/1541bd224d292c30573e864db3959d59_60_0.png)

图 4.3 `fork` 之后单个进程中的管道。

接下来，父进程关闭一个管道的读端，子进程关闭同一条管道的写端。这在两个进程之间提供了单向数据流，如图 4.4 所示。

![](img/1541bd224d292c30573e864db3959d59_60_2.png)

图 4.4 两个进程之间的管道。

当我们向 Unix shell 输入如 `who | sort` 的命令时，shell 执行之前描述的步骤来创建管道。shell 将管道的读端转换为标准输入，将写端转换为标准输出。

标准输出。通常这里是文件的内容，但如果指定的路径无法打开，服务器将返回一条错误消息。

图 4.10 显示了服务器函数。

```c
#include "unipc.h" pipe/server.c
void server(int readfd, int writefd)
{
    int fd;
    size_t n;
    char buff[MAXLINE + 1];

    /* read pathname from IPC channel */
    if ((n = Read(fd, buff, MAXLINE)) == 0)
        err_quit("end-of-file while reading pathname: %s", buff);
    buff[n] = '\0';

    if ((fd = open(buff, O_RDONLY)) < 0) {
        /* error: must tell client */
        printf("%s: cannot open, %s\n", buff, strerror(errno));
    } else {
        n = strlen(buff);
        Write(writefd, buff, n);
    } else {
        /* open success: copy file to IPC channel */
        while ((n = Read(fd, buff, MAXLINE)) > 0)
            Write(writefd, buff, n);
        Close(fd);
    }
}
```

![](img/1541bd224d292c30573e864db3959d59_64_0.png)

### 从管道读取路径

路径是由客户端写入管道并以终止符结束的。请注意，读管道在有数据时就会返回；它不会等待请求的字节数（示例中的 `MAXLINE`）。

### 打开文件，处理错误

文件以读模式打开，如果发生错误，则通过管道将错误消息字符串返回给客户端。我们使用 `strerror` 函数来返回与 `errno` 对应的消息字符串。（Unpv1 的第 690–691 页详细讨论了 `strerror(function)`）。

### 将文件复制到管道

如果打开成功，文件内容将被复制到管道中。

我们可以看到当路径正确以及发生错误时程序的输出。

### 管道与 FIFOs

```
solaris % mainpipe
/etc/inet/ntp.conf
multicastclient 224.0.1.1
driftfile %/etc/inet/ntp.drift
solaris % mainpipe
/etc/shadow
/etc/shadow: can't open, Permission denied
solaris % mainpipe
/no/such/file
/no/such/file: can't open, No such file or directory
```

- 一个包含两行的文件
- 一个我们无法读取的文件
- 一个不存在的文件

## 4.4 全双工管道

我们在上一节中提到，某些系统提供全双工管道：SVR4 的 `pipe` 函数以及许多内核提供的 `socketpair()` 函数。全双工管道究竟是做什么？首先，我们可以考虑如图 4.11 所示的半双工管道，它是图 4.2 的修改版，去掉了进程部分。

![](img/1541bd224d292c30573e864db3959d59_65_0.png)

图 4.11 半双工管道。

全双工管道可以像图 4.12 所示那样实现。这意味着管道只存在一个缓冲区，任何写入管道（通过一个描述符）的写入都会追加到缓冲区中，而对管道的任何读取（通过任一描述符）都只是从缓冲区头部取数据。
