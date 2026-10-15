
`/sbin/ipchains -A output -j ACCEPT -i $LOOPBACKIF -s UNIVERSE -d $UNIVERSE`

## 附录 D

## 强力数据包防火墙规则集

```
# DHCP：如果你在这台 Linux 机器上配置了 DHCP 服务器，
# 你需要启用以下规则集。
```

```bash
# 默认禁用。
#/sbin/ipchains -A output -i $INTIF -p udp -s $INTIF/32 bootps -d $BROADCAST/0 bootpc
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $INTIF/32 bootps -d $BROADCAST/0 bootpc
```

```bash
# HTTP：以下示例了如何允许 HTTP 流量访问内网
# WWW 服务器，同时不允许从外部
# 网络进行访问。
```

```bash
# 默认禁用。
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $INTIF/32 http -d $INTLAN
```

```bash
# 内部局域网主机的显式输出
```

```bash
# 此规则集仅允许内部局域网上的特定主机
# 访问此防火墙服务器本身。许多人可能认为
# 这些是极端的，但许多系统攻击也发生在内部网络中。
```

```bash
# 给出的示例允许通过 FTP、FTP-DATA、SSH 和 TELNET 访问。
```

```bash
# 为了使此规则集生效，你必须先注释掉上面那行
# 提供所有内部主机对内部局域网拥有完全访问权限的行。
```

```bash
# 默认禁用。
```

```bash
#echo " 为特定主机设置输出过滤器。"
```

```bash
# 第一个主机
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $ftp
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $ftp-data
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $ssh
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST1/32 -d $telnet
```

```bash
# 第二个主机
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $ftp
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $ftp-data
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $ssh
#/sbin/ipchains -A output -j ACCEPT -i $INTIF -p tcp -s $HOST2/32 -d $telnet
```

## 附录：强力数据包防火墙规则集

```bash
# 外部接口上的出站流量
```

```bash
# 此规则集将控制哪些流量可以从外部出去。
```

```bash
echo " - 为外部接口的流量设置输入过滤器。"
```

```bash
# 拒绝从远程接口到本地网网的出站流量，
# 填充路由；拒绝并记录
/sbin/ipchains -A output -j REJECT -i $EXTIF -s $UNIVERSE -d $INTLAN LOGGING
```

```bash
# 拒绝从外部接口到本地网的出站流量，
# 填充伪装，拒绝并记录
/sbin/ipchains -A output -j REJECT -i $EXTIF -s $INTLAN -d $UNIVERSE LOGGING
```

```bash
# DHCP 客户端：如果你的 Linux 服务器通过 DSL 或电缆调制解调器
# 连接并且获取动态 DHCP 地址，你需要
# 启用以下规则集。
```

```bash
# 默认启用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $UNIVERSE bootpc -d $UNIVERSE bootps
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p udp -s $UNIVERSE
```

```bash
# FTP：允许 FTP 流量（该 Linux 服务器是 FTP 服务器）
```

```bash
# 默认禁用。
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ftp-data -d $UNIVERSE
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ftp-data -d $UNIVERSE
```

```bash
# HTTP：允许 HTTP 流量（该 Linux 服务器是 WWW 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP http -d $UNIVERSE
```

```bash
# NTP：允许 NTP 更新（该 Linux 服务器是 NTP 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ntp -d $UNIVERSE
```

```bash
# TELNET：允许 telnet 流量（该 Linux 服务器是 TELNET 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP telnet -d $UNIVERSE
```

```bash
# SSH 服务器：允许出站 SSH 流量（该 Linux 服务器是 SSH 服务器）
```

```bash
# 默认禁用
/sbin/ipchains -A output -j ACCEPT -i $EXTIF -p tcp -s $EXTIP ssh -d $UNIVERSE
```

## 附录 D：强力数据包防火墙规则集

```bash
# 所有接口上的出站流量
# 此规则集将控制所有接口的流量。这通常
# 被认为是公共服务的。
# 我们提供了一些拒绝规则集作为示例，
# 但由于上面的 REJECT 语句，这些并不是必须的。
```

```bash
echo " 为所有接口的公共服务设置输出过滤器。"
# AUTH：允许所有接口身份验证（在 /etc/inetd.conf 中禁用）。
/sbin/ipchains -A output -j ACCEPT -p tcp -s $UNIVERSE -d $UNIVERSE
```

```bash
# DNS：如果你的 Linux 服务器是权威服务器，
# 你必须启用此规则集
# 默认禁用
#/sbin/ipchains -A output -j ACCEPT -p tcp -s $EXTIP domain -d $UNIVERSE
#/sbin/ipchains -A output -j ACCEPT -p udp -s $EXTIP domain -d $UNIVERSE
```

```bash
# ICMP：允许输出 ICMP 流量
# 注意：通过防火墙规则集禁用 ICMP 包的作用
# 不仅仅是防止人们 ping 你的机器。许多
# TCP/IP 及其应用程序依赖 ICMP。没有 ICMP，
# Linux 服务器和内部计算机可能无法工作。
#/sbin/ipchains -A output -j ACCEPT -p icmp -s $UNIVERSE -d $UNIVERSE
```

```bash
# NNTP：允许基于 NNTP 的新闻。
# SMTP：如果 Linux 服务器是权威服务器，
# 你必须允许此规则集。
#/sbin/ipchains -A output -j ACCEPT -p tcp -s $EXTIP smtp -d $UNIVERSE
```

## 附录 D：强力数据包防火墙规则集

### 特定输出拒绝

# 这些规则集拒绝你不想离开系统的流量。

# echo " - 拒绝特定的输出。"

# RPC。

/sbin/ipchains -A output -j REJECT -i $EXTIF -p udp -s $EXTIF -d $UNIVERSE LOGGING
