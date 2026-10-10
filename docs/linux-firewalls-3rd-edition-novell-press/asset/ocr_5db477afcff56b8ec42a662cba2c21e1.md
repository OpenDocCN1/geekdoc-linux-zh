# CHAPTER 5: Firewall Optimization

The actual declaration in the firewall shell script would be as shown here:

```
```
USER_CHAINS="EXT-input
            tcp-state-flags
            source-address-check
            local-dns-server-query
            local-tcp-client-request
            remote-tcp-client-request
            local-udp-client-request
            local-dhcp-client-query
            EXT-icmp-out
            EXT-log-in
            log-tcp-state"            EXT-output \
            connection-tracking \
            destination-address-check \
            remote-dns-server-response \
            remote-tcp-client-response \
            local-tcp-server-response \
            remote-udp-server-response \
            remote-dhcp-server-response \
            EXT-icmp-in \
            EXT-log-out \
```
```

# Firewall Initialization

The firewall script starts out identically to the example in Chapter 4. Recall that a number of shell variables were set, including one called $IPT to define the location of the iptables firewall administration command:

```
```bash
#!/bin/sh

IPT="/sbin/iptables"           # Location of iptables on your system
INTERNET="eth0"               # Internet-connected interface
LOOPBACK_INTERFACE="lo"       # However your system names it
IPADDR="my.ip.address"        # your IP address
ISP="my_isp_address_range"    # ISP server & NOC address range
SUBNET_BASE="my.subnet.network"   # Your subnet's network address
SUBNET_BROADCAST="my.subnet.broadcast"   # Your subnet's broadcast address
LOOPBACK="127.0.0.8"         # reserved loopback address range
CLASS_A="10.0.0.0/8"        # class A private networks
CLASS_B="172.16.0.0/12"     # class B private networks
CLASS_C="192.168.0.0/16"    # class C private networks
CLASS_D_MULTICAST="224.0.0.0/4"   # class D multicast addresses
CLASS_E_RESERVED_NET="240.0.0.0/5"   # class E reserved networks
BROADCAST_SRC="0.0.0.0"     # broadcast source address
BROADCAST_DEST="255.255.255.255"   # broadcast destination address
PRIVPORTS="0:1023"          # well-known, privileged port range
UNPRIVPORTS="1024:65535"    # unprivileged port range
```
```

A number of kernel parameters were also set; refer to Chapter 4 for an explanation of these parameters:

```
```
# Enable broadcast echo Protection
 echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
# Disable Source Routed Packets
for f in /proc/sys/net/ipv4/conf/*/accept_source_route; do
```
```