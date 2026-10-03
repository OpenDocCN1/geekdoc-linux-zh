
在这里，我取消了 `chain_len` 的注释并给它赋值为 3，这意味着 proxychains 现在将从我的 `/etc/proxchains.conf` 文件中使用三个代理，随机选择它们，并在代理宕机时移动到下一个。注意，虽然这种方法确实增强了你的匿名性，但它增加了你在线活动的延迟。

现在你已经知道如何使用 proxychains 了，我说“相对”的，因为在国家安全局（NSA）和联邦安全局（FSB）监视我们的在线活动的情况下，没有万无一的方法可以保持匿名——但通过 proxychains 的帮助，我们可以让检测变得困难。

## 关于安全

关于代理安全的最后一点，请务必明智地选择你的代理：proxychains 好坏取决于你使用的代理。如果你打算保持匿名，正如前面提到的，请不要使用免费代理。黑客应该使用可以信任的付费代理。事实上，免费代理可能在出售你的 IP 地址和浏览历史。正如著名的密码学家和安全专家 Bruce Schneider 曾经说过的：“如果某东西是免费的，那么你不是客户；你是产品。”换句话说，任何免费产品都可能在收集你的数据并出售。他们为什么要免费提供代理呢？

虽然你的代理 IP 地址离开了匿名性范围，但监控机构还有其他方法可以识别你。例如，代理所有者知道你的身份，在具有司法管权的间谍或执法机构的压力下，可能会为了保护自己的业务而提供你的身份。意识到代理作为匿名来源的局限性很重要。

## 虚拟专用网络

使用虚拟专用网络（VPN）可以是保持网络流量相对匿名和安全的有效方法。VPN 用于连接到虚拟网络，在你的设备和互联网之间创建一个加密隧道。

虽然你的代理 IP 地址离开了匿名性范围，但监控机构还有其他方法可以识别你。例如，代理所有者知道你的身份，在具有司法管权的间谍或执法机构的压力下，可能会为了保护自己的业务而提供你的身份。意识到代理作为匿名来源的局限性很重要。

ProtonMail 是由瑞士 CERN 强对加速器设施的一群年轻科学家创立的。瑞士人在保护秘密方面有着悠久而传奇的历史（还记得你听过的那些瑞士银行账户吗？），而且 ProtonMail 的服务器位于欧盟，而该地区在个人数据共享方面的法律比美国严格得多。ProtonMail 不对基础账户收取费用，但提供低廉费用的高级账户。需要注意的是，当与非 ProtonMail 用户交换电子邮件时，邮件的部分或全部内容可能无法加密。欲了解更多详细信息，请参阅 ProtonMail 支持知识库。

## 总结

我们不断受到商业公司和国家情报机构的监控。为了确保你的数据和网络旅行安全，你需要实施本章讨论的至少一种安全措施。通过结合使用这些措施，你可以最大限度地减少你在互联网上的足迹，并保持数据高度安全。

## 练习

- 1. 运行 `traceroute www.hackers-arise.com`。你和你喜爱的网站之间出现了多少次跳转（hops）？
- 2. 下载并安装 Tor 浏览器。现在，像使用任何其他浏览器一样在互联网上匿名浏览，看看你是否注意到速度上有任何差异。
- 3. 尝试使用 `proxychains` 配合 Firefox 浏览器访问你喜爱的网站。
- 4. 探索本章列出的某些供应商提供的商业 VPN 服务。选择一个并测试试用。
- 5. 打开一个免费的 ProtonMail 账户并向 `occupytheweb@protonmail.com` 发送一封安全的问候。

## 14 理解与检查无线网络

从你的系统扫描并连接其他网络设备的能力是成为一名成功黑客至关重要的。随着 Wi-Fi (IEEE 802.11) 和蓝牙等无线技术成为标准，发现并控制 Wi-Fi 和蓝牙连接是关键。如果有人可以破解无线连接，他们就可以进入设备并访问机密信息。当然，第一步是学习如何找到这些设备。

在第 3 章中，我们查看了 Linux 中的一些基础网络命令，包括无线网络的一些基础知识，并承诺在第 14 章将介绍更多无线网络内容。正如所承诺的，在这里我们来检查 Linux 中两种最常见的无线技术：Wi-Fi 和蓝牙。

