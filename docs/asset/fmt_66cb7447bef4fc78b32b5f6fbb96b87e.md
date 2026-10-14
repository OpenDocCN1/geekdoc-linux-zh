
## Arguments

`dev`

触发通知的设备

## Description

表示设备状态已更改。此函数调用 `netdev_chain` 通知链并向路由套字发送 `NEWLINK` 消息。

## dev_load

### Name

`dev_load` — 加载网络模块

### Synopsis

```
void dev_load (const char * name);
```

## Arguments

`name`

接口名称

## Description

如果不存在网络接口且进程具有相应权限，此函数将加载模块。如果内核中不支持模块加载，则它成为一个无操作操作（nop）。

### dev_open

#### Name

`dev_open` — 准备接口使用

#### Synopsis

```
int dev_open (struct net_device * dev);
```

## Arguments

`dev`

要打开的设备

## Description

将设备从关闭状态切换到开启状态。调用设备的私有打开函数，然后加载组播列表。最后将设备移动到开启状态并向 `netdev` 通知链发送 `NETDEV_UP` 消息。

在激活接口上调用此函数为无操作。失败时返回负 `errno`。

### dev_close

#### Name

`dev_close` — 关闭接口

#### Synopsis

```
int dev_close (struct net_device * dev);
```

## Arguments

`dev`

要关闭的设备

## Description

此函数将激活设备移动到关闭状态。向 `netdev` 通知链发送 `NETDEV_GOING_DOWN`。随后停用设备，最后向通知链发送 `NETDEV_DOWN`。

## register_netdevice_notifier

### Name

`register_netdevice_notifier` — 注册网络通知器

### Synopsis

```
int register_netdevice_notifier (struct notifier_block * nb);
```

## Arguments

`nb`

通知器

## Description

注册一个网络设备事件发生时调用的通知器。传递的通知器被链接到内核结构中，在注销之前不能重用。失败时返回负 `errno` 错误码。

## unregister_netdevice_notifier

### Name

`unregister_netdevice_notifier` — 注销网络通知器

### Synopsis

```
int unregister_netdevice_notifier (struct notifier_block * nb);
```

## Arguments

`nb`

通知器

注销之前通过 `register_netdevice_notifier` 注册的通知器。该通知器从内核结构中解除链接，之后可以重用。失败时返回负 `errno` 错误码。

#### 概要

```
int dev_queue_xmit (struct sk_buff * skb);
```

#### 参数

- `skb`

  要传输的缓冲区

#### 描述

将缓冲区加入队列以发送到网络设备。调用者在调用此函数之前必须设置设备和优先级并构建缓冲区。该函数可以从中断中调用。

失败时返回负的 `errno` 码。成功并不保证帧一定会被发送，因为它可能由于拥塞或流量整形而被丢弃。

# netif_rx

#### 名称

`netif_rx` — 将缓冲区提交到网络层代码

#### 概要

```
int netif_rx (struct sk_buff * skb);
```

#### 参数

`skb`

要提交的缓冲区

#### 描述

此函数从设备驱动程序接收一个数据包，并将其放入队列以供上层（协议层）处理。该函数总是执行执行的。在处理过程中，缓冲区可能会因为拥塞控制或协议层而被丢弃。

# 返回值

`NET_RX_SUCCESS` (无拥塞)

`NET_RX_CN_LOW` (低拥塞)

`NET_RX_CN_MOD` (中度拥塞)

`NET_RX_CN_HIGH` (高拥塞)

`NET_RX_DROP` (包被丢弃)

# net_call_rx_atomic

#### 名称

`net_call_rx_atomic` —

#### 概要

```
void net_call_rx_atomic (void (*fn) (void));
```

#### 参数

`fn`

要调用的函数

#### 描述

执行一个相对于协议层是原子的函数调用。

# register_gifconf

#### 名称

`register_gifconf` — 注册一个 SIOCGIF 处理程序

#### 概要

```
int register_gifconf (unsigned int family, gifconf_func_t * gifconf);
```

#### 参数

`family`

地址族

`gifconf`

函数处理程序

#### 描述

注册与协议相关的地址转储例程。传递的处理程序在被另一个处理程序替换之前，不能被释放或重用。

# netdev_set_set_master

#### 名称

`netdev_set_master` — 设置主从设备对

#### 概要

```
int netdev_set_master (struct net_device * slave, struct net_device * master);
```

#### 参数

- `slave`

  从设备

- `master`

  新的主设备

# 描述

更改从设备的主设备。传递 `NULL` 以断开绑定（bonding）。调用者必须持有 `RTNL` 信号量。失败时返回负的 `errno` 码。成功时调整引用计数，向路由套接字发送 `RTM_NEWLINK` 信号，函数返回零。

# dev_set_promiscuity

#### 名称

`dev_set_promiscuity` — 更新设备上的混杂模式计数

#### 概要

```
void dev_set_promiscuity (struct net_device * dev, int inc);
```

#### 参数

- `dev`

  设备

- `inc`

  修改值

# 描述

从设备上添加或移除混杂模式。只要设备中的计数保持为零，接口就会保持在混杂状态。一旦计数归零，设备将恢复到正常的过滤操作。负的 `inc` 值用于取消设备上的混杂模式。

# dev_set_allmulti

#### 名称

`dev_set_allmulti` — 更新设备上的全组播计数

#### 概要

```
void dev_set_allmulti (struct net_device * dev, int inc);
```

#### 参数

- `dev`

  设备

- `inc`

  修改值

# 描述

在设备上添加或移除对所有组播帧的接收。只要设备中的计数保持为零，接口就会保持监听所有接口。一旦计数归零，设备将恢复到正常的过滤操作。负的 `inc` 值用于在释放需要所有组播的资源时递减计数器。

# dev_ioctl

#### 名称

`dev_ioctl` — 网络设备 ioctl

#### 概要

```
int dev_ioctl (unsigned int cmd, void * arg);
```

#### 参数

`cmd`

要执行的命令

`arg`

用户空间中 `structreq` 结构体的指针

# 描述

向设备下发 `ioctl` 函数。这通常由用户空间接口调用，但有时对其他用途也有用。如果值为正，则返回系统调用的返回值；若出错则返回负的 `errno`。

# dev_new_index

#### 名称

`dev_new_index` — 分配 ifindex

#### 概要

```
int dev_new_index ( void );
```

#### 参数

`void`

无参数

# 描述

为新的设备接口编号返回一个唯一的值。调用者必须持有 `rtn` 信号量或 `dev_base_lock` 以确保其唯一性。

# netdev_finish_unregister

#### 名称

`netdev_finish_unregister` — 完成取消注销

#### 概要

```
int netdev_finish_unregister (struct net_device * dev);
```

#### 参数

`dev`

设备

# 描述

销毁并释放一个死亡的设备。成功时返回零。

# unregister_netdevice

#### 名称

`unregister_netdevice` — 从内核中移除设备

#### 概要

```
int unregister_netdevice (struct net_device * dev);
```

#### 参数

`dev`

设备

# 描述

此函数关闭设备接口并将其从内核表中移除。成功时返回 0，失败时返回负的 `errno`。
