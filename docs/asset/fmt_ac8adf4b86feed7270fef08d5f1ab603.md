
考虑内核的 I²C 子系统（在第 8 章“I²C 协议”中探讨）。I²C 层由核心基础设施、总线适配器设备驱动程序和客户机设备驱动程序组成。I²C 核心层使用 `bus_register()` 注册每个检测到的 I²C 总线适配器。当探测并检测到 I²C 客户机设备（例如，*电可擦除可编程只读存储器* [EEPROM] 芯片）时，通过 `device_register()` 记录其存在。最后，I²C EEPROM 客户机驱动程序使用 `driver_register()` 注册自身。这些注册通过 I²C 核心提供的服务函数间接完成。

`bus_register()` 在 `/sys/bus/` 中添加相应条目，而 `device_register()` 在 `/sys/devices/` 下添加条目。`struct bus_type`、`struct device` 和 `struct device_driver` 分别是总线、设备和驱动程序使用的主要数据结构。请查看 `include/linux/device.h` 了解它们的定义。

## 热插拔与冷插拔

连接到正在运行的系统上的设备被称为热插拔，而在系统启动前连接的设备则被视为冷插拔。早期，内核通过调用通过 `/proc` 文件系统注册的辅助程序来通知用户空间热插拔事件。但是，当当前内核检测到热插拔时，它们通过 netlink 套接字将 `uevents` 分发给用户空间。Netlink 套接字是使用套接字 API 在内核空间和用户空间之间进行通信的高效机制。在用户空间端，管理设备节点创建和删除的守护进程 `udevd` 接收 `uevents` 并管理热插拔。

为了查看热插拔处理如何最近演化，让我们考虑运行不同版本 2.6 内核的 udev 的渐进级别：

- 1. 使用 *udev-039* 包和 2.6.9 内核时，当内核检测到热插拔事件时，它调用注册在 `/proc/sys/kernel/hotplug` 的用户空间辅助程序。这默认为 `/sbin/hotplug`，它在其环境中接收热插拔设备的属性。`/sbin/hotplug` 在热插拔配置目录（通常是 `/etc/hotplug.d/default/`）内部查找并运行，例如，在执行 `/etc/hotplug/` 下的其他脚本后运行 `/etc/hotplug.d/default/10-udev.hotplug`。

    ```bash
    bash$ ls -l /etc/hotplug.d/default/
    ...
    lrwxrwxrwx 1 root root 14 May 11 2005 10-udev.hotplug -> /sbin/udevsend
    ...
    ```

    当 `/sbin/udevsend` 如此执行时，它将热插拔设备信息传递给 `udevd`。

- 2. 使用 udev-058 和 2.6.11 内核时，情况略有不同。`udevsend` 实用程序取代了 `/sbin/hotplug`：

    ```bash
    bash$ cat /proc/sys/kernel/hotplug
    /sbin/udevsend
    ```

- 3. 使用最新版本的 udev 和内核，`udevd` 完全负责管理热插拔，而不依赖于 `udevsend`。它现在通过 netlink 套接字直接从内核拉取热插拔事件（见图 4.4）。`/proc/sys/kernel/hotplug` 包含空内容：

    ```bash
    bash$ cat /proc/sys/kernel/hotplug
    bash$
    ```

Udev 也处理冷插拔。因为 udev 是用户空间的一部分，并且仅在内核启动后启动，所以需要一种特殊机制来模拟冷插拔设备的热插拔事件。在启动时，内核为所有设备在 `sysfs` 下创建一个名为 `uevent` 的文件，并向这些文件发出冷插拔事件。当 `udev` 启动时，它从 `/sys` 读取所有 `uevent` 文件，并为每个冷插拔设备生成热插拔事件。

## 微码下载

在某些设备准备好工作之前，必须向它们提供微码。微码由板载微控制器执行。设备驱动程序过去将微码存储在头文件中的静态数组中。但这变得不可行，因为微码通常由设备制造商作为专有二进制映像分发，这与 GPL 许可的内核混并不相容。反对将固件与内核源代码混合的另一个原因是它们运行在不同的发布时间线上。显然的解决方案是在用户空间中单独维护微码，并在需要时将其传递给内核。Sysfs 和 udev 提供了实现这一点的架构。

