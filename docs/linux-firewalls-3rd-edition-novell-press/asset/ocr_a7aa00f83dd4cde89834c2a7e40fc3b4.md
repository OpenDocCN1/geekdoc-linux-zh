```
$IPT -A FORWARD -p icmp \
--icmp-type fragmentation-needed -j ACCEPT

# Don't log dropped outgoing ICMP error messages
$IPT -A OUTPUT -p icmp \
--icmp-type destination-unreachable -j DROP

$IPT -A FORWARD -o $DMZ_INTERFACE -p icmp \
--icmp-type destination-unreachable -j DROP

# Intermedatie traceroute responses
$IPT -A INPUT -p icmp \
--icmp-type time-exceeded -j ACCEPT

$IPT -A FORWARD -o $LAN_INTERFACE -p icmp \
--icmp-type time-exceeded -d $LAN_ADDRESSES -j ACCEPT

# allow outgoing pings to anywhere
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -p icmp \
--icmp-type echo-request \
-m state --state NEW -j ACCEPT

$IPT -A FORWARD -o $DMZ_INTERFACE -p icmp \
--icmp-type echo-request -s $LAN_ADDRESSES \
-m state --state NEW -j ACCEPT
fi

# allow incoming pings from trusted hosts
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $DMZ_INTERFACE -p icmp \
-s $GATEWAY_IPADDR --icmp-type echo-request -d $DMZ_IPADDR \
-m state --state NEW -j ACCEPT

$IPT -A INPUT -i $LAN_INTERFACE -p icmp \
-s $LAN_ADDRESSES --icmp-type echo-request -d $LAN_IPADDR \
-m state --state NEW -j ACCEPT
fi
```

```
# DNS Name Server

# DNS LAN clients to private server ($33)

$IPT -A INPUT -i $LAN_INTERFACE -p udp \
-s $LAN_ADDRESSES --sport $UNPRIVPORTS \
```