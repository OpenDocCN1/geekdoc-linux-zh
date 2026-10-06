
从现实角度来看，整个 802.11 规范必须重写，重点关注加密帧头和/或对帧发送者执行某种双向认证/验证。然而，这是 IEEE 需要解决的问题，而且在可预见的未来，针对 IEEE 802.11 规范中管理和控制帧的攻击可能会继续并取得相当程度的成功。

# 第 8 章：无线网络

## 无线审计活动与程序

本节涵盖了你在对组织的无线暴露进行审计时，至少应该开展的各种活动。这些活动与执行基于 OSSTMM 的安全测试兼容。虽然攻击者不需要任何无线策略，但在审计期间模拟黑客活动的技术性无线审计员是需要这些，而且作为他们审计的一部分，他们必须处理组织政策，因此为了完整性，这些内容也包含在内。

### 审计无线策略

安全策略是成功的信息安全计划最重要的支柱之一。安全策略在管理组织预期状态方面起着至关重要的作用。尽管如此，无线策略可能是最被忽视的领域之一。许多组织总是忽视这个问题，因为他们觉得不需要它。然而，安全策略的存在在技术上并不能解决通过无安全介质连接的问题，它为实施必要的安全措施提供了一个整体框架，并允许对违规行为进行制裁。如果组织在其物理范围内实施了任何形式的无线基础设施，其无线策略、程序和指南必须扩展到许多可能被忽视的领域。这种立场应明确定义在其物理范围内对任何无线技术的使用。除了常见的 AP 类型设备外，还以无线功能笔记本电脑、PDA 和手机的形式存在。

安全策略是成功的信息安全计划最重要的支柱之一。安全策略在管理组织预期状态方面起着至关重要的作用。

* 访问策略
* 身份认证策略
* 审计责任策略
* 可用性
* 系统和网络维护策略
* 获取策略
* 违规报告
* 审计策略

### 构建基于 Linux 的审计/攻击平台

| 流行程度: | 7 |
| 简单易性: | 6 |
| 影响: | 10 |
| 风险评分: | 8 |

打开任何无线审计/黑客笔记本电脑，可能会发现一些对于执行成功的无线审计必不可少的软件和硬件工具。这些将在后续节中描述。

### 无线嗅探器

所有可用的无线嗅探器可以分为大类：被动嗅探器和探测嗅探器。这两类之间的区别在于被动嗅探器不发送任何流量。它们静静地接收只要无线网卡在 RFMON 模式下运行就能到的无线帧。

相反，探测嗅探器通过主动发送探测包来检测 AP。就此而言，无线站为其配置文件中设置的无线网络发送探测请求帧，并针对周围可能的任何无线网络发送探测帧。听到这些探测请求帧的 AP 将响应探测响应。探测嗅探器也使用这种技术，通过探测周围的 AP，并通过探测响应接收有关所发现 AP 的信息（例如 SSID、信号强度、噪声水平、工作信道和支持的数据以及加密能力）。

被动嗅探器的示例包括 `Kismet`、`Airdump-ng` 和 `Prismstbler`，而探测嗅探器的示例包括 `Wellenreiter` 和基于 Windows 的 `Netstumbler` 工具。

## 无线帧注入器

无线帧注入器允许攻击者自定义其发送的无线帧。例如，他们可以伪造一个取消认证无线帧（deauthentication frame），使其看起来源自接入点（AP），从而将连接到 AP 的无线客户端强制断开连接。

包注入工具可以构造几乎任意类型的 802.11 帧。某些工具可以通过注入信标帧（beacon frames）、探测帧（probes），甚至是认证和关联帧来模拟真实的 AP，欺骗无线客户端认为附近有一个合法的 AP。包注入器的示例包括 `Airplay-ng`、`Proemacker`、`Omerta`、`Void11`、`WLAN-Jack`、`FATA-Jack` 和 `File2Air`。

## WEP/WPA-PSK 破解器

