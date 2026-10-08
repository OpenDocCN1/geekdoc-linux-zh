

## 清单 A-13（续）

[19] oraNamesServerLookupFailures（名称服务器查找失败）
[20] oraNamesServerExactMatches（名称服务器精确匹配）
[21] oraNamesServerForwardFailures（名称服务器转发失败）
[22] oraNamesServerForwardTimeouts（名称服务器转发超时）
[23] oraNamesServerResponsesReceived（名称服务器收到的响应）
[24] oraNamesServerErrorResponsesReceived（名称服务器收到的错误响应）
[25] oraNamesServerRequestsForwarded（名称服务器转发的请求）
[26] oraNamesServerLastReload（名称服务器上次重载）
[27] oraNamesServerReloadCheckFailures（名称服务器重载检查失败）
[28] oraNamesServerLastCheckpoint（名称服务器上次检查点）
[29] oraNamesServerName（名称服务器名称）
[30] oraNamesServerAdminRegion（名称服务器管理区域）

### 监控说明

如果您打算编写自己的 SNMP 应用程序，Oracle 名称 MIB 的根 OID 为 1.3.6.1.4.1.111.6.

此 MIB 中的表项使用网络服务 MIB 中的 applIndex 进行索引。

oraNamesTNSTable 表中的运行时间可用于了解服务器已运行的时长。此表中的多个字段在 Oracle 名称中不受支持，包括启动日期、安全级别、状态、侦听地址和失败的侦听地址。

oraNamesConfigTable 包含重要的配置信息，例如服务器名称和管理区域名称。表中的多个字段在 Oracle 名称中不受支持，包括配置的 checkpoint 文件、默认转发器、与域相关的字段、配置日志文件目录、配置唯一日志标志、最大打开连接数、消息池初始大小、区域数据库标志、拓扑 checkpoint 文件以及与跟踪相关的字段。

oraNamesServerTable 包含重要的性能信息，例如收到的查询数量和发送的响应数量，以及处理查询所花费的时间。有多个字段不受支持：最近未找到的名称；有关删除、重命名和更新的信息；错误响应的统计信息；上次重载时间；以及上次 checkpoint 时间。

### Oracle Enterprise Manager MIB

Oracle Enterprise Manager (OEM) 提供数据库管理和监控功能。OEM 支持私有的 Oracle Enterprise Manager MIB，其中包含有关由 OEM 代理发现的数据库事件的信息。

#### MIB 定义

清单 A-14 展示了 Oracle 定义的 Oracle Enterprise Manager MIB 的完整规范。

### 清单 A-14 Oracle Enterprise Manager MIB 规范。

```text
enterprises
    [111] oracle
        [12] oraAgent
            [1] oraAgentObjects
                [1] oraAgentEventTable
                    [1] oraAgentEventEntry
                        [1] oraAgentEventIndex*
                        [2] oraAgentEventName
                        [3] oraAgentEventID
                        [4] oraAgentEventService
                        [5] oraAgentEventTime
                        [6] oraAgentEventSeverity
                        [7] oraAgentEventUser
                        [8] oraAgentEventAppID
                        [9] oraAgentEventMessage
                        [10] oraAgentEventArguments
                        [11] oraAgentEventResults
            [2] oraAgentTraps
                [1] oraAgentEventOcc
                [2] oraAgentEventDbUpdown
                [3] oraAgentEventDbAlert
                [4] oraAgentEventDbProbe
                [5] oraAgentEventDbUserBlock
                [6] oraAgentEventDbArchFull
                [7] oraAgentEventDbDumpFull
                [8] oraAgentEventDbMaxExtent
                [9] oraAgentEventDbChunkSmall
                [10] oraAgentEventDbDatafileLimit
                [11] oraAgentEventDbLockLimit
                [12] oraAgentEventDbProcessLimit
                [13] oraAgentEventDbSessionLimit
                [14] oraAgentEventDbUserLimit
                [15] oraAgentEventDbBuffCache
                [16] oraAgentEventDbChainRow
                [17] oraAgentEventDbDataDictionaryCache
                [18] oraAgentEventDbDiskIORate
                [19] oraAgentEventDbLibraryCache
                [20] oraAgentEventDbFreeIORate
                [21] oraAgentEventDbResponseTime
                [22] oraAgentEventDbSysStat
                [23] oraAgentEventDbSysStatDelta
                [24] oraAgentEventSQLNetUpdown
                [25] oraAgentEventHostCPULoad
                [26] oraAgentEventHostCPUUtil
                [27] oraAgentEventHostPaging
                [28] oraAgentEventHostSwapFull
                [29] oraAgentEventHostDiskFull
```

### 监控说明

如果您打算编写自己的 SNMP 应用程序，Oracle Enterprise Manager MIB 的根 OID 为 1.3.6.1.4.1.111.12。

OEM 代理发现的所有事件也可以作为 SNMP 陷阱发送。可能的陷阱包括达到可用文件空间或并发锁和会话的限制、低于配置的缓存命中率限制，以及达到系统性能阈值（如 CPU 利用率）。

### Oracle 多协议互连 MIB

Oracle 多协议互连（MPI）是一款通过在不同网络传输栈之间进行转换来提供应用程序连接的产品。它支持私有的 Oracle 多协议互连 MIB，其中包含有关多协议互连（MPI）及其组件当前状态的信息。

#### MIB 定义

清单 A-15 展示了 Oracle 定义的多协议互连 MIB 的完整规范。

