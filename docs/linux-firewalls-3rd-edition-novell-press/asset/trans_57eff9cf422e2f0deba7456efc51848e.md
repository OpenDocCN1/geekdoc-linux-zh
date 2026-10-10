

## 图 5.4
基于目标地址的用户自定义链。

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_206_0.png)

## 图 5.5
基于协议的用户自定义链。

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_206_1.png)

此列表总结了第 3 章“iptables：Linux 防火墙管理程序”中用户自定义链的特性。

- 用户自定义链是通过 `-N` 或 `--new-chain` 操作创建的。
- 用户自定义链的名称长度最多可达 30 个字符。
- 用户自定义链的名称可以包含连字符 (-)，但不能包含下划线 (_)。
- 用户自定义链作为规则目标进行访问。
- 用户自定义链没有默认策略。
- 用户自定义链可以调用其他用户自定义链。
- 如果数据包未匹配用户自定义链中的规则，控制权将返回到调用链中的下一条规则。
- 通过 RETURN 目标，可以提前退出用户自定义链，控制权返回到调用链中的下一条规则。
- 用户自定义链是通过 `-X` 或 `--delete-chain` 操作删除的。
- 在删除链之前，该链必须为空。
- 如果要删除链，该链不能有其他链引用它。
- 可以使用 `-F` 或 `--flush` 操作按名称特定地清空一个链，或者如果指定了 `-n`，则清空所有现有链。

下一节将利用用户自定义链以及规则组织部分中介绍的概念，来优化第 4 章中展示的单系统防火墙。

## 优化示例

在下面的示例中，Shell 变量和内核级保护服务与第 4 章示例中列出的相同。声明了一个新变量 USER_CHAINS，其中包含脚本中使用的所有用户自定义链的名称。

### 脚本中的用户自定义链

这些链列表如下：

- `tcp-state-flags`—包含用于检查无效 TCP 状态标志组合的规则。
- `connection-tracking`—包含用于检查与状态相关的匹配项，如 `INVALID`、`ESTABLISHED` 和 `RELATED` 的规则。
- `source-address-check`—包含用于检查非法源地址的规则。
- `destination-address-check`—包含用于检查非法目标地址的规则。
- `EXT-input`—包含 `INPUT` 链中针对特定接口的用户自定义链。在本示例中，该主机有一个连接到 Internet 的接口。

一些针对特定接口的链以 EXT 作为前缀，以区别于包含任何局域网接口规则的自定义链。此防火墙示例假设只有一个接口，即外部接口。这里的要点是建议可以按接口定义不同的规则和安全策略。

# 第 5 章：防火墙优化

在防火墙 Shell 脚本中的实际声明如下所示：

```bash
USER_CHAINS="EXT-input
            tcp-state-flags
            source-address-check
            local-dns-server-query
            local-tcp-client-request
            remote-tcp-client-request
            local-udp-client-request
            local-dhcp-client-query
            EXT-icmp-out
            EXT-log-in
            log-tcp-state
            EXT-output \
            connection-tracking \
            destination-address-check \
            remote-dns-server-response \
            remote-tcp-client-response \
            local-tcp-server-response \
            remote-udp-server-response \
            remote-dhcp-server-response \
            EXT-icmp-in \
            EXT-log-out"
```

## 防火墙初始化

防火墙脚本的开头与第 4 章的示例完全相同。回忆一下，设置了一系列 Shell 变量，包括名为 $IPT 的变量，用于定义 iptables 防火墙管理命令的位置：

