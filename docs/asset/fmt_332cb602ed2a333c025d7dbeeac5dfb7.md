
```bash
~ gedit ~/my-linux-imx/drivers/char/Kconfig
```

在文件末尾 `endmenu` 之上添加以下行：

```text
config HELLOWWORLD
	label "My simple helloworld driver"
	default y
```

编辑 `~/my-linux-imx/drivers/char/Makefile`：

```bash
~ sudo gedit ~/my-linux-imx/drivers/char/Makefile
```

在 `Makefile` 的末尾添加以下行：

```makefile
obj-$(CONFIG_HELLO) += helloworld_char_driver.o
```

现在你已经修改了 `Kconfig` 和 `Makefile`，将 `helloworld_char_driver` 作为内核的一部分而不是加载模块，继续构建内核。打开 `menuconfig` 窗口。从主菜单 -> Device Drivers -> My simple helloworld driver。按一次 `<space>` 使新配置中出现 `<*>` 如下所示。按 `<Exit>` 直退出 `menuconfig` 并记得保存新配置。

```bash
~/my-linux-imx$ make menuconfig ARCH=arm
```

![](img/739a35b59067f8a55eff80a58765146f_137_0.png)

```text
< IOMEM HW Random Generator support
< Atmel Random Number Generator support
< Freescale RNG Random Generator support
< Genics HW random generator support
< RAW driver (/dev/raw)
< Hardware Support
  * my simple helloworld driver
  [*] IMX test driver
```

```text
 <Select>  < Save >  < Load >
```

打开内核根目录下的 `.config` 文件将显示已添加了 `CONFIG_HELLO` 符号。

编译新镜像并拷贝到 `tftp` 文件夹：

```bash
~/my-linux-imx$ source /opt/linux/environment-setup-cortex9hf-vfp-neon-linux-gnueabi
~/my-linux-imx$ make zImage
~/my-linux-imx$ cp /arch/arm/boot/zImage /var/lib/tftp
```

打开 `minicom` 并执行网络启动。按下 SABRE 上的 `RESET SW2` 开始启动序列。按任意键跳过 U-Boot 序列。不需要像之前一层那样加载内核模块。

```bash
root@imx6qsabresd:~# cat /proc/devices /* 注册了 202 "my_char_device" */
root@imx6qsabresd:~# mknod /dev/mydev c 202 0 /* 分配设备号
root@imx6qsabresd:~# ./ioctl_test /* 运行 ioctl_test 应用程序 */
```

# 使用 devtmp 创建设备文件

在 Linux 2.6.32 之前，在基础 Linux 系统上，必须使用 `mknod` 命令手动创建设备文件。设备文件与内核处理的设备之间的一致性由系统开发者负责。随着 2.6 系列稳定内核的出现，出现了一个名为 `sysfs` 的新虚拟文件系统。`sysfs` 的工作是将硬件配置视图导出给用户空间进程。

你可能会好奇 `sysfs` 如何知道系统上的设备以及应该为它们使用什么设备号。编译进内核的驱动在被内核检测时直接向 `sysfs` 注册其对象。对于编译为模块的驱动，这种注册将在模块加载时发生。一旦挂载 `sysfs` 文件系统（位于 `/sys`），驱动向 `sysfs` 注册的数据即可供用户空间进程使用（包括对设备节点的修改）。内核使用 `sysfs` 将设备节点导出到用户空间供 `udev` 使用。

设备文件由内核通过 `devtmpmps` 文件系统创建。任何想要注册设备节点的驱动都通过 `devtmpmps`（通过核心驱动）来实现。当 `devtmpmps` 实例挂载到 `/dev` 时，设备节点最初以固定的名称、权限和所有者创建。所有设备节点都属于 `root` 且默认模式为 `0600`。

不久后，内核会发送 `udevd`。根据 `/etc/udev/rules.d`、` /lib/udev/rules.d` 和 `/run/udev/rules.d` 目录下的文件，`udev` 会为设备节点创建额外的符号链接，或者更改其权限、所有者或组，或者修改该对象的 `udev` 数据库条目（名称）。

# 实验 4.2: “字符类”模块

![](img/739a35b59067f8a55eff80a58765146f_139_0.png)

在这个内核模块实验中，你将使用之前写的 `helloworld_char_driver` 作为起点，但这次设备节点将使用 `devtmpfs` 创建，而不是手动创建。

在下一章的“为平台驱动程序添加 Sysfs 支持”节中，将详细介绍在 `/sys/class` 下创建的目录。在你当前的驱动程序中，你将向 `/sys/class` 目录添加一个条目。`/sys/class` 目录提供了按类分组的设备驱动视图。

当 `register_chdev_region()` 通知内核存在具有特定主号的驱动程序时，它并没有指定驱动程序的类型，因此它不会在 `/sys/class` 下创建条目。这个条目是必要的，以便 `devtmpfs` 可以在 `/dev` 下创建设备节点。对于每个创建的设备，驱动程序在 `/sys` 下有一个类名设备名。

驱动程序使用以下内核 API 创建类：

- `class_create()` 在 `/sys/class/class` 目录下创建一个类。
- `class_destroy()` 移除该类。

驱动程序使用以下内核 API 创建设备节点：

- `device_create()` 在 `/dev` 目录下创建一个设备节点。
- `device_destroy()` 移除 `/dev` 目录下的设备节点。

现在将描述与你之前的 `helloworld_char_driver` 不同的主要要点：

1. 包含以下头文件以创建类和设备文件：

```
#include <linux/device.h> /* class_create(), device_create() */
```

2. 你的驱动程序将有一个类名和一个设备名；使用 `"hello_class"` 作为类名，`"mydev"` 作为设备名。这导致在文件系统中 `/sys/hello_class/mydev` 处创建一个设备。为设备名和类名添加以下定义：

```
#define DEVICE_NAME "mydev"
#define CLASS_NAME "hello_class"
```

3. `hello_init()` 函数比在 `helloworld_char_driver` 中写的要长。这是因为现在它使用 `alloc_chrdev_region()` 函数为设备分配主号，同时注册了设备类并创建了设备节点。

```
static int __init hello_init(void)
{
    /* 分配动态设备号 */
    ret = alloc_chrdev_region(&dev_no, 0, 1, DEVICE_NAME);
    Major = MAJOR(dev_no);
    dev = MKDEV(Major,0);
    /* 初始化 cdev 结构 */
    /* 并将其添加到内核空间 */
    cdev_init(&my_dev, &my_dev_fops);
    ret = cdev_add(&my_dev, dev, 1);

    /* 注册设备类 */
    helloClass = class_create(THIS_MODULE, CLASS_NAME);

    /* 创建设备并将其注册到 sysfs */
    helloDevice = device_create(helloClass, NULL, dev, NULL,
                                 DEVICE_NAME);

    return 0;
}
```

# 列表 4-4: helloworld_class_driver.c

```
#include <linux/module.h>
#include <linux/fs.h>
#include <linux/device.h>
#include <linux/cdev.h>
```

```
#define DEVICE_NAME "mydev"
#define CLASS_NAME "hello_class"
```
