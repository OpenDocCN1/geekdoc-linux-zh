
```c
static const file_operations my_dev_fops = {

    .open = my_dev_open,

    .write = my_dev_write,

    .read = my_dev_read,

    .release = my_dev_close,

};

static struct miscdevice my_miscdev = {

    .minor = 0,

    .name = "mydev",

    .fops = &my_dev_fops,

};

static int __init my_dev_init(void) {

    int ret;

    ret = misc_register(&my_miscdev);

    if (ret) {

        pr_err("failed to register misc device\n");

        return ret;

    }

    return 0;

}

static void __exit my_dev_exit(void) {

    misc_unregister(&my_miscdev);

}

module_init(my_dev_init);

module_exit(my_dev_exit);

MODULE_LICENSE("GPL");

MODULE_AUTHOR("Alberto Liberal <liberal@europe.com>");

MODULE_DESCRIPTION("这是一个对多个缓冲区链表进行读写的的平台驱动")
```

# 驱动程序中的 DMA

直接内存访问 (`DMA`) 是一种允许外围组件直接与主内存传输数据而无需涉及系统处理器的硬件机制。

`CPU` 通过 `DMA` 控制器管理 `DMA` 操作。在 `DMA` 传输期间，`CPU` 可以继续执行代码。当 `DMA` 传输完成后，`DMA` 控制器将通过中断信号 `CPU`。

块内存拷贝的典型场景是网络数据包路由和视频流。在传输块较大或传输操作会消耗大量有效 `CPU` 时间的情况下，`DMA` 具有特别优势。

## 缓存一致性

在带有数据缓存的处理器上，使用 `DMA` 的一个副作用可能是缓存内容与主内存不再一致，这可能导致数据损坏问题。假设有一个配备缓存且允许设备直接访问外部内存的 `CPU`。当 `CPU` 访问主内存中的数据 `X` 时，可能该值已被处理器缓存，那么后续对 `X` 的操作将更新缓存副本，而不是外部内存版本（假设使用写回缓存）。如果在下一次设备 (`DMA`) 尝试传输 `X` 之前没有刷新缓存，设备将获得过值 `X`。同样，如果在设备 (`DMA`) 向主内存写入新值之前，没有失效缓存副本，`CPU` 将在旧值上进行操作。此外，当缓存刷新时，旧数据将写回主内存，从而覆盖 `DMA` 存储的新数据。结果是主内存中的数据是不正确的。

某些处理器包含名为嗅探（snooping）或缓存嗅探的机制；嗅探硬件会在外部 `DMA` 传输引用与缓存中数据匹配的主内存地址时通知，并刷新或失效缓存条目，以便 `DMA` 传输

## 设备驱动程序中的 Linux DMA

正确的数据和缓存条目的状态会相应更新。这些系统被称为相性架构，它们提供了硬件来处理缓存一致性问题。硬件本身会维护缓存与主内存之间的一致性，并确保所有子系统（`CPU` 和 `DMA`）对内存具有相同的视图。

对于非相性架构，设备驱动程序在启动传输或将数据缓冲区提供给总线设备之前，应该显式地刷新（flush）或失效（invalidate）数据。这会增加软件的复杂性并导致缓存与主内存之间更多的传输，但它允许应用程序将任意缓存区域作为数据缓冲区。

`Linux` 内核为 `ARM` 处理器提供了两种 `struct dma_map_ops` 结构：一种用于非相性架构（`arm_dma_ops`），它不提供额外的硬件一致性管理支持，因此需要软件处理；另一种用于相性 `ARM` 架构（`arm_coherent_dma_ops`），它提供了硬件来处理缓存一致性：

```c
struct dma_map_ops arm_dma_ops = {
    .alloc               = arm_dma_alloc,
    .free               = arm_dma_free,
    .mmap               = arm_dma_mmap,
    .get_sgtable        = arm_dma_get_sgtable,
    .map_page           = arm_dma_map_page,
    .unmap_page         = arm_dma_unmap_page,
    .map_sg             = arm_dma_sg,
    .unmap_sg           = arm_dma_unmap_sg,
    .sync_single_for_cpu = arm_dma_sync_single_for_cpu,
    .sync_single_for_device = arm_dma_sync_single_for_device,
    .sync_sg_for_cpu    = arm_dma_sync_sg_for_cpu,
    .sync_sg_for_device  = arm_dma_sync_sg_for_device,
};
EXPORT_SYMBOL(arm_dma_ops);
```

```c
struct dma_map_ops arm_coherent_dma_ops = {
    .alloc              = arm_coherent_dma_alloc,
    .free               = arm_coherent_dma_free,
    .mmap               = arm_coherent_dma_mmap,
    .get_sgtable        = arm_coherent_get_sgtable,
    .map_page           = arm_coherent_dma_map_page,
    .map_sg             = arm_dma_map_sg,
};
EXPORT_SYMBOL(arm_coherent_dma_ops);
```

## Linux DMA Engine API

`Linux DMA Engine API` 规范了用于实际 `DMA` 控制器硬件功能的接口，用于初始化/清理以及执行 `DMA` 传输。

从机 `DMA API` 的用法包含以下步骤：

- 分配 `DMA` 从机通道
- 设置从机和控制器的特定参数
- 获取事务的描述符（descriptor）
- 提交事务
- 发起待处理请求并等待回调通知

这些操作的细节如下：

- **分配 DMA 从机通道**：在从机 `DMA` 上文中，通道的分配略有不同。客户端驱动程序通常只需要某个特定 `DMA` 控制器的通道，在某些情况下需要一个从机通道。使用 `dma_request_chan()` 来请求通道。

`struct dma_chan *dma_request_chan(struct device *dev, const char *name)`

它将查找并返回与 `dev` 设备关联的 `DMA` 通道。通过此接口分配的通道由调用者独占，直到调用 `dma_release_channel()`。

- **设置从机和控制器的特定参数**：下一步总是向 `DMA` 驱动程序传递某些特定信息。从机 `DMA` 可以使用的大多数通用信息都在 `struct dma_slave_config` 中，它允许客户端为每个外设指定 `DMA` 方向、`DMA` 地址、总线位、`DMA` 突发长度。如果某些 `DMA` 控制器有更多需要发送的参数，它们应该尝试将 `struct dma_slave_config` 嵌入到其控制器特定的结构中。这为在需要时传递更多参数提供了灵活性。

`int dmaengine_slave_config(struct dma_chan *dma_chan, struct dma_slave_config *config)`

- **获取事务的描述符**：对于从机用法，`DMA-engine` 支持的从机传输模式有：

    - `slave_sg`：`DMA` 提供一组从/向外设的离散缓冲区（scatter buffers）。
    - `dma_cyclic`：从/向外设执行循环 `DMA` 操作，直到操作停止。
    - `interleaved_dma`：这对于从机和 `MM` 客户端都通用。对于外设从机：驱动程序可能已经知道 `FIFO`。通过给 `interleaved_template` 成员设置适当的值，可以表示不同类型的操作。

此 `API` 的非 `NULL` 值表示给定事务的“描述符”：
