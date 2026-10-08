
# 列表 A-1（续）

```text
[20] ipAddrTable
      [1 ] ipAddrEntry
           [1 ] ipAdEntAddr*
           [2 ] ipAdEntIfIndex
           [3 ] ipAdEntNetMask
           [4 ] ipAdEntBcastAddr
           [5 ] ipAdEntReasmMaxSize
[21] ipRouteTable
      [1 ] ipRouteEntry
           [1 ] ipRouteDest*
           [2 ] ipRouteIfIndex
           [3 ] ipRouteMetric1
           [4 ] ipRouteMetric2
           [5 ] ipRouteMetric3
           [6 ] ipRouteMetric4
           [7 ] ipRouteNextHop
           [8 ] ipRouteType
           [9 ] ipRouteProto
           [10] ipRouteAge
           [11] ipRouteMask
           [12] ipRouteMetric5
           [13] ipRouteInfo
[22] ipNetToMediaTable
      [1 ] ipNetToMediaEntry
           [1 ] ipNetToMediaIfIndex*
           [2 ] ipNetToMediaPhysAddress
           [3 ] ipNetToMediaNetAddress*
           [4 ] ipNetToMediaType
[23] ipRoutingDiscards
[5 ] icmp
      [1 ] icmpInMsgs
      [2 ] icmpInErrors
      [3 ] icmpInDestUnreachs
      [4 ] icmpInTimeExcds
      [5 ] icmpInParmProbs
      [6 ] icmpInSrcQuenchs
      [7 ] icmpInRedirects
      [8 ] icmpInEchos
      [9 ] icmpInEchoReps
      [10] icmpInTimestamps
      [11] icmpInTimestampReps
      [12] icmpInAddrMasks
      [13] icmpInAddrMaskReps
      [14] icmpOutMsgs
      [15] icmpOutErrors
      [16] icmpOutDestUnreachs
      [17] icmpOutTimeExcds
      [18] icmpOutParmProbs
      [19] icmpOutSrcQuenchs
      [20] icmpOutRedirects
      [21] icmpOutEchos
      [22] icmpOutEchoReps
      [23] icmpOutTimestamps
      [24] icmpOutTimestampReps
      [25] icmpOutAddrMasks
      [26] icmpOutAddrMaskReps
[6 ] tcp
    [1 ] tcpRtoAlgorithm
    [2 ] tcpRtoMin
    [3 ] tcpRtoMax
    [4 ] tcpMaxConn
    [5 ] tcpActiveOpens
    [6 ] tcpPassiveOpens
    [7 ] tcpAttemptFails
    [8 ] tcpEstabResets
    [9 ] tcpCurrEstab
    [10] tcpInSegs
    [11] tcpOutSegs
    [12] tcpRetransSegs
    [13] tcpConnTable
        [ 1 ] tcpConnEntry
            [ 1 ] tcpConnState
            [ 2 ] tcpConnLocalAddress*
            [ 3 ] tcpConnLocalPort*
            [ 4 ] tcpConnRemAddress
            [ 5 ] tcpConnRemPort
    [14] tcpInErrs
    [15] tcpOutRsts
[7 ] udp
    [1 ] udpInDatagrams
    [2 ] udpNoPorts
    [3 ] udpInErrors
    [4 ] udpOutDatagrams
    [5 ] udpTable
        [ 1 ] udpEntry
            [ 1 ] udpLocalAddress*
            [ 2 ] udpLocalPort*
[8 ] egp
    [1 ] egpInMsgs
    [2 ] egpInErrors
    [3 ] egpOutMsgs
    [4 ] egpOutErrors
    [5 ] egpNeighTable
        [1 ] egpNeighEntry
            [1 ] egpNeighState
            [2 ] egpNeighAddr*
            [3 ] egpNeighAs
            [4 ] egpNeighInMsgs
            [5 ] egpNeighInErrs
            [6 ] egpNeighOutMsgs
            [7 ] egpNeighOutErrs
            [8 ] egpNeighInErrMsgs
            [9 ] egpNeighOutErrMsgs
            [10] egpNeighStateUps
            [11] egpNeighStateDowns
            [12] egpNeighIntervalHello
            [13] egpNeighIntervalPoll
            [14] egpNeighMode
            [15] egpNeighEventTrigger
    [6 ] egpAs
[10] transmission
[11] snmp
    [1 ] snmpInPkts
    [2 ] snmpOutPkts
    [3 ] snmpInBadVersions
    [4 ] snmpInBadCommunityNames
    [5 ] snmpInBadCommunityUses
    [6 ] snmpInASNParseErrs
    [7 ] snmpInTooBigs
    [8 ] snmpInNoSuchNames
    [9 ] snmpInBadValues
    [10] snmpInReadOnlys
    [11] snmpInGenErrs
    [12] snmpInTotalReqVars
    [13] snmpInTotalSetVars
    [14] snmpInGetRequests
    [15] snmpInGetNexts
    [16] snmpInSetRequests
    [17] snmpInGetResponses
    [18] snmpInTraps
    [19] snmpOutTooBigs
    [20] snmpOutNoSuchNames
    [21] snmpOutBadValues
    [22] snmpOutGenErrs
    [23] snmpOutGetRequests
    [24] snmpOutGetNexts
    [25] snmpOutSetRequests
    [26] snmpOutGetResponses
    [27] snmpOutTraps
    [28] snmpEnableAuthenTraps
```