### 清单 A-15 Oracle 多协议互连 MIB 规范。

```text
enterprises
    [111] oracle
        [7] oraInterchangeMIB
            [1] oraInterchangeObjects
                [1] oraInterchgTable
                    [1] oraInterchgEntry
                        [1] oraInterchgConfigDirectory
                        [2] oraInterchgContactInfo
                [2] oraNavigatorTable
                    [1] oraNavigatorEntry
                        [1] oraNavigatorRunningTime
                        [2] oraNavigatorLogging
                        [3] oraNavigatorLogLevel
                        [4] oraNavigatorLogFile
                        [5] oraNavigatorTraceLevel
                        [6] oraNavigatorTraceFile
                        [7] oraNavigatorStoppable
                        [8] oraNavigatorAccumulatedSuccessfulRequests
                        [9] oraNavigatorAccumulatedFailedRequests
                        [10] oraNavigatorState
                        [11] oraNavigatorErrors
                        [12] oraNavigatorErrorMessage
                    [3] oraNavigatorListenAddressTable
                        [1] oraNavigatorListenAddressEntry
                            [1] oraNavigatorListenAddressIndex*
                            [2] oraNavigatorListenAddress
                    [4] oraNavigatorFailedAddressTable
                        [1] oraNavigatorFailedAddressEntry
                            [1] oraNavigatorFailedAddressIndex*
                            [2] oraNavigatorFailedAddress
                    [5] oraNavigatorRouteAddressTable
                        [1] oraNavigatorRouteAddressEntry
                            [1] oraNavigatorRouteAddressIndex*
                            [2] oraNavigatorRouteAddress
                [6] oraCmanagerTable
                    [1] oraCmanagerEntry
                        [1] oraCmanagerStartTime
                        [2] oraCmanagerRunningTime
                        [3] oraCmanagerLogging
                        [4] oraCmanagerLogFile
                        [5] oraCmanagerTraceLevel
                        [6] oraCmanagerTraceFile
                        [7] oraCmanagerStoppable
                        [8] oraCmanagerMaximumPumps
                        [9] oraCmanagerMaximumConnectionsPerPump
                        [10] oraCmanagerPumpStrategy
                        [11] oraCmanagerActivePumps
                        [12] oraCmanagerMaximumConnections
                        [13] oraCmanagerCurrentConnectionsInUse
                        [14] oraCmanagerAccumulatedSuccessfulConnections
                        [15] oraCmanagerAccumulatedFailedConnections
                        [16] oraCmanagerImmediateAverageBytes
                        [17] oraCmanagerMaximumConnectTime
                        [18] oraCmanagerMinimumConnectTime
                        [19] oraCmanagerAverageConnectTime
                        [20] oraCmanagerMaximumConnectDuration
                        [21] oraCmanagerState
                        [22] oraCmanagerErrors
                        [23] oraCmanagerErrorMessage
                    [7] oraCmanagerListenAddressTable
                        [1] oraCmanagerListenAddressEntry
                            [1] oraCmanagerListenAddressIndex*
                            [2] oraCmanagerListenAddress
                    [8] oraCmanagerFailedAddressTable
                        [1] oraCmanagerFailedAddressEntry
                            [1] oraCmanagerFailedAddressIndex*
                            [2] oraCmanagerFailedAddress
                [9] oraPumpTable
                    [1] oraPumpEntry
                        [1] oraPumpIndex*
                        [2] oraPumpActiveTime
                        [3] oraPumpTraceLevel
                        [4] oraPumpTraceFile
                        [5] oraPumpActiveConnections
                        [6] oraPumpSuccessfulConnections
                        [7] oraPumpFailedConnections
                        [8] oraPumpAccumulatedBytesSent
                        [9] oraPumpCurrentBytesPerSecond
                        [10] oraPumpMaximumAverageBytes
                        [11] oraPumpImmediateAverageBytes
                        [12] oraPumpMaximumConnectTime
                        [13] oraPumpMinimumConnectTime
                        [14] oraPumpAverageConnectTime
                        [15] oraPumpMaximumConnectDuration
                        [16] oraPumpMaximumBuffers
                        [17] oraPumpBufferUtilization
                        [18] oraPumpErrors
                        [19] oraPumpErrorMessage
                    [10] oraPumpListenAddressTable
                        [1] oraPumpListenAddressEntry
                            [1] oraPumpListenAddressIndex*
                            [2] oraPumpListenAddress
                    [11] oraPumpFailedAddressTable
                        [1] oraPumpFailedAddressEntry
                            [1] oraPumpFailedAddressIndex*
                            [2] oraPumpFailedAddress
                [12] oraConnectionTable
                    [1] oraConnectionEntry
                        [1] oraConnectionIndex*
                        [2] oraConnectionPumpID
                        [3] oraConnectionIdleTime
                        [4] oraConnectionDuration
                        [5] oraConnectionSourceAddress
                        [6] oraConnectionDestinationAddress
            [2] oraInterchgTraps
```

### 监控说明

如果您打算编写自己的 SNMP 应用程序，Oracle 多协议互连 MIB 的根 OID 为 1.3.6.1.4.1.111.7。

此 MIB 中的许多表项使用网络服务 MIB 中的 applIndex 进行索引。

此 MIB 包含有关 MPI 多个组件的信息，例如 Navigator（导航器）和 Connection Manager（连接管理器）。还提供了每个连接的持续时间和空闲时间。

