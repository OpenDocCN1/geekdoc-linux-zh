so that they can be properly analyzed and repeated as necessary. Some of the tasks involved include the following:

+   ■ **Monitor the system**  To do this, use
+      ■ **OS tools:** *sar, vmstat, iostat*  These tools can give you valuable information on how the system itself is performing at the OS level. High-level problems might be detected with these tools, such as CPU utilization at 100 percent an overloaded I/O subsystem.
+      ■ **Oracle tools:** *AWR, Statspack, dbastsudiso, v$views*  These tools can provide information on the performance of the Oracle instance and wait events, and on problems within the Oracle instance and application.
+      ■ **Third-party tools**  Third-party tools such as Veritas InDepth can provide information on how the application and SQL statements are performing.
+   ■ **Analyze OS and Oracle configuration parameters**  Analysis of OS and Oracle configuration parameters might highlight a fundamental problem that can be easily solved.

Performance monitoring is much more exciting and interesting than documenting the system configuration; however, documentation is equally important here. If you are saving performance data on the system, be sure to make notations on when that monitoring occurred and what was happening on the system at the time.

# # Step 3: Analyze Results

The goal of the analysis phase is to take the performance monitoring results in conjunction with the initial assessment and use this data to formulate a hypothesis in the next step. Here are some of the tasks involved:

+   ■ **Analyze data**  The data that you have collected during the monitoring phase should be carefully analyzed. You might be surprised at what you find, or it might confirm some suspicion that you might have.
+   ■ **Review error logs**  This is one task that is often overlooked. The error logs can be a valuable source of information in the event of some type of configuration error or hardware failure. Remember, there are more logs than just the Oracle alert log. There are the Linux system logs, /var/log/messages, and the kernel ring buffer (accessed with dmseg). There are also other log files such as the cluster manager log.