直接针对无线加密破解的工具类专门针对 WEP 和 WPA-PSK。在 WEP 破解领域，工具包括 `WEPCrack`、`Aircrack-ptw-ng` 和 `Airrack-ng`。这些工具依赖攻击者从目标网络收集足够的 WEP 加密数据帧，以便将其传递给如 `Airrack-ng` 这样的破解程序。数据帧的数量取决于所使用的破解方案。较新的 Pychkine-Tews-Mann 方法仅需 40,000 到 80,000 个帧，而 `Airrack-ng` 中的另一种 KoRek 方法则需要 500,000 到 100 万个数据帧。

对于 WPA-PSK 破解，这些工具运行 `PBKDF2` 或基于密码的密钥派生函数 v2.0 数学公式，主密钥用于创建由 SSID 和 SSID 长度以及密码生成的会话密钥（256 位密钥）。用于实际数据加密的临时会话密钥的派生和建立通过四次握手完成，除非授权客户端正尝试与 AP 关联，否则无线嗅探器可以轻松捕获四次握手，并对密码进行离线字典攻击。工具示例包括 `Cowpatty` 和 `Airrack-ng v0.7`。

## 无线中间人攻击 (MITM)

由于无线客户端与 AP 之间存在真空，中间人攻击（MITM）非常普遍且容易实现。

在此类攻击中，工具被用于自动化 MITM 设置过程的大部分步骤。这些工具通常将无线卡设置为监控模式（此前在“黑客设置：Linux 原生芯片组和驱动程序”中介绍过），导致无线网卡（WNIC）激活并响应无线客户端对网络的探测。随后，它会建立 DHCP 服务器、HTTP 服务器和 DNS 服务器，欺骗客户端认为它们正通过合法的 AP 连接到网络服务。

在某些情况下，工具会通过与该网络的次级连接将所有客户端流量导向真实的无线网络，从而使攻击者能够捕获目标客户端的每一个无线帧（因为攻击者充当 AP 本身，不会错过任何帧，因为所有客户端帧都会发送）。无线 MITM 工具的良好示例是 `Airsnarf`（配合取消认证/关联工具使用效果达到最大）。

## 无线客户端审计

在无线审计方面，今天没有哪个机构在进行任何形式的无线客户端审计之前会声称其物理场所内没有部署无线功能。即使机构执行“无无线策略”，如今市面上几乎所有的便携计算设备都带有某种无线功能，攻击者可以使用本章描述的工具对其进行利用。

内置在这些便携设备中的无线芯片组在未使用时经常被处于不安全的“开启”状态。可以使用 `Probemapper`、`Karma` 和 `Hotspot` 等工具在客户端开启时“欺骗”其连接到自己。当这些客户端连接到各个组织的有线网络时，攻击者创建的无线通道可以作为到有线网络的桥接，从而完全破坏无线客户端连接的内部网络。

攻击无线客户端领域的最新进展包括这些无线设备的驱动程序缺陷，允许攻击者只要目标设备开启，即可在这些客户端上执行恶意代码。尽管在编写本文时此类工具尚未公开发，但可能很快就会有人开发并向公共领域发布利用该漏洞的工具。事实上，WEP 通信下行漏洞（我们将在本章结尾详细介绍）也可以被任何具有主机模式能力的无线网卡的人利用，通过利用 Windows Centro 驱动程序中的关联过程处理缺陷，对具有 WEP 加密配置的 Windows 平台无线客户端发起不安全的连接。此外，用于发现这些设备驱动程序缺陷的无线模糊器（wireless fuzzers）也已公开于世。

## 无线模糊器

如上一节所述，无线模糊器有助于发现在 2006 年 DefCon 等几次安全会议上公布的各种设备驱动程序级缺陷。

无线模糊器本质上是产生一系列无线帧，并以配置的速度和数量向无线设备发送的工具。这允许操作员发现这些设备如何处理“畸形”无线数据包。无线模糊器的示例是一个名为 `Fuzz-e` 的工具，它是 `Airbase` 软件包的一部分，可以从 `http://www.802.11mercenary.net` 获取。

