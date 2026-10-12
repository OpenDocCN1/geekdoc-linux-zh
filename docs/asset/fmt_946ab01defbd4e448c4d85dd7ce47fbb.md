
# `skb_dequeue` 函数

`skb_dequeue` 从 `list` 指向的列表开头移除 `skb_buff`。它返回指向被移除套接字缓冲区的指针。

```c
struct sk_buff *skb_dequeue(struct sk_buff_head *list);
```

# `skb_dequeue_tail` 函数

`skb_dequeue_tail` 从列表结尾移除套接字缓冲区并返回被移除项的指针。

```c
struct sk_buff *skb_dequeue_tail(struct sk_buff_head *list);
```

# `skb_append` 函数

`skb_append` 在套接缓冲区列表的任意位置插入套接字缓冲区 `newsk`。将新的套接字缓冲区放在 `old` 指向的缓冲区之后。

```c
void skb_append(struct sk_buff *old, struct sk_buff *newsk);
```

# 第 6 章 套接缓冲区与 Linux 内存分配

### `skb_insert` 函数

与之前的函数一样，`skb_insert` 同样在 `sk_buff` 列表上插入套接缓冲区。然而，它将新的 `sk_buff` 放置在 `old` 指向的套接缓冲区之前。

```c
void skb_insert(struct sk_buff *old, struct sk_buff *newsk);
```

### `skb_queue_empty` 函数

该函数 `skb_queue_empty` 用于检查套接缓冲区列表是否为空。它通过检查 `sk_buff` 中的 `next` 字段是否指向自身来实现这一目的。如果列表为空，它返回 `TRUE`；否则，返回 `FALSE`。

```c
int skb_queue_empty(const struct sk_buff_head *list);
```

### `skb_queue_len` 函数

该函数 `skb_queue_len` 通过检查 `sk_buff_head` 结构体中的 `qlen` 字段，返回套接缓冲区列表的长度。

```c
__u32 skb_queue_len(const struct sk_buff_head *list);
```

### `skb_queue_purge` 函数

该组中的下一个函数 `skb_queue_purge` 会移除列表上所有的套接缓冲区。列表上的每个套接缓冲区都会通过调用 `kfree_skb` 被丢弃。

```c
void skb_queue_purge(struct sk_buff_head *list);
```

### `skb_peek_tail` 函数

该函数 `skb_peek_tail` 返回列表中最后一个 `skb` 的指针。

```c
struct sk_buff *skb_peek_tail(struct sk_buff_head *list);
```

### `skb_queue_head_init` 函数

最后，该组中的最后一个函数 `skb_queue_head_init` 初始化一个队列。它设置了队列头，以及 `list` 指向的 `sk_buff_head` 结构体中的 `next` 和 `prev` 指针。

```c
static inline void skb_queue_head_init(struct sk_buff_head *list);
```

## 一些实际考虑的考量

Slab 缓存分配统计数据存储在 `/proc` 文件系统中。可以通过执行命令 `cat /proc/slabinfo` 来查看。更多信息请参阅手册页 `slabinfo(5)`。

## 总结

在本章中，我们涵盖了 Linux 网络内存分配和 Linux 套接缓冲区结构。套接缓冲区是 Linux 网络内存分配最基础的部分，为了完整理解 Linux TCP/IP 协议族，应该对它们进行深入研究。我们首先讨论了用于在网络协议栈中分配数据包的各种内存分配方案。我们将 Linux 的 slab 分配方法与其他分配方案进行了对比，并比较了 slab 分配在效率和避免内存碎片化方面的优势。此外，我们还讨论了 Linux 套接缓冲区 `sk_buffs`，这是 Linux 用于存储网络数据包的主要结构体。我们讨论了套接缓冲区的克隆和复制，并列出了在不拷贝数据的情况下操作套接缓冲区头部和尾部空间的函数。此外，我们还涵盖了套接缓冲区的类型以及它们如何被组成列表和队列。

# 通过 UDP 和 TCP 从套接字发送数据

- 本章内容
- 几语
- 引言
- 套接字层胶水 (Socket Layer Glue)
- 传输层套接字初始化
- 在传输层发起连接
- 通过 UDP 从套接字发送数据
- 通过 TCP 从套接字发送数据
- TCP 输出
- 一些关键 TCP 数据结构
- TCP 定计时器

## 几语

我们从网络基础知识和 TCP/IP 协议族的基础开始这段旅程。本书的大部分内容关注 Linux 的内部结构。中间章节涵盖了网络接口驱动程序、Linux 套接字、Linux 基础设施和套接缓冲区。本章继续对 Linux TCP/IP 内部原理的讨论，包括传输层协议（UDP 和 TCP）的实现。通常，理解复杂协议系统的最佳方法是跟踪数据在系统中的流动。记住，理解 TCP 的良好方法是跟随数据流过系统的方式。在本章中，我们将关注 Linux TCP/IP 的内部原理，包括传输层协议 UDP 和 TCP 的实现。理解复杂协议系统的最佳方法通常是跟随数据流过系统的方式。当数据通过传输层传输到网络层时，我们将关注 TCP/IP 协议在传输层发生了什么。当应用程序向传输层写入数据时，我们将观察缓冲区如何流向套接字。

## 引言

在本章中，我们将观察 UDP 或 TCP 缓冲区在传输层发生的情况。当应用程序向传输层写入数据时，我们将观察缓冲区如何流向套接字。在本章中，我们将查看 `socket` 类型在传输层发生了什么。对于 `DGRAM` 类型，这种过程相对简单，但对于 `STREAM` 类型要复杂得多。我们将查看 `socket` 函数在传输层是如何调用的。接下来，我们将关注 `sendmsg` 函数以及数据如何通过传输层流向套接字。

# 套接字层胶水 (Socket Layer Glue)

在我们开始查看传输层每个协议的内部之前，应该查看传输层函数如何与套接字层关联。正如第 4 章“Linux 套接字”中所解释的，每个传输层协议注册到套接字层。

## `proto` 结构

注册过程的关键是 `proto` 数据结构体，它定义在 `/linux/include/sock.h` 中。在本章中我们不会讨论具体的注册机制，但将关注传输协议如何利用该结构体中的字段。这些字段大部分是函数指针，指向特定的传输协议函数。传输协议并不需要实现所有函数。例如，UDP 没有在连接终止后清理的 `shutdown` 函数，因此对 UDP 无关。然而，UDP 和 TCP 都实现了 `proto` 结构中的大部分函数。

```c
struct proto {
```

# 第 7 章 通过 UDP 和 TCP 从套接字发送数据

该结构的前七个函数（从 `close` 到 `shutdown`）将在本章后续章节中对 UDP 和 TCP 进行描述。

```c
void                (*close)(struct sock *sk, long timeout);
int                 (*connect)(struct sock *sk, struct sockaddr *uaddr, int addr_len);
int                 (*disconnect)(struct sock *sk, int flags);
struct sock *       (*accept)(struct sock *sk, int flags, int *err);
int                 (*ioctl)(struct sock *sk, int cmd, long arg);
int                 (*init)(struct sock *sk);
int                 (*destroy)(struct sock *sk);
void                (*shutdown)(struct sock *sk, int how);
```

`getsockopt` 和 `setsockopt` 函数用于 UDP 和 TCP（以及 `AF_INET` 家族中的其他协议）设置选项。UDP 和 TCP 的选项将在本章稍后详细介绍。

```c
int                 (*setsockopt)(struct sock *sk, int level, int optname, char *optval,
```
