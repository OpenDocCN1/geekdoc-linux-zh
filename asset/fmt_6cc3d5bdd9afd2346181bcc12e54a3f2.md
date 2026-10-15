
# 程序 B.2 restart.c

重启库。

```c
#include <errno.h>
#include <fcntl.h>
#include <limits.h>
#include <string.h>
#include <sys/select.h>
#include <sys/time.h>
#include <sys/wait.h>
#include "restart.h"
#define BLKSIZE PIPE_BUF
#define MILLION 100000000
#define D_MILLION 100000000.0
/* 私有函数 */
static int gettimeout(struct timeval end, struct timeval *timeoutp) {
    gettimeofday(timeoutp, NULL);
    timeoutp->tv_sec = end.tv_sec - timeoutp->tv_sec;
    timeoutp->tv_usec = end.tv_usec - timeoutp->tv_usec;
    if (timeoutp->tv_use >= MILLION) {
        timeoutp->tv_sec++;
        timeoutp->tv_use -= MILLION;
    }
    if (timeoutp->tv_use < 0) {
        timeoutp->tv_sec--;
        timeoutp->tv_use += MILLION;
    }
    if ((timeoutp->tv_sec < 0) || ((timeoutp->tv_sec == 0) && (timeoutp->tv_use == 0))) {
        errno = ETIMEOUT;
        return -1;
    }
    return 0;
}
/* 传统函数的重启版本 */
int r_close(int fildes) {
    int retval;
    while ((retval = close(fildes)) == -1 && (errno == EINTR));
    return retval;
}
int r_dup(int fildes, int fildes2) {
    int retval;
    while ((retval = dup2(fildes, fildes2)) == -1 && (errno == EINTR));
    return retval;
}
int r_open2(const char *path, int oflag) {
    int retval;
    while ((retval = open(path, oflag)) == -1 && (errno == EINTR));
    return retval;
}
int r_open3(const char *path, int oflag, mode_t mode) {
    int retval;
    while ((retval = open(path, oflag, mode)) == -1 && (errno == EINTR));
    return retval;
}
size_t r_read(int fd, void *buf, size_t size) {
    ssize_t retval;
    while ((retval = read(fd, buf, size)) == -1 && (errno == EINTR));
    return retval;
}
pid_t r_wait(int *stat_loc) {
    pid_t retval;
    while ((retval = wait(stat_loc)) == -1 && (errno == EINTR));
    return retval;
}
pid_t r_waitpid(pid_t pid, int *stat_loc, int options) {
    pid_t retval;
    while ((retval = waitpid(pid, stat_loc, options)) == -1 && (errno == EINTR));
    return retval;
}
size_t r_write(int fd, void *buf, size_t size) {
    ssize_t retval;
    size_t bytestrite;
    size_t totalbytes;
    for (buf = buf, bytestrite = size, totalbytes = 0; bytestrite > 0; ) {
        retval = write(fd, buf, bytestrite);
        if ((retval == -1) && (errno != EINTR))
            return -1;
        if (retval == -1)
            retval = 0;
        totalbytes += retval;
    }
    return totalbytes;
}
/* 工具函数 */
struct timeval addCurrenttime(double seconds) {
    struct timeval newtime;
    gettimeofday(&newtime, NULL);
    newtime.tv_sec += (int)(seconds);
    newtime.tv_use += (int)(seconds * D_MILLION + 0.5);
    if (newtime.tv_use >= MILLION) {
        newtime.tv_use -= MILLION;
    }
    return newtime;
}
int copyfile(int fromfd, int tofd) {
    int bytesread;
    int totalbytes = 0;
    while ((bytesread = read(fromfd, tofd)) > 0)
        totalbytes += bytesread;
    return totalbytes;
}
ssize_t read(int fd, void *buf, size_t size) {
    char *buf_ptr = (char *)buf;
    size_t bytestread;
    size_t totalbytes;
    for (buf_ptr = (char *)buf, bytestread = size, totalbytes = 0; bytestread > 0; ) {
        int bytesread = read(fd, buf_ptr, bytestread);
        if ((bytesread == 0) && (totalbytes == 0))
            return 0;
        if (bytesread == 0) {
            errno = EINVAL;
            return -1;
        }
        if ((bytesread == -1) && (errno != EINTR))
            return -1;
        if (bytesread == -1)
            bytesread = 0;
        totalbytes += bytesread;
    }
    return totalbytes;
}
int readline(int fd, char *buf, int nbytes) {
    int numread = 0;
    int retval;
    while (numread < nbytes - 1) {
        retval = read(fd, buf + numread, 1);
        if ((retval == -1) && (errno != EINTR))
            continue;
        if ((retval == 0) && (numread == 0))
            return 0;
        if (retval == 0)
            break;
        if (retval == -1)
            return -1;
        numread++;
        if (buf[numread-1] == '\n') {
            buf[numread] = '\0';
            return numread;
        }
    }
    errno = EINVAL;
    return -1;
}
size_t timedread(int fd, void *buf, size_t nbyte, double seconds) {
    struct timeval timedone;
    timedone = addCurrenttime(seconds);
    if (waitftime(fd, timedone) == -1)
        return (size_t) (-1);
    return r_read(fd, buf, nbyte);
}
int readwrite(int fromfd, int tofd) {
  char buf[BLKSIZE];
  int bytesread;
  if ((bytesread = r_read(fromfd, buf, BLKSIZE)) < 0)
    return -1;
  if (bytesread == 0)
    return 0;
  if (r_write(tofd, buf, bytesread) < 0)
    return -1;
  return bytesread;
}
int readwriteblock(int fromfd, int tofd, char *buf, int size) {
  int bytesread;
  bytesread = readblock(fromfd, buf, size);
  if (bytesread != size) /* 只能是 0 或 -1 */
    return bytesread;
  return r_write(tofd, buf, size);
}
```

