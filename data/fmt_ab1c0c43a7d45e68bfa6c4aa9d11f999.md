
在企业环境中，公司通常安装双射频 AP，一个射电在 2.4 GHz 频段广播，另一个射电在 5 GHz 频段广播。如果每个射电都配置为广播相同的 SSID，那么 AP 就需要两个 BSSID；一个用于唯一标识每个射电上的 BSS。将此逻辑进一步推进，AP 广播多个 SSID 是很常见的。因此，如果每个射电都配置为广播 3 个 SSID（一个员工 SSID、一个游客 SSID 和语音 SSID），那么每个射电就需要 3 个 BSSID，该 AP 总共需要 6 个 BSSID（2.4 GHz 射电 3 个 BSSID， 5 GHz 射电 3 个 BSSID）。在此示例中，每个 AP 为连接到 DS 的每个物理以太网端口都需要 MAC 地址，以及额外的 6 个 MAC 地址来支持 6 个 BSSID。根据型号，Aruba AP 通常每个射电可以配置最多 8 或 16 个 BSSID。建议每个射电最多配置 3 或 4 个 SSID，因为每个额外的 SSID 都需要传输额外的信标（beacon）。以每个 SSID 每秒 10 个信标的速率，这将消耗该频率内宝贵的空中时间。

Aruba 并没有为每个 AP 分配一组 MAC 地址，而是为 AP 的 Ethernet 0 端口分配一个 MAC 地址。使用 Ethernet 0 MAC 地址，Aruba 根据所需的 BSSID 数量通过算法生成虚拟 MAC 地址。你可以执行 `show ap bss-table` 命令在控制器上显示所有 BSSID 地址，如下 CLI 输出所示。为了便于阅读并关注 BSSID 地址，以下输出中删除了某些信息列。

```
#show ap bss-table

fm (forward mode): T-Tunnel, S-Split, D-Decrypt Tunnel, B-Bridge (s-standard, p-
persistent, b-backup, a-always), n-anyspot

Aruba AP BSS Table

| bss | ess | ip | phy | ch/EIRP/max-EIRP | ap name |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 18:64:72:c7:87:00 | emp | 10.1.90.153 | g-HT ap | 11/6/25.5 | AP115-70-1 |
| 18:64:72:c7:87:10 | emp | 10.1.90.153 | a-HT ap | 44+/18/19 | AP115-70-1 |
| d8:c7:c8:89:72:80 | emp | 10.1.90.151 | g-HT ap | 6/6/21.5 | AP135-80-1 |
| d8:c7:c8:8c:ce:10 | emp | 10.1.80.150 | a-HT ap | 149+/18/22.5 | AP135-80-3 |
| d8:c7:c8:89:72:90 | emp | 10.1.90.151 | a-HT ap | 157+/18/22.5 | AP135-80-1 |
| d8:c7:c8:8c:ce:00 | emp | 10.1.80.150 | g-HT ap | 1/6/21.5 | AP135-80-3 |
| d8:c7:c8:89:82:40 | emp | 10.1.90.152 | g-HT ap | 6/6/21.5 | AP135-80-2 |
| d8:c7:c8:89:82:50 | emp | 10.1.90.152 | a-HT ap | 48-/18/22 | AP135-80-2 |

通道后跟 "*" 表示由于配置的通道不支持而选择了该通道。
"Spectrum" 后跟 "^" 表示本地频谱覆盖（Spectrum Override）生效。

Num APs:8
Num Associations:0
```

此输出的最右侧列显示 `ap_name`。每个唯一名称都是不同的 AP。在此示例中，注意每个 AP 都列出了两次：一次针对 2.4 GHz 射电，一次针对 5 GHz 射电，显示在 `phy` 列中，详情在 `ch/EIRP/max-EIRP` 列。

## 术语

