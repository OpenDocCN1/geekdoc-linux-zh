
| 姓名：Chris Hurley |
| 邮箱：roamer@securitytribe.com |
| 注册 |
www.syngress.com

# 第 6 章：使用 OS X 进行 WarDriving 和无线渗透测试

当你完成 WarDriving 后，通过点击**文件（File）** > **导出（Export）** > **数据到 KisMAC 服务器（Data to KisMAC Server）** 将数据发送到 KisMAC 服务器。

除了将结果传输到 KisMAC 服务器外，KisMAC 账户还允许你搜索现有的 KisMAC 数据库。

> **注意** 在为客户工作之前，禁用 KisMAC 是一个好习惯，这样他们的数据就不会被发送到公共服务器。

## 使用 KisMAC 绘制 WarDrive Map

通常情况下，KisMAC 是一个非常直观且易用的工具；但有一个例外：*映射*。最初使用 KisMAC 绘制 WarDrive 可能会是一个令人沮丧的体验。本节详细介绍了成功导入地图供 KisMAC 使用所需的步骤。

### 导入地图

使用 KisMAC 绘制 WarDrive 的第一步是导入地图。这与许多其他 WLAN 发现应用程序（例如 Linux 的 Kismet 或 Windows 的 NetStumbler）不同，后者地图通常在 WarDrive 完成时生成。

KisMAC 需要你驱动中心区域的*纬度*和*经度*来导入地图。这些坐标可以手动输入，但先连接你的全球定位系统 (GPS) 并获得信号锁定会更容易。

### 使用 GPS

大多数能够国家海洋电子协会 (NMEA) 输出的 GPS 设备都可以与 KisMAC 工作。这些设备许多只有串口线可用。大多数情况下，你需要购买一个串口转 USB 适配器（约 25 美元）将 GPS 连接到你的 Mac。大多数此类适配器都带有 OS X 的驱动程序；确保你购买的包含这些驱动程序。此外，根据你的 GPS 型号，你可能可以使用 USB GPS 线，而无需 USB 转串口适配器。GPS Store 在 `http://www.thegpsstore.com/detail.asp?product_id=GL0997` 销售这些线缆。

连接 GPS 后，打开 KisMAC 偏好设置并选择 GPS 选项（见图 6.10）。如果没有自动选择，请从下拉菜单选择 `/dev/tty.usbserial0`。

#### 图 6.10 KisMAC GPS 偏好设置
![](img/792dbeecc8fbe4973ef2b3a6427b61de_243_0.png)

确保选中了“使用 GPS 坐标”（Use GPS coordinates）和“使用所有点”（Use all points），并且 `GPSd` 正在监听 `localhost` 端口 `2947`。你的 GPS 现在已配置好并准备就绪。安装 `GPSd`，请从 `http://gpsd.berlios.de/` 下载 OS X 版 `GPSd`。编译和使用 `GPSd` 的说明可以在 `http://kismac.bervarianz.de/wiki/wiki.php?KisMAC/WiFiHacksCompileGPSd` 查看。

另一个选项是蓝牙 GPS；然而，根据 KisMAC 网站，OS X 中的蓝牙栈存在问题；你仍然在使用这些设备时必须使用 `GPSd`。

### 准备导入

现在你的 GPS 设备已连接，你可以准备导入地图了。要导入地图，选择 **文件（File）** > **导入（Import）** > **地图来自（Map from）** > **服务器（Server）**。

#### 图 6.11 准备导入地图
![](img/792dbeecc8fbe4973ef2b3a6427b61de_244_0.png)

这将打开“下载地图”（Download Map）对话框（见图 6.12）。你当前的 GPS 坐标会自动导入此框。选择你想要导入的服务器和地图类型。

#### 图 6.12 选择地图服务器和地图类型
![](img/792dbeecc8fbe4973ef2b3a6427b61de_244_1.png)

有多种地图可用，以及不同类型的地图（即：普通地图或卫星地图）。见图 6.13。

#### 图 6.13 可用的地图服务器和地图类型
![](img/792dbeecc8fbe4973ef2b3a6427b61de_244_2.png)

www.syngress.com

# 使用 OS X 进行 WarDriving 和无线渗透测试 • 第 6 章

导入地图后，点击 KisMAC 保存。一旦设置好所有选项，就可以开始使用了。KisMAC 界面易于导航，并包含了一些高级功能，结合了其他 WarDriving 应用程序的许多特性，包括许多商业应用程序。

KisMAC 界面（见图 6.16）简单易懂。主窗口显示 KisMAC 发现的所有无线网络，并可以按数字（发现顺序）、SSID、BSSID 地址、使用的加密类型、当前/平均/最大信号强度、传输的数据包数量、数据流大小（以 KB 或 MB 为单位）以及访问点最后在范围内的时间（Last Seen）进行排序。

#### 图 6.14 KisMAC 偏好设置
![](img/792dbeecc8fbe4973ef2b3a6427b61de_245_0.png)

#### 图 6.15 KisMAC 地图
![](img/792dbeecc8fbe4973ef2b3a6427b61de_246_0.png)

## 234 第 6 章 • 使用 OS X 进行 WarDriving 探测与无线渗透测试

### 图 6.16 KisMAC 图形用户界面
![](img/792dbeecc8fbe4973ef2b3a6427b61de_248_0.png)

配置好 WarDrive 的选项后，点击 **Start Scan**（开始扫描）按钮（位于界面右下角）开始定位接入点。此外，底部工具栏上有四个按钮，允许你查看有关当前扫描的特定信息。

### KisMAC 窗口视图按钮

KisMAC 允许通过选择底部工具栏上的四个按钮之一来查看有关当前 WarDrive 的特定信息（见图 6.17）。

#### 图 6.17 KisMAC 窗口视图按钮
![](img/792dbeecc8fbe4973ef2b3a6427b61de_248_1.png)

**Show Networks**（显示网络）按钮是默认设置。在选择其他选项后要返回默认设置，请点击此按钮查看已发现的所有网络。

选择 **Show Traffic**（显示流量）按钮将调出 WarDrive 期间发现的网络信号图。默认情况下，此视图显示强度图（见图 6.18）。每个接入点由唯一的颜色表示，右上角的图例显示每个颜色对应哪个网络。图中线条越长，表示信号越强。

#### 图 6.18 “Show Traffic”视图
![](img/792dbeecc8fbe4973ef2b3a6427b61de_249_0.png)

左上角有两个下拉菜单。一个是显示的间隔时间（默认为 15 秒），另一个是允许你更改使用“Show Traffic”视图可以查看的信息类型的菜单。除了信号强度外，你还可以显示穿过无线网络的每秒数据包数，或者接入点发送和接收的字节总数。

**Show Map**（显示地图）按钮允许你查看当前 WarDrive 的实时地图（有关映射你的 WarDrive 的更多信息，请参阅本章前面的“使用 KisMAC 绘制 WarDrive Map”部分）。

最后一个视图通过 **Show Details**（显示详情）按钮访问。此视图允许你获取有关特定接入点的大量信息（见图 6.19）。

#### 图 6.19 "Show Details"视图
![](img/792dbeecc8fbe4973ef2b3a6427b61de_250_0.png)

默认视图中列出的 KisMAC 信息位于界面左侧，而连接到网络的客户端信息位于界面右侧。此视图中的可用信息对于渗透测试人员来说至关重要，将在本章稍后的“使用 OS X 进行渗透测试”章节中进行详细讨论。

### KisMAC 的其他视图选项

除了视图按钮外，KisMAC 还允许你在“Show Networks”视图下获取有关特定网络的额外信息。使用 OS X 菜单栏，点击 **Window** > **Show Hierarchy**（窗口 > 显示层级结构）（见图 6.20）。

#### 图 6.20 OS X 菜单层级结构
![](img/792dbeecc8fbe4973ef2b3a6427b61de_251_0.png)

显示“Show Hierarchy”（显示层级结构）后，你可以收集有关特定网络的信息；使用不同类型加密的网络；或在特定通道上传输的所有网络。这些信息在渗透测试期间至关重要。

#### 图 6.21 “KisMAC 层级结构”视图
![](img/792dbeecc8fbe4973ef2b3a6427b61de_251_1.png)

## 使用 OS X 进行渗透测试

除了作为 WarDriving 应用程序外，KisMAC 是可用的无线网络渗透测试的最佳工具。KisMAC 内置了执行任何最常见 WLAN 攻击的功能，并使用了简单的“点点”界面。此外，KisMAC 可以从其他程序导入数据包转储（packet dumps），以对无线网络进行许多离线攻击。本节将介绍目标网络上的许多此类攻击。

以下是一个工作示例。你受雇为一家公司执行渗透测试，并需要正确识别他们的无线网络。通过在你目标周围区域进行 WarDrive 期间收集的信息，你根据信号强度、地图数据和接入点使用的命名规范，成功识别了目标网络。要成功渗透该网络，你必须确定正在使用什么类型的加密。

### 使用 KisMAC 攻击 WLAN 加密

无线网络可以采用不同类型的加密。最常用的加密方案是 WEP 和 WPA，尽管还有其他更先进的方案。查看 KisMAC 的显示，你会发现 SSID 为 `Our_Target` 的接入点是一个 WEP 加密网络。

### 使用 KisMAC 攻击 WEP

由于你已经确定目标无线网络使用了 WEP，你现在必须决定想要如何破解密钥。KisMAC 有三种主要方法：

- 字典列表攻击（Wordlist attacks）
- 弱密钥攻击（Weak keys）
- 暴力破解攻击（Bruteforce attacks）

实现此操作最简单的方法是通过重新注入数据包来生成初始化向量（IVs）。一旦捕获了几个此类数据包，停止断认证（deauthentication）。

#### 图 6.22 断认证
![](img/792dbeecc8fbe4973ef2b3a6427b61de_254_0.png)

在断认证期间，注入数据包的数量应该增加（见图 6.22）。

### 重注入

一旦捕获了几个可能被拒绝的数据包（在 KisMAC 的“Show Details”视图中注明），是时候尝试重新注入了。点击 **Network** > **Reinject Packets**（注入数据包）（见图 6.23）。

#### 图 6.23 准备重新注入数据包
| Network Map | Window | |
|---|---|---|
| Delete | ⌘ | |
| Join Network | ⌘J | |
| Show Details | ⌘D | |
| Show Clients | ⌘C | |
| Deauthenticate | ⇧D | |
| Authentication Flood | | |
| Reinject Packets | | |
| Crack | | |

这会打开一个对话框（见图 6.24），指示 KisMAC 正在测试数据包以确定其是否可以成功注入网络。

#### 图 6.24 测试数据包
![](img/792dbeecc8fbe4973ef2b3a6427b61de_255_0.png)

一旦 KisMAC 找到合适的数据包，对话框将关闭，KisMAC 开始注入。可以通过查看“Network”选项来验证这一点（见图 6.25）。

#### 图 6.25 重注入
| Network Map Window | | | |
|---|---|---|---|
| Delete | ⌘ | | |
| Join Network | ⌘J | | |
| Show Details | ⌘D | | |
| Show Clients | ⌘C | | |
| Deauthenticate | ⇧D | | |
| Authentication Flood | | | |
| ✓ Reinjecting into 00:00:C1:C6:5B:11 | | | |
| Crack | | | |

## 242 第 6 章 • 使用 OS X 进行无线漫游与无线渗透测试

现在必须使用第二块网卡（通常在另一台机器上）捕获流量，以便获取足够的 IV 来尝试破解密钥。在获取了足够的 IV 后，可以使用 KisMAC 执行弱调度攻击；然而，使用 KisMAC 注入数据包，并使用 Aircrack 等工具进行实际的 WEP 破解可能更高效。

### 使用 KisMAC 攻击 WPA

与 WEP 不同，WEP 需要产生大量的流量才能破解密钥，而 WPA 只需要在认证时捕获四路局域网扩展身份认证协议（EAPOL）握手即可。此外，与破解 WEP 不同，WPA 采用的是字典攻击，这意味着当你使用 KisMAC 破解 WPA 预共享密钥（或密码）时，只需要捕获少量的流量；即使在你超出了接入点的范围内，也可以进行实际的攻击。

WPA 仅在使用短密码时容易受到攻击。即便如此，它也必须是字典中的单词或你词库中的单词。一个包含字母、数字和特殊字符组合的广泛词表可以帮助提高破解 WPA 的成功率。

