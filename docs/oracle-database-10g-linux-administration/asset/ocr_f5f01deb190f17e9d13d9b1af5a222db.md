# Monitoring the Undo Tablespace

In order to find out what the undo rate is, you can monitor the dynamic performance view, V$UNDOSTAT. Some of the data that is of particular interest is

| Parameter | Meaning |
| :--- | :--- |
| BEGIN_TIME | The time when the measurement interval began. |
| END_TIME | The time when the measurement interval ended. |
| TXNCOUNT | The total number of transactions committed during the measurement interval. |
| UNDOBLKS | The number of undo blocks that were consumed during the measurement interval. |
| SSOLDERRCNT | The number of OER errors that have occurred during the measurement interval. If this is high, the undo retention period should be re-evaluated. |
| NOSPACEERRCNT | Specifies the number of OER errors that have occurred for this instance. If this is high, the size of the undo tablespace should be reevaluated. |

If you are seeing non-zero values for the error counts, you can do one of two things: lower the retention period or increase the size of the undo tablespace.

# Tuning the Retention Period

The retention period allows you to specify how long undo information is retained. The parameter `UNDO_RETENTION` is specified in seconds. The length of time that undo information is retained is 30 seconds, by default. This is probably sufficient. If you feel that undo information needs to be retained longer, you can increase this value.

Increasing the retention periods allows undo information to be kept longer so that long-running transactions that require a consistent view of data have a better chance of finishing. If you receive the error message “snapshot too old,” increasing the undo retention period will reduce this.

# Rollback Segments or Rollback Segment Undo (RBU) Mode

Rollback segments record transactional information that may be used in the event that the transaction should be rolled back. They are also used to provide read consistency and enable database recovery. Since rollback segments were made obsolete in Oracle9i, they will not be covered here.