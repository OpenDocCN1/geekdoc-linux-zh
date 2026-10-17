
<service name="ssh"/>

<service name="mdns"/>

<service name="dhcpv6-client"/>

<forward/>

</zone>

```
ping 一个主机以验证你是否无法访问外部世界。稍等后，使用 Ctrl+C 退出 ping。
```

```
[root@testvm1:~~]# ping -c3 example.com
```

```
^C
```

```
PING 10.0.2.1 (10.0.2.1) 56(84) 字节数据。
```

```
^C
```

```
--- 10.0.2.1 ping 统计 ---
发送了 3 个数据包，接收 0 个，100% 包丢失，
时间 2120ms
```

```
[root@testvm1:~~]# firewall-cmd --panic-cmd success
```

```
[root@testvm1:~~]# ping -c3 example.com
```

```
PING example.com (93.184.216.34) 56(84) 字节数据。
64 bytes来自 93.184.216.34 (93.184.216.34): icmp_seq=1
ttl=50 time=13.7ms
64 bytes来自 93.184.216.34 (93.184.216.34): icmp_seq=2
ttl=50 time=13.6ms
64 bytes来自 93.184.216.34 (93.184.216.34): icmp_seq=3
ttl=50 time=13.7ms

294
第 10 章 使用 Firewalld 管理防火墙
--- example.com ping 统计 ---
发送了 3 个数据包，接收 3 个，0% 包丢失，
时间 2012ms

rtt min/max/mdev = 13.642/13.711/13.748/0.049
```

```
[root@testvm1:~~]#
```

当恐慌模式（panic mode）开启时，不允许任何入站或出站通信。
与其他防火墙设置一样，恐慌模式可以在指定时间内开启。计时器结束后，将恢复使用配置的防火墙区域进行正常访问。然而，我不建议这样做，因为无法预测修复最初导致我们设置恐慌模式的问题需要多久。

## firewall-config GUI

除了命令行工具外，firewalld 具有一个设计良好且实用的 GUI 界面。与许多 GUI 工具一样，它可能无法在你需要管理的主机（如服务器和作为防火墙的主机）上可用。然而，当可用时，它可以让 firewalld 变得更容易一些。我们仍然需要理解背后到底发生了什么，这就是为什么我们在命令行工具上花费了大量时间——而且即使在 GUI 工具不可用时，它们也总是可用的。

## nftables

`nftables` 规则和 `nftables.service` 以及同 `nft` 命令行工具构成了一个完整的防火墙解决方案。然而，在使用 firewalld 时，`nftables` 服务是被禁用的。

295
第 10 章 使用 Firewalld 管理防火墙

我们用于定义网络接口防火墙特性的区域文件将结合 `/etc/firewalld` 中的其他配置文件，使用 `nftables` 文件格式创建规则集。`firewalld` 被用于创建 `nftables` 规则，这些规则由相应的内核模块用于检查每个网络数据包并确定它们的去去。

你可以查看所有当前的 `nftables` 规则，但尽管它们是可读的，却并不易于理解。

## 实验 10-11：查看 nftables 规则

```
此命令显示当前激活区域的所有 nftables 规则。

[root@testvm1:~]# nft list rules | less

table inet firewalld {

chain mangle_PREROUTING {

```

```
type filter hook prerouting priority mangle

priority 10; policy accept;

    }

}

chain PREROUTING {

    type filter hook prerouting priority mangle

    priority 10; policy accept;

}

chain mangle_OUTPUT {

    type filter hook output priority mangle

    priority 10; policy accept;

}

chain OUTPUT {

    type filter hook output priority mangle

    priority 10; policy accept;

}

chain mangle_INPUT {

    type filter hook input priority mangle

    priority 10; policy accept;

}

chain INPUT {

    type filter hook input priority mangle

    priority 10; policy accept;

}

chain FORWARD {

    type filter hook forward priority mangle

    priority 10; policy accept;

}

```

无论你使用防火墙还是 iptables 作为防火墙前端，你都可以列出 nftables 规则并翻到底部，找到以下由 Fail2Ban 添加的条目：

```
[root@testvm1~]# nft list ruleset | less

table ip6 filter {

chain INPUT {

type filter hook input priority filter;

policy accept;

meta l4proto tcp tcp dport 22 counter

packets 68 bytes 11059 jump f2b-sshd

300

}

chain f2b-sshd {

ip6 saddr ::1 counter packets 4 bytes

320 reject

counter packets 54 bytes 9939 return

}

}

```

```
table filter {

chain INPUT {

type filter hook input priority filter;

policy accept;

meta l4proto tcp tcp dport 22 counter

packets 62 bytes 9339 jump f2b-sshd

}

chain f2b-sshd {

ip saddr 127.0.0.1 counter packets 2 bytes

120 reject

counter packets 54 bytes 8859 return

}

}

```

