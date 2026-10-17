
- 它们与设备树（Device Tree）配合工作。设备的设备树节点需要在其 `compatible` 属性中使用 `"generic-uio"`。

- UIO 平台设备驱动通过设备树进行配置并注册一个 UIO 设备。

![](img/739a35b59067f8a55eff80a58765146f_210_0.png)

UIO 平台设备驱动可以被用户提供的内核驱动所替换。内核空间驱动是一个从设备树配置的平台驱动，它在 `probe()` 函数中注册 UIO 设备。设备的设备树节点可以在 `compatible` 属性中使用任何你想要的内容，因为就像任何其他平台设备驱动一样，它只需要与内核空间驱动中使用的 `compatible` 字符串匹配。用户提供的内核驱动可以处理中断，然后通过共享内存等其他机制与用户空间驱动通信数据。

## 平台驱动

![](img/739a35b59067f8a55eff80a58765146f_211_0.png)

UIO 驱动必须在内核中启用。使用一个没有 source 过 `environment-setup-cortexa9hf-vfp-neon-poky-gnueabi` 的终端并打开 `menuconfig` 窗口。导航至 **main menu** -> **Device Drivers** -> **Userspace I/O drivers**。按一次`<spacebar>` 键，直到新配置旁边出现一个 `*`，如下图所示。连续按`<Exit>` 直到退出 menuconfig GUI 界面，并保存新配置。

```
~/my-linux-imx$ make menuconfig ARCH=arm
```

![](img/739a35b59067f8a55eff80a58765146f_211_1.png)

编译新镜像并将其拷贝到 ttfp 文件夹：

```
~/my-linux-imx$ source /opt/poky/1.7/environment-setup-cortexa9hf-vfp-neon-poky-linux-gnueabi
~/my-linux-imx$ make zImage
~/my-linux-imx$ cp /arch/arm/boot/zImage /var/lib/tfpboot
```

## UIO 如何工作

每个 UIO 设备都通过一个设备文件和若干 sysfs 属性文件访问。第一个设备的设备文件名为 `/dev/uio0`，后续设备依次为 `/dev/uio1`、`/dev/uio2` 等。

内核中的 UIO 驱动在 sysfs 系统中创建描述 UIO 设备的属性。`/sys/class/uio` 目录是所有属性的根目录。在 `/sys/class/uio` 下为每个 UIO 设备创建一个独立的编号目录：

1. 第一个 UIO 设备：`/sys/class/uio/uio0`。
2. `/sys/class/uio/uio0/name` 包含设备名称，该名称与 `uio_info` 结构中的名称对应。
3. `/sys/class/uio/uio0/maps` 是一个包含设备所有内存范围的目录。每个 UIO 设备可以有自己的目录或多个可用于内存映射的内存区域。每个映射在 sysfs 中都有自己的目录，第一个映射显示为 `/sys/class/uio/uio/maps/map0/`。随后的映射会创建 `map1/`、`map2/` 等目录。只有当映射大小不为 0 时，这些目录才会出现。每个 `mapX/` 目录包含四个只读文件，显示内存的属性：
   - `name`：此映射的字符串标识符。这是可选的，可以将字符串设置为此值，以便用户空间找到正确的映射。
   - `addr`：可以映射的内存地址。
   - `size`：由 `addr` 指向的内存的大小（单位：字节）。
   - `offset`：在 `mmap()` 返回的指针上可以的偏移偏移（单位：字节），以获取实际设备内存。如果设备内存没有按页对齐，这一点非常重要。

中断通过通过读取 `/dev/uioX` 来处理。对 `/dev/uioX` 进行一个阻塞的 `read()` 会在发生中断时立即返回。你也可以在 `/dev/uioX` 上使用 `select()` 来等待中断。从 `/dev/uioX` 读取的整数值代表总中断计数。你可以用此来判断是否漏掉了中断。设备内存通过调用 UIO 的 `mmap()` 函数映射到进程地址空间中。

