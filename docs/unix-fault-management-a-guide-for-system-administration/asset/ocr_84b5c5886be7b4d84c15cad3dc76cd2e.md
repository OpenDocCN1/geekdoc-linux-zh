![](bbox=[0.03, 0.13, 0.97, 0.16])

```

```pascal
{Alarm Network_Bottleneck > 90 for 2 minutes
start
    if Network_Bottleneck > 90 then
        red alert "Network Bottleneck possibility: Network_Bottleneck %"
        yellow alert "Network Bottleneck possibility %: Network_Bottleneck %"
repeat every 10 minutes
if Network_Bottleneck > 90 then
    red alert "Network Bottleneck probability %: Network_Bottleneck %"
    yellow alert "Network Bottleneck probability %: Network_Bottleneck %"
end
reset alert "End of Network Bottleneck Alert"

# The following alarm system that a red activated only for error percent
 alarm CBL_NET_ERROR_1_MIN_RATE > 10
 start
    white alert "Network error rate is over 10% for one minute"
end
reset alert "End of non-zero network error rate condition"

# The following are system table alarms. If swap overhead is a concern, and
# you find you will not have enough table utilization, you can use these.
# To delete these alarms

# Global swap space utilization alarm
 alarm CBL_SWAP_SPACE_UTIL > 95
 start
    red alert "Global swap space is nearly full"
end
...
```

```

GlancePlus can be launched from the command line, or you can start it from the Performance Monitors functional area in SAM (on HP-UX).

# PerfView

PerfView is a graphical performance monitoring tool that is used to monitor the performance and system resource utilization for multiple systems in your environment. A variety of performance graphs can be displayed. The graphs are based on data collected over a period of time, unlike the real-time graphs of GlancePlus. PerfView can show graphs from multiple systems simultaneously, so that comparisons can be made.

PerfView is integrated with other monitoring tools. For example, you can launch GlancePlus from within PerfView by accessing the Tools menu. And, PerfView can be launched from the IT/O Applications Bank. When troubleshooting an event in the IT/O Message Browser window, you can launch PerfView to see a related performance graph.

PerfView relies on MeasureWare data, so it can display performance information only for systems that support the MeasureWare Agent. Refer to the previous section on MeasureWare to see a list of the disk metrics available.