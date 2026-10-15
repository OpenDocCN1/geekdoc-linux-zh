
# 拒绝访问 syslog

`ipchains -A input -p udp -s 0.0.0.0/0 -d $EXTERNAL`

```bash
# 远程接口，声源为任何地址是有效的

ipchains -A input -i $EXTDEV -s 0.0.0.0/0 -d $EXTERNALIP/32
```

```bash
# 隧道 IP。只有在需要时才开启它。

ipchains -A input -i $EXTDEV -s $PORT

ipchains -A input -i $EXTDEV -s $CIPE_INET
```

```bash
ipchains -Ai -i $EXTDEV
```

```bash
# 隧道 IP 只有在需要时。

ipchains -A output -i $EXTDEV -s $CIPE_INET/32
```

```bash
# 伪装 IP 网段是有效的。

ipchains -A output -i $EXTDEV -s $CIPEREALNET/23 \
# j ACCEPT

ipchains -A output -i $EXTDEV -s $CIPEREALNET/23 \
# j ACCEPT

ipchains -A output -i $EXTDEV -s 0.0.0/0 -
```

```bash
# 捕获规则，所有其他出站被拒绝。

ipchains -A output -j DENY -1

ipchains -A output -j DENY

ipchains -A output -s 0.0.0/0 -1 DENY
```

```bash
echo "Done with the firewall rules*"

echo -n "acct..."
```

```bash
# 计数，刷新所有条目

ipchains -N acctin

ipchains -N acctout

ipchains -N acctio

# 仅跟踪到网络的流量
```

```bash
# 出站、刷新并设置默认策略为拒绝。实际上
# 默认策略是无关的，因为有一条包含
# 拒绝和记录的捕获规则。

echo "Setting new output rules"

echo -n "output..."
```

```bash
# 出站、刷新并设置默认策略为拒绝。

ipchains -F output

ipchains -P output DENY
```

```bash
# 本地接口，任何源到本地网段都是有效的

ipchains -A output -i $INTDEV -s 0.0.0.0/0 -d $INTNET/24 - ACCEPT

ipchains -A output -i $INTDEV -s 0.0.0.0/0 -d $INTNET/24 - ACCEPT
```

```bash
# 回环接口是有效的。

ipchains -A output -i lo -s 0.0.0.0/0 -d 0.0.0.0/0 - ACCEPT

ipchains -A output -i lo -s 0.0.0.0/0 -d 0.0.0.0/0 - ACCEPT
```

```bash
# 远程接口到本地网段：路由，拒绝。

ipchains -A output -i $EXTDEV -s 0.0.0.0/0 -d $INTNET/24 - DENY
```

```bash
# 远程接口从本地网段出站：识别，拒绝。

ipchains -A output -i $EXTDEV -s $INTNET/24 -d 0.0.0.0/0 - DENY
```

```bash
# 远程接口上的其他任何流量都是有效的

ipchains -A output -i $EXTDEV -s 0.0.0.0/0 - ACCEPT

ipchains -A output -i $EXTDEV -s $EXTERNALIP/32 -d 0.0.0.0/0 - ACCEPT
```

## 简单的 IPTables 防火墙（第8章）

```bash
# 将 xxx.xxx.xxx.xxx 替换为服务器 IP 地址

iptables -F

iptables -X

iptables -P INPUT ACCEPT

iptables -P OUTPUT ACCEPT

iptables -P FORWARD ACCEPT

iptables -A INPUT -i lo -j ACCEPT

iptables -A INPUT -p udp -s xxx.xxx.xxx.xxx --sport 53 -j ACCEPT

iptables -A INPUT -p tcp --syn -j REJECT

iptables -A INPUT -p udp -j REJECT
```

## IPTables 主机防火墙（第9章）

```bash
#!/bin/sh

################################################################################
# 主机防火墙 1.0                                                               #
# 用于单托管主机的防火墙，具有严格的（默认被 # 阻塞）                         #
# 输入和输出规则集，以及严格的 ICMP 规则集。#                                 #
# 包含 TCP 标志验证和 SYN 速率限制。                                           #
# 版权所有 (C) 2002 Bill McCarthy                                              #
# 本程序为自由软件；你可以根据自由软件基金会发布的                             #
# GNU 通用许可许可证条款重新分发和/或修改                                      #
# 它，版本 2 或更高版本。                                                      #
# 不提供任何保证，即使是关于商品性或                                          #
# 特定用途的适用性的暗示保证。详情请参阅 GNU                                  #
# 通用许可许可证。                                                             #
# 你应该随本程序收到一份 GNU 通用许可许可证                                    #
# 的副本，或者能够从该程序的下载站点获取它。                                   #
# 如果没有，你可以从自由软件基金会的                                           #
# 网站 www.gnu.org 获取它。                                                    #
################################################################################
```

## 附录 E：示例防火墙脚本 475

###################################################################################################################
# 加载内核模块
###################################################################################################################

```
/sbin/modprobe/ip_tables
/sbin/modprobe/ip_conntrack
/sbin/modprobe/iptables_filter
/sbin/modprobe/iptables_mangle
/sbin/modprobe/iptables_nat
/sbin/modprobe/ip_LOG
/sbin/modprobe/ipt_REJECT
/sbin/modprobe/ipt_limit
/sbin/modprobe/ipt_state
/sbin/modprobe/ip_conntrack_ftp
/sbin/modprobe/ip_conntrack_irc
```

###################################################################################################################
# 设置内核配置选项
###################################################################################################################

```
sysctl -w net.ipv4.conf.default.rp_filter = 1

sysctl -w net.ipv4.conf.eth0.accept_source_routing = 0
```
