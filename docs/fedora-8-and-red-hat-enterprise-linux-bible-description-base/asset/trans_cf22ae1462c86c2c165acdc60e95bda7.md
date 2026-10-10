

- **iwlwifi-firmware** — 包含适用于 Intel PRO/Wireless 3945 A/B/G 网络适配器的固件。这些卡片所使用的 Linux 驱动程序的项目页面位于：`http://intellinuxwireless.org`。
- **bcm43xx-fwcutter** — 包含 `bcm43xx-cutter` 命令，用于从基于 Broadcom 43xx 无线卡片的驱动程序中提取固件。由于这些卡片的固件无法自由分发，您需要下载随卡附带的驱动程序，并将固件提取到 `/lib/firmware` 目录中。

如果您的无线网卡受上述任何软件包支持，您可以尝试安装该软件包、重启系统并配置您的无线网卡。如果您的网卡不支持这种安装方式，请参阅下一节以了解如何使其他无线网卡正常工作。

### 选择无线局域网卡

无线局域网卡制造商对提供 Linux 驱动程序的积极性不高。大多数 Linux 原生的无线网卡驱动都是在没有这些制造商帮助的情况下创建的。此外，在许多情况下，根本不可用 Linux 驱动程序。

购买无线局域网卡的另一个问题是，制造商经常在不通知用户的情况下更改硬件。同名同型号的无线卡可能包含不同的无线芯片组。虽然这对 Windows 用户可能不是问题（因为厂商会包含匹配的 Windows 驱动程序），但在 Linux 机器上，该卡可能无法正常工作，尽管其他使用同名卡片的 Linux 用户坚称其运行良好。

因此，既然您知道无线卡到家后可能无法正常工作，让我们谈谈如何提高挑选到可用卡片的几率。以下是一些开始查找的地方：

- **原生 Linux 驱动** — 某些无线网卡拥有专门为 Linux 系统创建的驱动程序（参见上一节）。拥有这些驱动的卡片在被检测到并安装无线网卡后自动工作的几率很大。一个名为 Madwifi 的项目（`http://madwifi.org`）提供了额外的 Linux 无线驱动程序，这些程序专门为使用 Atheros（`www.atheros.com`）芯片组的无线局域网卡创建。选择 Madwifi Wiki 中的兼容性列表（`http://madwifi.org/wiki/Compatibility`）以查看支持的无线网卡。Livia.org 存储库中提供 Madwifi RPM 包（有关从 Linva.org 存储库安装软件包的信息，请参见第 2 章）。
- **Windows 驱动** — 在没有原生 Linux 驱动可用的情况下，有时可以结合名为 ndiswrapper 的开源驱动程序和 Windows 驱动程序在 Linux 中使用无线网卡。要查看 ndiswrapper 支持哪些卡片，请参阅 ndiswrapper 支持卡片的列表。前往 NDiswrapper wiki（`http://ndiswrapper.sourceforge.net/joomla/`），选择 Documents/Wiki → List of Cards。

表 15-1 列出了随 Fedora 和 RHEL 包含的具有 Linux 专用开源驱动程序的网卡列表。

> **注意：** 即使您的无线卡未列在表 15-1 中，它仍可能使用 Fedora 或 RHEL 包含的驱动程序正常工作。包含相同芯片组（因此使用相同驱动程序）的一些无线卡可能被称为不同的名称。为了不必追踪无线行业中各种收购和名称变更，请参阅 **Linux 无线局域网 HOWTO**（www.hpl.hp.com/personal/Jean_Tourrilhes/Linwx）。**驱动程序**部分提供了关于哪些驱动程序适用于哪些卡片的更多见解。

**表 15-1：支持的无线网卡适配器和模块**

