Using these statistics, the Database Buffer Cache hit ratio would be calculated as:

    $1 - (\frac{(4032 - 206 - 22)}{704252}) = .9945985$

or a 99.46 percent hit ratio.

# # Non-Hit Ratio Performance Measures

Hit ratios are one effective measure of Buffer Cache performance. However, there are also several non--hit ratio measures of Database Buffer Cache performance. These indicators are Buffer Cache--related system statistics found in dynamic performance views and the output from `STATSPACK` and `REPORT.TXT`.

![](bbox=[0.13, 0.38, 0.24, 0.43])

Because these statistics can help guide you toward the true tuning trouble- spot, using them as a starting point for Buffer Cache tuning is often more effective than calculating Buffer Cache hit ratios and blindly increasing the size of the Buffer Cache.

The following system statistics are related to the process of finding a free buffer in the Database Buffer Cache. There are three statistics that measure this activity:

+   *   **Free Buffer Inspected**    Number of Buffer Cache buffers inspected by user Server Processes before finding a free buffer. A closely related statistic is `dirty_buffer_inspected`, which represents the total number of dirty buffers a user process found while trying to find a free buffer.
+   *   **Free Buffer Waits**    Number of waits experienced by user Server Processes during Free Buffer Inspected activity. These waits occur whenever the Server Process had to wait for Database Writer to write a dirty buffer to disk.
+   *   **Buffer Busy Waits**    Number of times user Server Processes waited for a free buffer to become available. These waits occur whenever a buffer requested by user Server Processes is already in memory, but is in use by another process. These waits can occur for rollback segment buffers as well as data and index buffers.

High or steadily increasing values for any of these statistics indicate that user Server Processes are spending too much time searching for, and waiting for access to, free buffers in the Database Buffer Cache.

The `V$SYSSTAT` and `V$SYSTEM_EVENT` dynamic performance views can be used to monitor these secondary indicators of Buffer Cache Performance.