要对 KisMAC 进行字典攻击，你可能需要对客户端进行认证（详见“使用 KisMAC 攻击 WEP”章节）。然而，在尝试对 WPA 进行字典攻击时，所有操作可以在一个主机上完成，这将导致客户端断开网络并强制其重新连接。这需要再次传输四路 EAPOL 握手。

一旦捕获了客户端与 WPA 网络之间的关联，按下 **Network** > **Crack** > **Wordlist Attack** > **Wordlist against WPA-PSK Key**。系统会提示你要使用的词表或字典文件的位置。选择字典文件后，KisMAC 开始使用该文件中的每个单词对 WPA 预共享密钥 (PSK) 进行测试。

#### 图 6.26 WPA 破解
![](img/792dbeecc8fbe4973ef2b3a6427b61de_256_0.png)

www.syngress.com

当 KisMAC 成功确定密钥后，它将显示在“Show Details”（显示详情）视图中。

### 其他攻击

KisMAC 还提供了对其他形式的加密和身份验证进行攻击的能力。由于这些其他方法存在已知漏洞且客户端很少使用，因此本文不再详细讨论，但为了完整性将其包含在内。

#### 针对 40-bit WEP 的暴力破解攻击

KisMAC 包含了对 40-bit WEP 密钥执行暴力破解的功能。KisMAC 有四种方式实现此目标：

- 所有可能的字符
- 仅限字母数字
- 仅小写字母
- Newshams 21 位攻击

这些攻击每一种都非常有效，但也非常耗费时间和处理器资源。

#### 字典攻击

KisMAC 提供了在 WPA 攻击中执行多种类型字典攻击的功能。Cisco 开发了轻量扩展身份认证协议（LEAP），以帮助担心 WEP 漏洞的组织。遗憾的是，LEAP 同样容易受到类似于 WPA 的字典攻击。KisMAC 包含了使用与破解 WPA 相同的步骤对 LEAP 执行字典攻击的功能。选择 **against LEAP Key** 按钮以开始攻击。

此外，还可以以相同的方式对 40-bit 和 104-bit Apple 密钥或 104-bit 消息摘要5 (MD5) 密钥发起字典攻击。与任何字典攻击一样，只有在执行攻击时使用全面的字典文件（`www.securitytribe.com/~roamer/words.txt`），这些攻击才是有效的。

## 用于无线漫游和 WLAN 测试的其他 OS X 工具

KisMAC 是本章的重点；然而，还有其他几种无线工具可以让一个 OS X 黑客忙碌好几个小时。

EtherPEG (`www.etherpeg.org`) 是一个捕获并显示跨网络（包括 WLAN）传输的所有 JPEG 和 GIF 图像的程序。为了使用 EtherPEG 攻击无线网络，必须没有使用加密，或者你已经连接到网络。

iStumbler (`http://istumbler.net/`) 是一个适用于 OS X 的活动 WLAN 发现工具，适用于内置的 Airport Express 卡。除了 WLAN 发现外，iStumbler 还可以使用内置蓝牙适配器检测蓝牙设备。iStumbler 不需要设置，只需解压存档并点击 iStumbler 图标即可开始。

#### 图 6.27 iStumbler
![](img/792dbeecc8fbe4973ef2b3a6427b61de_258_0.png)

随着 OS X Tiger 的发布，已经开发并发布了几个 Dashboard 小组件，它们使用 Airport 和 Airport Express 卡进行主动扫描（例如，Air Traffic Control）（见图 6.28）。

#### 图 6.28 Air Traffic Control
| 名称 | 厂商 |
| :--- | :--- |
| 3 | Linksys |
| 10 | deHOME |
![](img/792dbeecc8fbe4973ef2b3a6427b61de_259_0.png)

## 总结

当人们想到 macOS 上的无线漫游（War-Driving）时，通常会想到 KisMAC。虽然有很多可用工具，但 KisMAC 是最多功能的工具之一，因为它可以执行主动和被动攻击。它还允许用户破解 WEP、WPA 和 LEAP 加密。

“切割攻击”（chopping attack）是 WEP 破解中的重大突破，因为它消除了对弱 IV 的需求。通过重新注入 ARP 包，攻击者可以在几小时而不是几周获取 WEP 密钥。其他工具如 iStumbler 和 EtherPEG 对于 WLAN 发现和流量分析也很有帮助。然而，随着安全协议的演进，用于测试和攻击它们的工具也会随之进化。
