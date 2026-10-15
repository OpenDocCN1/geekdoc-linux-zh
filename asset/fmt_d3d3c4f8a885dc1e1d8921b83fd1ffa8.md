
此代码没有进行错误检查。

文件描述符代表一个打开的文件或设备，可以被看作文件描述符表的索引。文件描述符表位于进程用户区域，提供了对关联文件或设备的系统信息。

当你从 shell 执行程序时，程序启动时带有三个关联的文件描述符：`STDIN_FILENO`、`STDOUT_FILENO` 和 `STDERR_FILENO`。`STDIN_FILENO` 和 `STDOUT_FILENO` 分别是标准输入和标准输出。默认情况下，这些流通常对应键盘输入和屏幕输出。程序应该使用 `STDERR_FILENO`（标准错误设备）处理错误信息，永远不要忘记它。在遗留代码中，标准输入、标准输出和错误分别由 0、1 和 2 表示。然而，你应该始终使用它们的符号名称而不是这些数值。第 4.6 解释了文件描述符的工作原理。

### 练习 4.2

执行以下代码会发生什么？

```c
char *buf;
ssize_t bytesread;
bytesread = read(STDIN_FILENO, buf, 100);
```

答案：

该代码段可以通过编译，但没有为 `buf` 分配空间。`read` 的结果不可预测的，但最可能会产生内存访问违规。`buf` 是存储在栈上的自动变量，它没有初始化为任何特定值。内存中恰好包含什么会被视为读取缓冲区的地址。

程序 4.1 中的 `readline` 函数每次读取一个字节并将其放入固定大小的缓冲区中，直到遇到换行符（`'\n'`）或发生错误。该函数处理文件结束（EOF）、受限的缓冲区大小以及信号中断。`readline` 函数返回读取的字节数，或者在发生错误时返回 -1。返回值为 0 表示读取的字节数。在这种情况下，缓冲区包含一个以换行符结尾的字符串。返回值为 -1 表示 `errno` 被设置为以下错误之一：

- 读取时发生错误。
- 至少读取了一个字节，但在读取到换行符之前发生了文件结束。
- 读取了 `nbytes-1` 个字节，且未找到换行符。

当成功返回大于 0 的值时，缓冲区包含一个以换行符结尾的字符串。如果 `readline` 读取到换行符，它会将该行视为错误。`readline` 函数在附录 B 的 `restart` 库可用。

## 程序 4.1 readline.c

`readline` 函数从文件中读取下一行。

```c
#include <errno.h>
#include <unistd.h>
int readline(int fd, char *buf, int nbytes) {
    int numread = 0;
    int returnval;
    while (numread < nbytes - 1) {
        returnval = read(fd, buf + numread, 1);
        if ((returnval == -1) && (errno == EINTR)) {
            continue;
        }
        if ((returnval == 0) && (numread == 0)) {
            return 0;
        }
        if (returnval == 0) {
            break;
        }
        if (returnval == -1) {
            return -1;
        }
        numread++;
        if (buf[numread] == '\n') {
            buf[numread] = '\0';
            return numread;
        }
    }
    errno = EINVAL;
    return -1;
}
```

## 示例 4.3

以下代码段调用程序 4.1 的 `readline` 函数，从标准输入读取最多 99 字节的行。

```c
int bytesread;
char mybuf[100];
bytesread = readline(STDIN_FILENO, mybuf, sizeof(mybuf));
```

## 练习 4.4

在什么情况下，程序 4.1 的 `readline` 函数会返回一个没有换行符的缓冲区？

答案：

这只有在返回值为 0 或 -1 时才可能发生。返回 0 表示没有读取到任何内容。返回 -1 表示发生了某种错误。在任何情况下，缓冲区可能不包含字符串。

`write` 函数尝试将用户缓冲区 `buf` 中的 `nbyte` 字节输出到文件描述符 `fildes` 代表的文件。

### 概要

```c
#include <unistd.h>
ssize_t write(int fildes, const void *buf, size_t nbyte);
```

### POSIX

如果成功，`write` 返回实际写入的字节数。如果失败，`write` 返回 -1 并设置 `errno`。下表列出了 `write` 的强制性错误。

