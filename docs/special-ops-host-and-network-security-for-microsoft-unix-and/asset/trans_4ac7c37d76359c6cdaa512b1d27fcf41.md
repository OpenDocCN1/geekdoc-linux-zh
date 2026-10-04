

# 攻击与防御 Windows XP 专业版 • 第 4 章

8195/udp开放未知
42811/udp开放未知

Nmap 扫描完成 -- 1 IP 地址 (1 个主机在线)，耗时 47 秒

如你所见，该系统开放了 TCP 和用户数据报文 (UDP) 端口。现在，你最初可能没有注意到的区别是这些端口与 Windows 2000 和 NT 等之前的平台不同。端口 445 在 XP 中通常用于身份验证，是 Windows 2000 和 XP 特有的端口，代表 Microsoft Direct Host（微软直接主机）。存在许多运行端口扫描的工具；同样，你可能可以在每种基于网络的编程语言中找到端口扫描器——此外，此功能内置在几乎每个商业和公共漏洞扫描器中。

# ICMP 发现与指纹识别

互联网控制消息协议 (ICMP) 是尝试对远程系统进行画像时最有用的协议之一。协议中可识别的异常允许你对目标主机的操作系统做出合理的推断。了解目标操作系统的明显益处在于针对特定操作系统确定攻击分类。除了 ICMP 之外，其他分析手段（如 Banner 信息、服务和协议）也是任何操作系统指纹识别方法的其他极佳补充。所有漏洞扫描产品都实现了某种形式的操作系统识别，但行业标准是 NMAP 的操作系统指纹识别库。因此，许多扫描器只是简单地实现了 NMAP 的功能。除了 NMAP 之外，产品中其他专有的操作系统检测工具包括 FoundScan 和 ISS。你可以在各自的网站上找到更多特定厂商的实现细节。

- Retina www.eeeye.com
- NMAP www.insecure.org/nmap
- Foundscan www.foundstone.com
- ISS www.iss.net

另一个很好的信息来源是 http://www.sys-security.com/html/projects/icmp.html。Sys Security Group 的创始人 Arkin 对 ICMP 进行了广泛研究，并发表了大量的论文、工具和入侵检测特征码，这些在教育上可能大有裨益。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_125_0.png)

# 第 4 章 • 攻击与防御 Windows XP 专业版

接下来的 NMAP 输出显示，NMAP 操作系统检测功能将操作系统缩小到三个潜在的匹配项之一。如果你后后本章的图 4.2，EEye 的 Retina 仅将潜在操作系统缩小到四个。

```
Starting nmap V. 3.00 ( www.insecure.org/nmap )
Interesting ports on (10.0.100.100):
Port            State           Service
139/tcp         open            netbios-ssn
Remote operating system guess: Windows Millennium Edition (Me), Win 2000,
or WinXP
```

Nmap 扫描完成 — 1 IP 地址 (1 个主机在线)，耗时 2 秒

要利用 NMAP 操作系统检测功能，你必须扫描并接收多个开放端口之一的响应。搜索基于微软的操作系统的良好端口是 139（常用的 NetBIOS 端口），利用 NMAP 确定操作系统类型。

# 收集相关的系统信息

可以且能够确定的杂杂相关系统信息包括：

- **MAC 地址**：介质访问控制 (MAC) 地址用作网络层和应用层之下的可寻址引用，用于直接的系统间通信。在大多数情况下，用户可以通过确定其 MAC 地址来判断正在使用什么类型的网卡。除了收集目标信息外，MAC 地址还可以用于伪造目标地址以及会话劫持攻击。
- **主机名**：系统的主机名是寻址或引用特定计算机系统的另一种方式，可以用于许多中间人攻击和直接攻击。在大多数情况下，完整的主机名还包含特定网络和域特定的信息。
- **主机路由 (Route to host)**：到主路由是通往目标系统的可识别路由或映射。在大多数情况下，你可以学习数据包在传输到目标系统途中经过的每个系统的 IP 地址。发现相关的主机路由是非常重要的，因为它允许

![](img/729efc56f204a2ebffb8295c3a2dfdfb_126_0.png)

用户可能具有攻破或针对附近系统的能力，希望这在破解初始目标系统时提供优势。此外，可以分析多条路由以创建目标系统环境的网络地图。

如果你有能力从目标系统所在的网络分段截获数据包，可以在无需验证的情况下确定大部分这些内容。如果你没有本地访问权限，获取 MAC 地址和相应的服务器可能会很困难。像 Retina 和 FoundScan 等漏洞扫描器会检索所有这些可用信息。你可能想要使用的工具还有 GetMAC 和 CTIS（你可以在 www.packetsecurity.org 找到两者）、nslookup、tracer 和 Ethereal。Nslookup 和 tracer（Unix 版本为 Traceroute）内置在几乎所有的 Windows 和基于 Unix 的操作系统中。Ethereal 的网站是 www.ethereal.org。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_127_0.png)

# 枚举用户、组和共享

与任何操作系统一样，Windows XP 专业版内置了用户和组。除了用户组和共享外，可以枚举这些用户。默认配置且可远程访问的系统共享与特定的系统目录绑定。例如，C 共享映射到 C:\，Admin 共享映射到 C:\Winnt\。IPC 共享供匿名用户使用空会话连接。

XP 专业版上默认配置的组包括：

- Administrators (管理员)
- Power Users (高级用户)
- Guests (访客)
- Backup Operators (备份操作员)
- Remote Desktop Users (远程桌面用户)
- Users (用户)
- Replicator (复制器)
- Debug Users (调试用户)
- HelpServicesGroup (帮助服务组)
- Network Configuration Operators (网络配置操作员)

XP 专业版默认配置的用户包括：

- Administrator (管理员)
- Guest (访客 (已禁用))

XP 专业版默认配置的共享包括：

- C$
- Admin$
- IPC$

图 4.2 所示的 Retina 漏洞扫描器是一个不错的工具，可以快速对目标系统进行画像。试用版可以下载并使用 15 天，无费用。图 4.2 显示了针对我们的目标专业系统执行的完整 Retina 漏洞和端口扫描。如你所见，Retina 识别了开放的共享、TCP 端口，

![](img/729efc56f204a2ebffb8295c3a2dfdfb_128_0.png)

# 攻击与防御 Windows XP 专业版 • 第 4 章

假设的操作系统、MAC 和主机路由（此处被省略）。除了这些，它还识别了在该机器上实现的多种服务和协议。Retina 等工具简化了画像过程并可以快速执行许多攻击。

# 图 4.2 Retina 

![](img/729efc56f204a2ebffb8295c3a2dfdfb_129_0.png)

# XP 互联网控制防火墙的异常

正如我讨论过的，Windows XP 带有互联网控制防火墙 (ICF)。ICF 不仅仅是一个管理出站连接的动态 IP 表过滤器。出站连接存储在动态表中，因此其响应包允许本地系统接收。该技术禁止了未请求的 ICMP 请求以及寻找错误或消息的伪造响应，此外禁止未请求的 TCP 数据包。单此这一事实就会阻碍大多数扫描工具，导致它们无法获取任何未请求或嗅探的信息。图 4.3 显示了当你对运行 ICE 的 XP 专业版系统执行单个系统扫描时，Retina “弹出”的错误。告警错误的原因是 Retina 没有收到任何系统发现响应。

