
## Other OSes

```
# ifconfig fxp0                  # Check the "media" field on FreeBSD
# arp -a                         # Check the router (or host) ARP entry (all OS)
# ping cb.vu                      # The first thing to try...
# traceroute cb.vu                # Print the route path to destination
# ifconfig fxp0 media 100baseTX mediaopt full-duplex # 100Mbit full duplex (FreeBSD)
# netstat -s                      # System-wide statistics for each network protocol
```

Additional commands which are not always installed per default but easy to find:

```
# arping 192.168.16.254          # Ping on ethernet layer
# tcptraceroute -f 5 cb.vu       # uses tcp instead of icmp to trace through firewalls
```

## 4.2 Routing

### Print routing table

```
# route -n                       # Linux or use "ip route"
# netstat -rn                     # Linux, BSD and UNIX
# route print                     # Windows
```

### Add and delete a route

FreeBSD

```
# route add 212.117.0.0/16 192.168.1.1
# route delete 212.117.0.0/16
# route add default 192.168.1.1
```

Add the route permanently in /etc/rc.conf

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

Permanent entries are set in entry in /etc/defaultrouter.

Windows

```
# Route add 192.168.50.0 mask 255.255.255.0 192.168.51.253
# Route add 0.0.0.0 mask 0.0.0.0 192.168.51.254
```

Use add -p to make the route persistent.

## 4.3 Configure additional IP addresses

### Linux

```
# ifconfig eth0 192.168.50.254 netmask 255.255.255.0      # First IP
# ifconfig eth0:0 192.168.51.254 netmask 255.255.255.0     # Second IP
# ip addr add 192.168.50.254/24 dev eth0                   # Equivalent ip commands
# ip addr add 192.168.51.254/24 dev eth0 label eth0:1
```

### FreeBSD

```
# ifconfig fxp0 inet 192.168.50.254/24          # First IP
# ifconfig fxp0 alias 192.168.51.254 netmask 255.255.255.0  # Second IP
# ifconfig fxp0 -alias 192.168.51.254                     # Remove second IP alias
```

Permanent entries in /etc/rc.conf

```
ifconfig_fxp0="inet 192.168.50.254  netmask 255.255.255.0"
ifconfig_fxp0_alias0="192.168.51.254 netmask 255.255.255.0"
```

### Solaris

Check the settings with ifconfig -a

```
# ifconfig hme0 plumb                         # Enable the network card
# ifconfig hme0 192.168.50.254 netmask 255.255.255.0 up  # First IP
# ifconfig hme0:1 192.168.51.254 netmask 255.255.255.0 up  # Second IP
```

## 4.4 Change MAC address

Normally you have to bring the interface down before the change. Don't tell me why you want to change the MAC address...

```
# ifconfig eth0 down
# ifconfig eth0 hw ether 00:01:02:03:04:05      # Linux
# ifconfig fxp0 link 00:01:02:03:04:05           # FreeBSD
# ifconfig hme0 ether 00:01:02:03:04:05          # Solaris
# sudo ifconfig en0 ether 00:01:02:03:04:05      # Mac OS X Tiger
# sudo ifconfig en0 lladdr 00:01:02:03:04:05     # Mac OS X Leopard
```

Many tools exist for Windows. For example etherchange4. Or look for "Mac Makeup", "smac".

## 4.5 Ports in use

Listening open ports:

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

## 4.6 Firewall

Check if a firewall is running (typical configuration only):

### Linux

```
# iptables -L -n -v               # For status
Open the iptables firewall
# iptables -P INPUT   ACCEPT       # Open everything
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT  ACCEPT
# iptables -Z                         # Zero the packet and byte counters in all chains
# iptables -F                          # Flush all chains
# iptables -X                          # Delete all chains
```

### FreeBSD

```
# ipfw show                         # For status
# ipfw list 65535 # if answer is "65535 deny ip from any to any" the fw is disabled
# sysctl net.inet.ip.fw.enable=0     # Disable
# sysctl net.inet.ip.fw.enable=1     # Enable
```
