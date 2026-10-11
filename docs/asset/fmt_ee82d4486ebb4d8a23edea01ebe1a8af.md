
## 第 10 章 UNIX

到此为止，我们一直关注的是 Linux 宿主机，并简要查看了微软技术。现在，我们将查看一种早于 Linux 的操作系统——即 UNIX。你可能很难辨别这两者之间的区别，在很多情况下，它们之间真的没有区别，因为那些诞生于 UNIX 系统的工具和程序已经逐渐进入了 GNU/Linux 的世界。在本章中，我们将使用一个真实的 UNIX 环境——Solaris 10，作为我们所探索的各种黑客活动的背景。我们还将向你展示如何在你的 Linux 发行版中复刻存在缺陷的 UNIX 服务，例如你一直在使用的 Ubuntu 虚拟机，以及我们可以用于测试的某些源 UNIX 发行版，我们还包含了一个供本章节使用的预构建实验室。在商业环境中，你可能会发现许多付费的 UNIX 发行版，它们由惠普、IBM 和甲骨文等公司提供。这些公司提供自己品牌的 UNIX，通常会附带服务水平协议和技术支持。这使得这些 UNIX 版本比 Linux 等开源操作系统更受企业欢迎，因为企业通常需要供应商的支持。

315 手动黑客，第一版。Matthew Hickey 和 Jennifer Arcur。
© 2020 John Wiley & Sons, Inc. 2020 年由 John Wiley & Sons, Inc. 出版。

### UNIX 系统管理

如果你打算黑进 UNIX，你需要像 UNIX 系统管理员一样思考。我们将像管理员一样查看管理工具和实用程序，尽管我们会访问某些我们没有凭据的区域。如果你不熟悉 Linux、UNIX 以及不同形式的 UNIX 之间的差异，在 `bhami.com/rosetta.html` 有一个非常好的网站，那里是“系统管理员的 UNIX 翻译器”所在地。假设你想知道如何在特定的基于 UNIX 的系统如 IBM 的 AIX 中执行某特定任务。假设你想在系统上运行 `uname` 命令，但它不起作用。你可以尝试使用等效的命令。Rosetta 石碑列出了 `prconf`、`lsconf` 以及其他你可能在 IBM AIX 系统上尝试的命令。只要你熟悉 UNIX 系统或 Linux，就可以利用这个资源帮助你在其他变体之间穿行。

> 提示：一位黑客将 Rosetta 石碑转换成了 SQLite 数据库，你可以在这里找到：`github.com/hackerhouse-opensource/tools/blob/master/rosetta.db`。如果你发现自己处于一个没有出站连接的网络中，并且需要在表中查找命令，这非常有用——你只需要在本地搜索你需要的命令即可。

### Solaris

在本章中，我们将向你展示来自名为 Solaris 的 UNIX 发行版的示例，它由太阳公司 Sun Microsystems 开发，该公司已于 2010 年被甲骨文收购。这个特定的 UNIX 变体非常有意思，因为它曾尽管被广泛使用，但包含许多有趣的缺陷和漏洞。如果你在 20 世纪 90 年代后期或 21 年代初运行这些系统并连接到互联网，那么你的机器极有可能已被各种个人和组织攻破多次。

这段时期是黑客活动活跃的时期，特别是针对 UNIX 系统。你可能认为最初负责这个操作系统 OS 的太阳公司并不是真的名声显赫或明显。但太阳公司对计算世界做出了巨大贡献。除了开发 Solaris 之外，太阳公司还创建了 Java 编程语言；网络文件系统 NFS；可扩展处理器架构 SPARC，这是一种早期且商业成功的 RISC 架构以及许多其他技术。太阳公司还负责开发外部数据表示 XDR 格式，这是许多协议用于系统间传输数据的底层数据格式，包括 NFS 和开放网络计算 ONC。

我们将介绍一些与 X 窗口系统 X Window System 交互的工具，允许接管摄像头并在远程主机上截屏。我们还将回顾 Solaris 时代合法 UNIX 管理员会使用的工具，如 R 服务和 Telnet。此类工具和服务在现实世界中已不再见到了，但偶尔还会出现。我们还将查看一些据报道由国家安全局 NSA 开发的工具，这些工具几乎绝不打算公开，但现在已经完全公开了！

### 第 10 章 » UNIX 319

这里是我们将讨论的一些工具列表：

- “经典” UNIX 管理工具，如 Telnet、Finger 和 Cron
- RPC 工具，如 RPCinfo 以及美国 NSA 的 EBBSHAVE 漏洞
- R-services 客户端程序
- SNMP 工具，如 SixtySiOne、SNMPcheck 以及美国 NSA 的 Ewok
- X Windows 工具；例如 Xwd、Xdotool、Xwininfo 和 Xspy

> **注意** 许多开源黑客工具已经泄露并现在处于公有领域。我们无法确定这些工具是否来自美国国家安全局 NSA，但我们可以非常确定 `code.nsa.gov` 上的资源来源。你可以在那里找到许多由 NSA 开发的开源软件程序。

### Solaris 端口扫描

以下是对运行 Solaris 10 的虚拟机进行基础端口扫描 `nmap <TargetIP>` 的结果。在本章中，我们将逐步分析其中的许多端口。

```
Nmap report for 192.168.56.107

Host is up (0.00050s latency).

Not shown: 977 closed ports

PORT STATE SERVICE

21/tcp open ftp

22/tcp open ssh

23/tcp open telnet

79/tcp open finger

111/tcp open rpcbind

513/tcp open login

514/tcp open shell

898/tcp open sun-manageconsole

4045/tcp open lockd

5987/tcp open wbmem-rmi

5988/tcp open wbmem-http

6000/tcp open X11

7100/tcp open font-service

32771/tcp open sometimes-rpc5

32772/tcp open sometimes-rpc7

32773/tcp open sometimes-rpc9

32774/tcp open sometimes-rpc11
```
