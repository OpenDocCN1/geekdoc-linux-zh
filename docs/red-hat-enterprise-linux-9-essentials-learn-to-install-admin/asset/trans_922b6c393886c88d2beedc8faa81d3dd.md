
## RHEL 9 网络管理

```
# nmcli con mod static_ip connection.permissions user:root,john,caitlyn
```

一旦 NetworkManager 重新加载了连接配置文件，*static_ip* 连接只有在至少有一位指定用户登录到系统上的活动会话时才会激活并可供其他用户访问。一旦这些用户中的最后一位注销，连接将关闭并保持非活动状态，直到其中一位用户重新登录。

此外，只有拥有权限的用户才能更改连接状态或配置。

### 12.7 摘要

NetworkManager 服务负责 RHEL 9 上的网络管理。NetworkManager 将网络视为由网络接口设备和连接组成。网络设备可以是物理以太网或 WiFi 设备，也可以是虚拟机客户机使用的虚拟设备。连接表示设备所连接的网络，并由连接配置文件进行配置。配置文件将在其他设置中定义连接是否具有静态或动态 IP 地址、网络使用的任何网关的 IP 地址，以及系统每次启动时是否应自动建立连接。

NetworkManager 可使用多种工具进行管理，包括 *nmcli* 和 *nmtui* 命令行工具、*nm-connection-editor* 图形工具以及 Cockpit Web 界面的网络设置部分。通常，nmcli 命令行工具提供最多的功能和灵活性。

## 13. RHEL 9 防火墙基础

防火墙是保护单个计算机系统或计算机网络免受外部攻击（通常来自互联网连接）的重要组成部分。任何直接连接到互联网连接的计算机 ideally 都应运行防火墙以防止恶意活动。同样，任何内部网络必须在其与外部互联网连接之间设置某种形式的防火墙。

RHEL 9 内置了强大的防火墙技术 *iptables*。有关配置 iptables 的书籍可以而且确实已经写过。如果您想了解 iptables，我们推荐以下内容：

https://www.linuxtopia.org/Linux_Firewall_iptables/index.html

本章将介绍防火墙、TCP/IP 端口和服务的一些基本概念。RHEL 9 上的防火墙配置将在题为“*RHEL 9 使用 firewalld 进行防火墙配置*”的章节中介绍。

### 13.1 理解端口和服务

目前使用的主要网络通信协议是 TCP/IP。它是互联网使用的协议，因此取代了用于局域网（LAN）的以前流行的协议。

TCP/IP 共定义了 65,535 个端口，其中 1023 个被认为是 *众所周知的端口*。必须了解这些并不是连接网络电缆的物理端口，而是每个网络连接上的虚拟端口，可供应用程序和服务通过 TCP/IP 网络连接进行通信。实际上，流行网络客户端和服务使用的端口数量只是众所周知端口组中更小的子集。

操作系统可以提供多种不同的 TCP/IP 服务。本章末尾的表格提供了此类服务的全面列表。然而，这些服务包括用于运行安全 Web 服务器的 HTTPS、用于允许文件传输的 FTP、用于提供安全远程登录访问和文件传输的 SSH，以及用于传输电子邮件消息的 SMTP。每个服务依次分配给标准的 TCP/IP 端口。例如，HTTPS 分配给端口 443，而 SSH 通信发生在端口 22。

### 13.2 保护端口和服务

保护服务器很大一部分工作涉及定义角色，并基于角色定义应启用哪些服务和端口。例如，仅充当 Web 服务器的服务器应仅运行 HTTPS 服务（此外可能还有 SSH 用于远程管理访问）。所有其他服务都应被禁用，并且理想情况下应从操作系统中完全删除（从而使入侵者更难重新启用该服务）。

保护系统涉及从操作系统中删除任何不必要的服务，并确保使用防火墙阻止与非必要服务关联的端口。定义哪些端口可访问以及在何种情况下可访问的规则是使用 iptables 确定的。

许多操作系统默认安装并激活了多个服务。在安装新操作系统之前，必须仔细规划安装。此规划涉及确定不需要的服务以及哪些服务默认已安装并已启用。部署新的操作系统安装绝不应仓促进行。系统上可用的服务和开放端口越少，攻击者的攻击面和机会就越小。

### 13.3 RHEL 9 服务和 iptables 规则

默认情况下，刚安装的 RHEL 9 系统没有定义 iptables 规则来限制对端口的访问。可以在终端窗口中执行以下命令以查看当前的 iptables 设置：

```
# iptables -L
Chain INPUT (policy ACCEPT)
target  prot opt source          destination

Chain FORWARD (policy ACCEPT)
target  prot opt source          destination

Chain OUTPUT (policy ACCEPT)
target  prot opt source          destination
```

如上输出所示，目前尚未定义任何规则。虽然这可能看起来是不安全的配置，但必须记住，刚安装的 RHEL 9 系统默认也运行的服务很少，使得端口对潜在攻击者毫无用处。例如，由于没有 Web 服务器服务默认安装或运行，因此无法访问刚安装的 RHEL 9 系统上的 Web 服务器。一旦系统开始激活服务，建立防火墙策略并定义 iptables 规则将变得很重要。

有多种方法可用于定义 iptables 规则，包括使用命令行工具和配置文件。例如，要阻止 IP 地址 192.168.2.76 访问端口 25（用于 SMTP 邮件传输协议），可以在终端窗口中发出以下命令：

```
# iptables -A INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP
```

如果我们现在检查当前规则，我们会看到该规则目前已列出：

```
# iptables -L
Chain INPUT (policy ACCEPT)
target  prot opt source          destination
DROP    tcp -- 192.168.2.76    anywhere    tcp dpt:smtp

Chain FORWARD (policy ACCEPT)
target  prot opt source    destination

Chain OUTPUT (policy ACCEPT)
target  prot opt source    destination
```

随后可以按如下方式删除该规则：

```
# iptables -D INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP
```

鉴于 iptables 的复杂性，创建了多个用户友好的配置工具来简化规则创建过程。其中一种工具是 firewall-cmd 命令行工具，将在“RHEL 9 Firewall Configuration with firewalld”章节中介绍。

### 13.4 众所周知的端口和服务

在继续介绍更复杂的防火墙规则之前，先花时间概述 RHEL 9 系统可以提供的一些关键服务以及相应的端口号是值得的：

| 端口 | 分配 | 描述 |
|------|------------|-------------|
| 20 | FTP | **文件传输协议（数据）** - 文件传输协议提供了一种在网络连接的计算机系统之间传输特定文件的机制。传输通常使用 ftp 客户端执行。大多数现代 Web 浏览器也可以浏览和从远程 FTP 服务器下载文件。FTP 使用 TCP（而不是 UDP）传输文件，这被认为是一种高度可靠的传输机制。FTP 不加密数据，也不被视为安全的 文件传输协议。强烈建议改用安全复制协议（SCP）和安全文件传输协议（SFTP）。 |
| 21 | FTP | **文件传输（控制）** - 传统上，FTP 分配了两个端口（端口 20 和端口 21）。端口 20 最初被认为是数据传输端口，而端口 21 被分配用于通信控制信息。然而，在现代实现中，端口 20 很少使用，所有通信都在端口 21 上进行。 |

