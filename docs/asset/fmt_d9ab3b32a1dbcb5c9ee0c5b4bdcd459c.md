
| 127.0.0.0 | | 255.0.0.0 | U | 0 | 0 | lo |

| default | 192.168.1.1 | 0.0.0.0 | UG | 0 | 0 | eth1 |

# 786 网络命令

假设你的网络有第二个路由器，作为连接另一个私有子网 `192.168.2.0`（子网掩码 `255.255.255.0`）的链路。该路由器本地侧的接口地址为 `192.168.1.200`。要添加一条静态路由条，将指向 `192.168.2.0` 子网的数据包发送到此路由器，可以使用以下命令：

```
$ route add 192.168.2.0 netmask 255.255.255.0 gw
192.168.1.200
```

# traceroute 命令

`traceroute` 命令显示了数据包从本地计算机到 Internet 目的地必须经过的所有路由器列表。这些路由器中的每一个被称为一个“跳”（hop）。如果你无法连接到另一台计算机，可以使用 Traceroute 查找问题发生的位置。

其语法如下：

```
traceroute [-i interface] host
```

虽然 `traceroute` 命令有多个选项，但你最可能用的是 `-i`，它允许你指定接口。如果你的电脑有多个网络适配器，这将非常有用。

# 附录 A：常用网站目录

在整本书中，我提到了许多你可以访问的网站，以获取有关各种网络主题的更多信息。本附将这些网站收集在一个方便的地方，并添加了许多同样值得抽空访问的网站。上网愉快！

## 认证

以下是查看官方认证信息的网站：

- www.microsoft.com/learning/mcp: 微软认证总部地

- www.comptia.org: 包含 A+、Network 和 Security+ 在内的独立认证

- www.novell.com/training/certinfo: Novell 认证主页

- www.ibm.com/cert: IBM 认证首页

- www.cisco.com/certification: 思科认证首页

- www.redhat.com/training/certification: 红帽认证首页

## 硬件

以下网站是研究计算机硬件的通用资源：

- http://reviews.cnet.com: CNET 的评测栏目提供了对所有类型计算机硬件的评论，并设有专门的网络网络板块。

- www.hardwarecentral.com: HardwareCentral 是另一个获取通用计算机硬件信息和建议的良好来源。

- www.tomshardware.com: 如果你想获取最新计算机组件的详细信息，Tom’s Hardware Guide 是首选。

# 788 家用和小型企业网络

以下制造商提供高端网络产品，包括服务器、路由器、交换机等：

- www.ibm.com/systems/networking: IBM 网络门户网站是必看站点。

- www.hp.com/servers: 该网站是惠普服务器产品的主页。

- www.dell.com/servers: 这是戴尔服务器产品的首页。

- www.oracle.com/servers: 这是 Sun 服务器的主页。

# 家用和小型企业网络

以下网站包含有关家庭和小型企业网络的通用信息：

- www.homenethelp.com: 这个优秀的网站致力于帮助人们建立并运行家庭网络，提供了分步操作程序和流程图。

- www.practicallyworked.com 该网站是家庭网络信息的绝佳来源，包含通用信息、技术博客、产品评测、故障排除建议等。

- www.hometoys.com: 该网站提供各种家用设备的信息，包括网络设备。

- www.ehpub.com: 这是 EH Publishing 的主页，他们出版了多本关于家庭技术的杂志。

- www.homepna.org: 这是 HomePNA 联盟的主页。

- www.homeplug.org: 这是 HomePlug 电力线联盟的主页，负责推广电力线网络。

- www.linksys.com: 这是 Linksys 的主页，它是家庭和小型办公室网络设备的流行制造商之一，包括 10/100BaseT、无线设备，甚至是电话和电力线设备。

- www.netgear.com: 这是 NETGEAR 的首页，他们制造家庭和小型办公室网络设备，包括 10/100BaseT 适配器和交换机、无线设备以及电话系统。

## Linux

以下网站包含有关 Linux 的通用信息：

- www.linux.org: 关于 Linux 的最好的综合网站之一。它是 Linux 信息和新闻的中心，包含了许多指向 Linux 发行版和可下载应用程序的链接。

- www.justlinux.com: 该网站包含一个热门讨论论坛，你可以在那里提问，并在运气好的情况下获得答案。

以下是一些最流行的发行版主页：

- www.redhat.com: 最流行的 Linux 发行版网站

- www.redhat/Fedora: Fedora 项目的主页

- www.suse.com: SUSE 发行版

- www.caldera.com: 来自 SCO 的 Caldera 发行版

- www.mandrivalux.com: Mandriva Linux 发行版（以前称为 Mandriva）

- www.slackware.com: Slackware，最古老的发行版之一

以下是一些最流行的发行版主页：

- www.isc.org: BIND 官方页面

- www.sendmail.org: Sendmail 官方网站

- www.apache.org: Apache 官方网站

- www.samba.org: Samba 官方网站

# 杂志

以下是各种杂志的链接：

- www.information.com: InformationWeek

- www.infoworld.com: InfoWorld

- www.networkcomputing.com: Network Computing

