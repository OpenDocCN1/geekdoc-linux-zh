Rules can be defined for the explicit purpose of logging certain kinds of packets. Most, packets of interest are suspicious packets indicating some sort of probe or scan. Because all packets are denied by default, if logging is desired for certain packet types, explicit rules must be defined before the packet falls off the end of the chain and the default policy takes effect. Essentially, out of all the denied packets, you might be interested in logging some of them, using rate-limited logging for some, and silently dropping others.

Which packets are logged is an individual matter. Some people want to log all dropped packets. For other people, logging all dropped packets could soon overflow their logs. Some people, secure in the knowledge that the packets are dropped, don't care about them and don't want to know about them. Other people are interested in the obvious scans or on some particular packet type.

Because of the first-matching-rules you could log all dropped packets with a single rule. The assumption here is that all packet-matching acceptance rules have been tested, and the packet is about to drop off the end of the chain and be thrown away:

```
$SIPT -A INPUT -i $INTERNET -j LOG
```

For some people, this will produce too many log entries—or too many uninteresting log entries. For example, you might want to log all dropped incoming ICMP traffic with the exception of ping because it is a common service, regardless of whether your site responds to ping:

```
$SIPT -A INPUT -i $INTERNET -p icmp \
    --icmp-type 8 -d $IPADDR -j LOG
```

You might want to log incoming TCP traffic to all ports and log incoming UDP traffic to your privileged ports:

```
$SIPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR -j LOG
```

Then again, you might want to log all dropped privileged port access, with the exception of commonly probed ports that you don't offer service on anyway:

```
# skip ftp, telnet, ssh
$SIPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR --dport 24 -j LOG
```

```
# skip smtp
$SIPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR --dport 26:78 -j LOG
```

```
# skip finger, www
$SIPT -A INPUT -i $INTERNET -p tcp \
    -d $IPADDR --dport 81:109 -j LOG
```