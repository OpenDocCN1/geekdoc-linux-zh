parameter, Oracle will perform additional checkpoints, beyond the ones performed at a log switch, in order to ensure that the checkpoints are happening frequently enough to meet the recovery target. This parameter is superseded by the FAST_START_IO_TARGET and LOG_CHECKPOINT_INTERVAL parameters if they are configured. However, both of these parameters are backward compatible Oracle8i parameters that are now deprecated in favor of the Oracle9i FAST_START_MTTR_TARGET parameter. The FAST_START_MTTR_TARGET can be set dynamically using the ALTER SYSTEM command or manually in init.ora. The default value for FAST_START_MTTR_TARGET is zero, which has the effect of disabling its functionality.

![](bbox=[0.13, 0.33, 0.25, 0.42])

**NOTE**

The FAST_START_MTTR_TARGET parameter is useful when Service Level Agreements dictate the maximum allowable outage related to an instance failure.

Once the FAST_START_MTTR_TARGET parameter is set, you use the V$INSTANCE_RECOVERY view to monitor its effectiveness. Selected columns from the V$INSTANCE_RECOVERY view which are related to this parameter are shown in Table 7.3.

# **TABLE 7.3** Descriptions of Selected Columns in V$INSTANCE_RECOVERY

| Column Name | Description |
| :--- | :--- |
| TARGET_MTTR | Indicates the target Mean Time to Recover. This will usually match the value specified in the init.ora, but may be slightly higher if limited system resources will not allow the specified target to be maintained. |
| ESTIMATED_MTTR | Indicates the estimated mean time to recover the instance if it were to fail at that moment. |


Using these columns, we can determine if our objectives for instance recovery times are being maintained:

```
SQL> SELECT target_mttr, estimated_mttr
2 FROM v$instance_recovery;
TARGET_MTTR ESTIMATED_MTTR
------------ ----------------
218 12
```