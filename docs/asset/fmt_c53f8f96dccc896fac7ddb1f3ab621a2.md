
| Module | Size | Used by |
| :--- | :--- | :--- |
| usbid | 18980 | 0 |
| hid | 31428 | 1 usbid |
| ehci_hcd | 30836 | 0 |
| usbcore | 129752 | 3 usbid |

在有了这些基础设施之后，大多数符合 HID 类驱动规范的常用 HID 设备（如鼠标、键盘和 Joystick）都应该被识别并启用。当我插上我的金士无线旅行鼠标时，看到以下内容：

```
usb 2-1:4: low speed USB device using fsl-ehci and address 4
usb 2-1:4: configuration #1 chosen from 1 choice
input: Kingston USB Mouse as /devices/platform/fsl-ehci.1/usb2-2-1/
2-1.4/2-1.4:1.0/input2
input: USB HID v1.10 [Kingston Kingston USB Mouse] on
ususb-fsl-ehci.1-1.4
```

正如我们处理 USB 存储时所做，我们可以在 sysfs 文件系统中找到内核在枚举鼠标时分配的设备号。由于我们已经知道设备号包含在 `dev` 属性中，我们搜索原因-

```
root@imx31:~# find /sys -name dev | grep input
/sys/devices/platform/fsl-ehci.1/usb2/2-1/2-1.4/2-1.4:1.0/input/input2/event2/dev
/sys/devices/virtual/input0/event0/dev
/sys/devices/virtual/input1/event1/dev
```

因为我们将鼠标设备插在了外部集线器的端口 4，所以我们选择物理地址为 2-1.4:1-0 的设备：

```
root@imx31:~ cat /sys/devices/platform/fsl-ehci.1/usb2/2-1/2-1.4/2-1.4:1.0/input
->input2/event2/dev
13:66
```

最后，我们使用这些设备号创建设备节点：

```
root@imx31:~ mknode /dev/mouse c 13 66
```

现在你已准备好使用该设备。对于 USB 存储，如果你有一个工作良好的 `udev` 配置（如下一章所述），你不需要手动创建设备节点。这是 `udev` 的工作。

## 18.5.3 USB CDC 类驱动

USB 通信设备类（CDC）驱动程序旨在为整类常用通信提供通用的驱动框架。定义了几种标准 CDC 类，包括 ATM、以太网、ISDN PSTN（公共电话）、无线移动设备、电缆调制解调器和类似设备。

CDC 类驱动程序中最好的是以太网 CDC 功能。在开发期间，让可能没有以太网接口的嵌入式设备实现以太网连接是非常困难的。此类设备有很多，例如手机手机和 PDA。

实现此功能有两种不同方法。一种是直接使用标准 USB 线在主机和外设设备之间建立点对链路。另一种模型是使用以太网“适配器”（dongle），本质上是一个带有 USB 插头的以太网接口。我们将查看这两种方法。

在主机和外设之间建立直接的 USB 链路相对简单。当然，你必须拥有适当的硬件。例如，你不能仅用一根 USB 线将笔记本电脑连接到台式电脑。每个 USB 链路中的一端必须是“上行”设备（主机或集线器），另一端将是“下行”设备（外设设备或“gadget”）。记住，USB 是一种主从协议。

我们将使用 Beagle 作为使用 CDC 驱动进行 USB 直接网络工作的示例。你将在内核中启用此功能。当然，你必须有主机控制器驱动，对于 Beagle 来说是 `musb_hdrc`。这通过在内核中选择 `USB_MUSB_HDRC` 启用。对于 Beagle，必须选择 `TWL030_USB` 以启用以太网收发器。通过在 Gadget 下选择 `USB_GADGET_HDRC` 启用外设模式。最后，在 Gadget 下选择以太网支持。这是外设侧的驱动。在你的台式机或笔记本主机上，你需要加载 `usnet.ko`。在大多数桌面发行版中，当你接入来自 Beagle 的 USB 线时，`udev` 会自动执行此操作。假设你已经启用了 Beagle 的 `g_ether` 驱动并配置了接口。看看它的样子。列表 18-11

```
# modprobe twl030
twl030_usb: Initialized
# modprobe g_ether
usb_hdrc: version 6.0, musb-dma, peripheral, debug=0
usb_hdrc: USB controller at d80ab00 DMA, IRQ 92
g_ether gadget: using random address
g_ether gadget: using random host address
usb0: MAC ae:9e:55:32:a:9c
usb0: MAC c2:de:61:21:9c
g_ether gadget: Ethernet Gadget, version:0
g_ether gadget: ready
```

可能会使用 CDC 的某些元素，在以下示例中使用以太网适配器并不是严格通过类驱动。更方便的方法是将 `TWL030_USB` 直接编译进内核，因为没有理由移除它，它适用于所有 USB 模式且占用空间较。列表 18-11 续

| Module | Size | Used by |
| :--- | :--- | :--- |
| g_ether | 23664 | 0 |
| musb_hdrc | 35524 | 1 g_ether |
| twl030_usb | 5744 | 0 |

