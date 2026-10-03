
> （注意，旧版本的 udev 使用单独的命令，如 `udevmonitor` 或 `udevtrigger`。新版本已将这些工具整合到一个管理程序 `udevadm` 中，如下所示。如果无法识别此命令，请检查你正在运行的版本。）

列表 19-1 典型 uevent：USB 设备

```
KERNEL[1244031028.077331] add /dev/platform/musb_hdrc/usb1/1-1 (usb)
ACTION=add
DEVPATH=/dev/platform/musb_hdrc/usb1/1-1
SUBSYSTEM=usb
TYPE=usb_device
DEVICE=/proc/bus/usb/001/002
PRODUCT=5ec3/608/702
TYPE=9/0/1
BUSNUM=001
DEVNUM=002
SEQNUM=1
MAJOR=189
MINOR=1
```

1. 你可以在 <http://en.wikipedia.org/wiki/Netlink> 了解更多关于 netlink 套接字的信息。

列表 19-1 显示了在 BeagleBoard 的 USB 端口插入四口集线器时，检测到发射的第一个内核 uevent 属性。第一行表示该 uevent 是一个“add”（添加）操作，意味着内核检测到了该 USB 设备。其内核名称为 `/devices/platform/musb_hrc/usb1/1-1`。

当内核检测到 uevent 时，它采取的默认操作之一是在 sysfs 文件系统中创建一个项（sysfs 通常始终挂载在 `/sys`）。`DEVPATH` 属性表示它在 `/sys` 目录层次结构中的位置，并在 udev 规则和工具的许多地方被引用。其他属性指示设备类型、设备、产品（厂商和设备 ID）以及关于设备在 USB 总线上的物理层级位置的一些信息。`DEVICE` 属性是内核为该设备节点指定的 ID。该设备在 USB 号 001 上被检测到，并分配了设备号 002。

在列表 19-1 中，产品厂商代码为 `5ec3`，设备 ID 为 `608`。参考 <http://www.linux-usb.org/usb.ids> 维护的列表，厂商 `05ec3` 是 Genes Logic, Inc.，产品 ID `0608` 是一个 USB 2.0 四口集线器。

每个发射的 uevent 序列号都会递增。最后，设备驱动程序的主号和小号也包含在 uevent 中。在本例中，分配了主号 189，小号为 1。

当 udev 接收到 uevent 时，它会扫描其规则数据库（在 19.4 节描述）。udev 寻找与设备属性匹配并规定执行的操作。在没有任何匹配规则的情况下，udev 的默认行为仅仅是使用内核提供的名称创建设备节点，并指定的主号和小号生成如下设备节点（如 `ls -l` 所示）：

```
crw-rw---- 1 root root 189 0 Jun 4 16:37 usdev1
```

udev 中存在规则，允许系统设计人员或发行维护人员应用适用于特定程序的自定义操作。通常，默认规则指定在 `/dev` 中创建相应的设备节点。它们通常还包括创建一个指向此新设备节点的符号链接（symlink），这可能是应用程序访问设备时常用的短名称。我们稍后将查看 udev 规则。

## 19.3 默认 udev 行为

你可能会惊讶地发现，列表 19-1 中详细说明的 uevent 是许多传递的内核 uevent 中的第一个。列表 19-2 详细说明了内核在插入此四口总线时生成的每一个 uevent。该列表是通过以下输入命令生成的：

```
# udevadm monitor --kernel
```

### 列表 19-2 四口集线器上的内核 uevent

| KERNEL add /devices/platform/musb_hdrc/usb1/1-1 (usb) | KERNEL add /devices/platform/musb_hdrc/usb1/1-1:1:0 (usb) | KERNEL add /class/usb_endpoint/usbdev1.2_ep81 (usb_endpoint) | KERNEL add /class/usb_device/usbdev1.2 (usb_device) | KERNEL add /class/usb_endpoint/usbdev1.2_ep00 (usb_endpoint) |

