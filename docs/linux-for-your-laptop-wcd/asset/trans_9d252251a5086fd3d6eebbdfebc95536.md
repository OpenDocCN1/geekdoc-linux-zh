

### 资源信息

http://www.astart.com/lprng/LPRng.html

Linux 替代打印队列系统 LPRng 的主页。

### 打印 HOWTO

Grant Taylor 关于如何配置和使用 Linux 打印的信息。通常可以在 `/usr/doc/HOWTO` 目录下找到，不过最新的副本（与几乎所有章节型文档一样）可以在 http://www.linuxdoc.org 上找到。

### IR（红外）HOWTO

http://home.sndf.de/wehe/ir_misc.html

一个详尽的设备表格，列出了包括笔记本电脑在内的可以使用 Linux 和 IrDA 的设备。

Werner Heuser 对 Linux IrDA 项目的总结，其中包含在 Linux 下使用 IrDA 的技巧和应用。可以在最新 Linux 发行版的 `/usr/doc/HOWTO` 目录下或 http://www.linuxdoc.org 上找到。

http://www.creative-it.com/linux/irda/toshiba_irda_howto.html

Guenther Wieser 针对东芝笔记本用户关于使用 IrDA 和 Linux 的具体说明。

http://www.physiol.usyd.edu.au/daved/linux/bjc-80.html

对于希望使用 IrDA 进行打印的 CanonBJC-50 和 BJC-80 移动 Linux 用户来说，这是最佳的入门起点。

http://www.linuxworld.com/linuxworld/lw-1999-06/lw-06-hylafax_p.html

一篇关于使用 HylaFax 的文章，附带有关互联网传真侧边栏信息。

## 第 15 章：在路上建立连接

- 拨号连接
- DSL 连接
- 无线连接
- 网络连接策略
- 免费服务
- 资源信息

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_354_0.png)

本章向你介绍各种技术和软件，使作为移动 Linux 用户的你能够在旅途中连接到你的互联网服务提供商（ISP）和互联网。你还将了解沿途可用的不同技术以提供帮助。本章首先展示一些通常随 Linux 提供的常见互联网连接工具，以及常见的互联网连接方式。然后，它指引你找到其他新技术和技术的来源，这些技术可以在你穿梭于办公室、家中、仓库或乡村时提供帮助。

### 拨号连接

调制解调器是连接互联网最常用的工具。随着其他技术（如数字用户线路服务 (DSL) 和蜂窝电话公司）在市场上争夺连接份额，这一状况将维持多久尚待观察。然而，目前内置、外置或 PC 卡调制解调器仍然是移动 Linux 用户的首选标准连接硬件。本节向你展示使用 Linux 软件连接 ISP 的三种方法。

拨号互联网连接使用点对点协议 (PPP) 通过串行线路提供网络服务和信息。一种先行的协议，串行线路接口协议 (SLIP)，曾经很流行，但现在似乎已失宠。PPP 在 Linux 下得到很好的支持。当你通过调制解调器与你的 ISP 连接时，Linux 会创建一个名为 ppp0（针对第一个 PPP 设备）的接口，几乎每个 Linux 网络实用程序或互联网程序都通过这个新接口进行通信。当你结束连接时，Linux 从内存中移除 ppp0 接口。

### 配置

你的第一项工作是确定你的 PC 卡或内置调制解调器在笔记本上连接到哪个串行端口。如果你使用外置调制解调器，你可能需要一个调制解调器电缆，一端是 DB-25 连接器，另一端是母 DB-9 插头（适合大多数笔记本电脑上的公 DB-9 串行连接器）。

如果你的笔记本电脑有一个用于内置调制解调器的 RJ-11 电话插孔，请确保该调制解调器可以与 Linux 一起工作（参见侧边栏“Linmodems”）。如果你使用 PCMCIA 调制解调器卡，它可能有一个 RJ-11 电话插孔或使用外置适配模块。使用 `dmesg` 命令查看 Linux 启动时发现的串行端口：

```bash
# dmesg | grep tty
ttyS00 at 0x03f8 (irq = 4) is a 16550A
ttyS01 at 0x02f8 (irq = 3) is a 16550A
```

