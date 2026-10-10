
# 第 5 章优化版 iptables 防火墙

对于大多数通过 DSL、电缆调制解调器或较低速度的租专线连接的计算机来说，Linux 网络代码处理数据包的速度往往比网络连接更快。特别是因为防火墙规则具有顺序依赖性且构建困难，所以为了可读性而组织规则，可能比为了速度而组织规则带来的收益更大。

除了通用的规则排序外，iptables 还支持用户自定义的规则列表，也称为链（chains），你可以利用它来优化防火墙规则。根据数据包头部中的值，将数据包从一个链传递到另一个链，提供了一种机制，可以仅将数据包针对 INPUT、OUTPUT 或 FORWARD 规则的一个子集进行测试，而不是针对列表中的每一条规则进行测试，直到找到匹配项为止。

基于这些特定的脚本，来自 NTP 时间服务器的入站数据包在未优化的防火墙脚本中必须对照众多入站规则进行测试，才能匹配其 ACCEPT 规则。使用用户自定义链来优化防火墙后，同一个入站数据包只需对照少得多的规则进行测试即可匹配其 ACCEPT 规则。再加上连接状态跟踪功能后，同一个入站数据包只需对照少数几条规则进行测试即可匹配其 ACCEPT 规则。

在用户自定义链中，规则用于在链之间传递数据包，同时定义数据包被接受或丢弃的条件。如果数据包未匹配用户自定义链中的任何规则，控制将返回到调用链。如果数据包未匹配顶级链选择规则，该数据包不会被传递到该链以对照该链的规则进行测试。数据包只需对照下一个链选择规则进行测试。

以下是使用用户自定义链优化后的第 5 章防火墙脚本：

