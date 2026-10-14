
如果你无法通过网卡面板（Network Card panel）配置你的无线局域网卡，可能可以使用来自 Atheros（www.atheros.com）、MadWiFi 项目（www.madwfi.org）或 Ndiswrapper 项目（ndiswhisper.sourceforge.net）的驱动程序和工具让无线网卡工作。

如果你需要准确确定你拥有哪种无线网卡，请尝试以下操作：

```bash
# lspci | grep -i wireless 搜索无线 PCI 卡
01:09.0 Network controller: Broadcom Corporation BCM4306 802.11b/g
无线 LAN 控制器 (rev 03)
```

假设你的无线网卡已运行，`wireless-tools` 软件包中包含一些实用的命令，可以查看和更改无线网卡的设置。特别是 `ifconfig` 命令可以帮助你处理无线局域网接口。以下命令将扫描你的网络接口以支持的无线网卡，并列出它们的当前设置：

```bash
# ifconfig
eth0 no wireless extensions.*
eth1 IEEE 802.11-DS ESSID:"* Nickname:HERMES I"
Mode:Managed Frequency:2.457 GHz Access Point:Not-Associated
Bit Rate:11 Mb/s Tx-Power=15 dbm Sensitivity:1/3
Retry limit:4 RTS thr:off Fragment:off
Encryption key:off
Power Management:off
```

无线接口可能命名为 `wlanX` 或 `ethX`，取决于使用的硬件和驱动程序。在无线接口上建立链路后，你可能获得更多信息：

```bash
# ip link set eth up
# ifconfig
eth1 IEEE 802.11-DS ESSID:"* Nickname:HERMES I"
Mode:Managed Frequency:2.457 GHz Access Point:None
Bit Rate:11 Mb/s Tx-Power=15 dBm Sensitivity:1/3
Retry limit:4 RTS thr:off Fragment:off
Encryption key:off
Power Management:off
Link Quality:0/92 Signal level=134/153 Noise level=134/153
Rx invalid nwid:0 Rx invalid crypto:0 Rx invalid frag:0
Tx excessive retries:0 Invalid misc:0 Missed beacon:0
```

设置可以通过几种方式进行修改。以下是使用 `ifconfig` 修改你的无线接口设置的方法。在以下示例中，我们对名为 `wlan0` 的无线接口进行操作。这些操作可能支持或不支持，取决于你使用的无线网卡和驱动程序：

```bash
# ifconfig wlan0 essid "MyWireless" 将 ssid 设置为 MyWireless
# ifconfig wlan0 channel 3 将通道设置为 3
# ifconfig wlan0 mode Ad-Hoc 从 Managed 模式更改到 Ad-Hoc 模式
```

```bash
# iwconfig wlan0 any any
# iwconfig wlan0 sens -50
# iwconfig wlan0 retry 20
# iwconfig wlan0 key 1234-5555
```

使用任何可用的接入点

将灵敏度设置为 -50

将 MAC 重传次数设置为 20

将加密密钥设置为 1234-5555

`ssid` 有时被称为网络名称（Network Name）或域 ID（Domain ID）。使用它作为通用名称来识别你的无线网络。设置通道允许你的无线局域网在该通道上运行。

在 Ad-Hoc 模式下，网络由相互连接的客户端组成，没有中央接入点。在 Managed/Infrastructure 模式下，通过将 `ap` 设置为特定的 MAC 地址，你可以强制网卡连接到该地址的接入点，或者将 `ap` 设置为 `any` 并允许连接到任何点。

如果你遇到性能问题，可以将灵敏度（`sens`）调整为负值（代表 dbm）或正值（可能是百分比或厂商设置的灵敏度值）。如果遇到重传失败，可以增加 `retry` 值，以便网卡在失败前发送更多数据包。

使用 `key` 设置加密密钥。你可以输入十六进制数字（XXXX-XXXX-XXXX-XXXX 或 XXXXXXXX）。通过在密钥前加上 `s:`，你可以输入 ASCII 字符串作为密钥（例如 `s:My927pwd`）。

## 拨号调制解调器

尽管高速 DSL、电缆调调器和无线局域网硬件已广泛可用，但有时电话线和调制解调器仍然连接互联网的唯一方法。Linux 提供了图形界面和命令行工具来配置和与调制解调器通信。

与 SUSE 中的其他连接一样，拨号调制解调器连接可以使用网络设备（Network Devices）面板配置。大多数外部串口调制解调器无需特殊配置即可在 Linux 下工作。大多数硬件 PCI 调制解调器也可以。然而，许多软件调制解调器（有时称为 Winmodems）在 Linux 中无法工作（某些可以使用特殊驱动配置，被称为 Linmodems）。

为了避免为了让 Winmodem 在 Linux 中工作而经历复杂的扭折，我们建议购买一个连接到外部串口的调制解调器或硬件调制解调器。如果你想尝试自己配置 Winmodem，请参考 Linmodems 网站（www.linmodems.org）。

如果你无法通过网络设备面板让你的调制解调器工作，可以尝试一些命令。首先尝试使用 `wvdialconf` 命令扫描串口端口上的任何调制解调器并创建配置：

```bash
# wvdialconf /etc/wvdial.conf 扫描串口端口上的任何调制解调器并创建配置
```

扫描你的串口端口以查找调制解调器：

```bash
# wvdialconf /etc/wvdial.conf 
```

扫描你的串口端口以查找调制解调器：

```bash
# wvdialconf /etc/wvdial.conf 
```

扫描你的串口端口以查找调制解调器：

```bash
# wvdialconf /etc/wvdial.conf 
```

扫描你的串口端口以查找调制解调器：

```bash
# wvdialconf /etc/wvdial.conf 
```

扫描你的串口端口以查找调制解调器：

```bash
# wvdialconf /etc/wvdial.conf 
```

扫描你的串口端口以查找调制解调器：

```bash
# wvdialconf /etc/wvdial.conf 
```

# 第 11 章：管理网络连接

`minicom`。（你需要安装 `minicom` 软件包。）第一次运行 `minicom` 时，使用 `-s` 进入设置模式：

```
# minicom -s
Create your modem settings
+-[configuration]-+
| Filenames and paths |
| File transfer protocols |
| Serial port setup |
| Modem and dialing |
| Screen and keyboard |
| Save setup as dfl |
| Save setup as.. |
| Exit |
| Exit from Minicom |
+
```

让我们暂时忘记调制调器，假设你想使用 COM1 连接到一个波特率为 9600 的 Cisco 设备。使用方向键导航到 **Serial port setup**（串口设置）并按回车选择它。按 `a` 编辑串口设备并将其更改为 `/dev/ttyS0`。接下来，按 `e` 进入设置，当 **Comm Parameters**（通信参数）出现时，按 `e` 设置为 9600。要切换硬件流控，按 `f`。按回车返回配置屏幕。

要更改调制调器参数，选择 **modem and dialing**（调制调器与拨号）。然后执行清除、重置、连接和挂起字符串（这些不适用于我们配置的 Cisco 设备）。完成后，从配置屏幕上选择 **save setup as dfl**（保存设置为默认）并选择 **Exit**（退出，而不是 Exit from Minicom）。

你现在处于 `minicom` 终端中。要了解更多如何使用 `minicom`，在完成操作后，按 `Ctrl+a`，然后按 `x` 退出 `minicom`。

> 警告！不要在具有默认按键绑定的 `screen` 环境中运行 `minicom`！否则，`Ctrl+a` 会被 `screen` 拦截！如果你不小心这样做，请切换到另一个 `screen` 窗口并输入：`killall minicom`。

# 检查名称解析
