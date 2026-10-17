
Christensen 的站点针对大多数当前 Solaris 版本（从 2.5 到 8）的日志软件，以及针对 Sparc 和 Intel 平台版本方面享有誉。SunFreeware 拥有大量适用于 Solaris 标准包格式和 Web Start 格式的预编译应用程序。还包含了这些软件的源代码，以防编译时的默认值不是你想要的。我在 SunFreeware 中发现最有用的部分是关于为预二进制文件制作自定义包的信息。Solaris 包是分发软件的一种极方法，但对许多管理员来说是个谜。Christensen 优秀的教程，加上几个 SunFreeware 客户提供的后续细节，是学习如何制作、验证和分发包的良好起点。另一个值得提及的站点是 `www.securityfocus.com` SecurityFocus。它更是一个软件分发站点的门户，SecurityFocus 包含了一些优秀的 Sun 安全软件和一些

# 使用免费安全工具加固 Solaris 安全 • 第 3 章

一个无可击的漏洞和利用数据库（包括修复和规避方案的信息），涉及许多种操作系统，包括 Solaris。该网站还托管了各种邮件列表，其中一些是针对 Solaris 的。Solaris 邮件列表通常会有非常优秀、专业级的讨论，这对于新手和经验丰富的管理员来说都将是极具价值的。

## Nmap 基础用法

Nmap 拥有大量的命令行选项来修改和引导其行为。我们将只关注其中的少数几个。运行 Nmap 最通用的方法是给它一个主机名或 IP 地址作为参数：

```
nmap [-options] <hostname>
```

你可以采取更通用一点的方法，让它执行其名称所暗示的功能，通过提供一个 CIDR 格式的网络地址来扫描整个网络：

```
nmap A.B.C.D/xx
```

在本章中，我们将重点关注以下选项和开关：

- `-sT` 启动 TCP `connect()` 扫描（在未提供其他选项时为默认值）。
- `-sU` 启动 UDP 端口扫描。此扫描需要你以 root 身份运行 Nmap。
- `-sP` 启动 ping 扫描。尝试 ping 指定的给定子网或范围内的主机。
- `-oN<logfile>` 告诉 Nmap 将其结果输出到名为 `<logfile>` 的、人类可读的 ASCII 文本文件中。
- `-O` 启动 TCP/IP 指纹识别。Nmap 尝试通过使用指纹文件（已包含）来检查并比较各种 TCP/IP 属性，从而确定目标机的远程操作系统。这需要 Nmap 以 root 身份运行。

虽然这是我们将关注的，但请记住查阅 Nmap 的文档和内置帮助。Nmap 拥有强大的功能，花一点时间学习它将会有丰厚的回报。

以我们虚构的 `la` 为例，假设你想查看 `www.incoming-traveller.com` 上哪些端口是开放的。一旦你在管理系统上安装了 Nmap 并正确配置了软件，请执行以下命令：

```
%nmap -sT www.incoming-traveller.com
```

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_97_0.png)

# 第 3 章 · 使用免费安全工具加固 Solaris

端口扫描本身可能需要 10 秒到 3 或 4 分钟，取决于扫描器发现并需要报告的端口数量。Nmap 扫描后的正常输出看起来类似于图 3.1。

## 3.1 Nmap 扫描后的正常输出

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_98_0.png)

前三个条目是显而易见的。端口 111 的条目表示该系统上运行着 `portbind` 进程，并且其他 RPC 服务也在运行。你使用 `rpcinfo` 命令收集有关这些服务的更多信息。端口 4045 和 6000 上的服务显示系统上运行着 X 会话（OpenWindows, CDE, KDE 等）。最后两个条目是开放 X 会话的产物，并可能存在漏洞，因为窗口系统可能有绑定到这些端口的存漏洞的子进程。

你可能会注意到没有 UDP 端口出现。这是因为 Nmap 需要 root 权限来进行更密集、更隐蔽的端口扫描。这在很大程度上防止了它被本地用户滥用。为了进行 UDP 扫描，切换到 root 权限执行：

