

## 以下是主要要点：

- 在此情况下，满足条件时值为零。
- 在此情况下，满足条件时值非零。
- 在此情况下，满足条件时值为零。

以下是主要思想的描述：

- 条件 1 导致结果 A。
- 条件 2 导致结果 B。
- 条件 3 导致结果 C。

关键在于主要思想是解释的核心。

以下是主要思想的描述：

- 条件 1 导致结果 A。
- 条件 2 导致结果 B。
- 条件 3 导致结果 C。

# 第四部分

## 附录

- A. 安全资源
- B. 防火墙示例和支持脚本
- C. VPN（虚拟专用网络）
- D. 术语表

# 附录 A

## 安全资源

本附录列出了当前互联网上一些常见的安全相关通知、信息、工具、更新和补丁的来源。虽然还有更多网站，且每天都有新网站出现——请将该列表视为起点，而非完整列表。该附录也作为本书的一般参考部分。

## 安全信息来源

各种安全信息、通知和警报、白皮书、教程等，可以在以下来源中找到：

- BugTraq：http://www.securityfocus.com/archive/1
- CERT 协调中心：http://www.cert.org/
- CIAC（计算机事件咨询能力中心）：http://www.ciac.org/ciac/
- Freshmeat：http://www.freshmeat.net/
- Geektools：http://www.geektools.com/
- 互联网工程任务组（IETF）：http://www.ietf.org/
- Packet Storm：http://packetstormsecurity.org/
- RFC 编辑：http://www.rfc-editor.org/
- SANS 研究所：http://www.sans.org/
- Security Focus：http://www.securityfocus.com/

## 参考论文和常见问题解答

一些有用的参考论文（其中一些在书中被引用）可以在这些网站找到：

- “帮助抵御拒绝服务攻击：逐步指南”：http://www.sans.org/dosstep/index.php
- “互联网防火墙常见问题解答”：http://www.interhack.net/pubs/fwfaq/
- “TCP SYN 泛洪和 IP 欺骗攻击”（CERT 公告 CA-96.21）：http://www.cert.org/advisories/CA-1996-21.html
- “TCP/UDP 服务端口号”（IANA）：http://www.iana.org/assignments/port-numbers
- “UDP 端口拒绝服务攻击”（CERT 公告 CA-1996.01）：http://www.cert.org/advisories/CA-1996-01.html

## 书籍

- *《构建互联网防火墙（第二版）》*，作者 Elizabeth D. Zwicky、Simon Cooper 和 D. Brent Chapman。O'Reilly & Associates, Inc.
- *《入侵签名与分析》*，作者 Stephen Northcutt、Mark Cooper、Matt Fearnou 和 Karen Frederick。New Riders Publishing。
- *《网络入侵检测：分析师手册（第三版）》*，作者 Stephen Northcutt 和 Judy Novak。New Riders Publishing。
- *《实用 Unix 和互联网安全》*，作者 Simson Garfinkel 等。O'Reilly & Associates, Inc.
- *《TCP/IP 详解（第一卷：协议）》*，作者 W. Richard Stevens。Addison-Wesley Professional。

# 附录 B

## 防火墙示例和支持脚本

第 4 章“构建和安装独立防火墙”描述了一个针对独立系统的防火墙。第 5 章“防火墙优化”对该独立示例进行了优化。第 6 章“数据包转发”扩展了该示例，使其能够作为网关或瓶颈防火墙运行，并在外部公共接口和内部本地网络接口上应用完整的防火墙规则集。网关作为互联网和包含公共服务器的 DMZ（非军事区）网络之间的链接。瓶颈防火墙作为私有 LAN（局域网）和 DMZ 之间的链接。

示例防火墙在第 4、5 和 6 章中分段呈现。本附录按照防火墙脚本中实际显示的方式呈现相同的防火墙示例。

## 第 4 章中独立系统的 iptables 防火墙

第 4 章涵盖了独立 Linux 机器上最可能使用的服务类型的应用协议和防火墙规则。此外，对于并非所有人都使用的服务，也提供了客户端和服务器规则。完整的 iptables 防火墙脚本（如显示在 /etc/rc.d/rc.firewall 或 /etc/init.d/firewall 中）如下所示：

```bash
#!/bin/sh

/sbin/modprobe ip_conntrack_ftp
```

```bash
CONNECTION_TRACKING= *1*
ACCEPT_AUTH=*0*
SSH_SERVER=*0*
FTP_SERVER=*0*
WEB_SERVER=*0*
SSL_SERVER=*0*
DHCP_CLIENT=*1*
```

