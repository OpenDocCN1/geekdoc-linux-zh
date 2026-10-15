
| 函数 | strerror (errno) | 是否终止？ | syslog 级别 |
|---|---|---|---|
| err_dump | | abort(); | LOG_ERR |
| err_msg | yes | return; | LOG_INFO |
| err_quit | no | exit(1); | LOG_ERR |
| err_ret | yes | return; | LOG_INFO |
| err_sys | yes | exit(1); | LOG_ERR |
| err_xti | yes | exit(1); | LOG_ERR |
| err_xtit | yes | return; | LOG_INFO |

图 D.4 标准错误函数总结。

图 D.5 显示了图 D.4 中的前五个函数。

## D.4节 标准错误函数

```c
va_list ap;

va_start(ap, fmt);
err_doit(1, LOG_INFO, fmt, ap);
va_end(ap);
return;
}
)
```

> /* 与系统调用相关的致命错误。
>  * 打印消息并终止。... */

```c
void
err_sys(const char *fmt,...)
{
    va_list ap;
    va_start(ap, fmt);
    err_doit(1, LOG_ERR, fmt, ap);
    va_end(ap);
    exit(1);
}
```

> /* 与系统调用相关的致命错误。
>  * 打印消息，转储核心映像并终止。* */

```c
void
err_dump(const char *fmt,...)
{
    va_list ap;
    va_start(ap, fmt);
    err_doit(1, LOG_ERR, fmt, ap);
    va_end(ap);
    abort(); /* 转储核心映像并终止 */
    exit(1);   /* 不应该执行到这里 */
}
```

> /* 与系统调用相关的非致命错误。
>  * 打印消息并返回。 */

```c
void
err_msg(const char *fmt,...)
{
    va_list ap;
    va_start(ap, fmt);
    err_doit(0, LOG_INFO, fmt, ap);
    va_end(ap);
    return;
}
```

> /* 与系统调用相关的致命错误。
>  * 打印消息并终止。 */

```c
void
err_quit(const char *fmt,...)
{
    va_list ap;
    va_start(ap, fmt);
    err_doit(0, LOG_ERR, fmt, ap);
    va_end(ap);
    exit(1);
}
```

/* 打印消息并返回调用者。 */
/* 调用者指定了 'errnoflag' 和 'level'。 */

```c
static void
err_doit(int errnoflag, int level, const char *fmt, va_list ap)
{
    int   errno_save, n;
    buf[MAXLINE];
    errno_save = errno;      /* 可能需要打印的值 */
#ifdef HAVE_VSPRINT
    vsnprintf(buf, MAXLINE, fmt, ap);  /* 这是安全的 */
#else
    vsnprintf(buf, fmt, ap);      /* 这是不安全的 */
#endif
    n = strlen(buf);
    if (errnoflag)
        snprintf(buf + n, MAXLINE - n, "%s", strerror(errno_save));
        strcat(buf, "\n");
    if (proc()) {
        daemon(buf);
        syslog(level, buf);
    } else {
        fflush(stdout);      /* 以防 stdout 和 stderr 相同 */
        write(stderr, buf);
        fflush(stderr);
    }
    return;
}
```

图 D.5 我们的标准错误函数。

## 附录 D

## 附录 E：部分练习题

### 1.3 要查找有关此错误的更多信息，首先使用 `grep` 在 `<sys/errno.h>` 头文件中搜索该字符串。

```bash
aix % grep "Address family not supported" /usr/include/errno.h
```
#define ENOSSUPPORT /* 地址族不支持 */
#define EADDRINUSE  /* 地址已在使用 */

```bash
aix % man socket
```

### 1.4 我们将第一个声明更改为

```c
int sockfd, n, counter = 0;
```

我们添加语句

```c
counter++;
```

作为 `while` 循环的第一条语句。最后，我们在终止之前执行

```c
printf("counter = %d\n", counter);
```
打印出的值始终为 1。

### 1.5 我们声明了一个 `int` 类型 `i`，并将 `write` 的调用更改为

```c
for (i = 0; i < strlen(buff); i++)
    write(fd, &buff[i], 1);
```
结果各异，取决于客户端和服务器主机。如果客户端和服务器在同一台主机上，计数器通常为 1，这意味着尽管服务器写入了 2 个字节，数据仍通过一次读取返回。但如果客户端运行在 Solaris 2.5 上，而服务器运行在 //OS 下，计数器通常为 2。如果我们在以太网上以数据包形式写入，我们会看到第一个字符作为一个数据包发送，但数据包包含了剩余的 25 个字符。（我们在第 7.9 节对 Nagle 算法的讨论解释了这种行为。）如果客户端运行在 BSD/OS 3.0 上而服务器运行在 Solaris 2 下，我们看到每个字符都通过自己的数据包发送。此处的目的是重申，不同的 TCP 对数据的处理方式不同，我们的应用程序必须准备好以字节流的形式读取数据，直到遇到数据流

## 第 2 章

2.1 所有的 RFC 都可以通过电子邮件、匿名 FTP 或万维网免费获取。一个起点是 `http://www.ietf.org`。目录 `ftp://isi.edu/in-notes` 是 RFC 的一个位置。起点是获取 RFC 索引文件 `normal rfc-index.txt`。查看 RFC 1340 的条目，其标题为“分配数字”，并注意它已被 RFC 1700 废弃。RFC 1700 在编写本文时是当前的，但在你读到它时，它可能已经废弃了。从这些废弃的 RFC 向后查找，找到“分配数字 RFC”中当前的（即编号最高的）RFC。

该 RFC 中标题为“版本号”的章节标识了不同的 IP 版本号。版本 0 是保留的，版本 1–3 是未分配的，版本 5 是互联网流协议。

2.2 如果我们以某种形式编辑 RFC（参见上一个练习的选择），并查找“Stream（流）”一词，我们发现 RFC 1819 定义了互联网流协议的第 2 版本。每当查找可能被 RFC 涵盖的信息时，都应该搜索 RFC 索引。

2.3 使用 IPv4，这会生成一个 576 字节的 IP 数据报（20 字节的 IPv4 头部和 20 字节的 TCP 头部），这是 IPv4 的最小重组接收缓冲区大小。

2.4 在此示例中，服务器充活动客户端，而不是客户端。

2.5 令牌环上的主机不能发送超过 1460 字节的数据包，因为 IPv4 的最小重组缓冲区大小是 1460。以太网上的主机可以发送高达 4096 字节的数据，但它不会超过输出接口的 MTU（最大传输单元）。TCP 不能超过对方宣告的 MSS，但它总是可以发送少于此量。

2.6 “分配数字”中的“协议数字”部分显示 OSPF 的值为 89。

### 第 3 章

3.1 在 C 语言中，函数无法按值传递参数。为了让被调用函数修改传递的值，需要传递指向该值的指针。

3.2 指针根据读取或写入的字节数增加，但 C 不允许对 `void` 指针进行增加（因为编译器不知道指向的数据类型）。

## 第 4 章

4.1 查看除 `INADDR_ANY`（全 0 位）和 `INADDR_NONE`（全 1 位）以外的常量定义。例如，D 类组播地址 `INADDR_MAX_LOCAL_GROUP` 定义为 0xe000ff 224.0.0.255，显然是主机字节序。

4.2 以下是调用 `connect` 后的新行：

```c
