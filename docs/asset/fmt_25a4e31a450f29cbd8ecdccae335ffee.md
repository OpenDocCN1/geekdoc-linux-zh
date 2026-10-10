
  第一条规则告诉 `udev`，每当它找到一个产品 ID 为 `0x0701`、供应商 ID 为 `0x05e3` 且名称以 `sr` 开头的 USB 设备时，它应该在 `/dev` 下创建一个同名节点，并创建一个名为 `usbdvd` 的符号链接指向该创建的节点。同样，第二条规则指示为 CD-RW 驱动器创建一个名为 `usbcdrw` 的符号链接。

  为了测试规则中的语法错误，在 `/sys/block/sr*` 上运行 `udevtest`。为了在 `/var/log/messages` 中开启详细消息，在 `/etc/udev/udev.conf` 中将 `udev_log` 设置为 "yes"。为了实时用新添加的规则重新填充 `/dev` 目录，使用 `udevstart` 重启 `udev`。完成后，你的 DVD 驱动器在系统中始终显示为 `/dev/usbdvd`，而你的 CD-RW 驱动器始终显示为 `/dev/usbcdrw`。你可以使用如下命令从 shell 脚本中确定性地挂载它们：

```
mount /dev/usbdvd /mnt/dvd
```

  设备节点（以及网络接口）的一致命名并不是 `udev` 的唯一能力。它也已经转变为 Linux 热插拔管理器。`Udev` 还负责按需自动加载模块以及向需要它们的设备下载微代码。但在深入探讨这些功能之前，让我们先对设备模型的内部结构有一个基本的了解。

## Sysfs、Kobjects 和设备类

  `Sysfs`、`kobjects` 和设备类是设备模型的构建模块，但它们性格内向，喜欢留在幕后。它们主要属于总线和核心实现的使用领域，隐藏在为设备驱动程序提供服务的 API 内部。

  `Sysfs` 是内核结构化设备模型在用户空间的体现。它类似于 `/procfs`，因为两者都是包含内核数据结构信息的内存文件系统。虽然 `/procfs` 是查看内核内部机制的通用窗口，但 `sysfs` 专门针对设备模型。因此，`sysfs` 并不是 `/procfs` 的替代品。诸如进程描述符和 `sysctl` 参数等信息属于 `/procfs` 而不是 `sysfs`。很快大家就会明白，`udev` 依赖于 `sysfs` 来实现其大部分扩展功能。

  对象引入了对常见对象属性（如使用引用计数）的封装。它们通常嵌入在更大的结构中。以下是 `kobject` 的主要字段，其定义在 `include/linux/kobject.h` 中：

- 1. 一个 `kref` 对象，用于执行引用计数管理。`kref_init()` 接口初始化 `kref`，`kref_get()` 增加与 `kref` 关联的引用计数，而 `kref_put()` 减少引用计数，如果没有剩余的引用则释放对象。例如，`URB` 结构（在“通用串行总线”第 11 章中解释）包含一个 `kref` 来跟踪对它的引用数量。[2]

- 2. 指向 `kset` 的指针，`kset` 是 `kobject` 所属的对象集合。

- 3. 一个 `kobj_type`，它是描述 `kobject` 的对象类型。

  `Kobjects` 与 `sysfs` 紧密交织。在内核中实例化的每个 `kobject` 都有一个 `sysfs` 表示。

  设备类的概念是设备模型的另一项特性，也是你在驱动程序中更可能使用的接口。类接口抽象了这样一种理念：每个设备都属于更广泛的设备类（或类别）。USB 鼠标、PS/2 键盘和摇杆都属于 `input` 类，并在 `/sys/class/input/` 下拥有条目。

  图 4.4 显示了一台连接了外部 USB 鼠标的笔记本电脑上的 `sysfs` 层次结构。顶层的 `bus`、`class` 和 `device` 目录被展开，以显示 `sysfs` 根据 USB 鼠标的设备类型及其物理连接提供的视图。鼠标是一个输入类设备，但在物理上是一个响应两个端点地址的 USB 设备，即控制端点 `ep00` 和中断端点 `ep81`。相关的 USB 端口属于总线 2 上的 USB 主机控制器，而 USB 主机控制器本身通过 PCI 总线桥接到 CPU。如果这些细节在这一点上意义不大，不用担心；在阅读讲解输入驱动程序（第 7 章）、PCI 驱动程序（第 10 章，“外围组件互连”）和 USB 驱动程序（第 11 章）的章节后，再回顾这一节。

