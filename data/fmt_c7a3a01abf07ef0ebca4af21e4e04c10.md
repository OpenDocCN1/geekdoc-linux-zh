
- `EXT-icmp-in`——包含入站 ICMP 包的规则。

- `EXT-log-in`——包含在默认 INPUT 策略之前的入站包规则。

- `EXT-log-out`——包含在默认 OUTPUT 策略之前的输出包规则。

- `log-tcp-state`——包含非法状态组合的规则。

- `remote-dhcp-server-response`——包含来自此主机的 DHCP 响应的规则。

- `local-dhcp-client-query`——包含输出 DHCP 包的规则。

某些特定接口标志带有 `EXT` 前缀，以将其与 LAN 接口的用户定义链区分开来。防火墙假设只有一个外部接口。这一点建议根据接口定义不同的规则和安全策略。防火墙中的实际声明为：

```
USER_CHAINS=EXT-input \
  tcp-state-flags \
  source-address-check \
  dns-server-query \
  remote-tcp-client-request \
  remote-tcp-client-request \
  local-udp-client-request \
  EXT-dhcp-client-query \
  EXT-icmp-out \
  EXT-log-in \
  log-tcp-state \
EXT-output \
  connection-tracking \
  destination-address-check \
  remote-dns-server-response \
  local-tcp-server-response \
  local-udp-server-response \
  remote-dhcp-server-response \
  EXT-icmp-in \
  EXT-log-out
```

# 防火墙初始化

脚本启动方式与第 5 章的示例类似。回想设置的一些 shell 变量，其中一个 `$IPT` 用于定义 `iptables` 命令的位置：

```bash
#!/bin/sh
IPT="/sbin/iptables" # 系统上 iptables 的位置
INTERNET="eth0" # 连接互联网的接口
LOOPBACK_INTERFACE="lo" # 根据系统命名
IPADDR="my.ip.address" # 你的 IP 地址
MY_ISP="my.isp.address.range" # ISP 地址范围
SUBNET="my.subnet.network" # 你的子网地址
SUBNET_BROCAST="my.subnet.broadcast" # 你的子网广播地址
LOOPBACK="127.0.0.0/8" # 留回地址范围
CLASS_A="10.0.0.0/8" # A 类私有网络
CLASS_B="172.16.0.0/12" # B 类私有网络
CLASS_C="192.168.0.0/16" # C 类私有网络
CLASS_MULTICAST="224.0.0.0/4" # D 类多播地址
CLASS_RESERVED="240.0.0.0/4" # E 类预留地址
BROADCAST_SRC="255.255.255.0" # 广播源地址
BROADCAST_DEST="255.255.255.255" # 广播目的地址
PRIVPORTS="0:1023" # 已知特权端口范围
PRIVPORTS="1024:65535" # 非特权端口范围
```

设置了一些内核参数；这些参数的解释请参考第 5 章：

```
# 启用 echo 保护
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts

# 禁用源路由
for i in /proc/sys/net/ipv4/*/accept_source_route; do
echo 0 > $i
done

# 启用 TCP SYN Cookie 保护
echo 1 > /proc/sys/net/ipv4/tcp_synookies

# 禁用 ICMP 重定向接受
for i in /proc/sys/net/ipv4/*/accept_redirects; do
echo 0 > $i
done

# 不发送重定向消息
for i in /proc/sys/net/ipv4/*/accept_redirects; do
echo 0 > $i
done

# 丢弃从接口进入的伪造包，如果对其进行响应，
# 将导致响应从不同的接口出去。
for i in /proc/sys/net/ipv4/*/rp_filter; do
echo 1 > $i
done

# 记录具有不可能地址的数据包。
for i in /proc/sys/net/ipv4/*/log_martians; do
echo 1 > $i
done
```

内置链和所有预先存在的自定义链都已清空：

```
# 清空所有链中的现有规则
$IPT --flush
$IPT -t nat --flush
$IPT -t mangle --flush
```

下一步是删除用户定义的链。可以使用以下命令进行删除：

```
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X
```

首先将所有内置链的默认策略设置为 ACCEPT：

```
# 重置默认策略
$IPT --policy INPUT ACCEPT
$IPT --policy OUTPUT ACCEPT
$IPT --policy FORWARD ACCEPT
$IPT -t nat --policy PREROUTING ACCEPT
$IPT --policy OUTPUT ACCEPT
$IPT -t mangle --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PREROUTING ACCEPT
$IPT --policy OUTPUT ACCEPT
```

以下是防火墙脚本开头的最终代码，即用于允许防火墙停止的代码。将此代码放置在上述代码之后，当使用参数 `stop` 调用脚本时，脚本将清空所有内容并重置默认策略，防火墙将有效停止：

```
if [ "$1" = "stop" ]
then
echo "Firewall completely stopped! WARNING: THIS HOST HAS NO FIREWALL RUNNING."
exit 0
fi
```

现在将默认策略恢复为 DROP：

```
$IPT --policy INPUT DROP
$IPT --policy OUTPUT DROP
$IPT --policy FORWARD DROP
```

启用通过回环接口的流量：

```
# 允许回环接口的无限流量
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT
```

现在脚本开始与第 5 章的示例有所不同。

现在可以创建自定义链了。它们的名称包含在 Shell 变量 `USER_CHAINS` 中，正是为了此目的：

```
# 创建自定义链
for i in $USER_CHAINS; do
$IPT -N $i
done
```

## 安装链

遗憾的是，安装链的这种类似于函数调用的性质并不利于通过脚本进行逐步解释，因为无法同时并排显示脚本中的不同位置。

其思路是将规则放置在自定义链上，并将这些链安装到内置的 INPUT、OUTPUT 和 FORWARD 链中。如果脚本在构建自定义链时发生错误并退出，内置链将不包含规则，默认的 DROP 策略将生效，且推测回环流量将处于开启。

因此，第一次安装实际上位于防火墙脚本的末尾。第一步是检查非合法的 TCP 阶段标志组合：

```
# 如果是 TCP：检查常见的隐身 TCP 阶段模式
$IPT -A INPUT -p tcp -j tcp-state-flags
$IPT -A OUTPUT -p tcp -j tcp-state-flags
```

注意，同一个链可以被多个一个调用链引用。自定义链上的规则不会在 INPUT 和 OUTPUT 链中重复。当数据包处理到达此点时，处理将“跳转”到自定义的 `tcp-state-flags` 链。当该链中的处理完成后，处理将传回并继续执行，直到在自定义链中找到数据包的最终处理结果。

如果使用了状态模块（state module），下一步一步是：如果数据包是正在进行的、先前已接受的交换的一部分，则完全绕过防火墙：

```bash
if [ "CONNECTION_TRACKING" = "1" ]; then
# 为已建立的交换跳过防火墙过滤
$IPT -A INPUT -j connection-tracking
$IPT -A OUTPUT -j connection-tracking
```

如果机器是 DHCP 客户端，则必须为初始化期间客户端与服务器之间发送的广播消息做出准备。必须允许接受源地址 `0.0.0.0`。源地址和地址检查测试将丢弃初始 DHCP 流量：
