
## ICMP Group

### ICMP Objects

| Object Name | OID | Object Type | Access Mode | Description |
|-------------|-----|-------------|-------------|-------------|
| icmpEchoReps | icmp.9 | Counter | read-only | The number of ICMP echo reply messages received |
| icmpTimestamps | icmp.10 | Counter | read-only | The number of ICMP timestamp request messages received |
| icmpInTimestampReps | icmp.11 | Counter | read-only | The number of ICMP timestamp reply messages received |
| icmpAddrMasks | icmp.12 | Counter | read-only | The number of ICMP address mask requests received |
| icmpAddrMasksReps | icmp.13 | Counter | read-only | The number of ICMP address mask reply messages received |
| icmpOutMsgs | icmp.14 | Counter | read-only | The number of ICMP messages that the system attempted to send |
| icmpOutErrors | icmp.15 | Counter | read-only | The number of ICMP messages that the system couldn't send because of ICMP problems |
| icmpOutDestUnreachs | icmp.16 | Counter | read-only | The number of ICMP destination-unreachable messages sent |
| icmpOutTimeExcds | icmp.17 | Counter | read-only | The number of ICMP time-exceeded messages sent |
| icmpOutParmProbs | icmp.18 | Counter | read-only | The number of ICMP parameter problem messages sent |
| icmpOutSrcQuenchs | icmp.19 | Counter | read-only | The number of ICMP source quench messages sent |
| icmpOutRedirects | icmp.20 | Counter | read-only | The number of ICMP redirect messages sent |
| icmpOutEchos | icmp.21 | Counter | read-only | The number of ICMP echo request messages sent |
| icmpOutEchoReps | icmp.22 | Counter | read-only | The number of ICMP echo reply messages sent |
| icmpOutTimestamps | icmp.23 | Counter | read-only | The number of ICMP timestamp request messages sent |
| icmpOutTimestampReps | icmp.24 | Counter | read-only | The number of ICMP timestamp reply messages sent |
| icmpOutAddrMasks | icmp.25 | Counter | read-only | The number of ICMP address mask request messages sent |
| icmpOutAddrMaskReps | icmp.26 | Counter | read-only | The number of ICMP address mask reply messages sent |

### Sample Output from Querying the ICMP Group

```text
icmp.icmpInMsgs.0 = 27
icmp.icmpInErrors.0 = 0
icmp.icmpInDstUnreachs.0 = 7
icmp.icmpInTimeExcds.0 = 0
icmp.icmpInParmProb.0 = 0
icmp.icmpInSrcQuenches.0 = 0
icmp.icmpInRedirects.0 = 0
icmp.icmpInEchos.0 = 8
icmp.icmpInEchoReps.0 = 12
icmp.icmpInTimestamps.0 = 0
icmp.icmpInTimestampReps.0 = 0
icmp.icmpInAddrMasks.0 = 0
icmp.icmpInAddrMaskReps.0 = 0
```

```text
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

## TCP Group

The tcp group stores statistical and operational information about the Transmission Control Protocol (TCP) on a system. This group contains a single table that stores information regarding each TCP connection on the system. Figure 6.11 shows the tree view of this group.

![Figure 6.11 The tcp group view.](img/f265c9d1f2610aca197c430cbfcd51f5_327_0.png)

### TCP Objects

| Object Name | OID | Object Type | Access Mode | Description |
|-------------|-----|-------------|-------------|-------------|
| tcpRtoAlgorithm | tcp.1 | Counter | read-only | The retransmission time algorithm; possible values include other(1), constant(2), rsrc(3), and varj(4) |
| tcpRtoMin | tcp.2 | Counter | read-only | The minimum value for the retransmission timer |
| tcpRtoMax | tcp.3 | Counter | read-only | The maximum value for the retransmission timer |
| tcpMaxConn | tcp.4 | Counter | read-only | The total number (or limit) of TCP connections that the system can support |
| tcpActiveOpens | tcp.5 | Counter | read-only | The number of active opens this system has supported |
| tcpPassiveOpens | tcp.6 | Counter | read-only | The number of passive opens this system has supported |
| tcpAttemptFails | tcp.7 | Counter | read-only | The number of failed connection attempts that occurred on this system |
| tcpEstabResets | tcp.8 | Counter | read-only | The number of resets that have occurred on this system |
| tcpCurrEstab | tcp.9 | Counter | read-only | The number of TCP connections that are in either ESTABLISHED or CLOSE-WAIT states |
| tcpInSegs | tcp.10 | Counter | read-only | The number of segments received, including those received in error |
| tcpOutSegs | tcp.11 | Counter | read-only | The number of segments sent, but excluding those that contained retransmitted bytes |
| tcpRetransSegs | tcp.12 | Counter | read-only | The number of retransmitted segments |
| tcpConnTable | tcp.13 | Counter | read-only | TCP connection information |
| tcpInErrors | tcp.14 | Counter | read-only | The number of segments received in error |
| tcpOutRsts | tcp.15 | Counter | read-only | The number of TCP segments sent that contained the RST flag |

### Sample Output from Polling a Linux System

```text
tcp.tcpRtoAlgorithm.0 = other(1)
tcp.tcpRtoMin.0 = 0
tcp.tcpRtoMax.0 = 0
tcp.tcpMaxConn.0 = 0
tcp.tcpActiveOpens.0 = 105422
tcp.tcpPassiveOpens.0 = 0
tcp.tcpAttempFails.0 = 2968
tcp.tcpEstabResets.0 = 0
tcp.tcpCurrEstab.0 = Gauge: 2
tcp.tcpInSegs.0 = 63591
tcp.tcpOutSegs.0 = 111130
tcp.tcpRetransSegs.0 = 1881
```

### tcpConnTable

The `tcpConnTable` table stores specific information regarding TCP connections on the system. Figure 6.12 shows the tree view of this table. The `tcpConnEntry` object is used as an index in the table. The size of this table is determined by the number of connections recorded on the system. On a busy server, it can be quite large.

![Figure 6.12 The tcpConnTable view.](img/f265c9d1f2610aca197c430cbfcd51f5_331_0.png)

The `tcpConnState` object identifies the current state of the connection. The valid values include the following: closed(1), listen(2), sysSent(3), sysReceived(4), established(5), finWait1(6), finWait2(7), closeWait(8), lastAck(9), closing(10), timeWait(11), and deleteTCB(12). Excluding `deleteTCB(12)`, the state values are representative of the TCP state machine model that was discussed in Chapter 2, "Simple Network Management Protocol." Recall that each connection will be in one of these defined states. The `deleteTCB(12)` state indicates that the TCP control block (TCB) for this connection has been deleted. The remaining objects store both the local and remote IP Addresses and port pair. For instance, consider the following output:
