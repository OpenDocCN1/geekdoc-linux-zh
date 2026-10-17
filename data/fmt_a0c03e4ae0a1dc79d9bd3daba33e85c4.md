
> **本书 CD 中包含一个自动发现模块。**

域名的标准 DNS 条目通常包括 WWW（互联网 Web 服务器）、Mail（邮件 SMTP 网关服务器）和 FTP（FTP 服务器）的名称到 IP 地址记录。扩展的 PING 查询可能会揭示我们目标网络 `206.0.125.x` 上的这些主机：

![](img/ba85bb40c695c02adae8cbd6666f2e0c_138_0.png)

**图 5.5** ICMP 回显请求（PING）数据包从我们的 DNS 传输到 InterNIC DNS，再到目标公司的 ISP DNS，最终到达 XYZ Web 服务器以获取响应。

```
C:\>ping www.xyzinc.com

Pinging www.xyzinc.com [206.0.125.0] with 32 bytes of data:
Reply from 206.0.125.10: bytes=32 time=489ms TTL=52
Reply from 206.0.125.10: bytes=32 time=751ms TTL=51
Reply from 206.0.125.10: bytes=32 time=499ms TTL=52
Reply from 206.0.125.10: bytes=32 time=484ms TTL=51

Ping statistics for 206.0.125.10:
 Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
 Minimum = 484ms, Maximum = 751ms, Average = 555ms
```

**图 5.6** PING 请求最终将 URL www.xyzinc.com 解析为 IP 地址 206.0.125.10。

```
C:\>PING MAIL.XYZINC.COM

Pinging mail.xyzinc.com [206.0.126.5] with 32 bytes of data:
Reply from 206.0.126.5 bytes=32 time=398ms TTL=49
Reply from 206.0.126.5 bytes=32 time=398ms TTL=49
Reply from 206.0.126.5 bytes=32 time=398ms TTL=49
Reply from 206.0.126.5 bytes=32 time=398ms TTL=49
```

```
C:\>PING FTP.XYZINC.COM

Pinging ftp.xyzinc.com [206.0.126.12] with 32 bytes of data:
Reply from 206.0.126.12 bytes=32 time=312ms TTL=53
Reply from 206.0.126.12 bytes=32 time=312ms TTL=53
Reply from 206.0.126.12 bytes=32 time=312ms TTL=53
Reply from 206.0.126.12 bytes=32 time=312ms TTL=53
```

PING 查询请求揭示了重要的网络地址信息，指示了 XYZ Inc 的以下 DNS 条目：

| 主机 | 域名 | IP 地址 |
| :--- | :--- | :--- |
| www | www.xyzinc.com | 206.0.126.10 |
| mail | mail.xyzinc.com | 206.0.126.5 |
| ftp | ftp.xyzinc.com | 206.0.126.12 |

## 互联网 Web 搜索查询

万维网（World Wide Web）常被称为信息高速公路，因为它包含了数百万兆字节的数据和信息，供世界各地无数的人浏览。万维网通过采用搜索引擎来容纳大部分流量，搜索引擎是 Web 上增长最快的站点。

搜索引擎和 Usenet 组群是研究目标域名的绝佳工具，因此这一步涵盖了获取这些信息以辅助目标网络发现过程的方法。可以使用 Web 前端进行的扩展搜索来获取和/或验证地址、电话号码和技术联系人姓名。更流行的搜索引擎和蜘蛛程序可以利用其信息收集能力。

推荐的当代搜索引擎列表包括：

- www.altavista.com
- www.businessseek.com
- www.clicheherefind.com
- www.deja.com
- www.excite.com
- www.goto.com
- www.hotbot.com
- infoseek.go.com
- www.lycos.com
- www.nationaldirectory.com
- www.peoplesearch.com
- www.planetsearch.com
- www.yellowpages.com

目标公司网站上的公司简介链接包含验证地址、电话号码和信息服务（IS）主管的信息。（还记得之前出现的行政联系人 Bill Thompson 吗？）这足以进行社会工程学查询，这将在下一步中介绍。

