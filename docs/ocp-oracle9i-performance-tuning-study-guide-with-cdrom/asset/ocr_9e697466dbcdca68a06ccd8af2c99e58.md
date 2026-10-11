# Explain how the Alert log file is used

The name of the Alert log varies by operating system. On Unix systems, it follows the naming convention of **alert_SID_log**. On Windows 2000 systems, it follows the naming convention of **SIDalert.log**. In both cases, _SID_ represents the name of the Oracle instance the Alert log belongs to. A sample Alert log from a Windows 2000 Oracle*9i* Server is shown in Figure 2.1.

# **FIGURE 2.1**  Sample section of Alert log file

```
```
Recovery of Online Redo Log; Thread 1 Group 3 Seq 591 Reading  
Mem# 0 errs 0; D:\ORACLE-ORADATA-PROD-REDO03A.RDO
Mem# 1 errs 0; D:\ORACLE-ORADATA-PROD-REDO03B.RDO
Mon Jan 14 18:18:50 2002
Ended recovery at
Thread 1: logseq 591, block 7761, scn 0.1741975
494 data blocks read, 494 data blocks written, 8192 redo blocks read
Crash recovery completed successfully
Mon Jan 14 18:22:50 2002
  Successful open of redo thread 1.
Mon Jan 14 18:48:50 2002
SMON: enabling cache recovery
Mon Jan 14 18:48:54 2002
Undo Segment 11 Onlined
Undo Segment 12 Onlined
Undo Segment 13 Onlined
Undo Segment 14 Onlined
Undo Segment 15 Onlined
Undo Segment 16 Onlined
Undo Segment 17 Onlined
Undo Segment 18 Onlined
Undo Segment 19 Onlined
Undo Segment 20 Onlined
Successfully onlined Undo Tablespace 12.
Mon Jan 14 18:48:54 2002
SMON: enabling tx recovery
Thread 1 advanced to log sequence 588
  Current log# 3 seq# 588 mem# 0: D:\ORACLE-ORADATA-PROD-REDO03A.RDO
  Current log# 3 seq# 588 mem# 1: D:\ORACLE-ORADATA-PROD-REDO03B.RDO
  Thread 1 advanced to log sequence 589
  Current log# 1 seq# 589 mem# 0: D:\ORACLE-ORADATA-PROD-REDO01A.RDO
  Current log# 1 seq# 589 mem# 1: D:\ORACLE-ORADATA-PROD-REDO01B.RDO
Errors in file d:\oracle\admin\PROD\bdump\prodsm00.TRC:
ORA-11556: error freeing extent (2) of rollback segment (18)
ORA-01554: attempt to wrap into rollback segment (18) extent (2) which is being freed
  Thread 1 advanced to log sequence 590
  Current log# 2 seq# 590 mem# 0: D:\ORACLE-ORADATA-PROD-REDO02A.RDO
  Current log# 2 seq# 590 mem# 1: D:\ORACLE-ORADATA-PROD-REDO02B.RDO
Mon Jan 14 19:58:53 2002
Errors in file D:\oracle\admin\PROD\bdump\prodpm01.TRC:
ORA-00600: internal error code, arguments: [1100], [0x37FE97E8], [ ], [ ], [
```
```