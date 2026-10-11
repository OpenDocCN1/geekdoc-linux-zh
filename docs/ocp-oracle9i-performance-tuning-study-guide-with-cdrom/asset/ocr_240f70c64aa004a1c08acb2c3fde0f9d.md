![](bbox=[0.12, 0.13, 0.22, 0.19])

Latch behavior differs on single and multiple CPU servers. On a single CPU server, a process requesting an in-use latch will release the CPU and sleep before trying the latch again. On multiple CPU servers, a process requesting an in-use latch will “spin” on the CPU a specific number of times before releasing the CPU and trying again. The number of spins the process will use is OS specific.

The following sections will show you how to detect latch contention if it is occurring in the instance.

# ### Measuring Latch Contention

Several sources of information on the performance of latches are available. These sources include the V$LATCH dynamic performance view, the output from STATSPACK and REPORT.TXT, and the OEM Performance Manager. However, before examining any of these sources, you should determine if latch contention is even occurring in your instance using the V$SYSTEM_EVENT dynamic performance view. Latch contention can be detected by examining the V$SYSTEM_EVENT view for occurrences of the latch free event. The following query shows a query that can be used for this purpose:

```
```
SQL> SELECT event, total_waits, time_waited
  2  FROM v$system_event
  3  WHERE event = 'latch free';
```
```

```
```
EVENT     TOTAL_WAITS TIME_WAITED
--------- ------------- -----------
latch free     59          22
```
```

The query shows that 59 latch-related wait events have occurred in the instance since startup. The total time spent waiting for these latches was 22 hundredths of a second.

**Oracle Objectives**

Diagnose contention for latches

Tune the appropriate resources to minimize latch contention