```bash
#!/bin/sh

IPT="/sbin/iptables"           # 您系统中 iptables 的位置
INTERNET="eth0"               # Internet 连接接口
LOOPBACK_INTERFACE="lo"       # 无论您的系统如何命名它
IPADDR="my.ip.address"        # 您的 IP 地址
ISP="my_isp_address_range"    # ISP 服务器和 NOC 地址范围
SUBNET_BASE="my.subnet.network"   # 您的子网网络地址
SUBNET_BROADCAST="my.subnet.broadcast"   # 您的子网广播地址
LOOPBACK="127.0.0.8"         # 保留的环回地址范围
CLASS_A="10.0.0.0/8"        # A 类私有网络
CLASS_B="172.16.0.0/12"     # B 类私有网络
CLASS_C="192.168.0.0/16"    # C 类私有网络
CLASS_D_MULTICAST="224.0.0.0/4"   # D 类多播地址
CLASS_E_RESERVED_NET="240.0.0.0/5"   # E 类保留网络
BROADCAST_SRC="0.0.0.0"     # 广播源地址
BROADCAST_DEST="255.255.255.255"   # 广播目标地址
PRIVPORTS="0:1023"          # 知名、特权端口范围
UNPRIVPORTS="1024:65535"    # 非特权端口范围
```

还设置了一些内核参数；请参阅第 4 章了解这些参数的说明：

```bash
# 启用广播回显保护
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
# 禁用源路由数据包
for f in /proc/sys/net/ipv4/conf/*/accept_source_route; do
    echo 0 > $f
done
# 启用 TCP SYN Cookie 保护
echo 1 > /proc/sys/net/ipv4/tcp_syncookies
# 禁用 ICMP 重定向接受
for f in /proc/sys/net/ipv4/conf/*/accept_redirects; do
    echo 0 > $f
done
# 不发送重定向消息
for f in /proc/sys/net/ipv4/conf/*/send_redirects; do
    echo 0 > $f
done
# 丢弃进入接口的欺骗数据包，如果对此类数据包进行回复，回复将从不同的接口发出。
for f in /proc/sys/net/ipv4/conf/*/rp_filter; do
    echo 1 > $f
done
# 记录具有不可能地址的数据包。
for f in /proc/sys/net/ipv4/conf/*/log_martians; do
    echo 1 > $f
done
```

清空内置链和任何现有的用户自定义链：

```bash
# 从所有链中移除任何现有规则
$IPT --flush
$IPT -t nat --flush
$IPT -t mangle --flush
```

下一步是删除用户自定义链。可以使用以下命令删除它们：

```bash
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X
```

首先将所有内置链的默认策略设置为 ACCEPT：

```bash
# 重置默认策略
$IPT --policy INPUT ACCEPT
$IPT --policy OUTPUT ACCEPT
$IPT --policy FORWARD ACCEPT
$IPT -t nat --policy PREROUTING ACCEPT
$IPT -t nat --policy OUTPUT ACCEPT
$IPT -t nat --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PREROUTING ACCEPT
$IPT -t mangle --policy OUTPUT ACCEPT
```

以下是防火墙脚本开头的最终代码，即让防火墙能够轻松停止的代码。将此代码放在上述代码之后，当您使用 stop 参数调用脚本时，脚本将刷新、清除并重置默认策略，从而有效地停止防火墙。

```bash
if [ "$1" = "stop" ]
then
 echo 'Firewall completely stopped! WARNING: THIS HOST HAS NO FIREWALL RUNNING.'
 exit 0
fi
```

现在将实际的默认策略重置为 DROP：

```bash
$IPT --policy INPUT DROP
$IPT --policy OUTPUT DROP
$IPT --policy FORWARD DROP
$IPT -t nat --policy PREROUTING DROP
$IPT -t nat --policy OUTPUT DROP
$IPT -t nat --policy POSTROUTING DROP
$IPT -t mangle --policy PREROUTING DROP
$IPT -t mangle --policy OUTPUT DROP
```

启用通过环回接口通信：

```bash
# 环回接口上的无限制流量
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT
```

现在脚本开始与第 4 章的示例有所不同。

现在可以创建用户自定义链。它们的名称被包含在单一的 Shell 变量 USER_CHAINS 中，正是为了这个目的：

```bash
# 创建用户自定义链
for i in $USER_CHAINS; do
    $IPT -N $i
done
```

## 安装链

不幸的是，构建和安装链的功能调用特性不适合在没有同时并排展示脚本中不同位置的能力下进行串行的逐步说明。

想法是将规则放置在用户自定义链上，然后将这些链安装在内置的 INPUT、OUTPUT 和 FORWARD 链上。如果脚本包含错误并且退出时
