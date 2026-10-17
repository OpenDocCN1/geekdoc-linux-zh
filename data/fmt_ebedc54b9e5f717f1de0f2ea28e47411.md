
数据包注入工具可以伪造几乎任何类型的无线 802.11 帧。存在某些工具可以通过注入信标帧（`beacon frames`）、探测响应帧（`probe responses`），甚至是认证帧（`authentication frames`）和关联帧（`association frames`）来模拟 AP，从而欺骗无线客户端使其认为附近有一个合法的 AP。数据包注入器的示例包括 `Airplay-ng`、`Probebemapper`、`Omerta`、`Void11`、`WLAN-Jack`、`FATA-Jack` 和 `File2Air`。

## WEP/WPA-PSK 破解器

涉及直接加密破解的工具类别专门针对 WEP 和 WPA-PSK。在 WEP 破解领域，工具包括 `Webrack`、`Airsnort`、`Aircrack-twp` 和 `Aircrack-ng`。所有这些工具都依赖于攻击者必须从目标无线网络收集足够数量的 WEP 加密数据帧，以便将其传递给如 `Aircrack-ng` 类的破解程序。数据帧的数量取决于破解方案。较新的 `Pyquine-Weissmann` 方法仅需 40,000 到 80,000 个帧，而 `Aircrack-ng` 中较旧的 `KoRek` 方法则需要 500,000 到 100 万个数据帧。

对于 WPA-PSK 破解，这些工具依赖于 `PBKDF2` 或基于密码的密钥派生函数 v2（`Password-Based Key Derivation Function v2`）公式，用于创建会话密钥的主密钥通过 `SSID` 进行哈希处理，而用于实际数据加密的临时会话密钥通过四次握手（`four-way handshake`）建立，这可以在授权客户端尝试与 AP 关联时被无线嗅探器捕获。捕获四次握手后，就可以对密码进行离线字典攻击。工具示例包括 `Cowpatty` 和 `Aircrack-ng v0.7` 及以上版本。

## 无线中间人攻击 (MITM)

由于无线客户端与 AP 之间存在空隙（air gap），中间人（MITM）类型攻击非常普遍且容易实现。

在此类攻击中，工具通常被构建用于自动化 MITM 设置过程的大部分部分。这些工具通常将无线卡配置为运行主模式（`master mode`）（在之前的“攻击设置：Linux 原生芯片和驱动程序”中介绍过），这会导致无线网卡（`WNIC`）变成一个 AP 并响应无线客户端对网络的探测。它会建立一个 DHCP 服务器、HTTP 服务器和 DNS 服务器，以欺骗客户端认为它们连接到了某个合法 AP 和网络服务。

在某些情况下，工具将通过与实际无线网络建立次要连接，将所有客户端流量转发到该网络，从而允许攻击者捕获目标客户端的每一个无线帧（因为攻击者本人充当了 AP，他不会错过任何帧，而所有的客户端帧都会被记录）。无线 MITM 工具的一个良好示例是 `Airsnarf`（结合去身份认证/去关联工具使用以获得最大效果）。

## 无线客户端审计

就无线审计而言，如今没有哪个机构可以声称在进行任何形式的无线审计客户端之前，在其场所内没有部署无线能力。即使该机构执行无无线政策，今天现市购买的几乎所有新型便携式计算设备都带有某种无线能力，攻击者可以使用本章描述的工具利用这些能力。

内置在这些便携设备中的无线芯片组在不使用时经常被保持“开启”状态。`Probemapper`、`Karma` 和 `Hotspot` 等工具可用于“欺骗”这些无线客户端在活跃时连接到它们。当这些客户端连接到各个机构的有线网络时，攻击者创建的无线通道可以被用来完全攻破无线客户端的内部网络。

# 破解攻防 Linux：Linux 安全秘密与解决方案

用户在执行某些操作时，例如更改无线网卡的 MAC 地址以进行无线帧注入。

