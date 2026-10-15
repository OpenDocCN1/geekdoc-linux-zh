
`ret_val = misc_register(&led_device->led_misc_device);`

`if (ret_val) return ret_val; /* misc_register 成功返回 0 */`

`/* 将私有结构体绑定到 pdev`

` * 以在 remove() 函数中恢复 */`

`platform_set_drvdata(pdev, led_device);`

`pr_info("leds_probe exit\n");`

`return 0;`

`}`

`/* remove() 函数每个 led 被调用 3 次 */`

`static int __exit led_remove(struct platform_device *pdev)`

`{`

`    struct led_dev *led_device = platform_get_drvdata(pdev);`

`    pr_info("leds remove enter\n");`

`    misc_deregister(&led_device->led_misc_device);`

`    pr_info("leds remove exit\n");`

`    return 0;`

`}`

`static const struct of_device_id my_of_ids[] = {`

`    {.compatible = "arrow,RGBleds"},`

`};`

`MODULE_DEVICE_TABLE(of, my_of_ids);`

`static struct platform_driver led_platform_driver = {`

`    .probe = led_probe,`

`    .remove = led_remove,`

`    .driver = {`

`        .name = "RGBleds",`

`        .of_match_table = my_of_ids,`

`    },`

`    .owner = THIS_MODULE,`

`};`

`static __init led_init(void)`

`{`

`    int ret_val;`

`    pr_info("demo_init enter\n");`

`    ret_val = platform_driver_register(&led_platform_driver);`

`    if (ret_val != 0) {`

`        pr_err("platform value returned %d\n", ret_val);`

`        return ret_val;`

`    }`

`    pr_info("demo_init exit\n");`

`    return 0;`

`}`

`static __exit led_exit(void)`

`{`

`    pr_info("led_driver enter\n");`

`    /* 在退出前清除所有 leds */`

`    iowrite32(PIO_ALL_LEDS, PIO_SDR1_W);`

`    platform_driver_unregister(&led_platform_driver);`

`    pr_info("led_driver exit\n");`

`}`

`module_init(led_init);`

`module_exit(led_exit);`

`MODULE_LICENSE("GPL");`

`MODULE_AUTHOR("Alberto@arrow.com");`

`MODULE_DESCRIPTION("这是一个控制三个 led 设备的平台驱动");`

## ledRGB_platform.ko 演示

```
root@sam2-explained:~# insmod ledRGB_platform.ko /* 加载模块 */
root@sam2-explained:~# ls /dev/led/* 设置设备 */
root@sam2-explained:~# echo on > /ledblue /* 开启 blue */
root@sam2-explained:~# echo on > /ledred /* 开启 red */
root@sam2-explained:~# echo on > /ledgreen /* 开启 green */
root@sam2-explained:~# echo 0 > /ledgreen /* 关闭 green */
root@sam2-explained:~# echo off > /ledred /* 关闭 red */
root@sam2-explained:~# echo cat /ledblue /* 检查 blue 状态 */
root@sam2-explained:~# echo cat /ledgreen /* 检查 green 状态 */
root@sam2-explained:~# echo cat /ledred /* 检查 red 状态 */
root@sam2-explained:~# rmmod ledRGB_platform.ko /* 移除模块 */
```

## 平台驱动

特定驱动管理的每个设备使用不同的硬件资源（例如 I/O 寄存器的内存地址、DMA 通道、IRQ 中断）。

平台驱动通过内核 API 访问这些资源。这些内核函数会自动从 `include/linux/platform_device.h` 中定义的 `struct platform_device` 数组数组。该数组已通过 DT 设备节点属性（例如 `reg`, `clocks`, `interrupts`）填充。位于 `Documentation/devicetree/bindings` 下的 `resource-names.txt` 文件可以通过索引访问的不同资源属性。

```c
struct platform_device {
    char *name;
    u32 id;
    struct device dev;
    u32 num_resources;
    struct resource *resource;
};
```

是 `struct resource` 结构的定义：

```c
struct resource {
    resource_size_t start;
    resource_size_t end;
    const char *name;
    unsigned long flags;
    unsigned long desc;
    struct resource *parent, *sibling, *child;
};
```

是上述结构体中每个元素的含义：

- `start`/`end`：表示资源的起始/结束位置。对于 I/O 或内存区域，代表它们的起始/结束位置。对于 IRQ 线、总线或 DMA 通道，`start`/`end` 的值必须相同。
- `flags`：这是一个表征资源类型的掩码，例如 `IORESOURCE_MEM`。
- `name`：标识或描述资源。

# 第 5 章

有许多辅助函数从资源数组中提取数据：

1. 在 `drivers/base/platform.c` 中定义的函数 `platform_get_resource` 用于为设备获取资源，并返回一个填充了资源值的 `struct resource` 结构。你可以在驱动代码中使用这些值，将它们映射到虚拟空间中。

下面是 `platform_get_resource` 函数的代码：

```c
struct resource *platform_get_resource(struct platform_device *dev,
                               unsigned int type,
                               unsigned int num) {
    int i;
    for (i = 0; i < dev->num_resources; i++) {
        struct resource *r = &dev->resource[i];
        if (type == resource_type(r) && num == 0)
            return r;
    }
    return NULL;
}
```

第一个参数告诉函数你感兴趣的设备，以便提取所需信息。第二个参数取决于你正在处理的资源类型。如果是内存（任何可以映射为内存的内容），则为 `IORESOURCE_MEM`。你可以在 `include/linux/ioport.h` 中看到所有的宏。最后一个参数确定所需的该类型的资源，零表示第一个。因此，例如驱动可以使用以下代码找到并映射其 MMIO 区域（DT `reg` 属性）：

```c
struct resource *r;
r = platform_get_resource(pdev, IORESOURCE_MEM, 0);
```
