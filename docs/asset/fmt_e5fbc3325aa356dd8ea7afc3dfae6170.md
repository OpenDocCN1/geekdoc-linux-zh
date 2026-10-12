
# IPv6 套接字实现

要创建一个 IPv6 套接字，我们在 `socket` 调用中指定 IPv6 地址族 `AF_INET6`。随着 IPv6 和其他协议族的引入，Linux 以及其他操作系统的 socket API 发生了一些变化，以使套接字更加通用，不再仅仅特定于 IPv4。IPv6 的语义要求套接字编程 API 必须与协议无关。为了支持这一点，Linux 套接字的实现使得套接字地址的定义完全与协议无关。事实上通过套接字使用的 IPv4 或 IPv6 协议对于应用程序程序员来说应该是完全透明的。除了针对 2.6 版本的几次更新外，通用套接字实现本身没有发生实现上的变化，如第 5 章所示，它已经完全与协议无关。`socket` 结构被定义为同时与两种地址族工作。

正如我们在前面的章节中所回顾的，`proto_ops` 结构将传输层内部函数映射到套接字函数调用。从以下函数映射的定义可以看出，与 IPv4 相比没有太大变化。接下来是 IPv6（`AF_INET6` 地址族）`SOCK_DGRAM` 类型套接字的 `proto_ops` 结构。`proto_ops` 结构在 `linux/net/ipv6/af_inet6.c` 文件中初始化。

## inet6_dgram_ops 结构体

```c
struct proto_ops inet6_dgram_ops = {

    .family = PF_INET6,

    .owner = THIS_MODULE,
```

`release` 和 `bind` 函数是 IPv6 所特有的。

```c
.release = inet6_release,

.bind = inet6_bind,

.connect = inet6_dgram_connect,

.socketpair = sock_no_socketpair,

.accept = sock_no_accept,
```

我们回顾一下，套接字的名称是其关联的地址规范。现在需要 `getname` 函数来支持 IPv6 的新地址映射能力。

```c
.getname = inet6_getname,

.poll = datagram_poll,
```

对于 IPv6，`ioctl` 必须是不同的。

```c
.ioctl = inet6_ioctl,

.listen = sock_no_listen,
```

### 第 11 章 协议版本 6 (IPv6) 569

```c
.shutdown = inet_shutdown,

.setsockopt = inet_setsockopt,

.getsockopt = inet_getsockopt,

.sendmsg = inet_sendmsg,

.recvmsg = inet_recvmsg,

.mmap = sock_no_mmap,

.sendpage = sock_no_sendpage,

};
```

`proto_ops` 中的 `SOCK_STREAM` 套接字映射与 IPv4 也没有太大区别。在 `AF_INET6` 地址族中，不属于各个成员协议特有的函数 `inet6_stream_ops` 被定义在 `linux/net/ipv6/af_inet6.c` 文件中。

```c
struct proto_ops inet6_stream_ops = {

  family = PF_INET6,

  owner = THIS_MODULE,

  release = inet6_release,

  bind = inet6_bind,

  connect = inet6_stream_connect,

  socketpair = sock_no_socketpair,

  accept = inet6_accept,

  getname = inet6_getname,

  poll = tcp_poll,

  ioctl = inet6_ioctl,

  listen = inet_listen,

  shutdown = inet_shutdown,

  setsockopt = inet_setsockopt,

  getsockopt = inet_getsockopt,

  sendmsg = inet_sendmsg,

  recvmsg = inet_recvmsg,

  mmap = sock_no_mmap,

  sendpage = tcp_sendpage

};
```

尽管前面的映射看起来与 IPv4 相似，但当用户打开 `AF_INET6` 套接字时，`SOCK_STREAM` 数据包将由 IPv6 版本的 TCP 处理，而 `SOCK_DGRAM` 数据包将由 IPv6 版本的 UDP 处理。这是因为 IPv6 在 `AF_INET6` 层注册了它自己独特的传输协议版本。传输的数据包通过传输层的 `send message` 函数通过 IPv4 或 IPv6 发送。

## ipv6_pinfo 结构

正如我们在第 5 章中回顾的，`sock` 结构包含一个联合体（union），为每个使用套接字的协议提供了特定于协议的区域。对于 IPv6，该区域由 `linux/include/linux/ipv6.h` 文件中的 `ipv6_pinfo` 结构定义。

```c
struct ipv6_pinfo {

    struct in6_addr      saddr;

    struct in6_addr      rcv_saddr;

    struct in6_addr      daddr;

    struct in6_addr      *daddr_cache;

    u32                 flow_label;

    u32                 frag_size;

    int                  hop_limit;

    int                  mcast_hops;

    int                  mcast_oif;
```

接下来的紧凑结构用于数据包选项标志位。

（注：原文此处 union 部分代码显示异常，翻译已跳过损坏部分或按原样保留结构）

## IPv6 分片协议初始化

在 IPv4 中，重组操作是网络层（或 IP 协议）不可或缺的一部分。相比之下，在 IPv6 中，重组是在单独协议中实现的。该协议必须经过初始化并注册，以便接收输入的数据包。

### frag_protocol 结构

由于 IPv6 分片位于跟随主 IPv4 头部之后的可选头部中，我们实际上在 `AF_INET6` 地址族中注册了一个独立的协议来处理分片头部类型。该协议在某种意义上类似于传输协议，因为当在 IP 头部的下一个头部字段（next header field）中遇到协议号 `IPPROTO_FRAGMENT` 时，其处理程序会被分发。这里我们展示了如何为 `AF_INET6` 族注册分片协议的处理函数结构。

```c
static struct inet6_protocol frag_protocol =

{

    // 我们将 ipv6_frag_rcv 初始化为处理函数，并设置标志指示该包类型不需要安全检查。

    .handler = ipv6_frag_rcv,

    .flags = INET6_PROTO_NOPOLICY,

};
```

### ipv6_frag_init 函数

分片协议通过 `ipv6_frag_init` 进行初始化。

```c
void __init ipv6_frag_init(void)

{

    if (inet6_add_protocol(&protocol, IPPROTO_FRAGMENT) < 0)

        printk(KERN_ERR "ipv6_frag_init: Could not register protocol\n");

    ...

}
```

### ipv6_frag_rcv 函数

分片接收处理程序 `ipv6_frag_rcv` 位于同一个文件中，当在 IPv6 数据包的下一个头部字段中遇到 `IPPROTO_FRAGMENT` 时会被执行。

```c
static int ipv6_frag_rcv(struct sk_buff **skbp)

...
```

## 第 11 章 互联网协议版本6 (IPv6)

在检查分片头部有效性后，我们尝试在现有的分片队列中查找具有相同标识值的分片。

```c
if ((fq = fq_find(hdr->identification, &hdr->saddr, &hdr->daddr)) != NULL) {

    int ret = -1;
```
