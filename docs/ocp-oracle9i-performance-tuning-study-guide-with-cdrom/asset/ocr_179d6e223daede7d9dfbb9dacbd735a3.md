following query shows that this database has three undo tablespaces, the default undo tablespace UNDOTBS, and two other undo tablespaces, UNDO and RBS:

```
SQL> SELECT tablespace_name, contents
2  FROM dba_tablespaces;
```

| TABLESPACE_NAME | CONTENTS |
| :-- | :-- |
| SYSTEM | PERMANENT |
| UNDOTBS | UNDO |
| APPL_IDX | PERMANENT |
| APPL_TAB | PERMANENT |
| TEMP | TEMPORARY |
| TOOLS | PERMANENT |
| USERS | PERMANENT |
| OEM_REPOSITORY | PERMANENT |
| UNDO | UNDO |
| RBS | UNDO |

# USING V$UNDOSTAT TO MANAGE UNDO TABLESPACES

The V$UNDOSTAT dynamic performance view can be used to monitor the usage of the system-managed undo tablespace. This view contains historical statistics, presented as a histogram. Each row in the V$UNDOSTAT view stores undo statistics from a previous 10-minute interval. Table 8.10 describes selected columns from this view.

# TABLE 8.10 Descriptions of Selected V$UNDOSTAT Columns

| Column Name | Description |
| :-- | :-- |
| BEGIN_TIME | Time and date when the undo statistics monitoring period began. |
| END_TIME | Time and date when the undo statistics monitoring period ended. |
| UNDOTSN | The ID of the tablespace where the undo activity took place. Can be joined to V$TABLESPACE on the TS# column in order to determine the name of the tablespace. |