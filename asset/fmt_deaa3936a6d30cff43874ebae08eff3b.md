
user.info (none) user.info kernel: usb 1-3 New USB device found, idVendor=0b95, idProduct=7720

Jan 1 00:02:38 (user) user.info kernel: usb 1-3: New USB strings:

Mfr=1,Product=2, SerialNumber=3

user.info kernel: usb 1-3: Product: AX8872

user.info kernel: usb 1-3: Manufacturer: ASIX Elec. Corp.

user.info kernel: usb 1-3: SerialNumber: 000001

user.debug kernel: usb 1-3: uevent

user.debug kernel: usb 1-3: usb_probe_device

user.info kernel: usb 1-3: configuration #1 chosen from 1 choice

user.debug kernel: usb 1-3: adding 1-3:1:0 (config #1, interface 0)

user.debug kernel: usb 1-3:1.0: uevent

user.debug kernel: drivers/usb/core/inode.c: creating file '003'

```
某些平台和驱动程序可能具有平台特定的调试选项。例如，使用 `musb_hdrc` 驱动的 BeagleBoard 内核可以编译调试功能。在内核配置中启用 `USB_MUS_DEBUG` 以获取此功能。要使用它，你必须在加载 `musb_hdrc` 驱动时为其传递一个调试级别。此特定选项可以产生详细的调试信息，包括设备之间发送的每个 USB 消息的信息。你可能记得，通过指定 `modprobe` 命令行或特定发行版的配置文件，来向模块传递模块参数。此示例将 `musb_hdrc` 驱动程序中的调试级别设置为 3：
```
# modprobe musb_hdrc debug=3
```

## 18.6.1 usbmon

如果你是一个硬核玩家，可以尝试使用 usbmon。这是一个类似于 tcpdump 的 USB 数据包嗅探器。USB 中并没有真正使用“数据包”（packet）一词，但概念是相同的。usbmon 允许你捕获 USB 总线上设备之间传输的原始轨迹。如果你正在从头开发一个 USB 设备，那么这可能会非常有帮助。

要使用 usbmon，你必须首先启用 `DEBUG_FS`，它位于内核配置中的 `Kernel Hacking` 菜单下。你必须启用 `USB_MON`，它位于 `Device Drivers -> USB Support -> Support for host side USB` 下。

启用后，你必须如下所示挂载调试文件系统：
```
# mount -t debugfs debugfs /sys/kernel/debug
```
然后加载 `usbmon.ko` 驱动：
```
# modprobe usbmon
```
完成后，跟踪功能已启用。你可以在 `/sys/kernel/debug/usbmon` 中看到 USB 驱动创建的调试套接字。内核将包转储到调试套接字中。像 tcpdump 一样，它们以文本格式转储，这使得它们（具有）人类可读性。只需在一个套接字上启动 `cat` 即可。列表 18-23 显示了将 USB 闪盘插入已启用 BeagleBoard 时的几行轨迹。

# 第 18 章 通用串行线

### 列表 18-13 usbmon 轨迹
```
# cat /sys/kernel/debug/usbmon/0u
c71ee40 1830790883 C:ii1:2002:1 0:2048 1 D
c71ee40 1830790944 S:ii1:2002:1 -115:2048 1 <
c71ee40 1830791005 S:ii1:2002:0 s a3 00 0000 0003 0004 4 <
c71ee40 1830791249 C:ii1:2002:0 4 = 0101010
c71ee40 1830791279 S:Co1:2002:0 s 23 01 0010 0003 0000 0
c71ee40 1830791524 C:Co1:2002:0 0 0
c71ee40 1830791554 S:Co1:2002:0 s 23 03 0016 0003 0000 0
```
`cat` 进程是在 USB 闪盘插入之前启动的。生成了五十三行输出，表示传输了 53 个 USB 包¹。深入讨论此输出轨迹的格式和细节超出了本书的范围。你可以参考内核源码树中 `.../Documentation/usb/usbmon.txt` 中的文章。然而，要完全理解它，需要对内部 USB 架构有更深入了解。如果你想在 USB 知识上更进一步，请参考本章末尾的参考文献。

## 18.6.2 有用的 USB 杂项

通常当你将 USB 设备插入主机时，并不会发生什么大变化。可能会出现很多问题，但最可能的情况是该设备没有可用的设备驱动程序。如果在插入 USB 设备时，你在 syslog 中看到类似下面的消息，这意味着设备已被识别，读取了其描述符并选择了一种配置，但 Linux 无法为该设备找到合适的设备驱动程序：
```
usb 1-1.1: high speed USB device using ehci_hcd and address 5
usb 1-1.1: configuration #1 choice from 1 choice
```
解决办法是找到并为你的 USB 插件启用正确的设备驱动程序。当然，作为嵌入式开发人员，你可能不得不自己写一个。

尽管这似乎显而易见，但依赖键盘或鼠标等 USB 设备系统应该将这些驱动程序配置为静态链接到内核（=y）。这可以防止在移除依赖模块时丢失控制台。

> “数据包”（packet）一词不在 USB 词汇中。然而，相关细节超出了本书的范围。如果你想深入研究，请查看本章末尾的参考文献。

## 18.7 总结

本章为理解相当复杂的 USB 子系统提供了基础。它描述了拓扑结构和概念，并检查了 USB 是如何配置和使用的。讨论了最常用的 USB 子系统。

- 通过检查物理和逻辑拓扑结构，你可以更好地理解 USB。
- 涵盖了不同类型的 USB 线缆和连接器。
- 展示了多个 USB 配置示例。
- sysfs 在第 9 章中介绍，并涵盖了其在 USB 中的用法。
- 详细介绍了多个用于理解和排错 USB 的有用工具。
- 引入了包括大存储、HID 和 CDC 在内的类驱动程序。
- 本章最后总结了一些有助于调试工具和技巧。

## 18.7.1 阅读建议

- Universal Serial Bus System Architecture, 2nd Edition
Don Anderson
Mindshare, Inc., 2001

Enhanced Host Controller Interface Specification for Universal Serial Bus Version 1.0
Intel Corporation
www.intel.com/technology/usb/download/ehci-r10.pdf

- Essential Linux Device Drivers
Chapter 11, “Universal Serial Bus"
Sreeakrishnan Venateswaran
Prentice Hall, 2008

- Linux Device Drivers, 3rd Edition
Chapter 13, “USB"
Jonathan Corbet, Alessandro Rubini, Greg Kroah-Hartman

在检测到硬件时，会运行“驱动程序”或“创建一个设备节点”。事实上，udev 经常默认执行这些操作，但你可以自定义在发现特定设备时所执行的动作。udev 的默认行为是根据内核提供的设备名称创建一个设备节点。

在 Linux 系统启动后，设备有许多方法可以突然出现在你的系统中的。一些例子包括将 USB 设备插到 USB 端口上，或者通过许多笔记本电脑上的开关启用无线接口。将硬盘热插到具有容错机箱中也可能是另一种方式。

## 19.2 设备发现

当内核发现新设备时，它会创建一个 uevent（用户事件），并将其传递给用户空间中 netlink 套接字¹ 上的监听器。该监听器就是 udev。列表 19-1 显示了内核传递的一个典型 uevent。它是通过如下方式使用 `udevadm` 工具捕获的，当时是将一个四口 USB 集线器插入到 BeagleBoard 的 USB 主机端口上：
```
# udevadm monitor --environment
```
