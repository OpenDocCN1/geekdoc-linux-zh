
# DNS

在本章较早部分，我们涵盖了可能流向和来自 DNS 服务器的流量类型。再次，我们首先允许进入端口 53 的入站 TCP 或 UDP 请求，以及所有属于已连接的数据包：

```bash
$IPT -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

```bash
$IPT -A INPUT -p tcp --dport 53 --sport 1024:65535 -m state \
-state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
$IPT -A INPUT -p udp --dport 53 --sport 53 -m state \
-state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
$IPT -A INPUT -p tcp --dport 53 1024:65535 -m state \
-state NEW,ESTABLISHED,RELATED -j ACCEPT
```

## 使用 Iptables 进行包过滤 195

根据版本（以及配置），BIND 在创建出站连接时使用端口 53 或非特权端口：

```bash
$IPT -A OUTPUT -m owner --uid-owner 0 -p tcp --sport 53 \
-m state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
$IPT -A OUTPUT -m owner --uid-owner 0 -p tcp --sport 1024:65535 \
-m state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
$IPT -A OUTPUT -m owner --uid-owner 0 -p udp --sport 53 \
-m state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
$IPT -A OUTPUT -m owner --uid-owner 0 -p udp --sport 1024:65535 \
-m state NEW,ESTABLISHED,RELATED -j ACCEPT
```

# SSH

之前我们提到通过连接 LAN 内部的服务器允许远程主机访问防火墙。这种远程访问并不理想，但在实践中可能是必要的，并且比直接访问防火墙要好。如果你选择这种设置，请确保正确配置守护进程——理想情况下它应该运行在另一台机器上。允许离开机器的唯一流量应该是指向防火墙的或者是守护进程与远程主机之间的已连接流量：

```bash
$IPT -A INPUT -p udp --sport 1024:65535 --dport 22 \
-d <防火墙IP地址> -m state \
--state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
$IPT -A OUTPUT -p udp --sport 22 -state ESTABLISHED,RELATED -j ACCEPT
```

## 5.3 防火墙管理：处理动态 IP

动态 IP 主要出现在拨号上网，分配给主机的时间从几小时到几个月不等。在以太网的网络上（例如电缆调制调器使用的），通常使用 DHCP；除了为主机分配 IP 地址外，DNS 服务器、网关和广播等信息也可能传递给客户端。这在创建防火墙时会产生问题。虽然可以使用 `MASQUERADE` 目标来避免知道主机的 IP 地址（此处由于原文拼写错误为 ES，应为 ADDRESS），但 DNS 服务器等信息通常被硬编码在防火墙脚本中。对于动态地址的主机，必须采取措施自动同步从 DHCP 服务器接收到的信息。

# DHCPCD

大多数 Linux 系统的默认 DHCP 客户端名为 `dhcpcd`。当配置了 DHCP 的接口启动时（例如进入运行级别 3），`dhcpcd` 在后台启动并尝试联系 DHCP 服务器。成功查询 DHCP 服务器后，检索的信息写入文件中。该文件的位置取决于发行版。在 SuSE 和较新版本的 Red Hat 中，可以在 `/var/lib/dhcpcd` 找到；在许多其他系统中，它位于 `/etc/dhcpcd`。文件的格式为 `dhcpcd-eth0.info`，其中 `eth0` 被替换为接口名称。

```text
# cat dhcpcd-eth2.info
IPADDR=1.2.3.4
NETMASK=255.255.255.0
NETWORK=1.2.3.0
BROADCAST=255.255.255.255
GATEWAY=1.2.3.254
HOSTNAME='host.example.org'
DNS=194.164.8.100,194.164.4.100
DHCPID=62.254.64.20
DHCPGIADDR=0.0.0.0
DHCPCHADDR=00:A5:24:4C:3E:57
DHCPHSADDR=00:0C:36:E5:54:8C
DHCPNAME=''
LEASETIME=61939
RENEWTIME=30969
```

## 使用 Iptables 进行包过滤 197

```text
REBINDTIME=54196

INTERFACE='eth2'

CLASSID='Linux 2.4.21-144-default i686'

CLIENTID=00:A0:24:4C:3E:57
```

使用一点 shell 脚本，你可以修改防火墙脚本来读取文件中存储的值：

```bash
#!/bin/bash
IP_EXT=$(grep IPADDR=/etc/dhcp/dhcpcd-eth0.info | cut -f 2 -d '=')
GATEWAY=$(grep GATEWAY=/etc/dhcp/dhcpcd-eth0.info | cut -f 2 -d '=')
```

对于 DNS 服务器，脚本稍微复杂一些，因为使用了逗号分隔的列表。这次，我们通过 `cut` 两次管道输出，第二次使用逗号作为分隔符。

如果列表中只有一个 IP 地址，`$IP_DNS2` 将具有与 `$IP_DNS1` 相同的值。

现在防火墙变量设置机制已经就绪，需要一种方法在这些变量可用时自动执行防火墙。这因发行版而异，我们在这里介绍最常见的方法。

在许多系统中，每当 DHCP 启动接口时，都会调用 shell 脚本 `/etc/dhcp/dhcp.exe`（可以通过调用 `-c` 切换切换要执行的脚本名称）。在其他系统中，会执行一个钩子脚本（SUSE 为 `/etc/sysconfig/network/scripts/dhcpcd-hook`）。无论如何，你只需要在适当的脚本中添加条目来执行防火墙，例如：

```bash
source /usr/local/etc/rc.firewall
```

## 阻塞与取消阻塞主机

在本章早期，你已经看到了如何使用外部文件来存储主机列表，然后这些列表可以被 Iptables 处理。在我们的示例中，我们使用该文件来维护一个需要拒绝访问的 IP 地址列表：

```bash
for host in /usr/local/etc/hosts.deny; do
IPT -I INPUT -s $host -j DROP
IPT -I FORWARD -s $host -j DROP
IPT -I OUTPUT -d $host -j DROP
IPT -I FORWARD -d $host -j DROP
done
```

这确实简化了阻塞主机的过程，但请记住，每当修改 `/usr/local/etc/hosts.deny` 时，必须重新加载防火墙规则集。我们可以通过编写脚本从阻塞列表中添加/删除主机，然后自动重启防火墙，让事情变得更加简单：
