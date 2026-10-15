
```
mary:KpRu2ozmy5A:500:100:Mary Smith:/home/mary:/bin/sh
joe:0sXrvznQaksi1:501:100:John Johnson:/home/joe:/bin/sh
jane:ptNoiueYEjWk:502:100:Jane Anderson:/home/jane:/bin/sh
bob:Ju2vY7A06Kkz:503:100:Bob Reynolds:/home/bob:/bin/sh
```

列表中的每一行对应 Linux 系统上的单个用户账户。每行由由冒号（:）分隔的七个字段组成。从左到右，这些字段分别是：登录名、加密密码、用户 ID、组 ID、描述（通常是人的名字）、家目录和默认 shell。查看第一行，你可以看到它是 root 账户的，其加密密码为 `Dks6uke79QQ`。你还可以看到 root 的用户 ID 为 0，组 ID 为 0，家目录为 `/root`，且 root 的默认 shell 为 `/bin/sh`。

所有这些值对于 root 账户来说都是正常的，但看到那个加密密码应该让你脑中敲响警报。它证实了你的系统没有使用影子文件。此时，你应该立即转换密码文件，使其使用 `/etc/shadow` 来存储密码信息。你通过 `pwconconv` 命令执行此操作。只需以 root 身份登录（或使用 `su` 命令变为 root），并在提示符处输入 `pwconconv` 命令。它不会打印任何信息，但当你的 shell 返回时，你应该应该有一个 `/etc/shadow` 文件，并且你的 `/etc/passwd` 文件看起来像这样：

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:

