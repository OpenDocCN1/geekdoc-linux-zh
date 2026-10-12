
用户账户控制 (`UAC`) 不是防火墙技术，但与安全密切相关。Windows Vista 首次引入了它，并在 Windows 7 中得到了扩展，在 Windows 10 中仍然存在。`UAC` 是一项安全功能，当任务需要管理员权限时提示用户输入管理员凭据。`UAC` 首次于 Windows Vista，但在 Windows Server 2008 和 Windows Server 2012 之后，它变得更加精细可调。此功能允许你决定希望用户账户控制如何响应。这不是一个简单的开启或关闭的问题，而是有不同程度的。

## Linux 防火墙

Linux 操作系统内置了防火墙功能。多年来，这一直是 Linux 操作系统的一部分，技术上偶尔会有改进。

### iptables

第一个广泛使用的 Linux 防火墙是 `iptchains`。它本质上是一系列过滤流量的规则链，因此命名。它首次在 Linux 内核 2.2 版本引入，取代了主要的 `ipfwadm`（后者并未广泛使用）。更现代的 `iptables` 取代了 `iptchains`，是 Linux 的主要防火墙。`iptables` 服务首次引入 Linux 内核 2.4。

在大多数 Linux 系统，`iptables` 安装在 `/usr/sbin/iptables`。然而，如果你的特定 Linux 安装中没有它，你可以稍后添加，如图 4-2 所示。

图 4-2 查找 `iptables`

### Linux 防火墙

`iptables` 防火墙由三种不同的对象组成：表（`tables`）、链（`chains`）和规则（`rules`）。基本上，表包含了规则链。换句话说，`iptables` 是 `ipchains` 概念的扩展。每条链都有一系列规则，定义了如何过滤数据包。实际上有有三个表，每个表都包含一些标准规则链。当然，你也可以添加自己的规则。这三个表及其标准链如下：

- 数据包过滤（Packet filtering）：该表是防火墙的核心部分。它是一个包过滤防火墙，包含三个标准链：`INPUT`、`OUTPUT` 和 `FORWARD`。`INPUT` 链处理传入的数据包，`OUTPUT` 链处理从机器发出的流量。如果防火墙系统同时充当路由器，则只有 `FORWARD` 链适用于路由包。

- 网络地址转换（Network address translation）：该表用于对发起新连接的出站流量进行网络地址转换。只有当你的机器作为网关或代理服务器时才会使用此表。

- 数据包篡改（Packet alteration）：该表仅用于特殊的数据包修改。它通常被称为 `mangle` 表，因为它会修改或篡改数据包。它包含两个标准链。许多标准防火墙可能甚至不需要此表。

#### Iptables 配置

`iptables` 需要一些配置。你可以通过 GUI（KDE、GNOME 等）进行配置，但 shell 命令在许多发行版中是通用的。让我们来看一些常见的基础配置问题。

要让 `iptables` 作为一个基础包过滤防火墙运行，你需要以下命令：

- `iptables -F`

- `iptables -N block`

- `iptables -A block -m state --state ESTABLISHED,RELATED -j ACCEPT`

显然，这是最基础且核心的 `iptables` 配置。然而，还有其他配置。

要列出你当前使用的 `iptables` 规则：

```
iptables -L
```

要允许特定端口的通信（在此例中为 SSH 端口 22），你使用：

```
iptables -A INPUT -p tcp --dport ssh -j ACCEPT
```

或者你可能需要允许所有传入的 Web/HTTP 流量：