```
%nmap -sU www.incoming-traveller.com
```

你将得到类似于图 3.2 的结果。这种类型的端口扫描通常需要 Nmap 花费更长时间才能完成。如你所见，`www.incoming-traveller.com` 不仅是一个 Web 服务器，还是一个 NFS 服务器（端口 2049）、syslog 服务器（端口 514）、名称服务器（端口 53）以及 X 服务器等。

这些服务中的每一个都代表一个漏洞，它可能是重大的，也可能是次要的。在过去的 24 个月中，出现了了许多 DNS/BIND 漏洞。该系统应该至少运行 BIND 8.2.3-REL，否则它可能会被几个漏洞中的一个攻破。syslog 条目是一个轻微的威胁，尽管它可能被利用来损坏或覆盖日志文件。在最坏的情况下，向 syslog 发送持续的消息可能被用来填满 syslog 文件所在的分区。这可能导致系统崩溃或不稳定。在 Solaris 系统上安装惠尔士-Packard Jetdirect/Jetadamin 软件时，经常发现 BOOTP 条目。除非 `.incoming-traveler.com` 为网络打印机提供 BOOTP 服务，否则你可以安全禁用该服务。

## 图 3.2 UDP 扫描结果

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_99_0.png)

`snmp` 和 `rpc` 服务在程序上通常互不相关，但它们值得额外关注。从某种意义上说，如果你的系统也是 NFS 服务器，那么它自然应该位于防火墙之后，并且 NFS 共享应该带有相应的权限和访问限制进行导出。诚然，这并没有完全解决 RPC `portmapper` 后面的其他服务。为了了解还有哪些服务，你需要查看 `/etc/inetd.conf` 和 `/etc/rc[1-3].d`，查看哪些 RPC 服务是在启动时启动的，哪些是需要启动的。确定你的系统提供哪些 RPC 服务的命令是 `rpcinfo`。你几乎可以将其用作 RPC 端口扫描器（尽管它不是），来查看哪些服务是已启动且可用的。

NFS 对时间戳敏感，因此系统时钟应与通用源同步。这就是 NTP 发挥用场的地方。NTP 将在将在少干预的情况下同步系统时钟，为你的网络化系统提供统一的时间戳。配置适当的 NTP 设置对你的系统威胁是极微的。

最后，需要注意的是，并不是所有服务都是根据 `/etc/inetd.conf` 启动的。大多数默认服务都是如此，但也有例外。

# 第 3 章 · 使用免费安全工具保护 Solaris

网络上的系统。假设 Incoming Traveller, Inc. 使用子网划分的 10.0.0.0 IP 空间，即 `10.1.1.0/24`。以 root 身份带有以下开关运行 `nmap`：

```
%nmap -sP 10.1.1.0/24
```

当 `nmap` 完成时（根据发现的系统数量，可能几分钟到几小时不等），你应该得到与图 3.3 类似的输出。

## 图 3.3 Nmap 对网络上 IP 和操作系统的清单结果

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_102_0.png)

接下来，使用 `-O` 选项运行 `nmap`（使用 root！）对网络上的主机进行指纹识别：

```
%nmap -O 10.1.1.0/24 >> /ip_and_fingerprints.out
```

当 `nmap` 完成后，你的文件将追加以下内容：

Starting nmap V. 2.53 by fyodor@insecure.org (www.insecure.org/nmap/)

Interesting ports on www.incoming-traveller.com (10.1.1.1:33):

(The 1517 ports scanned but not shown below are in state: closed)

| 端口 | State | 服务 |
| :--- | :--- | :--- |
| 22/tcp | open | ssh |
| 80/tcp | open | http |
| 111/tcp | open | sunrpc |
| 4045/tcp | open | locked |
| 6000/tcp | open | X11 |
| 32771/tcp | open | sometimes-rpc55 |
| 32780/tcp | open | sometimes-rpc23 |

TCP Sequence Prediction: Class=truly random

Difficulty=99999999 (Good luck!)

Remote operating system guess: Solaris 2.6 - 2.7 with tcp_strong_iss=2
