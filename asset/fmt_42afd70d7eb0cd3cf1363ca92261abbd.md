
- [http://www.cert.org/advisories/CA-2001-02.html](http://www.cert.org/advisories/CA-2001-02.html) **2001 年 1 月** _CERT® Advisory CA-2001-02 Multiple Vulnerabilities in BIND_

## 根服务器

有关根服务器的详细信息和讨论：

- [http://www.wia.org/database/](http://www.wia.org/database/)

- [http://www.icann.org/icp/icp-3.htm](http://www.icann.org/icp/icp-3.htm) **2001 年 7 月** _ICP-3: A Unique, Authoritative Root for the DNS_

- **RFC-2870 June 2000** _Root Name Server Operational Requirements_

## 主主服务器和辅助（从）服务器

区域的所有权威服务器都由该区域数据库中的 NS 资源记录标识；例如，你可以列出区域的这些记录

```
host -t ns example.com
```

从外部，你只能了解到服务器的这些信息；你无法分辨哪个是主服务器，哪些是辅助服务器（从服务器）。

在内部，主主服务器由其配置文件中的一个特殊选项标识。（配置文件与作为对该服务器接收到的查询的回复发送的资源记录数据库是分开的。）

- BIND 版本 4（现在已过时）使用语句 `primary`

- BIND 版本 8 和 9 使用语句 `zone ... type master`

辅助（从）服务器以类似方式标识：

- BIND 版本 4 使用语句 `secondary`

- BIND 版本 8 和 9 使用语句 `zone ... type slave`

服务器扮演的角色特定于区域，因此服务器软件的一个实例可能同时对某些区域是主主服务器，对其他区域是辅助（从）服务器，对另一些区域是仅缓存服务器。

## 缓存

在模块 8.10 中我们说客户端不缓存 DNS 响应。然而，正如我们在模块 19.7 中将看到的，当 Microsoft Windows NetBIOS 程序使用 DNS 时，它们 _确实_ 缓存响应。

## 域和主机名配置

Windows-2000 对 Windows 计算机名称和你给机器的 DNS 名称施加的约束与 NT-4 不同：

- **MS-KB-Q227410** _Computer Name and hostname Must Be the Same in Windows 2000_

尽管我们在第 8.14 节中说了什么，但有些人认为有充分的理由让 Windows 主机名与 DNS 或 WINS 名称不同：

- http://www.windowsitlibrary.com/Content/386/10/5.html NetBIOS: Friend or Foe? 为将“Computer name”设置为机器的 MAC 地址并使用更常规的描述性名称作为 DNS 名称提出了论据。（然而 Windows-2000 强制你对两者使用相同的名称。）

在第 7.4 节中我们提到 NT 不会尝试使用 DNS 解析简单名称（即没有点的名称）例如“bob”。这是正确的行为 – 请参阅：

- MS-KB-Q230744 Windows NT 4.0 SP4 DNR 客户端不会发送未限定 DNS 查询（“DNR”不是笔误：它代表“domain name resolver”域名解析器）。在引入此修改之前，Win-NT 的行为与 Win-9x 仍然一样：如果 Domain 和 Domain Suffix Search Order 均为空，当你 ping bob 时，会为名称 bob 发送 DNS 查询。这将一直追溯到根 DNS 服务器（其管理员会咆哮并抱怨大约 90% 的根服务器查询都是来自 Windows PC 或其使用的服务器的此类未限定名称）。出于这个原因，以及我们在第 8.13 节 – 第 8.15 节中描述的使用便利性，你应该养成始终定义其中一个域相关字段的习惯。这将使互联网对每个人来说都变得更好！

- MS-KB-Q198550 SP4 更改 DNS 名称解析

- MS-KB-Q195611 DNS 客户端不会尝试 DNS 服务列表中的所有服务器（错误，已在 SP5 中修复）

- MS-KB-Q214467 Windows NT 4.0 DNR 仅“退化”两个域后缀

## 反向查询

用于反向查询的相同侧向思维方法也在完全不同的上下文中使用，以发布已知发送垃圾邮件的电子邮件服务器列表（第 25.4 节）。

## 杂项

“Secure DNS” 正在开发中，这样你就可以真正知道 DNS 为机器名提供的 IP 地址是正确的，而不是有人想要劫持该机器流量的假地址。Secure DNS 也将用于分发加密公钥（第 27.6 节）。

如果你的站点将来扩展，而不是在单台机器上运行所有公共服务器（Web、FTP、SMTP 电子邮件、POP3 电子邮件、DNS 等），你可能需要将功能拆分到多台机器上以处理增加的负载。你可以通过提前规划 IP 地址分配和 DNS 配置来为自己节省大量麻烦。详情请参阅：

- http://www.uit.co.uk/resources > DNS 规划。

单个名称（例如 www.ibm.com）可以有多个 A 记录，即多个 IP 号码。正如我们在第 14 章中将看到的，许多网站使用此功能在多个 Web 服务器之间共享负载。

几乎所有 DNS 流量都使用 UDP 传输，我们将在第 15 章中介绍，并发送到端口 53。我们将在第 10 章中解释 UDP 和 TCP 以及端口。现在，如果你只想跟踪 DNS 流量，可以使用如下命令指示 `tcpdump` 这样做：

```
tcpdump -n port 53
```

对于区域传输，以及如果你使用 `nslookup` 的“-vc”选项（“virtual circuit”虚拟电路），DNS 使用 TCP 而不是 UDP。然而，现在请忘记这一点，因为我们要到第 10 章和第 15 章才解释 TCP 和 UDP；我们在这里提到它只是为了完整性。

# 附录

- 附录 6：使网络设置永久化 – Debian Linux

- Web 附录 7：在 Windows-NT 上设置简单的 DNS 服务器

- Web 附录 9：在 Linux 上设置简单的 DNS 服务器

- Web 附录 10：基本 DNS 服务器的示例 DNS 配置文件

- Web 附录 11：名称和域名注册

## 9 故障排除 DNS

- 9.1 故障排除 – 识别问题

- 9.2 失败名称解析的调试输出

- 9.3 DNS 问题和原因

- 9.4 其他名称解析系统的干扰

- 摘要

### 引言

在本章中我们介绍在使用 DNS 客户端解析名称或 IP 号码时可能遇到的各种问题

### 9.1 故障排除 – 识别问题

> **Tip:** 你经常可以通过在出现 DNS 问题时立即运行 `tcpdump -n` 来跳过下面逐步的故障排除方法。过一段时间后，你仅凭 `tcpdump` 的输出就能对正在发生的事情有一个很好的了解，尽管它很简洁。

你遇到的一些 DNS 困难可能并非由于你站点的配置错误或网络问题：

- 1.a. DNS 找不到你尝试解析的名称的 IP 地址，因为该名称不存在。如果你没有下面描述的任何错误，你将在 `tcpdump` 跟踪中看到状态 `NXDomain`（不存在的域名）：

```
192.0.2.17.3566 > 192.0.2.19.53: 19588 A? junk.example.com. (34)
192.0.2.19.53 > 192.0.2.17.3566: 19588 NXDomain* 0/1/0 (95)
```

请求名称解析的应用程序也会报告错误。如果名称解析深在应用程序内部，应用程序的错误消息可能不明确。为了确认，运行 `host` 或 `nslookup` 对导致问题的名称，然后你将得到下面的明确消息。原因可能是你打错了字，或者该名称确实不存在。

```
alice$ host junk.example.com
junk.example.com does not exist (Authoritative answer)
```

请注意 `host` 说答案是权威的（并且 `tcpdump` 通过在 NXDomain 后打印其“\*”指示它是权威的）。这意味着 DNS 真的通过了所有委派（在本例中为 **ibm.com**）并被告知该名称肯定不存在。这应该让你确信沿途没有其他问题（但该领域存在一个已知错误 – 请参阅注释）。下一个模块以完整细节展示典型的失败解析。
