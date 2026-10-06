
网络脚本会自动激活 IPsec 连接，并在必要时创建网络路由以通过 IPsec 路由器发送数据包。

## 2.7.7.2 手动 IPsec 网络到网络配置

假设 LAN A (`lana.example.com`) 和 LAN B (`lanb.example.com`) 希望通过 IPsec 隧道相互连接。LAN A 的网络地址位于 `192.168.1.0/24` 范围，LAN B 使用 `192.168.2.0/24` 范围。网关 IP 地址 LAN A 为 `192.168.1.254`，LAN B 为 `192.168.2.254`。IPsec 路由器与每个 LAN 网关分离，使用两个网络设备：`eth0` 分配一个从外部访问的静态 IP 地址以访问 Internet，而 `eth1` 作为路由点，用于处理并传输从一个网络到远程网络节点的 LAN 数据包。

每个网络之间的 IPsec 连接使用值为 `r3dh4tlinux` 的预共享密钥，A 和 B 的管理员同意 `racoon` 在每个 IPsec 路由器之间自动生成并共享身份密钥。LAN A 的管理员决定将 IPsec 连接命名为 `ipsec0`，而 LAN B 的管理员将 IPsec 连接命名为 `ipsec1`。

示例显示了用于 LAN A 网络到网络 IPsec 连接的 `ifcfg` 文件内容。示例中用于识别连接的唯一名称是 `ipsec0`，因此生成的文件为 `/etc/sysconfig/network-scripts/ifcfg-ipsec0`。

```
TYPE=IPSEC

ONBOOT=yes

KE_METHOD=PSK

SRCGW=192.168.1.254

DSTGW=192.168.2.254

SRCNET=192.168.1.0/24

DSTNET=192.168.2.0/24

DST=X.X.X
```

以下列表描述了该文件的内容：

- `TYPE=IPSEC`
  指定连接类型。

- `ONBOOT=yes`
  指定连接在启动时启动。

- `IKE_METHOD=PSK`
  指定连接使用预共享密钥方法进行身份验证。

- `SRCGW=192.168.1.254`
  源网关的 IP 地址。对于 LAN A，这是 LAN A 网关；对于 LAN B，这是 B 网关。

- `DSTGW=192.168.2.254`
  目标网关的 IP 地址。对于 LAN A，这是 LAN B 网关；对于 LAN B，这是 LAN A 网关。

- `SRCNET=192.168.1.0/24`
  指定 IPsec 连接的源网络，在示例中，这是 LAN A 的网络范围。

- `DSTNET=192.168.2.0/24`
  指定 IPsec 连接的目标网络，在示例中，这是 LAN B 的网络范围。

- `DST=X.X.X.X`
  LAN B 的外部可用 IP 地址。

示例显示了预共享密钥文件 `/etc/sysconfig/network-scripts/keys-ipsec`（其中 X LAN A 为 0，LAN B 为 1）的内容，两个网络使用该文件进行身份验证。该文件的内容应当相同，且只有 root 用户才能读取或写入此文件。

### IPsec 网络到网络配置

`IKE_PSK=r3dh4tl1nux`

> 重要提示
> 要更改 `keys-ipsecX` 文件使得只有 root 用户可以读取或编辑该文件，请在创建文件后使用以下命令：

```bash
chmod 600 /etc/sysconfig/network-scripts/keys-ipsec1
```

如需更改身份密钥，请编辑两个 IPsec 路由器上的 `keys-ipsecX`。两个密钥必须相同以确保正常连接。

以下示例是用于 IPsec 连接的 `/etc/racoon/racoon.conf` 文件内容。注意，文件底部的 `include` 行是自动生成的，仅在 IPsec 隧道激活时才会显示。

```
# Racoon 守护进程配置文件。

# 请参考 'main raccoon.conf' 获取格式和条目的描述。

path include "/etc/racoon/"

path pre_shared_key "/etc/racoon/ps.txt"

path certificate "/etc/racoon/certs"

sainfo anonymous

{

pfs_group 2;

lifetime time 1 hour;

encryption_algorithm 3des, blowfish 448, rijndael;

authentication_algorithm hmac_sha1, hmac_md5;

compression_algorithm deflate;

}

include "/etc/racoon/X.X"
```
（注：配置文件的 OCR 文本严重乱码；我根据标准 racoon 配置和上下文进行了重构。）