| errno | cause |
|---|---|
| `ECONNRESET` | 尝试对未连接的套接字写入 |
| `EAGAIN` | 文件描述符设置了 `O_NONBLOCK` 且线程将被延迟 |
| `EBADF` | `fildes` 不是有效的文件描述符或不可写 |
| `EFBIG` | 尝试写入超过实现定义最大限制的文件；该文件是普通文件，`nbyte` 大于0，且起始位置超过了最大偏移量 |
| `EINTR` | `write` 由于接收到信号而终止，且没有数据传输 |
| `EIO` | 进程是后台进程组的成员并尝试写入控制终端，设置了 `TOSTOP`，且既未阻塞也忽略 `SIGTTO`，且进程组已孤儿化 |
| `ENOSPC` | 包含文件的设备上没有剩余空间 |
| `EPIPE` | 尝试向未打开读取的管道或 FIFO 写入，或者其只有一个端点打开（线程也可能获得 `SIGPIPE`，或尝试对已关闭写入或未连接的套接字写入（如果未连接，也会产生 `SIGPIPE` 信号）） |
| `EWOULDBLOCK` | 文件描述符是标记为 `O_NONBLOCK` 的套接字，且 `write` 将导致阻塞（`EAGAIN` 为备选） |

## 练习 4.5

以下代码段可能会出现什么问题？

```c
#define BLKSIZE 1024
char buf[BLKSIZE];
read(STDIN_FILENO, buf, BLKSIZE);
write(STDOUT_FILENO, buf, BLKSIZE);
```

答案：

`write` 函数假设 `read` 已经用 `BLKSIZE` 字节填充了 `buf`。然而，`read` 可能会失败或没有读取完整的 `BLKSIZE` 字节。在这两种情况下，`write` 输出的是垃圾数据。

## 练习 4.6

从标准输入读取并写入标准输出的代码段可能会出现什么问题？

```c
#define BLKSIZE 1024
char buf[BLKSIZE];
size_t bytesread;
bytesread = read(STDIN_FILENO, buf, BLKSIZE);
if (bytesread > 0)
write(STDOUT_FILENO, buf, BLKSIZE);
```

答案：

`write` 函数假设 `read` 已经用 `BLKSIZE` 字节填充了 `buf`。然而，`read` 可能会失败或没有读取完整的 `BLKSIZE` 字节。在这两种情况下，`write` 输出的是垃圾数据。

```c
ssize_t retval;
while ((retval = read(fd, buf, size)) == -1 && errno == EINTR) {
  return retval;
}
```

### 程序 4.4 r_write.c

`r_write.c` 函数与 `write` 类似，不同之处如果被信号中断，会被重新启动并写入请求的全部字节。

```c
#include <errno.h>
#include <unistd.h>
ssize_t r_write(int fd, void *buf, size_t size) {
  char *buf;
  size_t bytestrowrite;
  ssize_t byteswritten;
  ssize_t totalbytes;
  for (buf = buf, bytestrowrite = size, totalbytes = 0;
       bytestrowrite > 0;
       buf += byteswritten, bytestrowrite -= byteswritten) {
    byteswritten = write(fd, buf, bytestrowrite);
    if (byteswritten == -1 && (errno != EINTR))
      return -1;
    if (byteswritten == -1)
      byteswritten = 0;
    totalbytes += byteswritten;
  }
  return totalbytes;
}
```

`r_read` 和 `r_write` 函数可以极大简化需要在读写的同时需要处理信号的程序。

程序 4.5 显示了 `readwrite` 函数，它从一个文件描述符读取字节，并将读取的所有字节写入另一个文件描述符。它使用一个大小为 `PIPE_BUF` 的缓冲区来传输最多 `PIPE_BUF` 字节。这对于写入大小为 `PIPE_BUF` 字节的管道非常有用，它是原子的。程序 4.6 显示了使用 `readwrite` 函数的 `copyfile` 版本。将其与程序 4.2 进行对比。

### 程序 4.5 readwrite.c

从一个文件描述符读取并将读取的所有字节写入另一个文件描述符的程序。

```c
#include <limits.h>
#include <restart.h>
#define BLKSIZE PIPE_BUF
int readwrite(int fromfd, int tofd) {
  char buf[BLKSIZE];
  int bytesread;
  if ((bytesread = r_read(fromfd, buf, BLKSIZE)) == -1)
    return -1;
  if (bytesread == 0)
    return 0;
  if (r_write(tofd, buf, bytesread) == -1)
    return -1;
  return bytesread;
}
```

### 程序 4.6 copyfile.c

使用 `r_read` 和 `r_write` 的 `copyfile` 简化实现。

```c
#include <unistd.h>
#include "restart.h"
#define BLKSIZE 1024
int copyfile(int fromfd, int tofd) {
  char buf[BLKSIZE];
  int bytesread;
  int byteswritten;
  int totalbytes = 0;
  for ( ; ; ) {
    if ((bytesread = r_read(fromfd, buf, BLKSIZE)) <= 0)
      break;
    if ((byteswritten = r_write(tofd, buf, bytesread)) == -1)
      break;
    totalbytes += byteswritten;
  }
  return totalbytes;
}
```

