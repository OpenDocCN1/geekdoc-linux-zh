# Data for analysis

To troubleshoot the problem, we need to gather and analyze the following information:

+   - sar output
+   - vmstat output
+   - iostat output

# Analysis and conclusion

Figure 5-45 shows the graph prepared from the vmstat output. From this graph, it is apparent that there are times at which all the CPUs are not being utilized. This is not because the other processes are utilizing the CPU but because of the application limitation.

![](bbox=[0.3, 0.48, 0.88, 0.78])

Figure 5-45 CPU utilization report based on the vmstat output