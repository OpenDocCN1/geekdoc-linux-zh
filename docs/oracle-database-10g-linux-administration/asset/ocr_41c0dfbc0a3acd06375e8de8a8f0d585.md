database. There are a number of ways that the standby database can be monitored. These include the following Oracle tables and dynamic performance views:

+   - **DBA_LOGSTDBY_LOG**  This table provides information on redo log files that were registered on the standby system.
+   - **DBA_LOGSTDBY_PROGRESS**  This table provides statistics on the overall progress of SQL Apply.
+   - **V$LOGSTDBY_STATS**  This view provides information on LogMiner statistics.
+   - **V$LOGSTDBY**  Provides a snapshot of information about the log Apply process.

As with a physical standby database, you can change the data protection mode. These are the same data protection modes that are used with the physical standby database (described earlier) and are maximum protection, maximum availability, and maximum performance.

In addition to setting the data protection mode, it is always a good idea to test and verify the operation of the standby database.

# ## Summary

In addition to the information provided here, there is much more that can be configured and tuned with Oracle Data Guard. There are many options and many modes of operation that can be configured. How you configure your system depends on your needs and requirements. As with many Oracle features such as Oracle RAC, deploying Data Guard in a Linux environment is all about the details. Careful planning and testing will make your deployment successful.