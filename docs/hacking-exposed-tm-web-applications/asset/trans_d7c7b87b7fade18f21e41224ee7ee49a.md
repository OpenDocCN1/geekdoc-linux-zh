

## 攻击管理接口

到此为止，我们还没有讨论通常运行在 Web 应用或周围的另一项关键服务：远程管理。Web  24/7 小时运行，这意味着当需要更新或修复时，Web 管理员并不总是坐在数据中心里。结合 Web 行业人员倾向于远程办公的本性（不需要着装规范），可以肯定的是，由于 Web 架构在某处开放了一个端口，以允许对服务器、内容、后端数据库等进行维护。

此外，自 90 年代中期以来生产的几乎每种网络产品（硬件或软件）可能都带有一个运行在嵌入式 Web 服务器上的 Web 管理接口。我们将在第 11 章中讨论这些接口，以及普通的 Web 服务器管理接口。

## 攻击客户端

在多年的专业 Web 应用测试中，我们看到的极少有审查报告花足够的时间来考虑对 Web 应用架构客户端的攻击。在我们看来，这是一个严重的疏忽。多年来，Web 用户社区遭受了许多毁灭性的攻击，包括跨脚本攻击（例如用于 eBay、ETrade 和花旗银行网站的攻击），以及像 Nimda 这样诞生于互联网的蠕虫，它们可以轻松地在恶意 Web 网站中实现，并通过 URL 发送给数百万人，或者发布到热门新闻组，或通过在线聊天转发。如果你认为这很糟糕，那么我们在第 12 章将涵盖的内容只是冰山一角。

## 发起拒绝攻击

假设攻击者已经进入了方法论的这一步，那么失败者的内心最后的避难所就是拒绝服务（DoS），这是当今互联网一个悲伤但真实的组成。正如名称所示，DoS 描述的是拒绝合法用户使用 Web 应用功能的行为。它通常通过向网站发送泛洪流量、冲掉合法请求来实现。我们将在第 3 章介绍针对 Web 服务器的 DoS 攻击，在第 8 章介绍针对 Web 应用的攻击。

## 总结

在本章中，我们从高空审视了 Web 应用架构、其潜在的安全漏洞以及发现和修复这些漏洞的方法论。本书的其余部分将专注于该方法论的细节。系好安全带，多萝西，因为堪萨斯要消失了。

## 参考文献和延伸阅读

| 参考文献 | 链接 |
| --- | --- |
| 通用参考文献 | |
| Microsoft IIS | http://www.microsoft.com/iis |
| Microsoft ASP | http://msdn.microsoft.com/library/psdk/iisref/aspguide.htm |
| Microsoft ASP.NET | http://www.asp.net/ |
| 超文本文本预处理器 (PHP) | http://www.php.net/ |
| Apache | http://www.apache.org/ |
| Netscape 企业产品 | http://enterprise.netscape.com/ |
| Java | http://java.sun.com/ |
| Java Server Pages (JSP) | http://java.sun.com/products/jsp/ |
| IBM Websphere App. Server | http://www.ibm.com/software/webservers/appserv/ |
| BEA Systems Weblogic App Server | http://www.broadvision.com/ |
| Broadvision | |
| Cisco Local Director | http://www.cisco.com/warp/public/cc/pd/cxsr/400/index.shtml |
| F5’s Big-IP | http://www.f5.com/ |
| 规范 | |
| RFC 索引搜索引擎 | http://www.rfc-editor.org/rfcsearch.html |
| W3C 超文本标记 | http://www.w3.org/MarkUp/ |
| 语言主页 可扩展标记语言 (XML) | http://www.w3.org/XML/ |
| WSDL | http://www.w3.org/TR/wsdl |
| UDDI | http://www.uddi.org/ |
| SOAP | http://www.w3.org/TR/SOAP/ |

## 第 2 章

![](img/2c61c2d28445b774d9266972920f432d_51_0.png)

## 26 Web 应用攻防指南

剖面分析（Profiling）识别了 Web 应用最基础的基础：

- 服务器 IP 地址，包括虚拟 IP
- 服务器端口和其他服务
- 服务器类型和版本（可能包括操作系统类型和版本）

我们将这些活动活动分别称为服务器发现、服务发现和服务识别。本章围绕对每项活动的讨论展开。本章涵盖的许多工具和技术都源于标准的安全评估/黑客攻击方法论，如《攻防》系列其他版本中涵盖的内容。为了完整起见，我们重复了这些内容，但排除了一些与 Web 应用安全无关的细节。我们建议感兴趣的读者咨询那些卷册。

## 服务器发现

正如我们在第 1 章中看到的，Web 应用运行在 Web 服务器上。因此，我们 Web 安全评估方法论的第一步是识别运行应用程序的物理服务器。执行此任务有若干种传统技术，我们将在本节中讨论。

## 直觉

在今天，在互联网上寻找 Web 服务器很难。只需在任何可以想象的术语、名称或短语后加上 www. 和 .com（或 .org 或 .edu 或 .gov），你就有很大机会发现一个 Web 服务器。针对你组织的攻击者可能会首先使用这种方法，因为这几乎不需要努力。他们可能会通过猜测常见主机名（如 www1.victim.com 或 shopping.victim.com）来枚举服务器。这不是产生全面结果的方法；我们将讨论更多方法。

## 互联网足迹

《攻防》的最新版本将足迹定义为为目标技术基础设施创建一个完整的画像。它考虑了该基础设施的几种接口：互联网、内网、外网和远程访问。对于面向互联网的 Web 应用，最相关的是互联网足迹。

互联网足迹主要通过 whois 工具进行，这是一个查询注册数据库的工具。whois 功能通常包含在大多数 Unix 操作系统中，Windows 版本也有。此外，whois 功能通过许多 Web 网站实现，任何拥有浏览器和互联网连接的人都可以访问。whois 可以跨类别查询信息，包括：

- 分配的 IP 地址范围
- 注册的域名和相关数据
- 互联网存在的管理联系

这两个类别可以帮助攻击者发现与特定组织或网站相关的服务器。让我们来看一些示例。

我们发现美国组织 IP 地址最好的方法是使用美国互联网注册局 (ARIN) 的 Web 网站进行 Web 版 whos 查询。只需在该网站输入组织名称并运行查询，就会显示与该组织相关的所有注册 IP 地址范围。典型的查询如图 2-1 所示。ARIN whos 产生的范围可以输入后续讨论的其他发现工具（ICMP ping、TCP ping 等），或者这些范围可以直接用于服务发现。

> 对于美国政府、军事和/或非美国互联网地址范围，查询表 2-1 中列出的注册机构。

