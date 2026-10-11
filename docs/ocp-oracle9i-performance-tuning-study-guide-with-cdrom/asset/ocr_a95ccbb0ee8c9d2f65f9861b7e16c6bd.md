The Alert log will frequently give you a quick indication of whether gross tuning problems exist in the database. Tables that are unable to acquire additional storage, sorts that are failing, and problems with rollback segments are all examples of tuning problems that can show up as messages in the Alert log. Because of this, you should examine your Alert log daily to see if any of these obvious tuning problems exist. Some common Alert log entries that are related to performance tuning issues are shown in Table 2.1. This is not a complete list, and not all of these messages will appear in every Alert log. Some of them can be found in the sample Alert log shown in the previous section.

# TABLE 2.1 Common Alert Log Messages Related to Performance Tuning

| Alert Log Message | Message Description |
| :--- | :--- |
| Unable to Extend Temp Segment by $n$ in Tablespace $x$ | Identified by the error code ORA-01652, this error occurs when a user's Server Process cannot find enough contiguous free space in their temporary tablespace to perform the required sort operation. Tuning of sort activity is discussed in Chapter 8, “Tuning Disk I/O.” |

| Unable to Extend Table $x$ by $n$ in Tablespace $x$ | Identified by the error code ORA-01653, this error occurs when a table segment is attempting to acquire an additional extent, but cannot do so because there is not enough contiguous free space in the tablespace. Extent management is discussed in Chapter 8, “Tuning Disk I/O.” |

| Unable to Extend Rollback Segment $x$ by $n$ in Tablespace $x$ | Identified by the error code ORA-01650, this error occurs when a rollback segment needs to grow, but is unable to because there is insufficient contiguous free space in the tablespace where the rollback segment resides. Rollback segment tuning is discussed in Chapter 8, “Tuning Disk I/O.” |

| Max # Extents $n$ Reached in Table $x$ | Identified by the error code ORA-01631, this error occurs when a table segment needs to grow, but is unable to because it would exceed its maximum allowed number of extents. Segment extent tuning is discussed in Chapter 8, “Tuning Disk I/O.” |