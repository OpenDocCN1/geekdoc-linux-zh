Comment: DB2 BACKUP ITSODB OFFLINE
Start Time: 20021028162533
End Time: 20021028162555
00006 Location: /db2home

# 5.1.2 Enable incremental backup

DB2 supports incremental and delta backups which is a copy of all data pages that have been updated since the last backup. To enable incremental or delta backup, you need to set the TRACKMOD database configuration parameter to ON, as shown:

```
db2 update db cfg for itsodb using TRACKMOD on
```

In a multi-partitioned environment you have to do this on each database partition. Once the TRACKMOD is set to ON, you need to do a full database backup once before starting incremental/delta backup. This mode only becomes active after a full backup of the database has been performed.

# 5.1.3 Enable usage of TSM

DB2 supports database backups and archive log backups using TSM storage. The TSM system consists of TSM server and TSM client. Our test was based on the following configuration:

+   - Server: WIN 2000 server with TSM server version 4.2.1
+   - Client: Linux SuSE V8.1 with TSM client version 4.2.3

Each host has to be registered on a TSM server.

![](bbox=[0.25, 0.84, 0.9, 0.92])

Figure 5-4 Registered clients on TSM server