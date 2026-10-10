```
$IPT -A INPUT -i $INTERNET -p udp \
-s $DHCP_SERVER --sport 67 \
-d $IPADDR -dport 68 -j ACCEPT
```

```
# Refuse directed broadcasts
# Used to map networks and for Denial of Service attacks
$iptables -A INPUT -i $INTERNET -d $SISUBNET_BASE -j DROP
$iptables -A INPUT -i $INTERNET -d $SUBNET_BROADCAST -j DROP
```

```
# Refuse limited broadcasts
$iptables -A INPUT -i $INTERNET -d $BROADCAST_DEST -j DROP
```

```
fi
```

```
############################################################################
# ICMP Control and Status Messages
```

```
# Log and drop initial ICMP fragments
$IPT -A INPUT -i $INTERNET --fragment -p icmp -j LOG \
--log-prefix "Fragmented ICMP: "

$IPT -A INPUT -i $INTERNET --fragment -p icmp -j DROP

$IPT -A INPUT -i $INTERNET -p icmp \
--icmp-type source-quench -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type source-quench -j ACCEPT
```

```
$IPT -A INPUT -i $INTERNET -p icmp \
--icmp-type parameter-problem -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type parameter-problem -j ACCEPT

$IPT -A INPUT -i $INTERNET -p icmp \
--icmp-type destination-unreachable -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type fragmentation-needed -j ACCEPT
```

```
# Don't log dropped outgoing ICMP error messages
$IPT -A OUTPUT -o $INTERNET -p icmp \
-s $IPADDR --icmp-type destination-unreachable -j DROP
```