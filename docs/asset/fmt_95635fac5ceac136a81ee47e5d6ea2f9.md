
```
# $DNSSERVER 是我们的 DNS 服务器。
$IPTABLES -P INPUT DROP
$IPTABLES -A INPUT -s 10.10.10.0/24 -p tcp \
  --dport 80 -j ACCEPT
$IPTABLES -A INPUT -s 192.168.1.0/24 -p tcp \
  --dport 80 -j ACCEPT
$IPTABLES -A INPUT -s 10.10.10.0/24 -p tcp \
  --dport 443 -j ACCEPT
$IPTABLES -A INPUT -s 192.168.1.0/24 -p tcp \
  --dport 443 -j ACCEPT
$IPTABLES -A INPUT -s 172.16.32.32 -p tcp \
  --dport 22 -j ACCEPT
$IPTABLES -A INPUT -p udp -m udp \
  -s $DNSSERVER --port 53 -d 0/0 -j ACCEPT
```

第二个示例实现了相同的效果，但具有更高的灵活性且对整体网络更友好，因为 `REJECT` 会返回 `RST/ACK`。之前的规则使用 `DROP`，它只是直接将数据包丢弃一边：

# `$DNSSERVER` 是你的 DNS 服务器的 IP 地址。

```
$IPTABLES -N WEBCLIENTS
$IPTABLES -A INPUT -N WEBCLIENTS
$IPTABLES -A FORWARD -j WEBCLIENTS

$IPTABLES -A WEBCLIENTS -p tcp -m tcp --dport 80 \
  -s 10.10.0/24 --syn -j ACCEPT

$IPTABLES -A WEBCLIENTS -p tcp -m tcp --dport 80 \
  -s 192.168.1.0/24 --syn -j ACCEPT

$IPTABLES -A WEBCLIENTS -p tcp -m tcp --dport 443 \
  -s 10.10.0/24 --syn -j ACCEPT

$IPTABLES -A WEBCLIENTS -p tcp -m tcp --dport 443 \
  -s 192.168.1.0/24 --syn -j ACCEPT

$IPTABLES -A WEBCLIENTS -p tcp -m tcp --dport 22 \
  -s 172.16.32.32 --syn -j ACCEPT
$IPTABLES -A WEBCLIENTS -p udp -m udp -s $DNSSERVER \
  --sport 53 -d 0/0 -j ACCEPT

$IPTABLES -A WEBCLIENTS -p tcp -m tcp --syn -j REJECT
$IPTABLES -A WEBCLIENTS -p udp -m udp -j REJECT
```

## 转发从防火墙到内部 Web 服务器的连接

这种配置假设你有一个防火墙（Host-A）和一个位于 DMZ 的服务器（Host-B，`192.168.1.0/24`）。允许网络 `10.10.10.0/24` 和 `192.168.1.0/24` 仅通过 80 和 443 端口连接。SSH 连接仅允许来自主机 `172.16.32.32`。图 15.1 描述了：

```
# $DNSSERVER 是我们的 DNS 服务器。
$IPTABLES -P INPUT DROP
$IPTABLES -A INPUT -s 10.10.10.0/24 -p tcp \
  --dport 80 -j ACCEPT
$IPTABLES -A INPUT -s 192.168.1.0/24 -p tcp \
  --dport 80 -j ACCEPT
$IPTABLES -A INPUT -s 10.10.10.0/24 -p tcp \
  --dport 443 -j ACCEPT
$IPTABLES -A INPUT -s 192.168.1.0/24 -p tcp \
  --dport 443 -j ACCEPT
$IPTABLES -A INPUT -s 172.16.32.32 -p tcp \
  --dport 22 -j ACCEPT
$IPTABLES -A INPUT -p udp -m udp \
  -s $DNSSERVER --port 53 -d 0/0 -j ACCEPT
```

## 转发：到互联网上的远程服务器

这种特定的场景我们在处理托管领域的系统时经常遇到。这是一个相当具有迁移性的业务，服务器经常在大型托管提供商之间移动。这种想法是将内容和业务迁移到新服务器，并在旧系统上设置防火墙规则，将流量 NAT 到新服务器。这通常用于在不同提供商之间迁移时，以便在 DNS 记录传播期间避免停机。

以下脚本是前一个脚本的功能性工作示例，但它将所有流量转发到远程服务器的 IP 地址。它使用一个重定向的外部文件来以这种格式列出源 IP 和目的 IP：源-IP:目的-IP（例如 `11.22.33.44:22.33.44.55`）。

```
#!/bin/sh

IPTABLES="/sbin/iptables"
CONFIG=/etc/rc.d/forwarded
EXTERNAL=eth0
```

```bash
# 启用连接跟踪
$IPTABLES -A INPUT -m state \
  --state ESTABLISHED,RELATED -j ACCEPT
$IPTABLES -A OUTPUT -m state \
  --state NEW,ESTABLISHED,RELATED -j ACCEPT
$IPTABLES -A FORWARD -i EXTERNAL -o EXTERNAL \
  --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
for i in `cat $CONFIG`; do
SOURCEIP=$(echo $i | awk '{print $1}')
DESTIP=$(echo $i | awk -F: '{print $2}')
echo "Forwarding $SOURCEIP to $DESTIP"
$IPTABLES -A FORWARD -i $EXTERNAL -o $EXTERNAL \
  -d $SOURCEIP -m state \
  NEW,ESTABLISHED,RELATED -j ACCEPT
$IPTABLES -t nat -A PREROUTING -i $EXTERNAL \
  -d $SOURCEIP -j DNAT --to-destination $DESTIP
$IPTABLES -t nat -A POSTROUTING -d $DESTIP \
  -j SNAT --$SOURCEIP
done
```

```bash
### 在内核中启用 IP 转发
echo "1" > /proc/sys/net/ipv4/ip_forward
```

在托管环境中，一个接口上拥有多个甚至有时是数百个 IP 是非常常见的。这种方法使得缓解在服务器之间移动大量虚拟主机时通常会经历停机时间成为可能。

## FORWARD：过滤对转发服务器的访问

接下来的规则显示了如何限制可以连接到转发的 Web 服务器的主机。在示例中，我们的防火墙 Host-A 将连接转发到内部服务器 Host-B (`192.168.1.80`)。允许以下网络连接：`22.33.44.0/24`（Internet）到 TCP 端口 80 和 443。

第一个配置演示了使用 DNAT 规则实现此类类型配置所需的规则：

```bash
# eth0 是外部接口（Internet）
# eth1 是内部接口（10.10.10.0/24）
# eth2 是 DMZ 接口（192.168.1.0/24）
# EXTERNALIP 是你防火墙上的外部 IP
# 192.168.1.1 是防火墙
# eth2 接口上的内部 IP 地址

IPTABLES -A FORWARD -i eth0 -o eth2 -p tcp \
  -s 22.33.44.0/24 --dport 80 -m state \
  --state NEW,ESTABLISHED,RELATED -j ACCEPT
IPTABLES -A FORWARD -i eth0 -o eth2 -p tcp \
  -s 22.33.44.0/24 --dport 443 -m state \
  --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```bash
# 对于来自 22.33.44.0/24 的互联网用户
IPTABLES -t nat -A PREROUTING -i eth0 -p tcp \
  -s 22.33.44.0/24 --dport 80 -d $EXTERNAL \
  -j DNAT --to-destination 192.168.1.80:80
```
