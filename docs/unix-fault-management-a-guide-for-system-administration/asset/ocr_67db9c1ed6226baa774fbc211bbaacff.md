| Variable | MIB Table | Description |
| :--- | :--- | :--- |
| appUptime | appTable | Length of time database has been running |
| appOperStatus | appTable | Status of database server |
| appInboundAssociations | appTable | Number of currently active local and remote conversations |
| rdbmsSrvInfoStartupTime | rdbmsSrvInfoTable | Timestamp of last server restart |
| rdbmsSrvInfoFinished-Transactions | rdbmsSrvInfoTable | Number of transactions committed or aborted |
| rdbmsSrvInfoDiskReads | rdbmsSrvInfoTable | Number of physical reads by server |
| rdbmsSrvInfoLogicalReads | rdbmsSrvInfoTable | Number of logical reads by server |
| rdbmsSrvInfoDiskWrites | rdbmsSrvInfoTable | Number of physical writes by server |
| rdbmsSrvInfoLogicalWrites | rdbmsSrvInfoTable | Number of logical writes by server |
| rdbmsSrvInfoHighWater-InboundAssociations | rdbmsSrvInfoTable | Greatest number of simultaneous inbound associations handled by server |
| rdbmsSrvMaxInbound-Associations | rdbmsSrvInfoTable | Maximum number of simultaneous inbound associations allowed |
| rdbmsDbInfoSizeAllocated | rdbmsDbInfoTable | Disk space allocated for this database |
| rdbmsDbInfoSizeUsed | rdbmsDbInfoTable | Disk space actually used by this database |
| rdbmsRelState | rdbmsRelTable | Status of database |

physical reads can be used to determine the appropriate cache size, for example. However, the information in the server info table is aggregated for the database server, so database-specific statistics are not available here (unless the database server is handling only one database). The database relation table is used to match a database to its server.

If you want to monitor Informix, the rdbmsSrvLimitedResource table is useful, because it contains current resource limits and thresholds reached. This table is not supported for Oracle. Other interesting variables in the RDBMS MIB not generally available for Oracle, but available for Informix, include:

+   - rdbmsDbInfoLastBackup: Indicates the timestamp of the last database backup.
- rdbmsSrvInfoOutOfSpaces: Indicates the number of times the database server has been unable to obtain the disk space that it wanted.
- rdbmsRelActiveTime: Indicates the time this database was made active by the database server.

Because MIB definitions rarely change, after you configure some MIB variables to be monitored, the configuration is likely to work with multiple database versions. This can help to reduce the burden of recertification for a new database software release.