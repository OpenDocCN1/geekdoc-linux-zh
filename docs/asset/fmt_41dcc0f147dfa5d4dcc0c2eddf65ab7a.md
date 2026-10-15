
```
# netstat -an | grep LISTEN
# lsof -i                # Linux list all Internet connections
# socklist               # Linux display list of open sockets
# sockstat -4            # FreeBSD application listing
# netstat -anp --udp --tcp | grep LISTEN   # Linux
# netstat -tup           # List active connections to/from system (Linux)
# netstat -tupi          # List listening ports from system (Linux)
# netstat -ano            # Windows
```

### 4.6 防火墙

检查防火墙是否正在运行（典型配置）：

#### Linux

```
# iptables -L -n -v               # For status
```
打开 `iptables` 防火墙
```
# iptables -P INPUT   ACCEPT       # Open everything
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT  ACCEPT
# iptables -Z                         # Zero the packet and byte counters in all chains
# iptables -F                          # Flush all chains
# iptables -X                          # Delete all chains
```

#### FreeBSD

```
# ipfw show                         # For status
# ipfw list 65535 # if answer is "65535 deny ip from any to any" the fw is disabled
# sysctl net.inet.ip.fw.enable=0     # Disable
# sysctl net.inet.ip.fw.enable=1     # Enable
```

### 4.7 IP 转发用于路由

Linux

检查并启用 IP 转发：

```
# cat /proc/sys/net/ipv4/ip_forward   # Check IP forward 0=off, 1=on
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

或编辑 `/etc/sysctl.conf`：

```
net.ipv4.ip_forward = 1
```

FreeBSD

检查并启用：

```
# sysctl net.inet.ip.forwarding      # Check IP forward 0=off, 1=on
# sysctl net.inet.ip.forwarding=1
# sysctl net.inet.ip.fastforwarding=1      # For dedicated router or firewall
```

永久生效请在 `/etc/rc.conf` 中添加条目：

```
gateway_enable="YES"      # Set to YES if this host will be a gateway.
```

Solaris

```
# ndd -set /dev/ip ip_forwarding 1   # Set IP forward 0=off, 1=on
```

### 4.8 NAT 网络地址转换

Linux

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE      # to activate NAT
# iptables -t nat -A PREROUTING -p tcp -d 78.31.70.238 --dport 20022 -j DNAT \
--to 192.168.16.44:22      # Port forward 20022 to internal IP port ssh
# iptables -t nat -A PREROUTING -p tcp -d 78.31.70.238 --dport 993:995 -j DNAT \
--to 192.168.16.254:993-995      # Port forward of range 993-995
# ip route flush cache
# iptables -L -t nat      # Check NAT status
```

使用 `-D` 代替 `-A` 删除端口转发。程序 `netstat-nat`⁵ 非常有用，可以追踪连接（它使用 `/proc/net/ip_conntrack` 或 `/proc/net/nf_conntrack`）。

```
# netstat-nat -n      # show all connections with IPs
```

```
# natd -s -m -u -dynamic -f /etc/natd.conf -n fxp0
```

或编辑 `/etc/rc.conf`：

```
firewall_enable="YES"      # Set to YES to enable firewall functionality
firewall_type="open"      # Firewall type (see /etc/rc.firewall)
natd_enable="YES"      # Enable natd (if firewall_enable == YES).
natd_interface="tun0"      # Public interface or IP address to use.
natd_flags="-s -m -u -dynamic -f /etc/natd.conf"
```

端口转发配置：

```
# cat /etc/natd.conf
same_ports yes
use_sockets yes
unregistered_only
# redirect_port tcp insideIP:2300-2399 3300-3399  # port range
redirect_port udp 192.168.51.103:7777 7777
```

### 4.9 DNS

在 Unix 上，DNS 条目对所有接口有效，并存储在 `/etc/resolv.conf` 中。主机所属的域也存储在此文件中。最小配置如下：

`nameserver 78.31.70.238`

`search sleepyowl.net intern.lab`

`domain sleepyowl.net`

使用以下命令检查系统域名：

```
# hostname -d          # Same as dnsdomainname
```

### Windows

在 Windows 上，DNS 按接口配置。要显示已配置的 DNS 并刷新 DNS 缓存，请使用：

```
# ipconfig /?
# ipconfig /all
```

#### 刷新 DNS

刷新操作系统的 DNS 缓存，部分应用程序使用自己的缓存（例如 Firefox）不受影响。

```
# /etc/init.d/nscd restart    # Restart nscd if used - Linux/BSD/Solaris
# lookupd -flushcache          # OS X Tiger
# dscacheutil -flushcache      # OS X Leopard and newer
# ipconfig /flushdns           # Windows
```

#### 转发查询

`Dig` 是测试 DNS 设置的好帮手。例如公共 DNS 服务器 `213.133.105.2` `ns.second-ns.de` 可用于测试。查看客户端从哪个服务器接收到响应（简化答案）。

```
# dig sleepyowl.net
sleepyowl.net.      600  IN  A     78.31.70.238
;; SERVER: 192.168.51.254#53(192.168.51.254)
```

路由器 `192.168.51.254` 作出了响应，响应为 A 记录。任何记录都可以查询，并且可以使用 `@` 指定 DNS 服务器：
