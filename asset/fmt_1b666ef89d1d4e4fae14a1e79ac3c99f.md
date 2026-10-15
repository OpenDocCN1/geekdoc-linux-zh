
# 第 3 章 套接字引论

## 套接字简介

`sockaddr` 指向一个长度为 `addrlen` 的套接字地址结构。该函数使用其静态缓冲区返回结果，并将指向该缓冲区的指针作为返回值。

> 注意，对结果使用静态存储会导致该函数无法是重入的或不是线程安全的。我们将在第 3.14 节中详细讨论这一点。表现形式是 IPv4 的点分十进制或 IPv6 的十六进制格式，后跟一个空字符。我们在第 3.15 节中方便地调用它。

缓冲区大小至少为 IPv4 的 `INET_ADDRRLEN` 或 IPv6 的 `INET6_ADDRRLEN`（16 或 46 字节）。

```c
char *
nntop(int family, const void *addrptr, char *strptr, size_t len)
{
    const u_char *p = (const u_char *)addrptr;

    if (family == AF_INET) {
        char temp[INET_ADDRSTRLEN];

        snprintf(temp, sizeof(temp), "%d.%d.%d.%d", p[0], p[1], p[2], p[3]);
        if (strlen(temp) >= len) {
            errno = ENOSPC;
            return (NULL);
        }
        strcpy(strptr, temp);
        return (strptr);
    }
    errno = EAFNOSSUPPORT;
    return (NULL);
}
```

我们提供了在我们从流式套接字读取或写入时使用的三个函数。

```c
#include <unp.h>

ssize_t read(int fd, void *buf, size_t bytes);
ssize_t write(int fd, const void *buf, size_t bytes);
ssize_t readline(int fd, void *buf, size_t maxlen);
```

所有函数返回：读取或写入的字节数，出错时返回 -1。

图 3.14 显示了 `read` 函数。图 3.15 显示了 `write` 函数，图 3.16 显示了 `readline` 函数。

### `readn`、`writn` 和 `readline` 函数

```c
#include "unp.h"
ssize_t    /* 从描述符中读取 'n' 个字节。 */
readn(int fd, void *vptr, size_t n)
{
    size_t nleft;
    size_t nread;
    char *ptr;

    ptr = vptr;
    nleft = n;
    while (nleft > 0) {
        if ((nread = read(fd, ptr, nleft)) < 0) {
            if (errno == EINTR) /* 再次调用 */
                nread = 0;
            else
                return (-1);
        } else if (nread == 0) /* 文件结束 */
            break;
        }
    }

    nleft -= nread;
    ptr += nread;
    }
    return (n - nleft);
}
```

图 3.14 `readn` 函数：从描述符中读取 `'n'` 个字节。

```c
#include "unp.h"
ssize_t    /* 向描述符写入 'n' 个字节。 */
writn(int fd, const void *vptr, size_t n)
{
    size_t nleft;
    size_t nwritten;
    const char *ptr;

    ptr = vptr;
    nleft = n;
    while (nleft > 0) {
        if ((nwritten = write(fd, ptr, nleft)) <= 0) {
            if (errno == EINTR) /* 再次调用 */
                nwritten = 0;
            else
                return (-1); /* 错误 */
        }
        nleft -= nwritten;
        ptr += nwritten;
    }
    return (n);
}
```

图 3.15 `writn` 函数：向描述符写入 `'n'` 个字节。

```c
#include "unp.h"

size_t
readline(int fd, void *vptr, size_t maxlen)
{
    ssize_t n, rc;
    char c, *ptr;
    ptr = vptr;
    for (n = 1; n < maxlen; n++) {
        if ((rc = read(fd, &c, 1)) == 1) {
            *ptr++ = c;
            if (c == '\n')
                break;
        } else if (c == 0) {
            if (n == 1)
                return (0); /* EOF，未读到数据 */
        } else {
            break; /* EOF，读取了部分数据 */
        }
    } else {
        if (errno == EINTR)
            goto error;
        return (-1); /* 错误，errno 由 read() 设置 */
    }
    *ptr = 0; /* 像 fgets() 一样空空终止 */
    return (n);
}
error:
```

`test/readline1.c`

我们的三个函数会查找错误 `EINTR`（系统调用被一个捕获的信号中断，我们将在第 5.9 节中详细讨论），并在发生该错误时继续读取或写入。我们在这里处理错误，而不是强制调用者再次调用 `readn` 或 `writn`，因为这三个函数的目的是防止调用者处理短计数（short count）。

在 13.3 中，我们提到 `MSG_WAITALL` 标志可以与 `recv` 函数一起使用，以替代单独 `readline` 函数的需求。

注意，我们的 `readline` 函数为每个字节的数据调用了系统的 `read` 函数。这是低效的，正如 APUE 第 3.9 节所示。我们想做的是通过调用 `read` 获取尽可能多的数据并进行缓冲，然后逐字节检查缓冲区。实现此点的一种方法是使用缓冲区，如我们在 3.8 节所示。图 3.16 显示了 `readline` 的一个版本，它每次读取 `MAXLINE` 字节，并逐字节返回。

```c
#include "unp.h"

static ssize_t
my_read(int fd, char *ptr)
{
    static int read_cnt = 0;
    static char *read_ptr;
    static char read_buf[MAXLINE];

    if (read_cnt < 0) {
        again:
            if ((read_cnt = read(fd, read_buf, sizeof(read_buf))) < 0) {
                if (errno == EINTR)
                    goto again;
                return (-1);
            } else if (read_cnt == 0) {
                return (0);
            }
        }
        read_cnt--;
        *read_ptr++;
        return (1);
    }
}
```