# 防火墙

保护关键企业信息的 PC 到数据中心解决方案。防火墙可以是独立的硬件解决方案，例如 Cisco、Nokia 和 Sonicwall 的防火墙设备。Checkpoint、McAfee 和 Symantec 等供应商也为家庭和商业市场开发了专有的软件防火墙解决方案。

除了硬件防火墙和软件防火墙的区别外，防火墙的功能方式也存在，，了不同的解决方案。表 2.2 “防火墙类型”详细介绍了三种常见的防火墙类型及其工作原理：

| 方法 | 描述 | 优点 | 缺点 |
| --- | --- | --- | --- |
| NAT | 网络地址转换 (NAT) 将 IP 子网置于一个或一小组公共地址池之后，将所有请求伪装成单个源而非多个源。Linux 内核通过 Netfilter 内核内置了此功能。 | - 可以对局域网上的机器进行透明化配置 - 保护一个或多个 IP 地址后的许多机器和服务简化了管理工作 -可以通过打开和关闭 NAT 防火墙/网关上的端口来限制用户对局域网的访问 | - 一旦用户连接到防火墙的服务出口，就无法防止恶意活动 |
| 数据包过滤 | 数据包过滤读取通过局域网的每个数据包。它可以通过报头信息读取并处理数据包，并根据防火墙管理员实施的一组可编程规则过滤数据包。Linux 内核通过 Netfilter 内核内置了数据包过滤功能 | - 可以通过 iptables 前端进行自定义 - 不需要在客户端进行自定义，因为所有网络活动都在路由器层过滤而非应用层过滤 - 由于数据包不通过代理传输，由于从客户端到远程主机的直接连接，网络性能更快 | - 无法像代理防火墙那样过滤数据包内容 - 在协议层处理数据包，无法在应用层过滤数据包 - 复杂的网络架构可能使建立防火墙规则变得困难，特别是当与 IP 映射或本地子网及 DNS 网络结合时 |
| 代理 | 代理防火墙将所有协议或来自局域网客户端的请求发送到代理，由代理代表客户端向 Internet 发起请求。代理机器在恶意用户和内部网络客户端之间充当缓冲区。 | - 可以控制哪些应用程序和协议在局域网外运行 - 部分服务器在本地缓存频繁访问的数据，而不是使用 Internet 请求。这有助于减少带宽消耗 - 代理服务器可以进行密密记录和监控，允许对通过单个源传输的网络资源利用进行更严格的控制，而不是直接从客户端到远程服务 | - 代理是特定特定的（HTTP、Telnet 等）或受协议限制的（大多数代理仅适用于 TCP 连接的服务） - 应用服务无法在代理后运行，因此您的应用程序服务器必须使用单独的网络安全形式 - 代理可能会成为网络瓶颈，因为所有请求和传输都是 |

## 第 2 章 保护您的网络

## 2.8.1. Netfilter 和 IPTables

Linux 内核具有一个强大的网络子系统 *Netfilter*。Netfilter 子系统提供有状态或无状态的数据包过滤，以及 NAT 和 IP 伪装服务。Netfilter 还具有对 IP 头部信息进行*修改*的能力，用于高级路由和连接状态管理。Netfilter 使用 *iptables* 工具进行控制。

### 2.8.1.1. IPTables 概述

Netfilter 的强大和灵活性是通过 **iptables** 管理工具实现的，这是一个命令行工具，其语法与它的前身 **ipchains** 相似。

语法相似并不意味着实现相似，**ipchains** 需要复杂的规则集来过滤源路径；过滤目的地；以及过滤源和目的端口。

相比之下，**iptables** 使用 Netfilter 子系统来增强网络连接、检查和处理。**iptables** 具有高级日志、路由前和路由后操作、网络地址转换和转发总计，全部在一个命令行界面中实现。

本节提供了 **iptables** 的概述。更多详细信息，请参阅 [第 2.9 节，IPTables]。

## 2.8.2. 基础防火墙配置

