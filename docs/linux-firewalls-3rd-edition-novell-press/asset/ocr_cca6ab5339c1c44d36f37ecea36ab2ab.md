```
-d $LAN_IPADDR --dport 53 \
-m state --state NEW -j ACCEPT

$IPT -A INPUT -i $LAN_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport SUNPRIVPORTS \
-d $LAN_IPADDR --dport 53 \
-m state --state NEW -j ACCEPT

$IPT -A INPUT -i $DMZ_INTERFACE -p udp \
-s $DMZ_ADDRESSES --sport SUNPRIVPORTS \
-d $DMZ_IPADDR --dport 53 \
-m state --state NEW -j ACCEPT

# DNS caching & forwarding name server (53)

$IPT -A OUTPUT -o $DMZ_INTERFACE -p udp \
-s $DMZ_IPADDR --sport 53 \
-d $NAMESERVER --dport 53 \
-m state --state NEW -j ACCEPT

$IPT -A OUTPUT -o $DMZ_INTERFACE -p udp \
-s $DMZ_IPADDR --sport SUNPRIVPORTS \
-d $NAMESERVER --dport 53 \
-m state --state NEW -j ACCEPT

$IPT -A OUTPUT -o $DMZ_INTERFACE -p tcp \
-s $DMZ_IPADDR --sport SUNPRIVPORTS \
-d $NAMESERVER --dport 53 \
-m state --state NEW -j ACCEPT
```

```
#########################################################
# Filtering the AUTH User Identification Service (TCP Port 113)

$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport SUNPRIVPORTS --dport 113 \
-m state --state NEW -j Accept

$IPT -A FORWARD -i $DMZ_INTERFACE -o $LAN_INTERFACE -p tcp \
--sport SUNPRIVPORTS -d $LAN_ADDRESSES --dport 113 \
-m state --state NEW -j ACCEPT

$IPT -A INPUT -i $LAN_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport SUNPRIVPORTS -d $LAN_IPADDR --dport 113 \
-m state --state NEW -j ACCEPT
```