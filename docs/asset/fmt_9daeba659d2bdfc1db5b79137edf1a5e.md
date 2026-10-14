
根据本章使用的示例，完整脚本应如下所示：

```sh
#!/bin/bash
PATH=$PATH:/bin:/usr/sbin:/bin:/usr/bin
export PATH
# Set up anti-spoofing
for f in /proc/sys/net/ipv4/conf/*/rp_filter; do echo 1 > $f; done
# Block input, output, and forward chains while firewall \
rules are being installed
iptables -A input -i ! lo -j DENY
iptables -A output -i ! lo -j DENY
iptables -A forward -j DENY
# Load protocol specific special masquerade modules
/sbin/modprobe -a
/sbin/modprobe ip_masq_ftp
/sbin/modprobe ip_masq_raudio
/sbin/modprobe ip_masq_irc
/sbin/modprobe ip_masq_quake ports=26000,27000,27910,27960
/sbin/modprobe ip_masq_cuseeme
/sbin/modprobe ip_masq_vdolive
# Make sure IP source forwarding is turned on
echo "1" > /proc/sys/net/ipv4/ip_forward
# Create user-defined chains
iptables -N prv-dmz
iptables -N dmz-priv
iptables -N ext-dmz
iptables -N priv-ext
iptables -N ext-priv
# Set up the user-defined chains to be called from the forward chain
iptables -A forward -s 10.0.0.0/255.0.0.0 -i eth2 -j priv-dmz
iptables -A forward -s 10.0.0.0/255.0.0.0 -i eth0 -j eth0
iptables -A forward -s 192.115.144.0/255.255.255.240 -i eth1 -j dmz-priv
iptables -A forward -s 192.115.144.0/255.255.255.240 -i eth0 -j ext-dmz
iptables -A forward -i eth2 -j ext-dmz
iptables -A forward -i eth1 -j ext-priv
# Log anything that doesn't match any of these
# This should never happen
iptables -A forward -j DENY -l
```