```bash
IPT=* /sbin/iptables * # 系统中 iptables 的位置
INTERNET=*eth0* # 连接互联网的接口
LOOPBACK_INTERFACE=*lo* # 无论系统如何命名
IPADDR=*my.ip.address* # 你的 IP 地址
SUBNET_BASE=*my.subnet.base* # ISP 网络段基地址
SUBNET_BROADCAST=*my.subnet.bcast* # 网络段广播地址
MY_ISP=*my.isp.address.range* # ISP 服务器和网络运营中心地址范围
```

```bash
NAMESERVER=*isp.name.server* # 远程名称服务器地址
POP_SERVER=*isp.pop.server* # 远程 pop 服务器地址
MAIL_SERVER=*isp.mail.server* # 远程邮件网关地址
NEWS_SERVER=*isp.news.server* # 远程新闻服务器地址
TIME_SERVER=*some.time.server* # 远程时间服务器地址
DHCP_SERVER=*isp.dhcp.server* # 你的 ISP dhcp 服务器地址
```

```bash
LOOPBACK=*127.0.0.0/8* # 保留的环回地址范围
CLASS_A=*10.0.0.0/8* # A 类私有网络
CLASS_B=*172.16.0.0/12* # B 类私有网络
CLASS_C=*192.168.0.0/16* # C 类私有网络
CLASS_D_MULTICAST=*224.0.0.0/4* # D 类多播地址
CLASS_E_RESERVED_NET=*240.0.0.0/5* # E 类保留地址
BROADCAST_SRC=*0.0.0.0* # 广播源地址
BROADCAST_DEST=*255.255.255.255* # 广播目标地址
```

```bash
PRIVPORTS=*0:1023* # 知名、特权端口范围
UNPRIVPORTS=*1024:65535* # 非特权端口范围
```

```bash
SSH_PORTS=*1024:65535*
```

```bash
NFS_PORT=*2049*
LOCKD_PORT=*4045*
SOCKS_PORT=*1080*
OPENWINDOWS_PORT=*2000*
XWINDOW_PORTS=*6000:6063*
SQLID_PORT=*3128*
```

```bash
############################################################################

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

# 丢弃从接口进入的欺骗数据包，如果回复，
# 会导致回复从不同的接口发出。
for f in /proc/sys/net/ipv4/conf/*/rp_filter; do
  echo 1 > $f
done

# 记录具有不可能地址的数据包。
for f in /proc/sys/net/ipv4/conf/*/log_martians; do
  echo 1 > $f
done

############################################################################

# 删除所有链中的现有规则
$IPT --flush
$IPT -t nat --flush
$IPT -t mangle --flush
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X
$IPT --policy INPUT   ACCEPT
$IPT --policy OUTPUT  ACCEPT
$IPT --policy FORWARD ACCEPT

```

```bash
$IPT -t nat --policy PREROUTING ACCEPT
$IPT -t nat --policy OUTPUT ACCEPT
$IPT -t nat --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PREROUTING ACCEPT
$IPT -t mangle --policy OUTPUT ACCEPT
if [ "$1" = "stop" ]
then
	echo '防火墙已完全停止！警告：此主机没有正在运行的防火墙。'
	exit 0
fi

# 在环回接口上允许无限制流量
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT

# 将默认策略设置为丢弃
$IPT --policy INPUT DROP
$IPT --policy OUTPUT DROP
$IPT --policy FORWARD DROP

$IPT -t nat --policy PREROUTING DROP
$IPT -t nat --policy OUTPUT DROP
$IPT -t nat --policy POSTROUTING DROP

$IPT -t mangle --policy PREROUTING DROP
$IPT -t mangle --policy OUTPUT DROP

#######################################################
# 隐蔽扫描和 TCP 状态标志
```

```bash
# 不干净的包
$IPT -A INPUT -m unclean -j DROP
# 所有位都清零
$IPT -A INPUT -p tcp --tcp-flags ALL NONE -j DROP
# SYN 和 FIN 都置位
$IPT -A INPUT -p tcp --tcp-flags SYN,FIN SYN,FIN -j DROP
# SYN 和 RST 都置位
$IPT -A INPUT -p tcp --tcp-flags SYN,RST SYN,RST -j DROP
# FIN 和 RST 都置位
$IPT -A INPUT -p tcp --tcp-flags FIN,RST FIN,RST -j DROP
# 仅 FIN 位置位，没有预期的伴随 ACK
$IPT -A INPUT -p tcp --tcp-flags ACK,FIN FIN -j DROP
# 仅 PSH 位置位，没有预期的伴随 ACK
$IPT -A INPUT -p tcp --tcp-flags ACK,PSH PSH -j DROP
# 仅 URG 位置位，没有预期的伴随 ACK
$IPT -A INPUT -p tcp --tcp-flags ACK,URG URG -j DROP
```

