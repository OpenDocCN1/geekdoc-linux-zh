
## DMA 映射

为了设置 DMA 传输，必须进行 DMA 映射（DMA Mapping），这涉及两个步骤：分配缓冲区，并为其生成一个供设备使用的地址。具体的实现细节取决于架构，但分配和释放的函数在各个平台上是相同的：

```c
void *dma_alloc_coherent (struct device *dev, size_t size, dma_addr_t *dma_handle, gfp_t flag);
void dma_free_coherent (struct device *dev, size_t size, void *vaddr, dma_addr_t dma_handle);
```

分配函数返回一个长度为 `size` 字节的缓冲区内核虚拟地址。第三个参数指向总线上的地址（可选使用）。`flag` 参数控制内存的分配方式，如果不允许睡眠（例如在中断上下文中），通常使用 `GFP_KERNEL` 或 `GFP_ATOMIC`。如果掩码需要，也可以分配 `GFP`。这部分内存可以使用 `dma_free_coherent()` 释放，它同时需要两个地址。

使用 `dma_alloc_coherent()` 分的内存区域用于所谓的相干 DMA 映射（Coherent DMA Maps），它们被认为是同步或一致的。它们具有以下属性：

- CPU 和设备可以并行访问该缓冲区。
- 设备或 CPU 的写入可以立即被另一方读取，而无需担心缓存问题或刷新。（然而，你可能仍然需要使用各种内存屏障，因为 CPU 可能会重排 I/O 指令以维持维护普通系统内存时的一致性）。
- 最小分配通常是一个页。在 x86 上，实际上获得的是 2 的幂方的页数，因此这可能开销较大。

由于这种方法相对昂贵，它通常用于贯穿设备生命周期的 DMA 缓冲区。一个很好的例子是网络 DMA 环描述符。

对于单次操作，设置一致性流 DMA 映射（Streaming DMA mappings），它们也可以被视为异步的。它们由以下函数控制：

```c
dma_addr_t dma_map_single (struct device *dev, void *ptr, size_t size,
	enum dma_data_direction direction);
void dma_unmap_single (struct device *dev, dma_addr_t dma_addr, size_t size);
```

### 表 22.1：DMA 传输值

| 值 | 含义 |
| :--- | :--- |
| `PCI_DMA_DEVICE` | 数据流向设备，例如写入。 |
| `PCI_DMA_FROMDEVICE` | 来自设备的数据，例如读取。 |
| `PCI_DMA_BIDIRECTION` | 数据双向传输。 |
| `PCI_DMA_NONE` | 用于调试；任何尝试使用该内存的操作都会导致失败。 |

流式 DMA 映射可能用于网络数据包、文件系统缓冲区。它们具有以下属性：

- 传输方向必须与映射时给出的值匹配。
- 缓冲区映射后，它属于设备而非 CPU；驱动程序在取消映射之前不应触碰该缓冲区。
- 因此，对于写入，数据应在映射之前放入缓冲区中；对于读取，在取消映射（可以通过中断完成）之前不应触碰它。

第三种映射类型是所谓的离散-聚集 DMA（Scatter-gather DMA）。它允许多个（可能是不连续的）缓冲区同时向设备或从设备传输。还可以设置一个 DMA 池（DMA pool），其工作方式类似于内存缓存。

内核没有使用通用接口，而是使用了 PCI 特有的接口。这些函数与以下内容一一对应：

```c
#include <linux/pci.h>

int pci_dma_supported(struct pci_dev *dev, u64 mask);
int pci_set_dma_mask(struct pci_dev *dev, u64 mask);
void pci_alloc_coherent(struct pci_dev *dev, size_t size, dma_addr_t *dma_handle);
void pci_free_consistent(struct pci_dev *dev, size_t size, void *vaddr, dma_addr_t dma_handle);
dma_addr_t pci_map_single(struct pci_dev *dev, void *ptr, size_t size, int direction);
void pci_unmap_single(struct pci_dev *dev, dma_addr_t dma_addr, size_t size, int direction);
```

虽然这个旧的 API 尚未移除，但它现在只是更通用接口的封装，在任何新代码中都应该使用后者。

## 22.6. DMA 池 (Pool)

假设你需要进行小内存传输，设置一致性流 DMA 映射。对于传输，`dma_alloc_coherent()` 的最小单位是页。因此，可以使用一个 DMA 池，其工作方式非常类似于内存缓存。

基础函数如下：

```c
#include <linux/dmapool.h>

struct dma_pool *dma_pool_create(const char *name, struct device *dev, size_t size, size_t align);
void dma_pool_destroy(struct dma_pool *pool);
```

```c
void *dma_pool_alloc(struct dma_pool *pool, gfp_t flags, dma_addr_t *handle, size_t size);
void dma_pool_free(struct dma_pool *pool, void *vaddr, dma_addr_t dma_addr);
```

使用 `dma_pool_create()` 设置一个带有 `name` 并与 `dev` 关联的长度为 `size` 字节的池。`align` 参数（字节为单位）是分配的对齐方式。如果 `align` 不零，则池中的缓冲区不会跨越边界。

实际分配通过 `dma_pool_alloc()` 完成。`flags` 参数提供常用的分配标志（`GFP_KERNEL`, `GFP_ATOMIC` 等）。返回值为内核虚拟地址，存储在 `handle` 中作为总线地址。

为了防止内存，缓冲区应通过 `dma_pool_free()` 返回池中；当所有缓冲区都释放后，可以使用 `dma_pool_destroy()` 清除池。

注意，使用池分配的内存将具有一致性 DMA 映射，这意味着设备和驱动程序可以使用它们而无需刷新缓存。

## 22.7. 离散-聚集映射

如果你只有一个（大或小小的）连续缓冲区可以操作，那么 DMA 传输就很简单。你只需提供起始地址和长度即可开始传输。

然而，你可能同时需要传输多个缓冲区，并且它们是不连续的。这可能由于：

- `readv()` 或 `writev()` 系统调用。
- 磁盘 I/O 请求。
- 映射内核 I/O 缓冲区列表（例如在使用 `get_user_pages()` 时）。

当然，你可以链接一系列单独请求，每个请求代表一个连续区域。但许多设备能够在硬件层面提供帮助，可以给设备一个由指针和长度组成的离散列表（scatterlist），然后它将作为一个操作来处理。

为了实现这一点，你首先必须建立描述所需缓冲区的结构数组。对于 x86，该结构描述在 `/usr/src/linux/arch/x86/include/asm/scatterlist.h` 中，看起来如下：

```c
struct scatterlist {
unsigned long page_link;
	unsigned int offset;
	unsigned int length;
	dma_addr_t dma_address;
	unsigned int dma_length;
};
```

填充字段的最佳方式是：

```c
void sg_set_page(struct scatterlist *sg, struct page *page, unsigned int len,
	unsigned int offset);
```

定义在 `/usr/src/linux/include/linux/scatterlist.h` 中，以及许多其他用于聚集分散结构（gathering-scatter structures）的实用便利函数。

驱动程序为数组中的每个缓冲区设置页（page）、偏移（offset）和长度（length）字段；注意长度以字节为单位。

`dma_address` 字段由函数填充：
