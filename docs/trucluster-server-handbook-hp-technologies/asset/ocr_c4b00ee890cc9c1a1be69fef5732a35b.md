```
# rsh molari /usr/sbin/netstat -I tu0
Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Coll
tu0 1500 <Link> 0:10:64:30:12:31 1244810 0 595031 3 0
tu0 1500 DLI none 1244810 0 595031 3 0
tu0 1500 192.168.0 molari 1244810 0 595031 3 0
```

```
# ping clualias
PING clualias.dec.com (192.168.18.23): 56 data bytes
64 bytes from 192.168.18.23: icmp_seq=0 ttl=64 time=1 ms
64 bytes from 192.168.18.23: icmp_seq=1 ttl=64 time=0 ms
----clualias.dec.com PING Statistics----
2 packets transmitted, 2 packets received, 0% packet loss
round-trip (ms) min/avg/max = 0/0/1 ms
```

Before shutting down sheridan (the current proxy ARP master), the client has the "3a:29" address in its ARP cache.

```
# arp clualias
clualias (192.168.18.23) at 00-10-64-30-3a-29
```

Shutdown sheridan!

After shutting down sheridan, the client sees the "12:31" address in its ARP cache.

```
# arp clualias
clualias (192.168.18.23) at 00-10-64-30-12-31
```

Client access still works seamlessly.

```
# ping clualias
PING clualias.dec.com (192.168.18.23): 56 data bytes
64 bytes from 192.168.18.23: icmp_seq=0 ttl=64 time=0 ms
64 bytes from 192.168.18.23: icmp_seq=1 ttl=64 time=0 ms
----clualias.dec.com PING Statistics----
2 packets transmitted, 2 packets received, 0% packet loss
round-trip (ms) min/avg/max = 0/0/0 ms
```

Can't get to sheridan anymore (member is down).

```
# rsh sheridan /usr/sbin/netstat -I tu0
sheridan: Connection timed out
```