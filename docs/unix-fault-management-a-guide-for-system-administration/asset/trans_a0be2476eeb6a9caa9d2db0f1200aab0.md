

一个 oraDbmsDbTable 条目很可能对应于多个表空间表条目。例如，除了指示已分配和正在使用的空间量之外，状态变量 oraDbTablespaceState 还指示该表空间是离线状态还是可访问状态。

oraDbDataFileTable 记录针对数据文件执行的磁盘读和写操作次数。oraDbConfigTable 存储重要的数据库配置参数，例如 **DB_BLOCK_BUFFERS**，该参数用于确定缓冲区缓存的大小。

oraDbLibraryCacheTable 记录有关库缓存的性能数据。该表中的变量（如 oraDbLibraryCachePins 和 oraDbLibraryCacheReloads）可用于计算库缓存未命中率。每个表条目代表系统中当前数据库实例内的一个特定库缓存。oraDbLibraryCacheSumTable 提供数据库中所有库缓存的汇总信息。

## Oracle 网络监听器 MIB

Oracle 网络监听器 MIB 是一个协议独立的应用程序，用于接收来自远程数据库用户的连接请求。Oracle 提供了一个私有的网络监听器 MIB，其中包含有关监听器进程当前状态的附加信息。

### MIB 定义

列表 A-12 展示了 Oracle 定义的 Oracle 私有网络监听器 MIB 的完整规范。

**列表 A-12** Oracle 网络监听器 MIB 规范。

```text
enterprises
   |
      [111] oracle
      |
         [5 ] oraListenerMIB
         |
            [1 ] oraListenerObjects
            |
               [1 ] oraListenerTable
               |
                  [1 ] oraListenerEntry
                  |
                     [1 ] oraListenerIndex*
                     [2 ] oraListenerName
                     [3 ] oraListenerVersion
                     [4 ] oraListenerStartDate
                     [5 ] oraListenerUptime
                     [6 ] oraListenerTraceLevel
                     [7 ] oraListenerSecurityLevel
                     [8 ] oraListenerParameterFile
                     [9 ] oraListenerLogFile
                     [10] oraListenerTraceFile
                     [11] oraListenerState
                     [12] oraListenerNumberOfServices
                     [13] oraListenerContact
               [2 ] oraSIDTable
               |
                  [1 ] oraSIDEntry
                  |
                     [1 ] oraSIDListenerIndex*
                     [2 ] oraSIDName*
                     [3 ] oraSIDCurrentConnectedClients
                     [4 ] oraSIDReservedConnections
               [3 ] oraDedicatedSrvTable
               |
                  [1 ] oraDedicatedSrvEntry
                  |
                     [1 ] oraDedicatedSrvIndex*
                     [2 ] oraDedicatedSrvEstablishedConnections
                     [3 ] oraDedicatedSrvRejectedConnections
               [4 ] oraDispatcherTable
               |
                  [1 ] oraDispatcherEntry
                  |
                     [1 ] oraDispatcherIndex*
                     [2 ] oraDispatcherEstablishedConnections
                     [3 ] oraDispatcherRejectedConnections
                     [4 ] oraDispatcherActiveConnections
                     [5 ] oraDispatcherMaximumConnections
                     [6 ] oraDispatcherState
                     [7 ] oraDispatcherProtocolInfo
               [5 ] oraPrespawnedSrvTable
               |
                  [1 ] oraPrespawnedSrvEntry
                  |
                     [1 ] oraPrespawnedSrvIndex*
                     [2 ] oraPrespawnedSrvEstablishedConnections
                     [3 ] oraPrespawnedSrvRejectedConnections
                     [4 ] oraPrespawnedSrvCurrentConnections
                     [5 ] oraPrespawnedSrvMaximumConnections
                     [6 ] oraPrespawnedSrvState
                     [7 ] oraPrespawnedSrvProtocolInfo
                     [8 ] oraPrespawnedSrvProcessorID
               [6 ] oraListenAddressTable
               |
                  [1 ] oraListenAddressEntry
                  |
                     [1 ] oraListenAddressIndex*
                     [2 ] oraListenAddress
               [2 ] oraListenerTraps
               |
                  [1 ] oraListenerStateChange
```

### 监控说明

如果您打算编写自己的 SNMP 应用程序，Oracle 网络监听器 MIB 的根 OID 为 1.3.6.1.4.1.111.5。

oraListenerTable 中的每个条目代表系统中当前数据库实例的网络监听器。您应该监控监听器的状态（oraListenerState），以确保进程仍在运行。如果监听器未运行，则无法处理新的客户端连接请求。您可以通过让管理站监听 oraListenerStateChange 陷阱来监控这一情况，该陷阱指示监听器状态已发生变化。这是当前 MIB 提供的唯一陷阱。请注意，Oracle 的 OEM MIB 还包含一个陷阱，当 OEM 代理检测到监听器宕机时会发送该陷阱。

