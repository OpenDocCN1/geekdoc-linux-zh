# **Listing 7-5**  MeasureWare alarm definition for an application's CPU utilization.

```
ALARM finance\_app:app\_cpu\_total\_util > 30 FOR 5 MINUTES
START
{
    WARNING ALERT "Your app is busy."
    EXEC "echo 'finance app is very busy'|mailx root"
}
REPEAT EVERY 15 MINUTES
    CRITICAL ALERT "finance app continues to be busy."
END
    RESET ALERT "finance app no longer busy."
```

in an alarm definitions configuration file. You can then decide whether the alarm definitions will generate too many or too few alarms. You can see what messages would have been printed and what programs would have been executed. An alarm summary report shows a count of the number of alarms and the amount of time each alarm would have been active.

MeasureWare's extract command in the utility program can be used to export data to other tools, such as spreadsheet programs. The extract command makes raw log files usable by PerfView as well.

The following application-level metrics are available on HP-UX and Sun Solaris:

+   * CPU use during interval
* Number and rate of physical disk transfers during interval
* Average number of processes in application
* Average number of active processes in application
* Number of application processes that completed during interval
* Runtime of completing application processes
* Average process priority in application
* Standard deviation of process priorities
* CPU use for user processes during interval
* CPU use for system processing
* Main memory use
* Swap space use on disk

These additional application-level metrics are available on HP-UX:

+   * Number and rate of I/O transfers to all devices
* Number of terminal transactions during interval
* Average terminal first-response time
* Average terminal response-to-prompt time
* Number of user-defined transactions during interval