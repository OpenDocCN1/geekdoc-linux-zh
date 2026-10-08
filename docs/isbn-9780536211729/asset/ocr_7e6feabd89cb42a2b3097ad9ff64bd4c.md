# 7.9 Logging Dropped Outgoing Packets

```
# skip pop-3, sunrpc
IPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR --port 112:136 -j LOG
# skip NetBIOS
IPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR --port 140:142 -j LOG
# skip imap
IPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR --port 144:442 -j LOG
# skip secure_web/SSL
IPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR --port 444:65535 -j LOG

#UDP rules
IPT -A INPUT -i $INTERNET -p udp \
    -d $IPADDR --port 0:110 -j LOG
# skip sunrpc
IPT -A INPUT -i $INTERNET -p udp \
    -d $IPADDR --port 112:160 -j LOG
# skip snmp
IPT -A INPUT -i $INTERNET -p udp \
    -d $IPADDR --port 163:634 -j LOG
# skip NFS mounted
IPT -A INPUT -i $INTERNET -p udp \
    -d $IPADDR --port 636:5631 -j LOG
# skip pcAnywhere
IPT -A INPUT -i $INTERNET -p udp \
    -d $IPADDR --port 5633:31336 -j LOG
# skip traceroute's default ports
IPT -A INPUT -i $INTERNET -p udp \
    -sport $TRACEROUTE_SRC \
    -d $IPADDR --port $TRACEROUTE_DEST -j LOG
# skip the rest
IPT -A INPUT -i $INTERNET -p udp \
    -d $IPADDR --port 33344:65535 -j LOG
```

# 7.9 Logging Dropped Outgoing Packets

Logging outgoing traffic blocked by the firewall rules is necessary for debugging the fire-wall rules and to be alerted to local software problems.

With the exception of outgoing ICMP type 3 errors, which were dropped previously, possibly traffic about to be dropped by the default policy could be logged:

```
IPT -A OUTPUT -o $INTERNET -j LOG
```