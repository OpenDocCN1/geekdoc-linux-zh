
`sock_bind_wild`将通配符地址和临时端口绑定到套接字上。`sock_cmp_addr`比较两个套接字地址结构的地址部分，`sock_cmp_port`比较两个套接字地址结构的端口号。`sock_get_port`将套接字地址结构的主机部分转换为表示格式（不是端口号）。`sock_set_addr`仅将套接字地址结构的地址部分设置为`ptr`所向的值，`sock_set_port`仅将套接字地址结构的端口号。`sock_set_wild`将套接字地址结构的地址部分设置为通配符。与文中所有函数一样，我们提供了一个名称以"s"开头的包装函数，用于所有这些返回值非`void`的函数，并通常在我们的程序中调用该包装函数。我们没有显示所有这些函数的源代码，但它们是免费提供的（参见前言）。

[ LiB 团队 ]

# 3.9 read, write, 和 readline 函数

流套接字（例如 TCP 套接字）在`read`和`write`函数上的行为与普通文件 I/O 不同。在流套接字上进行`read`或`write`输出的字节数可能少于请求数，但这并不是错误条件。原因是内核可能达到了缓冲区限制。某些 Unix 版本向管道写入超过 4,096 字节时，如果需要再次调用`read`或`write`函数，也会表现出这种行为。这种情况在可读的流套接字上是可能的，但只有在套接字是非阻塞的情况下，通常才会出现在写入操作中。尽管如此，我们总是调用自己编写的函数而不是`write`，以防实现返回短计数（short count）。

我们提供了每次从流套接字读取或向其写入时都会用到的三个函数：

```
#include "unp.h"

size_t read(int fd, *buf, size_t nbytes);

size_t write(int fd, const void *buf, size_t nbytes);

size_t readline(int fd, *buf, size_t maxlen);
```

全部返回：读取或写入的字节数，错误时返回 -1

图 3.15 显示了`read`函数，图 3.16 显示了`write`函数，图 3.17 显示了`readline`函数。

## 图 3.15 read 函数：从描述符读取 n 字节。

`lib/read.c`

```
#include "unp.h"

size_t                 /* 从描述符读取 "n" 字节。 */
read(int fd, void *vptr, size_t n)
{
    size_t nleft;
    size_t nread;
    char *ptr;
    ptr = vptr;
    nleft = n;
    while (nleft > 0) {
        if ((nread = read(fd, ptr, nleft)) < 0) {
            if (errno == EINTR) {
                continue;
            } else {
                return (-1);
            }
        } else if (nread == 0) {
            break;
        }
        nleft -= nread;
        ptr += nread;
    }
    return (nread);
}
```

## 图 3.16 write 函数：向描述符写入 n 字节。

`lib/write.c`

```
#include "unp.h"

ssize_t                 /* 向描述符写入 "n" 字节。 */
write(int fd, const void *buf, size_t n)
{
    size_t nleft;
    ssize_t nwritten;
    const char *ptr;
    ptr = buf;
    nleft = n;
    while (nleft > 0) {
        if ((nwritten = write(fd, ptr, nleft)) < 0) {
            if (errno == EINTR) {
                continue;
            } else {
                return (-1);
            }
        }
        nleft -= nwritten;
        ptr += nwritten;
    }
    return (nwritten);
}
```

## 图 3.17 readline 函数：从描述符读取一行。

`lib/readline.c`

```
#include "unp.h"

size_t                 /* 从描述符读取一行。 */
readline(int fd, void *vptr, size_t maxlen)
{
    size_t nleft;
    size_t nread;
    char *ptr;
    char c;
    ptr = vptr;
    nleft = maxlen;
    while (nleft > 0) {
        if ((nread = read(fd, &c, 1)) < 0) {
            if (errno == EINTR) {
                continue;
            } else {
                return (-1);
            }
        } else if (nread == 0) {
            break;
        }
        *ptr++ = c;
        if (c == '\n') {
            break;
        }
        nleft--;
    }
    return (ptr - (char *)vptr);
}
```

```c
static int read_cnt;
static char *read_ptr;
static char *read_buf[MAXLINE];
ssize_t
my_read(int fd, char *ptr)
{
    if (read_cnt <= 0) {
    again:
        if ((read_cnt = read(fd, read_buf, sizeof(read_buf))) < 0) {
            if (errno == EINTR)
                goto again;
            return (-1);
        } else if (read_cnt == 0)
            return (0);
        read_ptr = read_buf;
    }
    read_cnt--;
    *ptr = *read_ptr++;
    return (1);
}
ssize_t
readline(int n, void *vptr, size_t maxlen)
{
    ssize_t n, rc;
    char c, *ptr;
    ptr = vptr;
    for (n = 0; n < maxlen; n++) {
        if ((rc = my_read(fd, &c)) == 1) {
            *ptr++ = c;
            if (c == '\n')
                break; /* newline is stored, like fgets() */
        } else if (rc == 0) {
            *ptr = 0;
            return (n - 1); /* EOF, n - 1 bytes were read */
        } else
            return (-1); /* error, errno set by read() */
    }
    *ptr = 0; /* null terminate like fgets() */
    return (n);
}
ssize_t
readlinebuf(void **vptrptr)
{
    if (read_cnt)
        *vptrptr = read_ptr;
```
