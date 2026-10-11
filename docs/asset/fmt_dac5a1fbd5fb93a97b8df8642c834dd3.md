
```
ipfwadm -O -a accept -P tcp             -W $EXTERNAL_INTERFACE \
  -S $IPADDR $UNPRIVPORTS \
  -D ANYWHERE $UNPRIVPORTS
```

# 正常端口模式 FTP 数据通道

```
ipfwadm -O -a accept -P tcp -k -W $EXTERNAL_INTERFACE \
  -S $IPADDR $UNPRIVPORTS \
  -D ANYWHERE 20
```

# NTP (123) - 访问远程网络时间服务器

```
ipfwadm -O -a accept -P udp -W $EXTERNAL_INTERFACE \
  -S $IPADDR $UNPRIVPORTS \
  -D <my.time.provider> 123
```

```
ipfwadm -I -a accept -P udp -W $EXTERNAL_INTERFACE \
  -S <my.time.provider> 123 \
  -D $IPADDR $UNPRIVPORTS
```

# 路由追踪 (TRACEROUT)

## 启用出站路由追踪请求

```
ipfwadm -O a accept -P udp -W EXTERNAL_INTERFACE \
  -S $IPADDR TRACEROUTE_SRC_PORTS \
  -O ANYWHERE TRACEROUTE_DEST_PORTS
```

## 启用来自 ISP 的入站路由追踪请求

```
ipfwadm -I a accept -P udp -W EXTERNAL_INTERFACE \
  -S $MY_ISP TRACEROUTE_SRC_PORTS \
  -D $IPADDR TRACEROUTE_DEST_PORTS
```

# (11) 超超时 (Time_Exceeded)

## 出站超时条件，

```
ipfwadm -O a accept -P icmp -W EXTERNAL_INTERFACE \
  -S $IPADDR 11 -O $MY_ISP
```

# PING

## 允许来自信任主机的入站 ping

```
ipfwadm -I a accept -P icmp -W EXTERNAL_INTERFACE \
  -S $MY_ISP 8 -D $IPADDR
```

```
ipfwadm -O a accept -P icmp -W EXTERNAL_INTERFACE \
  -S $IPADDR 0 -D $MY_ISP
```

# DNS TCP 客户端模式 (53)

## 协议允许 TCP 客户端到服务器的请求

## 当 UDP 请求失败时。这种情况很少见。

```
ipfwadm -I a accept -P tcp -k -W EXTERNAL_INTERFACE \
  -S ANYWHERE 53 \
  -D $IPADDR $UNPRIVPORTS
```

```
ipfwadm -O a accept -P tcp -W EXTERNAL_INTERFACE \
  -S $IPADDR $UNPRIVPORTS \
  -D ANYWHERE 53
```

```
echo "done"

exit 0
```

# 使用用户定义链优化 ipchains

除了常规的规则排序外，`ipchains` 还支持用户定义的规则列表（或称为“链”），你可以使用它们来优化防火墙规则。根据数据包报头中的值将数据包从一个链传递到另一个链，提供了一种选择性地针对输入、输出或转发规则子集测试数据包的方法，而不是对列表中的每个规则进行测试直到找到匹配项。

例如，使用未优化的防火墙脚本，来自 NTP 时间服务器的入站包必须经过大约 40 条入站规则的测试才能匹配其 ACCEPT 规则。使用用户定义链优化防火墙，同一个入站包在匹配其 ACCEPT 规则之前只需测试大约 15 条规则。

在 `ipchains` 中，规则用于在链之间传递数据包，并定义数据包在什么条件下被接受或拒绝。如果数据包不匹配用户定义链中的任何规则，控制权将返回调用链。如果数据包不匹配选择规则，则数据包将不会传递到该链进行链规则的测试。数据包将直接对下一个链选择规则进行测试。

以下是经过 `ipchains` 优化后的之前的防火墙脚本：

```
#!/bin/sh

echo 'Starting firewalling... ' 

# 为了便于维护的某些定义。

# 请根据你的系统和 ISP 修改这些内容。

EXTERNAL_INTERFACE="eth0"
LAN_="eth1"
LOOPBACK_INTERFACE="lo"

IPADDR="my.ip.address"
LAN_IPADDR="192.168.1.1"
LAN_ADDRESS="192.168.1.0/24"

WHERE="any/0"

MY_ISP="my.isp.address.range"
NAMESERVER1="my.name.server.1"

SMTP_SERVER="any/0"
SMTP_GATEWAY="my.smtp.server"
POP_SERVER="my.pop.server"
NEWS_SERVER="my.news.server"
WEB_PROXY_SERVER="my.www.proxy"
WEB_PROXY_PORT="www.proxy"

# 连接互联网的
# 连接局域网
# 或本地命名约定

# 公共 IP 地址
# 内部接口
# 匹配任何 IP 地址

# ISP 范围
# 每个人至少有一个

# 外部服务器
# 外部中继
# 外部 pop 服务器，如果任何
# 外部新闻服务器，如果任何
# 外部 代理服务器，如果任何
# 通常为 8000 或 8080
## 附录 B 示例

```

LOOPBACK="127.0.0.0/8"

CLASS_A="10.0.0.0/8"

CLASS_B="172.16.0.0/12"

CLASS_C="192.168.0.0/16"

CLASS_D_MULTICAST="224.0.0.0/4"

BROADCAST_SRC="0.0.0.0"

BROADCAST_DEST="255.255.255"

PORTS="1:1023"

PRIVILEGED_PORTS="1024:65535"

TRACEROUT_SRC_PORTS="32769:65535"

TRACEROUT_DEST_PORTS="3343:33523"

SOCKS_PORTS="1080"

OPENWINDOW_PORTS="2048"

NFS_PORTS="2049"

# 回环地址范围

# A 类私有网络

# B 类私有网络

# C 类私有网络

# D 类组播地址

# 广播源

# 广播目的

# 良知端口范围

# 非权限端口范围

# (TCP) socks

# (TCP) 窗口

# (TCP/UDP) NFS

# 修改这些以匹配服务器或连接

# 支持。

WINDOW_PORTS="6000"

# (TCP) 窗口

SSH_PORTS="1024:1823"

# 同步连接

# 启用 TCP Syn Cookie 保护

echo 1 >/proc/sys/ipv4/tcp_syncookies

# 启用 IP 伪装防护

# 开启源验证

for f in /proc/sys/ipv4/conf/rp_filter; do

echo 1 > $f

done

# 禁用 ICMP 重定向

for f in /proc/sys/ipv4/conf/accept_redirect; do

echo 0 > $f

done

# 禁用源路由

for f in /proc/sys/ipv4/conf/accept_source; do

echo 0 > $f

done

# 清空所有链中的现有规则

ipchains -F

ipchains -F spoofed

ipchains -F tcp-c-o

ipchains -F tcp-s-i

ipchains -F udp-c-o

ipchains -F udp-s-i

ipchains -F tcp-c-i

ipchains -F tcp-s-o

ipchains -F misc-out

ipchains -F misc-in

ipchains -F icmp-in

ipchains -F icmp-out

ipchains -F log-in

ipchains -F log-out

ipchains -X spoofed

ipchains -X tcp-c-o

ipchains -X tcp-s-i

ipchains -X udp-c-o

ipchains -X udp-s-i

ipchains -X tcp-c-i

ipchains -X tcp-s-o

ipchains -X misc-out

ipchains -X misc-in

ipchains -X icmp-in

ipchains -X icmp-out
