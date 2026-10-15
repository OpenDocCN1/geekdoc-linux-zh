
```c
struct pci_driver {
	uint32_t id;
	const struct pci_device_id *id_table;
	char *name;
	const struct ops *driver; /* 必须非 NULL 以调用 probe */
	int (*probe)(struct pci_dev *dev, void *id); /* 插入新设备时 */
	int (*remove)(struct pci_dev *dev); /* 设备移除时（如果没有热插槽） */
	int (*suspend)(struct pci_dev *dev, struct message_state *state); /* 挂起时 */
	int (*resume)(struct pci_dev *dev); /* 设备唤醒时 */
	void (*shutdown)(struct pci_dev *dev);
	void (*error_handlers)(char *err_handler);
	struct device *driver;
	size_t pci_device_count;
}
```

数据结构的重要元素是：我们没有提供跳转表的描述。对于特定设备的函数可以设置为 NULL。ID 表是 `pci_device_id` 结构数组，必须以 NULL 条目结尾：

```c
struct pci_device_id {
	u16_t vendor;            /* 厂商 ID */
	u16_t device;            /* 子系统 ID 和 PCI ID */
	u16_t class, subclass;  /* 如果是三元组的类，子类 */
	u32_t driver_data;      /* 驱动私有 */
};
```

此表使用 `pci_driver()` 宏进行填充，如下：

```c
static struct pci_device_id tgb_pci_table[] = {
	PCI_DEVICE(PCI_VENDOR_BROAD, PCI_DEVICE_TIGON3_5700),
	PCI_DEVICE(PCI_VENDOR_BROAD, PCI_DEVICE_TIGON5_5701),
	PCI_DEVICE(PCI_VENDOR_ALTIM, PCI_DEVICE_ALTIM_AC9100),
	PCI_DEVICE(PCI_VENDOR_APPLE, PCI_DEVICE_APPLE_TIGON3),
	{0 }
};
```

在对设备进行任何操作之前，调用 `pci_enable(dev)` 启用设备是非常重要的。这会开启 I/O 和内存区域，分配可能需要的资源，并在设备处于挂起状态时唤醒。该函数由 `probe` 回调调用。

## 22.4 访问配置空间

内核在 `usr/src/linux/Documentation/pci.txt` 文件中包含了编写 PCI 设备驱动程序的优秀介绍。

找到设备后，在对其进行任何操作之前，你需要调用函数 `ci_enable_device(struct pci_dev *pci_dev)` 来启用它。

### 示例

定位并启用特定设备：

```c
#include <linux/pci.h>

struct pci_dev *pdev = NULL;

if (pdev != pci_get_device(pci, PCI_VENDOR_ID_INTERG, PCI_DEVICE_ID_INTERG_162, pdev)) {
    return -ENOMEM;
}
```

如果需要，可以调用函数

`char *pci_name = pci_dev_name(pdev);`

来获取设备名称、设备和功能号。它不是通过探测实现的，而是通过遍历列表实现的。

## 22.3 结构和函数

头文件 `usr/src/linux/include/pci.h` 定义了值的名称。可以通过以下方式定位：

```c
#include <pci.h>
```

```c
struct pci_dev *pci_get_device(unsigned vendor, unsigned device);
struct pci_dev *pci_get_remove(unsigned vendor, unsigned device);
struct pci_dev *pci_get_class(unsigned class, unsigned subclass);
```

这些函数通常在循环中被调用。如果函数的返回值不是 NULL，则返回描述设备的结构，并增加引用计数。当设备被移除（系统卸载）时，必须调用函数：

```c
void pci_dev_put(struct pci_dev *dev);
```

来减少引用计数；否则如果是热插槽，它将无法从系统中移除。

## 22.4 访问配置空间

配置空间可以通过 8 位、16 位或 32 位数据进行访问。

```c
int pci_read_config(struct pci_dev *dev, int offset, u32 *val);
int pci_read_config(struct pci_dev *dev, int offset, u16 *val);
int pci_read_config(struct pci_dev *dev, int offset, u8 *val);
int pci_write_config(struct pci_dev *dev, int offset, u32 val);
int pci_write_config(struct pci_dev *dev, int offset, u16 val);
int pci_write_config(struct pci_dev *dev, int offset, u8 val);
```

这些函数用于写入或从由 `dev` 标识的配置空间读取。配置空间的偏移由 `where` 给出。

注意 (`u8`, `u16`, `u32`, `u64`) 的使用。这些是在需要双精度时使用的内核数据类型。（有符号版本，如 `s16`, `s32`, `s64`，很少使用）。只要在前面加上双核心前缀，你也可以在用户态中使用这些（例如 ...`u32`），并包含 `linux.h`。

# 第 22 章. PCI

## 22.6 PCI EXPRESS 261

根据 PCI 标准，配置寄存器中的多字节条是小端序（little-endian），这是 x86 平台的惯例。数据类型和函数会处理任何所需的字节交换，除非在像 SPARC 这样的大端序系统上，否则你不需要担心位顺序。但应该注意这一点。字节序由 `word` 和 `dand` 函数处理（注意某些架构，如 `alpha` 和 `IA64` 是小端序，且可以配置为任何一种）。

配置变量通过使用 `/usr/src/linux/include/pci_reg.h` 中定义的符号进行访问：

```c
pci_read_config_dev(dev, PCI_REVISION_ID, kredev),
```

也可以使用 `setci` 工具来获取和设置配置中的值。

```
2.6.31: 772    mmio_start = pci_resource_start(dev, 1);
2.6.31: 773    mmio_end = pci_resource_end(dev, 1);
2.6.31: 775    mmio_flags = pci_resource_flags(dev, 1);
2.6.31: 776    mmio_len = pci_resource_len(dev, 1);
    ...
```

## 22.6 PCI EXPRESS

PCI 早于 1991 年引入，后来增强为 PCI-X，它已经显得有些过时了。特别是带宽限制为最高 133 MB/s。此外，带宽在总线上的所有设备之间共享，必须对带宽的竞争进行协商。

1997 年引入了 AGP（加速图形接口），它拥有自己的带宽。但 AGP 缺乏后续动力。

PCI Express（现在称为 PCIe）于 2004 年引入并正受到关注。它的主要优势是点对点连接；带宽通过串行总线直接传输。此外，提供链式连接更简单，且功耗比 PCI 低。

每个设备通过数量数量通道（lanes）连接，每个通道都是双向的，每个方向的数据速率为 250 MB/s，总数据传输速率高达 500 MB/s。

通道的数量取决于插槽和卡；有 1、2、4 和 16 个插槽可用；x16 插槽的带宽为 8000 MB/s，用于显卡。x32 和 x64 卡也用于该插槽。

任何 PCI 卡都可以在任何与它等大的插槽中正常工作；例如，如果你将一个 x1 卡插入 x16 插槽，它将使用较少的通道。

由于用于 PCI 的设备驱动程序在 PCIe 上也能良好工作，因为该标准的设计目标是尽可能减少干扰。

## 22.5 访问 I/O 空间和内存空间

提到的，我们不仅可以访问配置寄存器，还可以访问与 PCI 设备相关的 I/O 端口和内存区域。虽然列出这些寄存器是可能的，但使用内核提供的通用资源管理函数更简单。

相关函数为：
