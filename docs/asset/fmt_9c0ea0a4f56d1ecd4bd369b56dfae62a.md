
## 4. 每个 UIO 设备可以提供一个或多个内存区域用于内存映射

每个映射在 sysfs 中都有自己的目录，第一个个映射显示为 `/sys/class/uio/uioX/maps/map0/`。随后的映射会创建 `map1/`、`map2/` 等目录。只有当映射索引不为 0 时，这些目录才会出现。每个 `mapX/` 目录包含四个只读文件，显示内存的属性：

- `name`: 此映射的字符串标识符。可选的，字符串可以为空。驱动程序可以使用此让用户空间更容易找到正确的映射。
- `addr`: 可映射的内存地址。
- `size`: 指向内存的大小，以字节为单位。
- `offset`: 在 `mmap()` 返回的指针上增加的字节偏移，以获取实际的设备内存。如果设备内存未对齐，则非常重要。记住 `mmap()` 返回的指针总是对齐的，因此良好的做法是始终加上此偏移。

中断通过读取 `/dev/uIO` 来处理。对 `/dev/uIO` 的阻塞型 `read()` 会在发生中断时立即返回。你也可以在 `/dev/uIO` 上使用 `select()` 等待中断。从 `/dev/uIO` 返回的整数值表示总中断计数。你可以使用这个数字来判断你是否漏掉了中断。

通过调用 UIO 驱动程序的 `mmap()` 函数，将设备内存映射到进程地址空间中。

## 内核 UIO API

UIO API 简单且易用：

1. `uio_info` 结构体告知你驱动程序的详细信息。其中一些成员是强制性的，另一些可选的。以下是 `uio_info` 的部分成员：
- `const char *name`: 强制性。驱动程序在 sysfs 中显示的名称。建议使用模块名称作为名称。
- `const char *version`: 强制性。此字符串出现在 `/sys/class/uio/uioX/version` 中。
- `struct uio_mem mem[MAX_UIO_MAPS]`: 如果你有可以使用 `mmap()` 映射的内存，则是强制性的。对于每个映射，你需要填充一个 `uio_mem` 结构体。详情见下文描述。
- `long irq`: 强制性。如果你的硬件产生中断，那么在初始化期间确定 irq 号是模块的任务。如果你没有硬件产生的中断，但想通过其他方式触发中断处理程序，将 `irq` 设置为 `UIO_IRQ_CUSTOM`。如果你完全没有中断，可以设置为 `UIO_IRQ_NONE`，尽管这很少有意义。
- `unsigned long irq_flags`: 如果你将 `irq` 设置为硬件中断号，则是强制性的。这里的标志将用于 `request_irq()` 的调用。
- `int (*mmap)(struct uio_info *info, struct vm_area_struct *vma)`: 可选。如果你需要特殊的 `mmap()` 函数，可以在这里设置。如果此指针不为 NULL，则将调用该函数而不是内置函数。
- `int (*open)(struct uio_info *info, struct node *inode)`: 可选。你可能想要有自己的 `open()`，例如仅在设备实际被使用时启用中断。
- `int (*release)(struct uio_info *info, struct node *inode)`: 可选。如果你定义了自己的 `open()`，你可能也会创建一个自定义的 `release` 函数。
- `int (*control)(struct uio_info *info, s32 irq_on)`: 可选。如果你需要通过向 `/dev/uioX` 写入来启用或禁用中断，请实现此函数。

通常，你的设备将有一个或多个可以映射到用户空间的内存区域。对于每个区域，你需要在 `mem[]` 数组中设置一个 `uio_mem` 结构体。`uio_mem` 结构体的字段描述如下：

- `int memtype`: 使用映射时是强制性的。如果你有物理内存需要映射，将其设置为 `UIO_MEM_PHYS`。对于逻辑内存使用 `UIO_MEM_LOGICAL`（例如通过 `kmalloc()` 分配）。还有用于虚拟内存的 `UIO_MEM_VIRTUAL`。
- `unsigned long size`: 填充 `addr` 指向的内存块的大小。如果大小为0，则该映射被视为未使用。注意，你必须将所有未使用的映射的 `size` 初始化为0。
- `void *internal_addr`: 如果你的内核模块可以访问此内存区域，你可能希望使用类似 `ioremap()` 的对其进行内部映射。此函数返回的地址无法映射到用户空间，因此你不能将其存储在 `addr` 中。使用 `internal_addr` 来记录此类地址。

`uio_register_device()` 函数将驱动程序连接到 UIO 框架：
- 需要一个 `uio_info` 结构体作为输入。
- 通常在平台设备驱动程序的 `probe()` 函数中调用。
- 它在 sysfs 中创建设备。
- `uio_unregister_device()` 函数将驱动程序与 UIO 框架断开。

## 平台驱动程序（第 5 章）

在本实验中，我们将为 UIO 开发一个平台驱动程序。UIO 驱动将把硬件寄存器暴露给用户空间。

```c
#include <linux/module.h>
#include <linux/platform.h>
#include <linux/io.h>
#include <linux/uio.h>
#include <linux/device.h>

static struct uio_info uio_info;
struct resource *res;
void *g_ioremap_addr;

static int my_probe(struct platform_device *pdev) {
    struct device *dev = &pdev->dev;

    /* 从设备树获取资源 */
    res = platform_get_resource(pdev, IRESOURCE_MEM);
    if (!res)
        return -ENEM;

    /* 映射内存并获取虚拟地址 */
    g_ioremap_addr = devm_ioremap(dev, res->start, resource_size(res));
    if (!g_ioremap_addr)
        return -ENEM;

    /* 初始化 uio_info 结构体 */
    uio_info.name = "led uio";
    uio_info.version = "1.0";
    uio_info.mem[0].type = UIO_PHYS;
    uio_info.mem[0].addr = res->start; /* 内核映射所需的物理地址 */
    uio_info.mem[0].size = resource_size(res);
    uio_info.mem[0].name = "demo_uio_driver_hw_region";
    uio_info.mem[0].internal_addr = g_ioremap_addr; /* 内部使用的虚拟地址 */

    /* 将设备注册到 UIO 框架 */
    if (uio_register_device(dev, &uio_info))
        return -EIO;

    return 0;
}

static int my_remove(struct platform_device *pdev) {
    uio_unregister_device(&pdev->dev);
    return 0;
}

static const struct of_device_id my_of_ids[] = {
    {.compatible = "arrow,UIO"},
};
MODULE_DEVICE_TABLE(of, my_of_ids);

static struct platform_driver my_platform_driver = {
    .probe = my_probe,
    .remove = my_remove,
    .driver = {
        .name = "UIO",
        .of_match_table = my_of_ids,
        .owner = THIS_MODULE,
    },
};

module_platform_driver(my_platform_driver);
MODULE_LICENSE("GPL");
```

# 第 5 章

## 平台驱动

8. 在“平台驱动”总线上注册你的驱动：

```c
module_platform_driver(my_platform_driver);
```
