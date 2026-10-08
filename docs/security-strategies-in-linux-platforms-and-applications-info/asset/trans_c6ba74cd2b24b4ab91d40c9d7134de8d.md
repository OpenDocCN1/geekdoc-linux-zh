

# 第 9 章 | 网络化应用安全

- 虚拟局域网 (VLANs)—通过虚拟局域网 (VLANs) 实现的网络分区可以保持流量隔离。

- 适当的防火墙规则——语音流量需要某些优先级；防火墙规则应设置服务类型 (TOS)，以最大限度地减少交换机延迟，例如使用 `-j TOS --set Minimize-Delay`。

- 限制数据包泛洪——防火墙规则允许通过 SIP 和 RTP 协议连接，但应阻止 SYN 泛洪攻击。

## Asterisk 身份验证

如果没有身份验证，黑客可能会劫持连接两端的通话。可以通过多种方法实现 Asterisk 身份验证，包括轻量级目录访问协议 (LDAP)、远程认证拨入用户服务 (RADIUS) 和基于主机的身份验证。

## 更多 Asterisk 安全选项

额外的 Asterisk 安全选项使用了 TCP/IP 协议族中数据链路层的信息。这些安全选项包括以下内容：

- 动态主机配置协议 (DHCP) 侦探——DHCP 侦探将网络访问限制在具有已知 IP 和硬件地址的系统中。

- 动态地址解析 (ARP) 检查—这检查 IP 地址与介质访问控制 (MAC) 硬件地址之间的绑定，最大限地减少伪造硬件地址的风险。

- IP 源防护—根据 DHCP 租约文件中存储的信息检查 IP 地址与关联硬件地址的匹配情况。

- VLAN 访问控制列表 (ACL)—检查为 VLAN 创建的 ACL，以最大限地减少伪造风险。

## 限制打印机

Linux 打印机配置和管理的标准服务是通用 UNIX 打印系统 (CUPS)。它是一个多功能系统。当默认 CUPS 版本与端口 631 上的互联网协议 (IPP) 通信时，它可以用于从各种其他服务管理打印机，包括 Samba、旧的行打印机下一代系统 (LPring)、HP JetDirect 打印机等。微软操作系统支持 IPP。苹果 拥有 CUPS 软件并根据开源许可维护它。由于 Macintosh 操作系统基于 Linux 的亲戚——伯利发行版，这使得 CUPS 成为其操作系统的默认打印服务器。

CUPS 配置在 `/etc/cups/` 目录下的文件中。主要的 CUPS 配置文件是 `cups.conf`，也是本节的重点。

# 第 2 部分 | 分层安全与 Linux

## 打印机管理员

通常位于 `cupsd.conf` 文件早期的指令是 `SystemGroup`。列在此指令之后的组是经过授权在 CUPS 系统中管理打印机的组。你可以在 `/etc/group` 和 `/etc/gshadow` 配置文件中向指定的组添加用户。这些组可能会有所不同。在 Red Hat 系统上，`sys` 组的成员是默认打印管理员；在 Ubuntu 系统上，`ladmin` 组的成员是默认打印管理员。

## 共享打印机

CUPS 打印机是本地的，除非允许远程访问。远程访问从 `Listen` 指令开始，默认情况下启用通过所有 IP 地址上的端口 631 进行访问。如果你想将访问限制在系统上的多个网卡之一，可以设置如下所示的指令，其中 `192.168.0.10` 是允许接收 CUPS 通信的本地网卡的 IP 地址：

```
Listen 192.168.0.10:631
```

如果打印机通过 Samba 等其他系统共享，则必须开放该服务的端口。使用默认指令可以在本地网络显示共享打印机，这些指令几乎是自言自语的。它们激活了本地打印机的浏览，并决定优先考虑 `BrowseAllow` 还是 `BrowseDeny` 指令。这些指令中的任一或两者都可包含单个主机或网络的 IP 地址或域名。最后一行 `BrowseLocalProtocol` 指定了使用 CUPS 打印机浏览的使用情况，以及使用基于 DNS 的服务发现 (DNSSSD) 协议进行 CUPS 打印机浏览。