## Wi-Fi 网络

我们将从 Wi-Fi 开始。在本节中，我将向你展示如何找到、检查和连接 Wi-Fi 接入点。在此之前，让我们回顾基础 Wi-Fi 术语和技术，以帮助你更好地理解本章中许多查询的输出内容：

- **AP (接入点)**：无线用户连接以访问互联网的设备。
- **ESSID (扩展服务集标识符)**：这与我们在第 3 章讨论的 SSID 相同，但用于无线局域网中的多个 AP。
- **BSSID (基本服务集标识符)**：这是每个 AP 的唯一标识符，与设备的 MAC 地址相同。
- **SSID (服务集标识符)**：这是网络名称。
- **通道 (Channels)**：Wi-Fi 可以在 14 个信道中的任何一个（1 到 14）。在美国，Wi-Fi 限制在信道 1 到 11。
- **功率 (Power)**：你离 Wi-Fi AP 越近，功率越大，连接越容易被追踪。
- **安全 (Security)**：这是正在读取的 Wi-Fi AP 上使用的安全协议。Wi-Fi 有三种主要的安全协议。原始的等线隐私保护 (WEP) 有严重缺陷且易于破解。其替代品 Wi-Fi 保护访问 (WPA) 稍微安全一些。WPA2-PSK 更安全，并使用所有用户共享的共享密钥 (PSK)，被几乎所有的 Wi-Fi AP 使用（企业 Wi-Fi 除外）。在最近几年中，行业对新的 AP 采取了 WPA，这使得破解 Wi-Fi 密码变得更加困难。
- **模式 (Modes)**：Wi-Fi 可以以三种模式运行：管理 (managed)、主机 (master) 或监控 (monitor)。你将在下一节中学习这些模式的含义。
- **无线范围 (Wireless range)**：在美国，Wi-Fi AP 法律必须以 0.5 瓦的上限广播其信号。在该功率下，其正常范围约为 300 英尺（100 米）。高增益天线可以将此范围扩大到多 20 英里。
- **频率 (Frequency)**：Wi-Fi 设计运行在 2.4 GHz 和 5 GHz 上。现代 Wi-Fi AP 和无线网卡通常同时使用两者。

## 基础无线命令

在第 3 章中，你接触了基础 Linux 网络命令 `ifconfig`，它列出了系统上每个激活的网络接口并带有一些基础统计数据，包括（最重要的）每个接口的 IP 地址。让我们再次查看运行 `ifconfig` 的结果，这次重点关注无线连接。（请注意，如果你在虚拟机中运行 Kali，你需要一个外部 USB Wi-Fi 适配器，例如 Alfa 的适配器）。

```bash
ifconfig
eth0:BROADCAST,MULTICAST,UP,RUNNING  mt:1500  ether 00:...
        inet 192.168.1.10  netmask:255.255.255.0  broadcast:192.168.1.255
lo:BROADCAST,MULTICAST,UP,RUNNING  mt:65536
        inet 127.0.0.1  netmask:255.0.0.0
wlan0:BROADCAST,MULTICAST,UP,RUNNING  mt:1500  ether 00:...
        inet 192.168.1.15  netmask:255.255.255.0  broadcast:192.168.1.255
```

`ifconfig` 的输出显示了网络接口。要查看关于无线连接的详细信息，我们可以使用 `iwlist`。

```bash
iwlist wlan0 scan
wlan0  Scan completed
Cell 01 - Address:88:AD:43:75:B3:82
      ID="Hackers-Arise"
      Frequency:2412.0 MHz (MHz)
      Channel:1
      Frequency:2.412GHz (Channel 1)
      Quality=70/70 Signal=-38 dB
      Encryption:none
      SSID="Hackers-Arise"
```

`iwlist` 的输出包含了每个 MAC 地址 (BSSID)、频率、通道、质量、信号强度以及是否加密。

另一个用于管理 Wi-Fi 连接的非常有用的命令是 `nmcli`（网络管理器命令行界面）。提供网络接口（包括无线接口）的高级接口的 Linux 守护进程被称为网络管理器。通常，Linux 用户通过图形界面熟悉该守护进程，但也可以从命令行使用。

