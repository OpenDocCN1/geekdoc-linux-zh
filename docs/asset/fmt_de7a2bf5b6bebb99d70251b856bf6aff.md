
#include <pcap.h>

`pcap_handle` `handle` = `pcap_open_live(interface,65536,1,100000,errbuf)`;

// 当发生错误时

if(`pcap_handle` == NULL)

{

  `fprintf(stderr,"Error in pcap_open_live: %s\n",errbuf)`;

  `cleanup_failure()`; // exits

}
```
这段代码显示了 Probember 工具打开了一个 pcap 接口，该接口将用于从该无线接口获取数据包。代码使用了通过 `pcap_open_live` 创建的句柄和 `pcap_next` 函数来提取从该无线接口接收的数据。随后的行检查在没有接收到任何内容时的错误：

```c
packet = pcap_next(pcap_handle, &hdr);
if(packet == NULL)
{
  fprintf(stderr,"No packets: %s\n", errbuf);
  cleanup_failure(); // exits
}
```

# 第 8 章：无线网络

在嗅探无线接口时需要理解的下一个重点是，无线接口需要处于监控模式（monitor mode）才能嗅探无线流量，无论是数据帧、管理帧还是控制帧。通过无线驱动程序收集的每个无线帧前面都添加了一个特殊的头部，报告了网卡（NIC）接收到帧时的信号电平、噪声水平和速率。根据无线驱动/固件的组合以及这些驱动程序，会添加不同的头部。识别所添加的头部类型非常重要，因为嗅探器需要知道数据包头部的结构以及如何处理它们。通常会添加三类型的头部：RadioTap 头部、WLAN-ng PRISM 头部和 WLAN-ng AVS 头部。为了能够在程序中区分这些添加到你的数据包中的头部，你可以使用 `pcap_datalink` 调用，其总结如下：

```c
#define DLT_PRISM_HEADER 1
#define DLT_IEEE80211_RADIO 2
#define DLT_IEEE80211_AVS 3
// PRISM Header
if (pcap_datalink(pcap_handle) == DLT_PRISM_HEADER)
{
    ..process PRISM header here
}
// AVS Header
if (pcap_datalink(pcap_handle) == DLT_IEEE80211_AVS)
{
    ..process AVS header here
}
// Radio Tap Header
if (pcap_datalink(pcap_handle) == DLT_IEEE80211_RADIO)
{
    ..process Radio Tap header
}
```

## Radiotap 头部结构

- `IEEE 802.11_RADIOTAP_LOCK_QUALITY` `u16`
- `IEEE80211_RADIOTAP_TX_ATTENUATION` `u16`
- `IEEE80211_RADIOTAP_DB_TX_ATTENUATION` `u16`

Radiotap 捕获头部的结构与其他两个头部不同之处在于，它是一个变长度头部，其字段是可选的。它通过位图切换来指示哪些字段存在，哪些字段不存在。

处理完捕获头部后，嗅探器代码将对无线帧剩余部分作为一个具有特定结构的框架进行处理。在此代码中，接收到的帧（去掉捕获头部后）被强制转换为一个管理结构：

```c
#define T_MGMT 0X0
#define ST_AUTH 0xB
#define FC_TYPE(fc) ((fc) > 2) & 0x3)
#define FC_SUBTYPE(fc) ((fc) > 4) & 0xF)
struct mgmt_header {
    u_int16_t fc;
    u_int16_t duration;
    u_int8_t da[6];
    u_int8_t sa[6];
    u_int8_t bssid[6];
    u_int16_t seq_ctrl;
};
// 从数据包中提取管理头部
mgmt_header = (struct mgmt_header_t *) packet;
if (FC_TYPE(mgmt_header->fc) == T_MGMT) { 处理管理无线帧的代码 }
if (FC_SUBTYPE(mgmt_header->fc) == ST_AUTH) { 处理身份验证请求帧的代码 }
```

`LORCON` 是 Loss of Radio Connectivity（无线电连接丢失）的缩写。它是由 Joshua Wright 和 Dragonn 编写的一组库。这些库在编写编写数据包注入工具时简化了编程人员的工作，因为它消除了处理多个无线芯片组的复杂性和错综性，避免了为应用程序中支持的每一个无线网卡（WNIC）编写特定代码的，因为每个 WNIC 的代码功能都不相同。

可以从 `http://802.11ninja.net/code/LORCON-current.tgz` 下载 `LORCON`。安装 `LORCON` 后，如果你想编写一个使用 `LORCON` 库的应用程序，你需要使用额外的库 `-lorcon` 来进行编译。