### 图 4.4. USB 鼠标的 Sysfs 层次结构。

## 代码视图

```
/sys
  +block
  -[bus]-[sb]-[devices]-[usb2]-[2-2]-[2-2:1.0]-[usbendpoint:usbdev2,2-ep81]
  -[class]-[input]-[mouse2]-[devic2]-[bus]-[usbendpoint:usbdev2,2-ep81]
      -[usb_device]-[usbdev2]-[device]-[bus]
      -[usb_endpoint]-[usbdev2,2-ep00]-[device]
          -[usbdev2,2-ep81]-[device]
  -[devices]-[pci0000:00]-[0000:00:1d:11]-[usb2]-[2-2]-[2-2:1.0]
  +[firmware]
  +[fs]
  +[kernel]
  +[module]
  +[power]
```

浏览 `/sys`，寻找与其他设备（例如您的网卡）相关联的条目，以更好地理解其分层组织。第 10 章中“寻址与标识”一节展示了 `sysfs` 如何映射笔记本电脑上 CardBus 以太网调制解调器卡的物理连接。

类编程接口建立在 `kobjects` 和 `sysfs` 之上，因此它是深入理解设备模型各组件之间端到端交互的好起点。让我们以 RTC 驱动程序为例。RTC 驱动程序（`drivers/char/rtc.c`）是一个杂项（或“misc”）驱动程序。我们将在第 5 章讨论字符设备驱动程序时详细介绍杂项驱动程序。

插入 RTC 驱动程序模块，查看在 `/sys` 和 `/dev` 下创建的节点：

```
bash> modprobe rtc
bash> ls -lR /sys/class/misc
drwxr-xr-x 2 root root 0 Jan 15 01:23 rtc
/sys/class/misc/rtc:
total 0
-rw-r--r-- 1 root root 4096 Jan 15 01:23 dev
-w------- 1 root root 4096 Jan 15 01:23 uevent
bash> ls -l /dev/rtc
crw-r--r-- 1 root root 10, 135 Jan 15 01:23 /dev/rtc
```

`/sys/class/misc/rtc/dev` 包含分配给该设备的主设备号和次设备号（将在下一章讨论），`/sys/class/misc/rtc/uevent` 用于冷插拔（将在下一节讨论），而 `/dev/rtc` 供应用程序访问 RTC 驱动程序使用。

让我们理解通过设备模型的代码流程。杂项驱动程序在初始化期间利用 `misc_register()` 的服务，如果剥离一些代码，它看起来像这样：

```c
/* ... */
dev = MKDEV(MISC_MAJOR, misc->minor);

misc->class = class_device_create(misc_class, NULL, dev,
                                  misc->dev,
                                  "%s", misc->dev,
                                  "%s", misc->name);
if (IS_ERR(misc->class)) {
    err = PTR_ERR(misc->class);
    goto out;
}
/* ... */
```

图 4.5 继续剥离更多层，以揭示设备建模的底层。它展示了波及类、`kobjects`、`sysfs` 和 `udev` 的转换，从而生成前面列出的 `/sys` 和 `/dev` 文件。

### 图 4.5. 将设备模型的各部分联系起来。

![](img/07cc6f9c8c74622020874f66bfb53dc4_109_0.png)

请参见并行端口 LED 驱动程序（第 5 章“与并行端口通信”一节中的清单 5.6）和虚拟鼠标输入驱动程序（第 7 章“设备示例：虚拟鼠标”一节中的清单 7.2），以了解在 `sysfs` 内创建设备控制文件的示例。

设备模型的另一部分抽象是 `bus-device-driver`（总线-设备-驱动程序）编程接口。内核设备支持被清晰地结构化为总线、设备和驱动程序。这使得单个驱动程序实现更简单且更具通用性。例如，*总线* 实现可以搜索能够处理特定设备的驱动程序。