```bash
#!/bin/sh

/sbin/modprobe ip_conntrack_ftp

CONNECTION_TRACKING="1"
ACCEPT_AUTH="0"
DHCP_CLIENT="0"
IPT="/sbin/iptables"                 # 你的系统上 iptables 的位置
INTERNET="eth0"                      # 连接互联网的接口
LOOPBACK_INTERFACE="lo"              # 根据你的系统命名而定
IPADDR="my.ip.address"               # 你的 IP 地址
SUBNET_BASE="network.address"        # ISP 网络段基地址
SUBNET_BROADCAST="directed.broadcast" # 网络段广播地址
MY_ISP="my.isp.address.range"        # ISP 服务器和网络运营中心（NOC）地址范围
NAMESERVER_1="isp.name.server.1"     # 远程域名服务器的地址
NAMESERVER_2="isp.name.server.2"     # 远程域名服务器的地址
NAMESERVER_3="isp.name.server.3"     # 远程域名服务器的地址
POP_SERVER="isp.pop.server"          # 远程 POP 服务器的地址
MAIL_SERVER="isp.mail.server"        # 远程邮件网关的地址
NEWS_SERVER="isp.news.server"        # 远程新闻服务器的地址
TIME_SERVER="some.time.server"       # 远程时间服务器的地址
DHCP_SERVER="isp.dhcp.server"        # 你的 ISP DHCP 服务器的地址
SSH_CLIENT="some,ssh,client"

LOOPBACK="127.0.0.0/8"               # 保留的回环地址范围
CLASS_A="10.0.0.0/8"                 # A 类私有网络
CLASS_B="172.16.0.0/12"             # B 类私有网络
CLASS_C="192.168.0.0/16"            # C 类私有网络
CLASS_D_MULTICAST="224.0.0.0/4"     # D 类组播地址
CLASS_E_RESERVED_NET="240.0.0.0/5"  # E 类保留地址
BROADCAST_SRC="0.0.0.0"             # 广播源地址
BROADCAST_DEST="255.255.255.255"    # 广播目的地址

PRIVPORTS="0:1023"                  # 知名、特权端口范围
UNPRIVPORTS="1024:65535"            # 非特权端口范围

NFS_PORT="2049"
LOCKD_PORT="4045"
SCKS_PORT="1080"
OPENWINDOWSD_PORT="2000"
XWINDOWD_PORTS="6000:6063"
SQUID_PORT="3128"

# traceroute 通常使用 -S 32769:65535 -D 33434:33523
TRACEROUTE_SRC_PORTS="32769:65535"
TRACEROUTE_DEST_PORTS="33434:33523"

USER_CHAINS="EXT-input EXT-output \
tcp-state-flags connection-tracking \
source-address-check destination-address-check \
local-dns-server-query remote-dns-server-response \
local-tcp-client-request remote-tcp-server-response \
remote-tcp-client-request local-tcp-server-response \
local-udp-client-request remote-udp-server-response \
local-dhcp-client-query remote-dhcp-server-response \
EXT-icmp-out EXT-icmp-in \
EXT-log-in EXT-log-out \
log-tcp-state*"

#####################################################
# 系统配置参数

# 启用广播回响保护
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts

# 禁用源路由数据包
for f in /proc/sys/net/ipv4/conf/*/accept_source_route; do
   echo 0 > $f
done

# 启用 TCP SYN Cookie 保护
echo 1 > /proc/sys/net/ipv4/tcp_syncookies

# 禁用 ICMP 重定向接收
for f in /proc/sys/net/ipv4/conf/*/accept_redirects; do
   echo 0 > $f
done

# 不发送重定向消息
for f in /proc/sys/net/ipv4/conf/*/send_redirects; do
   echo 0 > $f
done

# 丢弃通过接口进入的伪造数据包，如果回复这些数据包，
# 将会导致回复通过不同的接口发出。
for f in /proc/sys/net/ipv4/conf/*/rp_filter; do
   echo 1 > $f
done

# 记录具有不可能地址的数据包。
for f in /proc/sys/net/ipv4/conf/*/log_martians; do
   echo 1 > $f
done

#####################################################
# 初始化 iptables

# 从所有链中删除现有规则
$IPT --flush
$IPT -t nat --flush
$IPT -t mangle --flush
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X

$IPT --policy INPUT  ACCEPT
$IPT --policy OUTPUT ACCEPT

$IPT -A INPUT -i $INTERNET -p udp \
-s $DHCP_SERVER --sport 67 \
-d $IPADDR -dport 68 -j ACCEPT

# 拒绝定向广播
# 常用于网络映射和拒绝服务攻击
$iptables -A INPUT -i $INTERNET -d $SUBNET_BASE -j DROP
$iptables -A INPUT -i $INTERNET -d $SUBNET_BROADCAST -j DROP

# 拒绝受限广播
$iptables -A INPUT -i $INTERNET -d $BROADCAST_DEST -j DROP

fi

############################################################################
# ICMP 控制和状态消息

# 记录并丢弃初始的 ICMP 分片
$IPT -A INPUT -i $INTERNET --fragment -p icmp -j LOG \
--log-prefix "Fragmented ICMP: "

$IPT -A INPUT -i $INTERNET --fragment -p icmp -j DROP

$IPT -A INPUT -i $INTERNET -p icmp \
--icmp-type source-quench -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type source-quench -j ACCEPT

$IPT -A INPUT -i $INTERNET -p icmp \
--icmp-type parameter-problem -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type parameter-problem -j ACCEPT

$IPT -A INPUT -i $INTERNET -p icmp \
--icmp-type destination-unreachable -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type fragmentation-needed -j ACCEPT

# 不记录被丢弃的出站 ICMP 错误消息
$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type destination-unreachable -j DROP

# 中间 traceroute 响应
$IPT -A INPUT -i $INTERNET -p icmp \
      --icmp-type time-exceeded -d $IPADDR -j ACCEPT

# 允许向任何位置发送出站 ping
if [ "$CONNECTION_TRACKING" = "1" ]; then
   $IPT -A OUTPUT -o $INTERNET -p icmp \
      -s $IPADDR --icmp-type echo-request \
      -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p icmp \
    -s $IPADDR --icmp-type echo-request -j ACCEPT

$IPT -A INPUT -i $INTERNET -p icmp \
     --icmp-type echo-reply -d $IPADDR -j ACCEPT

# 允许来自可信主机的入站 ping
if [ "$CONNECTION_TRACKING" = "1" ]; then
   $IPT -A INPUT -i $INTERNET -p icmp \
     -s $MY_ISP --icmp-type echo-request -d $IPADDR \
     -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p icmp \
     -s $MY_ISP --icmp-type echo-request -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
     -s $IPADDR --icmp-type echo-reply -d $MY_ISP -j ACCEPT

#------------------------------------------------------------
# 记录被丢弃的数据包

# 不记录被丢弃的入站 echo-request
$IPT -A INPUT -i $INTERNET -p icmp \
     --icmp-type ! 8 -d $IPADDR -j LOG

$IPT -A INPUT -i $INTERNET -p tcp \
     -d $IPADDR -j LOG

$IPT -A OUTPUT -o $INTERNET -j LOG

exit 0
```