我们可以使用 `nmcli` 命令查看附近的 Wi-Fi AP 及其数据，就像我们之前用 `iwlist` 做的那样，但此命令提供了更多信息。我们使用的格式为 `nmcli dev wifi`，如下：

| SSID | MODE | CHAN | RATE | SIGNAL | BARS | SECURITY |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Hackers-Arise | Infra | 1 | 54 Mbits/s | 100 | | WPA1 WPA2 |
| Xfinity | Infra | 1 | 54 Mbits/s | 75 | | WPA2 |
| TPTV1 | Infra | 11 | 54 Mbits/s | 44 | | WPA1 WPA2 |

连接到网络。幸运的是，由于这是我们的 AP（接入点），知道密码是 12345678，所以输入以下命令：

```bash
kali> nmcli dev wifi connect Hackers-Arise password 12345678
wlan0 successfully activated with '39a45bf4-8a44-36f8-49beda6cb53b0'
```

尝试连接，你懂的，当你成功连接到该无线 AP 后，运行 `iwconfig` 查看发生了什么。这里是我从 Hackers-Arise 连接的输出：

```bash
kali> iwconfig
no wireless extensions

wlan0 802.11bg ESSID:"Hackers-Arise"
Mode:Managed Frequency:2.452GHz Access Point:00:25:9C:97:4F:48
Bit Rate=32 Mbps Tx-Power=20 dbm
retry limit:7 RTS:off Fragment:off
Encryption:off
Power Management:off
Link Quality=64/70 Signal level=-46 db
Rx invalid:0 Rx crypt:0 Rx invalid:0
Tx excessive:0 Invalid mis:13 Missed beacon:0

eth0 no wireless extensions
```

注意，你的 `iwconfig` 显示 ESSID 为 "Hackers-Arise"，且该 AP 运行在 2.452 GHz 的频率上。在无线网络（Wi-net）中，多个 AP 可能属于同一个网络，可能有许多 AP 组成 Hackers-Arise 网络。MAC 地址 00:25:9C:97:4F:48 正如你所想的，是我所连接的 AP 的 MAC 地址。Wi-Fi 网络使用的安全类型、它是运行在 2.4 GHz 还是 5 GHz、其 ESSID 是什么以及 AP 的 MAC 地址是什么，都是进行 Wi-Fi 攻击所需的关键信息。现在你已经知道了基础命令，让我们开始一些黑客攻击。

# 使用 aircrack-ng 进行 Wi-Fi 侦测

对于新手来说，最流行的利用之一是破解 Wi-Fi 接入点。如所述，在考虑攻击 Wi-Fi AP 之前，你需要目标 AP 的 MAC 地址 (BSSID)、客户端的 MAC 地址以及 AP 运行的通道。

我们可以使用 `aircrack-ng` 工具包中的更多工具来获取所有信息。我已经提到过这套 Wi-Fi 攻击工具几次了，现在是时候真正使用它了。这套工具包含在 Kali 的每个版本中，所以不需要下载任何东西。为了有效使用这些工具，你需要将无线网卡设置为**监听模式**（monitor mode），以便网卡能够看到通过的所有流量。监听模式类似于有线网络中的混杂模式（promiscuous mode）。要将无线网卡设置为监听模式，使用 `airmon-ng` 命令。该命令的语法简单：

```
sudo airmon-ng start <interface>
```

因此，如果你想将指定为 `wlan0` 的无线网卡设置为监听模式，输入以下内容：

```bash
kali> sudo airmon-ng start wlan0
```

发现可能导致问题的进程。如果 `airdump-ng`、`replay-ng` 或 `airmon-ng` 在短时间后停止，你可能需要分别运行 `airmon-ng kill`。在网卡处于监听模式的情况下，你可以访问无线适配器范围内的所有流量（标准范围约为 300 到 500 英尺）。注意 `airmon-ng` 会重命名你的接口：我的被重命名为 `wlan0`，你的可能不同。务必记住你无线接口的指定名称，因为你将在下一步中需要该信息。

现在我们将使用 `aircrack-ng` 工具包中的另一个工具从无线流量中查找数据。`airdump-ng` 命令用于捕获并显示来自广播 AP 以及任何连接到这些 AP 或位于附近的客户端的数据。语法非常直观：只需输入 `airdump-ng`，后跟你运行 `airmon-ng` 得到的接口名称即可：

