

# 60 第一部分：攻击技术与防御

这些用于在交换机上对流量进行代理。考虑存在于网络交换机上的以下主机：

-   受害者主机
-   网关主机
-   恶意主机

为了执行 ARP 欺骗，主机 M 将向主机 G 和主机 V 发送 ARP 响应数据包。这些 ARP 响应数据包将导致主机 V 将主机 M 的 MAC 地址映射到主机 G 的 IP 地址上，并导致 G 将 M 的 MAC 地址映射到主机 V 的 IP 地址上。由于以太网数据包是根据 MAC 地址进行路由的，主机 M 将接收到所有在 G 和 V 之间传输的数据。现在，如果 M 通过将 MAC 地址替换为主机 G 或 V 的 MAC 地址并将这些数据包路由到正确的目的地，受害者主机 G 和 V 将完全不知道它们的连接正被主机 M 探测。可以使用 Dsniff 和 Ettercap 等工具执行 ARP 欺骗。
Ettercap 可以在 http://ettcap.sourceforge.net/ 下载。Dsniff 可以在 http://monkey.org/dugsong/dsniff 获取。

# 常见的嗅探防御措施

网络嗅探工具使得恶意用户很容易捕获网络分段上的数据。强烈建议采取以下防御措施：

-   不要使用明文协议。
-   某些交换机允许管理员静态映射 MAC 地址。然而，这对于大型企业来说可能不可行。
-   许多入侵检测系统（IDS）可以检测并报告 ARP 欺骗。可以使用 Ettercap 帮助检测网络上的 ARP 响应。

# 中间人

此类攻击涉及恶意用户拦截并更改两个或多个受害者主机之间的数据。

例如，注意，由于他已成功破解了 somecompanyasanexample.com 的内部 DNS 服务器，该入侵者可能会更改 DNS 服务器配置，使所有针对 `intranet.somecompanyasanexample.com` 的 DNS 查询都指向入侵者的 IP 地址。这将导致用户在不知情的情况下连接到入侵者的主机，而不是 `intranet.somecompanyasanexample.com`。入侵者随后可以将受害者的连接代理到 `intranet.somecompanyasanexample.com` 的真实 IP 地址。在这种情况下，入侵者将成功发起了一次中间人攻击。

# 防止中间人攻击

使用 SSH、IMAPS 和 HTTPS 等安全协议。虽然这些协议可能受到中间人攻击的影响，但它们可能利用加密密钥和证书，从而让软件客户端警告终端用户可能发生的攻击。

# 配置错误

通常，服务的配置错误会导致向未经验身份的用户暴露不必要的信息。有时，配置错误可能会导致主机被完全攻陷。常见的配置错误及其防御措施列在下面的“远程服务漏洞”章节。

# 审计并加固主机配置

定期审计和加固主机配置策略是一个好主意。请参阅本书第二部分的章节，了解如何加固策略和服务的。

# 软件漏洞

软件漏洞是由设计缺陷引起的，例如不当的输入验证和边界检查。此类漏洞通常可以远程利用，允许攻击者在运行漏洞软件的主机上执行恶意代码。

缓冲区溢出是许多可远程利用条件的原因。当进程向内存中写入超过分配的缓冲区空间的数据时，就会发生这种情况。这会导致可执行栈空间被任意数据覆盖。攻击者可以利用这种条件通过提供自己的输入，可能导致进程用攻击者提供的可执行数据覆盖其栈。如需更多信息和细节，请参阅“Aleh One”的《Smashing the Stack for Fun and Profit》，该文档位于 http://www.insecure.org/stf/smashstack.txt。

# 62 第一部分：攻击技术与防御

许多在线安全资源发布针对各种漏洞的利用代码。请对此类利用程序保持谨慎，因为它们可能各异，并且已知包含恶意后门，可能导致执行利用程序的主机被攻陷。在虚拟机环境下测试未知的利用程序是一个好主意。最广泛使用的虚拟机软件由 VMware 提供。详情请参阅 http://www.vmware.com/。

# 针对软件漏洞利用的常见防御

有时，软件漏洞的远程利用会通过漏洞公告提供，或者发布补丁。此类利用程序通常被称为零日漏洞。防御针对未公布漏洞的利用是不可能的。但除了遵循这些建议外，每位系统管理员必须监控并对异常的系统活动采取行动：

-   保持软件补丁为最新。
-   订阅漏洞监控列表，例如 Bugtraq。（更多信息请访问 http://securityfocus.com/cgi-bin/sfonline/subscribe.pl。）参阅本书参考中心中的“在线资源”部分以获取许多其他安全资源的索引。
-   为了防止某些类型的缓冲区溢出，有几种解决方案：
     StackGuard: http://www.immunix.org/stackguard.html
  -   Libsafe: http://www.research.avalabs.com/project/libsafe/
  -   StackGhost: http://stackghost.pierdas.stanford.edu/
  -   Openwall: http://www.openwall.com/linux

如果使用 Solaris，编辑 /etc/system 并添加以下行：

```
set noexec_user_stack=1
set noexec_usr_stack_log=1
```

-   监控并响应 IDS 日志。

# 远程服务漏洞

以下是常用利用的服务列表。它是基于服务已知通常监听的标准端口号。

# 识别在非标准端口运行的服务

此处列出的任何服务都可以配置为在非标准端口上监听。可以使用 Amap（可在 http://www.thehackers.com 获取）等工具来识别非标准端口上的服务。

# 关闭不必要的服务

某些服务被配置为接受任何源的连接。例如，一个 HTTP 服务器允许所有用户查看组织的网站。在这种情况下，无法隐藏组织正在运行 HTTP 服务器的事实。

然而，根据组织的需求和网络架构，某些服务可能只期望授权 IP 地址的连接。在这种情况下，应建立防火墙规则阻止来自未经授权 IP 地址的连接。此外，必须通过防火墙关闭不必要的服务。

# FTP（文件传输协议）：21 (TCP)

FTP 是一种从一个主机到另一个主机传输文件的协议。

可以使用 Hydra 暴力破解 FTP 账户。

# 暴力破解 FTP

以下是使用 Hydra 暴力破解账户的示例：

```
[bash]$ hydra -L usernames.txt -P passwords.txt
ftp.companyexample.com ftp
```

Hydra v2.0 (c) 2002) Hauser / THC - 仅允许合法用途。
Hydra 正在启动！[并行任务：4, 登录尝试：4 (1:2/p)]
[21][ftp] login: joe password: mypassword
Hydra 结束。

# 防止 FTP 暴力破解

请参见“针对暴力破解的常见防御”。由于 FTP 是一种明文协议，可以捕获在网络上传输的用户名和密码。Etter 等工具有助于获取 FTP 数据。

# 嗅探 FTP 身份验证

以下是使用 Ettercap 捕获网络上传输的 FTP 凭据的示例：

```
[bash]# ettercap -m -C -N
```

```
ettercap 0.6.7 (c) 2002 ALOr & NaGa

你的 IP: 10.0.0.102 MAC 地址: 01:11:04:6A:A3 接口: eth0

加载插件... 完成。

解析本地主机名...

* |==================================| 100.00 %

按 'h' 查看帮助...

嗅探 (基于 MAC): ANY --> ANY

TCP + UDP 数据包... (默认)

收集密码...
```

