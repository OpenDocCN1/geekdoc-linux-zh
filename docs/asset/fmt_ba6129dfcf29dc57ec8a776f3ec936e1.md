
```
root@raspberry:/home/pi# ./ioctl_test
my_dev_open() is called.
my_dev_ioctl() is called. cmd = 100, arg = 110
my_dev_close() is called.
```

移除模块：

# 第 4 章

## 字符驱动

```
root@raspberry:~/home/pi# rmod helloworld_rpi3_class_driver.ko
```

带有参数 `exit` 的 Hello

### 杂字符驱动

`Misc Framework`（杂框架）是 Linux 内核导出的一个接口，允许模块注册各自的次设备号。

作为杂设备实现的设备驱动程序使用 Linux 内核为杂设备分配的主设备号。这消除了为驱动程序定义唯一主设备号的需求；这是重要的，因为主设备号冲突变得越来越可能，而使用杂设备类（`misc device class`）是一种有效的策略。每个探测到的设备都会被动态分配次设备号，并以 sysfs 伪文件系统中 `/sys/class/misc` 下目录条目的形式列出。

主设备号 `10` 正式分配给杂设备驱动。模块可以向杂设备驱动注册单个次设备号并处理小型设备，只需要单一的入口点。

### 注册次设备号

`miscdevice` 结构在内核源码树的 `include/linux/miscdevice.h` 中声明：

```c
struct miscdevice {
  int minor;
  const char *name;
  const struct file_operations *fops;
  struct list_head list;
  struct device *parent;
  struct device *this_device;
  const char *nodename;
  umode_t mode;
};
```

其中：

- `minor` 是正在注册的次设备号。
- `name` 是该设备的名称，可以在 `/proc/misc` 文件中找到。
- `fops` 是指向 `file_operations` 结构的指针。
- `parent` 是指向设备结构的指针，代表由此驱动程序暴露的硬件设备。

杂设备驱动导出两个函数 `misc_register()` 和 `misc_deregister()`，用于注册和注销其所有者的次设备号。这些函数在 `include/linux/miscdevice.h` 中声明，并在内核源码树的 `drivers/char/misc.c` 中定义：

```c
int misc_register(struct miscdevice *misc);
int misc_deregister(struct miscdevice *misc);
```

### 字符驱动

`misc_register()` 函数向内核注册一个杂设备。如果次设备号被设置为 `MISC_DYNAMIC_MINOR`，则会动态分配次设备号并放入 `miscdevice` 结构的 `minor` 字段中。在其他情况下，将使用请求的次设备号。

作为参数传递的结构与键链接，并且在注销之前不会被销毁。默认情况下，对设备文件的 `open()` 调用将 `file-private_data` 指向该结构。成功时返回 `0`，失败时返回负错误码（`errno`）。

分配动态次设备号的典型代码段如下：

```c
static struct miscdevice my_dev;

int init_module(void)
{
    my_dev.minor = MISC_DYNAMIC_MINOR;
    my_dev.name = "my_device";
}
```

```c
#include <linux/module.h>
#include <linux/fs.h>
#include <linux/miscdevice.h>
#include <linux/uaccess.h>
#include <linux/device.h>

static int my_dev_open(struct inode *inode, struct file *file)
{
    printk("my_dev_open() is called.\n");
    return 0;
}

static int my_dev_close(struct inode *inode, struct file *file)
{
    printk("my_dev_close() is called.\n");
    return 0;
}

static long my_dev_ioctl(struct file *file, unsigned int cmd, unsigned long arg)
{
    printk("my_dev_ioctl() is called. cmd = %d, arg = %ld\n", cmd, arg);
    return 0;
}

static const struct file_operations my_fops = {
    owner = THIS_MODULE,
    open = my_dev_open,
    release = my_dev_close,
    unlocked_ioctl = my_dev_ioctl,
};

static struct miscdevice my_miscdevice = {
    minor = MISC_DYNAMIC_MINOR,
    name = "mydev",
    fops = &my_fops,
};

static int __init hello_init(void)
{
    int ret_val;
    printk("Hello world init\n");
    ret_val = misc_register(&my_miscdevice);
    if (ret_val != 0) {
        printk_err("could not register the misc device mydev\n");
        return ret_val;
    }
    return 0;
}

static void __exit hello_exit(void)
{
    printk("Hello world exit\n");
    misc_deregister(&my_miscdevice);
}

module_init(hello_init);
module_exit(hello_exit);
```

## 平台驱动程序 (Platform Drivers)

到目前为止，你一直在构建一个在运行时加载的可加载驱动模块。字符设备驱动已经完成，并已通过用户空间应用程序了充分测试。在下一次作业中，你将字符设备驱动转换为平台驱动程序（`platform driver`）。在嵌入式系统中，设备通常不通过总线连接，因此这些设备不支持枚举和热插拔。

然而，你仍然希望所有这些设备成为设备模型的一部分。这类设备不是通过动态检测，而是必须通过两种不同的方法进行静态描述：

1. **直接实例化** `platform_device` 结构，这在一些未基于设备树的 ARM 平台上很常见。定义位于特定开发板或特定 SoC 的代码中。
2. 使用**设备树（Device Tree）**，这是一种用于某些架构的硬件描述文件。设备驱动与 `.dts` 文件中描述的物理设备匹配。匹配成功后，会调用驱动的 `probe()` 函数。驱动代码中必须包含一个 `of_match_table` 以允许匹配。

在不可自动发现的设备中，有一个巨大的家族是直接属于系统芯片的：UART 控制器、以太网控制器、SPI 控制器、图形或音频设备等。在 Linux 内核中，创建了一个特殊的总线——**平台总线（platform bus）**来处理此类设备。它支持处理平台设备的平台驱动。它的工作方式与其他任何总线（如 USB、PCI）类似，但设备是静态枚举的，而不是动态发现的。

每个平台驱动程序负责实例化并注册一个 `platform_driver` 结构实例。平台驱动遵循标准的驱动模型约定，其中发现/枚举在驱动外部处理，而驱动提供 `probe()` 和 `remove()` 方法。平台驱动使用标准约定支持电源管理和关机通知。`platform_driver` 结构最重要的成员所示所示：