`LORCON` 暴露了一系列函数调用，任何将 `LORCON` 库编译到其代码中的应用程序都可以这些这些。通过使用 `LORCON` 库，应用程序开发人员无需编写特定驱动代码来处理不同驱动程序/芯片组注入数据包时的差异。这里展示的代码结构/格式说明了该库的能力，从展示如何建立接口到如何传输无线帧：

```c
#include <tx80211.h>
#include <tx80211_packet.h>
/* 初始化接口 */
if (tx80211_init(&in_tx, iface, drivertype) < 0) {
    处理错误的代码
}
/* 设置监控模式 */
if (tx80211_setmode(&in_tx, IW_MONITOR) < 0) {
    处理错误的代码
}
/* 切换到指定通道 */
if (tx80211_setchannel(&in_tx, channel) < 0) {
    处理错误的代码
}
/* 打开接口以获取套字 */
if (tx80211_open(&in_tx) < 0) {
    处理错误的代码
}
/* 发送数据包 */
if (tx80211_txpacket(&in_tx, &in_packet) < 0) {
    处理错误的代码
}
```

本书还附带 Promemaber，这是一个 GPL 许可的无线客户端检测和无线配置识别程序，它利用了 `LORCON` 库。Promemaber 也可以在 `http://securitystartshere.org/page-downloads.htm` 获取（那里也存放了与 Promemaber 配的 `LORCON` 库副本）。

## 防御审计/黑客平台组装

结论：从技术角度来看，你无法阻止别人为了审计或黑客目的组装工具包，就像你无法阻止某人生产叉子一样。防止嗅探器等工具的创建、审计平台的组装以及代码的编写是不可能的。要阻止组装黑客平台的手，你必须亲临现场防止其执行构建工具的物理动作、在键盘上打字或进行组装活动。

守护者防止工具开发、编译和组装最明显的方法是实施禁止生产或编译平台的法律。然而，即使有了这些法律，也无法阻止某人生产或编译这些平台。执法完全是另一回事，特别是涉及跨境案件时。

在编写时的大多数司法管辖区，创建、编译或组装平台本身并不违法（也不应该被判定为违法！），尽管像德国等国家正试图立法将其定为非法。真正重要的是所创建的平台或工具包的目的。以我们的例子来说，任何人都可以使用禁用叉子来吃饭或戳人的眼睛。那么，这是否意味着我们必须禁止叉子呢？

## 无线基础设施审计

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 9 |
| 风险等级 | 8 |

在编写时的大多数司法管辖区，平台的创建、编译或组装本身并不违法（也不应该被判定为违法！），尽管德国等国家正试图将其定为非法。真正重要的是所创建的平台或工具包的目的。在审计网络时，你需要确保无线网卡可以执行。这些活动分类如下：

- 频谱分析
- 设备识别
- 加密破解
- 射频边界
- DoS/劫持

### 频谱分析

在本章之前，我们讨论了频谱分析的重要性。从审计人员/黑客的角度来看，理解频谱将有助于你识别超出范围外的设备。审计人员现在可以通过该频率识别属于组织的 AP 列表。

如果检测到特定频率上的活动，审计人员需要确保使用的无线设备可以接收和发送，进入下一阶段。

### 设备识别

在此阶段，审计人员将通过查看层信息开始进行设备和协议分析。

`Kismet` 常用于执行设备识别。如本章所述，`Kismet` 是一种 802.11 无线网络检测器和嗅探器，具有入侵检测能力。它可以与任何支持射频监控（RFMON）模式的 WNIC 配合工作，取决于 WNIC 的容量。

`Kismet` 的运行主要通过其配置文件 `Kismet.conf` 控制。文件中最重要的配置设置是指定 `Kismet` 的源。`Kismet` 中的源告诉 `Kismet` 使用哪种特定类型的 WNIC，因为不同的驱动程序使用不同的方法报告信息。支持的各种 WNIC/驱动组合及其相应的源条目可以在 `Kismet` 的 README 文件中的“Capture Sources”部分找到。

`Kismet` 不仅允许审计人员识别到的无线 AP 的 SSID（在 `Kismet` 文档和 GUI 中引用），还能获取与每个检测 AP 相关的信息列表，例如 BSSID、AP 传输频率、信号强度、使用的加密方案、IP 范围识别、支持的速率以及连接的无线客户端。审计人员现在可以通过它们的 SSID、BSSID、加密方案以及有时的信号强度识别属于组织的 AP 列表。然而，审计人员不应仅依赖 `Kismet` 界面提供的信息，就像他们不应仅使用其他工具一样。他们应该学习读取 `Kismet` 转储的数据包，并通过对比 `Kismet` 显示的信息与实际捕捉并写入文件的帧来确定 `Kismet` 输出的准确性。

