
```sh
#!/bin/sh
#
# n 最后修改者为 Gerhard Mourani: 02-01-2000
#
# 版权所有 (C) 1997, 1998, 1999 Robert L. Ziegler
#
# 特此许可出于教育、研究、私人和非营利目的，
# 免费使用、复制、修改和发行此软件及其文档，
# 且无需书面协议。
# 本软件仅作为个人防火墙开发的示例和基础。
# 本软件不提供任何保证。
#
# Robert L. Ziegler 提供的任何材料均按“原样”提供。
# 他对任何事项均不提供任何形式的明示或隐含保证，
# 包括但不限于：对于特定用途的适用性、排他性或从使用该材料中获得结果的任何保证。
```

© 版权所有 1999-2000 Gerhard Mourani 和 Open Network Architecture ® 118

```sh
# 从 /etc/rc.d/init.d/firewall 调用。
# chconfig-:60 95
# 说明: 启动和停止 IPCHAINS 防火墙 \
# 用于提供防火墙网络服务。
```

```sh
# 引入函数库。
/etc/rc.d/init.d/functions
```

```sh
# 引入网络配置。
./etc/sysconfig/network
```

```sh
# 检查网络是否启动。
if [ "$RESERVED" = "no" ; then
  exit 0
fi

[ -f /sbin/ipchains ] || exit 0

# 我们是如何调用的。
case "$1" in
start)
  echo -n "Starting Firewall Services:"

# 为了便于维护的一些定义。
```

```sh
------------------------------------------------
# 根据你的系统和 ISP 修改这些内容。

EXTERNAL_INTERFACE="eth0" # 你使用的任何接口
LOOPBACK_INTERFACE="lo"
IPADDR="208.168.162.0"
ANYWHERE="any"
NAMESEMSERVER_1="mail.openarch.com"
NAMESEMSERVER_2="208.168.162.25"
```

```sh
# 主 DNS 服务器
# 副 DNS 服务器

SYSLOG_SERVER=" # 你的内部 syslog 服务器
SYSLOG_CLIENT="208.168.162.0/24" # 你的内部 syslog 客户端
```

```sh
LOOPBACK="127.0.0.1"
CLASS_A="10.0.0.0"
CLASS_B="172.16.0.0/12"
CLASS_C="192.168.0.0/16"
CLASS_D_MULTICAST="224.0.0.0/4"
CLASS_E_SERVED_NET="240.0.0.0/5"
BROADCAST_SRC="0.0.0.0"
BROADCAST_DST="255.255.255.255"
PRIVPORTS="0:1023"
UNPRIVPORTS="1024-65535"
```

```sh
------------------------------------------------
# SSH 从 123 开始，每增加并发入站连接
# 就向下递减到 513。
SSH_PORTS="1022:1023" # SSH 特权端口范围

# traceroute 使用 32769:65535
```

```sh
------------------------------------------------

# 默认策略为 DENY

```

关于本书的意见和建议请发送至 `gmourani@videotron.ca`

```bash

ipchains -A input - $EXTERNAL_INTERFACE -s 76.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 77.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 78.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 79.0.0.0/8 - DENY

# 80:01010000 / masks 80-95

ipchains -A input - $EXTERNAL_INTERFACE -s 80.0.0.0/4 - DENY

# 96:01100000 / masks 96-111

ipchains -A input - $EXTERNAL_INTERFACE -s 96.0.0.0/4 - DENY

# 126:01111111 / 3 127-need 112-126 spelled out

ipchains -A input - $EXTERNAL_INTERFACE -s 112.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 113.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 114.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 115.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 116.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 117.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 118.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 119.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 120.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 121.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 122.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 123.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 124.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 125.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 126.0.0.0/8 - DENY

# 217:11010101 / 2 includes 216-need 217-219 spelled out

ipchains -A input - $EXTERNAL_INTERFACE -s 217.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 218.0.0.0/8 - DENY

ipchains -A input - $EXTERNAL_INTERFACE -s 219.0.0.0/8 - DENY

# 223:10111111 / 6 masks 220-223

ipchains -A input - $EXTERNAL_INTERFACE -s 220.0.0.0/6 - DENY

```

```bash

#

# ICMP

# 为了防止基于 ICMP 过滤的拒绝服务攻击，

# 禁止入站重定向 (5) 和出站目的不可到达 (3)。

# 注意，不建议禁用目的不可到达 (3)，

# 因为它被用于协商数据包分片大小。

# 用于双向 ping：

# 消息类型：回显响应 (0), 回显请求 (8)

# 为了防止攻击，将源地址限制在您的 ISP 范围范围内。

# 用于出站 traceroute：

# 消息类型：入站目的不可到达 (3), 时间超时 (11)

# 默认 UDP 基础端口：33434 到基础端口+跳数-1

# 用于入站 traceroute：

# 消息类型：出站目的不可到达 (3), 时间超时 (11)

# 要阻止此操作，阻止出站 3 和 11

# 0: echo-reply (ping)

# 3: 目的不可到达、端口不可到达、分片需要、等。

# 4: 源猝制

# 5: 重定向

# 8: echo-request (ping)

# 11: time-expired
```
