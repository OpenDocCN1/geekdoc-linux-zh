+   * applUptime
* applOperStatus
* applLastChange
* applInboundAssociations

Note that although Oracle and other database vendors use this MIB, it is not being used for more traditional network services, such as telnet.

# RDBMS MIB

The Relational Database Management System (RDBMS) MIB contains information that is meant to be generic for all RDBMS systems. This MIB is supported by all the major database vendors. It provides availability information, such as database status and server uptime, and performance information, such as the number of logical database reads.

# MIB Definition

Listing A-10 shows the complete specification for the RDBMS MIB, as defined in RFC 1697.

**Listing A-10**  RDBMS MIB specification.

```
mib_2
    [39]  rdbmsMIB
      [1]  rdbmsObjects
        [10]  rdbmsWellKnownLimitedResources
          [1]  rdbmsLogSpace
        [1]  rdbmsDbTable
          [1]  rdbmsDbEntry
            [1]  rdbmsDbIndex*
            [2]  rdbmsDbPrivateMibOID
            [3]  rdbmsDbVendorName
            [4]  rdbmsDbName
            [5]  rdbmsDbContact
          [2]  rdbmsDbInfoTable
            [1]  rdbmsDbInfoEntry
              [1]  rdbmsDbInfoProductName
              [2]  rdbmsDbInfoVersion
              [3]  rdbmsDbInfoSizeUnits
              [4]  rdbmsDbInfoSizeAllocated
              [5]  rdbmsDbInfoSizeUsed
              [6]  rdbmsDbInfoLastBackup
            [3]  rdbmsDbParamTable
              [1]  rdbmsDbParamEntry
                [1]  rdbmsDbParamName*
                [2]  rdbmsDbParamIndex
                [3]  rdbmsDbParamID
```