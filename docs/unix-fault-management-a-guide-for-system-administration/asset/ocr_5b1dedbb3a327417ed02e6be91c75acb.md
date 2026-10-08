# Oracle Private Database MIB

Oracle’s Private Database MIB contains additional RDBMS statistics specific to the Oracle7 architecture. It is meant to be used as a supplement to the RDBMS MIB. The majority of the information in this MIB is performance-related.

# MIB Definition

Listing A-11 shows the complete specification for Oracle’s Private Database MIB, as defined by Oracle.

**Listing A-11** Oracle Private Database MIB specification.

```
enterprises

| [111] oracle
| [4 ] oraDbMIB
| [1 ] oraDbObjects
| [1 ] oraDbSysTable
| [1 ] oraDbSysEntry
| [1 ] oraDbSysConsistentChanges
| [2 ] oraDbSysConsistentGets
| [3 ] oraDbSysDbBlockChanges
| [4 ] oraDbSysDbBlockGets
| [5 ] oraDbSysFreeBufferInspected
| [6 ] oraDbSysFreeBufferRequested
| [7 ] oraDbSysParseCount
| [8 ] oraDbSysPhysReads
| [9 ] oraDbSysPhysWrites
| [10] oraDbSysRedoEntries
| [11] oraDbSysRedoLogSpaceRequests
| [12] oraDbSysRedoSyncWrites
| [13] oraDbSysSortsDisk
| [14] oraDbSysSortsMemory
| [15] oraDbSysSortsRow
| [16] oraDbSysTableFetchRowid
| [17] oraDbSysTableFetchContinuedRow
| [18] oraDbSysTableScanBlocks
| [19] oraDbSysTableScanRows
| [20] oraDbSysTableScansLong
| [21] oraDbSysTableScansShort
| [22] oraDbSysUserCalls
| [23] oraDbSysUserCommits
| [24] oraDbSysUserRollbacks
| [25] oraDbSysWriteRequests
| [2 ] oraDbTablespaceTable
| [1 ] oraDbTablespaceEntry
| [1 ] oraDbTablespaceIndex*
```