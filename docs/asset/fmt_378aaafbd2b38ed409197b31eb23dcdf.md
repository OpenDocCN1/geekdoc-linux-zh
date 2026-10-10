
- `iwl3945-firmware` — 包含 Intel xc2 xae PRO/Wireless 3945 A/B/G 网络适配器所需的固件。用于这些卡的 Linux 驱动的项目页面位于：http://wireless.org。
- `iwl4965-firmware` — 包含 Intel xc2 xae PRO/Wireless 4965 A/G/N 网络适配器所需的固件。
- `zd2111-firmware` — 包含与基于 ZD2111 和 ZD211B 芯片的无线局域网 USB 须工作所需的固件。这些无线卡的 Linux 驱动源码和文档可以在此处找到：www.de-taler.de/zd2111/。
- `rt61ci-firmware` — 包含 Ralink xc2 xae RT2561/RT2661 A/B/G 网络适配器所需的固件。
- `rt73usb-firmware` — 包含 Ralink xc2 xae RT2571W/RT2671 A/B/G 网络适配器所需的固件。
- `bcm43xx-fwcutter` — 从 Broadcom 43xx 无线卡创建的驱动程序中提取固件的 `bcm43xxx-fwcutter` 命令。由于这些卡的固件无法自由分发，你需要下载随卡附的驱动程序并将固件提取到 `/lib/firmware` 目录。

如果你有受这些包之一支持的无线卡，可以尝试安装该包、重启并启动 NetworkManager。如果你的卡不支持这种方式支持，请参考下一节获取关于启动其他无线卡的信息。

## 选择无线局域网卡

无线局域网卡制造商对提供 Linux 驱动程序表现出太大兴趣。大多数 Linux 原生无线卡驱动程序是在没有制造商帮助的情况下创建的。此外，在许多情况下完全没有 Linux 驱动程序。

购买无线局域网卡相关的另一个问题是，制造商经常在不通知的情况下更改硬件。相同名称和型号的无线卡可能包含不同的无线芯片组。这对于 Windows 用户可能不是问题（因为供应商会包含匹配的 Windows 驱动程序），但你的 Linux 机器可能会失效，尽管其他在 Linux 中使用相同名称卡的人发言其运行良好。

所以，现在你知道你的无线卡在安装之前可能无法工作，让我们谈谈如何最有概率挑选到一个工作的卡。这里是一些地方：

- 原生 Linux 驱动 — 某些无线卡有专门为 Linux 系统创建的驱动程序（见前节）。带有这些驱动程序的无线卡在你安装无线卡后很有可能被检测到。为使用 Atheros 芯片组的无线局域网创建了 Madwifi (http://madwifi.org) 项目。从 Madwifi Wiki (http://madwifi/wiki/Compatibility) 选择支持的无线卡。来自 Livna.org 的 Madwifi RPM 包。

### 表 15-1：支持的无线适配器

| 无线适配器 | 模块 |
| :--- | :--- |
| 350 (Cisco Systems) | `airo.ko` |
| ADMtec8211 | `adm8211.ko` |
| Aironet PC400 (Cisco Systems) | `airo.ko` |
| Aironet PC4500 (Cisco Systems) | `airo.ko` |
| Aironet PC4800 (Cisco Systems) | `airo.ko` |
| AT&T WaveLAN | `wavel.ko` |
| Atheros 802.11 | `ath5k.ko` |
| Atmel AT76C50 | `atmel.ko` |
| Atmel AT76C50X (PCI) | `atmel_pci.ko` |
| Broadcom 43xx | `bcm43xx` |
| Cabletron Roam 802.11 | `wavel.ko` |
| Compaq WL100 | `orinoco.ko` |
| ELSA AirLancer MC-11 | `wvlan.ko` |
| Intel PRO/Wireless 2100 Connection mini PCI | `ipw2100.ko` |
| Intel PRO/Wireless 2915ABG and 2200BG Network Connection mini PCI | `ipw2200.ko` |
| Lucent Technologies WaveLAN | `wvlan.ko` |
| Intersil PRISM2 11 Mbps | `wvlan.ko` |
| Lucent Technologies WaveLAN/IEEE Adapter | `orinoco.ko` |
| MELCO WLI-PCM-L11 | `orinoco.ko` |
| MELCO WLI-PCM-L11G | `orinoco.ko` |
| NCR WaveLAN | `wavel.ko` |
| Orinoco PC Cards | `orinoco.ko` |
| PLANEX GeoWave/GW-CF1110 | `orinoco.ko` |
| Planet WL3501 | `wl3501_cs.ko` |
| Prism54 PCI wireless | `prism54pci.ko` |
| Prism54 USB wireless | `prism54_usb.ko` |
| Realtek RTL8187 USB | `rtl8117` |
| Xircom CreditCard Netwave | `netwave_cs.ko` |
| ZCOMAX AirRunner/XI-300 | `orinoco.ko` |
| ZyDAS ZD1201 wireless LAN USB sticks | `zd1201.ko` |
| ZyDAS ZD2111 wireless LAN USB sticks | `zd2111rw.ko` |

### 表 15-2：支持的网卡

| 无线网络适配器 | 模块 |
| :--- | :--- |
| Broadcom 43xx | `bcm43xx` |
| Cabletron Roam 802.11 | `wavel.ko` |
| Compaq WL100 | `orinoco.ko` |
| Digital Roam/DS | `wavel.ko` |
| ELSA AirLancer MC-11 | `wvlan.ko` |
| Intel PRO/Wireless 2100 Connection mini PCI | `ipw2100.ko` |
| Intel PRO/Wireless 2915ABG and 2200BG Network Connection mini PCI | `ipw2200.ko` |
| Lucent Technologies WaveLAN | `wvlan.ko` |
| Intersil PRISM2 11 Mbps | `wvlan.ko` |
| Lucent Technologies WaveLAN/IEEE Adapter | `orinoco.ko` |
| MELCO WLI-PCM-L11 | `orinoco.ko` |
| MELCO WLI-PCM-L11G | `orinoco.ko` |
| NCR WaveLAN | `wavel.ko` |
| Orinoco PC Cards | `orinoco.ko` |
| PLANEX GeoWave/GW-CF1110 | `orinoco.ko` |
| Planet WL3501 | `wl3501_cs.ko` |
| Prism54 PCI wireless | `prism54pci.ko` |
| Prism54 USB wireless | `prism54_usb.ko` |
| Realtek RTL8187 USB | `rtl8117` |
| Xircom CreditCard Netwave | `netwave_cs.ko` |
| ZCOMAX AirRunner/XI-300 | `orinoco.ko` |
| ZyDAS ZD1201 wireless LAN USB sticks | `zd1201.ko` |
| ZyDAS ZD2111 wireless LAN USB sticks | `zd2111rw.ko` |

## 选择天线

如果你在距离彼此很的几台电脑之间建立无线局域网，你可能不需要额外的天线。然而，为了应对障碍和更远的距离，你可以为你的无线硬件添加室内或室外天线。

## 第15章：设置网络连接与局域网 657

在接下来的章节中，我将介绍与这些网卡兼容的不同类型的室内和室外天线。

## 使用室内天线

无线局域网卡内置的天线通常能够良好的开放区域计算机通信。如果无线局域网卡之间的直接视线被阻，额外的室内天线将非常有用。计算机可能被锁在储物室里，或卡在桌子下。一堆纸可能会抑制传输，而一块金属板可能会导致信号中断。一个能让传输信号远离网卡的小天线可能是解决这些问题的答案。
