

### 附录 A-10（续）

```text
[5] rdbmsSrvLimitedResourceHighwater
[6] rdbmsSrvLimitedResourceFailures
[7] rdbmsSrvLimitedResourceDescription
[9] rdbmsRelTable
    [1] rdbmsRelEntry
    [1] rdbmsRelState
    [2] rdbmsRelActiveTime
[2] rdbmsTraps
    [1] rdbmsStateChange
    [2] rdbmsOutOfSpace
[3] rdbmsConformance
    [1] rdbmsCompliances
        [1] rdbmsCompliance
    [2] rdbmsGroups
        [1] rdbmsGroup
```

## 监控说明

如果您打算编写自己的 SNMP 应用程序，RDBMS MIB 的根 OID 为 1.3.6.1.2.1.39。

RDBMS MIB 包含故障信息和性能信息。MIB 包含每个数据库的状态。通过交叉引用服务器表和“网络服务”MIB 中的应用条目，可以获得数据库实例的状态。这样，您就可以看到进程状态（applOperStatus）。为了验证服务器是否正在响应，您可以检查 applAccumulatedInboundAssociations，以查看连接数是否仍在增加。Informix 支持此字段，但 Oracle 不支持。

性能信息包括已提交的数据库事务数以及数据库 I/O 和缓存命中率。

您还可以使用此 MIB 来确定数据库表是否已达到其配置的限制。

数据库供应商并未实现此 MIB 的所有组件。例如，Oracle 和 Informix 未实现 RDBMS MIB 中的以下表：

- rdbmsDbParamTable
- rdbmsDbLimitedResourceTable

此外，Oracle 未实现 RDBMS MIB 中的 rdbmsSrvLimitedResourceTable。

## Oracle 专有数据库 MIB

Oracle 的专有数据库 MIB 包含特定于 Oracle7 架构的额外 RDBMS 统计信息。它旨在作为 RDBMS MIB 的补充。此 MIB 中的大部分信息都与性能相关。

## MIB 定义

附录 A-11 展示了 Oracle 定义的 Oracle 专有数据库 MIB 的完整规范。

### 附录 A-11 Oracle 专有数据库 MIB 规范。