mary:x:500:100:Mary Smith:/home/mary:/bin/sh
joe:x:501:100:Joe Johnson:/home/joe:/bin/sh
jane:x:502:100:Jane Anderson:/home/jane:/bin/sh
bob:x:503:100:Bob Reynolds:/home/bob:/bin/sh
```

加密密码数据被替换为 `x`。密码数据已移动到 `/etc/shadow`。

要检查你的系统使用的密码验证类型，请打开身份验证窗口（系统 -> 管理 -> GNOME 桌面）。该工具允许你选择使用 MD5 验证、LDAP 验证、Kerberos 5 或其他验证方法。

要处理组密码，你可以使用 `grpunconv` 命令将 `/etc/shadow` 中的密码转换为影子组密码。如果你更改了 `passwd` 或组密码并导致某些功能损坏（你无法登录账户），可以使用 `pwconconv` 和 `grpunconv` 命令来反转密码转换。

所以，现在你正在使用影子密码文件并关注良好的细节。你为保护系统迈出了伟大的一步。你现在可能已经注意到，安全不仅仅是一次性工作。它是一个持续的过程，策略与程序同样重要。继续阅读以了解更多。

# 使用 iptables 防墙保护 Linux

什么是防火墙？在非计算机世界中，防火墙是防止火蔓延的物理屏障。计算机防火墙具有类似的作用，但它们试图阻止来自互联网黑客攻击的“火灾”。在这种背景下，防火墙（也称为包过滤器）是一种在你的网络和互联网之间进行切换的物理硬件，用于调节和控制信息流。

今天最常用的防火墙类型是过滤型防火墙。过滤防火墙允许你根据 IP 地址、端口号或协议等标准定义哪些流量是被允许或阻止的规则。

## 第三部分：管理 Fedora RHEL

将外部接口分配给公用网络以获得信任。然而，你可能有一个专用的网络连接或连接到一个小型本地局域网（LAN），你希望它是受信任的。

伪装（Masquerading） — 通过将某个接口识别为伪装接口，你可以允许局域网内其他具有私有 IP 地址的计算机使用你的计算机作为通往互联网（或其他网络）的路由器。这假设你的 Fedora 系统具有另一个可以通往互联网的网接口。通过选择至少一个网络接口提供 IP 伪装，数据包转发支持将自动开启。（参见本章稍后关于伪装的描述。）

- **自定义规则（Custom Rules）** — 创建自定义规则比简单地开放端口访问要复杂一些。你可以在单独文件中创建一个 iptables 规则（格式为本章稍后描述的 iptables-save 格式），并将规则分配给过滤（filter）、NAT 或修改（mangle）iptables。点击“添加”（Add）并指定地址类型（ipv4 或 ipv6）、表类型以及包含规则的文件。点击“确定”（OK）添加规则。

在点击“应用”（Apply）保存设置之前，请考虑这将将覆盖你现有的防火墙规则。如果你对配置文件（`/etc/sysconfig/iptables`）进行过任何编辑，这些更改将被覆盖。在继续之前，请为该文件创建一个备份。

配置 iptables 以设置日志、端口转发、网络地址转换和其他功能，都可以按照后续节的描述手动完成。

## 配置 iptables 防火墙

本章中关于 iptables 的剩余部分描述了在 Linux 中操作 iptables 防火墙的一种更具手动性的。我还涵盖了如何实现“防火墙配置”窗口中不可提供的简单 iptables 特性（例如端口转发和 NAT）。

## 开启 iptables

当你安装 Fedora 或 RHEL 时，iptables 特性（也称为 netfilter）是默认的防火墙软件。

本节描述了如何开启 iptables 并针对几种不同情况设置防火墙规则。它还告诉你如何开启防火墙功能，允许你的 iptables 防火墙能够执行网络地址转换 (NAT)、IP 伪装、端口转发和透明代理。

> 注意：如果你使用了服务，Fedora 的启动脚本会在你的防火墙上“打一个洞”，因此即使它们在你的 iptables 配置中没有被显式启用也能正常工作。例如，NTP（从网络服务器设置系统时间）和 DNS 解析（让你联系 DNS 服务器来解析地址）都会在你的防火墙中打开它们所需的端口。

## 第 14 章：计算机安全问题 589

接下来的步骤描述了如何在你的 Fedora 或 RHEL 系统上运行 iptables。

- 1. 设置 iptables 脚本在引导启动时自动启动：

```
# chkconfig iptables on
```

- 2. 在启动 iptables 之前，你必须有一组已放在 `/etc/sysconfig/iptables` 文件中的可工作规则。要创建这些规则，请参考后续节中的示例。（如果没有准备好配置文件，iptables 将静默失败。）

> 提示：如果你是 iptables 的新手，可以在安装 Fedora 或 RHEL 期间通过配置防火墙，从一组可用的默认值开始。我建议将其设置为启用防火墙，并仅启用你那些你已准备好提供的服务。生成的 `/etc/sysconfig/iptables` 文件将让你看到 Fedora 或 RHEL 是如何创建防火墙的。

- 3. 如果你正在进行 IP 伪装，请开启 IP 数据包转发。允许此的一种方法是将 `/etc/sysctl.conf` 文件中的 `net.ipv4.ip_forward` 的值改为 1。以 root 用户身份使用任何文本编辑器打开该文件，并将该行修改为：

```
net.ipv4.ip_forward = 1
```

- 4. 重启网络接口使 IP 数据包转发生效。

```
# /etc/init.d/network restart
```

- 5. 文件准备到位后，启动 iptables：

```
# /etc/init.d/iptables start
```

- 6. 此时，iptables 已作为你的防火墙安装。你可以使用 `lmod` 命令检查 iptables 使用的模块是否已加载，如下：

```
# lmod |grep ^ip
ipt_REJECT 4736 1
ipt_state 1536 7
ipt_conntrack 24368 1 ipt_state
iptables_filter 2176 1
iptables 13568 3 ipt_REJECT,iptables_state,iptables_filter
```

- 7. 如果你想允许来自局域网计算机的被动 FTP 或 IRC 连接，你可能需要通过将它们添加到 `/etc/modprobe.conf` 文件来加载这些模块。基础连接跟踪模块 `ip_conntrack` 默认情况下应该已经加载了。（参见防火墙示例节之后的关于被动 FTP 和 IRC 的描述。）

如果你的 `/etc/sysconfig/iptables` 文件中有错误，你可以制作该文件的副本，然后通过运行 `system-configsecuritylevel` 并设置基础防火墙来尝试创建一个可工作的配置。然后你可以修改你的防火墙以添加你需要的功能。
