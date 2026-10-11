Figure 7.5 shows a sample query on V$SYSTEM_EVENT showing the waits related to checkpoint activities that have occurred in the database.

# FIGURE 7.5 Checkpoint activity shown in V$SYSTEM_EVENT

```
SQL> SELECT event, total_waits, average_wait
   2  FROM V$SYSTEM_EVENT
   3  WHERE event LIKE '%check%'
   4  or event LIKE '%log file switch%';

EVENT                          TOTAL_WAITS AVERAGE_WAIT
checkpoint completed              1         10
log file switch (checkpoint incomplete) 54         38
```

Two events found in the V$SYSTEM_EVENT view are indicators of checkpoint performance: checkpoint completed and log file switch (checkpoint incomplete).

**Checkpoint Completed** This event shows how often waits occurred for the checkpoint to complete its activities. High or steadily increasing values for this event indicate that checkpoints need to be tuned. The output in Figure 7.5 shows that one **Checkpoint Complete** event had to wait 10 hundredths of a second to complete.

**Log File Switch (Checkpoint Incomplete)** This event shows how often the Online Redo Log switched from one log to the next, before the checkpoint from the previous log switch had time to complete. When this occurs, the in-progress checkpoint is abandoned and a new checkpoint is begun. Because incomplete checkpoints cause excess I/O that do not provide any recovery benefits, frequent occurrences of this event indicate that checkpoint activity should be tuned. The output from Figure 7.5 shows that log switches that lead to incomplete checkpoints occurred 54 times, experiencing an average wait of 38 hundredths of a second.

Another indicator of checkpoint performance can be found in the V$SYSSTAT dynamic performance view. Two statistics, **background checkpoints started** and **background checkpoints completed**, can be used to determine whether all the checkpoints that were started, actually completed. Discrepancies between these two statistics indicate that checkpoints are starting, but not completing. As with the **log file switch (checkpoint incomplete)** event, this situation occurs anytime checkpoints are occurring too closely together. Figure 7.6 shows an example of this problem using the V$SYSSTAT dynamic performance view.