```
# ifconfig usb0 192.168.4.2
```

在加载列表 18-11 所示的两个设备驱动后，注意 usb0 接口已创建并枚举。`lsmod` 显示了这些步骤后加载的模块。注意 `modprobe` 自动加载了 `musb_hdrc`。最后一步是为接口配置有效的 IP 地址。当来自 Beagle 的 USB 线连接到你的 Ubuntu 8.04 笔记本时，会有相应的日志条目：

```
usb 7-3: new high speed USB device using ehci_hcd and address 1
usb 7-3: configuration #1 chosen from 1 choice
usb0: register 'cdc_ether' at usb-0000:00:7.3, CDC Ethernet Device, 32:89:fb:33:00:04
usbcore: registered new interface driver cdc_ether
adapter(NETDEV_CHANGE): usb0: link becomes ready
```

链路主机侧自动安装了 `cdc_ether.ko` 及其依赖模块 `usbnet.ko`。在你的 Ubuntu 8.04 笔记本上：

```bash
$ lsmod | n 3
```

| Module | Size | Used by |
| :--- | :--- | :--- |
| cdc_ether | 7168 | 0 |
| usbnet | 20232 | 1 cdc_ether |

我们为主机侧的 `usb0` 接口配置有效的 IP 地址（如果在同一子网内最简单），现在我们有了从 BeagleBoard 到笔记本 USB 接口的工作以太网接口。注意，如果你的笔记本/桌面发行版没有运行 `udev`（由于不可想象的原因）或未正确配置，你必须在链路的主机端手动加载 `usbnet` 和 `cdc_ether`。如果配置良好的外设设备（如 BeagleBoard）连接到台式机/笔记本主机的 USB 端口，加载这些模块将创建并枚举 usb0 接口。

## 18.5.4 USB 网络支持

在带有 USB 端口的嵌入式设备上启用以太网的另一种方法是使用插入 USB 主机端口以太网适配器。这些适配器在许多电子商店和网上都可以买到。我们在下一个示例中使用的是从 Radio Shack 购买的。它在中国制造的普通设备，包含一个 ASIX 芯片。插入 USB 主机端口时，它就变成了一个完全工作的以太网端口。

你需要在内核中支持此功能。对于这种特定的适配器，你必须启用 `USB_USBNET` 和 `USB_NET_AX8817X`。这些选项位于内核配置工具的 Device Drivers -> Network Devices -> USB Network Support 下。在加载必要的 USB 底层驱动后，加载 ASIX 驱动并插入以太网适配器。如下所示：

```
# modprobe asix
# usb: register new interface driver asix
# usb 1-1.3: high speed USB device using musb_hdrc and address 3
usb 1-1.3: configuration #1 chosen from 1 choice
eth0(asix): not net_device_ops yet
eth0: register 'asix' at usb-musb_hdrc-1.3, ASIX AX8872 USB 2.0 Ethernet,
00:50:b6:03:c8:f8
```

首先你看到底层 USB 支持的消息，枚举 USB 设备 (1-1.3)。然后 ASIX 驱动接管并创建一个新的以太网接口 eth0。除非你在加载 ASIX 模块时通过参数覆盖它，否则它会创建一个随机的以太网地址。

下一步是为接口配置有效的 IP 地址：

```
# ifconfig eth0 192.168.4.159
eth0: link up, 100Mbps, full-duplex, lpa 0xCDE1
eth0: link up, 100Mbps, full-duplex, lpa 0xCDE1
# ping 192.168.4.1
PING 192.168.4.1 (192.168.0.1) 56 (84) bytes of data.
64 bytes from 192.168.4.1: icmp_seq=1 ttl=64 time=1002 ms
64 bytes from 192.168.4.1: icmp_seq=2 ttl=64 time=0.305 ms
64 bytes from 192.168.4.1: icmp_seq=3 ttl=64 time=0.336 ms
```

就是这些了！

## 18.6 USB 调试

启用 USB 支持后，有许多调试选项可用。启用详细调试信息是查看系统运行情况的良好方法。在内核配置中启用 `USB_DEBUG` 可以查看来自 uscore 和集线器驱动（uscore 的一部分）的调试消息。启用 `USB_ANNOUNCE_NEW_DEVICES` 会为每个插入的设备生成报告，列出来自设备描述符的供应商、产品、制造商和序列号。这两个选项都会将输出到 syslog，并可以在“USB 支持（USB Support） -> 主机侧 USB（Host-side USB）”下找到。

列表 18-12 显示了在编译了上述提到的调试配置选项的内核后，插入以太网适配器后的 syslog 日目。

### 列表 18-12 插入以太网适配器时的调试输出