让我们以在多台笔记本电脑上找到的 Intel PRO/Wireless 2100 WiFi mini PCI 卡为例。该卡围绕一个微控制器构建，该微控制器需要执行外部提供的微码才能正常运行。让我们逐步了解 Linux 驱动程序向卡下载微码的步骤。假设您已从 `http://ipw2100.sourceforge.net/firmware.php` 获取所需的微代码映像（`ipw2100-1.3.fw`）并将其保存在系统的 `/lib/firmware/` 下，并且您已经插入了驱动程序模块 `ipw2100.ko`。

- 1. 在初始化期间，驱动程序调用以下命令：

    ```
    request_firmware(..., "ipw2100-1.3.fw", ...);
    ```

- 2. 这将向用户空间分发一个热插拔 `uevent`，并附带所请求的微代码映像的身份信息。

- 3. `udevd` 接收 `uevent` 并通过调用 `/sbin/firmware_helper` 进行响应。为此，它使用 `/etc/udev/rules.d/` 下文件中的类似以下规则的规则：

    ```
    ACTION=="add", SUBSYSTEM=="firmware", RUN="/sbin/firmware_helper"
    ```

- 4. `/sbin/firmware_helper` 在 `/lib/firmware/` 内部查找并定位所请求的微代码映像 `ipw2100-1.3.fw`。它将映像转储到 `/sys/class/0000:02:02.0/data`。（在这种情况下，`0000:02:02` 是 WiFi 卡的 PCI 总线:设备:功能标识符。）

- 5. 驱动程序接收微码并将其下载到设备。完成后，它调用 `release_firmware()` 以释放相应的数据结构。

- 6. 驱动程序完成其余的初始化过程，WiFi 适配器开始信标传输。

## 模块自动加载

按需自动加载内核模块是 Linux 支持的一个方便功能。为了理解内核如何发出“模块故障”以及 udev 如何处理它，让我们将一个 Xircom CardBus 以太网适配器插入笔记本电脑的 PC 卡插槽中。

1. 在编译时，所支持设备的标识作为驱动模块对象的一部分生成。请查看支持 Xircom CardBus 以太网组合卡的驱动（`drivers/net/tulip/xircom_cb.c`），你会找到这段代码：

```
static struct pci_device_id xircom_pci_table[] = { {0x115D, 0x0003, PCI_ANY_ID, PCI_ANY_ID,}, {0,},};
/* Mark the device table */
MODULE_DEVICE_TABLE(pci, xircom_pci_table);
```

这声明了该驱动可以支持任何 PCI 供应商 ID 为 `0x115D` 且 PCI 设备 ID 为 `0x0003` 的卡（关于此点的更多细节参见第 10 章）。当安装驱动模块时，`depmod` 实用程序会查看模块映像内部，解读设备表中存在的 ID。然后，它会将以下条目添加到 `/lib/modules/kernel-version/modules.alias` 中：

```
alias pci:v0000115Dd00000003sv*sd*bc*sc*i* xircom_cb
```

其中 `v` 代表 VendorID（供应商 ID），`d` 代表 DeviceID（设备 ID），`sv` 代表 subvendorID（子供应商 ID），`*` 代表通配符匹配。

2. 当将 Xircom 卡热插拔到 CardBus 插槽时，内核生成一个 `uevent`，宣布新插入设备的标识。你可以使用 `udevmonitor` 查看生成的 `uevent`：

```
bash> udevmonitor --env
...
MODALIAS=pci:v0000115Dd00000003sv0000115Dsd00001181bc02sc00i00
...
```

3. `udevd` 通过 netlink 套接字接收该 `uevent`，并调用 `modprobe` 执行内核向上层传递的上述 MODALIAS：

```
modprobe pci:v0000115Dd00000003sv0000115Dsd00001181bc02sc00i00
```