```
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

记录被丢弃的数据包也是好主意。以下命令可以实现这一点：

```
iptables -I INPUT 5 -m limit --limit 5/min -j LOG --log-prefix "iptables denied: "
--log-level 7
```

如你所示，可以传递给 `iptables` 命令的标志。以下是最常用的标志列表及其功能。

- `A`: 将此规则追加到规则链中。

- `L`: 列出当前的过滤规则。

- `p`: 使用的连接协议。

- `dport`: 此规则所需的目的端口。可以给出单个端口，也可以以 `开始:结束` 的形式给出一个范围。

- `limit`: 最大匹配率，格式为数字后跟 `/second`、`/minute` 或 `day`，取决于你希望规则匹配的频率。如果未使用此选项但使用了 `-m limit`，则默认值是 "3/hour"。

- `ctstate`: 定义规则匹配的状态列表。

- `log-prefix`: 记录日志时，将此文本放在日志消息之前。使用双引号括起来要使用的文本。

- `log-level`: 使用指定的 syslog 级别记录日志。

- `i`: 仅当数据包来自指定接口时才匹配。

- `v`: 详细输出。

- `s`: `--source`: 地址[掩码] 源规范。

- `d`: `--destination`: 地址[掩码] 目的规范。

- `o`: `--out-interface`: 输出名称[+] 网络接口名称 ([+) 用于通配符。

这不是一个完整的列表，只是一些常用的标志。但它应该足够让你完成 `iptables` 的基本配置并运行。

## 诺克顿防火墙 (Symantec Norton Firewall)

Norton AntiVirus 的制作商还销售一种个人单机防火墙。它是 Norton 安全套件的一部分。

Norton 防火墙还包含一些额外功能，如弹出广告拦截和隐私保护。它通过防止信息在用户不知情的情况下通过浏览器传输来完成最后一个任务。该防火墙为你提供了一个相对易于使用的界面，类似于 Windows 资源管理器，同时也允许你设置浏览器安全。它还有一个功能，允许你连接到 Norton 网站并让该网站扫描你的系统漏洞。该功能如图 4-3 所示。

![](img/b9022ea8d49ef539d37d0ec09f73f71c_128_0.png)

图 4-3 Norton 漏洞扫描

需要注意的是，所有这些任务可以在没有 Norton 的情况下完成。你可以设置浏览器安全设置，并扫描你的机器的漏洞（使用从互联网下载的免费工具，其中一些将在第 12 章“评估系统安全性”中讨论）。然而，通过 Norton，你可以通过简单得多的界面完成所有操作。这对于新手用户特别有吸引力。还应该强调的是，与高级防火墙不同，Norton 防火墙也可以阻止出站流量。

从 2016 版本的 Norton 防火墙开始，它增加了一些类似于入侵检测系统的额外功能。它会通知你任何端口扫描、可疑流量或异常连接尝试。它也像任何防火墙一样支持规则。你可以在此处了解更多关于 Norton 防火墙的信息：http://ftp.symantec.com/public/english_us_canada/products/norton_internet_security/2015/manuals/IShelp.pdf。

Norton 防火墙优优总结如下。

### 优点

- Norton 防火墙可以与 Norton AntiVirus 软件一起购买。

- Norton 防火墙易于使用和设置。

- Norton 防火墙具有若干额外功能，例如扫描你的系统漏洞的能力。

- Norton 防火墙具有其他非常实用的 IDS（入侵检测系统）功能。

### 缺点

- Norton 防火墙每份花费约 40 美。

- Norton 防火墙的许多功能可以通过单独的免费工具完成。

## McAfee 个人防火墙 (McAfee Personal Firewall)

McAfee 和 Norton 是广泛使用的防病毒软件供应商。McAfee 防火墙现在是 McAfee Protection 套件的一部分，有许多版本，从个人版到企业版。个人版易于使用。图 4-4 显示了 McAfee 防火墙的初始屏幕，图 4-5 显示了使用 McAfee 进行过滤。

![](img/b9022ea8d49ef539d37d0ec09f73f71c_129_0.png)

**图 4-4** McAfee 防火墙界面

![](img/b9022ea8d49ef539d37d0ec09f73f71c_129_1.png)

**图 4-5** 使用 McAfee 进行过滤

### Linux 防火墙 109

McAfee 提供了一些在大多数个人防火墙中没有的有趣功能：

- **跟踪（Tracking）**：McAfee 个人防火墙是一种可以在地图上显示攻击路径的工具。它的原理与 `traceroute` 命令类似，但是对传入的数据包执行 `traceroute` 命令并将路由显示在地图上。

- **连接 HackerWatch.org**：McAfee 个人防火墙连接到 HackerWatch.org，这是一个防攻击网站，允许你获取最新威胁的提示和新闻。