在这个例子中，Linux 发现了两个串行端口。其中这些端口（在笔记本电脑上）将是外置串行端口或内置调制解调器端口之一。有时 Linux 在笔记本电脑上会发现三个或更多串行端口，特别是如果插入了 IrDA 端口、内置调制解调器、外置串行端口，并且在笔记本的 Type II 插槽中插入了 PC 卡调制解调器。

`dmesg` 输出中的 ttyS 设备对应于 `/dev/` 目录下找到的设备文件。例如，你可以使用 `ls` 命令查找这些设备：

```bash
# ls /dev/ttyS*
/dev/ttyS0  /dev/ttyS1  /dev/ttyS2  /dev/ttyS3
```

这些是 Linux 设备文件描述符，当 Linux 应用程序希望使用串行端口进行通信时使用这些。请注意，与瞬时的 eth0 和 ppp0 网络接口不同，这些设备不会即时创建，在使用后也不会从你的 Linux 文件系统中移除。这些设备的串行端口的中断和输入/输出地址应该如下所示：

```text
/dev/ttyS0  0x2F8  IRQ 4
/dev/ttyS1  0x2F8  IRQ 3
/dev/ttyS2  0x3F8  IRQ 4
/dev/ttyS3  0x2E8  IRQ 3
```

请注意，如果 Linux 识别出三个串行端口，而其中两个恰好使用相同的 IRQ，你可能会有问题。如果发生这种情况，请使用 `setserial` 命令，连同串行设备名称、`irq` 关键字和新的 IRQ，更改端口的设置。例如：

```bash
# setserial /dev/ttyS2 irq 10
```

这有时可能是必要的，特别是当你试图配置 IrDA 端口时。

如果你有一个 PC 卡调制解调器，在尝试配置串行端口之前，请确保已启用 Card Services。如果你使用 Red Hat 或 Mandrake Linux，请查看文件 `/etc/sysconfig/pcmcia`。在大多数情况下，它应该看起来像这样：

```text
PCMCIA=yes
PCC=182365
```

### 没有 PCMCIA

虽然 Apple iBook 没有 PCMCIA 插槽，但你可以使用其内置调制解调器拨号并启动 PPP 连接。使用 Apple 的 OpenFirmware 提示符和 Yaboot 实用程序启动 Yellow Dog Linux。iBook 内置调制解调器将被识别为 /dev/ttyS0。

然后你可以使用 `ntsysv` 命令确保 Card Services 将在下次 Linux 启动时运行，或者你可以立即使用以下命令启动它：

```bash
# /etc/rc.d/init.d/pcmcia start
```

如果你在配置 PCMCIA 调制解调器时遇到困难，请阅读 David Hinds 的 PCMCIA-HOWTO，通常可以在 `/usr/src/linux/pcmcia*` 目录下找到。

### Linmodems

软件驱动、无控制器的调制解调器，俗称“winmodems”，被许多台式机制造商和笔记本制造商用来节省生产成本。然而，这些所谓的调制解调器以额外的成本向消费者提供通信服务。例如，这些调制解调器几乎都只适用于来自垄断软件行业巨头（我可以让你猜猜是哪一个）的商业操作系统。驱动程序源代码未提供，目前也无法获取。如果你处于商业操作系统升级的跑步机上，没有保证会有适合你笔记本的调制解调器驱动程序的可用新版本！此外，这些“调制解调器”使用你笔记本的 CPU 完成大部分工作，当你试图最大限度地利用电池电量时，这提供了另一种资源消耗。不要为 Linux 购买 winmodem！Lucent Technologies 是唯一站出来为 Linux 提供可能解决方案的制造商，通过发布一个仅二进制（当然没有源代码）的内核模块，该模块已验证可在 IBM ThinkPad 390X 和许多其他笔记本上工作。如果你不幸拥有一个带有无控制器调制解调器的笔记本，该模块可能工作也可能不工作，具体取决于你配备 Lucent 芯片的笔记本。浏览位于 http://www.linmodems.org 的 Linux Winmodem (Linmodem) 页面，你会发现其他可能的解决方案，例如使用 Ambient Tech 芯片组调制解调器的驱动程序。

你可以使用 `minicom` 通信命令交互式测试你的调制解调器。然而，你首先应该创建一个名为 /dev/modem 的符号链接，指向你的调制解调器串行端口。此外，请确保你的调制解调器已插好，

