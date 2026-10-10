```
# Intermediate traceroute responses
$IPT -A INPUT -i $INTERNET -p icmp \
      --icmp-type time-exceeded -d $IPADDR -j ACCEPT

# allow outgoing pings to anywhere
if [ "$CONNECTION_TRACKING" = "1" ]; then
   $IPT -A OUTPUT -o $INTERNET -p icmp \
      -s $IPADDR --icmp-type echo-request \
      -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p icmp \
    -s $IPADDR --icmp-type echo-request -j ACCEPT

$IPT -A INPUT -i $INTERNET -p icmp \
     --icmp-type echo-reply -d $IPADDR -j ACCEPT

# allow incoming pings from trusted hosts
if [ "$CONNECTION_TRACKING" = "1" ]; then
   $IPT -A INPUT -i $INTERNET -p icmp \
     -s $MY_ISP --icmp-type echo-request -d $IPADDR \
     -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p icmp \
     -s $MY_ISP --icmp-type echo-request -d $IPADDR -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p icmp \
     -s $IPADDR --icmp-type echo-reply -d $MY_ISP -j ACCEPT

#------------------------------------------------------------
# Logging Dropped Packets

# Don't log dropped incoming echo-requests
$IPT -A INPUT -i $INTERNET -p icmp \
     --icmp-type ! 8 -d $IPADDR -j LOG

$IPT -A INPUT -i $INTERNET -p tcp \
     -d $IPADDR -j LOG

$IPT -A OUTPUT -o $INTERNET -j LOG

exit 0
```