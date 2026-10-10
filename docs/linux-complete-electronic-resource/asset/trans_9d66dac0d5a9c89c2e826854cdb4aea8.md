

编译并安装内核后，你需要使用 `ipfwadm` 命令来配置 IP 流量统计。拆分统计信息的方法有很多种。我挑选了一个可能很有用的简单示例。更多详细信息请参阅 `ipfwadm` 的手册页。

场景：你有一个通过 PPP 链路连接到互联网的以太网。在你的以太网上，有一台机器提供了多种服务，你希望了解每种 FTP 和万维网（WWW）流量产生了多少数据，以及 TCP 和 UDP 流量的总数。

你可能使用类似以下内容的命令集（以 Shell 脚本形式展示）：

```bash
#!/bin/sh

# 清空流量统计规则
ipfwadm -A -f

# 设置快捷变量
localnet=44.136.8.96/29
any=0/0

# 为本地网段添加规则
ipfwadm -A in -a -P tcp -D $localnet ftp-data
ipfwadm -A out -a -P tcp -S $localnet ftp-data
ipfwadm -A in -a -P tcp -D $localnet www
ipfwadm -A out -a -P tcp -S $localnet www
ipfwadm -A in -a -P udp -D $localnet
ipfwadm -A out -a -P udp -S $localnet
ipfwadm -A in -a -P udp -D $localnet
ipfwadm -A out -a -P udp -S $localnet

# 默认规则
ipfwadm -A in -a -P tcp -D $any ftp-data
ipfwadm -A out -a -P tcp -S $any ftp-data
ipfwadm -A in -a -P tcp -D $any www
ipfwadm -A out -a -P tcp -S $any www
ipfwadm -A in -a -P udp -D $any
ipfwadm -A out -a -P udp -S $any
ipfwadm -A in -a -P udp -D $any
ipfwadm -A out -a -P udp -S $any

# 列出规则
ipfwadm -A -l -n
```

名称 "ftp-data" 和 "www" 指的是 `/etc/services` 文件中的相应条目。最后一条命令列出每个流量统计规则并显示累计的总和。

分析 IP 流量统计时需要注意的一个重要点是：*所有匹配规则的总和都会被累加*，因此要获取差值数据，你需要进行相应的数学计算。例如，如果我想了解既不是 *ftp* 也不是 *www* 的数据量有多少，我需要从匹配所有端口的规则总和中减去各个特定规则的总和。

```bash
root# ipfwadm -A -l -n
```

IP 流量统计规则

| 数据包 | 字节 | 方向 | 协议 | 源地址 | 目标地址 | 端口 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 入 | tcp | 0.0.0.0/0 | 44.136.8.96/29 | * -> 20 |
| 0 | 0 | 出 | tcp | 44.136.8.96/29 | 0.0.0.0/0 | 20 -> * |
| 10 | 1166 | 出 | tcp | 0.0.0.0/0 | 44.136.8.96/29 | * -> 80 |
| 10 | 572 | 出 | tcp | 44.136.8.96/29 | 0.0.0.0/0 | 80 -> * |
| 252 | 10943 | 入 | tcp | 0.0.0.0/0 | 44.136.8.96/29 | * -> * |
| 231 | 18831 | 出 | tcp | 44.136.8.96/29 | 0.0.0.0/0 | * -> * |
| 0 | 0 | 入 | udp | 0.0.0.0/0 | 44.136.8.96/29 | * -> * |
| 0 | 0 | 出 | udp | 44.136.8.96/29 | 0.0.0.0/0 | * -> * |
| 0 | 0 | 入 | tcp | 0.0.0.0/0 | 0.0.0.0/0 | * -> 20 |
| 0 | 0 | 出 | tcp | 0.0.0.0/0 | 0.0.0.0/0 | 20 -> * |
| 10 | 1166 | 入 | tcp | 0.0.0.0/0 | 0.0.0.0/0 | * -> 80 |
| 10 | 572 | 出 | tcp | 0.0.0.0/0 | 0.0.0.0/0 | 80 -> * |
| 253 | 10983 | 入 | tcp | 0.0.0.0/0 | 0.0.0.0/0 | * -> * |
| 231 | 18831 | 出 | tcp | 0.0.0.0/0 | 0.0.0.0/0 | * -> * |
| 0 | 0 | 入 | udp | 0.0.0.0/0 | 0.0.0.0/0 | * -> * |
| 0 | 0 | 出 | udp | 0.0.0.0/0 | 0.0.0.0/0 | * -> * |

## IP 流量统计（适用于 Linux 2.2）

