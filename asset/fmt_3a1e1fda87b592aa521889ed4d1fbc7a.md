
你可能已经注意到 `request_region()` 函数返回一个指向类型为结构的指针：

```c
struct resource {
    const char *name;
    unsigned long start, end;
    unsigned long flags;
    struct resource *parent, *sibling, *child;
};
```

它代表了一层抽象：资源是某个实体的一部分，可以独占地分配给某个设备驱动程序。在这种情况下，它是 I/O 端口的范围。

在此结构中，`name` 元素描述资源的所有者，`start` 和 `end` 元素给出资源的范围（它们的精确含义取决于资源的具体类型），`flags` 元素可以用于描述各种属性，而 `sibling` 和 `child` 字段将该结构置于资源树中，该树包含了所有相同类型的资源。

因此，所有引用 I/O 端口的项都在从 `ioport_resource` 根节点派生的树中。I/O 端口的管理可以通过以下函数完成：

```c
#include <ioport.h>
int request_resource(struct resource *root, struct resource *new);
int release_resource(struct resource *new);
```

而不是通过之前描述的 `*_region()` 函数，这些函数仅仅是 `*_region()` 函数的封装。

# 示例：

```c
#include <ioport.h>
static struct resource my_dev_resource = { "my_dev", };
static int my_dev_detect( unsigned long port_addr,
```

## 19.5 从 I/O 寄存器读写数据

```c
unsigned long end = port_addr + extent;
my_resource.start = port_addr;
my_resource.end = end;
```

```c
if (!request_resource(&ioport_resource, &my_resource)) {
    return -EBUSY;
}/* 端口忙 */
```

```c
if (mydrv_probe(port_addr, extent) != 0) {
    release_resource(&my_resource);
    return -ENODEV; /* 找不到设备 */
}
return 0;
```

对于特定的总线，有一些可选的便利函数，用于请求 I/O 资源并对其进行重映射。对于 PCI，可以使用在 `/usr/src/linux/drivers/pci/pci.c` 中定义的函数（以及函数）：

```c
int pci_request_region(struct pci_dev *pdev, int bar, const char *res_name);
int pci_request_regions(struct pci_dev *pdev, const char *res_name);
int pci_release_regions(struct pci_dev *pdev);
void pci_release_region(struct pci_dev *pdev, int bar);
```

你可以请求与设备相关的特定 `bar`（基地址寄存器），`bar` 的范围从 0 到 5，也可以请求与设备相关的所有区域。

`res_name` 参数是显示在 `/proc/iomem` 下的内容。

## 19.5 从 I/O 寄存器读写数据

下列宏定义在 `asm/io.h` 中，它们提供了单次或多次读写 8 位、16 位和 32 位端口的能力：

读取：

```c
unsigned char inb (unsigned long port_address);
unsigned short inw (unsigned long port_address);
unsigned long inl (unsigned long port_address);
void             insb (unsigned long port_address, void *addr, unsigned long count);
void             insw (unsigned long port_address, void *addr, unsigned long count);
void             insl (unsigned long port_address, void *addr, unsigned long count);
```

写入：

```c
void outb (unsigned char b, unsigned long port_address);
void outw (unsigned short w, unsigned long port_address);
```

```c
void outl (unsigned long 1, unsigned long port_address);
void outsb (unsigned port_address, void *addr, unsigned long count);
void outsw (unsigned port_address, void *addr, unsigned long count);
void outsl (unsigned port_address, void *addr, unsigned long count);
```

长长度函数仅提供 32 位操作，即使在 64 位平台上也没有 64 位的数据路径。

上述函数带有 `count` 参数，但并不是写入一个地址范围；它们只写入单个端口地址，但它们会高效地循环执行该操作。

这些函数都以小端序（little-endian）进行 I/O 操作，并进行任何必要的字节交换。

读写 I/O 端口可能需要使用内存屏（memory barriers），我们之前讨论过这些。

示例：

```c
outb(MSE_CONTROL, MSE_PORT);
dx = (inb)(MSE_PORT);
```

## 19.6 硬件 I/O

下列宏定义在 `asm/io.h` 中，提供了单次或多次读写 8 位、16 位和 32 位端口的能力：

（此处文本似乎存在重复或碎片化，保持结构）

有时，你可能会发现使用以下函数将 I/O 寄存器或端口与 I/O 内存关联起来：

```c
#include <asm-generic/iopmap.h>
void iomap(unsigned long io_port, unsigned int count);
void ounmap(void *addr);
```

通过使用这些函数，I/O 端口显示为内存。在此之前通常会请求这些端口。完成后，可以使用后续讨论的读写函数进行访问。

## 19.7 分配与映射 I/O

非平凡设备几乎总是通过内存访问。具体的访问方式取决于架构。然而，Linux 通过通用接口处理了这种依赖。

使用这些区域有三个基本步骤：请求、重映射以及使用相应的读写函数。

在使用此类内存区域之前，必须请求（并最终释放）：

```c
struct resource *request_mem_region(unsigned long start, unsigned long len, char *name);
void release_mem_region(unsigned long start, unsigned long len);
```

这些函数作用于设备，从地址延伸，并使用名称描述在 `/proc/mem` 中创建的条目。起始地址是设备的特性；例如，PCI 设备可以从配置寄存器读取，或从函数 `pci_resource_start()` 获取。

你不能直接使用起始地址的指针；相反必须对其进行重映射并最终取消：

```c
#include <linux/iopmap.h>
void iomap(unsigned long phys_addr, unsigned long size);
void ounmap(void *addr);
```

一旦有了特定总线的可选便利函数，例如：

```c
void pci_iomap(struct pci_dev *dev, int bar, unsigned long maxlen);
void pci_iounmap(struct pci_dev *dev, void *iomem *addr);
```

定义在 `/usr/src/linux/lib/iopmap.c` 中。

注意这些函数并不请求内存区域，那必须单独完成。

## 19.8 访问 I/O 内存

对重映射的 I/O 内存进行读写可以通过以下函数实现：