## 社会工程学查询

这一步解释了一种迫使潜在受害者透露网络访问信息的尝试。这是全球黑客、破解者和电话贼（phreaks）常用的一种技术。该方法的简单成功变体包括伪装成新用户以及技术人员。

### 伪装成新用户

根据先前步骤收集的信息，黑客可以拨打 XYZ 的主电话号码，要求转接至 IS 部门或技术支持组，然后假装是一名被告知联系他们以获取临时用户名和密码的临时员工。

更多的研究可以大大提高这一过程的成功率。例如，打电话询问市场营销部主管的名字可能会改变上述场景：在被转接至技术人员后，黑客可以先说：“你好，我叫 Tom Friedman。我是市场营销主管 Sharon Roberts 的新临时工，她让我打电话给你以获取临时用户名和密码。”

### 伪装成技术人员

要使用这种变体，黑客可能会要求转接至销售部门的某人。在那里，他或她可以说明 IS 总监 Bill Thompson 要求联系该部门的每个用户以验证登录访问权限，因为将引入一台新服务器以替换旧服务器。这些信息将使黑客能够成功登录，从而使服务器集成对他来说是透明的。

社会工程学查询过程有无限的变体。彻底且详细的研究收集有助于开发出最适合目标公司的变体。社会工程学查询产生 surprisingly 高的成功率。有关此方法的更多信息和成功案例，请搜索本书 CD 上 Tiger Tools Repository 中的链接。

## 站点扫描

如本章开头所述，扫描的基本思想是探测尽可能多的端口，并记录那些对特定黑客攻击有反应或有用的端口。扫描程序会报告这些有响应的监听者，分析弱点，并将这些弱点与已知黑客方法数据库进行交叉引用，以备后用。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_140_0.png)

> 本书中描述的技术涉及严重的法律问题。如果没有获得目标公司的书面同意，这些程序中的大多数在美国和许多其他国家都是非法的。作者或出版社对本书中包含信息的使用或误用不承担责任。

### 扫描技术

漏洞扫描器的功能可以分解为三个步骤：定位节点、在节点上执行服务发现，最后测试这些服务是否存在已知的安全漏洞。一些

本节描述的扫描技术能够穿透防火墙。虽然安全与黑客世界中部署了众多工具，但很少有工具的地位高于扫描器。

> 在本书中，防火墙被定义为一个旨在保护组织网络免受来自其他网络（如互联网）的外部威胁的安全系统。防火墙阻止组织内的计算机与外部计算机直接通信，反之亦然。相反，所有通信都通过组织网络外部的代理服务器进行路由；由代理服务器决定是否允许特定消息或文件安全地通过到组织网络。

扫描器在通信介质上发送多个数据包，遵循利用服务端口的各种协议，然后监听并记录每个响应。本章稍后将介绍的最流行扫描器（例如 `nmap`）采用已知技术来检查端口和协议，包括：

- **TCP 端口扫描**。这是最基本的扫描形式。使用此方法，你尝试建立一个完整的 TCP 端口连接，以确定该端口是否处于活动状态，即“正在监听”。

- **TCP SYN 扫描**。这种技术通常被称为*半开*或*隐蔽*扫描，因为你没有建立完整的 TCP 连接。你发送一个 SYN 数据包，仿佛你要建立一个真实连接，并等待响应。SYN/ACK 表明该端口正在监听。因此，RST 响应表明该端口未监听。如果收到 SYN/ACK，你立即发送 RST 来终止连接。这种扫描技术的主要优点是更少站点会记录它。

- **TCP FIN 扫描**。有时，即使是 TCP SYN 扫描也不够隐蔽，无法避免被记录。某些防火墙和包过滤器会监视针对受限端口的 SYN，并且 Synlogger 和 Courtney 等程序可用于完全检测这些扫描。另一方面，FIN 数据包可能能够无阻碍地通过。其理念是，关闭的端口倾向于用适当的 RST 回复你的 FIN 数据包，而开放的端口倾向于忽略相关数据包。