- www.windowsit.com: Windows IT

- www.2600.com: 2600

- www.linuxjournal.com: Linux Journal

- www.linuxmagazine.com: Linux

# 微软

微软的网站非常庞大。以下是一些链接：

- www.microsoft.com/windows: Windows

- www.microsoft.com/windowss2003: Server 2003

- www.microsoft.com/windowss2008: Server 2008

- www.microsoft.com/windowsxp: Windows XP

- www.microsoft.com/windowsvista: Windows Vista

- www.microsoft.com/windows7: Windows 7

- www.microsoft.com/sserversystem: 服务器系统

- www.microsoft.com/exchange: Exchange

- www.microsoft.com/sqlserver: SQL Server

- www.microsoft.com/iis: IIS

- http://sharepoint.microsoft.com: SharePoint

- http://technet.microsoft.com: TechNet

# 网络标准

研究标准时，以下网站非常有用：

- www.ansi.org: 美国国家标准协会 (ANSI)，官方标准组织。

- www.ieee.org: 电子电气工程师学会 (IEEE)，发布关键标准（如 IEEE 802.3）的国际组织。

- www.iso.org: 国际标准化组织 (ISO)，全球 100 个标准组织的联合。

- www.isoc.org: 互联网协会 (ISOC)，负责全球互联网协调与合作的国际组织。

- www.ietf.org: 互联网工程任务组 (IETF)，负责驱动互联网的协议。

- www.iana.org: 互联网分配机构 (IANA)，负责 IP 地址空间。

- www.w3c.org: 世界维网联盟 (W3C)，负责万维网标准开发的国际组织。

- www.rfc-editor.org: 这是 RFC 的官方库，包含一个允许通过名称或关键词查找 RFC 的功能。

# 参考

许多通用和计算机特定的参考网站提供百科全书式的文章或计算机网络术语的简单定义。如果你不确定某新技术，可以从这些网站开始：

- www.webopedia.com: Webopedia 是一个很好的计算机和互联网在线词典。不确定直接序列频谱是什么吗？去 Webopedia 查查！

- www.wikipedia.org: Wikipedia 是一个巨大的用户编写的在线百科全书。

- www.whatis.com: What Is 是另一个很好的计算机和网络术语词典。

- www.howstuffworks.com: 该网站包含许多技术的通用信息：计算机、汽车、电子、科学等。计算机部分提供了计算机硬件、互联网和安全等各种主题的良好入门。

# 搜索

当你试图解决网络问题并需要快速获取信息时，搜索引擎通常是你第一个考虑的地方：

- www.google.com: Google 是目前互联网上最流行的搜索引擎，拥有不断更新的海量 网站和新闻文章数据库。Google 拥有强大的关键词功能，允许你在搜索过程中不断进行优化。

## 792 TCP/IP 与互联网

- **www.bing.com**: 微软自己的搜索引擎，旨在与 Google 竞争。

- **www.yahoo.com**: 雅虎！作为最早的网站目录之一，如果你想浏览类别而不是搜索关键词，这里仍然是最佳去处。

- **www.msnsearch.com**: 微软 MSN 门户网站的搜索页面。

- **www.webfetch.com**: Webfetch 是一个元搜索工具，可以同时搜索多个引擎。

- **www.dogpile.com**: 另一个搜索引擎聚合器，可以同时搜索多个引擎。

## TCP/IP 与互联网

以下网站包含关于互联网的有趣信息：

- **www.internic.net**: InterNIC 网站是域名注册信息的中心枢纽。在此处查看经过批准的域名注册商列表。

- **www.networksolutions.com**: Network Solutions 的主页，它是最流行的域名注册网站。

- **www.register.com**: Register.com 是另一个域名注册网站。

- **www.isc.org**: 互联网系统协会（Internet Systems Consortium）的成员是那些每年进行两次域名调查，以估计互联网规模的人员。

欲需 DNS 信息，请尝试 www.dnsstuff.com，它允许你执行各种 DNS 查询，确保你的 DNS 区域设置正确。

检查这些网站查找有关 Web 浏览器的信息：

- **www.microsoft.com/ie**: Internet Explorer 的官方主页。

- **www.mozilla.org**: Firefox 的主页，一种流行的替代 Web 浏览器。许多用户认为 Firefox 是目前最好的 Web 浏览器。

- **www.opera.com**: Opera 的主页，Internet Explorer 的另一个替代方案。

## 无线网络

以下是一些包含有关无线网络通用信息的网站：

- www.wi-filplanet.com: Wi-Fi Planet 是一个致力于无线网络新闻、信息和产品评论的大型网站。

- http://www.wfinetworks.com: Wi-Fi Networking News 是无线网络每日新闻的来源。

以下是最流行的无线网络产品品牌的网站：

- www.linksys.com: Linksys 是无线网卡和接入点的制造商。

- www.netgear.com: NETGEAR（网达）是另一个无线组件的制造商。

- www.dlink.com: D-Link 是另一个廉价无线产品的制造商。

- www.smc.com: SMC 的主页，另一个无线网络产品的制造商。