```bash
kali> sudo airdump-ng wlan0
```

```
CH 9[ Elapsed: 28 s ] 
```

| BSSID | PWR | Beacons | #Data s | CH | ENC | CIPHER | AUTH | ESSID |
|---|---|---|---|---|---|---|---|---|
| 01:01:AA:BB:CC:22 | -1 | 4 | 26 | 10 | WPA2 | CCMP | PSK | Hacker-Arise |

| BSSID | Station | Pwr | Rate | Lost | Frames | Probe |
|---|---|---|---|---|---|---|
| (not associated) | 01:02:CC:DD:03:CF | | | | | |
| 01:01:AA:BB:CC:22 | A:44:7C:E5 | | | | | |

当你执行此命令时，你的无线网卡将从附近所有 AP 的无线流量中获取关键信息（列在下方）：

- **BSSID**：AP 或客户端的 MAC 地址
- **PWR**：信号强度
- **ENC**：用于加密传输的加密方式
- **Data**：数据吞吐量速率
- **CH**：AP 运行的通道
- **ESSID**：AP 的名称

注意 `airdump-ng` 将屏幕分为上半部分和下半部分。上半部分包含有关广播 AP 的信息，包括 BSSID、AP 功率、检测到的帧数、数据吞吐速率、通过无线网卡的包数、通道（1-14）、理论限制、加密协议、用于加密算法、认证类型以及 ESSID（通常称为 SSID）。在客户端部分，输出告诉我们客户端未关联（意味着它检测到了但未连接到 AP），而另一个已关联（意味着它连接到了该地址的 AP）。

现在你拥有了破解 AP 需要的所有信息！虽然这是本书的范围，但要破解无线 AP，你需要客户端 MAC 地址、AP MAC 地址、目标运行的通道以及一个密码列表。

为了破解 Wi-Fi 密码，你需要打开三个终端。在第一个终端中，你输入类似下面的命令，并指定客户端和 AP MAC 地址以及通道：

```bash
sudo airdump-ng -c 10 --ssid 01:01:AA:BB:CC:22 -w Hacker-ArisePSK wlan0mon
```

该命令使用 `-c` 选项捕获通道 10 的所有包。

在另一个终端中，可以使用 `airplay-ng` 命令踢掉（取消认证）任何连接到 AP 的用户，并强制他们重新认证，如下所示。当他们重新认证时，你可以捕获在 WPA2-PSK 四次握手中交换的密码哈希。密码哈希将出现在右上角的：

最后，在终端中输入以下内容：

```bash
sudo airplay-ng -a 01:01:AA:BB:CC:22 -c 10 wlan0mon
```

| PHY | INTERFACE | DRIVER | Chipset |
|---|---|---|---|
| phy0 | rt8117 | Realtek Semiconductor RTL8187 | |
| wlan0 | | | |

BlueZ 提供了许多简单的工具，用于管理和扫描蓝牙设备，包括以下工具：

- **hcitfig**：该工具的操作方式与 Linux 中的 `ifconfig` 非常相似，但它是针对蓝牙设备的。正如列表 14-1 所示，我已使用它启动了蓝牙接口并查询了设备的规格。
- **hcitool**：此查询工具可以为我们提供设备名称、设备 ID、类别和时钟信息，使设备能够同步工作。
- **hcidump**：该工具允许我们嗅探蓝牙通信，这意味着我们可以捕获通过蓝牙信号发送的数据。

使用蓝牙进行扫描和侦查的第一步是检查我们使用的系统蓝牙适配器是否被识别并启用——我们也可以将其用于其他设备。我们可以使用内置的 BlueZ 工具 `hcitool` 来实现此，如列表 14-1 所示。

```bash
kali> sudo hcitool
hci0: BR/EDR Bus: USB
BD Address: AE:60:58:F1:37 ACL MTU: 310:100 SCO: 64:8
UP RUNNING PSCAN INQUIRY
RX bytes: 131433 acl5 sco:10519 errors:0
TX bytes: 42881 acl5 sco:5081 errors:0
```

列表 14-1: 扫描蓝牙设备

如你所示，我的蓝牙适配器已被识别，MAC 地址为 10:AE:60:58:F1:37。该适配器被命名为 hci0。
