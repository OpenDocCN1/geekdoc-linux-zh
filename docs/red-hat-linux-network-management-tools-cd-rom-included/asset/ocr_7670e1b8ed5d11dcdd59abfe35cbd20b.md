```
icmp.icmpOutMsgs.0 = 10
icmp.icmpOutErrors.0 = 0
icmp.icmpOutDestUnreachs.0 = 2
icmp.icmpOutTimeExcds.0 = 0
icmp.icmpOutParmProbs.0 = 0
icmp.icmpOutSrcQuenchs.0 = 0
icmp.icmpOutRedirects.0 = 0
icmp.icmpOutEchos.0 = 0
icmp.icmpOutEchoReps.0 = 8
icmp.icmpOutTimestamps.0 = 0
icmp.icmpOutTimestampReps.0 = 0
icmp.icmpOutAddrMasks.0 = 0
icmp.icmpOutAddrMaskReps.0 = 0
```

As you can see from the output, many of the counters are quite low. This is as it should be. High counts for certain objects such as icmpInTimeExcds indicate a configuration problem or other operational problem.

# TCP Group

The tcp group stores statistical and operational information about the Transmission Control Protocol (TCP) on a system. This group contains a single table that stores information regarding each TCP connection on the system. Figure 6.11 shows the tree view of this group.

The tcp group has the following objects:

**Object Name:**

tcpToAlgorithm

**OID:**


tcp.1

**Object Type:**


Counter

**Access Mode:**


read-only

**Description:**


The retransmission time algorithm; possible values include other(1), constant(2), rsrc(3), and varj(4)