`r_write` 函数写入所有字节，并在被信号中断时重新启动写入，且通常重启的字节数比写入的少。`r_read` 仅重启比请求更的字节。`reread` 函数是 `read` 的一个版本，它会继续读取直到读取了请求的字节数或发生错误。程序 4.7 显示了读取结构体的实现。`reread` 函数是 restart 库的一部分。它对于读取结构体特别有用。

## 程序 4.7 readblock.c

一个读取特定数量字节的函数。

```c
#include <errno.h>
#include <unistd.h>
ssize_t readblock(int fd, void *buf, size_t size) {
  char *bufp;
  size_t bytestread;
  size_t bytesread;
  size_t totalbytes;
  for (buf = buf, bytestread = size, totalbytes = 0;
       bytestread > 0;
       buf += bytesread, bytestread -= bytesread) {
     bytesread = read(fd, buf, bytestread);
     if ((bytesread == 0) && (totalbytes == 0))
        return 0;
     }
     if (bytesread == 0) {
       errno = EINVAL;
       return -1;
     }
     if ((bytesread == -1 && (errno != EINTR)) {
       return -1;
     }
     if (bytesread == -1)
       bytesread = 0;
     totalbytes += bytesread;
  }
  return totalbytes;
}
```

`readblock` 的返回值只有三种可能。`readblock` 函数在读取任何字节之前发生文件结束时返回 0。这发生在第一次调用 `read` 返回 0 时。如果 `readblock` 成功，它返回 `size`，表示成功读取了请求的字节数。否则，`readblock` 返回 -1 并设置 `errno`。如果 `readblock` 在读取了部分但不是全部需要的字节后到达文件结束，它将返回 -1 并设置 `errno`。

## 示例 4.10

以下代码段用于从一个文件描述符读取。

```c
struct {
  int x;
  int y;
};
if (readblock(fd, &point, sizeof(point)) <= 0)
  printf(stderr, "Cannot read\n");
```

### 程序 4.8 readwrite.c

一个从一个文件描述符读取并将所有字节写入另一个文件描述符的程序。

```c
#include "restart.h"
int readwrite(int fromfd, int tofd) {
  int bytesread;
  if ((bytesread = r_read(fromfd, buf, PIPE_BUF)) == -1)
    return -1;
  if (bytesread == 0)
    return 0;
  if (r_write(tofd, buf, bytesread) == -1)
    return -1;
  return bytesread;
}
```

## 4.3 打开和关闭文件

`open` 函数将文件描述符（句柄）与文件关联。`oflag` 参数指定访问模式和标志。如果你使用 `O_CREAT`，你必须添加第三个参数来指定权限。

**用法**

```c
#include <fcntl.h>
#include <sys/stat.h>
int open(const char *path, int oflag, ...);
```

如果成功，返回表示文件描述符的非负整数。如果失败，返回 -1 并设置 `errno`。下表列出了 `open` 的错误。

| errno | 原因 |
| :--- | :--- |
| `EACCES` | 拒绝访问 |
| `EEXIST` | 设置了 `O_CREAT` 和 `O_EXCL`，文件存在 |
| `EINTR` | 打开时捕获信号 |
| `EISDIR` | 路径组件不是目录 |
| `ELOOP` | 解析存在循环 |
| `EMFILE` | 最大打开文件描述符 |
| `ENAMETONG` | 路径超过 `PATH_MAX` |
| `ENFILE` | 当前允许打开的文件数 |
| `ENOENT` | 文件或目录不存在 |
| `ENSPC` | 新文件无法扩展 |
| `ENXIO` | 设置了 `O_NONBLOCK`，文件为 FIFO |
| `EOVERFLOW` | 特殊文件无法用对象表示 |
| `EROFS` | 文件位于只读文件系统上 |
| `EOTTY` | 设备是终端 |

通过对访问模式和标志所需的组合进行按位或（`|`）操作来构造标志。访问模式的 POSIX 值为 `O_RDONLY`、`O_WRONLY` 和 `O_RDWR`。你必须指定其中一个（只读、只写）。

额外的标志包括 `O_APPEND`、`O_CREATE`、`O_EXCL`、`O_NOCTTY`、`O_NONBLOCK` 和 `O_TRUNC`。`O_APPEND` 标志在写入时将文件移动到末尾。相比之下，`O_TRUNC` 将文件的长度截断为 0。`O_CREATE` 标志在文件不存在时创建一个。如果你使用 `O_CREAT`，必须额外添加第三个参数来指定权限。为了避免覆盖现有文件，使用组合 `O_CREAT|O_EXCL`。如果文件存在，这将返回错误。

后续的读或写操作，操作将失败。

### 示例 4.13

以下代码段在发生信号后重新打开文件。

```c
int myfd;
```