当 802.11 标准在 1997 年首次通过时，它支持跳频频谱（FHSS）和直接序列频谱（DSSS）。随着额外的 802.11 修订案通过，每个修订案都增加了新的物理层（PHY）技术，从而提高了数据传输速率。802.11b 在 2.4 GHz 频段引入了高速率直接序列频谱（HR-DSSS），速率为 11 Mbps。802.11a 在 5 GHz 频段引入了正交复用（OFDM），速率为 54 Mbps。802.11g 在 2.4 GHz 频段引入了 OFDM，速率为 54 Mbps。802.11n 引入了高吞吐（HT），速率为 600 Mbps，能够在 2.4 GHz 和 5 GHz 频段传输。802.11ac 引入了极高吞吐（VHT），速率为 9.3 Gbps，但它仅在 5 GHz 频段运行。尽管 802.11ac 的速率定义为 9.3 Gbps，但行业实现的速率要慢得多。在引入这些技术时，行业通常通过它们的名称进行引用。为了进行类比，并不是所有的 AP 都是这样的。同样，802.11a 是一种 5 GHz 技术，在引入 802.11a 时，它是使用 5 GHz 频段的唯一 Wi-Fi 技术。然后，802.11n 支持 2.4 GHz 和 5 GHz 频率；因此引用 802.11n 可能意味着这两个频段之一，这可能会引起混淆。

表 1-1：802.11 常用引用

| 修订案 | 支持 |
| :--- | :--- |
| 802.11g | 支持 802.11b 或 802.11g 的 2.4 GHz |
| 802.11g/n | 支持 802.11b、802.11g 和 802.11n 的 2.4 GHz |
| 802.11g-HT | 与 802.11g/n 相同 |
| 802.11a | 仅支持 802.11a 的 5 GHz |
| 802.11a/n | 支持 802.11a 和 802.11n 的 5 GHz |
| 802.11a-HT | 与 802.11a/n 相同 |
| 802.11a-VHT | 支持 802.11a、802.11n 和 802.11ac 的 5 GHz |

以下 CLI 输出中的 `phy` 列显示了射电引的一些示例。为了便于阅读，输出中删除了某些信息列。

```
#show ap bss-table

fm (forward mode): T-Tunnel, S-Split, D-Decrypt Tunnel, B-Bridge (s-standard, p-
persistent, b-backup, a-always), n-anyspot

Aruba AP BSS Table

| bss | ess | ip | phy | ap name |
| :--- | :--- | :--- | :--- | :--- |
| 9c:1c:12:88:57:a3 | guest90 | 10.1.90.150 | g-HT | AP225-90-1 |
| 9c:1c:12:88:57:a0 | employee | 10.1.90.150 | g-HT | AP225-90-1 |
| 9c:1c:12:88:57:b2 | wps2psk | 10.1.90.150 | a-VHT | AP225-90-1 |
| 9c:1c:12:88:57:b1 | camera | 10.1.90.150 | a-VHT | AP225-90-1 |
| 9c:1c:12:88:57:b3 | guest90 | 10.1.90.150 | a-HT | AP225-90-1 |
| 9c:1c:12:88:57:a2 | wps2psk | 10.1.90.150 | g-HT | AP225-90-1 |
| 9c:1c:12:88:57:a1 | camera | 10.1.90.150 | g-HT | AP225-90-1 |
| 9c:1c:12:88:57:b0 | employee | 10.1.90.150 | a-VHT | AP225-90-1 |
```

## ArubaOS 架构

- 初始（主）控制器
- AP 启动过程
- GRE 隧道说明
- 添加本地控制器
- 多控制器 AP 启动过程
- AP 转发模式
- GRE/隧道
- 桥接 (Bridge)
- 解密隧道 (Decrypt-Tunnel)
- 分流隧道 (Split-Tunnel)

## 第 2 章了解 ArubaOS 环境

**在本章中，你将学习以下内容：**

本章将向你介绍 Aruba 操作系统 (ArubaOS) 的架构。本章不会教你如何一步步配置网络，而是将从概念上解释其工作机制。随着代码的每次新发布，细节可能会发生，但概念可能会保持不变。在本书的其他章节中，你将学习如何配置不同的组件。
