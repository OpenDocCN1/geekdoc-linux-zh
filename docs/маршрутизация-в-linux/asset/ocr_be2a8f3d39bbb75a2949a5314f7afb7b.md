```
icmp.icmpInTimeExcds.0 = Counter32: 0
icmp.icmpInParmProbs.0 = Counter32: 0
icmp.icmpInSrcQuenchs.0 = Counter32: 0
icmp.icmpInRedirects.0 = Counter32: 0
icmp.icmpInEchos.0 = Counter32: 3
icmp.icmpInEchoReps.0 = Counter32: 3
icmp.icmpInTimestamps.0 = Counter32: 0
icmp.icmpInTimestampReps.0 = Counter32: 0
icmp.icmpInAddrMasks.0 = Counter32: 0
icmp.icmpInAddrMaskReps.0 = Counter32: 0
icmp.icmpOutMsgs.0 = Counter32: 9
icmp.icmpOutErrors.0 = Counter32: 0
icmp.icmpOutDestUnreachs.0 = Counter32: 6
icmp.icmpOutTimeExcds.0 = Counter32: 0
icmp.icmpOutParmProbs.0 = Counter32: 0
icmp.icmpOutSrcQuenchs.0 = Counter32: 0
icmp.icmpOutRedirects.0 = Counter32: 0
icmp.icmpOutEchos.0 = Counter32: 0
icmp.icmpOutEchoReps.0 = Counter32: 3
icmp.icmpOutTimestamps.0 = Counter32: 0
icmp.icmpOutTimestampReps.0 = Counter32: 0
icmp.icmpOutAddrMasks.0 = Counter32: 0
icmp.icmpOutAddrMaskReps.0 = Counter32: 0
```

Here is an snmpwalk that shows all the data that makes up the IP routing table:

```
[root@lefty /root]# snmpwalk 192.168.1.254 'readaccess ip.ipRouteTable'
ip.ipRouteTable.ipRouteEntry.ipRouteDest.0.0.0.0 = IpAddress: 0.0.0.0
ip.ipRouteTable.ipRouteEntry.ipRouteDest.127.0.0.0 = IpAddress: 127.0.0.0
ip.ipRouteTable.ipRouteEntry.ipRouteDest.192.168.1.0 = IpAddress: 192.168.1.0
ip.ipRouteTable.ipRouteEntry.ipRouteDest.192.168.1.254 = IpAddress: 192.168.1.25
4
ip.ipRouteTable.ipRouteEntry.ipRouteIfIndex.0.0.0.0 = 2
ip.ipRouteTable.ipRouteEntry.ipRouteIfIndex.127.0.0.0 = 3
ip.ipRouteTable.ipRouteEntry.ipRouteIfIndex.192.168.1.0 = 2
ip.ipRouteTable.ipRouteEntry.ipRouteIfIndex.192.168.1.254 = 2
ip.ipRouteTable.ipRouteEntry.ipRouteMetric.0.0.0.0 = 1
ip.ipRouteTable.ipRouteEntry.ipRouteMetric.127.0.0.0 = 0
ip.ipRouteTable.ipRouteEntry.ipRouteMetric.192.168.1.0 = 0
ip.ipRouteTable.ipRouteEntry.ipRouteMetric.192.168.1.254 = 0
ip.ipRouteTable.ipRouteEntry.ipRouteNextHop.0.0.0.0 = IpAddress: 192.168.1.1
ip.ipRouteTable.ipRouteEntry.ipRouteNextHop.127.0.0.0 = IpAddress: 0.0.0.0
ip.ipRouteTable.ipRouteEntry.ipRouteNextHop.192.168.1.0 = IpAddress: 0.0.0.0
ip.ipRouteTable.ipRouteEntry.ipRouteNextHop.192.168.1.254 = IpAddress: 0.0.0.0
ip.ipRouteTable.ipRouteEntry.ipRouteType.0.0.0.0 = indirect(4)
ip.ipRouteTable.ipRouteEntry.ipRouteType.127.0.0.0 = direct(3)
ip.ipRouteTable.ipRouteEntry.ipRouteType.192.168.1.0 = direct(3)
ip.ipRouteTable.ipRouteEntry.ipRouteType.192.168.1.254 = direct(3)
ip.ipRouteTable.ipRouteEntry.ipRouteProto.0.0.0.0 = local(2)
ip.ipRouteTable.ipRouteEntry.ipRouteProto.127.0.0.0 = local(2)
ip.ipRouteTable.ipRouteEntry.ipRouteProto.192.168.1.0 = local(2)
ip.ipRouteTable.ipRouteEntry.ipRouteProto.192.168.1.254 = local(2)
```