## 内核 UIO API

UIO API 既小又易于使用：

1. `uio_info` 结构体向框架提供了驱动的详细信息。某些成员是强制的，另一些是可选的。以下是 `uio_info` 的成员：
   - `const char *name`：强制性。你的驱动在 sysfs 中显示的名称。建议使用模块名称作为此值。
   - `const char *version`：强制性。此字符串出现在 `/sys/class/uio/uioX/version`。
   - `struct uio_mem mem[MAX_UIO_MAPS]`：如果你有可以被 `mmap()` 映射的内存，则是强制性的。详情见下文描述。
   - `long irq`：强制性。如果你的硬件产生中断，则需要此项。
   - `unsigned long irq_flags`：如果你通过其他方式触发中断，则需要此项。
   - `int (*mmap)(struct uio_info *info, struct vm_area_struct *vma)`：可选。如果你需要自定义 `mmap()`，则会调用默认的实现。
   - `int (*open)(struct uio_info *info, struct inode *inode)`：可选。如果你需要自定义 `open()`，则会调用此函数。
   - `int (*release)(struct uio_info *info, struct inode *inode)`：可选。如果你需要自定义 `release()`，则可以使用此函数。
   - `int (*ioctl)(struct uio_info *info, int32 irq_on)`：可选。如果你需要通过写入 `/dev/uio` 来启用或禁用中断，可以实现此函数。参数 `irq_on` 为 0 表示禁用，1 表示启用。

你的设备具有可以映射到用户空间的内存区域。对于每个区域，你必须设置 `mem[]` 数组。以下是 `uio_mem` 字段的描述：
   - `int type`：如果你使用了映射，则是强制性的。如果是物理内存，设置 `UIO_MEM_PHYS`。对于逻辑内存（例如通过 `kmalloc()` 分配），使用 `UIO_MEM_LOGICAL`。对于虚拟内存使用 `UIO_MEM_VIRTUAL`。
   - `unsigned long addr`：使用了映射，则是强制性的。填充内存块的地址。该地址出现在 sysfs 中。
   - `unsigned long size`：填充 `addr` 指向的内存的大小。如果大小为 0，则该映射被视为未使用。注意，对于未使用的映射必须将 size 初始化为零。
   - `void *internal_addr`：如果你需要在内核模块内部访问此内存，可以使用 `ioremap()` 等方法进行内部映射。此返回的地址无法映射到用户空间，因此不要将其存储在 `addr` 中。请使用 `internal_addr` 来记录此类地址。

2. `uio_register_device()` 函数将驱动连接到 UIO 框架：
   - 需要一个 `struct uio_info` 输入。
   - 通常在平台驱动的 `probe()` 函数中调用。
   - 它创建设备文件（从0 开始）以及所有相关的 sysfs 文件属性。
   - `uio_unregister_device()` 函数将驱动从 UIO 框架断开并删除设备文件。

## 实验 5.4：“LED UIO 平台设备模块

![](img/739a35b59067f8a55eff80a58765146f_215_0.png)

在这个内核模块实验中，你将开发一个 UIO 用户空间驱动来控制上一个实验使用的 LED。UIO 驱动的主要功能是将硬件寄存器暴露给用户空间，而在内核空间内不进行控制。该驱动的功能与列表 5-4 中的应用程序 `led_app.c` 类似，但这次 LED 由 UIO 用户空间驱动通过访问内存映射寄存器直接控制。你还将编写内核驱动，从设备树获取参数并使用这些参数初始化 `struct uio_info`。你将在内核驱动的 `probe()` 函数中注册 UIO 设备。

现在描述两个驱动的主要代码部分：

### 用户提供的内核驱动

1. 包含所需的头文件：

```c
#include <linux/io.h> /* devm_ioremap() */
#include <linux/platform_device.h> /* struct platform_get_resource() */
#include <linux/uio_driver.h> /* struct uio_info, uio_register_device(),
uio_unregister_device() */
```

### 第 5 章
