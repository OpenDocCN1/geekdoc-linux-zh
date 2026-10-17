
kali >`tail -n507 /etc/snort/snort.conf | head -n 6`
```
nested_ip inner \
whitelist $WHITE_LIST_PATH/white_list.rules, \
blacklist $BLACK_LIST_PATH/black_list.rules
############################################
# Step #6: Configure output plugins
```

在这里，我们使用 `tail` 从第 507 行开始并输出到 `head`，只返回前六行，从而给了我们 Step #6 行在前的五行以及该行本身。

## 使用 sed 进行查找和替换

`sed` 命令允许你搜索单词或模式的出现并对其执行某些操作。该命令名称是 stream editor 的缩写，在最正式的形式中，sed 的操作类似于 Windows 中的查找和替换功能。

使用 `grep` 在 `snort.conf` 文件中搜索单词 `mysql`，如下所示：

```
kali >`cat /etc/snort/snort.conf | grep mysql`
include $RULE_PATH/mysql.rules
#include $RULE_PATH/server-mysql.rules
```

你应该判断出 `grep` 命令发现了两个 `mysql` 的出现。

假设你想将每次 `mysql` 的出现替换为 `MySQL`（记住，Linux 是区分大小写的），然后将新文件保存为 `snort2.conf`。

你可以通过以下方式实现：

*(注：此处原文中存在大量重复的 OCR 错误描述，已根据要求提取核心逻辑并翻译)*

`s` 命令执行查找：你提供要搜索的词 (`mysql`) 以及要替换的词 (`MySQL`)，并用斜杠 (`/`) 分隔。`g` 命令告诉 Linux 替换是全局执行的。结果保存到名为 `snort2.conf` 的新文件中。

现在，当你对 `snort2.conf` 使用 `grep` 搜索 `mysql` 时，你会发现没有了实例。（注：原文此处 OCR 错误描述混乱，此处已按逻辑简化翻译）。

output。要找到配置文件的该部分，你只需搜索 `output`，如下所示：

```
# Snort build options:
# Options: --enable-gre --enable-mpls --enable-targetbased
  --ppm --enable-perprofiling enable-zlib --enable-active
  --response --enable-normalizer --enable-reload --enable-react
/output
```

这将立即带你到 output 第一次出现的地方并高亮显示。你可以通过输入 `n`（代表 next）来查找下一个 output。

## 第 6 步：配置输出插件

## 欲更多信息，请参考 Snort 手册，配置 Snort - 输出模块

### unified2

### 推荐大多数安装使用

# output unified2: filename merged.log, limit 128, nostamp, mpls_event_types, vlan_event_types

output unified2: filename snort.log, limit 128, nostamp, mpls_event_types, vlan_event_types

### 针对特定类型安装的额外配置

# output alert unified2: filename snort.alert, limit 128, nostamp

# output log_unified2: filename snort.log, limit 128, nostamp

```
### syslog
# output alert_syslog: LOG_AUTH LOG_ALERT\:
```

如你所见，查看单词 output 的下一个出现处将高亮显示所有搜索术语。在这种情况下，它直接跳转到了 Snort 的输出部分。真方便！

## 总结

Linux 有许多种处理文本的方法，每种方法都有自己的优缺点。我们在本章中提到了几种最实用的方法，但我建议你尝试每种方法，并培养你自己的感觉和偏好。例如，我认为 `grep` 是不可或缺的，我用得并不广泛，但你可能有不同的感受。

## 练习题

在进入第 3 章之前，请尝试完成以下练习来检验你在本章中学到的技能：

1. 目录 `/usr/share/wordlists/metasploit`。这是一个包含多个字典列表的目录，可以使用 Metasploit（最流行的渗透测试和黑客框架）对各种受密码保护的设备进行暴力破解。

2. 使用 `cat` 命令查看文件 `passwords.lst` 的内容。

3. 使用 `more` 命令显示文件 `passwords.lst`。

4. 使用 `less` 命令查看文件 `passwords.lst`。

5. 现在使用 `nl` 命令为 `passwords.lst` 中的密码加上行号。应该有 88396 个密码。

6. 使用 `tail` 命令查看 `passwords.lst` 中的最后 20 个密码。

7. 使用 `cat` 命令显示 `passwords.lst` 并通过管道（pipe）找到所有包含 123 的密码。

# 3 分析与管理网络

理解网络对于任何有志向的黑客来说都是至关重要的。在很多情况下，你将通过网络对某些东西进行攻击，一个优秀的黑客需要知道如何连接并与网络交互。例如，你可能需要在隐藏 Internet 协议（IP）地址的情况下连接到计算机，或者你可能需要将目标的域名系统（DNS）查询重定向到你的系统；这类任务相对简单，但需要一些 Linux 网络知识。本章将向你展示在网络黑客冒险中用于分析和管理网络的某些基本 Linux 工具。

## 使用 ifconfig 分析网络

`ifconfig` 命令是检查和与活动网络接口交互的最基础工具之一。你只需在终端中输入 `ifconfig` 即可查询你的活动网络连接。尝试一下吧，你应该看到类似于列表 3-1 的输出。

```
kali #`ifconfig`
eth0 Linkenc:EthernetHwaddr 00:0c:29:ba:2:0f
inet addr:192.168.181.131 Bcast:192.168.181.255 Mask:255.255.255.0
--inet-lo Linkenc:local Loopback
inet addr:127.0.0.1 Mask:255.255.0.0
--inet-wlan0 Link enc:EthernetHwaddr 00:c0:3f:ee:02
```

