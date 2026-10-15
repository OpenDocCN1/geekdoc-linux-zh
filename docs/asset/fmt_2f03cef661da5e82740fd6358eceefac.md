
那么什么是管道呢？虽然管道看起来像文件，但它不是文件，也没有与之关联的文件指针。它在概念上就像一条传送带，由固定数量的逻辑块组成，这些逻辑块可以被填满和清空。每次向管道写入时，只要未超出管道的最大大小，就会填满满足该写入所需的块数；如果未达到管道大小限制，则会为下一次写入分配一个新块。已填充的块会被传送到管道的读端，并在被读取时清空。这类管道被称为未命名管道，因为它们在文件系统中不存在于任何位置，它们没有名字。

UNIX 中的未命名管道¹ 通过 `pipe()` 系统调用创建。

```c
#include <unistd.h>
int pipe(int filedes[2]);
```

系统调用 `pipe(fd)` 接收一个大小为 2 的整数数组 `fd`，创建一对文件描述符 `fd[0]` 和 `fd[1]`，分别指向管道 inode 的“读端”和“写端”。如果成功，返回 0，否则返回 -1。之后进程可以使用 `write()` 系统调用向写端 `fd[1]` 写入数据，并使用 `read()` 系统调用从读端 `fd[0]` 读取数据。读端和写端会因 `pipe()` 调用而自动打开。写入的数据按先进先出（FIFO）顺序读取。下面的程序（`demos` 目录中的 `pipedemo0.c`）演示了这个简单的情况。

### 列表 8.1：pipedemo0.c

```c
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>

#define READ_END 0
#define WRITE_END 1
#define NUM 5
#define BUFSIZE 32

int main(int argc, char* argv[])
{
    int i, nbytes;
    int fd[2];
    char message[BUFSIZE + 1];

    if ( -1 == pipe(fd)) {
        perror("pipe call");
        exit(2);
    }

    for ( i = 1; i <= NUM; i++ ) {
        sprintf(message, "hello #%d\n", i);
        write(fd[WRITE_END], message, strlen(message));
    }
    close(fd[WRITE_END]);

    printf("%d messages sent; sleeping a bit. Please wait...\n", NUM);
    sleep(3);

    while ( ( nbytes = read( fd[READ_END], message, BUFSIZE)) != 0 )
    {
        if ( nbytes > 0 ) {
            message[nbytes] = '\0';
            printf("%s", message);
        }
        else
            exit(1);
    }
    fflush(stdout);
    exit(0);
}
```

#### 注意事项

- 在该程序中，`write` 调用没有进行错误检查，而实际上应该进行检查。`while` 循环条件中的 `read()` 进行了错误检查：如果返回值严格小于零，则执行 `exit(1)`。
- `read()` 调用默认是阻塞读取；如果你希望它非阻塞，则必须明确地将其设置为非阻塞。按照设计，对管道的阻塞读取会一直等待数据，只要管道的写端仍保持打开。如果程序在读循环开始前没有关闭管道的写端，它将永远挂起，因为 `read()` 会持续等待数据。如果读循环事先确切地知道期望的字节数，则可以避免这种情况，因为那样它可以只读取那么多字节然后退出循环，但通常人们无法预知要读取多少数据。当然，进程必须在读循环开始之前将数据写入管道，否则将没有数据可读！
- 注意 `read()` 调用总是读取相同数量的数据。此例说明读者可以读取固定大小的块，并将它们组装成更大的块，因为数据是按发送顺序到达的（不同于通过网络发送的数据）。管道没有消息边界的概念——它们只是字节流。
- 最后，注意在调用 `printf()` 将字符串打印到标准输出之前，字符串必须以空字符结尾。

![](img/edd55012c780b4e999320d08ab27959e_416_0.png)

Figure 8.2: Parent and child sharing a pipe.

从管道读取的语义比从文件读取复杂得多。下表总结了当进程尝试从当前有 `p` 个字节尚未被读取的管道中读取 `n` 个字节时会发生什么。

| Pipe Size (p) | Writer open: writer sleeping | Writer open: no writer sleeping | Writer open: non-blocking read | No writer open: blocking read | No writer open: non-blocking read |
| --- | --- | --- | --- | --- | --- |
| p = 0 | Copy n bytes and return n, waiting for data as necessary when the pipe is empty. | Block until data is available, copy it and return its size. | Return -EAGAIN. | Return 0. | Return 0. |
| 0 < p < n |  | Copy p bytes and return p, leaving the buffer empty. |  |  |  |
| p ≥ n | Copy n bytes and return n leaving p-n bytes in the pipe buffer. |  |  |  |  |

语义取决于是否有写入者在之前尝试向管道写入但管道已满时被置于睡眠状态。在非阻塞读取请求中，如果请求的字节数 `n` 大于管道中当前的数据量，并且至少有一个写入者处于睡眠状态，则读取将尝试读取 `n` 个字节，随着管道被清空，写入者将被唤醒以向管道写入。如果没有写入者在睡眠并且管道为空，则读取将阻塞直到有数据可用。

### 8.2.1 Parent and Child Sharing a Pipe

当然，进程没有理由创建管道来向自身写入消息。管道存在的目的是允许两个不同的进程进行通信。通常，一个进程会创建管道，然后 `fork` 一个子进程。`fork` 之后，父进程和子进程各自拥有管道的读端和写端的拷贝，因此会有两个数据通道和总共四个描述符，如图 8.2 所示。

在某些 Unix 系统上，例如 System V Release 4 Unix，管道以全双工模式实现，允许同时写入和读取两个描述符。POSIX 仅允许半双工模式，这意味着数据只能沿管道单向流动，并且
