
# `net_device` 结构定义

`net_device` 结构定义在 `include/net/device.h` 中，它是定义网络接口实例的数据结构。它跟踪所有连接到 TCP/IP 栈的网络接口的状态。该结构看起来比比的更长、更复杂，但包含了在最初定义更通用网络接口之后添加的设备字段。在我们对 `net_device` 结构的描述中，对网络接口编写者最感兴趣的字段包含了解释。我们还包含了将网络接口驱动程序连接到 TCP/IP 栈所需的项的解释。通常情况下，我们只关注驱动程序数据结构的公共部分，但驱动程序数据结构私有部分中的某些关键字段对于 PCI 设备很重要。这是因为它们必须用指向 PCI 卡配置空间的指针进行初始化，而该指针在驱动程序为映射到 PCI 空间以太网分配缓冲区时随后会被解引用。然而，本节的大部分讨论都涉及 `net_device` 设备中包含的结构公共部分。

```c
struct net_device
```

第一个字段 `name` 是该结构可见部分的起始。它包含了接口名称的字符串。我们所说的*可见的*，是指该数据结构的这部分是通用的，不包含任何针对特定类型设备的私有区域。

```c
char name[IFNAMSIZ];
```

`mem_end` 是指向设备特定内存区域末尾的指针，`mem_start` 是指向该区域开头的指针。

```c
unsigned long mem_end;
unsigned long mem_start;
```

`base_addr` 是 x86 处理器和其他映射到 IRQ 的架构使用的设备 I/O 地址。它是设备的中断处理程序，也被 x86 处理器使用。

```c
unsigned long base_addr;
unsigned int irq;
```

以下两个字段均被某些硬件类型使用，但通常由 `linux/drivers/net/dev.c` 指定，该文件持有各种类设备的初始配置。

```c
unsigned char port;
unsigned char dma;
```

此字段持有网络设备状态。值是队列层私有的，不在其他任何地方使用。它们显示在表 4.1 中。

| 表 4.1: 队列层设备状态 | 状态 | 值 | 描述 |
| :--- | :--- | :--- | :--- |
| `_LINK_STATE_XOFF` | 0 | 设备队列关闭。 |
| `_LINK_STATE_START` | 1 | 设备队列开启。 |
| `_LINK_STATE_PRESENT` | 2 | 设备准备好进行调度。 |
| `_LINK_STATE_SCHED` | 3 | | |
| `_LINK_STATE_NOCRIER` | 4 | | |
| `_LINK_STATE_RX_SCHED` | 5 | 设备放入轮询列表。 |
| `_LINK_STATE_LINK_PENDING` | 6 | | |

```c
unsigned long state;
struct net_device *next;
```

`init` 是指向设备初始化函数的指针。该函数被调用一次。这是由 `linux/drivers/net/dev.c` 中的探测函数预初始化的最后一个字段。

```c
int (*init)(struct net_device *dev);
struct net_device *next_sched;
```

`ifindex` 是接口索引，`iflink` 是唯一设备标识符。

```c
int ifindex;
int iflink;
```

`net_device` 字段包含了将网络接口驱动程序连接到 TCP/IP 栈所需的项（注：原文此处描述有误，应指代后续字段）。`net_stats` 是指向网络接口统计的指针，`iflink` 是唯一设备标识符。

```c
struct net_device (*get_stats)(struct net_device);
```

现在我们来到 `net_device` 可可见部分的末尾。后续字段是内核内部的。`trans_start` 是最后发送数据包的 jiffies 时间戳，而 `last_rx` 是最后接收数据包的时间戳。

```c
unsigned long trans_start;
unsigned long last_rx;
```

下一个字段 `flags` 是 BSD 风格的接口标志。

```c
unsigned short flags;      /* 接口标志 (BSD) */
unsigned short gflags;
```

此字段 `priv_flags` 与 `flags` 类似，但它是私有的，且不会在用户级别显示。

```c
unsigned short priv_flags;
unsigned short unused_fix;
```

`mtu` 包含了接口的最大传输单元 (MTU) 值。下一个字段 `type` 是接口硬件类型。

```c
unsigned mtu;
unsigned short type;
```

`hard_header_len` 是链路层头部的大小（在 Linux 中称为硬件头）。`priv` 是指向驱动程序私有区域的指针。我们将在下一节查看如何初始化它，而 `master` 是指向该设备主设备的指针。

```c
unsigned short hard_header_len;
void *priv;
struct net_device *master;
```

下一个字段包含了接口链路层地址信息。`broadcast` 是链路层广播地址，`dev_addr` 是接口特定地址，`addr_len` 是地址的长度。

```c
unsigned char broadcast[MAX_ADDR_LEN];
unsigned char dev_addr[MAX_ADDR_LEN];
unsigned char addr_len;
```

`mc_list_` 是网络接口链路层或 MAC 组播地址列表，`mc_count` 是列表中地址的数量。如果为 true，该字段表示接口设置了混杂模式。混杂模式在前面的章节中讨论过。它允许接口看到线缆上的所有数据包。

以下两个字段用于定时器，其中一个供此接口使用。

```c
int watchdog_timeout;
struct timer_list watchdog_timer;
```

下一个字段是协议特定的指针。`atalk_ptr` 是指向 AppleTalk 特定数据的指针，`ip_ptr` 是指向 IPv4 特定数据的指针。`dn_ptr` 是 DECNet 特定数据的指针，`ec_ptr` 是 Econet 特定的指针，而 `ax25_ptr` 是针对 AX.25 协议特定的。

```c
void *atalk_ptr;
void *ip_ptr;
void *dn_ptr;
void *ip6_ptr;
void *ec_ptr;
void *ax25_ptr;
```

下一个字段 `poll_list` 是一个指向队列数据包列表的指针。该字段以及下一组字段供队列层使用，允许网络接口设备使用多个队列策略（queuing disciplines）。`quota` 用于块设备（block_dev）的输入队列，而 `weight` 也是 `block_dev` 用于输入数据包的积压权重。

```c
struct list_head      poll_list;
int                   quota;
int                   weight;
```

Qdisc 是用于该网络接口的队列策略。

```c
struct Qdisc         *qdisc;
struct Qdisc         *qdisc_sleeping;
```

`qdisc_sleeping` 指向用于该网络接口设备的注册队列策略列表，而下一个字段 `qdisc_ingress` 是用于输入数据包的队列策略。`tx_queue_len` 是该设备允许的最大输出数据包数量。

```c
struct Qdisc         *qdisc_list;
struct Qdisc         *qdisc_ingress;
unsigned long       tx_queue_len;
```

这两个字段是在用于多 CPU 应用时，用于同步驱动程序的 `hard_start_xmit` 函数的自旋锁（spinlock）。`Queue_lock` 是设备队列的互斥锁（mutex lock）。

```c
spinlock_t       xmit_lock;
int               xmit_lock_owner;
spinlock_t       queue_lock;
```

`refcnt` 包含对该设备的引用计数。

```c
atomic_t         refcnt;
```

`Todo_list` 用于延迟设备注册和注销，`reg_state` 是延迟注册和注销的状态机。

```c
struct list_head  todo_list;
enum              { NETREG_UNINITIALIZED_LIST=0,
```
