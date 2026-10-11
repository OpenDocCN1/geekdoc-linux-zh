
```c
struct platform_driver {
  int (*probe)(struct platform_device *);
  int (*remove)(struct platform_device *);
  void (*shutdown)(struct platform_device *);
  int (*suspend)(struct platform_device *, pm_message_t state);
  int (*suspend_late)(struct platform_device *, pm_message_t state);
  int (*resume_early)(struct platform_device *);
  int (*resume)(struct platform_device *);
  struct device_driver driver;
};
```

至少必须提供 `probe()` 和 `remove()` 回调函数。`probe()` 函数在“总线驱动程序”将“设备”配对“设备驱动”时被调用。`probe()` 函数负责在相应的内核框架中初始化并注册它：

- 1. 它获取设备结构指针作为参数（例如，`struct pci_dev *`, `usb_dev *`, `struct platform_device *`, `struct i2c_client *`）。
- 2. 它初始化设备、映射 I/O 内存、分配缓冲区、注册中断处理程序等。
- 3. 它将设备注册到特定的框架中。

`suspend()` 和 `resume()` 函数用于支持低功耗管理功能的设备。

负责平台的平台驱动程序应通过 `platform_driver_register()` 函数注册到平台核心。在 `module init()` 函数中注册你的平台驱动，并在 `module exit()` 函数中注销它，如下代码段所示：

```c
static int hello_init(void)
{
  pr_info("demo_init enter\n");
  platform_driver_register(&platform_driver);
  pr_info("hello_init exit\n");
  return 0;
}

static void hello_exit(void)
{
  pr_info("demo_exit enter\n");
  platform_driver_unregister(&platform_driver);
  pr_info("demo_exit exit\n");
}

module_init(hello_init);
module_exit(hello_exit);
```

你也可以使用 `module_platform_driver()` 宏。这是一个对于在特殊的 `module_init()`/`exit()` 中不执行特殊操作的驱动的辅助宏。这消除了大量的模板代码。每个模块只能使用此宏一次，调用它会替换 `module_init()` 和 `module_exit()`。

```c
/*
 * module_platform_driver() - 用于那些在 module init/exit 中
 * 不执行特殊操作的驱动的辅助宏。这消除了大量的
 * 模板代码。每个模块只能使用此宏一次，且
 * 调用它会替换 module_init() 和 module_exit()
 */
#define module_platform_driver(__platform_driver) \
    module_driver(__platform_driver, platform_driver_register, platform_driver_unregister)
```

## 实验 5.1: "平台设备" 模块

此平台驱动的功能与杂项驱动（misc driver）相同，但这次你将在 `probe()` 函数而不是 `init()` 函数中注册设备。当内核加载时，平台设备驱动通过 `platform_driver_register()` 函数向平台总线注册自己。当平台设备驱动程序将其其中一个兼容字符字符串（包含在其中一个 `device_id` 结构* 中）与 DT 节点设备的兼容属性值匹配成功时，`probe()` 函数会被调用。将设备与设备关联的过程被称为“绑定（binding）”，在内核源码树的 `include/linux/mod_device.h` 中声明：

```c
/*
 * 用于匹配设备的结构
 */
struct of_device_id {
    char name[32];
    char compatible[128];
    const void *data;
};
```

驱动的主代码现在将是：

- 1. 包含平台设备头文件，该文件包含平台所需的结构：

   `#include <linux/platform.h>`

- 2. 驱动支持的设备列表。创建一个结构数组并初始化其 `compatible` 字段：

```c
static const struct of_device_id my_of_ids[] = {
    { compatible = "hellokeys" },
};
MODULE_DEVICE_TABLE(of, my_of_ids);
```

- 3. 添加注册到平台总线的 `platform_driver` 结构：

```c
static struct platform_driver my_platform_driver = {
    .probe = my_probe,
    .remove = my_remove,
    .driver = {
        .name = "hellokeys",
        .of_match_table = my_of_ids,
        .owner = THIS_MODULE,
    }
};
```

- 加载内核模块后，当发现匹配的设备时，`my_probe()` 将调用。当驱动卸载时，`my_remove()` 将调用。因此，`my_probe()` 承担了 `hello_init()` 函数的角色，`my_remove()` 承担了 `hello_exit()` 函数的角色。所以用 `my_probe()` 替换 `hello_init()` 并用 `my_remove()` 替换 `hello_exit()` 是合理的：

```c
static int __init_my_probe(struct platform_device *pdev)
{
    int ret_val;
    pr_info("my_probe function is called.\n");
    ret_val = misc_register(&helloworld_miscdevice);
    if (ret_val != 0) {
        pr_err("could not register the misc device my_dev\n");
        return ret_val;
    }
    pr_info("my_dev: got minor %i%n", helloworld_miscdevice.minor);
    return 0;
}

static int __exit_my_remove(struct platform_device *pdev)
{
    pr_info("my_remove() function is called.\n");
    misc_deregister(&helloworld_miscdevice);
    return 0;
}
```

- 将你的平台驱动注册到平台总线：

`module_platform_driver(my_platform_driver);`

- 修改设备树文件（位于内核源码树的 `arch/arm/boot/dts/` 中），包含你的 DT 节点。必须有一个与驱动的 `of_device_id` 结构中存储的兼容字符串相同的 DT 节点属性。打开 `bcm2710-rpi-3-b.dts` 文件并在 `soc` 节点中添加 `hellokeys`：

```c
soc {
    virtgpio virtgpio {
        compatible = "bcm2835-virtgpio";
    };
}
```

# 第5 章

## 平台驱动程序

```
gpio-controller;
#gpio-cells = <2>;
firmware = <<firmware>;
status = "okay";

hellockys {
  compatible = "arrow,hellockys";
}
```

- 7. 在 `linux_5.4_rpi3_drivers` 文件夹中创建一个新的修改过的 `hellockys_rpi3.c` 文件，并将 `hellockys_rpi3.0` 添加到你的 Makefile 的 `obj-m` 变量中，然后编译并将模块部署到树莓派：
