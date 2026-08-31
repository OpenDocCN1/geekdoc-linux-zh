
# Kali Linux 上的 Xplico 介绍及安装方法

> 原文：<https://blog.eldernode.com/install-xplico-on-kali-linux/>

![Introducing And How To Install Xplico On Kali Linux](img/11456efd74d4afa6c08db786506d66fd.png)

`Xplico`是一个**网络取证分析工具**（Network Forensic Analysis Tool）。它使用**端口独立协议识别技术**（Port Independent Protocol Identification）识别协议并重构数据。该软件是免费开源的，遵循 GNU **通用公共许可证第 2 版**（GPLv2）。`Xplico`提取并重建所有网页内容，如图像、文件、cookies 等。您可以从互联网流量捕获中提取`Xplico`所包含的应用程序数据。请继续阅读本文，了解**Kali Linux 上 Xplico 的介绍及安装方法**。在 [Eldernode](https://eldernode.com/) 上选购您心仪的 [Linux VPS](https://eldernode.com/linux-vps/)，然后继续阅读。

## Kali Linux 上的 Xplico 介绍

### Xplico 特性

1. `Xplico`支持 HTTP、SIP、POP、SMTP、TCP、UDP、IPv6 等协议。
2. `Xplico`是多线程的。
3. 在 [SQLite 数据库](https://blog.eldernode.com/migrate-sql-databases/)或 MySQL 数据库和/或文件中输出数据和信息。
4. 根据流的数量、协议类型以及计算机 RAM、CPU、HD 访问时间的性能，`Xplico`提供实时细化。
5. TCP 重组，对任何数据包进行 ACK 验证或软 ACK 验证；TCP/IP 协议解码器。
6. 从包含在输入文件中的 DNS 包进行反向 DNS 查找，而非从外部 DNS 服务器。
7. 唯一的限制是硬盘大小，数据输入或文件输入数量没有大小限制。
8. 支持 IPv4 和 IPv6。
9. 输入接口、协议解码器和输出接口均为模块，每个`Xplico`组件都是模块化的。
10. `Xplico`能够轻松创建任何类型的调度程序，以最合适、最有用的方式组织提取的数据。
11. 网络和数字取证。
12. 数据包嗅探器。
13. 嗅探器。
14. PCAP 解析器。
15. `Xplico`能够对 140 多种协议进行分类（应用程序）。

### 模块讲解

`Xplico`能够读取流量数据。由于协议种类繁多，它将从这些数据中解析信息，并最终将信息发送到期望的输出目的地。上述三个部分属于不同类型的模块，下面将解释它们是插件还是模块。

**捕获模块**：理论上，这些模块允许与任何类型的数据采集系统接口。这些模块位于`capture`顶层目录中。

**解析器模块**：这些模块分为支持 eth、IP、tcp 等协议的子目录。它们可以破译协议，并从流量中提取特定于协议的信息，位于`dissectors`的顶级目录中。

**调度模块**：理论上，这些模块允许通过套接字连接与任何类型的数据存储系统接口，例如目录/文件、SQLite、Oracle、MySQL、PostgreSQL、系统存储。它将数据导出到上述数据库和套接字目的地。调度模块能够在不轻易修改解析器模块的情况下实现这一点。这些模块位于`dispatchers`顶层目录中。

### Xplico 接口

您可以使用带 Web 界面的`Xplico`来创建新案例、上传新文件或显示任何已解码的材料。`Xplico`接口基于 CakePHP 框架，用 PHP 开发。该接口使用 SQLite 或 MySQL 数据库。此外，`Xplico`也可在控制台模式下使用，作为允许您解码单个`pcap`文件、pcap 文件目录或从 eth0、eth1 等以太网接口实时解码的替代方案。

### Xplico 组件

`Xplico`系统由以下 4 个组件构成：

1. 解码器管理器
2. IP 解码器
3. 数据操纵器
4. 可视化系统

您可以通过上传 PCAP 捕获文件来开始新案例，或在连接到`Xplico` Web 界面时从现有接口实时获取数据。

### Xplico 替代品

您还可以使用其他一些取证分析工具，例如：

1. 黑客攻击（Hacking）
2. 无 SIF（NoSIF）
3. 凯恩（Kaine）
4. 预发现法医（Pre-Discovery Forensics）
5. 五向取证（Five Directions Forensics）

### 截图

**VoIP：SIP 和 RTP**（无信令协议）。

![SIP and RTP](img/b37b604a3074005656137b121566f69a.png)

**DNS 图表**

![Dns Graphs](img/59ecf300893a68d017d3024e1b518cfb.png)

---

![Dns Graphs](img/3dad1f3b7caad421fcd955057f4dac32.png)

**登录页面和案例列表页面。**

![Login page](img/087a73d8a3575fb495024285ac259ca4.png)

---

![Cases list page - Install Xplico On Kali Linux](img/16d5ccc1a8adc9c1cb302c2f5ee2679c.png)

**会话页面。**

![Session pages - Install Xplico On Kali Linux](img/c0e25ab15a9de6a279aea31e5226a4f3.png)

---

![Session pages - Install Xplico On Kali Linux](img/299ffab95994b2d6059bd0071ab016d8.png)

**电子邮件页面。**

![Email pages - Install Xplico On Kali Linux](img/8120b8fc94d28bc9652b3c9e56ed7b6f.png)

**网页。**

![Web pages](img/ad8159d8d30dc8cde59bfa1e052c89ce.png)

**视频和图像页面。**

![video pages](img/3216b1faba62e478e06e476e6795bb17.png)

---

![Image page](img/df9b93c30f7f257714885097090315cc.png)

**FTP 页面。**

![Ftp pages](img/6d83076c4b1b4d2fab80a4f9bdaafca6.png)

---

![Ftp pages](img/812fc066fbc696ae9c6f06208914a684.png)

**彩信页面。**

![MMS pages](img/7e297263994aaf46ae053670e03d8cba.png)

---

![MMS pages](img/438e2fb7f2025d874e05d002c1c2a985.png)

**GeoMap 页面。**

![GeoMap page Introducing And How To Install Xplico On Kali Linux](img/556cfa4723a2cc2c470e4e106cbc11eb.png)

![MMS pages](img/7e297263994aaf46ae053670e03d8cba.png)

## 如何在 Kali Linux 上安装 Xplico

默认情况下，`Xplico`在 DEFT Linux、Kali Linux 和 CAINE Linux 上可用。`Xplico`能够从 pcap 文件中提取每封电子邮件（POP、IMAP 和 SMTP 协议）、所有 HTTP 内容、每个 VoIP 呼叫（SIP、NGCP、H323）、FTP、TFTP 等。

要安装`Xplico`，您只需运行以下命令：

```
sudo apt-get update
```

```
sudo apt-get install xplico
```

它将安装`Xplico`及所有需要的软件包。

然后，使用下面的命令安装其依赖项：

```
sudo apt-get install
```

最重要的是，您也可以通过 [Kali.org](https://tools.kali.org/kali-metapackages) 网站安装取证元包。如果您安装元包，您将能够安装相同类别的所需工具，如无线、漏洞评估和取证工具。

## 结论

在本文中，您了解了 Kali Linux 上 Xplico 的介绍及安装方法。从现在起，您将知道如何安装`Xplico`，以及为什么需要使用这个强大的工具来分析具有多个协议解析器的网络流量。如果您有兴趣阅读更多内容，可以查阅另一篇关于 [Kali Linux 服务器及其应用介绍](https://blog.eldernode.com/introduction-kali-linux-server-and-its-applications/) 的文章。