除了 `Kismet` 之外，还可以使用 `Airdump-ng`（`Aircrack-ng` 工具套的一部分，位于 `http://www.aircrack-ng.org/doc.php`）来交叉验证关键信息是否

## Kismet 图形界面示例

| 网络列表 (SSID) | 信道 | 数据包 | 标志 | IP 范围 | 大小 | 信息 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| - 隐藏 ssid | A N 001 | 89 | | 0.0.0.0 | 08 | 数据包 |
| - 隐藏 ssid | A N 001 | 107 | | 0.0.0.0 | 08 | 客客 |
| - 隐藏 ssid | A N 001 | 15 | | 0.0.0.0 | 700 | 加密 |
| - 隐藏 ssid | A U 011 | 77 | | 0.0.0.0 | 08 | 留 |
| - 隐藏 ssid | A N 001 | 0 | | 0.0.0.0 | 08 | 0 |
| tinksys_SES_45843 | A N 006 | 2 | | 0.0.0.0 | 08 | 噪声 |
| laptop | A N 001 | 3 | | 0.0.0.0 | 08 | 7 |
| vishal-home | A N 008 | 1 | | 0.0.0.0 | 08 | 丢弃 |
| | | | | | | 7 |
| | | | | | | 包/秒 |
| | | | | | | 7 |
| wifi10 | | | | | | 2 |
| | | | | | | 已用时间 |
| | | | | | | 00:00:51 |

警报：从 00:16:B6:63:DF 探测到长度为 0 的 SSID 探测响应
警报：从 00:16:B6:63:DF 探测到长度为 0 的 SSID 探测响应
警报：从 00:16:B6:63:DF 探测到长度为 0 的 SSID 探测响应
电池：：100%

图 8-21 `Kismet` 的图形界面

由 `Kismet` 识别的确实准确且可靠。这是一个使用一个工具来验证另一个工具观察结果的示例。

### 破解加密

在审计的这一阶段，审计人员手持 AP 列表及其各自的加密方案，尝试针对每个 AP 破解目标组织所使用的加密方案。

有线等效隐私保护 (`WEP`) 是在 802.11b 无线标准引入时实施的首种加密标准。直到最近，许多 AP 仅出于链路加密的目的而支持 `WEP`。即使对于那些能够支持改进型帧加密方案的设备，`WEP` 仍然被广泛使用。`WEP` 加密实现中的缺陷已被大量记录，其中决定性的解释来自 Fluhrer、Mantin 和 Shamir 在 2001 年写的一篇论文《RC4 密钥调度算法的缺陷》。

第一代 `WEP` 破解工具（如 `Airsnort` 或 `Dwecrack`）完全依赖于捕获的帧数量，这些帧中包含带有弱性（即有趣的）初始化向量（IVs）的加密数据。因此，审计人员必须花费很长时间来破解无线数据包（大约 1000 万个加密包），这些第一代工具才能发现正在使用的 `WEP` 密钥。

## 破解暴露的 Linux：Linux 安全秘密与解决方案

有时在 2004 年，引入了一种 `WEP` 统计密码分析攻击方法，大大减少了破解 `WEP` 密钥所需的帧数。`Aircrack-ng` 是这种第二代工具的示例，它结合新技术与改进的 Fluhrer-Martin-Shamir 技术，使破解快得多。使用 `Aircrack-ng`，你不再需要捕获数百万帧，只需要几十万具有唯一 IV 的帧即可。

`Aircrack-ng` 套件包含的 `Airodump-ng` 是一种嗅探工具，它旨在与 `Aircrack-ng` 协同工作。`Airodump-ng` 的输出可以输入 `Aircrack-ng`，后者可以在 `Airodump-ng` 捕获帧的同时执行同步破解攻击。以下输出显示了正在运行的 `Airodump-ng` 实例：

```
usage: airodump-ng <interface> <output prefix> [channel] [IVs]
```

指定 0 为信道以便在 2.4 GHz 信道之间跳跃。
将可选的 IVs 标志设置为 1 以仅保存捕获的 IVs - 结果文件仅对 `WEP` 破解有用。

如果 `gpsd` 守护正在运行，`airodump-ng` 将检索并以文本格式保存当前的 GPS 坐标：

```
[ CH 7 ] BAT: 1 hours 13 mins ][ 2006-10-23 14:32 ]
```