### 开启浏览

- BrowseOrder allow, deny
BrowseAllow all
BrowseLocalProtocols CUPS dnsssd

## 远程管理

CUPS 服务器的远程管理基于 `cupsd.conf` 文件中的后续三个 `Location` 段。这三个段的格式非常相似。它们都受 `Location` 指令限制。它们指定了主机或可能的用户访问。区别在于每个 `Location` 句。

`Location` 段支持对本地配置的打印机的访问。该段的默认版本将此类访问限制在本地系统：

```
<Location />
Order allow, deny
</Location>
```

你可以通过以下指令扩展到本地网络的访问：

```
Allow @LOCAL
```

如果需要，你可以为目标网络替换 IP 地址和网络掩码，例如 `192.168.0.0/255.255.255.0`。该网络上的系统可能也可以访问管理工具和配置文件，取决于后续的段。或者，你可以通过两个指令进一步限制访问：

```
Allow from 192.168.0.10
Deny from 192.168.0.0/255.255.255.0
```

带有 `<Location /admin>` 指令的第二段允许访问管理区域，以便查看当前的打印设置。第三段定义了在本地 CUPS 服务上添加和修改打印机的用户和系统。`AuthType` 指令指向常规的用户验证数据库。`Require user @system` 指向 `SystemGroup` 指令。因为 `@system` 指向 `SystemGroup` 指令。

```
<Location /admin>
AuthType regular
Require user @system
Order allow, deny
</Location>
```

### @system 指令

`@system` 指令指向 `cupsd.conf` 文件中定义的 `SystemGroup`。因为 `@system` 指向 `SystemGroup` 指令，它允许你指定一组用户，而不是单个账户。

### Location 段

`Location` 段支持对本地配置的打印机的访问。该段的默认版本将此类访问限制在本地系统：

```
<Location />
Order allow, deny
</Location>
```

你可以通过以下指令扩展到本地网络的访问：

```
Allow @LOCAL
```

如果需要，你可以为目标网络替换 IP 地址和网络掩码，例如 `192.168.0.0/255.255.255.0`。该网络上的系统可能也可以访问管理工具和配置文件，取决于后续的段。或者，你可以通过两个指令进一步限制访问：

```
Allow from 192.168.0.10
Deny from 192.168.0.0/255.255.255.0
```

带有 `<Location /admin>` 指令的第二段允许访问管理区域，以便查看当前的打印设置。第三段定义了在本地 CUPS 服务上添加和修改打印机的用户和系统。`AuthType` 指令指向常规的用户验证数据库。`Require user @system` 指向 `SystemGroup` 指令。

```
<Location /admin>
AuthType regular
Require user @system
Order allow, deny
</Location>
```

### 管理工具

`@system` 指令指向 `cupsd.conf` 文件中定义的 `SystemGroup`。因为 `@system` 指向 `SystemGroup` 指令，它允许你指定一组用户，而不是单个账户。

### Location 段

`Location` 段支持对本地配置的打印机的访问。该段的默认版本将此类访问限制在本地系统：

```
<Location />
Order allow, deny
</Location>
```

你可以通过以下指令扩展到本地网络的访问：

```
Allow @LOCAL
```

如果需要，你可以为目标网络替换 IP 地址和网络掩码，例如 `192.168.0.0/255.255.255.0`。该网络上的系统可能也可以访问管理工具和配置文件，取决于后续的段。或者，你可以通过两个指令进一步限制访问：

```
Allow from 192.168.0.10
Deny from 192.168.0.0/255.255.255.0
```

带有 `<Location /admin>` 指令的第二段允许访问管理区域，以便查看当前的打印设置。第三段定义了在本地 CUPS 服务上添加和修改打印机的用户和系统。`AuthType` 指令指向常规的用户验证数据库。`Require user @system` 指向 `SystemGroup` 指令。

```
<Location /admin>
AuthType regular
Require user @system
Order allow, deny
</Location>
```

