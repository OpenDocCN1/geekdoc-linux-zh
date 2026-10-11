+   11. C. If the number of background checkpoints started and number of background checkpoints completed differ by more than 1, checkpoints are not always completing before the next one begins.

+   12. C. This parameter specifies the desired mean time to recover an instance. From this measure, Oracle can then perform checkpointing sufficient to accommodate this requirement.

+   13. B. The ratio of Redo Log Buffer entries to Redo Log Buffer retries should be less than 1 percent.

+   14. D. Another option for improving the performance of the Redo Log Buffer is to improve the speed of Redo Log archiving.

+   15. B. Regular application DML is still recorded in the Redo Log Buffer even if a table is a NOLOGGING table.

+   16. A. The V$SYSTEM_EVENT view contains information about Online Redo Log performance. The statistics to take note of are log file switch complete and log file parallel write.

+   17. D. The size of the Redo Log Buffer is specified in bytes using the LOG_BUFFER parameter in init.ora.

+   18. B. Because checkpoints occur on log switches, increasing the size of the Redo Logs will decrease the frequency of checkpoints. This is one technique to manage the checkpoint frequency.

+   19. B. The LGWR background process writes the contents of the Redo Log Buffer to the Online Redo Log when the buffer is one-third full. This helps ensure that space will always be available for subsequent transactions.

+   20. C, D. The two valid values are ENABLE and DEFER. When set to ENABLE, the Archiver process will write archive logs to the corresponding LOG_ARCHIVE_DEST_n destination. When set to DEFER, the Archiver process will not write archive logs to the corresponding LOG_ARCHIVE_DEST_n destination until the value is changed to ENABLE.