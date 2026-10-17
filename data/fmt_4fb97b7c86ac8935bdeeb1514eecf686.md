
通过 `inetd(8)`，几乎任何东西都可以成为网络服务。

## DHCP

动态主机配置协议 (DHCP) 是向计算机分发 IP 地址的标准方法。虽然 DHCP 服务没有内置集成到 FreeBSD 中，但在实现如无盘工作站和 PXE 安装等服务时通常需要它们。FreeBSD Ports 集合包含了 `dhcpd`，它由为我们带来 BIND（见第 14 章）的团队提供：`/usr/ports/net/isc-dhcpd-server`。按照第 11 章的说明安装该端口。初始选项突出了 `dhcpd` 的功能和能力，例如 LDAP 集成。安装的工具包括 `dhcpd(8)`、配置文件 `/local/etc/dhcpd.conf` 以及大量的手册页。

## DHCP

动态 DHCP 是向计算机分发 IP 地址的标准方法。虽然 DHCP 服务没有内置集成到 FreeBSD 中，但在实现如无盘工作站和 PXE 安装等服务时通常需要它们。FreeBSD Ports 集合包含了 `dhcpd`，它由为我们带来 BIND（见第 14 章）的团队提供：`/usr/ports/net/isc-dhcpd-server`。按照第 11 章的说明安装该端口。初始选项突出了 `dhcpd` 的功能和能力，例如 LDAP 集成。安装的工具包括 `dhcpd(8)`、配置文件 `/local/etc/dhcpd.conf` 以及大量的手册页。

# 网络协议

`qotd` 服务要求你连接到网络端口并获取返回内容，因此它需要在 TCP 上运行。请记住，UDP 是无连接的——不需要应答。我们必须在 `inetd` 配置中指定 `tcp`，这意味着我们必须在第四字段中指定 `wait`。

## 用户

最佳实践是创建一个非特权用户来运行 `qotd` 服务，效仿于 `pop` 或 `proxy` 等用户。在本文示例中，我们将仅使用通用的非特权用户 `nobody`，但如果你在生产环境中实现它，你会想要创建一个非特权用户 `qotd`。

# 路径

在 `/usr/games/fortune` 找到 `fortune`。

# 运行命令

`fortune(6)` 不需要任何命令行参数，但如果你喜欢，也可以添加它们。墨菲法则的信奉者可以使用 `fortune merry`，而《星际迷航》粉丝可以使用 `fortune startrek` 获取引言。（后者仅包含真正的《星际迷航》，不包含任何模仿的续作。）我使用 `fortune -a`，因为任何连接到我服务器的人都应该得到他们想要的。

# 示例 inetd.conf 配置

将这一切整合在一起，`/etc/inetd.conf` 的条目如下：

| qotd | stream | tcp | nowait | nobody | /usr/games/fortune | fortune |

你可能认为这个示例很微不足道，但通过 `inetd(8)` 提供其他服务并没有困难。

# 启动 inetd(8)

首先，通过向 `/etc/rc.conf` 添加以下条目在启动时启用 `inetd(8)`：

```
inetd_enable=YES
```

设置此项后，通过 `/etc/rc.d/inetd start` 手动启动 `inetd`。现在 `inetd` 正在运行，telnet 到端口 17 并测试我们的新服务：

```
telnet localhost 17
```

- 尝试连接 127.0.0.1...
- 已连接到 localhost。
- 转义字符是 '^]'

- 当每十二分钟就会被十二只跳舞并唱着卫生纸的兔子干扰时，很难制作出一部既尖锐又深入的电视纪录片。
-- Rod Serling
远程主机关闭连接。

它工作了！我们获得了通常的 TCP/IP 连接信息和我们的随机运势。（作为额外奖励，你也知道为什么我不为电视节目写稿了）。

# 更改 inetd 的行为

`inetd` 的行为取决于你为它设置的标记（flags）。默认标记开启 TCP wrappers，其在 `/etc/hosts.allow` 中配置（见第 9 章）。表 15-2 列出了一些实用的标记。

表 15-2：`inetd(8)` 标记

| 标记 | 说明 |
| :--- | :--- |
| `-l` | 记录每次成功的连接 |
| `-c` | 设置对任何服务每秒允许的最大连接数。默认情况下没有限制。注意，“无限”不等同于“无限”——硬件只能处理许多连接。 |
| `-R` | 设置一个 IP 地址一分钟内连接到单个服务的次数。此连接速率默认不限制，但使用它对于防止人们垄断你的带宽或资源非常有用。 |
| `-S` | 设置任何服务一分钟内可以启动的最大次数。默认是 256。如果你使用 `-R`，则允许对任何服务进行无限连接。 |
| `-a` | 设置 `inetd(8)` 绑定的 IP 地址。默认情况下，`inetd` 监听在绑定到系统的所有 IP 地址上。 |
| `-w` | 为 `inetd(8)` 启动的程序使用 TCP wrappers，如 `hosts.allow`（见第 9 章）。 |
| `-u` | 为与 `inetd(8)` 集成的服务使用 TCP wrappers，如 `hosts.allow`（见第 9 章）。 |

作为一个极端示例，如果你想使用 TCP wrappers，允许任何单个主机每秒仅进行两次连接，允许每分钟无限次服务调用，并且仅在 IP 地址 192.168.1.2 上监听，你可以在 `/etc/rc.conf` 中将其设置为：

```
inetd_flags="-w -c 2 -R 0 -a 192.168.1.2"
```
