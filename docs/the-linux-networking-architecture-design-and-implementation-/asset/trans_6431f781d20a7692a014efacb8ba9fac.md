

# 第 26 章 Socket 的概念

```c
case SYS_BIND:
  err = sys_bind(a0, (struct sockaddr*)a1, a[2]);
  break;
case SYS_CONNECT:
  err = sys_connect(a0, (struct sockaddr*)a1, a[2]);
  break;
case SYS_LISTEN:
  err = sys_listen(a0,a1);
  break;
...
{
}
```

BSD socket 支持中最重要的结构是 `struct socket`。
它定义在 `include/linux/net.h`：

```c
struct socket {
  struct_state       state;
  unsigned long      flags;
  struct proto_ops    *ops;
  struct inode        *inode;
  struct fasync_struct *fasync_list; /* 异步唤醒列表 */
  struct file         *file; /* 用于垃圾回收的文件指针 */
  struct sock         *sk;
  wait_queue_head_t wait;

  short               type;
  unsigned char      passcred;
};
```

与早期的内核版本相比，该结构略有简化。
存储在 `state` 中的 socket 状态可以取以下值（见 `include/linux/net.h`）：SS_FREE（空闲）、SS_UNCONNECTED（未连接）、SS_CONNECTING（正在连接中）、SS_CONNECTED（已连接）、SS_DISCONNECTING（正在断开）。`flags` 用于同步访问。`ops` 指针在初始化后引用已连接协议的协议操作（例如 TCP 或 UDP）。就像 Linux 中的每个文件都有一个 `inode` 一样，每个 socket 也被分配了一个 `inode`。指向文件结构的指针存储在 `file` 中；它与 socket 相连，也可以用于对其进行寻址。如果任何进程正在等待该文件的事件，则可以通过 `fasync_list` 找到该进程。

通过 `sk` 指针可以使用匹配的 `sock` 结构。该结构由 BSD socket 底层的特定协议 socket（例如 `PF_INET` socket）初始化并赋值给此指针。`wait` 条目用于实现同步（阻塞）请求。`type` 字段用于存储与文件中 socket 同名的第二个参数。行政管理参数定义在 `include/asm/socket.h` 中：SOCK_STREAM、SOCK_DGRAM、SOCK_RAW、SOCK_RDMA 和 SOCK_PACKET。（后者不应使用。）

现在，让我们看看当应用程序调用 `socket()` 时，这在 Linux 内核中是如何运作的。如所述，该调用在 `net/socket.c` 的 `sys_socketcall()` 函数中通过调用 `sys_socket()` 函数传递的。

## 26.2 BSD Socket

```c
sys_socket()
net/socket.c
```

该函数通过调用 `sock_create()` 和 `sock_map_fd()` 函数来初始化 socket 结构，并分配 `inode` 和文件描述符。

```c
sock_create()
net/socket.c
```

在该函数中，第一步是检查协议族是否可用。可能会尝试加载该族模块。随后，描述了 socket 结构的 `type` 字段，并调用了两个额外的函数：`sock_alloc()`（用于提供一个 socket）和 `net_families[family]->create()`。`sock_alloc()` 函数将在稍后描述。`net_families[family]->create()` 执行底层 socket 的 `create()` 函数。

为此，相应的注册会在系统启动或通过 `sock_register()` 函数（`net/socket.c`）加载适当模块时，与向量 `struct_proto_family *net_families[NPROTO]` 处进行注册。它们还传递了协议族的名称和指向 `create()` 函数的指针。在这种情况下，示例通过调用 `sock_register(&inet_family_ops)`（`net/ipv4/af_inet.c`）完成，该调用导出了 `inet_create()` 函数。此时，控制流允许 BSD socket 区域传递给底层 socket 的实现。

```c
sock_alloc()
net/socket.c
```

此函数最初由 `sock_create()` 调用；它预留了一个新的 `inode` 并分配了一个 `socket` 结构。socket 结构的字段初始化为 `null`。

```c
sock_map_fd()
net/socket.c
```

该函数使用多个辅助函数为 socket 分配文件描述符，用于寻址该 socket。它也被称为 描述符，但与其他描述符没有区别。这就是为什么你可以使用 `read()` 和 `write()` 在 socket 上进行读写。socket 结构的文件条目在 `sock_map_fd()` 函数中设置。

