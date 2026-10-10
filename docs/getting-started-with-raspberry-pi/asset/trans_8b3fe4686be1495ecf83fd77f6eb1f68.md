

发送例程 `my_device_xmit()` 负责启动反向的 DMA。它将发送包 DMA 到卡内存中。为此，`my_device_xmit()` 选择一个未被卡使用（或设置了 `FREE_FLAG`）的 TX DMA 描述符，并使用关联的发送缓冲区进行数据传输。`FREE_FLAG` 随后被清除，表明该描述符现在属于卡。当卡在完成发送后发出中断时，中断处理程序会释放该描述符（再次设置 `FREE_FLAG`）（这在列表 10.6 中未展示）。

此示例驱动使用了一种简化的缓冲区管理方案，该方案对性能不敏感。高速网络驱动实现了一个更复杂的方案，采用一致性和流式 DMA 映射的组合。它们维护发送和接收描述符的链表，并实现用于缓冲区管理的空闲池和使用中池。它们的接收和发送数据结构如下所示：

```c
/* 接收缓冲区环 */
struct rx_list {
    void *dma_buffer_rx;      /* 发送描述符的内核虚拟地址 */
    dma_addr_t dma_bus_rx;    /* 发送描述符的总线地址 */
    unsigned int size;        /* 缓冲区大小 */
    struct list_head next_desc; /* 指向下一个元素的指针 */
    struct sk_buff *skb;      /* 网络数据包 */
    dma_addr_t sk_bus;        /* 网络数据包的总线地址 */
} *rxlist;

/* 发送缓冲区环 */
struct tx_list {
    void *dma_buffer_tx;      /* 接收描述符的内核虚拟地址 */
    dma_addr_t dma_bus_tx;    /* 发送描述符的总线地址 */
    unsigned int size;        /* 缓冲区大小 */
    struct list_head next_desc; /* 指向下一个元素的指针 */
    struct sk_buff *skb;      /* 网络数据包 */
    dma_addr_t sk_bus;        /* 网络数据包的总线地址 */
} *txlist;
```

接收和发送 DMA 描述符（`rxlist->dma_buffer_rx` 和 `txlist->dma_buffer_tx`）按照列表 10.5 中所示以一致性方式映射。然而，有效载荷缓冲区（`rxlist->skb->data` 和 `txlist->skb->data`）是使用流式 DMA 映射的。接收缓冲区在设备打开时预分配并流式映射到空闲池中，而发送缓冲区则是即时映射的。这避免了由 `mydevice_interrupt()` 执行的一致映射接收 DMA 缓冲区到网络缓冲区的额外数据拷贝（以及由 `mydevice_xmit()` 执行的反方向额外拷贝）。

```c
/* 预分配/补充接收缓冲区。另请参阅第 15 章中的“缓冲区管理和并发控制”部分 */
/* ... */
struct sk_buff *skb = dev_alloc_skb();
skb_reserve(skb, NET_IP_ALIGN);
/* 使用流式 DMA 映射 */
rxlist->sk_bus = pci_map_single(pdev, rxlist->skb->data,
                                 rxlist->skb->len, PCI_DMA_TODEVICE);

/* 分配一个 DMA 描述符并用上述映射的地址填充它。
   将该描述符添加到接收描述符环 */
/* ... */
```

## 调试

在内核配置菜单中启用 *Bus Options* → *PCI Support* → *PCI Debugging*，以要求 PCI 核心发出调试消息。查看 `/proc/bus/pci/devices` 和 `/sys/devices/pcix:Y/` 以获取有关系统上 PCI 设备的信息，例如本章讨论的 CardBus 以太网调制解调器卡。`/proc/interrupts` 列出了系统上活跃的中断请求（IRQ），包括由 PCI 层使用的那些。

如前所述，`lspci` 获取了有关系统上所有 PCI 总线和设备的信息。您也可以使用它来转储 PCI 卡的配置空间。

PCI 总线分析仪有助于调试底层问题并调整性能。

## 查看源代码

PCI 核心和总线访问例程位于 `drivers/pci/` 中。要获取 PCI 子系统提供的辅助例程列表，请在此目录内搜索 `EXPORT_SYMBOL`。有关 PCI 层相关的定义和原型，请查看 `include/linux/pci*.h`。

您可以在 `drivers/net/`、`drivers/scsi/` 和 `drivers/video/` 下的子目录中发现多个 PCI 设备驱动。要定位所有 PCI 驱动，请在 `drivers/` 目录树中递归地 grep `pci_register_driver()`。