```
user.info kernel: usb 1-1.3: new speed USB device using musb_hrdc
and address 3
user.debug kernel: usb 1-1.3: default language 0x0409
user.info kernel: usb 1-1.3: (none) USB device found, idVendor=0b95, idProduct=7720
Jan 1 00:02:38 user.info kernel: usb 1-1.3: New USB device strings:
Mfr=1, Product=2, SerialNumber=3
user.debug kernel: usb 1-1.3: Product:ASX88772
user.info kernel: usb 1-1.3: Manufacturer: ASIX Elec. Corp.
user.info kernel: usb 1-1.3: SerialNumber: 000001
user.debug kernel: usb 1-1.3: uevent
user.debug kernel: usb 1-1.3: usb_probe_device
user.info kernel: usb 1-1.3: configuration #1 chosen from 1 choice
user.debug kernel: usb 1-1.3: adding 1-1.3.1.0 (config 1, interface 0)
user.debug kernel: usb 1-1.3.1.0: uevent
user.debug kernel: drivers/usb/core/inode.c: creating file '003'
```

大部分日志条目都是自显其明的。你可能对最后一条条目感到好奇，它宣布了文件‘003’的创建。当你在目标系统上找不到它时，可能会感到困惑。它是 USB 设备系统 `usbfs` 的一部分，在像之前描述的那样挂载 `usbfs` 之前它是不可见的：

```
# mount -t usbfs usbfs /proc/bus/usb
```

在挂载 usbfs 后，你会在 /proc/bus/usb/001 看到创建的文件，它代表实例化的 USB 接口。`001` 是编号，`003` 代表设备。该文件不是人类可读的；它包含了 USB 接口的描述符。

某些平台和驱动程序可能具有特定平台的调试选项。例如，使用 `musb_hdrc` 驱动的 BeagleBoard 内核可以编译调试功能。要使用它，你必须在加载 `musb_hdrc` 驱动时向其传递调试级别。此特定选项可以产生详细的调试信息，包括设备之间发送的每个 USB 消息的信息。你可能记得通过在 `modprobe` 命令行中指定或在特定发行版的配置文件中向模块传递模块参数。此示例将 `musb_hdrc` 驱动中的调试级别设置为 3：

```
# modprobe musb_hdrc debug=3
```

## 16.6.1 usbmon

如果你是硬核玩家，可以尝试一下 `usbmon`。这是一个类似于 `tcpdump` 的 USB 数据包捕获器。USB 中并没有真正使用“包（packet）”一词，但概念是。`usbmon` 允许你捕捉 USB 总线上设备之间传输的原始跟踪。如果你正在从头开发 USB 设备，它可能会很有帮助。

要使用 `usbmon`，必须首先启用 `DEBUG_FS`，它位于内核配置中的“内核黑客（Kernel Hacking）”菜单下。你还需要启用 `USB_MON`，它位于“设备驱动（Device Drivers） -> USB 支持（USB Support） -> 主机侧 USB 支持（Support for host side USB）”下。

启用后，你必须如下如下挂载 `debugfs` 文件系统：

```
# mount -t debugfs debugfs /sys/kernel/debug
```

然后加载 `usbmon.ko` 驱动：

```
# modprobe usbmon
```

完成后，跟踪功能已启用。你在 /sys/kernel/debug/usbmon 中看到 USB 驱动创建的调试套接字。内核将数据包转储到这些调试套接字中。像 `tcpdump` 一样，它们以文本格式转储，使得（某种程度上）人类可读。只需其中一个套接字上启动 `cat`。列表 18-13 显示了在启用 `usbmon` 的 BeagleBoard 上插入 USB 闪盘时的几行跟踪信息。

### 列表 18-13 usbmon 跟踪

```
# cat /sys/kernel/debug/usbmon/usbmon/0
c717ee40 1830790883 Ci:i:002:1 0:2048 1 D
c717ee40 1830790944 Si:i:002:1 -115:2048 1 <
c717e140 1830791005 S:i:002:0 a3 03 00 0000 0003 0004 4 <
c717e140 1830791249 C:i:002:0 0 4 = 01010100
c717e140 1830791279 S:i:002:0 23 01 0010 0003 0000
c717e140 1830791524 C:i:002:0 0 0
c717e140 1830791554 S:i:002:0 23 03 0016 0003 0000
```

## 19.2 设备发现

当检测到硬件时，系统会“加载驱动程序”或“创建设备节点”。事实上，udev 通常会默认执行这些操作，但你可以自定义在发现特定设备时所执行的操作。udev 的默认行为是根据内核提供的设备名称创建一个设备节点。

在系统启动后的很久以后，设备有许多方式突然出现在你的 Linux 系统中。一些显而易见的例子包括将 USB 设备插入 USB 端口，或者使用许多笔记本电脑上的开关启用无线接口。将硬盘热插到容错性机箱中也可能是另一种情况。

当内核发现新设备时，它会创建一个 uevent（内核事件），并将其传递给用户空间中 netlink 套接字上的监听器。该监听器就是 udev。列表 19-1 显示了内核传递的一个典型 uevent。该事件是使用 udevadm 工具捕获的，当时正向 BeagleBoard 的 USB 主端口插入一个四口集线器：

```
# udevadm monitor --environment
```
