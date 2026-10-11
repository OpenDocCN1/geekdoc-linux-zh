
# WHOIS 客户端 (43)

```
ipchains -A tcp-s-i -p tcp \
      --source-port whois -j ACCEPT
```

# DNS TCP 客户端模式 (53)
协议允许在 UDP 请求失败时允许 TCP 客户端到服务器的请求。
这种情况非常罕见。

```
ipchains -A tcp-s-i -p tcp \
      -s $ANYWHERE domain -j ACCEPT
```

# 外部接口 - UDP 客户端输出链 (udp-c-o)
# UDP 对等转发模式 (53)

```
ipchains -A udp-c-o -p udp \
      --source-port domain \
      -d $DNS_SERVER -j ACCEPT
```

# 优化防火墙规则 417

# UDP 客户端模式 (53)

```
ipchains -A udp-c-o -p udp \
  --source-port $UNPRIVPORTS
  -d ANYWHERE -j ACCEPT
```

# NTP (23) - 访问远程时间服务器

```
ipchains -A udp-c-o -p udp \
  --source-port $UNPRIVPORTS
  -d $DNS_SERVER -j ACCEPT
```

# 外部接口 - 服务器输入链 (udp-s-i)
# UDP 对等转发模式 (53)

```
ipchains -A udp-c-o -p udp \
  -s $DNS_SERVER \
  --destination-port domain -j ACCEPT
```

# UDP 客户端模式 (53)

```
ipchains -A udp-s-i -p udp \
  -s $ANYWHERE \
  --destination-port $UNPRIVPORTS -j ACCEPT
```

# NTP (23) - 访问远程时间服务器

```
ipchains -A udp-s-i -p udp \
  -s $DNS_SERVER \
  --destination-port domain -j ACCEPT
```

# 外部接口 - 客户端输入链 (tcp-c-i -p tcp)
# HTTP 服务器 (80)
# 允许入站请求

```
ipchains -A tcp-c-i -p tcp \
  --destination-port http -j ACCEPT
```

# 435

# AUTH 服务器 (113)
# 允许入站请求

```
ipchains -A tcp-c-i -p tcp \
    --destination-port auth -j ACCEPT
```

# 特权端口 避免避免管理问题。入站连接

```
ipchains -A tcp-c-i -p tcp -y \
    --destination-port $UNPRIVPORTS -j DENY
```

# SOCKS 入站连接

```
ipchains -A tcp-c-i -p tcp -y \
    --destination-port $SOCKS_PORT -j DENY
```

# NFS 连接

```
ipchains -A tcp-c-i -p tcp -y \
    --destination-port $NFS_PORT -j DENY
```

# 外部接口 - 服务器输出链 (tcp-s-o -p tcp)
# HTTP (80)
# 允许入站请求

```
ipchains -A tcp-s-o -p tcp \
    --source-port http -j ACCEPT
```

# AUTH (113)
# 允许入站请求

```
ipchains -A tcp-s-o -p tcp \
    --source-port auth -j ACCEPT
```

# 优化防火墙规则 419

# 外部接口 - 杂项输出链 (misc-out)

# SSH 客户端 (22) - 允许客户端访问远程 SSH 服务器

```
ipchains -A misc-out -p tcp \
    --source-port $SSH_PORTS \
    --destination-port ssh -j ACCEPT
```

# 追踪路由
# 允许向任何地方发出追踪路由请求

```
ipchains -A misc-out -p udp \
    --source-port $TRACOUTE_SRC_PORTS \
    --destination-port $TRACOUTE_DEST_PORTS -j ACCEPT
```

# 允许来自 ISP 的入站追踪路由请求
# (3) 目的不可达，最终追踪响应
# (11) 超时，中间追踪响应

```
ipchains -A misc-out -p icmp \
    --icmp-type port-unreachable -d $MY_ISP -j ACCEPT
```

```
ipchains -A misc-out -p icmp \
    --icmp-type time-exceeded -d $MY_ISP -j ACCEPT
```

# PING

# 允许向信任主机发送回包

```
ipchains -A misc-out -p icmp \
    --icmp-type echo-reply -d $MY_ISP -j ACCEPT
```

# 外部接口 - 杂项输入链 (misc-in)

# SSH 客户端 (22) - 允许客户端访问远程 SSH 服务器

```
ipchains -A misc-in -p tcp -j y \
    --source-port ssh \
    --destination-port $SSH_PORTS -j ACCEPT
```

# 420 录 B 防火墙示例和支持脚本

# FTP (20, 21) - 允许客户端访问远程 FTP 服务器

# 正常端口 FTP 数据通道

```
ipchains -A misc-in -p tcp \
  --source-port ftp-data \
  --destination-port $UNPRIVPORTS -j ACCEPT
```

# NFS: UDP 连接

```
ipchains -A misc-in -p udp \
  --destination-port $NFS_PORT -j DENY -1
```

# 追踪路由

# 启用来自 ISP 的入站追踪路由请求

```
ipchains -A misc-in -p udp \
  -s $MY_ISP $TRACEROUTE_SRC_PORTS \
  --destination-port $TRACEROUTE_DEST_PORTS -j ACCEPT
```

# PING

# 允许来自信任主机的入站 ping

```
ipchains -A misc-in -p icmp \
  -s $MY_ISP cho echo-request -j ACCEPT
```

# 入站 ICMP 链

```
ipchains -A icmp-in -p icmp --icmp-type echo-reply -j ACCEPT
ipchains -A icmp-in -p icmp --icmp-type destination-unreachable -j ACCEPT
ipchains -A icmp-in -p icmp --icmp-type source-quench -j ACCEPT
ipchains -A icmp-in -p icmp --icmp-type time-exceeded -j ACCEPT
ipchains -A icmp-in -p icmp --icmp-type parameter-problem -j ACCEPT
```

# 出发 ICMP 链
