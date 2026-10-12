
```c
struct nada_cb *nada_cb = (struct nada_cb*)&sk->cb;

struct sockaddr_nada *nad = (struct sockaddr_nada*)&sk->nad;

int ret;
```

我们将套地址结构初始化为零，并设置来自数据包的信息。

### 第 10 章 协议族实现 543

```c
memset(nad, 0, sizeof(struct sockaddr_nada));

ad->family = AF_ADA;

ad->port = port;

ad->net = net;

ad->station = station;
```

最后，我们调用通用接收函数 `sock_rcv_skb` 将数据包放入队列。

```c
ret = sock_rcv_skb(sk, skb);

return ret;
```

## 控制块结构

控制块 `nada_cb` 包含在套缓冲区。关于套缓冲区的更多信息请参见第 6 章。对于 TCP 等复杂协议，控制块包含状态。在我们的简单族中，它包含协议信息。

```c
struct nada_cb
{
    struct sockaddr_nada nad;
};
```

## 从套字发送数据包

数据包传输在用户调用 `write(2)`、`sendmsg(2)` 或类似函数时启动。我们知道，当这些函数被调用时，套字层调用相关的 `proto_ops` 结构。

## `nada_sendmsg` 函数

该函数在套字调用 `proto_ops` 结构的 `sendmsg` 字段时执行。由于我们的协议非常简单，我们在此函数中完成所有处理，并将数据包通过网络接口驱动程序传输。正如我们在第 5 章所知，大多数协议并不直接将数据包发送到设备。相反，根据数据包是直接发送给对方还是路由器，遵循更复杂的路径。此外，数据包会被排入包含多个队列的设备无关层，由网络接口驱动程序调度。

### 第 10 章 嵌入式系统 Linux TCP/IP 网络 544

```c
static int(struct kiocb *iocb, struct socket *sock,
struct msghdr *msg, size_t len)
{
```

首先，我们设置通用 `sock` 结构的指针和 `AF_NADA` 特有的套字结构。还将套字的名称转换为 `sockaddr` 结构。该名称对应用户级 `sendto(2)` 系统调用字段。

```c
struct sock *sk = sock->sk;
struct nada_sock *nsk = nada_sk(sk);
struct sockaddr_nada *naddr = (struct sockaddr_nada*)msg->nmsg_name;
```

```c
#if 0
unsigned char eth_addr[ETH_HLEN];
#endif
```

我们需要一个本地地址结构来构建传出数据包的地址。

```c
struct nada_address nad;
struct sk_buff *skb = NULL;
struct net_device *dev;
int ret = 0;
```

这些变量用于构建传出数据包头部：`proto`、`port`、`station` 和 `net` 根据名称或本地地址计算得出。变量 `proto` 设置我们的协议号。

```c
unsigned short proto = htons(ETH_P_NADA);
struct nada_hdr *nhdr;
unsigned char port;
unsigned char station;
unsigned char net;
```

首先，我们检查消息标志。这些标志位于 `sendmsg(2)` 系统调用的参数中。目前我们不支持任何标志。

```c
ret = -EINVAL;

if (msg->msg_flags)
    goto out;
```

### 第 10 章 一种协议族的实现 545

接下来，我们检查用户在名称中指定的目的地址的有效性。如果没有目的地址，我们将根据绑定到此套接字的本地地址构建一个。由于我们的大部分数据包流是点对点的，这种方法运行良好。在我们简单的协议以太网中，我们不支持回环地址。

```c
if (naddr == NULL) {
    naddr.station = naddr->nads_addr.station;
    naddr.net = naddr->nads_addr.net;
    port = naddr->nad_port;
} else {
    nad.station = nsk->station;
    nad.net = nsk->net;
    port = nsk->port;
}
```

现在，我们必须选择一个输出网络接口来发送数据包。我们调用 `nada_dev_list` 根据用户指定的或在此函数稍早计算出的网络地址来查找设备。

```c
dev = nada_dev_list[nad.net];
```

在这里，我们使用了借自 Econet 代码中的方法。如果没有输出设备，如果有默认设备，则使用默认设备。默认设备位于 `nada_dev_list` 的位置零，它是一个输出网络设备结构数组。这类似于 IP 路由中的默认路由器，默认网络接口始终指向与默认网关有可达链路的网络。

```c
if (dev == NULL) {
    dev = nada_dev_list[0];
    ret = -ENETOWN;
    if (dev == NULL) {
        goto out;
    }
}
```

在这个协议族中，我们不支持分片。当数据包大小超过设备的 MTU 时，分片是由 IP 完成的。在我们的协议中，如果大小超过 MTU，我们直接拒绝该请求。在计算 MTU 时，我们包含了 nada 协议头部的长度。此外，我们持有该设备，这意味着在调用传输函数之前都会对其进行锁定。

### 第 10 章 嵌入式系统的 Linux TCP/IP 网络编程 546

```c
ret = -MSGSIZE;
if (len + sizeof(struct nada_hdr) > dev->mtu)
    goto out;
dev_hold(dev);
```

在这里，我们为输出数据包分配套接字缓冲区 `skb`。我们在套接字缓冲区中为 nada 头部留出足够的空间。

```c
skb = sock_alloc_send_skb(sk, sizeof(struct nada_hdr),
msg->msg_flags & MSG_DONTWAIT, &ret);

if (skb == NULL)
    goto out_dev;
```

我们根据之前计算的地址设置目的地址和端口。

```c
port = naddr->nad_port;
station = naddr->nads_addr_station;
net = naddr->nads_addr_net;
```

我们现在决定将数据包发送到哪里。与具有 ARP（至少对于以太网）的 IPv4 以及使用邻居发现（ND）的 IPv6 不同，我们做的要简单得多。在我们的测试网络中，我们使用 `tun` 驱动程序，它支持 `tap` 或 `tun`，其中 `tap` 包含伪造的太网头部，而 `tun` 不包含头部。在这里，如果需要，我们会构建一个伪造的太网头部。

```c
#if 1
if (dev->hard_header) {
```

我们可以调用 `get_eth_address` 生成一个任意的伪造以太网头部，并在地址的最后字节中任意插入目的和站点号。然而，如果我们使用的是真实的以太网设备，底层将使用 ARP 协议来确定目的。在我们的情况下，我们主要是在测试使用隧道点对点设备的小型协议族。本质上，我们可以将网络层推迟到链路层地址映射问题。

```c
//get_eth_address(eth_addr, &naddr->nads_addr);
```