就像建筑试图防止火灾蔓一样，计算机防火墙试图防止恶意软件扩散到您的计算机。它还有助于防止未经的用户访问您的计算机。

在默认的 Fedora 安装中，您的计算机或网络与任何不可信的网络（即 Internet）之间存在一个防火墙。它决定了您的远程用户可以访问哪些服务。配置适当的防火墙可以极大提高您系统的安全性。建议为任何连接 Internet 的 Fedora 配置防火墙。

## 2.8.2.1. 防火墙配置工具

在 Fedora 安装的**防火墙配置**屏幕期间，您被赋予启用基本防火墙以及允许特定设备、入站服务和端口的选项。

安装后，您可以使用**防火墙配置工具**更改您的偏好。

启动此应用程序，请使用以下命令：

```
[root@myServer ~] # system-config-firewall
```

## 防火墙配置

在这里您可以定义哪些服务是受信任的。受信任的服务可以从所有主机和网络访问。

| 服务 | 端口/协议 |
| --- | --- |
| WWW (HTTP) | 80/tcp |
| SSH | 22/tcp |
| WWW (HTTPS) | 443/tcp |
| Samba Client | 137/udp, 138/udp |
| Samba | 137/udp, 138/udp, 139/tcp, 445/tcp |
| RADIUS | 1812/udp, 1813/udp |
| POP3-over SSL | 995/tcp |
| OpenVPN | 2094/udp |
| NFS4 | 2049/tcp, 2049/udp |
| 网络打印服务器 (IPP) | 631/tcp, 631/udp |
| 网络打印客户端 (IPP) | 631/udp |
| 多播 DNS (mDNS) | 5353/udp |

防火墙已启用。

**图 15. 防火墙配置工具**

> 注意
> 防火墙配置工具仅配置基本防火墙。如果需要更复杂的规则，请参阅第 2.9 节“IPTables”。

## 2.8.2.2. 启用和禁用防火墙

- 禁用防火墙，除非您在受信网络（非 Internet）上运行或需要使用 iptables 配置自定义规则。
- 启用 —— 系统将拒绝请求，例如 DNS 响应。

> 警告
> 防火墙配置和任何自定义规则存储在 `/etc/sysconfig/iptables`。如果您选择禁用。

## 2.8.2.3. 受信任的服务

在**信任服务**列表中启用选项允许指定的服务通过防火墙。

### WWW (HTTP)

HTTP 协议被 Apache（以及其他 Web 服务器）用于提供网页。如果您计划让您的 Web 服务器公开，请勾选此复框。对于本地查看网页或开发网页，不需要此选项。此服务需要安装 `httpd` 包。

### WWW (HTTPS)

启用 HTTPS 将为 HTTPS（HTTP 的 SSL 版本）打开端口。如果需要此服务，请勾选 WWW (HTTPS) 复框。

### FTP

FTP 协议用于在机器之间传输文件。如果您计划让您的 FTP 服务器公开，请勾选此复框。此服务需要安装 `vsftpd` 包。

### SSH

Secure Shell (SSH) 是一个用于登录远程机器并执行命令的套件。要允许通过 ssh 访问机器，请勾选此复框。此服务需要安装 `openssh-server` 包。

### Telnet

Telnet 是用于登录远程机器的协议。Telnet 通信未加密，无法防止网络嗅探。不建议允许入站 Telnet 。要允许通过 telnet 访问机器，请勾选此复框。此服务需要安装 `telnet-server` 包。

SMTP 协议允许远程主机连接到您的机器以投递邮件。如果您使用 POP3 或 IMAP 从 ISP 服务器收集邮件，或者使用 fetchmail 等工具，则不需要启用此服务。要允许向您的远程机器投递邮件，请勾选此复框。注意，配置不当的 SMTP 服务器允许远程访问您的服务器来发送垃圾邮件。

### NFS4

网络文件系统 (NFS) 是一种常用的 *NIX 系统文件共享协议。该协议的第 4 版本比之前的版本更安全。如果您想与其他网络用户共享系统上的文件或目录，请勾选此复框。

### Samba