如果您没有找到开发自定义 PCI 网络驱动的良好起点，请从骨架 PCI 网络驱动 `drivers/net/pci-skeleton.c` 开始。有关 PCI 编程的简要教程，请查看 `Documentation/pci.txt`。有关 PCI DMA API 的描述，请阅读 `Documentation/DMA-mapping.txt`。

表 10.4 总结了本章使用的主要数据结构。

| 数据结构 | 位置 | 描述 |
| :--- | :--- | :--- |
| **pci_dev** | `include/linux/pci.h` | PCI 设备的表示 |
| **pci_driver** | `include/linux/pci.h` | PCI 驱动的表示 |
| **pci_device_id** | `include/linux/mod_devicetable.h` | PCI 卡的身份标识 |
| **dma_addr_t** | `include/asm-your-arch/types.h` | DMA 缓冲区的总线地址 |
| **scatterlist** | `include/asm-your-arch/scatterlist.h` | DMA 缓冲区的分散-聚集列表 |
| **sk_buff** | `include/linux/skbuff.h` | 主要网络数据结构（更多说明见第 15 章） |

表 10.5 列出了本章使用的主要内核编程接口及其定义位置。

| 内核接口 | 位置 | 描述 |
| :--- | :--- | :--- |
| **pci_read_config_byte()** | `include/linux/pci.h` | 操作 PCI 配置空间的例程。 |
| **pci_read_config_word()** | `drivers/pci/access.c` | |
| **pci_read_config_dword()** | | |
| **pci_write_config_byte()** | | |
| **pci_write_config_word()** | | |
| **pci_write_config_dword()** | | |
| **pci_resource_start()** | `include/linux/pci.h` | 这些例程操作 PCI I/O 和内存区域以获取基地址、长度、结束地址和控制标志。 |
| **pci_resource_len()** | | |
| **pci_resource_end()** | | |
| **pci_resource_flags()** | | |
| **pci_request_region()** | `drivers/pci/pci.c` | 保留 PCI I/O 或内存区域。 |
| **pci_disable_device()** | `drivers/pci/pci.c` | `pci_enable_device()` 的反向操作。 |
| **pci_set_master()** | `drivers/pci/pci.c` | 将设备设置为 DMA 总线主控模式。 |

# 第 11 章. 通用串行总线

## 本章内容

- **USB 架构** 312
- **Linux-USB 子系统** 317
- **驱动数据结构** 317
- **枚举** 324
- **设备示例：遥测卡** 324
- **类驱动** 338
- **设备驱动（Gadget Drivers）** 348
- **调试** 349
- **查看源代码** 351

> *通用串行总线*（USB）是当今计算机中事实上的外部总线。凭借其支持热插拔、通用类驱动和灵活的数据传输模式，USB 是消费电子领域将多种技术引入计算机系统的常见途径。其广泛的流行度及其带来的规模化经济效应，在推动全球计算机外围技术的采用和接受方面发挥了作用。

### USB 架构

USB 是一种主从协议，其中主控制器与客户设备进行通信。图 11.1 显示了 PC 环境中的 USB。USB 主控制器是南桥芯片组的一部分，并通过 PCI 总线与处理器通信。

![](img/07cc6f9c8c74622020874f66bfb53dc4_291_0.png)

图 11.2 说明了嵌入式设备上的 USB。图中的 SoC 内置支持四个总线和三种操作模式的 USB 控制器硅片：

- 总线 1 运行在主模式，并通过 USB 收发器连接到 A 型接口（参见侧边栏“USB 接口和收发器”）。您可以将此端口连接 USB 闪存驱动器或键盘。
- 总线 2 也运行在主模式，但相关的收发器连接到内部 USB 设备，而不是接口。内部 USB 设备的例子包括生物特征扫描仪、加密引擎、打印机、*芯片盘*（DOCs）、触摸控制器和遥测卡。
- 总线 3 运行在设备模式，并通过收发器连接到 B 型接口。B 型接口通过 B 到 A 的电缆连接到主计算机。在此模式下，嵌入式设备作为例如 USB 闪存驱动器，将存储分区导出到外部世界。与 PC 系统相比，MP3 播放器和手机等嵌入式设备更有可能处于 USB 的设备端，因此许多嵌入式 SoC 除了主控制器外还支持 USB 设备控制器。
- 总线 4 由 *On-The-Go*（OTG）控制器驱动。例如，您可以使用此端口将闪存驱动器连接到您的系统，或将您的系统变成闪存驱动器并连接到主机。与总线 1