### 监控说明

使用 HP OpenView MIB 浏览器等工具导航 MIB 层次结构时，您会看到 MIB 变量的助记符名称。MIB-II 的助记符是 iso.org.dod.internet.mgmt.mib-2。但是，如果您打算编写自己的 SNMP 应用程序，您需要了解 MIB-II 的数值根 OID，即 1.3.6.1.2.1。操作员可以查询此信息并将其关联起来以跟踪错误率。

此 MIB 包含一些故障信息。例如，Hewlett-Packard 的 EMS HA Monitors 产品使用此 MIB 来监控每个网络接口的状态。

MIB-II 还包含网络性能信息，包括每种协议发送和接收的数据量。但是，数据并不相关或转换为速率。因此，为了准确了解网络性能，您必须在一段时间内收集这些数据，然后自行记录变化。

### RMON MIB

RMON MIB 旨在提供一种收集网络性能数据的标准方法。监视器或*探针*放置在特定的 LAN 段上，然后收集这些段的数据。MIB 中可存储网络数据包统计信息和网络性能历史记录。RMON 还提供主要网络用户列表，例如发送包含错误的数据包最多的系统。

### MIB 定义

列表 A-2 显示了在 RFC 1757 中定义的完整 RMON 规范。

# 列表 A-2 RMON MIB 规范。

```text
mib_2
|   [16]  rmon
|   |   [1 ]   statistics
|   |   |   [1 ]   etherStatsTable
|   |   |   |   [1 ]   etherStatsEntry
|   |   |   |   |   [1 ]   etherStatsIndex*
|   |   |   |   |   [2 ]   etherStatsDataSource
|   |   |   |   |   [3 ]   etherStatsDropEvents
|   |   |   |   |   [4 ]   etherStatsOctets
|   |   |   |   |   [5 ]   etherStatsPkts
|   |   |   |   |   [6 ]   etherStatsBroadcastPkts
|   |   |   |   |   [7 ]   etherStatsMulticastPkts
|   |   |   |   |   [8 ]   etherStatsCRCAlignErrors
|   |   |   |   |   [9 ]   etherStatsUndersizePkts
|   |   |   |   |   [10]  etherStatsOversizePkts
|   |   |   |   |   [11]  etherStatsFragments
|   |   |   |   |   [12]  etherStatsJabbers
|   |   |   |   |   [13]  etherStatsCollisions
|   |   |   |   |   [14]  etherStatsPkts64Octets
|   |   |   |   |   [15]  etherStatsPkts65to127Octets
|   |   |   |   |   [16]  etherStatsPkts128to255Octets
|   |   |   |   |   [17]  etherStatsPkts256to511Octets
|   |   |   |   |   [18]  etherStatsPkts512to1023Octets
|   |   |   |   |   [19]  etherStatsPkts1024to1518Octets
|   |   |   |   |   [20]  etherStatsOwner
|   |   |   |   |   [21]  etherStatsStatus
|   |   |   [ 2 ]  history
|   |   |   |   |   [ 1 ]  historyControlTable
|   |   |   |   |   |   [ 1 ]  historyControlIndex*
|   |   |   |   |   |   [ 2 ]  historyControlDataSource
|   |   |   |   |   |   [ 3 ]  historyControlBucketsRequested
|   |   |   |   |   |   [ 4 ]  historyControlBucketsGranted
|   |   |   |   |   |   [ 5 ]  historyControlInterval
|   |   |   |   |   |   [ 6 ]  historyControlOwner
|   |   |   |   |   |   [ 7 ]  historyControlStatus
|   |   |   |   [ 2 ]  etherHistoryTable
|   |   |   |   |   [ 1 ]  etherHistoryEntry
|   |   |   |   |   |   [ 1 ]  etherHistoryIndex*
|   |   |   |   |   |   [ 2 ]  etherHistorySampleIndex*
|   |   |   |   |   |   [ 3 ]  etherHistoryIntervalStart
|   |   |   |   |   |   [ 4 ]  etherHistoryDropEvents
|   |   |   |   |   |   [ 5 ]  etherHistoryOctets
|   |   |   |   |   |   [ 6 ]  etherHistoryPkts
|   |   |   |   |   |   [ 7 ]  etherHistoryBroadcastPkts
|   |   |   |   |   |   [ 8 ]  etherHistoryMulticastPkts
|   |   |   |   |   |   [ 9 ]  etherHistoryCRCAlignErrors
|   |   |   |   |   |   [10]  etherHistoryUndersizePkts
|   |   |   |   |   |   [11]  etherHistoryOversizePkts
|   |   |   |   |   |   [12]  etherHistoryFragments
|   |   |   |   |   |   [13]  etherHistoryJabbers
|   |   |   |   |   |   [14]  etherHistoryCollisions
|   |   |   |   |   |   [15]  etherHistoryUtilization
|   |   |   |   [ 3 ]  alarm
|   |   |   |   |   [ 1 ]  alarmTable
```