现在来看几个日志文件。在 `/var/log` 中，首先查看 `/var/log/secure`。你应该看到许多指示密码失败的条目。这些是 Fail2Ban 用于检查失败情况的日志条目。

查看 `/var/log/fail2ban.log` 文件。此日志显示了在 secure 日志中发现触发条目的时间，以及为了保护系统而采取的封禁和解封操作。

请注意，在触发首次封禁之前，`f2b-sshd` 链的条目不会出现在 iptables 规则集中。一旦触发首次封禁，该链的第一行和最后一行不会被删除，但拒绝特定 IP 地址的行会随着超时被移除。弄清楚这一点花了一点功夫。

# 301

# 第 10 章 使用防火墙管理防火墙

安装 Fail2Ban 会安装 logwatch 报告 Fail2Ban 活动所需的配置文件。你可以为 Fail2Ban 创建自己的过滤器（filters）和动作（actions），但这超出了本课程的范围。

请务必查看 `fail2ban.local` 文件中的各种监狱（jails）。有很多不同的事件可以触发 fail2ban 封禁源 IP 地址访问特定端口或服务。

# 清理

在继续之前，我们需要进行一些清理工作。

找到 `ignoreself = false` 这一行，它应该是第 87 行。这是我们在实验 10-12 中修改的行。删除注释并将其更改为 `# ignoreself = true`。我们这样做是为了 Fail2Ban 再次忽略来自本地的失败登录尝试。

滚动到 `bantime = 1m` 行（第 101 行），并将其更改 10 分钟（10m）。

将 `maxretry = 2` 改回 5。

最后，停止 Fail2Ban。我们没有启用它，所以无论在什么情况下它下次启动时都不会运行。

## 总结

安全是我们系统管理员工作的重要部分，而防火墙是保持网络安全的主要工具。虽然 Linux 在初始安装时相当安全，但任何连接到有线或无线网络的设备始终都是黑客的目标。在网络与互联网交互接口的边缘设置一个良好的防火墙是确保网络加固的良好步骤。然而，如果网络中的每个主机上没有配置恰当的防火墙，攻破防火墙主机的黑客也将立即访问你网络上的每个主机。

# 第 10 章 使用防火墙管理防火墙

设置任何防火墙的最佳方法是从阻塞所有内容开始。只有这样，你才开始考虑允许访问你网络的特定服务。firewall 在使用 `public`（公共）区域作为默认防火墙方面表现出色，因为它阻止了几乎所有内容。像我做的那样，你应该通过实验查看是否更严格的区域配置可以为你的主机和网络提供所需的所有访问，同时让它们更加安全。

我建议你不要更改预装的区域文件。我建议你像我一样，复制最符合你需求的现有区域文件并根据需要进行修改。firewall 提供了一些基础但安全的区域文件供起始。你可能会发现其中某一个完美符合你某些部分或所有主机的需求。

我们探索了“区域”（zones）这一概念以及它们的工作原理，以及如何调整它们以更好地满足你的需求。这是在工作站背景下进行的，而不是服务器或保护整个网络的专用防火墙。

## 练习

执行以下练习以完成本章。

这是一个关于向你的防火墙添加新区域的单一练习。下列表描述了该区域的要求，以及你成功完成此任务需要遵循的一些特定指令和要求：

- 1. 复制现有的区域文件以创建一个新的。*不要*使用 **firewall-cmd --new-zone** 命令。将新区域命名为 "telnet"。
- 2. 配置新区域以阻止除 SSH 和 Telnet 外的所有外部访问。
- 3. 不需要转发（forwarding）和伪装（masquerading）。
- 4. 不要将此新区域设置为默认。你的默认区域应该是 `public` 区域。如果不是，
- 5. 显式地将新区域分配给。
- 6. 测试新区域以确保
- 7. 为了清理，
- 8. 该区域。

303

第 10 章 使用防火墙管理防火墙

# 第 11 章

# 资源

# 管理

# 使用 cgroups

## 目标

在本章中，你将学习：

- 什么是 cgroups
- 为什么使用 cgroups
- 如何使用 systemd cgroups
- 如何管理资源

## 引言

对于我们系统管理员来说，没有什么比意外耗尽资源更令人沮丧的。在多次情况下，我耗尽了可用资源。资源管理是系统管理员执行的最任务之一。

© David 2025

305

D. 系统管理员，https://doi.org/10.1007/979-8668-1328_31

第 11 章资源管理

资源管理的目的是确保所有进程都能公平地访问系统。资源管理还涉及确保内存和容量。应该防止那些故意或无意占用系统资源的用户。

