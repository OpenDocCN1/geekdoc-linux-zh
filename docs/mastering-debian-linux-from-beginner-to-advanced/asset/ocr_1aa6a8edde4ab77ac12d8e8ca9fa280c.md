To run iostat:

```
iostat
```

Key features of iostat:

+   CPU statistics: Displays CPU utilization report.  
+    Device utilization: Shows I/O statistics for each device.  
+    Extended options: Provides detailed reports with additional flags.

Useful iostat options:

+   - -c: Display CPU utilization report only.  
+   - -d: Display device utilization report only.  
+   - -x: Display extended statistics.  
+   - -p: Display statistics for block devices and all their partitions.

Example usage:

```
iostat -x 5 3
```

This command will display extended statistics every 5 seconds for 3 iterations.

# # Other Useful Monitoring Tools

+   vmstat: Reports information about processes, memory, paging, block I/O, traps, and CPU activity.