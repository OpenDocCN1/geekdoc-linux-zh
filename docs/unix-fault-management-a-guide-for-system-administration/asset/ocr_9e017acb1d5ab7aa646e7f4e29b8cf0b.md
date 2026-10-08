One rdbmsDbTable entry is likely to correspond to multiple tablespace table entries. For example, addition to indicating the amount of space allocated and in use, the state variable oraDbTablespaceState indicates whether the tablespace is offline or accessible.

The oraDbDataFileTable keeps track of the number of disk reads and writes being made to a data file. The oraDbConfigTable stores important database configuration parameters, such as **DB\_BLOCK\_BUFFERS**, which is used to determine the buffer cache size.

The oraDbLibraryCacheTable keeps track of performance data about the library cache. Variables in this table, such as oraDbLibraryCachePins and oraDbLibraryCacheReloads, can be used to calculate the library cache miss rate. Each table entry represents a given library cache within a current database instance on the system. The oraDbLibraryCacheSumTable provides summary information for all the library caches in a database instance.

# ## Oracle Network Listener MIB

The Oracle Network Listener MIB is a protocol-independent application that receives connection requests from remote database users. Oracle provides a private Network Listener MIB that includes additional information about the current status of the listener process.

# ### MIB Definition

Listing A-12 shows the complete specification for Oracle's private Network Listener MIB, as defined by Oracle.

**Listing A-12** Oracle Network Listener MIB specification.

```
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
         [5 ] oraSIDTable
```