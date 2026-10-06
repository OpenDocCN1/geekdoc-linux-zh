

如果你展开一个分支，你将看到子文件夹。其中许多子文件夹又有更多的子文件夹，在到达特定条目之前，可能多达四个或更多子文件夹。Windows 注册表中的特定条目被称为“键”（key）。键是一个包含你系统某些特定方面设置的条目。如果你修改了注册表，你实际上是在更改特定键的设置。

这是关于注册表的简要概述。如果你打算对注册表进行比设置适当安全设置更广泛的工作，可以使用以下资源：

- - 50 最佳 Windows 注册表黑客技巧：https://www.howtgeek.com/howto/37920/the-50-best-registry-hacks-that-make-windows-better/

- - Windows 注册表技巧：http://techtweek.com/windows/all-important-windows-registry-tips-and-tweaks

- - 微软 Windows 注册表支持：https://support.microsoft.com/en-us/help/256986/windows-registry-information-for-advanced-users

> 提示：安全注册表设置

请记住，Windows 注册表控制 Windows 的一切。因此，为了真正加固 Windows，你必须安全地配置注册表。遗憾的是，注册表的默认设置是不安全的。本节描述了如何在你的机器上应用安全注册表设置。第 12 章“评估系统安全”在评估系统的章节中提供了有关安全注册表设置的更多信息。你将学习有关在线可用的软件产品，这些产品会通知你机器上任何不安全的注册表设置。这些工具由第三方供应商出售，不是 Windows 的一部分。

请记住，注册表设置在不同的 Windows 版本中可能会发生变化，因此你可能找不到以下一个或多个设置，或者它们的位置略有不同。要查找并检查你针对任何这些设置的注册表设置，只需展开相应的节点并进入特定键。例如，第一个是 HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer。你可以先展开 LOCAL_MACHINE\SYSTEM 节点，然后是 CurrentControlSet 节点，最后是 Services 节点。你也应该能够找到你正在寻找的特定注册表键；在示例中，我们找到了 LanmanServer。该过程适用于任何键；LanmanServer 键是为此示例随机选择的。

## 限制空会话访问

空会话（Null sessions）是一个重要的弱点，可以通过计算机上的各种共享进行利用。空会话是 Windows 指定匿名连接的方式。每当你匿名连接到任何服务器时，你都会引入重大的安全风险。通过添加 RestrictNullSessionAccess 来修改对计算机共享的空会话访问，这是一个注册表值，用于切换空会话的开启或关闭，以决定服务器服务是否允许没有用户名和密码认证的系统帐户客户端访问。将该值设置为 1 可以限制未身份验证用户对所有服务器管道和共享的空会话访问，但 NullSessionPipes 和 NullSessionShares 条目列出的项除外。

键路径：HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer
操作：确保设置为：值 = 1

## 限制通过命名管道的空会话访问

更改通过命名管道（named pipes）访问空会话注册表设置的原因与前面的空会话注册表设置相同。限制此类访问有助于防止通过网络进行未经的访问。要限制通过命名管道和共享目录的空会话访问，请编辑注册表并删除值，如表 8-5 所示。

键路径：HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer
操作：删除所有值

表 8-5 TCP/IP 栈注册表设置

| 键路径 SourceRouting | 推荐值 |
|---|---|
| DisableIPSourceRouting | 2 |
| EnableGWDetect | 0 |
| EnableCMPRedirect | 0 |
| EnablePMTUDiscovery | 0 |
| EnableSecurityFilters | 1 |
| KeepAlive | 300,000 |
| NoNameReleaseOnDemand | 1 |
| PerformRouterDiscovery | 0 |
| SynAttackProtect | 2 |
| TcpMaxConnectResponseRetransmissions | 2 |
| TcpMaxConnectRetransmissions | 3 |
| TCPMaxPortsExhausted | 5 |

## 限制匿名访问