新的流量统计代码通过 “IP 防火墙链（IP Firewall Chains）” 访问。更多信息请参阅 IP *ichains* 主页（[http://www.aladei4w.net.au/~rusr/comp/ipchains/iphchains.html](http://www.aladei4w.net.au/~rusr/comp/ipchains/iphchains.html)）。除了其他更改外，你现在需要使用 *ipchains* 而不是 *ipfwadm* 来配置你的过滤器。（参见最新内核源码中的 *Documentation/Changes*）。

## IP 别名（IP Aliasing）

在某些应用场景中，能够为单个网络设备配置多个 IP 地址是非常有用的。互联网服务提供商（ISP）经常使用此功能，为客户的万维网和 FTP 服务提供“定制化”的域名。有关更多信息，请参阅 “IP-Alias 迷你 HOWTO”。

**内核编译选项：**

```text
Networking options -->
  ...
  [*] Network aliasing
  ...
  <>: IP; aliasing support
```

编译并安装带有 IP_Alias 的内核后，支持配置非常简单。别名被添加到与真实网络设备相关联的虚拟网络设备上。这些设备遵循一个简单的命名约定：<设备名>::<虚拟设备号>，例如 `eth0:0`、`ppp0:10` 等。请注意，ifname:number 设备只能在主接口设置好之后才能进行配置。

例如，如果你有一个同时支持两个不同 IP 子网的以太网，并且希望你的机器能直接访问这两个子网，你可以使用类似以下命令：

```bash
root# ifconfig eth0 192.168.1.1 netmask 255.255.255.0 up
root# route add -net 192.168.1.0 netmask 255.255.255.0 eth0

root# ifconfig eth0:0 192.168.10.1 netmask 255.255.255.0 up
root# route add -net 192.168.10.0 netmask 255.255.255.0 eth0:0
```

要删除别名，只需在其名称末尾添加 “-” 并引用它，操作非常简单：

```bash
root# ifconfig eth0:- 0
```

与该别名相关的所有路由也会自动被删除。

## IP 防火墙（适用于 Linux 2.2）

IP 防火墙及防火墙问题在 Firewall-HOWTO 中得到了更深入的探讨（参见 [http://metalab.unc.edu/](http://metalab.unc.edu/)）。IP 防火墙允许你通过过滤或允许来自或发往指定 IP 地址的数据报，来保护机器免受未授权的网络访问。规则分为三类：入站过滤、出站过滤和转发过滤。入站规则应用于网络接收到的数据报。出站规则应用于网络发送的数据报。转发规则应用于接收到的但不是发给本机（即会被路由转发）的数据报。

**内核编译选项：**

```text
Networking options --->
[*] Network firewalls
......
[*] IP: forwarding/gatewaying
......
[*] IP: firewalling
[ ] IP: firewall packet logging
```

IP 防火墙规则的配置是使用 `ipfwadm` 命令完成的。如前所述，我不是安全方面的专家，因此虽然我会提供一个可供使用的示例，但如果你对安全至关重要，建议你自己进行研究并制定属于自己的规则。

IP 防火墙最常见的用途之一是当你将 Linux 机器用作路由器和防火墙网关，以保护你的本地网络免受来自外部网络的未授权访问时。

以下配置基于 Arnt Gulbrandsen <agulbra@troll.no> 提供的贡献。

该示例描述了在 Linux 防火墙/路由器机器上配置防火墙规则的方法，如图中的示意图所示：

![](img/a3584dae761d2e3abed8bf40d7637389_258_0.png)

通常，以下命令应放置在 rc 文件中，以便系统每次启动时自动执行。为了获得最大安全性，这些操作应在配置网络接口之后，但在接口实际启动之前执行，以防止任何人在防火墙机器重启期间获得访问权限。

```bash
#!/bin/sh
# 清空 'forwarding'（转发）规则表
# 将默认策略更改为 'accept'（接受）
#
/sbin/ipfwadm -F -f
/sbin/ipfwadm -F -p accept

# .. 以及针对 'Incoming'（入站）
#
/sbin/ipfwadm -I -f
/sbin/ipfwadm -I -P accept

# 首先，封锁 PPP 接口
# 我更喜欢使用 '-a reject' 而不是 '-a reject -y'，但那样做的话
# 就不可能从该接口发起连接了。
# -o 选项会导致所有被拒绝的数据报被记录。
# 这是以磁盘空间换取对攻击或配置错误的感知。
#
/sbin/ipfwadm -I -a reject -y -o -P tcp -S 0/0 -D 172.16.174.30

# 立即丢弃某些明显伪造的数据包类型：
# 任何来自组播/任播/广播地址的数据都不应到达
#
/sbin/ipfwadm -F -a deny -o -S 224.0/3 -D 172.16.37.0/24
#
# 并且来自回环网络的数据绝不应该出现在物理线路上
#
/sbin/ipfwadm -F -a deny -o -S 127.0/8 -D 172.16.37.0/24

# 接受入站 SMTP 和 DNS 连接，但仅允许
# 连接到邮件/域名服务器
#
/sbin/ipfwadm -F -a accept -P tcp -S 0/0 -D 172.16.37.19 25 53
#
# DNS 既使用 UDP 也使用 TCP，因此也允许
# 发给我们域名服务器的 UDP 查询
#
/sbin/ipfwadm -F -a accept -P udp -S 0/0 -D 172.16.37.19 53
#
# 但不允许发往 NFS 以及 Larry McVoy 的 NFS 扩展等危险端口的
# ‘应答’。如果你运行 squid，请在此添加其端口。
#
/sbin/ipfwadm -F -a deny -o -P udp -S 0/0 53 \
-D 172.16.37.0/24 2049 2050

# 发往其他用户端口的应答是可以的
#
/sbin/ipfwadm -F -a accept -P udp -S 0/0 53 \
-D 172.16.37.0/24 53 1024:65535
```

