This is a classic case in which we experience that a performance bottleneck can arise even when the all the resources on the system are not used.

# Case study 2 - slow database server response

In this case study we examine a problem reported as a slow database server response.

# Problem

Performance tests done on a database server indicate that the expected results are not attained.

# Data for analysis

To troubleshoot the problem, we need to gather and analyze the following information:

+   - sar, vmstat, and iostat outputs
+   - Information about the disk configuration
+   - Oracle statspack output

# Analysis and conclusion

The database used is Oracle. From the Oracle statspack output shown in Figure 5-48 it is clear that the log file sync event is taking a long time to complete. log file sync is the event that writes the updated data in the log buffer into online redo log files when dirty blocks in the dirty buffer are written onto the disks.

Top 5 Timed Events
Event | Waits | Time (s) | Avg wait (ms) | %Total Call Time
log file sync | 960,319 | 1,574 | 2 | 48.7
cr request retry | 900 | 836 | 929 | 25.9
log file parallel write | 514,887 | 316 | 1 | 9.8
CPU time |  | 237 |  | 7.4
gc current block busy | 7,575 | 94 | 12 | 2.9

Figure 5-48 Oracle statspack output

Upon investigation of the disk volume hosting the redo log file, and the disk I/O for that volume, it became clear that logical volume is not striped. Because of this, all the I/O was concentrated on one disk rank and there was a bottleneck. So, striping the volume to multiple ranks solved the issue, since that resulted in distributing the I/O evenly across multiple disk ranks instead of concentrating only on one. This is an example of a performance bottleneck because of an incorrect system configuration.