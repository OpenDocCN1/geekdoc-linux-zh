
`int (*sk_backlog_rcv)(struct sock *sk, struct sk_buff *skb);`

最后，最后一个字段是该 socket 实例的析构函数。当所有引用消失且引用变为零时调用它。

当 socket 实例从 slab 分配时，紧随 `sock_struct` 之后，后者包含一个 IPv6 和 IPv4 的协议信息部分。

```c
struct inet_sock {
    struct socket sk;
#if defined (CONFIG_IPV6) || defined (CONFIG_IPV6_MODULE)
    struct ipv6_pinfo *pinfo6;
#endif
}
```

IPv4 的 `inet_opt` 结构在 5.11.1 节中进行了讨论。

```c
struct inet_opt inet;
```

### 5.3.2 Socket 结构

socket 结构是持有 socket 层控制和状态信息的通用结构。它支持 BSD 类型 socket 接口。

```c
struct socket {
}
```

第一个字段包含套接字的状态以及表 5.8 显示的套接字状态值之一。套接字标志位于下一个字段，持有套接字等待缓冲区，包含 `SOCK_ASYNC_NOSPACE` 等值。

```c
socket__state      state;
unsigned long      flags;
```

`ops` 指向特定于套接字的操作。该数据结构在本章之后显示。

```c
struct proto_ops    *ops;
```

下一个字段 `fasync_list` 指向异步文件调用的唤醒列表。更多信息请参见 `fysync(2)`。`file` 指向该套接字的文件结构。我们需要在这里保留一个指针以便垃圾回收。

```c
struct fasync_struct *fasync_list;
struct file             *file;
```

`sk` 指向该套接字的 `sock` 结构。`wait` 是套接字等待队列。

```c
struct sock           *sk;
wait_queue_head_t    wait;
```

`type` 是套接字类型，通常为 `SOCK_STREAM`、`SOCK_DGRAM` 或 `SOCK_RAW`。`passed` 不用于 TCP/IP。它用于 BSD 风格的凭据传递，持有 `SO_PASSEDCRED` 套接字选项的值。

```c
short               type;
unsigned char      passedcred;
```

### 5.3.3 Proto-ops 结构

该结构包含此特定组套接字操作的族（family）。对于 IPv4，它将被设置为 `AF_INET`。

```c
struct proto_ops {
}
```

`family` 是地址族。对于 IPv4，它被设置为 `AF_INET`。`owner` 是拥有该套接字的模块。

```c
int family;
struct module*owner;
```

以下每个字段都对应一个套接字调用。它们都是指向实现特定协议操作的函数的指针。

```c
int             (*release)  (struct socket *sock);
int             (*bind)     (struct socket *sock,
struct sockaddr *myaddr,
int sockaddr_len);
int (*connect) (struct socket *sock,
struct sockaddr *vaddr,
int sockaddr_len, int flags);
int (*socketpair) (struct socket *sock1,
struct socket *sock2);
int (*accept) (struct socket *sock,
struct socket *newsock, int flags);
int (*getname) (struct socket *sock,
struct sockaddr *addr,
int *addr_len, int *peer);
unsigned int (*poll) (struct file *file, struct socket *sock,
struct poll_table_struct *wait);
int (*ioctl) (struct socket *sock, unsigned int cmd,
unsigned long *arg);
int (*listen) (struct socket *sock, int len);
int (*shutdown) (struct socket *sock, int flags);
int (*setsockopt) (struct socket *sock, int level,
int optname, char *optval,
int optlen);
int (*getsockopt) (struct socket *sock, int level,
int optname, char *user_optval,
int *user_optlen);
int (*sendmsg) (struct socket *sock,
struct iovec *ioc, struct socket
struct msghdr *m, int total_len);
int (*recvmsg) (struct socket *sock,
struct iovec *ioc, struct socket
struct msghdr *m, int total_len,
int flags);
int (*mmap) (struct file *file, struct socket *sock,
struct vm_area_struct *vma);
ssize_t (*sendpage) (struct socket *sock, struct page *page,
int offset, size_t size, int flags);
```

## 5.4 Linux 层初始化

网络基础设施可以支持多个协议栈或地址族。每个支持的协议套件可以使用已在套接字层注册的地址族。这就是通用的套接字 API 如何被用于不同协议套件中的成员协议。每个地址族都列在表 5.1 中。在本书中，我们在内核初始化期间主要关注 TCP/IP 及其地址族 `AF_INET`，连接 `AF_INET` 族与 TCP/IP 协议套件的内部钩子（hooks）是在套接字初始化期间完成的。然而，可以在套接字层动态注册新的协议族。第 6 章包含了更多关于通用 Linux 内核初始化机制的 own。但在在本节中，我们主要关注 `AF_INET` 地址族的套接字初始化。我们还涵盖了 TCP/IP 中每个成员协议是如何进行协议注册的。

套接字层像任何 Linux 内核设施一样，在内核初始化期间会在文件 `linux/net/socket.c` 中调用一个初始化函数。注意，初始化函数可以很容易找到，因为它们都被类型为 `__init`。`sock_init` 在内核协议注册之前被调用，因为套接字初始化必须在每个 TCP/IP 成员协议与套接字层注册之前完成。

```c
void __init sock_init(void)
{
    int i;
}
```

`sock_init` 执行的第一件事是初始化 `net_mem` 数组，这是套接字协议注册的基本机制。第 5.10 节详细描述了套接字层如何将每个用户调用映射到底层协议。

```c
for (i = 0; i < NPROTO; i++)
    net_familes[i] = NULL;
```

接下来，调用 `sk_init` 来初始化套接字数据结构的 slab 缓存（cache）。这个之前讨论过的数据结构包含了所有的内部套接字状态信息。接着，`sock_init` 调用 `sk_init` 来设置 slab 缓存。

```c
sk_init();
#ifdef SLAB_SKB
skb_init();
#endif
#ifdef WAN_ROUTER
wanrouter_init();
#endif
```

现在，我们描述伪文件系统，第一步是设置 inode 缓存。Linux 像其他操作系统一样使用 inode 作为基本单元。

```c
init_inodecache();
```

接下来，通过调用 `register_filesystem` 创建套接字的伪文件系统 `sock_type`。协议初始化的剩余部分在执行 `main.c` 中的 `do_initcalls` 函数时完成。`sock_init` 最后执行的工作是初始化已配置的过滤器。

```c
```
