
| AF_SECURITY | 15 | 安全协议。 |
| AF_KEY | 16 | 密钥环协议。 |
| AF_NETLINK | 17 | Netlink 协议。 |
| AF_ROUTE | 18 | 路由协议。 |
| AF_ECONET | 19 | 以太网协议。 |
| AF_SNA | 20 | SNA 协议。 |
| AF_IRDA | 21 | 红外线协议。 |
| AF_PPPO | 22 | PPPo 协议。 |
| AF_WANPIPE | 23 | WAN 管道协议。 |
| AF_LLC | 24 | LLC 协议。 |
| AF_BLUETO | 25 | 蓝牙协议。 |
| AF_PACKET | 26 | 数据包协议。 |
| AF_ASH | 27 | Ash 协议。 |
| AF_NETUI | 28 | NETUI 协议。 |
| AF_NETP | 29 | NETP 协议。 |
| AF_MAX | 30 | 最大地址族值。 |
| AF_SPEC | 31 | 特定的地址族。 |

第三种数据结构是本章将详细讨论的另一个结构。它被称为 `sock` 结构，定义在 `linux/include/net/sock.h` 文件中。这是一个更复杂的结构，用于保存已连接的状态信息。它主要在 TCP 协议内部通过 TCP/IP 协议访问。通常通过一个名为 `sk` 的变量引用。

```
struct sock *sk;
```

### 5.3.1 Sock 结构

在内核的早期版本中，`sock` 结构要复杂得多。然而，它已经被大大简化为一个适用于所有协议族的通用公共部分。另一个不同之处在于，在 Linux 2.6 中，`sock` 结构的实例是从特定协议的 slab 缓存分配的，而不是从通用缓存。此外，接下来的结构是 IPv4 和 IPv6 特有的部分，包含了协议族中每个成员的 `proto_info`。这部分将在第 5.11.1 节作为套接字创建的一部分讨论。

`sock` 结构的第一部分保留在一个名为 `sock_common` 的结构中。

```
struct sock_common {
```

`sk_family` 中的第一个字段包含网络地址族，例如用于 IPv4 的 `AF_INET`。`skc_state` 是连接状态，`skc_reuse` 持有 `SO_REUSEADDR` 套接字选项的值。

```
unsigned short skc_family;
volatile unsigned char skc_state;
unsigned char skc_reuse;
```

下一个字段 `skc_bound_dev_if` 持有绑定的网络接口设备的索引。

```
int skc_bound_dev_if;
```

接下来的两个字段持有协议查找表的链接。最后，`skc_refcnt` 是该套接字的引用计数。

```
struct hlist_node skc_node;
struct hlist_node skc_bind_node;
atomic_t skc_refcnt;
```

现在我们来看 `sock` 结构本身。

```
struct sock {
```

`sock` 结构中的第一个成员必须是之前描述的 `sock_common`。`sock_common` 放在第一是因为 `tcp_w_bucket` 结构以及可能的其他结构也将 `sock_common` 作为第一部分。这是为了允许在这类结构上使用相同的列表处理和队列函数。

```
struct sock_common _sk_common;
```

这里我们有一些定义，以便在通用部分查找字段。

```
#define sk_family _sk_common.skc_family
#define sk_state _sk_common.skc_state
#define sk_reuse _sk_common.skc_reuse
#define sk_bound_dev_if _sk_common.skc_bound_dev_if
#define sk_node _sk_common.skc_node
#define sk_bind_node _sk_common.skc_bind_node
#define sk_refcnt _sk_common.skc_refcnt
```

该字段未用于 TCP/IP。

该字段未用于 TCP/IP。

```
volatile unsigned char _sk_zapped;
```

下一个字段用于 `RCV_SHUTDOWN` 和 `SEND_SHUTDOWN` 套接字选项。正如我们在稍后的章节中看到的，在 TCP 中，当设置了 `SEND_SHUTDOWN` 选项时，关闭套接字将发送一个 RST 包。

```
unsigned char _sk_shutdown;
```

下一个字段如果设置，则表示该套接字有一个有效的写队列。该字段与 `write_space` 回调函数一起使用。它指示是否在 `sock_wfree` 函数中调用 `sk_write_space`。`sk_userlocks` 锁定了 `SO_SBUF` 和 `SO_RCVBUF` 套接字选项。

```
unsigned char _sk_use_write_queue;
unsigned char _sk_userlocks;
```

`sk_lock` 是用于套接字同步的单个套接字锁。下一个字段 `sk_rcvbuf` 是接收缓冲区的字节大小，通过 `SO_RCVBUF` 套接字选项设置。

```
socket_lock_t _sk_lock;
int _sk_rcvbuf;
```

`sk_sleep` 是睡眠等待队列，`sk_dst_cache` 是指向目的缓存条目的的指针。

```
wait_queue_head_t *sk_sleep;
struct dst_entry *sk_dst_cache;
rwlock_t _sk_dst_lock;
```

该字段用于安全策略数据库 (`SPD`)。更多信息请参阅第 6 章。

```
struct xfrm_policy *sk_policy[2];
```

接下来的四个字段用于队列。`sk_rmem_alloc` 是接收数据包队列中提交的字节数，`sk_receive_queue` 是接收队列。`sk_wmem_alloc` 是传输队列长度，`sk_write_queue` 是传输队列。

```
atomic_t _sk_rmem_alloc;
struct sk_buff_head sk_receive_queue;
atomic_t sk_wmem_alloc;
struct sk_buff_head sk_write_queue;
```

下一个字段是选项提交字节的大小。它被套接字过滤器使用，下一个字段 `sk_wmem_queued` 是持久性写队列的大小。

```
atomic_t sk_wmem_alloc_dup;
int sk_wmem_queued;
```

`sk_forward_alloc` 是预分配页中的字节数，`sk_allocation` 类型是分配模式。

```
int sk_forward_alloc;
unsigned int sk_allocation;
```

`sk_sndbuf` 是发送缓冲区的大小，由 `SO_SNDBUF` 套接字选项设置。

```
int sk_sndbuf;
```

`sk_flags` 包含套接字选项 `SO_BROADCAST`、`SO_KEEPALIVE` 和 `SO_OOBINLINE` 的值。接下来，`sk_no_check` 包含 `SO_NO_CHECK` 套接字选项的值，并指示是否禁用校验。`sk_debug` 持有 `SO_DEBUG` 套接字选项，`sk_rcvstamp` 持有 `SO_TIMESTAMP` 套接字选项。

```
unsigned long sk_flags;
unsigned char sk_no_check;
unsigned char sk_debug;
unsigned char sk_rcvstamp;
```

下一个字段中的值指示是否发送大型 TCP 段。`sk_route_caps` 是路由能力 `NETIF_TSO`。

```
unsigned char sk_no_largesize;
int sk_route_caps;
```

如果设置了 `SO_LINGER` 套接字选项，则 `sk_lingetime` 的值为 TRUE。`sk_hashent` 包含每个表的哈希项。`sk_pair` 是套接字对。

```
unsigned long sk_lingetime;
int sk_hashent;
struct sk_pair;
```

下一个字段 `sk_backlog` 是套接字回压队列（backlog）。它用于安全策略数据库 (`SPD`)。更多信息请参阅第 6 章。
