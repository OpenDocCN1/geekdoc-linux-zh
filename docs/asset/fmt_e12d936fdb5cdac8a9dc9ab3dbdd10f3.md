
从前面的宏中，你可以理解数据字段仅包含部分数据。`usmon` 的二进制版本为 `URB` 提供完整信息。然而，这些额外数据大多是特定类别的，针对这些模块的专用数据包分析器比 `usmon` 更有效。例如，针对大存储（mass storage）和 `SCSI` 等类有特定类的数据包监控器。

在对处理 `usmon` `URB` 事件的数据结构有了简要概述后，后续章节将关注 `usmon` 内部的序列流、它如何挂钩信息以及如何与用户空间共享挂钩信息。

## USB 监控器原理

与其他任何模块一样，`usmon` 通过文件系统将 Linux 内核细节扩展到用户空间。由于 `usmon` 模块用于调试，因此它使用了 `debugfs`。

## USB 监控器：usbmon

`usb_mon_operations` 使用 `usbcore` 导出的回调方法。

```c
struct usb_mon_operations {
    void (*submit)(struct usb_bus *bus, struct urb *urb);
    void (*submit_error)(struct usb_bus *bus, struct urb *urb, int err);
    void (*complete)(struct usb_bus *bus, struct urb *urb, int status);
    void (*unlink)(struct usb_bus *bus, struct urb *urb);
};
```

# 第 18 章 使用 Linux USB 进行调试

![](img/779a74a6577501a55983f193067274a3_280_0.png)

**图 18.5** `usmon` 的 `URB` 挂钩序列。

`usbcore` 在 `urb.c` 中使用 `usb_submit_urb`。在更新 `URB` 结构以包含额外信息后，`URB` 被传递给 `usbcore` 的 `hcd.c`。现在 `URB` 已完成，并准备好通过 `usb_hcd_submit_urb` 函数提交给主机控制器驱动。一旦 `URB` 到达 `usb_hcd_submit_urb`，就会调用包装器 `usbmon_urb_submit`。如果 `usmon` 注册了它的回调接口，包装器将带有 `URB` 信息调用回调函数。

`usmon` 模块会根据 `usbcore` 中可用的 USB 总线数量创建对应文件。文本模式会根据总线编号创建两个带有后缀 `u` 或 `t` 的文件。以 `t` 后缀的文件是已弃用的版本，而 `u` 后缀的文件包含更多细节，例如等时事务。你需要挂载 `usmon` VFS 来查看这些文件，如下一节“如何使用 `usmon`”所解释的那样。

`usmon` 为用户扩展了三个主要文件操作：`open`、`read` 和 `release`，以便用户获取内核部分捕获的 `URB` 数据。

图 18.6 展示了当用户空间与 `usmon` 模块交互时发生的动作序列。从图中可以推断，用户空间应用程序打开一个 `usmon` 文件（可能是 `0u`），此时内部注册的打开文件操作（`mon_text_open`）被调用。操作处理句程序使用 `mon_reader_add` 为 `usmon` 添加了文本读取器回调。这开始了在 `struct read` 操作中排队后续 `URB` 活动的过程，随后从用户空间应用程序中出队（dequeues）`URB` 活动并将其呈现给用户应用程序。当 `URB` 事件列表为空时，用户应用程序进程被添加到等待队列中，直到下一次 `URB` 事务发生。到为止，之前的章节重点关注了 `usmon` 如何与其他模块交互。接下来的章节将探索如何使用 `usmon` 来捕获 USB 事务。

![](img/779a74a6577501a55983f193067274a3_281_0.png)

**图 18.6** `usmon` 与用户空间应用程序之间的交互序列。

# 如何使用 usmon

`usmon` 模块负责在初始化期间设置 USB 调试框架的根目录。它使用 `debugfs` 基础设施为 `usmon` 初始化框架。`usmon` 文件相对于其根路径。当你挂载 `debugfs` 时（例如在 `/sys/kernel/debug` 中），`usmon` 文件可能位于 `/sys/kernel/debug/usmon/` 目录下。因此，为了让 `usmon` 正常工作，构建内核时需要包含 `debugfs` 模块。

因此，你需要挂载 `debugfs` 文件系统来查看 `usmon` 文件。通常，它被挂载到 `/sys/kernel/debug`。以下终端活动显示了在加载 `usmon` 模块之前如何挂载 `debug` 文件系统及其初始目录内容。

```
root@rajaram-laptop:~# mount -t debugfs none_debugs /sys/kernel/debug
root@rajaram-laptop:~# cd /sys/kernel/debug/
root@rajaram-laptop:~# ls /sys/kernel/debug#
kprobes
root@rajaram-laptop:~# /sys/kernel/debug#
```

在确保成功挂载 `debug` 文件系统后，你就可以将 `usmon` 模块插入内核了。在成功 `modprobe usmon` 后，该模块会为内核注册的每个 USB 总线创建 `usmon` 文件。以下终端活动显示了成功插入 `usmon` 模块后 `usmon` 目录的内容。

