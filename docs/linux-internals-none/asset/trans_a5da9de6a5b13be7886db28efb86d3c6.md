
## DMA 映射的类型

DMA 映射有两种类型，*一致性*（consistent）和*流式*（streaming）。

一致性 DMA 映射通常在驱动程序初始化时进行映射，并在驱动程序初始化结束时解除映射。硬件应保证设备和 CPU 可以并行访问数据，并且无需显式软件刷新即可看到彼此所做的更新。

一致性映射的良好应用包括：

- 网络卡 DMA 环形描述符。
- SCSI 适配器的邮箱命令数据结构。
- 从主内存执行的设备固件微代码。

这些示例共同要求的不变条件是，任何 CPU 到内存的存储操作都能立即被设备看到，反之亦然。一致性映射保证了这一点。

流式 DMA 映射通常是为一次 DMA 传输进行映射，并在传输完成后立即解除映射（除非你使用下面的 `pci_dma_sync`）。硬件可以为顺序访问优化流式映射。

流式映射的良好应用包括：

- 设备发送或接收的网络缓冲区。
- SCSI 设备写入或读取的文件系统缓冲区。

流式映射的接口是这样设计的，使得实现者可以根据硬件允许的性能优化进行优化。为此，在使用此类映射时，你必须明确说明你希望发生什么。

## 使用一致性 DMA 映射

要分配并映射一个一致性 DMA 区域，你应该输入：

```c
dma_addr_t dma_handle;
cpu_addr = pci_alloc_consistent(dev, size, &dma_handle);
```

其中 *dev* 是一个 *struct pci_dev*。对于设备没有 *struct pci_dev* 的 PCI 类总线（如 ISA 和 EISA），你应该传入 *NULL*。需要这个参数是因为 DMA 翻译可能是总线特定的（并且通常是专属于设备所连接的总线的）。

size 参数是驱动程序需要分配的区域长度。

该例程为该区域分配 RAM，因此其作用类似于 `_get_free_pages`，但它接受的是大小而不是页面顺序。它返回两个值：虚拟地址（你可以使用它从 CPU 访问该区域）和 `dma_handle`（你将其传递给卡）。

CPU 返回地址和 DMA 总线主控地址都保证对齐到大于或等于请求大小的最小 `PAGE_SIZE` 顺序。这个不变条件的存在（例如）是为了保证，如果你分配一个小于或等于 64 千节的块，你收到的缓冲区范围不会跨越 64K 边界。

要解除映射并释放这样的 DMA 区域，驱动程序调用：

```c
pci_free_consistent(dev, size, cpu_addr, dma_handle);
```

其中 `dev, size` 与上述调用中的相同，`cpu_addr` 和 `dma_handle` 是 `pci_alloc_consistent` 返回给你的值。

### DMA 方向

下面描述的接口接受一个 DMA 方向参数，它是一个整数，取以下值之一：

- `PCI_DMA_BIDIRECTIONAL`
- `PCI_DMA_TODEVICE`
- `PCI_DMA_FROMDEVICE`
- `PCI_DMA_NONE`

如果你知道确切的 DMA 方向，请提供它。

值 `PCI_DMA_TODEVICE` 表示“从主内存到 PCI 设备”；`PCI_DMA_FROMDEVICE` 表示“从 PCI 设备到主内存。”强烈建议设备驱动程序开发者尽可能精确地指定这一点。

如果你绝对无法知道 DMA 传输的方向，请指定 `PCI_DMA_BIDIRECTIONAL`。这意味着 DMA 可以朝任一方向进行。平台保证你可以合法地指定这一点并且它会起作用，但这可能会以牺牲性能为代价。

值 `PCI_DMA_NONE` 用于调试。可以在你尚未得知 DMA 传输的确切方向之前，将此值保留在数据结构中。这有助于捕获方向跟踪逻辑未能正确设置参数的情况。

精确指定此值的另一个优势（除了潜在的平台特定优化外）在于调试。有些平台实际上有一个写权限布尔标志，可以用它来标记 DMA 映射，就像用户程序中的页面保护一样。此类平台可以并且确实会在内核日志中报告错误，当 PCI 控制器硬件检测到权限设置违规时。

只有流式映射指定方向；一致性映射隐含具有 `PCI_DMA_BIDIRECTIONAL` 的方向属性设置。

SCSI 子系统提供了机制，让你可以轻松获取在 SCSI 命令中使用的方向：

```c
scsi_to_pci_dma_dir(SCSI_DIRECTION)
```

其中 `SCSI_DIRECTION` 是从你的驱动程序正在处理的 SCSI 命令的 `sc_data_direction` 成员中获取的。上面提到的接口返回一个适合传递给下面流式 DMA 映射接口的值。