针对监听器所监控的每个数据库实例，都存在一个 oraSIDEntry。您应该比较当前连接的客户端数量与最大保留数量，以查看是否接近限制。当达到限制时，新请求将被重定向到专用服务器，这需要更多的系统资源。

调度器（Dispatchers）和预生成服务器（prespawned servers）是帮助客户端连接数据库的可选进程。同样，为了检查问题是否即将发生，请检查当前连接数是否接近允许的最大连接数。

## Oracle Names MIB

Oracle Names 产品为数据库信息提供了企业目录服务。有关 Oracle Names 的更多信息，请参阅 Oracle 出版的 *Oracle Names 管理员指南*。这个私有的 Oracle MIB 提供了有关 Oracle Names 产品当前状态的附加信息。

### MIB 定义

列表 A-13 展示了 Oracle 定义的 Oracle Names MIB 的完整规范。

**列表 A-13** Oracle Names MIB 规范。

```text
enterprises
   |
      [111] oracle
      |
         [6 ] oraNamesMIB
         |
            [1 ] oraNamesObjects
            |
               [1 ] oraNamesTNSTable
               |
                  [1 ] oraNamesTNSEntry
                  |
                     [1 ] oraNamesTNSStartDate
                     [2 ] oraNamesTNStraceLevel
                     [3 ] oraNamesTNSsecurityLevel
                     [4 ] oraNamesTNSparameterFile
                     [5 ] oraNamesTNSlogFile
                     [6 ] oraNamesTNStraceFile
                     [7 ] oraNamesTNSstate
                     [8 ] oraNamesTNScontact
                     [9 ] oraNamesTNSlistenAddresses
                     [10] oraNamesTNSfailedListenAddresses
                     [11] oraNamesTNSreload
                     [12] oraNamesTNSrunningTime
               [2 ] oraNamesConfigTable
               |
                  [1 ] oraNamesConfigEntry
                  |
                     [1 ] oraNamesConfigAdminRegion
                     [2 ] oraNamesConfigAuthorityRequired
                     [3 ] oraNamesConfigAutoRefreshExpire
                     [4 ] oraNamesConfigAutoRefreshRetry
                     [5 ] oraNamesConfigCacheCheckpointFile
                     [6 ] oraNamesConfigCacheCheckpointInterval
                     [7 ] oraNamesConfigConfigCheckpointFile
                     [8 ] oraNamesConfigDefaultForwarders
                     [9 ] oraNamesConfigForwardersOnly
                     [10] oraNamesConfigDomainCheckpointFile
                     [11] oraNamesConfigDomainHints
                     [12] oraNamesConfigDomains
                     [13] oraNamesConfigForwardingAvailable
                     [14] oraNamesConfigForwardingDesired
                     [15] oraNamesConfigLogDirectory
                     [16] oraNamesConfigLogStatsInterval
                     [17] oraNamesConfigLogUnique
                     [18] oraNamesConfigMaxOpenConnections
                     [19] oraNamesConfigMaxOpenForwards
                     [20] oraNamesConfigMessagePoolStartSize
                     [21] oraNamesConfigNoModifyRequests
                     [22] oraNamesConfigNoRegionDatabase
                     [23] oraNamesConfigResetStatsInterval
                     [24] oraNamesConfigServerName
                     [25] oraNamesConfigTopologyCheckpointFile
                     [26] oraNamesConfigTraceDirectory
                     [27] oraNamesConfigTraceFunc
                     [28] oraNamesConfigTraceMask
                     [29] oraNamesConfigTraceUnique
               [3 ] oraNamesServerTable
               |
                  [1 ] oraNamesServerEntry
                  |
                     [1 ] oraNamesServerQueriesReceived
                     [2 ] oraNamesServerLastNamesNotFound
                     [3 ] oraNamesServerQueriesTotalTime
                     [4 ] oraNamesServerDeletesReceived
                     [5 ] oraNamesServerDeletesRefused
                     [6 ] oraNamesServerDeletesTotalTime
                     [7 ] oraNamesServerRenamesReceived
                     [8 ] oraNamesServerRenamesRefused
                     [9 ] oraNamesServerRenamesTotalTime
                     [10] oraNamesServerUpdatesReceived
                     [11] oraNamesServerUpdatesRefused
                     [12] oraNamesServerUpdatesTotalTime
                     [13] oraNamesServerCorruptMessagesReceived
                     [14] oraNamesServerResponsesSent
                     [15] oraNamesServerErrorResponsesSent
                     [16] oraNamesServerAliasLoopsDetected
                     [17] oraNamesServerLookupsAttempted
                     [18] oraNamesServerCreatedOnLookup
```