# 附录 C. UICI 实现

本附录包含了 UICI 实现的源代码。UICI 分三部分：TCP、UDP 和名称解析。TCP 和 UDP UICI 是通过套接字（`sockets`）实现的。提供了不同的名称解析函数实现。名称解析函数被 UICI TCP 和 UDP 使用，但 UICI TCP 和 UDP 之间是相互独立的。C.1 节给出了 UICI TCP 的实现，C.2 节给出了名称解析的实现，C.3 节给出了。

## C.1 面连接的 UICT TCP 实现

本节给出了 sockets 中 UICT TCP 函数的完整实现。

### 程序 C.1 uici.h

包含 UICT 函数原型的头文件。

```
************************************ uici.h *******************/
/* 三个公共 UICT 函数的原型 */
/*****************************************************************/
#define UPORT
typedef unsigned short u_port_t;
int u_open(u_port_t port);
int u_accept(int fd, char *hostn, int hostsize);
int u_connect(u_port_t port, char *hostn);
```

`u_accept` 和 `u_connect` 函数分别调用名称解析函数 `addrname` 和 `nameaddr`。C.2.1 节、C.2.2 节和 C.2.3 节讨论了这些名称解析函数的几种实现。

向没有读取者的套接字写入数据会产生 `SIGPIPE` 信号。如果应用程序不处理此信号，远程主机可能会导致应用程序提前关闭连接。通过 `u_open` 和忽略 `SIGPIPE` 的 `u_ignore_sigpipe`，`SIGPIPE` 的默认操作（终止进程）将生效。

`u_open` 函数还设置了套接字的 `SO_REUSEADDR` 选项，使得服务器在端口未使用时可以立即重用该端口。这在调试期间非常有用，否则在终止服务器后，你必须等待（可能需要几分钟）才能在相同的端口上启动服务器监听。默认最大队列设置为 50，但你可以通过修改 `uici.c` 文件或设置编译器选项 `(-D)` 来更改此值。

`u_accept` 函数带有三个参数调用 `addrname`。第一个参数是 `struct in_addr` 类型的地址，它会被转换为 ASCII 字符串。第二个参数指向存储字符串的缓冲区指针，第三个参数是缓冲区长度。如果缓冲区不足以包含主机名，`addrname` 会静默地截断字符串而不产生错误。如果 `nameaddr` 无法确定主机名，它将使用点进制表示法。

`u_connect` 函数调用 `nameaddr` 将 ASCII 主机名转换为 Internet 地址。如果 `nameaddr` 执行失败，`u_connect` 返回 -1 并设置 `errno` 为 `EINVAL`。

ASCII 主机名可以是传统名称，也可以是点进制表示法的地址。对于后者，`name2addr` 的所有实现都使用 `inet_addr` 将名称转换为地址。当 `u_connect` 被信号中断时，必须以特殊方式处理。如果被信号中断，`u_connect` 将继续异步建立连接，且不应再次调用它。相反，`u_connect` 调用 `select` 等待套接字可用。此时连接即建立。

### 程序 C.2 uici.c

```c
/* uici.c 实现 */
#include <errno.h>
#include <signal.h>
#include <string.h>
#include <unistd.h>
#include <sys/select.h>
#include <sys/socket.h>
#include "uici.h"
#include "uicname.h"
#ifndef MAXBACKLOG
#define MAXBACKLOG 50
#endif
/*
* u_ignore_sigpipe
* 如果默认操作生效，则忽略 SIGPIPE。
*
* 返回: 成功返回 0
*   错误返回 -1 并设置 errno
*/
static int u_ignore_sigpipe() {
    struct sigaction action;
    if (sigaction(SIGPIPE, (struct sigaction*)NULL, &action) == -1) {
        return -1;
    }
    if (action.sa_handler == SIG_DFL) {
        action.sa_handler = SIG_IGN;
        if (sigaction(SIGPIPE, &action, (struct sigaction*)NULL) == -1) {
            return -1;
        }
    }
    return 0;
}
```

```c
/*
* u_open
* 返回一个绑定到给定端口的文件描述符。
* 参数:
*   s = 要绑定的端口号
* 返回:
```
