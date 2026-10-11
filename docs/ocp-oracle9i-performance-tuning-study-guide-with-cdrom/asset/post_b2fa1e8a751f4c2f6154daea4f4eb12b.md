
the redo entries from the Redo Log Buffer. However, the average wait for this event was so short that it appears as an average wait of zero.

## Using OS Utilities to Measure Redo Log Performance

Another way to gather I/O information about the Redo Logs is to use the **V$LOGFILE** view to determine the locations of the Redo Log files and then use an OS utility to monitor I/O on those devices. The Unix utilities **sar** and **iostat** are both useful for monitoring disk I/O on the devices where Redo Logs are located. A brief description of each of these Unix utilities is shown in Table 7.4.

| Utility Name | Description |
| :--- | :--- |
| sar | System Activity Reporter utility. This utility is used to obtain detailed information about the I/O activities against the devices where the Redo Logs are located. |
| iostat | I/O Statistics utility. This utility is also used to monitor I/O activity against the devices where the Redo Logs are located. However, the output from iostat is less verbose than that of the sar utility. |

The output and options for **sar** and **iostat** vary by operating system. For Unix systems, see your Unix **man** pages for complete details on their usage in your environment.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_387_0.png)

Performance Monitor can be used for similar monitoring on Windows 2000 systems, but the output is not as detailed.

## Improving Redo Log Performance

If the above measures indicate Redo Log performance problems, the usual technique for improving their performance is to locate the Redo Logs on the available storage devices in such a way as to minimize contention and maximize throughput.

### **Oracle Objective**

Monitor and tune Redo Logs

### Minimizing Redo Log Contention

One of the easiest ways to ensure that the Redo Logs will not cause any I/O performance issues is to separate them from other database files, like Datafiles, Control Files, and Archive Logs, onto their own devices. For example, separating Redo Logs from Datafiles generally helps performance since the I/O activity of the former is typically sequential and the I/O activity of the latter is random. Separating these disparate I/O patterns can help devices more efficiently perform their I/O activities.

### Maximizing Redo Log Throughput

When the Redo Logs are separated from the other database files as described above, care should also be taken to place them on the fastest devices available. Placing the Redo Logs on fast devices will allow LGWR to perform its writes as quickly as possible. For this reason, it is not recommended that Redo Logs be placed on RAID volumes where write activity incurs additional I/O overhead.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_388_0.png)

> Redo Logs can be created on raw devices in order to maximize throughput.

## Tuning Archiving Operations

The process of *archiving* refers to the copying of the Redo Log files’ contents to a secondary destination so that the archived logs can be used for database recovery in the event of media failure or user error. While this mechanism is an important part of the backup and recovery aspect of administering a database, it can also be a significant source of I/O performance problems and should therefore be monitored and tuned accordingly.

### Measuring the Performance of Archiving

A primary bottleneck for the performance of the Redo Log Buffer is the frequency and efficiency with which the archive background process, ARC0, copies the contents of the Redo Log files to the archive destination when the database is operating in archive log mode. If LGWR needs to write to a Redo Log that is currently being archived by ARC0, LGWR will wait until ARC0 finishes copying the Redo Log’s contents to the archive destination. To reduce the likelihood of this occurrence, LGWR will automatically start additional archive background processes (ARC1, ARC2, etc.) when demands on the system warrant them. However, two areas related to the archiving process can also cause performance problems. Common performance problems issues related to the archiving process are:

- The archive destination fills with archived logs, causing database processing to halt until additional space is made available.
- The ARC0 background process does not keep up with the Redo Log switching activity, causing a wait to occur when the Redo Logs wrap before ARC0 has completed archiving the contents of the log.

These events can be monitored using the `V$ARCHIVE_DEST`, `V$ARCHIVE_PROCESSES`, and `V$SYSTEM_EVENT` dynamic data dictionary views.

### Filling the Archive Location