注意，时间戳已被移除并替换为 ts，以适应页面并使其易阅读。每个 uevent 都有像 19-1 中那样的时间戳。你可以看到插入四口集线器产生了五个事件。这些代表了 USB 设备的各个部分，其架构在第 18 章中描述为“通用总线”。

### 列表 19-3 udev 创建的初始设备

```
crw-rw---- 1 root root 189, 0 Jan 02:03 usb1
crw-rw---- 1 root root 189, 0 Jan 02:03 usbdev1.1
crw-rw---- 1 root root 253, 1 Jan 02:03 usbdev1.1_ep00
crw-rw---- 1 root root 253, 0 Jan 02:03 usbdev1.1_ep81
crw-rw---- 1 root root 189, 1 Jan 02:04 usbdev1.2
crw-rw---- 1 root root 253, 3 Jan 02:04 usbdev1.2_ep00
crw-rw---- 1 root root 253, 2 Jan 02:04 usbdev1.2_ep81
```

图 19-1 显示了产生列表 19-3 中设备的硬件配置。

**图 19-1** 四口集线器

列表 19-3 中的第一行代表 BeagleBoard 上的控制器。正如我们在第 18 章中学到的，我们可以通过查看 `/sys` 中的属性看到它。它是 BeagleBoard 上德州仪器 OMAP350 芯片的高速双速率控制器（泛称为 USB 主机）。这是我们使用 `/sys` 检查设备的方法：

```
# cd /sys/devices/platform/musb_hdrc/usb1
# cat idVendor idProduct
1d6b
0002
USB host
```

列表 19-3 中的后续三行代表与控制器始终相关的单口集线器。这是第 18 章中讨论的根集线器。你可以将物理连接器视为该单口集线器。正如第 18 章所讨论的，USB 设备由称为接口和端点的逻辑实体组成。设备节点 `usbdev1.1` 代表 USB 接口，而命名为 `usbdev1.1_ep00` 和 `usbdev1.1_ep01` 的 USB 设备代表跨 USB 总线通信的逻辑端点。

四口集线器插入 BeagleBoard 的 USB 端口后，列表 19-3 中的最后三个设备节点是由 udev 使用其默认行为生成的。注意设备节点的编号，`.2` 代表连接的 USB 集线器层次结构中的第二个集线器。

你可能会想不同的名称可能更好地代表这类设备。如果设备直接供程序使用（例如 USB 鼠标），那么像 `usbdev1.3_ep00` 这样的名称将非常不友好。这就是 udev 规则派上用场的地方。

> 如果你将鼠标直接插入这个四口集线器，它会被命名为这样。

## 19.4 理解 udev 规则

udev 的真正威力来自于它的规则引擎。系统设计人员和发行维护人员使用 udev 规则来组织 `/dev` 层次结构，并为其创建的设备分配用户友好的名称。大多数情况下，会创建一个默认设备名称，并同时创建一个带有用户友好名称的符号链接，将内核名称与用户友好名称相关联。

udev 的规则引擎还可以用于加载设备驱动（模块）。事实上，使用 udev 规则，你可以在检测到设备插入或移除时执行想象的任何操作。然而，udev 规则最常用的用途是设备重命名——创建具有人类可读名称的符号链接以及设备加载。

让我们看一组 udev 用于决定在接收内核事件后采取什么操作的典型规则。在较新版本的 udev 中，udev 规则的默认位置是 `/lib/udev/rules.d`。我们将在后续讨论中使用它作为默认位置。许多发行版将 udev 规则放置在 `/etc/udev/rules.d`。规则文件通常由发行维护人员自定义。它们通常根据功能分组以便于维护。如果你在阅读此内容时坐在 Linux 机器旁，请花点时间浏览它的规则文件。

尽管 udev 查找规则的默认目录是 `/lib/udev/rules.d`，但 udev 也会在 `/etc/udev/rules.d` 中查找同名的覆盖规则文件，允许你覆盖默认规则。

在现代 Linux 发行版中，规则文件共同构成了 udev 发现或移除时要采取的操作映射。我的笔记本发行版包含 31 条规则，拥有近 1400 行代码和近 700 条独立规则！如果你扫描这些规则文件，你就会开始欣赏 udev 的活性和威力。