对于网络驱动程序，这是一件相当简单的事情。对于传输数据包，使用 `PCI_DMA_TODEVICE` 方向说明符进行映射和解除映射。对于接收数据包，则正好相反：使用 `PCI_DMA_FROMDEVICE` 方向说明符进行映射和解除映射。

## 使用流式 DMA 映射

流式 DMA 映射例程可以从中断上下文中调用。每种映射/解除映射都有两个版本，其中一个映射或解除映射单个内存区域，另一个映射或解除映射分散列表。

要映射单个区域，请输入：

```c
dma_addr_t dma_handle;
dma_handle = pci_map_single(dev, addr, size, direction);
```

要解除映射，请输入：

```c
pci_unmap_single(dev, dma_handle, size, direction);
```

你应该在 DMA 活动完成时调用 `pci_unmap_single`，例如，当中断状态告诉你 DMA 传输已完成时。

同样，对于分散列表，通过输入以下内容来映射从几个区域收集的缓冲区：

```c
int i, count = pci_map_sg(dev, sglst, nents, direction);
struct scatterlist *sg;
for (i = 0, sg = sglst; i < count; i++, sg++) {
    hw_address[i] = sg_dma_address(sg);
    hw_len[i] = sg_dma_len(sg);
}
```

其中 `nents` 是 `sglist` 中的条目数。

实现可以将几个连续的 `sglist` 条目合并为一个，并返回其映射到的实际 `sg` 条目数量。例如，如果 DMA 映射以 `PAGE_SIZE` 粒度完成，那么任何连续的 `sglist` 条目都可以合并为一个——前提是第一个条目结束且第二个条目开始于页面边界。事实上，这对于无法进行分散聚集或具有非常有限的分散聚集条目数量的卡来说是一个巨大的优势。

在这种情况下，你应该循环 `count` 次（这可能少于 `nents` 次），并使用 `sg_dma_address()` 和 `sg_dma_length()` 宏，而不是像上面所示那样访问 `sg->address` 和 `sg->length`。

要解除分散列表的映射，只需调用：

```c
pci_unmap_sg(dev, sglst, nents);
```

确保 DMA 活动已完成。

> **注意**
>
> *`pci_unmap_sg` 调用中的 `nents` 参数必须与你传入 `pci_map_sg` 调用的相同；它不应该是 `pci_map_sg` 调用返回的 `count` 值。*

每个 `pci_map_(single,sg)` 调用都应该有对应的 `pci_unmap_(single,sg)` 调用，因为总线地址空间是一种共享资源（尽管在某些端口中，映射是每个*总线*的，因此竞争同一总线地址空间的设备更少）。你可能会通过消耗所有总线地址而使机器无法使用。

如果你需要多次使用相同的流式 DMA 区域，并且在 DMA 传输之间接触数据，只需使用 `pci_map_(single,sg)` 映射该区域即可。每次 DMA 传输后，调用以下任一命令：

```c
pci_dma_sync_single(dev, dma_handle, size, direction);
```

或者：

```c
pci_dma_sync_sg(dev, sglist, nents, direction);
```

并且在最后一次 DMA 传输后，调用一个 DMA 解除映射例程 `pci_unmap_(single,sg)`。如果你没有接触第一个 `pci_map*` 的数据，并直接调用 `pci_unmap*`，那么你根本不需要调用 `pci_sync*` 例程。

下面是一些伪代码，展示了你需要使用 `pci_dma_sync_*( )` 接口的一种情况。

```c
my_card_setup_receive_buffer(struct my_card *cp, char *buffer, int len)
{
    dma_addr_t mapping;

    mapping = pci_map_single(cp->pdev, buffer, len, PCI_DMA_FROMDEVICE);
    cp->rx_buf = buffer;
    cp->rx_len = len;
    cp->rx_dma = mapping;
    give_rx_buf_to_card(cp);
}

...

my_card_interrupt_handler(int irq, void *devid, struct pt_regs *regs)
{
    struct my_card *cp = devid;
    ...
    if (read_card_status(cp) == RX_BUF_TRANSFERRED) {
        struct my_card_header *hp;

        /* 检查头部以查看我们是否希望
        * 接受数据。但首先要同步
        * DMA 传输与 CPU，
        * 以便我们看到更新的内容。
        */
        pci_dma_sync_single(cp->pdev, cp->rx_buf, cp->rx_len,
                           PCI_DMA_FROMDEVICE);

        /* 现在检查缓冲区是安全的。 */
        hp = (struct my_card_header *) cp->rx_buf;
        if (header_is_ok(hp)) {
            pci_unmap_single(cp->pdev, cp->rx_buf, cp->rx_len,
                            PCI_DMA_FROMDEVICE);
            pass_to_upper_layers(cp->rx_buf);
            make_and_setup_new_rx_buf(cp);
        } else {
            /* 只需将缓冲区交还给卡。 */
            // ...
        }
    }
}
```

