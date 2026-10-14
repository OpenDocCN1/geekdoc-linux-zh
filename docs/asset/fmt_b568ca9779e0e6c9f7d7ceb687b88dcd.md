
对于这两个调用，`sock` 是套接字的描述符，`addr` 是指向用于返回结构的缓冲区指针。结构的大小和类型取决于套接字域。`addrlen` 参数是一个值结果参数。在调用之前，它应该初始化为 `addr` 指向的缓冲区长度；返回时，它包含了实际写入缓冲区的字节数。

`getsockname()` 函数返回套接字的地址族以及套接字绑定的地址。如果套接字是由另一个程序（例如 `inet()`）绑定的且套接字文件描述符在 `exec()` 后被保留，则这是非常有用的。如果我们想确定内核在对 Internet域套接字进行隐式绑定时分配的临时端口号，调用 `getsockname()` 也是非常有用的。内核在以下情况下执行隐式绑定：

- 在未通过 `bind()` 绑定到地址的 TCP 套接字上调用 `connect()` 或 `listen()` 后；
- 在未先绑定到地址的 UDP 套接字上执行首次 `sendto()` 后；
- 在 `bind()` 调用端口号（`sin_port`）被指定为 0 后。在这种情况下，`bind()` 指定了套接字的 IP 地址，但内核选择一个临时端口号。

`getpeermename()` 系统返回流式套接字连接上对端套接字的地址。这主要用于 TCP 连接，当服务器想要查找建立连接的客户端地址时，它非常有用。在调用 `accept(t)` 时也可以获取此类信息；但是，如果服务器是由执行 `accept(t)` 的程序（例如 `inetd`）派出的，那么它将继承套接字描述符，但 `accept(t)` 提供的地址信息将不再可用。

示例 61-3 展示了 `getsockname()` 和 `getpeermename()` 的用法。该程序使用了我们在 59-9（第 1228 页）中定义的函数，该函数执行了以下步骤：

1. 使用我们的 `inetListen()` 函数创建一个监听套接字 `listenFD`，它绑定到通配符 IP 地址和程序命令行参数中指定的端口。端口可以以数字形式或服务名称指定。`len` 参数返回该套接字域的地址结构长度。此值将传递给随后的 `malloc()` 调用中，用于分配一个缓冲区，用于从 `getsockname()` 和 `getpeermename()` 调用中返回套接字地址。
2. 使用我们的 `inetConnect()` 函数创建第二个套接字 `connFD`，用于向步骤 1 中创建的套接字发送连接请求。
3. 在监听套接字上调用 `accept()` 以创建第三个套接字 `acceptFD`，它连接到上一步创建的套接字。
4. 调用 `getsockname()` 和 `getpeermename()` 获取两个连接套接字（`connFD` 和 `acceptFD`）的本地和对端地址。在执行完每个调用后，程序使用我们的 `inetAddressStr()` 函数将套接字地址转换为可打印的形式。
5. 睡眠几秒，以便我们可以运行 `netstat` 来确认套接字地址信息（我们在 61.7 节中描述了 `netstat`）。

下面的会话日志了该程序的示例：

```
$ /..names 55555 &

getsockname(connFD): (localhost, 32835)

getsockname(acceptFD): (localhost, 55555)

getpeermename(connFD): (localhost, 55555)

getpeermename(acceptFD): (localhost, 32835)

[1] 8171

$ netstat -a | egrep 'Address' Local Address State

Proto Recv-Q Send-Q Local Address State

tcp 0 *:55555 *: LISTEN

tcp 0 localhost:32835 localhost:55555 ESTABLISHED

tcp 0 localhost:55555 localhost:32835 ESTABLISHED
```

从上述输出中，我们可以看到连接的套接字（`connFD`）绑定到了临时端口 32835。`netstat` 命令向我们展示了程序创建的所有三个套接字的信息，并允许我们确认两个连接套接字的端口信息，它们处于 `ESTABLISHED` 状态（在第 61.6.3 节描述）。

## 列表 61-3：使用 `gethostname()` 和 `getpeename()`

```c
#include <sys/socket.h>    /* 声明我们的套接字函数 */
#include <netinet/in.h>

int
main(int argc, char *argv[]) {
    int listenFd, acceptFd, connFd;
    socklen len;                               /* 套接字地址缓冲区的大小 */
    void *addr;
    char addrStr[IS_ADDR_STR_LEN];      /* 套接字地址的缓冲区 */

    if (argc != 2 || strcmp(argv[1], "--help") == 0)
        usageErr("%s\n", argv[0]);

    listenFd = listen(argv[1], 5, &len);
    if (listenFd == -1)
        errExit("listen");

    connFd = connect(listenFd, NULL, SOCK_STREAM);
    if (connFd == -1)
        errExit("connect");

    acceptFd = accept(listenFd, NULL);
    if (acceptFd == -1)
        errExit("accept");

    addr = malloc(len);
    if (addr == NULL)
        errExit("malloc");

    if (gethostname(connFd, &len) == -1)
        errExit("gethostname");

    printf("%s\n",
        inetAddressStr(addr, len));

    if (getpeermename(connFd, &len) == -1)
        errExit("getpeermename");

    printf("%s\n",
        inetAddressStr(addr, len));

    if (getpeermename(acceptFD, &len) == -1)
        errExit("getpeename");

    printf("%s\n",
        inetAddressStr(addr, len));

    sleep(30);                          /* 给时间运行 netstat */
    exit(EXIT_SUCCESS);
}
```
