
```c
if (dev->reg_state == NETREG_UNINITIALIZED) {

    printk(KERN_DEBUG "unregister_netdevice: device %s/%p never "

      "was registered \n", dev->name, dev);

    return -ENODEV;

}
```

`BUG_ON(dev->reg_state != NETREG_REGISTERED);`

接下来，我们检查网络设备结构 `flags` 中的 `IFF_UP` 标志，以判断设备是否正在运行。如果设备正在运行，我们会调用网络接口通用函数 `dev_close` 处理该设备。

```c
if (dev->flags & IFF_UP) {
    dev_close(dev);
}
```

接下来，我们从设备链列表中移除 `net_device` 结构，并调用 `dev_shutdown` 关闭针对生效队列规则的设备队列。

```c
for (dp = dev->dev_base; (d = *dp) != NULL; dp = &d->next) {
    if (d == dev) {
        write_lock_bh(&dev->dev_base_lock);
        *dp = d->next;
        write_unlock_bh(&dev->dev_base_lock);
        break;
    }
}
if (!d) {
    printk(KERN_ERR "unregister_netdevice: '%s' not found\n",
      dev->name);
    return -ENODEV;
}
dev->reg_state = NETREG_UNREGISTERING;
synchronize_net();
#ifdef CONFIG_NET_FASTROUTE
dev_clear_fastroute(dev);
#endif
dev_shutdown(dev);
```

我们通过调用第 4.10 节介绍的 `notifier_call_chain` 向任何感兴趣的协议发送通知消息，告知该设备即将被销毁。

```
notifier_call_chain(&netdev_dev_chain, NETDEV_UNREGISTER, dev);
```

我们清空设备的多组播地址列表。

```
dev_mc_destroy(dev);
if (dev->uninit) {
    dev->uninit(dev);
```

这是对通知链的检查。它应该已经将我们从通知组中的主设备中分离。

```
BUG_TRAP(!dev->master);
```

```
free_divert_blk(dev);
```

在 Linux 2.6 中，设备注册是异步的。如果设备正忙，设备注册和注销可以推迟。

```
net_set_todo(dev);
```

最后，我们通过调用 `dev_put` 检查 `net_device` 结构 `refent` 字段中的引用计数。如果为 1 或更高，则说明对设备的引用仍然活跃，我们可以减少引用计数。

```c
dev_put(dev);
return 0;
}
```

为了完成网络设备注册这一节，我们将列出几个获取设备的函数。

```
struct net_device *dev_get_by_name(const char *name);
struct net_device *dev_get_by_index(int ifindex);
struct net_device *dev_get_by_dev(struct net_device *dev);
int register_netdev(struct net_device *dev);
int unregister_netdev(struct net_device *dev);
int unregister_netdev_dev(struct net_device *dev);
void dev_put(struct net_device *dev);
void dev_close(struct net_device *dev);
```

## 4.7 网络接口服务函数

如前面的章节所示，网络接口函数实现在 `linux/net/core/dev.c`。大多数函数影响网络接口的状态，例如开启、关闭或其他其他状态。状态维护在设备的标志中。

表 4.4：网络接口标志

| 标志 | 值 | 含义 |
| :--- | :--- | :--- |
| IFF_UP | 0x1 | 接口已开启。 |
| IFF_BROADCAST | 0x2 | 广播地址有效。 |
| IFF_DEBUG | 0x4 | 开启调试。 |
| IFF_LOOPBACK | 0x8 | 接口是环回。 |
| IFF_POINPOINT | 0x10 | 接口是点对链路。 |
| IFF_NOTRAILERS | 0x20 | 避免使用尾部。 |
| IFF_RUNNING | 0x40 | 接口运行且资源已分配。 |
| IFF_NOARP | 0x80 | 此接口不支持 ARP 。 |
| IFF_PROMISC | 0x100 | 接口处于混杂模式。接收所有包。 |
| IFF_ALLMULTI | 0x200 | 接口接收所有组播包。 |
| IFF_MASTER | 0x400 | 负载均衡的主设备。 |
| IFF_SLAVE | 0x800 | 负载均衡的从设备。 |
| IFF_MULTICAST | 0x1000 | 接口支持组播。 |
| IFF_VOLATILE | 0x2000 | (IFF_LOOPBACK|IFF_POINPOINT|IFF_BROADCAST|IFF_MASTER|IFF_SLAVE|IFF_RUNNING) |
| IFF_PORTSEL | 0x2000 | 可在此接口上设置媒体类型。 |
| IFF_AUTOMEDIA | 0x4000 | 自动设备已激活。 |
| IFF_DYNAMIC | 0x8000 | 接口是地址变化的拨号设备。 |

在本节中，我们讨论了驱动程序的特定函数和通用函数。在大多数情况下，我们讨论通用函数，因为许多将驱动程序连接到 TCP/IP 栈栈的工作是在通用函数中完成的。

在本节中，描述了更常见的网络接口服务函数。所有设备驱动程序必须实现在本节描述的函数。

### 4.7.1 Open 网络接口服务函数

驱动程序函数通过 `net_device` 结构体中的 `open` 字段调用。

```
int (*open) (struct net_device *dev);
```

`open` 由 `linux/net/core/dev.c` 中的通用函数 `dev_open` 回调。

```
int dev_open(struct net_device *dev);
```