列表 3-1：使用 ifconfig 获取网络信息

如你所见，`ifconfig` 命令显示了关于系统活动网络的一些有用信息。输出顶部是检测到的第一个接口 `eth0`，它是 Ethernet0 的缩写（Linux 从 0 开始计数而不是 1）。这是第一个网络连接。如果有更多以太网接口，它们将以相同的格式（eth1、eth2 等）显示在输出中。

接下来列出正在使用的网络类型（Ethernet）、`Hwaddr` 和一个地址；这是标记在每件硬件设备上的全局地址——在这种情况下，即网卡（NIC），通常被称为介质访问控制（MAC）地址。

第二行包含分配给网络接口的 IP 地址信息（192.168.181.131）。`Bcast` 是 192.168.181.255，`Mask` 是 255.255.255.0。`--inet-lo` 是本地环回接口，地址为 127.0.0.1，掩码为 255.255.0.0。`--inet-wlan0` 是 `Hwaddr` 00:c0:3f:ee:02。

（此处由于原文存在大量 OCR 错误和重复内容，已根据逻辑进行了去重和翻译处理……）

## 修改你的网络掩码和广播地址

你也可以使用 `ifconfig` 命令更改网络掩码（netmask）和广播地址。例如，如果你想给同一个 eth0 接口分配掩码为 255.255.0.0、广播地址为 192.168.1.255 的 IP，你可以输入以下命令：

```
kali >`ifconfig eth0 192.168.181.115 netmask 255.255.0.0 broadcast 192.168.1.255`
kali >
```

再次，如果你的所有操作都正确，Linux 会返回一个新的命令提示符。现在再次输入 `ifconfig` 以验证每个参数是否已相应更改。

## 伪装你的 MAC 地址

你可以使用 `ifconfig` 来更改 MAC 地址（或 Hwaddr）。MAC 地址是全球唯一的，通常用作安全措施，将黑客排除在网络之外——或者用来追踪他们。将你的 MAC 地址伪装成另一个 MAC 地址几乎是轻而易举的，并且可以消除这些安全措施。因此，这是一种绕过网络访问控制非常有用的技术。

要伪装你的 MAC 地址，只需使用 `ifconfig` 命令选项关闭接口（此处为 eth0）。然后通过接口输入 `ifconfig` 命令（使用 `hw` 代表硬件，`ether` 代表以太网）以及新的伪装 MAC 地址。最后，使用选项重新启用接口使更改生效。这里是一个示例：

```
kali >`ifconfig eth0 down`
kali >`ifconfig eth0 hw ether 00:11:22:33:44:55`
kali >`ifconfig eth0 up`
```

现在，当你用 `ifconfig` 检查设置时，你应该会看到 Hwaddr 已经变为你新的伪装 MAC 地址！

## 从 DHCP 服务器分配新 IP 地址

Linux 拥有一个动态主机配置协议（DHCP）服务器，它运行着一个守护进程——在后台运行的进程——称为 `dhcpd` 或 dhcp 守护进程。DHCP 服务器为子网上的所有系统分配 IP 地址，并记录任何时候哪个 IP 地址分配给了哪台机器。这使其成为取证分析师在攻击后追踪黑客的极佳资源。因此，了解 DHCP 服务器如何工作是有用的。

通常，要从局域网连接互联网，你必须有一个由 DHCP 分配的 IP 地址。因此，在设置静态 IP 地址后，必须返回并获取一个新的 DHCP 分配的 IP 地址。为了做到这一点，你可以随时重启系统，但我将向你展示如何在不需要关闭和重启系统的情况下获取新的 DHCP 地址。

向 DHCP 请求 IP 地址，只需使用 `dhclient` 命令调用 DHCP 服务器，后跟你想分配地址的接口。不同的 Linux 发行版使用不同的 DHCP 客户端，但 Kali 是基于 Debian 构建的，后者使用 `dhclient`。因此，你可以分配一个新的地址如下：

```
kali >`dhclient eth0`
```

从指定的网络接口（此处为 eth0）发送 DHCPDISCOVER 请求。如果它收到了来自 DHCP 服务器的 DHCPOFFER（在这种情况下为 192.168.181.131），并通过 DHCPREQUEST 向 DHCP 服务器确认 IP 分配。

```
kali >`ifconfig`
eth0 Linkenc:Ethernet Hwaddr 00:0c:29:ba:82:0f
inet addr:192.168.181.131 Bcast:192.168.181.131 Mask:255.255.255.0
```

取决于 DHCP 服务器的配置，每个情况下分配的 IP 地址可能不同。

当你输入 `ifconfig` 时，你应该看到 DHCP 服务器已为你的网络接口 eth0 分配了新的 IP 地址、新的广播地址和新的网络掩码。

## 操纵域名系统

黑客可以在目标的域名系统（DNS）中找到大量的宝贵信息。DNS 是互联网的关键组件，尽管它的设计是将域名翻译为 IP 地址，但黑客可以利用它来获取有关目标的信息。

## 使用 dig 检查 DNS

DNS 是将像 `hackers-arise.com` 这样的域名转换为相应 IP 地址的工具；这样，你的系统就知道如何获取它。如果没有 DNS，我们都必须为喜爱的网站记住成千上万个 IP 地址——对于天才来说也不是一项轻松的任务。