## 无线指纹识别

无线安全领域的一个较新进展是指纹识别。指纹识别工具的一个早期示例是 `Johnny`。

### 专业无线审计 LiveCD

大多数用于审计的工具最初是为 Linux 设计的，然后移植到 Windows。幸运的是，有一个工具通过将整个操作系统和各种工具压缩到一张 CD 中解决了这个问题。这类工具通归为 LiveCD，因为整个操作系统和工具环境在 CD 上是“现场”运行的。你只需要将 CD 驱动器并启动即可。

`OS Assistant` 可以在 `http://securitystarts.org` 免费下载。

该工具包具有以下功能：

- 基于 CD 的工具包专门为无线审计设计。
- 支持对 802.11 (WiFi)、蓝牙和 RFID 技术进行审计/黑客。
- 菜单布局和界面针对用户效率和易用性进行了优化（这意味着你不需要到处寻找条目）。
- 所有工具都位于 `/usr/local/apps`，便于访问日志或转储文件。你不需要在笔记本电脑上安装任何软件或修改硬盘。
- 你可以插入 U 盘来保存转储、日志和文件。
- `ActivityMap` 帮助系统旨在帮助家庭和 SOHO 配置对自己的网络进行基础审计。
- CD 自身以及工具包下载网站还提供了 FAQ 和硬件/软件文档。
- 该工具免费下载和使用！

软件工具包包含 GPL 和免费使用的软件，任何人都可以出于合法目的使用，例如帮助对组织的 WLAN 进行渗透测试，或测试家庭网络的漏洞。

你以 `.iso` 格式下载 LiveCD。下载 `.iso` 镜像后，可以使用任何 CD 刻录软件（如 Linux `K3B` 或其他能够刻录 `.iso` 的软件）将镜像写入标准的 700MB/80 分钟 CD 中。

一旦你启动 CD 并进入工具包界面，基于 Web 的界面会自动加载。除了对工具包原理和用途的简要说明外，它还允许用户选择是否运行 `ActivityMap` 帮助系统。

用户在执行某些操作时，例如更改无线卡的 MAC 地址以进行无线帧注入。

`OSWA-Assistant` 工具包的一个新新增功能是 `MoocherHunter` 无线黑客/蹭用者跟踪软件（参见 `http://moochunter.securitystarts.org`）。在适当硬件的支持，该软件可以帮助执法人员和无线网络管理员跟踪可能接入安全和非安全无线网络的未经授权用户。根据定义，蹭用者（moochers）想要使用服务，因此他们面临着选择：要么蹭用并暴露自己的身份，要么不蹭用。该工具仅在特殊许可协议下作为 `OSWA-Assistant` 的部分提供。

### 编写你自己的无线软件

除了使用他人编写并发表的工具外，攻击者可能还需要编写自己的自定义工具。以下内容强调了在编写无线工具时需要注意的一些重要要点。

#### Libpcap

在开发无线工具时，最需要熟悉的代码库之一是 `Libpcap` 库。它最初开发于劳伦斯·伯克利实验室，目前由维护 `Tcpdump`（命令行数据包捕获工具 `http://tcpdump.org`）的同一组人员维护。在嗅探工具中使用 `Libpcap` 库使得从程序员的角度来看，它是许多编码的必需品，使其在编写工具时成为一种不可或缺的东西。

```c
#include <pcap.h>
pcap_handle = pcap_open_live(interface,65536,1,1000000,errbuf);
// 当发生错误时
if (pcap_handle == NULL)
{
    fprintf(stderr,"Error in pcap_open_live: %s\n", errbuf);
    cleanup_failure(); // exits
}
```

这段代码显示了 `Probemapper` 工具打开了一个 pcap 接口，该接口后续将用于从该无线接口获取数据包。后续代码使用通过 `pcap_open_live` 创建的句柄和 `pcap_next` 函数调用来提取无线接口接收的数据。随后的三行会在未接收到任何内容时检查并报告错误。