```text
enterprises
    [111] oracle
        [4] oraDbMIB
            [1] oraDbObjects
                [1] oraDbSysTable
                    [1] oraDbSysEntry
                    [1] oraDbSysConsistentChanges
                    [2] oraDbSysConsistentGets
                    [3] oraDbSysDbBlockChanges
                    [4] oraDbSysDbBlockGets
                    [5] oraDbSysFreeBufferInspected
                    [6] oraDbSysFreeBufferRequested
                    [7] oraDbSysParseCount
                    [8] oraDbSysPhysReads
                    [9] oraDbSysPhysWrites
                    [10] oraDbSysRedoEntries
                    [11] oraDbSysRedoLogSpaceRequests
                    [12] oraDbSysRedoSyncWrites
                    [13] oraDbSysSortsDisk
                    [14] oraDbSysSortsMemory
                    [15] oraDbSysSortsRow
                    [16] oraDbSysTableFetchRowid
                    [17] oraDbSysTableFetchContinuedRow
                    [18] oraDbSysTableScanBlocks
                    [19] oraDbSysTableScanRows
                    [20] oraDbSysTableScansLong
                    [21] oraDbSysTableScansShort
                    [22] oraDbSysUserCalls
                    [23] oraDbSysUserCommits
                    [24] oraDbSysUserRollbacks
                    [25] oraDbSysWriteRequests
                [2] oraDbTablespaceTable
                    [1] oraDbTablespaceEntry
                    [1] oraDbTablespaceIndex*
                    [2] oraDbTablespaceName
                    [3] oraDbTablespaceSizeAllocated
                    [4] oraDbTablespaceSizeUsed
                    [5] oraDbTablespaceState
                    [6] oraDbTablespaceLargestAvailebleChunk
                [3] oraDbDataFileDataTable
                    [1] oraDbDataFileEntry
                    [1] oraDbDataFileIndex*
                    [2] oraDbDataFileName
                    [3] oraDbDataFileSizeAllocated
                    [4] oraDbDataFileDiskReads
                    [5] oraDbDataFileDiskWrites
                    [6] oraDbDataFileDiskReadBlocks
                    [7] oraDbDataFileDiskWrittenBlocks
                    [8] oraDbDataFileDiskReadTimeTicks
                    [9] oraDbDataFileDiskWriteTimeTicks
                [4] oraDbLibraryCacheTable
                    [1] oraDbLibraryCacheEntry
                    [1] oraDbLibraryCacheIndex*
                    [2] oraDbLibraryCacheNameSpace
                    [3] oraDbLibraryCacheGets
                    [4] oraDbLibraryCacheGetHits
                    [5] oraDbLibraryCachePins
                    [6] oraDbLibraryCachePinHits
                    [7] oraDbLibraryCacheReloads
                    [8] oraDbLibraryCacheInvalidations
                [5] oraDbLibraryCacheSumTable
                    [1] oraDbLibraryCacheSumEntry
                    [1] oraDbLibraryCacheSumGets
                    [2] oraDbLibraryCacheSumGetHits
                    [3] oraDbLibraryCacheSumPins
                    [4] oraDbLibraryCacheSumPinHits
                    [5] oraDbLibraryCacheSumReloads
                    [6] oraDbLibraryCacheSumInvalidations
                [6] oraDbSGATable
                    [1] oraDbSGAEntry
                    [1] oraDbSGAFixedSize
                    [2] oraDbSGAVariableSize
                    [3] oraDbSGADatabaseBuffers
                    [4] oraDbSGARedoBuffers
                [7] oraDbConfigTable
                    [1] oraDbConfigEntry
                    [1] oraDbConfigDbBlockBuffers
                    [2] oraDbConfigDbBlockCkptBatch
                    [3] oraDbConfigDbBlockSize
                    [4] oraDbConfigDbFileSimWrites
                    [5] oraDbConfigDbMultiBlockReadCount
                    [6] oraDbConfigDistLockTimeout
                    [7] oraDbConfigDistRecoveryConnectHold
                    [8] oraDbConfigDistTransactions
                    [9] oraDbConfigLogArchiveBufferSize
                    [10] oraDbConfigLogArchiveBuffers
                    [11] oraDbConfigLogBuffer
                    [12] oraDbConfigLogCheckpointInterval
                    [13] oraDbConfigLogCheckpointTimeout
                    [14] oraDbConfigLogFiles
                    [15] oraDbConfigMaxRollbackSegments
                    [16] oraDbConfigMTSMaxDispatchers
                    [17] oraDbConfigMTSMaxServers
                    [18] oraDbConfigMTSServers
                    [19] oraDbConfigOpenCursors
                    [20] oraDbConfigOpenLinks
                    [21] oraDbConfigOptimizerMode
                    [22] oraDbConfigProcesses
                    [23] oraDbConfigSerializable
                    [24] oraDbConfigSessions
                    [25] oraDbConfigSharedPool
                    [26] oraDbConfigSortAreaSize
                    [27] oraDbConfigSortAreaRetainedSize
                    [28] oraDbConfigTransactions
                    [29] oraDbConfigTransactionsPerRollback
```

## 监控说明

Oracle 专有数据库 MIB 助记符根 OID 为 iso.org.dod.internet.private.ent-prises.oracle.oraDbMIB。如果您打算编写自己的 SNMP 应用程序，Oracle 专有数据库 MIB 的数字根 OID 为 1.3.6.1.4.1.111.4。

此 MIB 中的许多表条目使用“网络服务”MIB 中的 appIndex 作为索引。

此 MIB 包含若干对性能监控很有用的字段。它们提供诸如块更改次数、用户调用、一致性 Get、块 Get、物理读取、递归调用、用户提交和一致性更改等统计信息。需要定期查询这些数据以建立基线，并能够确定是否存在持续的性能问题。

oraDbSysTable 中的每个条目对应系统上的一个当前数据库实例。该表使用 RDBMS MIB 中的 rdbsDbIndex 作为索引。

oraDbTablespaceTable 中的每个条目代表当前数据库实例内的指定表空间。该表使用 RDBMS MIB 中的 rdbsDbIndex 和 oraDbTablespaceIndex 作为索引。

