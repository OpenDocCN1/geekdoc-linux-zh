
## 2. 声明结构体 `uio_info`：

```c
static struct uio_info the_uio_info;
```

## 3. 在 `probe()` 函数内部声明 `resource` 变量：

```c
struct resource *r;
```

## 4. 在 `probe()` 函数内部编写 `platform_get_resource()` 函数。它将从设备获取内存资源并将其返回给 `resource` 变量：

```c
r = platform_get_resource(dev, IORESOURCE_MEM, 0);
if (!r) {
    pr_err("IORESOURCE_MEM, 0 does not exist\n");
    return -EINVAL;
}
```

## 5. 初始化 "struct uio_info"：

```c
the uio_info.name = "led uio";
the uio_info.version = "1.0";
the uio_info[0].type = UIO_MEM_PHYS;
the uio_info[0].addr = r->start; /* 内内核用户映射的物理地址 */
the uio_info[0].size = resource_size(r);
the uio_info[0].name = "uio_driver_hw_region";
the uio_info[0].internal_addr = g_ioremap_addr; /* 内部驱动使用的虚拟地址 */
```

## 6. 将设备注册到 UIO 框架：

```c
uio_register_device(&dev->dev, &the_uio_info);
```

## 7. 将 "UIO" 添加到驱动支持的设备列表，以及 `platform_driver` 结构体中：

```c
static const struct device_id my_of_ids[] = {
    .compatible = "arrow,UIO",
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
```

## 8. 在设备树（Device Tree）中添加 "UIO" 节点。你将添加 `reg` 属性，包括 GPIO 内存的基地址及其大小。

```
UIO {
  compatible = "arrow,UIO";
  reg = <0x0209C000 0x4000>
  pinctrl-0 = <&pinctrl_led>
};
```

# UIO 用户态驱动

## 1. 包含所需的头文件：

```c
#include <sys/mman.h> // mmap()
```

## 2. 定义 sysfs 参数的路径，从该路径获取要映射内存的大小：

```c
#define UIO_SIZE "/sys/class/uio/uio0/maps/map0/size"
```

## 3. 打开 UIO 设备：

```c
open("/dev/uio0", O_RDWR | O_SYNC);
```

## 4. 获取要映射内存的大小：

```c
FILE *size_fp = fopen(UIO_SIZE, "r");
sscanf(size_fp, "0%08X", &u_size);
```

## 5. 返回一个指向虚拟地址的指针，对应于在内核空间驱动中获取的 `r->start` 物理地址。现在你可以通过向返回指针变量指向的虚拟寄存器地址控制 LED：

```c
demo_driver_map = mmap(NULL, uio_size, PROT_READ | PROT_WRITE, MAP_SHARED, devuio_fd, 0);
```

# 列表 5-5：led_UIO_platform.c

```c
#include <linux/module.h>
#include <linux/platform_device.h>
#include <linux/io.h>
#include <linux/uio_driver.h>

static void iomem *g_ioremap_addr;
static struct uio_info *uio_info;
static int __init my_probe(struct platform_device *pdev)
{
    struct resource *r;
    struct device *dev = &pdev->dev;
    int i;
    unsigned int temp;

    pr_info("platform_probe enter\n");

    /* 从设备树获取我们的第一个内存区域 */
    r = platform_get_resource(pdev, IORESOURCE_MEM, 0);
    if (!r) {
        pr_err("IORESOURCE_MEM does not exist\n");
        return -ENVAL;
    }
    pr_info("r->start = 0x%08lx\n", (long (unsigned int)r->start);
    pr_info("r->end = 0x%08lx\n", (long (unsigned int)r->end);

    /* ioremap 内存区域并获取虚拟地址 */
    g_ioremap_addr = devm_ioremap(dev, r->start, resource_size(r));
    if (!g_ioremap_addr) {
        pr_err("ioremap failed \n");
        return -ENOMEM;
    }

    /* 初始化 uio_struct */
    uio_info->name = "led_uio";
    uio_info->version = "1.0";
    uio_info->info[0].type = UIO_MEM_PHYS;
    uio_info->info[0].addr = r->start; /* 内核用户映射的物理地址 */
    uio_info->info[0].size = resource_size(r);
    uio_info->info[0].name = "uio_driver_hw_region";
    uio_info->info[0].internal_addr = g_ioremap_addr; /* 内部驱动使用的虚拟地址 */

    /* 注册设备 */
    ret_val = uio_register_device(&dev->dev, &uio_info);
    if (ret_val != 0) {
        pr_warn("Could not register device_uio...\n");
    }
    return 0;
}
static int __exit my_remove(struct platform_device *pdev)
{
    pr_info("platform remove\n");
    uio_unregister_device(&uio_info);
    return 0;
}

static const struct device_id my_of_ids[] = {
    {.compatible = "arrow,UIO"},
    {},
};
MODULE_DEVICE_TABLE(of, my_of_ids);

static struct platform_driver my_platform_driver = {
    .probe = my_probe,
    .remove = my_remove,
    .driver = {
        .name = "UIO",
        .of_match_table = my_of_ids,
        .owner = THIS_MODULE,
    }
};
module_platform_driver(my_platform_driver);
MODULE_LICENSE("GPL");
MODULE_AUTHOR("Alberto Liberal <liberal@europe.com>");
MODULE_DESCRIPTION("这是一个用于控制 LED 的 UIO 平台驱动");
```

# 列表 5-6：UIO_app.c

```c
```
