```
# ICMP rules
$IPT -A EXT-log-in -p icmp \
      --icmp-type ! echo-request -m limit -j LOG

# TCP rules
$IPT -A EXT-log-in -p tcp \
      --dport 0:19 -j LOG

# skip ftp, telnet, ssh
$IPT -A EXT-log-in -p tcp \
      --dport 24 -j LOG

# skip smtp
$IPT -A EXT-log-in -p tcp \
      --dport 26:78 -j LOG

# skip finger, www
$IPT -A EXT-log-in -p tcp \
      --dport 81:109 -j LOG

# skip pop-3, sunrpc
$IPT -A EXT-log-in -p tcp \
      --dport 112:136 -j LOG

# skip NetBIOS
$IPT -A EXT-log-in -p tcp \
      --dport 140:142 -j LOG

# skip imap
$IPT -A EXT-log-in -p tcp \
      --dport 144:442 -j LOG

# skip secure web/SSL
$IPT -A EXT-log-in -p tcp \
      --dport 444:65535 -j LOG

# UDP rules
$IPT -A EXT-log-in -p udp \
      --dport 0:110 -j LOG

# skip sunrpc
$IPT -A EXT-log-in -p udp \
      --dport 112:160 -j LOG
```