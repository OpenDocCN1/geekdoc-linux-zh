activity against the Redo Logs. However, the **V$SYSTEM_EVENT** dynamic performance view and selected OS utilities can be useful when monitoring Redo Log performance.

Monitor and tune Redo Logs

# ### Using V$SYSTEM_EVENT to Measure Redo Log Performance

As with checkpoint performance, the **V$SYSTEM_EVENT** table can also be used to monitor the activity of the Redo Logs. Two events, **logfile switch completion** and **logfile parallel write**, can be good indicators of Redo Log performance.

**Log File Switch Completion** This event indicates the amount of time that LGWR waited for a log switch to complete. High or increasing values for this event indicate that Redo Logs may be a performance bottleneck.

**Log File Parallel Write** This event indicates how long it took for LGWR to write the redo entries from the Redo Log Buffer to the Online Redo Logs. High or increasing values for this event can indicate that the Redo Logs are a performance bottleneck.

Figure 7.11 shows a sample query on **V$SYSTEM_EVENT**, checking for occurrences of these two events.

# **FIGURE 7.11** Redo Log activity shown in V$SYSTEM_EVENT

```
```sql
1 SQL> SELECT event, total_waits, average_wait
2   FROM v$system_event
3  WHERE event = 'log file switch completion'
4    or event = 'log file parallel write';
```
```
 EVENT              TOTAL_WAITS  AVERAGE_WAIT
 ------------------- ----------- -------------
 log file parallel write         71041            0
 log file switch completion        57           38
```
```

The output from this query shows that 57 waits for log files to complete their switching have occurred since instance startup. The average time spent waiting for those log switches to complete is 38 hundredths of a second. The query also shows that 71,041 waits have occurred for LGWR to write