```
root@rajaram-laptop:/sys/kernel/debug# modprobe usmon
root@rajaram-laptop:/sys/kernel/debug# cd usmon/
root@rajaram-laptop:/sys/kernel/debug/usmon# ls
0 1s 1u 2t 3s 3u 4t 5s 5u 6t 7s 7u
0u 1t 2s 2u 3t 4s 4u 5u 6s 6u 7t
root@rajaram-laptop:/sys/kernel/debug#
```

在 Linux 中，USB 总线编号从 1 开始，`usmon` 创建以总线号为前缀来捕获特定 USB 总线上的 `URB` 事务。`usmon` 还会创建一个以 `0` (`0u`) 前缀的文件来捕获所有总线的 `URB` 事务。要捕获连接设备的事务，你应该知道设备连接到哪个总线。要确定总线连接，你可以使用 `lsusb` 或查看由 `usfs` 导出的设备，通常在 `/proc/bus/usb/devices` 中。在示例设置中，ID 为 `1221:3234` 的设备是有感兴趣的设备，`lsusb` 列出了设备列表以及总线号。

```
root@rajar-laptop:~# lsusb
Bus 007 Device 003: ID 1221:3234
Bus 007 Device 001: ID 0000:0000
Bus 006 Device 002: ID 064e:a103
Bus 006 Device 001: ID 0000:0000
Bus 005 Device 001: ID 0000:0000
Bus 004 Device 001: ID 0000:0000
Bus 003 Device 001: ID 0000:0000
Bus 002 Device 001: ID 0000:0000
Bus 001 Device 001: ID 0000:0000
```

示例连接的设备是连接到 USB 总线 7 的存储设备。要捕获大存储设备的 USB 事务，你可以编写一个简单的应用程序来读取并显示信息，或者使用 `cat` 命令将文件重定向到日志。在下面的终端活动中，感兴趣的设备连接到总线 7 并重定向到 `usmog.txt`。

```
root@rajar-laptop:/sys/kernel/debug#
root@rajar-laptop:/sys/kernel/debug# cat 7u >usmog.txt
root@rajar-laptop:/sys/kernel/debug#
```

你可以按照自己的节奏分析 `usmog.txt` 中捕获的 `URB` 信息。随附的是完整日志文件。为了方便分析，只查看捕获大存储设备的日志部分。该片段包含了 Linux 主机和大存储设备之间发生的一些控制和批量事务。

如果你查看后续日志，可以将日志文件的第一行解释为针对总线 7 端点 0 的 `CONTROL` 传输。这是到 USB 地址 5 设备的控制传输。第二行捕获状态为 0 的 `SET_ADDRESS` `URB` 完成。

```
d2263a80 261300221 S C:7:0000:0 05 00 0500 0000 0000
d2263a80 2613001276 C:7:0000:0
d2263a80 2613121192 S C:7:0005:0 80 06 0100 0000 0012 18 <
d2263a80 2613121399 C:7:0005:0 18 = 12010002 0000040 2112342 0006102 | 0301
```

# 第 18 章 使用 Linux USB 进行调试

`cad4aa80 2613121452 S C:7:0005:0 80 06 0200 0000 09 9 <`

`nc4aa80 2613121662 C:7:0005:0 9 = 0922050 010108 32`

日志格式与上一节讨论的 `struct usb_mon_event` 数据结构匹配。后续章节将更详细地解析 `usmon` 日志。

注意日志以 `URB` 地址 (`d2263a80`) 开头，随后是 `URB` 提交时间 (`261310221`)。时间戳以及 USB 相关信息有助于测量完成 `URB` 事务所需的时间。图 18.7 提供了 `usmon` 日志的详细分解。

本节解析了大存储驱动程序的 `URB` 传输示例。以下终端活动是存储设备 5 和批量端点 1 的命令块封装 (CBW) 传输捕获。图 18.8 提供了 `usmon` 存储日志的详细分解。

```
d2263780 2618I25421 S Bo:7:005:1 -115 31 = 55534243 01000000 24000000 80000612 0000024 00000000 000000000

| URB Address | Time Stamp | Transfer & Event | Bus Number | Device Number | Endpoint Number | URB Status | Type | bRequest | wValue | wIndex |
|---|---|---|---|---|---|---|---|---|---|---|
| d2263a80 | 2613100221 | | Co | | | | s | | 5 | 0 |

| URB Address | Time Stamp | Transfer & Event | Bus Number | Device Number | Endpoint Number | URB Status | Type | bRequest | wValue | wIndex | wLength (Hex) | wLength (Decimal) | Direction (IN) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| d2263a80 | 2613112192 | | | | | s | 80 | 0 | 100 | 7c | 12 | < |

| URB Address | Time Stamp | Transfer & Event | Bus Number | Device Number | Endpoint Number | URB Status | Type | bRequest | wValue | wIndex | bLength&Descriptor/Type bUSB DeviceSubClass&Protocol MaxSize (HEX) | Vendor ID (Product) | iManufacturer Product | iSerialNumber&Configuration |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| d2263a80 | 2613121399 | | Ci | | | 5 | | 18 | 12010002 | 0000040 | 2112342 | 0006102 | 0301 |
```