- www.cisco.com: Cisco（思科）是高端无线网络的首选之地。

- www.3com.com: 3Com 是无线网络组件的另一个良好去处。

以下网站包含关于无线网络安全的有趣信息：

- www.netstumbler.com: NetStumbler 的制作，该软件用于检测无线网络访问和安全问题。

- www.airwave.com: AirWave 的制作，这是一种基于软件的工具，用于监听未经授权的接入点。

- www.wardriving.com: 一个致力于翘游（wardriving）实践的广泛网站。

## 智能手机

以下网站包含关于各种智能手机平台的有用信息：

- www.blackberry.com: Research In Motion 公司 Blackberry 平台的主网站。

- www.blackberryforums.com: Blackberry 平台一个流行的讨论版论坛网站。

- www.microsoft.com/windowsmobile: Windows Mobile 平台的主页。

- www.android.com: Google Android 平台的主页。

- www.apple.com/iphone: Apple iPhone 的主页。

## 附录 B：术语表

**10Base2**: 一种曾用于以太网中最常用的同轴电缆。被称为 *thinnet* 或 *cheapernet*。单段最大长度为 185 米（600 英尺）。

**10Base5**: 原始以太网同轴电缆，现在已过时。被称为 **yellow cable**（黄缆）或 **thick cable**（粗缆）。单段最大长度为 500 米（1640 英尺）。

**10BaseT**: 双绞线，通常用于以太网。也被称为 *twisted pair*（双绞线）或 *twisted sister*（开个玩笑的！）。单段最大长度为 100 米（330 英尺）。在三种以太网电缆中，这种最容易处理。

**100BaseFX**: 用于高速光纤连接的以太网标准。

**10BaseT4**: 用于 100 Mbps 以太网的替代标准，使用四对 3 类电缆。

**100BaseTX**: 100 Mbps 以太网的领先标准，使用两对 5 类双绞线。

**100VG AnyLAN**: 一种 100 Mbps 以太网标准，不如 100BaseT 流行，它使用双绞线。

**1000BaseT**: 一种用于 1000 Mbps 以太网的新标准，使用四对 5 类非屏蔽双绞线。1000BaseT 也被称为千兆以太网（Gigabit Ethernet）。

**1000000000000BaseT**: 嗯，其实并不如此。如果目前的趋势持续，我们将得到...

## 798 后台

**BackOffice（后台）**: 一套设计用于在 Windows 服务器上运行的微软程序包。

**backup（备份）**: 对你的重要文件的复制，用于在原始文件发生意外情况时进行保存；你应该每天都进行备份。

**banner（横幅页）**: 一个在打印作业之间打印的精美页面，以便你轻松地区分不同的打印作业。

**batch file（批处理文件）**: 一个包含一个或多个命令的文件，这些命令作为一组一起执行。你使用文本编辑器创建批处理文件，并在命令行提示符中输入其名称来运行。

**BDC**: 在 Windows NT 中，*备份域控制器*为域提供备份管理。Active Directory（活动目录）不使用 BDC。

**benchmark（基准测试）**: 一种你用来判断网络性能的可重复测试。最好的基准测试是那些与你经常在网络上执行的工作类型密切相关的测试。

BES: 参见 **BlackBerry Enterprise Server（黑莓企业服务器）**。

**BlackBerry（黑莓）**: 由 Research In Motion (RIM) 制造的流行手机。

**BlackBerry Enterprise Server (BES)（黑莓企业服务器）**: 运行在 Windows 服务器上的软件，允许黑莓设备与 Microsoft Exchange 同步。

**Bluetooth（蓝牙）**: (1) 十世纪使用过丹麦和挪威的维京人。(2) 一种用于短距离网络的无线网络协议，主要用于无线键盘、鼠标和手机等设备。

**BNC connector（BNC 连接器）**: 与 10Base 线配合使用的连接器。

**bottleneck（瓶颈）**: 你网络中最慢的链路，会导致网络拥堵。提高网络的第一的第一是识别瓶颈。

**bridge（网桥）**: 不是那种流行的扑牌游戏，而是一种能够将两个网络连接在一起的设备。网桥足够小，可以知道哪些计算机在桥的哪一，因此它们只允许需要到达另一侧的消息跨越网桥。这种设备可以提高性能。

**broadband（宽带）**: 用于广域网的高速连接。

## Centrex 799

**buffer（缓冲区）**: 一块用于存放传输往其他地方数据的内存区域。例如，硬盘缓冲区在数据于你的计算机和硬盘之间传输时存储数据。

**bus（总线）**: 一种网络拓扑结构，网络节点沿着称为“段”的单根电缆排列。10Base2 和 LocalTalk 网络使用总线拓扑结构。总线也指你计算机内部的扩展槽行。

**cable tie（扎带）**: 小塑料条，对于固定电缆或将它们捆绑在一起特别方便。

**cache（缓存）**: 一种复杂的缓冲形式，预留了大量内存来存储数据，以便快速访问。

**call forwarding（呼叫转接）**: PBX 系统的一种功能，可自动将未接听电话转接到另一个目标，例如另一个分机或语音信箱。
