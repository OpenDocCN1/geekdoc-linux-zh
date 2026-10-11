
## 第 24 章.网络驱动 II：数据结构

`3.1: 925`
`struct scatterlist *sgl,`

`3.1: 926`
`unsigned int scg);`

`3.1: 927 #define NETDEV_FCOE_WWNN O (*fcoe_get_wwn)(struct net_device *dev,`

`3.1: 928 #define NETDEV_FCOE_WWPN I u64 *wwn, int type);`

`3.1: 929`

`int`

`3.1: 930`

`(*ndo_rx_flow_steer)(struct net_device *dev,`

`3.1: 931 #endif #ifdef CONFIG_RFS_ACCEL`

`struct sk_buff *skb,`

`3.1: 932`

`uu16 rxq_index,`

`3.1: 933\int u32 flow_id);`

`3.1: 934`

`(*ndo_add_slave)(struct net_device *dev,`

`3.1: 935`

`struct net_device *dev,`

`3.1: 936`

`struct net_device *dev);`

`3.1: 937 #endif`

`(*ndo_fix_features)(struct net_device *dev,`

`3.1: 938\int features);`

`3.1: 939`

`(*ndo_set_features)(struct net_device *dev,`

`3.1: 940`

`u32 features);`

`3.1: 941`

`u32`

`3.1: 943`

头文件详尽地记录了这些每一个方法。最重要的是：

### 功能性方法

| 字段 | 含义 |
| :--- | :--- |
| `(*ndo_open)` | 每当激活接口时，打开接口。 |
| `(struct net_device *dev)` | 注册它。 |
| `(*ndo_stop)` | 停止接口。 |
| `(struct net_device *dev)` | 该设备。 |
| `(*ndo_start_xmit)` | 硬件传输。 |
| `(struct sk_buff *skb)` | 发送数据包。 |
| `(*ndo_set_multicast_link)` | 设置多组列表。 |
| `(struct net_device *dev)` | 修改地址。 |
| `(*ndo_set_address)` | 设置地址。 |
| `(struct net_device *dev)` | 该设备。 |
| `(*ndo_do_ioctl)` | 执行 ioctl 命令。 |
| `(struct ifqr, int cmd)` | 配置。 |
| `(*ndo_config)` | 修改配置。 |
| `(struct ifap *map)` | 该设备。 |
| `(*ndo_change_mtu)` | 修改 MTU。 |
| `(struct net_dev *dev, int new_mtu)` | 该设备。 |
| `(*ndo_neighbor_stcg)` | 邻居参数。 |
| `(struct neigh_parms *)` | 该设备。 |
| `(*ndo_do_timeout)` | 处理超时。 |
| `(struct net_dev *struct rtnl_link_stats*64 (*ndo_get_stats64))` | 获取统计数据。 |
| `(struct rtnl_link_stats64 *storage)` | 该设备。 |
| `(struct net_dev_stats* (*ndo_get_stats))(struct net_dev *)` | 获取统计数据。 |
| `(*ndo_van_add_vid)` | 添加 VLAN。 |
| `(struct net_dev *unsigned signed vid)` | 该设备。 |
| `(*ndo_van_rx_kill_vid)` | 删除 VLAN。 |
| `(struct net_dev *unsigned signed vid)` | 该设备。 |
| `(*ndo_poll_controller)` | 轮询控制器。 |
| `(struct net_dev (*ndo_netpoll_wakeup)(struct net_dev *)` | 唤醒 netpoll。 |
| `(struct netpoll_info *info)` | 该设备。 |
| `(*ndo_netpoll_cleanup)(struct net_dev *)` | 清理 netpoll。 |
| `(*ndo_get_vf_mac)(struct net_dev *)` | 获取 VF MAC。 |
| `(*ndo_set_vf_lan)` | 设置 VLAN。 |
| `(struct net_dev *int queue, u16 val, u8 qs)` | 该设备。 |
| `(*ndo_set_vf_tx_rate)` | 设置 VF 速率。 |
| `(struct net_dev *int vf, int rate)` | 该设备。 |
| `(*ndo_get_vf_config)(struct net_dev *)` | 获取 VF 配置。 |
| `(struct net_dev *int vf; struct ifla_vf_info *ivf)` | 该设备。 |
| `(*ndo_set_vf_port)(struct net_dev *)` | 设置 VF 端口。 |
| `(struct net_dev *int vf; struct nattr *port[])` | 该设备。 |
| `(*ndo_get_vf_port)(struct net_dev *)` | 获取 VF 端口。 |
| `(struct net_dev *int vf, struct sk_buff *skb)` | 该设备。 |
| `(*ndo_setup_tc)(struct net_dev *, u8 tc)` | 设置 TC。 |
| `(*ndo_fgoe_enable)(struct net_dev *)` | 启用 FGOE。 |
| `(*ndo_fgoe_disable)(struct net_dev *)` | 禁用 FGOE。 |
| `(*ndo_fdopp_setup)(struct net_dev *)` | 设置 FDOPP。 |
| `(struct net_dev *u16 did; struct scatterlist *sgl, unsigned int sgc)` | 该设备。 |
| `(*ndo_fdopp_done)(struct net_dev *)` | 完成 FDOPP。 |
| `(struct net_dev *u16 did)` | 该设备。 |
| `(*ndo_fdopp_target)(struct net_dev *)` | 目标 FDOPP。 |
| `(struct net_dev *u16 did, struct scatterlist *sgl, unsigned int scg)` | 该设备。 |
| `(*ndo_rx_flow_steer)(struct net_device *dev)` | 流引导。 |
| `(struct net_device *dev, struct sk_buff *skb, uu16 rxq_index, u32 flow_id)` | 该设备。 |
| `(*ndo_add_slave)(struct net_device *dev)` | 添加从设备。 |
| `(struct net_device *dev, struct net_device *dev)` | 该设备。 |
| `(*ndo_fix_features)(struct net_device *dev)` | 修复特性。 |
| `(struct net_dev *dev, u32 features)` | 该设备。 |

### 2.3 skbuff

+ 关于套接缓冲区的所有信息都包含在头文件 `/usr/src/include/linux/skbuff.h` 中。`skbuff` 结构是另一个复杂的结构，描述数据包：![](img/134c05ee9bbbe3f433570ac_256.png)

图 24.1: 套接字布局

+ 省略了某些元素：

## 24.4 套接缓冲区函数

+ 有许多用于套接缓冲区的函数。它们列在 `/usr/src/include/linux/skbuff.h`，并定义在 `/usr/src/linux/net/core/skbuff.c` 中。重要的有：

### 24.4. SOCKET 缓冲区函数

表 24.9: Socket 缓冲区函数

| 类型 | 函数 | 用途 |
|---|---|---|
| `struct sk_buff *` | `unsigned int length(unsigned int length);` | 分配一个新的套接缓冲区，将其引用计数置 1，并初始化数据、尾部和头部指针。 |