你现在已经知道 `usmon` 提供了关于 `URB` 状态以及 Linux 主机与 USB 设备之间发生的 USB 活动的详细信息。通过这些信息，你可以轻松修复平台上的任何与 USB 相关的问题。

# 使用 UBSFS_SNOOP 进行调试

上一节讨论了 `usmon`，这是一种低级工具，用于捕获 USB 流中通过 `URB` 事务，以便使用 Linux 调试 USB 系统。有时，调试 Linux USB 子系统并不需要如此详细的信息。这为 Linux 上提供的另一种更简单的方法铺平了道路，该方法可以嗅探 USB 事务。`usfs_snoop` 是作为 `uscore` 的可用的一种调试机制，它可以在 USB 事务的更高层级嗅探 USB 数据，并将其作为系统日志的一部分打印出来。

图 18.9 展示了 `usfs_snoop` 在 Linux USB 子系统中的位置。正如名称所示，`usfs_snoop` 功能嗅探了在 `usfs` 文件系统上执行的操作所产生的 USB 细节。它捕获了用户应用程序通过 `usfs` 文件操作传递给 `uscore` 的 `URB`。虽然该

![](img/779a74a6577501a55983f193067274a3_285_0.png)

**图 18.9** `usfs_snoop` 在 `uscore` 中的设计位置。

# 第 18 章 使用 Linux USB 进行调试

功能是 `uscore` 的一部分，图 18.9 在 `uscore` 之外展示了该功能，以便更好地表示它 `usfs` 和 `uscore` 之间的作用。

在 `uscore` 中，`/drivers/usb/core/devio.c` 文件实现了 `usfs` 文件操作，这是 `usfs_snoop` 嗅探 `URB` 操作和 `URB` 状态的理想位置。在 `devio.c` 中实现的 `snoop_urb` 例程处理了这种嗅探活动。

```c
static void snoop_urb(struct usb_dev *udev, void *buffer, int pipe, unsigned long length, int timeout, enum snoop_status)
```

`uscore` 模块在 `devio.c` 中定义了模块参数 `static int usfs_snoop;`。该模块允许用户在运行时配置配置和控制 `usfs_snoop` 功能。要配置此 `usfs_snoop` 参数，用户应拥有相应的权限来更新参数文件。

```c
static int usfs_snoop;
module_param(usfs_snoop, bool, S_IRU | S_IW);
MODULE_PAR_DESC(usfs_snoop, "true to log all usfs traffic");
```

通常，Linux 将其模块参数导出为文件，使用户可以在用户空间访问它们。该模块参数声明为 `uscore` 的一部分，你可以在 `/sys/module/uscore/parameters/` 中找到该参数。下面的终端显示了 `uscore` 模块的参数。

```bash
root@laptop:~ ls /sys/module/uscore/parameters/
-rw-r--r-- 1 root 4096 May 28 autospend
-r----r-- 1 root 4096 May 28 lights
-r----r-- 1 root 4096 May 28 usb
-r----r-- 1 root 4096 May 28 old_scheme
-r----r-- 1 root 4096 May 28 usfs_snoop
-r----r-- 1 root 4096 May 28 use_both_schemes
root@laptop:~ 
```

在早前的讨论中，你看到 `usfs_snoop` 模块参数充当标志来控制嗅探调试信息。`snoop` 标志可以持有 `true` (1) 或 `false` (N)。下面的终端说明了如何读取 `usfs_snoop` 参数的值并解释了如何配置它。要了解标志的当前状态，你可以在参数文件上运行 `cat` 命令。

```bash
root@laptop:~ cat /sys/module/uscore/parameters/usfs_snoop
```

要配置此 `usfs_snoop` 参数，用户可以在参数文件上运行 `echo` 命令如下所示。

```bash
root@laptop:~ echo 1 > /sys/module/uscore/parameters/usfs_snoop
root@laptop:~ cat /sys/module/uscore/parameters/usfs_snoop
```

一旦设置标志，`URB` 信息就会被嗅探，你就可以准备收集内核日志的一部分调试数据。

注意

`usmon` 和 `usfs_snoop` 的主要区别在于，前者捕获内核和 `uscore` 之间的 `URB` 信息，而后者捕获用户应用程序和 `uscore` 之间的 `URB` 信息。另一个重要的点是，除非有用户文件操作，否则 `usfs_snoop` 不会在枚举期间捕获 `URB`。要使用 `usfs_snoop` 触发 `URB` 嗅探，你可以执行简单的实验，例如 `lsusb -v`，如下所示。
