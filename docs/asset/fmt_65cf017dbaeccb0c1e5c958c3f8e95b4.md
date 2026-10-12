
`msg_name` 包含套接字的名称。这是此消息的目的 IP 地址和端口号。`msg_namelen` 是 `msg_name` 指向地址的长度。`msg_iov` 是一个要发送或接收的数据缓冲区数组，通常被称为“分散聚集数组”（scatter gather array），但并非仅用于 DMA 操作。`msg_iovlen` 是 `msg_iov` 指向的数组中的缓冲区数量。辅助数据由一系列对组成，`msg_control` 用于控制信息传递给底层协议。更多信息请参阅 Linux man page(3)。`msg_flags` 包含接收消息的标志。

#### `iovec` 结构

`iovec` 结构用于前面描述的 `msghdr` 结构。它定义在 `linux/include/linux/uio.h` 文件中。`iovec` 的目的是为内核和用户空间之间的地址转换设置内存。`iov_base` 是指向缓冲区基地址的指针。在 BSD 实现中，该字段类型为 `addr_t`。缓冲区的大小。

```c
struct iovec {
    void *iov_base;
    size_t iov_len;
};
```

### `recv`、`recvfrom` 和 `recvmsg` 调用

接下来的三个套接字调用 `recv`、`recvfrom`、`recvmsg` 从对端套接字接收消息。与 `send` 调用一样，`recv` 通常用于已连接的套接字，但 `recvfrom` 可用于从任何机器获取数据报。

```c
int recv(int s, void *buf, size_t len, int flags);
int recvfrom(int s, void *buf, size_t len, int flags, struct sockaddr *from, socklen_t *fromlen);
int recvmsg(int s, struct msghdr *msg, int flags);
```

通常，这些调用会阻塞，直到有指定长度的数据可用。每个调用返回从套接字读取的数据的长度。在 `recvfrom` 返回后，`from` 和 `fromlen` 包含了发送者的地址和长度。

### `getsockopt` 和 `setsockopt` 调用

这两个套接字调用 `getsockopt` 和 `setsockopt` 是为了让调用者访问底层协议的选项。

```c
int getsockopt(int s, int level, int optname, void *optval, socklen_t *optlen);
int setsockopt(int s, int level, int optname, const void *optval, socklen_t *optlen);
```