底层 socket 的 `create()` 函数由 `net_families[family]->create()` 调用——现在它必须填充 socket 结构的字段——特别是指向 `proto_ops`（`include/linux/net.h`）的指针。该结构为 BSD socket 提供底层 socket 的函数。

```c
struct proto_ops {
    int    family;
    int (*release) (...);
    int (*bind) (...);
    int (*connect) (...);
    int (*socketpair) ();
    int (*accept)();
    int (*getname)();
    unsigned int (*poll)();
    int (*ioctl)();
    int (*listen)();
    int (*shutdown)();
    int (*setsockopt)();
    int (*getsockopt)();
    int (*sendmsg) (();
    int (*recvmsg)();
    ssize_t (*sendpage)();
};
```

注意，并非所有函数都必须实现：然而，在 socket 上发送数据是可以理解的：例如，当应用程序通过 `sendto()` 发送数据时，`net/socket.c` 中的 `sys_socketcall()` 执行了由传输数据、地址和控制字段组成的消息。最后，`sendmsg()` 函数使用 `socket->ops->sendmsg()` 调用相应底层协议的传输。

BSD socket 支持许多协议，因此定义了一个通用结构 `sockaddr`（`include/linux/socket.h`）。它由协议族标识符和相应的地址组成：

```c
struct sockaddr {
    sa_family_t sa_family;
    char            sa_data[14]; /* 地址 */
};
```

## 26.3 特定协议 Socket

BSD socket 底层所有特定协议 socket 的核心结构是 `struct sock`。早期内核版本中该结构面向 TCP/UDP 和 IP。随着 ATM 等其他协议的添加，sock 结构得到了扩展，其他条目从结构中部分移除。最初创建的结构具有几个协议所需的条目。随着三个结构（`net_pinfo`、`tp_pinfo` 和 `prot_info`）的引入，每个结构包含指向匹配层选项的引用，这种情况会逐渐改善，结构仍然非常广泛，但我们在后续章节中仅介绍感兴趣的条目。

### 26.3.1 PF_INET SOCKET

本节描述了应用程序使用 `socket()` 时 PF_INET socket 层次的初始化。

```c
inet_create() net/ipv4/inet.c
```

如所述，该函数由 `sock_create()` 调用以初始化 socket 结构。最初，BSD socket 的状态设置为 `SS_UNCONNECTED`，然后由第 4 章描述的 `sk_alloc()` 函数分配一个 socket 结构。此时协议族只能是 `PF_INET`，但我们仍然必须区分类型和协议。现在通过对比列表 `struct inet_protosw inetsw_array` 中的信息来实现，该列表在内核启动时由 `inet_register_protosw()`（`net/ipv4/inet.c`）创建。

接下来填充 BSD socket 结构的 `ops`。`sk` 指针将 BSD socket 连接到新的 socket 结构，后者通过 `ops` 指针连接到 BSD socket（见 `net/core/sock.c` 中的 `sock_init_data()`）。与 `proto_ops` 结构类似，`proto` 提供了底层协议的函数：

```c
struct proto {
    void (*close) (...);
    int (*connect) (...);
    int (*disconnect) (...);
    struct sock* (*accept) (...);
    int (*ioctl) (...);
    int (*init) (...);
    int (*destroy) (...);
    void (*shutdown) (...);
    int (*setsockopt) (...);
    int (*getsockopt) (...);
    int (*sendmsg) (...);
    int (*recvmsg) (...);
    int (*bind) (...);
    int (*backlog_rcv) (...);
    void (*hash) (...);
    void (*unhash) (...);
    int (*get_port) (...);
    char name[32];
    struct {
        int use;
        unsigned char _pad[SMP_CACHE_BYTES - sizeof(int)];
    } stats[NR_CPUS];
};
```

因此，`proto` 结构代表了从 socket 层到传输协议的接口。`hash()` 和 `unhash()` 函数用于在哈希表中定位或查找 socket 结构。

最后，`inet_create()` 根据 `proto` 结构中识别出的协议调用 `inet()` 函数（如果存在）。例如，在 TCP 中，这将是 `tcp_v4_init_sock()`（`net/ipv4/tcp_ipv4.c`）函数。在 `net/ipv4.c` 中存在类似的函数用于直接访问 IP (SOCK_RAW)。其他协议函数现在可以通过这些 `init()` 函数中的 socket 结构来使用。

