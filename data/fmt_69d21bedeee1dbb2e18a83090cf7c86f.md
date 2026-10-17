
`Register_netdev` 已调用。

```
NETREG_REGISTERING,
```

注册完成。

```
NETREG_REGISTERED,
```

注销开始。

```
NETREG_UNREGISTERING,
```

注销完成。

```
NETREG_UNREGISTERED,
```

调用 `free_netdev` 函数来释放 `net_device` 结构。

```
NETREG_RELEASED,
reg_state;
```

后续字段包含网络接口设备的特征。特征列于表 4.2。

**表 4.2：`Net_device` 结构中 `Features` 字段的位定义**

| 名称 | 值 | 目的 |
|---|---|---|
| `NETIF_F_SG` | 0x1 | 如果设备支持离散/聚集（scatter/gather）IO，则意味着设备可以通过单次调用 `hard_start_xmit()` 传输多个缓冲区。 |
| `NETIF_F_IP_CSUM` | 0x2 | 如果设备硬件仅能对 IPv4 上的 TCP/UDP 进行校验和，则设置此位。 |
| `NETIF_F_NO_CSUM` | 0x4 | 如果设备不需要校验和（例如环回设备），则设置此位。 |
| `NETIF_F_HW_CSUM` | 0x8 | 如果设备可以对所有数据包进行校验和，则设置此位。 |
| `NETIF_F_HIGDMA` | 0x20 | 如果设备可以 DMA 到内存，则设置此位。 |
| `NETIF_F_FRAGLIST` | 0x40 | 另一个离散/聚集 IO 标志。它表示该设备可能进行 IP 分片。 |
| `NETIF_F_HW_VLAN_TX` | 0x80 | 此设备支持 VLAN 硬件加速。 |
| `NETIF_F_HW_VLAN_RX` | 0x100 | 设备接收 VLAN 硬件加速。 |
| `NETIF_F_HW_VLAN_FILTER` | 0x200 | 设备接收 VLAN 接收过滤。 |
| `NETIF_F_VLAN_CHALLENGED` | 0x400 | 表示设备无法处理 VLAN 数据包。 |
| `NETIF_F_TSO` | 0x800 | 设备可以卸载 TCP/IP 分段。 |

该函数单元在设备从网络断开后调用，并在最后一个用户引用被移除后调用析构函数（destructor）。

```
void (*unit) (struct net_device *dev);
void (*destructor) (struct net_device *dev);
```

`net_device` 结构中的后续是指向网络接口设备服务例程的指针。这些函数在第 4.7 节中进行了详细讨论。

```
int                 (*open) (struct net_device *dev);
int                 (*stop) (struct net_device *dev);
int                 (*hard_start_xmit) (struct sk_buff *skb,
                               struct net_device *dev);
#define HAVE_NETDEV_POLL
int                 (*poll) (struct net_device *dev, int *quota);
int (*hard_header)(struct sk_buff *skb,
                               struct net_device *dev,
                               unsigned short type,
                               void *daddr,
                               void *saddr,
                               unsigned len);
int                 (*rebuild_header) (struct sk_buff *skb);
#define HAVE_MULTICAST
void                (*set_multicast_list) (struct net_device *dev);
#define HAVE_SET_MAC_ADDR
int                 (*set_mac_address) (struct net_device *dev,
                               void *addaddr);
#define HAVE_PRIVATE_IOCTL
int                 (*do_ioctl) (struct net_device *dev,
                               struct ifreq *ifr);
#define HAVE_SET_CONFIG
int                 (*set_config) (struct net_device *dev,
                               struct ifreq *ifr);
#define HAVE_HEADER_CACHE
int                 (*header_update) (struct net_device *dev,
                               struct ifreq *ifr);
#define HAVE_CHANGE_MTU
int                 (*change_mtu) (struct net_device *dev,
                               struct ifreq *ifr);
#define HAVE_TIMEOUT
void                (*timeout) (struct net_device *dev);
void                 (*register) (struct net_device *dev,
                               struct ifreq *ifr);
```

## 4.4 网络设备初始化

网络设备初始化是在 Linux 内核通过调用探测函数来查找特定类型的设备时开始的，寻找硬件与其驱动程序的匹配。一旦发现匹配，就会调用驱动特定的初始化函数。该函数通常类型为 `__devinit` 或 `__init`，两者都定义在 `linux/include/init.h` 文件中。当接口驱动程序的初始化或探测函数被调用时，它执行的操作是分配设备私有数据结构，该结构还包含了通用的 `net_device` 结构。接下来，它设置了结构中的几个关键字段，第一个是 `name` 字段，它之后用于设置一个字符串。例如，在以太网设备中，名称字段以 "eth" 开始。当设备注册时，格式字符串将被替换为 0 到 99 之间的数字。这两个初始化步骤可以通过至少三种方式进行。

![](img/296413c166cb1a4dbce2e3ed88300315_63_0.png)

图 4.1: 网络驱动程序注册序列。

Linux 为网络接口驱动程序的编写者提供了一些通用的设备分配和初始化函数。这些函数大部分位于 `linux/net/net_init.c` 中，但以以太网设备的函数除外。例如，我们将查看图 4.1 所示的以太网网络接口设备的初始化序列。该序列对以太网设备使用了一种分配方法。函数 `alloc_ethdev` 定义在 `drivers/net/net_init.c` 中，并在 `linux/include/linux/etherdevice.h` 中声明，它同时执行了 `alloc_netdev` 并将指向设置函数的指针作为第二个参数传递。该函数在早期的内核版本中被称为 `ether_setup`。此时，函数 `netdev_boot_setup` 实际上将任何启动时的设置保存在 `netdev_boot_setup` 结构体的实例中。稍后，通过调用 `netdev_boot_setup_check` 将这些设置放入 `net-device` 结构中。
