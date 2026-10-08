fi

```
IPT -A OUTPUT -o $INTERNET -p tcp \
-m multiport --destination-port 554,7070 \
---syn s $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

```
IPT -A INPUT -i $INTERNET -p tcp \
-m multiport --destination-port 554,7070 \
! --syn -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

The next rule allows the preferred UDP data stream from the server:

```
IPT -A INPUT -i $INTERNET -p udp \
---sport $UNPRIVPORTS \
-d $IPADDR --dport 6970:7170 -j ACCEPT
```

The next rule establishes the TCP data stream connection with the server:

```
if [ "CONNECTION_TRACKING" = "1" ]; then \
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
---dport 7071 -m state --state NEW -j ACCEPT
```

fi

```
IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
---dport 7071 -j ACCEPT
```

```
IPT -A INPUT -i $INTERNET -p tcp | --syn \
---d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

# 7.6 Enabling Common UDP Services

The stateless UDP protocol is inherently less secure than the connection-based TCP protocol. Because of this, many security-conscious sites completely disable, or limit as much as possible, all access to UDP services. Obviously, UDP-based DNS exchanges are necessary, but the remote name servers can be explicitly specified in the firewall rules. As such, this section provides rules for only three services:

+   - traceroute
- Dynamic Host Configuration Protocol (DHCP)
- Network Time Protocol (NTP)

# 7.6.1 traceroute (UDP Port 33434)

On Unix and Linux systems, traceroute is a UDP service that causes intermediate systems to generate ICMP Time Exceeded messages to gather hop count information, and that