```c
pcap = pcap_next(pcap_handle, &hdr);
if (pcap == NULL)
{
    fprintf(stderr,"No packets: %s\n", errbuf);
    cleanup_failure(); // exits
}
```

在嗅探无线接口时需要理解的下一个重点是，无线接口必须设置为监控模式（monitor mode），RFMON 才能嗅探无线流量，无论是数据帧、管理帧还是控制帧。通过无线驱动程序收集的每个无线帧前面都有一个特殊的头部，报告无线网卡（WNIC）接收帧时点的信号电平、噪声水平、频率和速率信息。不同的无线驱动/固件组合会附加不同的头部，在某些情况下，还取决于这些驱动程序/固件的设置。识别所附加的头部类型非常重要，因为嗅探器的代码必须能够识别被捕获数据包的结构以及如何相应地对其进行处理。

通常会附加三种类型的头部：Radiotap 头部、WLAN-ng PRISM 头部和 PRISM AVS 头部。为了区分附加在每个无线数据包上的头部，你可以使用 `pcap_datalink` 函数调用，其总结如下所示：

```c
#define DLT_PRISM_HEADER 119
#define DLT_IEEE802_11_RADIO_AVS 163
#define DLT_IEEE802_11_RADIO 127
// 识别 PRISM Header
if (pcap_datalink(pcap_handle) == DLT_PRISM_HEADER)
{
    ..process PRISM header code here
}
// 识别 AVS Header
if (pcap_datalink(pcap_handle) == DLT_IEEE802_11_RADIO_AVS)
{
    ..process AVS header here
}
// 识别 Radio Tag Header
if (pcap_datalink(pcap_handle) == DLT_IEEE802_11_RADIO)
{
    ..process Radio Tag here
}
```

由于头部结构定义不同，处理这些头部的代码也必须不同。编写无线应用时，这三个头部的数据结构定义如下：

#### PRISM Header

```c
struct wlan_ng_prism2_header {
    uint32_t msgcode            __attribute__ ((packed));
    uint32_t msglen             __attribute__ ((packed));
    uint8_t  dev_name[WLAN_DEV_NAME_MAX]  __attribute__ ((packed));
    uint32_t hoststime          __attribute__ ((packed));
    uint32_t mactime            __attribute__ ((packed));
    uint32_t channel            __attribute__ ((packed));
    uint32_t rssi               __attribute__ ((packed));
    uint32_t sq                 __attribute__ ((packed));
    uint32_t signal             __attribute__ ((packed));
    uint32_t noise              __attribute__ ((packed));
    uint32_t rate               __attribute__ ((packed));
    uint32_t flags              __attribute__ ((packed));
    uint32_t frameno             __attribute__ ((packed));
};
```

#### AVS Header

```c
struct avs_80211_header {
    uint32_t version;
    uint32_t length;
    uint64_t mactime;
    uint64_t hoststime;
    uint32_t phytype;
    uint32_t channel;
    uint32_t datarate;
    uint32_t antenna;
    uint32_t priority;
    uint32_t ssi_type;
    int32_t ssi_signal;
    int32_t ssi_noise;
    uint32_t preamble;
    uint32_t encoding;
};
```

#### RadioTap Header

```c
struct ieee80211_radiotap_header {
    u8 version;
    u8 pad;
    u16_t len;
    u32_t present;
    uint64_t ts;
    uint16_t channel;
    uint16_t fhss;
    u8 rate;
    int8_t dbm_signal;
    int8_t dbm_noise;
    u8 db_noise;
    uint16_t quality;
    uint16_t tx_attenuation;
    uint16_t db_tx_attenuation;
};
```

Radiotap 头部的结构与其他两个头部的不同在于，它是一个带有 `present` 字段的变长头部。该字段通过其位图指示哪些字段存在，哪些不存在。在获取头部后，嗅探器代码将根据其结构处理无线帧的剩余部分。在下面的代码中，获取头部头部后接收到的帧被强制转换为管理头部：