匿名访问注册表设置允许匿名用户列出域用户名并枚举名称。它应该被关闭。该键的可能设置为：

- 0—允许匿名用户
- 1—限制匿名用户
- 2—允许具有显式匿名权限的用户

键路径：HKLM\SYSTEM\CurrentControlSet\Control\Lsa
操作：设置值 = 2

## 正确配置 Windows

> 注意
> 所有键都位于此路径：HKLM\SYSTEM\CurrentControlSet\Services\Tcpip。

## TCP/IP 栈设置

许多注册表设置影响 TCP/IP 栈处理传入数据包的方式。妥当设置这些设置有助于防止你受到 DoS 攻击的脆弱性。这一过程（堆栈调优）在第 2 章“攻击类型”中描述。由于这些设置都是关联的并位于相同的键路径，因此它们在表 8-5 中一起显示。

如表 8-5 所示，这些设置大部分用于防止数据包重定向，更改连接的超时时间，并通常更改 Windows 处理 TCP/IP 连接的方式。你可以在微软网站上找到有关设置 TCP/IP 栈注册表设置建议的更多详情：https://msdn.microsoft.com/en-us/library/ff64853.aspx。

## 提示：默认共享

Windows 操作系统在每次安装后使用系统帐户打开默认共享文件夹。因为它们是默认共享，它们对于所有 Windows 机器都是相同的。由于它们是默认共享，它们对于所有 Windows 机器都是相同的。由于它们是默认共享，它们对于所有 Windows 机器都是相同的。这些共享可以被黑客作为切入点。你可以通过两种方式禁用默认共享：

- 1. 停止服务，这将移除对计算机的共享。（但是，你仍然可以访问。）
- 2. 编辑注册表。要更改注册表中的默认共享，请转到 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters。对于服务器，设置为0。对于工作站，编辑 AutoShareWks。由于某些原因，注册表没有它：https://social.technet.microsoft.com/Forums/en-US/c9d61c2-1059-4a8a-a6bd

有关默认共享的更多信息或查看有关它们的公告，请咨询以下网站：

- www.cert.org/historical/advisories/CA-2003-08.cfm
- www.sans.org/top20/

## 注册表的远程访问

注册表的远程访问是另一个黑客的漏洞。Windows XP 注册表编辑工具默认支持远程访问，但只有管理员应该拥有注册表的访问权限。幸运的是，后续版本的 Windows 默认关闭了此功能。事实上，专家建议任何人都不要远程访问。这一点是有争议的。如果你的管理员经常需要远程更改注册表，那么完全阻止远程访问将降低他们的工作效率。然而，完全阻止注册表的远程访问更为安全。要限制对注册表的网络访问：

- 1. 在注册表中添加以下键：HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\ControlSecurePipeServers\winreg2. 选择 winreg，点击安全菜单，然后点击权限。
- 3. 将管理员设置为完全控制，确保没有其他用户或组，然后点击确定。
   推荐值 = 0

## 其他注册表设置

调整之前讨论的注册表设置将帮助你避免 Windows 注册表设置中常见的安全漏洞，并增加任何服务器的安全性。然而，为了最高安全性，管理员花时间仔细研究注册表，寻找任何可以变得更安全的区域。你可能想要查看的一些额外设置：

- 限制对注册表的匿名访问
- NTLMV2（影响发送到服务器的密码安全性）
- KeepAlive（影响保持连接活跃的时间）
- SynAttackProtect（防止一种非常特定的 SYN 攻击）

## 服务

服务是在计算机用户直接干预的情况下运行的程序。在 Unix/Linux 环境中，这些被称为守护进程（daemon）。你计算机上的许多项目都作为服务运行。互联网信息服务、FTP 服务和许多系统服务都是很好的例子。任何运行的服务都是黑客的潜在切入点。显然，你的计算机必须运行服务以执行其所需的功能。然而，你的机器上存在你未使用的服务。如果你不使用某个服务，应该将其关闭。