| 无线网卡适配器 | 模块 |
|:---|:---|
| 350 系列无线局域网适配器（思科系统） | airo_cs.ko |
| ADMtec ADM8211 无线 | adm8211.ko |
| Aironet PC4500（思科系统） | airo_cs.ko |
| Aironet PC4800（思科系统） | airo_cs.ko |
| AT&T WaveLAN 适配器 | wavelan_cs.ko |
| Atheros 802.11 无线 | ath5k.ko |
| Atmel AT76C50X 无线 | atmel_cs.ko |
| Atmel AT76C50X 无线（PCI 版本） | atmel_pci.ko |
| Broadcom 43xx 无线 | bcm43xx.ko |
| Cabletron RoamAbout 802.11 DS | wlan_cs.ko |
| Compaq WL100 11 Mbps 无线适配器 | orinoco_cs.ko |
| Digital RoamAbout/DS | wavelan_cs.ko |
| ELSA AirLancer MC-11 | wlan_cs.ko |
| Intel PRO/Wireless 2100 网络连接 mini PCI 适配器 | ipw2100.ko |
| Intel PRO/Wireless 2915ABG 和 2200BG 网络连接 mini PCI 适配器 | ipw2200.ko |
| 卢森特（Lucent Technologies）WaveLAN 适配器 | wavelan_cs.ko |
| Intersil PRISM2 11 Mbps 无线适配器 | wlan_cs.ko |
| 卢森特（Lucent Technologies）WaveLAN/IEEE 适配器 | orinoco_cs.ko |
| MELCO WLI-PCM-L11 | orinoco_cs.ko |
| MELCO WLI-PCM-L11G | orinoco_cs.ko |
| NCR WaveLAN 适配器 | wavelan_cs.ko |
| Orinoco PC 卡 | orinoco_cs.ko |
| PLANEX GeoWave/GW-CF110 | orinoco_cs.ko |
| Planet WL3501 | wl3501_cs.ko |
| Prism54 PCI 无线 | prism54pci.ko |
| Prism54 USB 无线 | prism54usb.ko |
| Realtek RTL8187 USB 无线 | rtl8187 |
| Xircom CreditCard Netwave | netwave_cs.ko |
| ZCOMAX AirRunner/XI-300 | orinoco_cs.ko |
| ZyDAS ZD1201 无线局域网 USB 棒 | zd1201.ko |
| ZyDAS ZD1211 无线局域网 USB 棒 | zd1211rw.ko |

## 选择天线

如果您在彼此紧邻的几台计算机之间设置无线局域网，可能不需要额外的天线。但是，为了应对障碍物和更长的距离，您可以在无线硬件中添加室内或室外天线。

在接下来的章节中，我将展示与这些卡片兼容的不同类型的室内和室外天线。

## 使用室内天线

内置于无线局域网卡中的天线通常足够在开放区域实现计算机之间的通信。如果无线局域网卡之间的直接视线被阻挡，额外的室内天线会很有用。计算机可能被锁在储物柜里或卡在书桌下面。一堆文件可能会阻碍传输，或者一块金属可能会完全阻断它。一个将传输信号从卡片引开的小天线可能是解决这些问题的答案。

虽然大多数无线局域网卡不需要完全无障碍的视线，但障碍物肯定会减慢接收速度。为了解决这个问题，像 Orinoco IEEE 范围扩展器这样的天线可以直接插入 Orinoco Gold 或 Silver 无线局域网卡。1.5 米的延长线可以将信号从关闭的門后引出，或延伸到书桌顶部。设置天线时，建议将其：

- 放置在中心位置
- 垂直安装
- 远离障碍物（特别是金属表面，以及在较小程度上混凝土墙或文件堆等实心物体）

请参考随天线提供的说明，了解有关天线放置和安装的具体指南。

## 使用室外天线

为您的无线局域网选择和设置室外天线可能比在室内设置更加困难和昂贵。但是，一旦室外天线就位，您就可以省钱，因为您不需要多个互联网访问账户（月度费用、DSL/电缆调制解调器等）。

尽管本章的范围不包括使用室外天线配合无线局域网的完整描述，但这里有一些帮助您选择最适合无线局域网的天线的提示。

- **点对点与多点** — 如果您在两个室外位置之间创建点对点链接（例如，在两座建筑之间共享互联网连接），定向天线可以帮助您实现更远的距离和传输速度。但是，如果您的天线为其他多个室外天线或无线客户端（例如在草坪上使用笔记本电脑的学生）提供多点访问，全向天线可能更合适。
- **净空** — 每个室外天线之间的视线越清晰，您可以实现的距离和传输速度就越大。将天线放置在尽可能高的点上可以防止因树木、汽车、建筑物和其他物体导致的性能下降。障碍物与无线传输覆盖范围之间的距离被称为净空系数（参见图 15-9）。

![](img/fb202c163797a743c3c6cf236316bc96_685_0.png)

**图 15-9**：障碍物距离无线信号的距离称为净空。

- **距离** — 尽管天线发送和接收数据的实际距离因不同因素而异，您可以使用室外天线实现数英里的距离。例如，两个 Orinoco 24 dBi 定向抛物面栅格天线理论上可以在 180 米净空条件下以 11 Mbps 的传输速度实现最远 52 英里的距离。将该传输速率降低到 1 Mbps