当 udev 启动时，它会读取 `/lib/udev/rules.d` 中的所有规则，当发现设备时，udev 将内核传递的设备和属性与其维护的全局规则表进行匹配。当找到匹配项时，就会执行 udev（或规则）决定的操作。让我们来看一个例子。

继续之前的 BeagleBoard 示例，看看把一个普通鼠标插入 USB 端口时会发生什么。在没有规则的情况下，udev 使用内核提供的原始名称创建设备节点：

这些设备代表了基础的 USB 基础设施。没有创建其他设备。如果你熟悉 Linux 中的输入设备，你可能期望在系统中找到一个名为 `mouse-smoothing`（鼠标平滑）的设备。许多常用应用程序都期望找到一个具有此类设备名称的鼠标。此外，没有加载设备驱动程序来处理新插入的模块。在配置恰当的桌面系统中，假设使用了现代且运行良好的 Linux 发行版，你将找到一个具有通用名称（如 `mouse*`）的设备，并且你预期输入设备驱动程序和鼠标驱动已经加载。

回想第 8 章，我们可以使用 `lsmod` 命令检查加载了哪些模块：

```
evenroot@beagle:~# lsmod
Module      Size Used by
musb_hdrc  36352 0
usbcore     143324 2 musb_hdrc
```

记住，这是一个没有 `udev` 设备的精简版系统。目前只加载了主机控制器驱动（`musb_hdrc`）和 USB 核心子系统（`usbcore`），它们是为了这部分手动加载的。我们稍后会看到 udev 可以自动加载这些平台驱动程序。这里有趣的点是，没有加载任何处理鼠标（输入）设备的设备驱动程序！

现在让我们为 udev 添加一些规则，如列表 19-4 所示。

### 列表 19-4 简单的 udev 规则

```
DRIVER="*", (MODALIAS)="" RUN="/sbin/modprobe %b"
KERNEL="mouse|*", NAME="input/%k", MODE="0640"
```

这两个规则放置在 `/lib/udev/rules.d` 中以 `.rules` 结尾的随机文件中。第一条规则包含了加载驱动程序的“魔法”：如果 `DRIVER` 属性未设置（表示内核不知道或未提供驱动程序），udev 指令运行 `modprobe` 程序，并将 `MODALIAS` 变量的内容传递给它。稍后我们将检查 `MODALIAS`，但目前假设你正在处理一个动态加载设备驱动的系统。在生产环境中，我们可能会对这些规则文件施加更合理的结构。

### 19.4.1 Modalias

当检测到设备时（我们在这里使用的示例 USB 鼠标），内核会发送一系列事件报告设备的添加。列表 19-7 详细列出了 USB 鼠标插入 USB 端口时的内核事件。列表 19-7 是使用以下命令生成的：

```
# udevadm monitor --kernel
```

#### 列表 19-7 USB 插入内核事件

```
KERNEL add /devices/platform/musb_hdrc/usb1/1-1 (usb)
KERNEL add /devices/platform/musb_hdrc/usb1/1-1:1.0 (usb)
KERNEL add /class/endpoint/usbdevv1.2_ep1 (usb_endpoint)
KERNEL add /class/usb_device/usbdevv1.2 (usb_device)
KERNEL add /class/endpoint/usbdevv1.2_ep0 (usb_endpoint)
KERNEL add /module/hid (module)
KERNEL add /bus/hid (bus)
KERNEL add /module/mousehid (module)
KERNEL add /bus/hid/generic-usb (drivers)
KERNEL add /devices/platform/musb_hdrc/usb1/1-1/1.0/0003:047D:1035:0001 (hid)
KERNEL add /class/input/mouse0 (input)
KERNEL add /bus/hid/generic-usb (drivers)
KERNEL add /module/mousehid (module)
KERNEL add /class/input/event0 (input)
KERNEL add /class/input/mice (input)
```

列表 19-7 详细列出了 USB 鼠标插入时的内核事件。