The location of the archived Redo Log files is specified using the `init.ora` parameter `LOG_ARCHIVE_DEST` or `LOG_ARCHIVE_DEST_n` where *n* is a value between 1 and 10, which allows you to specify up to ten archive destinations for extra assurance of recoverability. When the archive destination becomes full, database processing halts, and an error message is written to the database Alert log. Figure 7.12 shows an example of what this error message looks like.

When this error occurs, the database will remain halted until space is made available in the archive location. You can also temporarily change the archive location using the following command:

```sql
SQL> ALTER SYSTEM ARCHIVE LOG ALL TO
2  '/u04/oradata/PROD' ;
```

Once space is made available in the archive destination, archiving will resume, and a message will be written to the Alert log to indicate that archiving has resumed.

**FIGURE 7.12** Alert log error message when archive destination is full

![](img/832fbc6aca8b6075843ca6f2356c0a8d_390_0.png)

### ARC0 Processes Causing Waits at Log Switch

If the Redo Logs are filling and switching too frequently, LGWR may wrap around and try to write to a Redo Log that has not yet been archived by ARC0. Since a database in archive log mode cannot reuse a Redo Log until it has been archived, LGWR will hang for a moment until the Redo Log has been archived and becomes available. To prevent this, LGWR automatically starts new Archive processes (i.e., ARC1, ARC2, etc.) any time it detects that the current number of Archiver processes is insufficient to keep up with the switching of the Redo Logs. The DBA can also start additional Archiver processes at instance startup by setting the `init.ora` parameter `LOG_ARCHIVE_MAX_PROCESSES` to a value between 2 and 10 (1 is the default).

You can actively monitor the need for additional Archiver processes by querying the `V$ARCHIVE_PROCESSES` dynamic performance view. This view shows the status of each Archiver process and whether it is currently busy or idle.

Additionally, if the log file switch (archiving needed) event appears in the `V$SYSTEM_EVENT` dynamic performance view, LGWR may be held up by the actions of ARC0. This event indicates how often the writing of the contents of the Redo Log Buffer to the Online Redo Log by LGWR was interrupted by a wait for the ARC0 Oracle background process to copy the contents of the Redo Log to the archive destination.

### Improving the Performance of Archiving

If you have identified the archiving mechanisms or ARC0 itself as a performance bottleneck, you can improve the performance of these processes by adding more Redo Logs, making the existing Redo Logs bigger, actively managing the archive destinations, and creating additional ARC0 processes to assist with the archiving process.

## Add More

Every Oracle database must have at least two Redo Log groups. However, by adding additional Redo Log groups to your database, you decrease the likelihood that LGWR will wrap around through all the Redo Logs and back to the one that may still be archiving. There is no magic number of Redo Log groups that is correct for all situations, but between 5 and 20 logs is generally adequate on most online transaction processing systems.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_391_0.png)

> In addition to having an adequate number of Redo Log groups, each group should have at least two members. Having multiple Redo Log members in each group minimizes possible data loss due to the corruption or loss of an Online Redo Log.

## Make It Bigger

In addition to adjusting the quantity of Redo Logs, increasing their size can also cut down on the frequency of log switches and the archiving overhead that comes with them. For the purposes of checkpointing and recoverability, Oracle recommends that a log switch take place approximately every 20 to 30 minutes. However, as we have seen, checkpoint frequency can be tuned using the `FAST_START_MTTR_TARGET` parameters in `init.ora`. Therefore, it is possible to increase the size of your Redo Logs without negatively affecting checkpoint frequency.

## Tune Archive Destinations

There are several `init.ora` parameters that you can use to lessen the likelihood of a database stoppage due to a filled archive location. These parameters allow you to specify multiple, concurrent archive destinations so that database transaction processing can continue even if one of the other locations fills with archive logs.

`LOG_ARCHIVE_DUPLEX_DEST` This parameter is used in conjunction with the `LOG_ARCHIVE_DEST` parameter discussed in the previous section. By setting this parameter, ARC0 is instructed to write archived Redo Logs
