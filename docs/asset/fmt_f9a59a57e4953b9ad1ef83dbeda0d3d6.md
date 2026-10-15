
此 `MIB` 包含一些故障信息。例如，`Hewlett-Packard` 的 `EMS HA Monitors` 产品使用此 `MIB` 来监控每个网络接口的状态。

`MIB-II` 还包含网络性能信息，包括每种协议发送和接收的数据量。但是，数据并不相关或转换为速率。因此，为了准确了解网络性能，您必须在一段时间内收集这些数据，然后自行记录变化。

## RMON MIB

`RMON MIB` 旨在提供一种收集网络性能数据的标准方法。监视器或`探针`放置在特定的 `LAN` 段上，然后收集这些段的数据。`MIB` 中可存储网络数据包统计信息和网络性能历史记录。`RMON` 还提供主要网络用户列表，例如发送包含错误的数据包最多的系统。

### MIB 定义

列表 `A-2` 显示了在 `RFC 1757` 中定义的完整 `RMON` 规范。

## 列表 A-2 RMON MIB 规范。

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

## 清单 A-2