我们有很多工具可以监控和管理各种资源。许多工具允许我们监控内存、I/O、存储（磁盘等）、网络、交换空间、CPU 使用。这些工具，特别是以 CPU 为中心的工具，大多数基于运行进程是控制单元的范式。它们至少提供调整 nice 值（通过优先级）或杀死进程的方法。

312

SystemV 环境中的其他资源管理工具通过 `/etc/security/limits.conf` 文件和位于 `/etc/security/limits.d` 目录的本地配置文件进行管理。可以按用户或组以简单有效的方法限制资源。可以管理的资源包括内存、每天总 CPU 时间、数据总量、优先级、nice 值、并发登录数、进程数、最大文件大小等。

## 使用 cgroups 管理进程

`systemd` 和 SystemV 的一个主要区别在于它们处理进程的方式。SystemV 将每个进程视为独立的实体。`systemd` 将资源收集到称为 cgroups 的控制组中，并作为一个整体管理系统资源。这意味着可以按应用程序进行资源管理，而不是组成应用程序的单个进程。

306

第 11 章资源管理 

cgroups 的控制单元是 slice 。Slice 是一种概念化，允许 systemd 以树状格式排列进程以便于管理。我在 Red Hat Steve Owens 的一文中发现了下面的描述，它为系统本身如何使用 cgroups 提供了一个很好的示例：

> 你可能知道或不知道，Linux 内核负责系统中所有的硬件交互。这意味着，除了让操作系统 (OS) 理解硬件的代码（驱动程序）之外，它还限制了特定程序可以向系统要求的资源。这在讨论系统内存 (RAM) 容量时最容易理解

将资源分配给计算机可能执行的所有应用程序。在最基本的形式下，Linux 系统允许无限制地运行大多数应用程序。如果所有应用程序都能良好地协同工作，这对通用计算是非常有利。但如果程序出现错误并开始消耗所有可用内存会发生什么？内核有一个名为内存溢出杀手（OOM Killer）的机制。它的工作是停止应用程序以释放内存，以便操作系统能够在不崩溃的情况下继续运行。

你可能会说这很棒，但这与 cgroups 有什么关系呢？嗯，OOM过程充当了系统崩溃前的最后防线。它虽然很有用，但由于内核可以从源头上控制哪些进程必须生存以及消耗过多的内存，因此 cgroups 是一种内置在内核中的一种机制，允许管理员对系统上的任何进程设置资源利用限制。通常情况下，cgroups 控制：

- 每个进程的 CPU 份额数（shares）。
- 每个进程的内存限制。
- 每个进程的块设备 I/O。
- 哪些网络数据包被识别为特定类型，以便另一个应用程序执行网络流量规则。

涉及方面不仅限于这些，但这些是大多数管理员关心的主要类别。

## 第 11 章 使用 Cgroups 进行资源管理

## 实验 11-1：查看 CGROUPS

让我们从一些允许我们查看 cgroups 各种类型信息的命令开始，`systemctl status <service>` 命令显示指定服务的 slice 信息，包括其所属的 slice。此示例展示了守护进程。

```
[root@studentvm1 ~] systemctl status atd.service
```

- atd.service - 延迟执行调度器
Loaded: loaded (/usr/lib/systemd/system/atd.service); 
enabled: preset enabled;
Drop-In: /usr/lib/systemd/system/service.d/10-timeout-abort.conf, 50-keep-warm.conf
Active: active (running) since Wed 2025-01-15 14:45:11 EST 3 days ago
Invocation: 0c610fa7054e62ba04d3aeb04c7ec4
Docs: man:atd(8)
Main PID: 1245 (atd)
Tasks: 1 (limit: 9472)
Memory: 336K (peak: 1020K)
CPU: 19ms
CGroup: /system.slice/atd.service

```
1245 /usr/sbin/atd -f
```
Jan 15 13:45:11 testvm1.both.org systemd[1]: Started atd.service - Deferred execution scheduler.
Jan 15 13:45:11 testvm1.both.org (atd)[1245]: atd.service: Referenced but unset environment variable

这是一个极好的示例，说明了为什么我发现 systemd 比 systemV 和旧的 init 程序更有用；这里提供的信息是 systemV 无法提供的。cgroup 条目包含了分级结构，其中 system.slice 是 systemd (PID 1)，而 atd.service 位于下一层，并且是 system.slice 的一部分。cgroup 条目的第二行还显示了进程 ID (PID) 和启动守护进程时使用的命令。

systemctl 命令允许我们看到多个 cgroup 条目。`--all` 选项显示所有 slice，包括当前未激活 slice。

```
[root@studentvm1 ~]# systemctl -t slice --all
```