`OSWA-Assistant` 工具包的一个新新增项是 `MoocherHunter` 无线黑客/移动者跟踪软件（见 `http://moocherhunter.securitystarshare.org`）。在合适的硬件下，该软件可以帮助执法部门和无线网络管理员跟踪那些接入受保护和未加密无线网络的未经授权无线用户。根据定义，“白蹭网者”（moochers）想要使用这些服务，因此他们面临着选择：要么继续“白蹭”并暴露自己的身份，要么停止“白蹭”。该工具仅在特殊许可下作为 `OSWA-Assistant` 的组成部分提供。

# 编写你自己的无线软件

除了他人编写并发布的预存工具外，攻击者可能也需要编写自己的自定义工具。接下来的章节将重点介绍在编写无线工具时需要注意的一些重要点。

### Libpcap

在开发无线工具时，最需要熟悉的代码库之一是 `Libpcap` 库。它最初开发于劳伦斯·伯克利实验室，目前由维护 `Tcpdump`（命令行数据包捕获工具，`http://tcpdump.org`）的同一组人员维护。在嗅探中使用 `Libpcap` 库从程序员的角度来说简化了大量的编码工作，使其在编写工具时成为必不可少的。

为了说明，请看以下 `Probamember` 代码片段，它是 C 语言编写的：

```c
#include <pcap.h>
pcap_handle handle = pcap_open_live(interface, 65536,1,1000000, errbuf);
// 当发生错误时
if (pcap_handle == NULL)
{
  fprintf(stderr,"Error in pcap_open_live: %s\n", errbuf);
  cleanup_failure(); // exits
}
```

这段代码显示 `Probamember` 工具打开了一个 pcap 接口，该接口将随后用于从该无线接口获取数据包。

以下代码使用通过 `pcap_open_live` 创建的句柄和 `pcap_next` 函数调用来提取无线接口接收的数据。随后的三行会在没有接收到任何内容时检查并报告错误。

```c
packet = pcap_next(pcap_handle, &header);
if (packet == NULL)
{
  fprintf(stderr,"No packets: %s\n", errbuf);
  cleanup_failure(); // exits
}
```

在嗅探无线接口时需要理解的下一个重要点是：无线接口需要处于 RFMON 模式才能嗅探无线流量（无论是数据帧、管理帧还是控制帧）。通过无线驱动程序采集的每个无线帧前面都带有一个特殊的头部，报告帧在被无线网卡（`WNIC`）接收时的信号电平、噪声水平、频率和速率信息。根据所使用的无线驱动/固件组合以及驱动/固件的设置，添加的头部类型也不同。识别添加的头部信息类型非常重要，因为嗅探器需要编码好的节点来了解捕获的数据包头结构，以及此后如何对其进行相应的处理。

通常会添加三种类型的头部：`Radiotap` 头部、`WLAN-ng PRISM` 头部和 `WLAN-ng PRISM AVS` 头部。为了在程序中区分这些附加在每个无线数据包上的头部，你可以使用 `pcap_datalink` 函数调用，其总结如下：：

```c
#define DLT_PRISM_HEADER 119
#define DLT_IEEE8002_11_RADIO_AVS 163
#define DLT_IEEE8002_11_RADIO 127
// 识别 PRISM 头部
if (pcap_datalink (pcap_handle) == DLT_PRISM_HEADER)
{
  ..process PRISM header code here
}
// 识别 AVS 头部
if (pcap_datalink (pcap_handle) == DLT_IEEE8002_11_RADIO_AVS)
{
  ..process PRISM AVS header code here
}
// 识别 Radio Tap 头部
if (pcap_datalink (pcap_handle) == DLT_IEEE8002_11_RADIO)
{
  ..process Radio Tap header code here
}
```

由于各种头部的结构定义不同，处理这些头部的代码也必须不同。在编写无线应用程序时，这三个头部定义的的数据结构在这里记录：
