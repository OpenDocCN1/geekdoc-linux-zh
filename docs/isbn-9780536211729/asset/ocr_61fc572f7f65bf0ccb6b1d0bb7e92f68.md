```
$IPT -A -i INTERNET -p tcp --syn \\
-s $WEB_PROXY_SERVER --sport $WEB_PROXY_PORT \\
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

# 7.5.7 Whois (TCP Port 43)

The whois program accesses the InterNIC Registration Services database. Table 7.11 lists the complete client/server connection protocol for the whois service.

Table 7.11 Whois Protocol

| Description | Protocol | Remote Address | Remote Port | In/Out | Local Address | Local Port | TCP Flag |
|---|---|---|---|---|---|---|--|
| Local client request | TCP | ANYWHERE | 43 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | ANYWHERE | 43 | | IPADDR | 1024:65535 | ACK |

The two rules enable you to query an official remote server:

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o INTERNET -p tcp \\
-s $IPADDR --sport $UNPRIVPORTS \\
--dport 43 -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -1 INTERNET -p tcp --syn \\
--sport 43 \\
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

# 7.5.8 RealAudio, RealVideo, and QuickTime
(TCP Ports 554 and 7070)

RealAudio, RealVideo, and QuickTime use the same ports. The control connection to the server is built on top of the Real-Time Streaming Protocol (RTSP). For RFC 2326, "Real Time Streaming Protocol (RTSP)," for more information on the protocol. The incoming data stream is built on top of the Real-Time Transport Protocol (RTP). See RFC 3550, "RTP: A Transport Protocol for Real-Time Applications," for more information on the RTP protocol. See http://www.realnetworks.com for more information on RealAudio and RealVideo firewall requirements.