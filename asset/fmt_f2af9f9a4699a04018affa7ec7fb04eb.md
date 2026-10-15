
```c
static struct net_device *init_mycard(struct pci_dev *pdev, const
                                        struct pci_device_id *id)
*/
```

```c
static struct net_device *
init_mycard()
{
   struct net_device *netdev;
   struct priv_struct mycard_priv;
   /* ... */
   netdev = alloc_etherdev(sizeof(struct priv_struct));
   /* 通用方法 */
   netdev->open = &mycard_open;
   netdev->stop = &mycard_close;
   netdev->do_ioctl = &mycard_ioctl;
   /* 数据传输 */
   netdev->hard_start_xmit = &mycard_xmit_frame; /* 发送 */
   netdev->poll = &mycard_poll;                   /* 接收 - NAPI */
   netdev->weight = 64;                           /* 公平性 */
   /* 看门狗 */
   netdev->tx_timeout = &mycard_timeout;          /* 恢复函数 */
   netdev->watchdog_timeo = 8*HZ;                 /* 8 秒超时 */
   /* 统计信息和配置 */
   netdev->get_stats = &mycard_get_stats;          /* 统计支持 */
   netdev->ethtool_ops = &mycard_ethtool_ops;     /* Ethtool 支持 */
   netdev->set_mac_address = &mycard_set_mac;  /* 更改 MAC */
   netdev->change_mtu = &mycard_change_mtu;  /* 修改 MTU */
   strncpy(netdev->name, pci_name(pdev),
           sizeof(netdev->name) - 1);         /* 名称（用于 PCI） */
   /* 总线特定参数。对于 PCI NIC，如下所示 */
   netdev->mem_start = pci_resource_start(pdev, 0);
   netdev->mem_end   = netdev->mem_start + pci_resource_len(pdev, 0);
   /* 注册接口 */
   register_netdev(netdev);
   /* ... */
   /* 从连接的 EEPROM 获取 MAC 地址 */
   /* ... */
   /* 如需要则下载微代码 */
   /* ... */
}
```

### 中断处理程序

```c
static irqreturn_t
mycard_interrupt(int irq, void *dev_id)
{
  struct net_device *netdev = dev_id;
  struct sk_buff *skb;
  unsigned int length;
  /* ... */
  if (receive_interrupt) {
    /* 因数据包接收而触发中断。此时，NIC 已将接收的数据 DMA 到在设备打开时预先分配并映射的 sk_buff 中。根据你的数据结构设计获取 sk_buff 的地址并将其赋给 'skb'。类似地，'length' 是通过读取用于从卡中 DMA 数据的描述符从 NIC 获取的。现在，skb->data 包含接收的数据。 */
    /* ... */
    /* 对于 PCI 卡，对接收缓冲区执行 pci_unmap_single()，以便允许 CPU 访问该缓冲区 */
    /* ... */
    /* 通过将 skb->tail 向下移动 length 字节并相应地增加 skb->len，允许数据到达数据包尾部 */
    skb_put(skb, length);
    /* 将数据包传递给 TCP/IP 协议栈 */
    #if !defined (USE_NAPI)  /* 采用旧方式 */
        netif_rx(skb);
    #else                     /* 采用 NAPI 方式 */
        if (netif_rx_schedule_prep(netdev)) {
            /* 禁用 NIC 中断。实现未显示。 */
            disable_nic_interrupt();
            /* 将数据包提交到协议层，并将设备添加到轮询列表 */
            __netif_rx_schedule(netdev);
        }
    #endif
  } else if (tx_complete_interrupt) {
    /* 发送完成中断 */
    /* ... */
    /* 取消映射并释放发送资源，例如 DMA 描述符和缓冲区。释放 sk_buff 或将其回收至空闲池 */
    /* ... */
  }
  return IRQ_HANDLED; /* 假设的返回值，基于标准 IRQ 处理，尽管未在 OCR 片段中明确显示，逻辑暗示如此 */
}
```

### 驱动程序打开

```c
static int
mycard_open(struct net_device *netdev)
{
    /* ... */
    /* 请求 irq */
    request_irq(irq, mycard_interrupt, IRQF_SHARED,
                netdev->name, dev);
    /* 填充发送和接收环 */
    /* 参见章节“缓冲区管理和并发控制” */
    /* ... */
    /* 向卡提供空闲描述符地址 */
    /* ... */
    /* 传达你已准备好接受来自网络协议栈数据的信号 */
    netif_start_queue(netdev);
    /* ... */
    return 0;
}
```

### 驱动程序关闭

```c
static int
mycard_close(struct net_device *netdev)
{
    /* ... */
    /* 要求网络协议栈停止向下发送数据 */
    netif_stop_queue(netdev);
    /* ... */
    return 0;
}
```

### 设备移除

```c
/* 当设备被拔出或模块被释放时调用。对于 PCI 卡，这由（或本身就是）remove() 方法调用。在这种情况下，该函数声明为：
   static void __devexit mycard_remove(struct pci_dev *pdev)
*/
static void __devexit
mycard_remove()
{
    struct net_device *netdev;
    /* ... */
    /* 对于 PCI 卡，如下获取关联的 netdev，* 假设 probe() 方法在分配 netdev 后执行了相应的 * pci_set_drvdata(pdev, netdev) */
    netdev = pci_get_drvdata(pdev);
    /* ... */
    unregister_netdev(netdev); /* register_netdev() 的反向操作 */
    /* ... */
    free_netdev(netdev); /* alloc_netdev() 的反向操作 */
    /* ... */
}
```

### 挂起方法

```c
static int
mycard_suspend(struct pci_dev *pdev, pm_message_t state)
{
    /* ... */
    netif_device_detach(netdev);
    /* ... */
    return 0;
}
```

### 恢复方法

```c
static int
```
