
`dma_pool_create()` 不会执行实际映射；它只是建立了一个带有名称的设备结构关联的池；如果请求分配，将按大小进行分配。

对齐参数（如果为0）是池分配的硬件对齐方式。池中的最终分配如果不是 `PAGE_SIZE`，则不会跨越页边界。

实际映射由 `dma_pool_alloc()` 完成。`flags` 参数决定映射是否为一致性（如 `GFP_SYNC` 等）。返回值是 DMA 缓冲区的虚拟地址，CPU 可以访问该地址。

为了避免内存泄漏，应该通过 `dma_pool_free()` 将缓冲区返回池，并在完成后使用 `dma_pool_destroy()` 清除池。

注意，池的分配将使用一致性 DMA 映射，这意味着设备和驱动程序都可以在无需刷新缓存的情况下使用。

## 23.7 分散/聚集映射 (Scatter/Gather Mappings)

![](img/5f0cab84232061dba742ffc69894b1f1_145_0.png)

如果你只有一个（大或小）连续缓冲区可以工作，那么创建 DMA 是很容易的。你只需要提供起始地址和长度，让驱动程序处理传输即可。

然而，可能需要同时运行多个缓冲区，且它们可能是不连续的。这可能由于：

- `Read()` 或 `write()` 系统调用。
- 磁盘 I/O 请求。
- 映射的内核 I/O 缓冲区中一组页的传输（例如使用连续区域时的情况，许多设备都能做到这一点）

2.4 内核没有使用通用接口，而是使用了 PCI 特有的接口。这些函数与通用函数一一对应，如下：

```c
#include <linux/pci.h>

int dma_lease(struct pci_dev *dev, size64 size);

int dma_alloc_consistent(struct pci_dev *dev, size_t size, void **addr, int __handle);

void dma_free_coherent(struct pci_dev *dev, void *ptr, size_t size);

size_t dma_map(struct pci_dev *dev, void *addr, size_t size, size_t direction, int __handle);

void dma_unmap(struct pci_dev *dev, void *ptr, size_t size, size_t direction);
```

虽然这个旧 API 已经被移除，但它现在是通用接口的封装，任何新代码都应该使用它。

当然可以链链一系列单个请求，每个请求代表一个连续区域。许多设备能够在硬件层面组装这些；因此可以给设备提供一个指针和长度的散列表（scatterlist），它将负责将这一切作为一个一个操作完成。

一旦到了传输每个缓冲区时，由于架构差异，不应直接引用 scatterlist 数据结构，而应该使用宏：

为了符合要求，你首先必须设置一个描述所需传输的结构数组。对于 x86，该结构定义在 `/usr/src/linux/arch/x86/include/asm`，看起来如下：

```c
dma_set_dma_address(struct scatterlist *sg);
```

```c
unsigned int dma_map_len(struct scatterlist *sg);
```

```c
struct scatterlist {
    unsigned long page_link;
    unsigned int offset;
    unsigned int dma_addr;
    unsigned int length;
    unsigned int unused;
};
```

驱动程序映射数组中每个缓冲区的页、偏移和长度字段；注意 `length` 是以字节为单位的。设备将在后续函数中填充字段：

```c
dma_map_sg(struct device *dev, struct scatterlist *sg, int nents, enum dma_data_direction);
```

```c
void dma_unmap_sg(struct device *dev, void *ptr, size_t size, size_t direction);
```

在完成传输后，调用返回总线（DMA）地址和缓冲区的长度（这与传递给 `dma_map_sg` 的值不同，因为缓冲区一致性）。这里是数组中的缓冲区数量。此函数返回要传输的缓冲区数量。因为相邻缓冲区会被合并：

## 23.8 ISA 下的 DMA (DMA UNDER ISA)

有两种 ISA DMA 传输：原生主板控制器和 ISA 主模式（由外设设备控制一切）。这种类型很少见，我们并不常见，但它与 PCI 传输类似。

![](img/5f0cab84232061dba742ffc69894b1f1_146_0.png)

DMA 控制器（8237）管理传输的方向和状态。当收到 DMA 请求时，它会信号 CPU。随后设备就可以读写数据。这些电路现在是主板控制器的一部分，而不是独立的 8237。

外设设备在需要读写时必须发出 DMA 请求。对于传输，更容易准备好，在传输完成时响应中断。

在内核版本 2.6.24 中，scatterlist 结构变为：

```c
struct scatterlist {
    unsigned long page_link;
    unsigned int offset;
    unsigned int length;
    unsigned int dma_addr;
    unsigned int unused;
};
```
