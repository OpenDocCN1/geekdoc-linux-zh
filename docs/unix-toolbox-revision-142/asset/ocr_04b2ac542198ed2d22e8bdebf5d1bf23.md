# 4.7 IP Forward for routing

Linux

Check and then enable IP forward with:

```
# cat /proc/sys/net/ipv4/ip_forward   # Check IP forward 0=off, 1=on
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

or edit /etc/sysctl.conf with:

```
net.ipv4.ip_forward = 1
```

FreeBSD

Check and enable with:

```
# sysctl net.inet.ip.forwarding      # Check IP forward 0=off, 1=on
# sysctl net.inet.ip.forwarding=1
# sysctl net.inet.ip.fastforwarding=1      # For dedicated router or firewall
Permanent with entry in /etc/rc.conf:
gateway_enable="YES"      # Set to YES if this host will be a gateway.
```

Solaris

```
# ndd -set /dev/ip ip_forwarding 1   # Set IP forward 0=off, 1=on
```

# 4.8 NAT Network Address Translation

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

Delete the port forward with -D instead of -A. The program netstat-nat⁵ is very useful to track connections (it uses /proc/net/ip_conntrack or /proc/net/nf_conntrack).

```
# netstat-nat -n      # show all connections with IPs
```

```
# natd -s -m -u -dynamic -f /etc/natd.conf -n fxp0
Or edit /etc/rc.conf with:
firewall_enable="YES"      # Set to YES to enable firewall functionality
firewall_type="open"      # Firewall type (see /etc/rc.firewall)
natd_enable="YES"      # Enable natd (if firewall_enable == YES).
natd_interface="tun0"      # Public interface or IP address to use.
natd_flags="-s -m -u -dynamic -f /etc/natd.conf"
```

Port forward with:

```
# cat /etc/natd.conf
same_ports yes
use_sockets yes
unregistered_only
# redirect_port tcp insideIP:2300-2399 3300-3399  # port range
redirect_port udp 192.168.51.103:7777 7777
```

# 4.9 DNS

On Unix the DNS entries are valid for all interfaces and are stored in /etc/resolv.conf. The domain to which the host belongs is also stored in this file. A minimal configuration is: