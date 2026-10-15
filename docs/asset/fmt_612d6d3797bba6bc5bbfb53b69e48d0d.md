
（注：由于提供的原文文本存在严重的重复，此处译文已基于核心内容进行去重翻译。）

## 4.5 popen 和 pclose 函数

作为管道的另一个示例，库提供了 `popen()`，它创建一个管道并启动另一个进程。shell 或 `cat` 程序的输出被复制到标准输出。

这种实现与图 4.8 中的实现的区别在于，我们现在依赖于系统程序生成的错误消息，而这通常是不够的。例如，在 Solaris 2.6 中，尝试读取我们没有权限的文件时会得到以下错误：

```
solaris $ cat /shadow

cat: cannot open /shadow
```

在 BSD/OS 3.1 下，尝试读取类似的文件会得到更详细的错误：

```
bsdi $ cat /master.passwd

cat: /master.passwd: cannot open [Permission denied]
```

还要注意到，在这种情况下 `popen` 的调用是成功的，但 `fgets` 第一次调用时仅返回文件结束符。`cat` 程序将其错误消息写入标准错误，`popen` 对其没有特殊处理——只有标准输出被重定向到它创建的管道。

### 示例

图 4.15 显示了使用 `popen` 函数和 `cat` 程序的另一种客户端解决方案。

```c
1 #include "unipc.h"
2 int
3 main(int argc, char **argv)
4 {
5     size_t n;
6     char buff[MAXLINE], command[MAXLINE];
7     FILE *fp;
8     /* read pathname */
9     fgets(buff, MAXLINE, stdin);
10    n = strlen(buff);    /* fgets() guarantees byte at end */
11    if (buff[n-1] == '\n')
12        buff[n-1] = 0;
13    printf("%s:%s", command, command);
14    fp = popen(command, "r*");
15    /* copy from pipe to standard output */
16    while (fgets(buff, MAXLINE, fp) != NULL)
17        fputs(buff, stdout);
18    pclose(fp);
19    exit(0);
20 }
```

图 4.15 使用 `popen` 的客户端-服务器。

## 4.6 FIFOs

管道（Pipes）没有名称，它们最大的缺点是只能在具有共同父进程的进程之间使用。两个不相关的进程无法在其之间创建管道并用于进程间通信（IPC，忽略描述符传递）。

FIFO 代表“先进先出”（first in, first out），Unix FIFO 与管道类似。它是一个单向（半双工）的数据流。与管道不同，FIFO 关联了一个路径名，允许不相关的进程访问同一个 FIFO。FIFO 也称为命名管道（named pipes）。

FIFO 通过 `mkfifo` 函数创建。

```c
#include <sys/types.h>
#include <sys/stat.h>

int mkfifo(const char *pathname, mode_t mode);

返回值：成功时返回 0，错误时返回 -1
```

`pathname` 是一个标准的 Unix 路径，这就是 FIFO 的名称。第二个参数指定文件权限位，类似于文件的权限位。图 2.4 显示了来自 `/sys/stat.h` 头文件的六个常量，用于指定 FIFO 的这些权限位位。

`mkfifo` 函数隐含了 `O_CREATE | O_EXCL`。这意味着它会创建一个新的 FIFO，或者如果命名 FIFO 已经存在，则返回 `EEXIST` 错误。如果不需要创建命名 FIFO，请调用 `open` 而不是 `mkfifo`。要打开已存在的 FIFO 或在其不存在时创建一个新 FIFO，请调用 `mkfifo`，检查是否发生 `EEXIST` 错误，如果发生，则改调用 `open`。

`mkfifo` 命令也可以创建 FIFO。这可以从 shell 脚本或命令行中使用。

一旦创建了 FIFO，必须以只读或只写的模式打开，可以使用 `open` 函数或标准 I/O 函数（如 `fopen`）。FIFO 必须以只读或只写模式打开。它不能以读-写模式打开，因为 FIFO 是半双工的。

向管道或 FIFO 写入总是追加数据，而读取总是返回管道或 FIFO 开头的内容。如果对管道或 FIFO 调用 `seek`，将返回错误 `EPIPE`。

### 示例

我们现在重新实现图 4.8 中的客户端-服务器模型，使用两个 FIFO 替替管道。我们的客户端和服务器函数保持不变；所有更改都在 `main` 函数中，我们在图 4.16 中展示。

```c
#include <unistd.h>                               --pipe/mainfifo.c

#define FIFO1                               "/tmp/fifo.1"
#define FIFO2                               "/tmp/fifo.2"

void client(int, int), server(int, int);
```

```c
int
main(int argc, char **argv) 
{
    int readfd, writefd;
    pid_t childpid;

    /* 创建两个 FIFO；如果已存在则 OK */
    if (mkfifo(FIFO1, FILE_MODE) < 0 && (errno != EEXIST)) {
        err_sys("can't create %s", FIFO1);
        if (mkfifo(FIFO2, FILE_MODE) < 0 && (errno != EEXIST)) {
            unlink(FIFO1);
            err_sys("can't create %s", FIFO2);
        }
    }

    if ((childpid = fork()) == 0) { /* 子进程 */
        readfd = open(FIFO1, O_RDONLY);
        writefd = open(FIFO2, O_WRONLY);
        server(readfd, writefd);
        exit(0);
    }

    /* 父进程 */
    writefd = open(FIFO1, O_WRONLY, 0);
    readfd = open(FIFO2, O_RDONLY);
    client(readfd, writefd);
    waitpid(childpid, NULL, 0); /* 等待子进程终止 */
    close(readfd);
    close(writefd);
    unlink(FIFO1);
    unlink(FIFO2);
    exit(0);
}
```

### 创建两个 FIFO

在 `/tmp` 文件系统中创建了两个 FIFO。如果 FIFO 已经存在，即 `FILE_MODE` 在我们的 `unpipic.h` 头文件（图 4.1）中定义为

```c
#define FILE_MODE  S_IRUSR | S_IRGRP | S_IROTH

             /* 新文件的默认权限 */
```
