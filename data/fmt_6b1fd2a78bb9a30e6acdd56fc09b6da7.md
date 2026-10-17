
# ethtool eth0                         # Show the ethernet status (replaces mii-diag)
# ethtool -s eth0 speed 100 duplex full # Force 100Mbit Full duplex
# ethtool -s eth0 autoneg off          # Disable auto negotiation
# ethtool -p eth1                       # Blink the ethernet led - very useful when supported
# ip link show                          # Display all interfaces on Linux (similar to ifconfig)
# ip link set eth0 up                   # Bring device up (or down). Same as "ifconfig eth0 up"
# ip addr show                          # Display all IP addresses on Linux (similar to ifconfig)
# ip neigh show                         # Similar to arp -a

## 其他操作系统

```
# ifconfig fxp0                  # Check the "media" field on FreeBSD
# arp -a                         # Check the router (or host) ARP entry (all OS)
# ping cb.vu                      # The first thing to try...
# traceroute cb.vu                # Print the route path to destination
# ifconfig fxp0 media 100baseTX mediaopt full-duplex # 100Mbit full duplex (FreeBSD)
# netstat -s                      # System-wide statistics for each network protocol
```

默认情况下并非总是安装但易于找到的附加命令：

```
# arping 192.168.16.254          # Ping on ethernet layer
# tcptraceroute -f 5 cb.vu       # uses tcp instead of icmp to trace through firewalls
```

### 4.2 路由

#### 打印路由表

```
# route -n                       # Linux or use "ip route"
# netstat -rn                     # Linux, BSD and UNIX
# route print                     # Windows
```

#### 添加和删除路由

FreeBSD

```
# route add 212.117.0.0/16 192.168.1.1
# route delete 212.117.0.0/16
# route add default 192.168.1.1
```

在 `/etc/rc.conf` 中永久添加路由

```
static_routes="myroute"
route_myroute="-net 212.117.0.0/16 192.168.1.1"
```

Linux

```
# route add -net 192.168.20.0 netmask 255.255.255.0 gw 192.168.16.254
# ip route add 192.168.20.0/24 via 192.168.16.254      # same as above with ip route
# route add -net 192.168.20.0 netmask 255.255.255.0 dev eth0
# route add default gw 192.168.51.254
# ip route add default via 192.168.51.254 dev eth0     # same as above with ip route
# route delete -net 192.168.20.0 netmask 255.255.255.0
```

Solaris

```
# route add -net 192.168.20.0 -netmask 255.255.255.0 192.168.16.254
# route add default 192.168.51.254 1                   # 1 = hops to the next gateway
# route change default 192.168.50.254 1
```

永久条目设置在 `/etc/defaultrouter` 中的条目。

Windows

```
# Route add 192.168.50.0 mask 255.255.255.0 192.168.51.253
# Route add 0.0.0.0 mask 0.0.0.0 192.168.51.254
```

使用 `add -p` 使路由持久化。

### 4.3 配置附加 IP 地址

#### Linux

```
# ifconfig eth0 192.168.50.254 netmask 255.255.255.0      # First IP
# ifconfig eth0:0 192.168.51.254 netmask 255.255.255.0     # Second IP
# ip addr add 192.168.50.254/24 dev eth0                   # Equivalent ip commands
# ip addr add 192.168.51.254/24 dev eth0 label eth0:1
```

#### FreeBSD

```
# ifconfig fxp0 inet 192.168.50.254/24          # First IP
# ifconfig fxp0 alias 192.168.51.254 netmask 255.255.255.0  # Second IP
# ifconfig fxp0 -alias 192.168.51.254                     # Remove second IP alias
```

`/etc/rc.conf` 中的永久条目

```
ifconfig_fxp0="inet 192.168.50.254  netmask 255.255.255.0"
ifconfig_fxp0_alias0="192.168.51.254 netmask 255.255.255.0"
```

#### Solaris

使用 `ifconfig -a` 检查设置

```
# ifconfig hme0 plumb                         # Enable the network card
# ifconfig hme0 192.168.50.254 netmask 255.255.255.0 up  # First IP
# ifconfig hme0:1 192.168.51.254 netmask 255.255.255.0 up  # Second IP
```

### 4.4 修改 MAC 地址

通常你必须在更改前将接口关闭。不要告诉我你为什么想更改 MAC 地址...

```
# ifconfig eth0 down
# ifconfig eth0 hw ether 00:01:02:03:04:05      # Linux
# ifconfig fxp0 link 00:01:02:03:04:05           # FreeBSD
# ifconfig hme0 ether 00:01:02:03:04:05          # Solaris
# sudo ifconfig en0 ether 00:01:02:03:04:05      # Mac OS X Tiger
# sudo ifconfig en0 lladdr 00:01:02:03:04:05     # Mac OS X Leopard
```

Windows 上存在许多工具。例如 `etherchange4`。或查找 "Mac Makeup"、"smac"。

### 4.5 使用中的端口

正在监听的开放端口：
