
在 Linux 内核中，这两个任务由网络设备概念处理，并通常被视为一个单一单元。然而，区分这两种视图并分别讨论它们是有意义的。由于这个原因，下一节介绍了从“顶部”可见的网络设备接口，它为高层协议实例的物理传输提供统一的接口。随后，5.3 节将讨论“下半部分”：实际网络驱动的适配器特定函数。随后，第 6 章将引入一个示例，描述在连接高层的网络设备级别如何发送和接收数据包。

Linux 内核中的每个网络设备并不代表物理网络适配器。存在回环网络设备，提供逻辑网络功能。网络设备的接口也经常用于绑定协议，例如点对点协议 (PPP)。

![](img/5a25b942ec3329b8799f2b5f0de564f6_95_0.png)

图 5–1 网络设备接口的结构。

## 5.1 `net_device` 接口

字符设备和块设备之外，网络设备是 Linux 内核中第三类适配器 [RuCo01]。本节从高层协议的角度以及其数据结构和管理描述了网络设备的概念。

网络适配器与第 2.5 节介绍的字符设备和块设备显著不同。它们的主要特征之一是在设备文件系统 `/dev/` 中没有表示，这意味着无法通过简单的读写操作对其进行寻址。此外，这是可能的，因为面向网络设备的工作只能通过使用复杂的协议（例如 TCP）来实现。例如，不存在以数据包为基础的网络行为；像 `/dev/eth0` 或 `/dev/atm1` 这样的网络设备。网络设备在应用层通过 `ifconfig` 工具单独配置。最近，另一个可用工具是 `ip`，可用于对网络功能的广泛配置。

网络设备之所以如此特殊的原因之一是网络适配器的操作无法绑定到唯一的进程；相反，它们运行在内核中，并独立于用户进程 [RuCo01]。例如，硬盘请求向内核发送一个数据块：该操作由适配器触发（对于网络适配器而言），并且适配器必须显式请求内核传递数据包。

### 5.1.1 `net_device` 结构

```c
struct net_device {
    char name[IFNAMSIZ];
    unsigned long rmem_end, rmem_start, mem_end, mem_start, base_addr;
    unsigned int irq;
    unsigned char if_port, dma;
    unsigned long state;
    struct net_device *next, *next_sched;
    int ifindex, ifflink;

    unsigned long trans_start, last_rx;
    unsigned short flags, gflags, mtu, type, hard_header_len;
    void *priv;
    struct net_device *master;
    unsigned char broadcast[MAX_ADDR_LEN], pad;
    unsigned char dev_addr[MAX_ADDR_LEN], addr_len;

struct dev_mc_list {
    struct list_head *mc_list;
    int mc_count, promiscuity, allmulti;
};

int watchdog_timeout;
struct timer_list watchdog_timer;

struct {
    void *atalk_ptr, *ip_ptr, *dn_ptr, *ip6_ptr, *ec_ptr;
    struct Qdisc {
        unsigned long *qdisc, *qdisc_sleeping, *qdisc_list, *qdisc_ingress;
        unsigned int tx_queue_len;
    };

    spinlock_t xmit_lock;
    int xmit_lock_owner;
    spinlock_t queue_lock;
    atomic_t refcnt;

    int features;
    void (*init)(struct net_device *dev);
    void (*uninit)(struct net_device *dev);
    void (*destructor)(struct net_device *dev);
    int (*open)(struct net_device *dev);
    int (*stop)(struct net_device *dev);
    int (*hard_start_xmit)(struct sk_buff *skb,
        struct net_device *dev);
    int (*hard_header)(struct sk_buff *skb, struct net_device 
        *dev, unsigned short type, void *daddr, void *saddr,
        unsigned int len);
    int (*rebuild_header)(struct sk_buff *skb);
    void (*set_multicast_list)(struct net_device *dev);
    int (*set_mac_address)(struct net_device *dev, void *addaddr);
    int (*do_ioctl)(struct net_device *dev, struct ifreq *ifr,
        int cmd);
    int (*set_config)(struct net_device *dev, struct ifmap *
        *map);
    int (*hard_header_cache)(struct neighbour *neigh, struct 
        hh_cache *hh);
    void (*header_update)(struct hh_cache *hh, struct 
        net_device *dev, unsigned *haddr);
    void (*change_mtu)(struct net_device *dev, int new_mtu);
    void (*tx_timeout)(struct net_device *dev);
    int (*hard_parse)(struct sk_buff *skb, unsigned 
        char *haddr);
    int (*neigh_setup)(struct net_device *dev, struct 
        neigh_parms *);
};
struct net_device_stats *(*get_stats)(struct net_device *dev);
struct iw_statistics *(*get_wireless_stats)(struct net_device *dev);

struct module {
    struct module *owner;
    struct net_bridge_port *br_port;
};
```

`net_device` 结构构成了 Linux 内核中每个网络设备的基础。它不仅包含了关于网络适配器硬件的信息（中断、池、驱动函数等），还包含了关于高层协议的网络配置数据（IP 地址、子网掩码等）。正如本文开头提到的，`net_device` 结构代表了高层实例与底层硬件之间的通用接口。它允许从网络组件中抽象出硬件。为了高效实现这种抽象，我们使用了 `net_device` 结构。

*(注：原文中存在大量重复的段落，此处已根据要求去重，仅保留核心描述)*

数据（ack 中断），然后它可以引入适当的操作。为了实现这些目的，内核 2.4 及更高版本使用一个名为 `watchdog_timer` 的定时器。`last_rx` 包含最后一个数据包到达的时间（以 jiffies 为单位）。

`priv` 是指向网络设备私有数据或其驱动程序私有数据的指针。私有数据包含了管理网络适配器所需的变量和结构。它们并不存储在 `net_device` 结构中，但通常是特定于适配器的。

`qdisc` 指向类型为 `Qdisc` 的结构，它镜像了当前网络设备的调度策略。第 18 章将详细讨论这个问题。

`xmit_lock`、`xmit_lock_owner` 和 `queue_lock` 用于防止并行处理发送过程或访问发送队列。例如，`xmit_lock_owner` 包含了当前执行发送函数 `hard_start_xmit()` 的处理器编号。当当前没有处理器正在发送数据时，`xmit_lock_owner` 的值为 -1。

`refcnt` 指的是对该网络设备的引用计数。

### 硬件特定字段