Samba 是微软专有 SMB 网络协议的实现。如果您需要与 Microsoft Windows 机器共享文件、目录和本地连接的打印机，请勾选此复框。

## 2.8.2.4. 其他端口

防火墙配置工具包含一个“其他端口”部分，用于指定被 iptables 信任的自定义 IP 端口。例如，允许 IRC 和网络打印协议 (IPP) 通过防火墙，请将它们添加到以下“其他端口”部分：

```
194:tcp, 631:tcp
```

## 2.8.2.5. 保存设置

点击确定保存更改并启用或禁用防火墙。如果选择了“启用防火墙 (Enable firewall)”，这些选项将被翻译为 iptables 命令并写入 `/etc/sysconfig/iptables` 文件。同时也会启动 iptables 服务，以便防火墙在保存选项后立即激活。如果选择了“禁用防火墙 (Disabled firewall)”，则会删除 `/etc/sysconfig/iptables` 文件并立即停止 iptables 服务。

所选选项还被写入 `/etc/sysconfig/system-config-securitylevel` 文件，以便在下次启动应用程序时可以恢复设置。请勿手动编辑此文件。

尽管防火墙会立即激活，但 iptables 服务并未配置为在系统启动时自动启动。更多信息请参阅第 2.8.2.6 节“激活 IPTables 服务”。

## 2.8.2.6. 激活 IPTables 服务

只有在 iptables 服务运行时，规则才会生效。要手动启动服务，请使用以下命令：

```
[root@myServer] # service iptables restart
```

要确保 iptables 在系统启动时启动，请使用以下命令：

```
[root@myServer] # chkconfig --level 345 iptables on
```

Fedora 中不包含 iptchains。但是，如果安装了 iptchains（例如，执行了升级且系统之前有 iptables），则不应同时激活 iptchains 和 iptables 服务。要禁用 iptchains 服务并配置为不在启动时启动，请使用以下两个命令：

```
[root@myServer] # service iptchains stop
[root@myServer] # chkconfig --level 345 iptchains off
```

## 2.8.3. 使用 IPTables

使用 iptables 的第一步是启动 iptables 服务。使用以下命令启动 iptables 服务：

```
[root@myServer] # service iptables restart
```

## 第 2 章 保护网络安全

> 注意
> 如果你打算仅使用其他服务，可以关闭 iptables 服务。如果你禁用了 iptables 服务，请记住也停用 IPv6 网络。永远不要在没有匹配的防火墙的情况下让网络设备处于激活状态。

要强制 iptables 在系统启动时默认激活，请使用以下命令：

```
[root@myServer ~] # hkconfig --level 34 iptables on
```

这将强制 iptables 在系统以运行级别 3、4 或 5 启动时运行。

## 2.8.3.1. IPTables 命令语法

以下 iptables 命令说明了基本的命令语法：

```
[root@myServer ~] # iptables -A <chain> -j <target>
```

--

`-A` 选项指定要附加到 `<chain>` 的规则。每个链（chain）都由一条或多条规则组成，因此被称为规则集（ruleset）。

三个内置链是 INPUT、OUTPUT 和 FORWARD。这些链是永久的，无法删除。链指定了数据包被处理的时间点。

`-j <target>` 选项指定规则的目标（target）；即如果数据包匹配规则，执行的操作。内置目标的示例有 ACCEPT、DROP 和 REJECT。

请参阅 iptables 帮助页面（man page）以获取可用链、选项和目标。

## 2.8.3.2. 基本防火墙策略

建立基础防火墙策略为构建更详细的用户自定义规则奠定了基础。

每个 iptables 链由一个默认策略和零或多个规则组成，这些规则与默认策略共同工作，定义防火墙的整体规则。具有安全意识的管理员通常实施 DROP 默认策略，并根据情况仅允许特定的数据包。例如，以下策略阻止网络网关上所有的入站和出站流量：

```
[root@myServer ~] # iptables -P INPUT DROP
[root@myServer ~] # iptables -P OUTPUT DROP
```

还建议拒绝转发包——即从防火墙路由到目的节点的网络流量——以限制内部客户端意外暴露在网上。要实现这一点，请使用以下规则：

```
[root@myServer ~] # iptables -P FORWARD DROP
```
