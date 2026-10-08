
The MeasureWare agent is installed on individual systems throughout a distributed environment. It collects resource and performance measurement data on the individual systems. The PerfView management console, which you would typically install on a management system, is then used to display the historical MeasureWare data. You could also set alarms that are set off by exception conditions using the MeasureWare agent. For instance, if the MeasureWare agent detects an exception condition, such as CPU utilization greater than 90%, it produces an alarm message. The alarm messages are then displayed with PerfView. We're going to use the PerfView Analyzer in our upcoming examples; however, PerfView consists of the following three components:

- Monitor Provides alarm monitoring capability by accepting alarms from MeasureWare and displays alarms. This is not part of the base PerfView product.
- Planner Provides forecasting capability by extrapolating MeasureWare data for forecasts. This is not part of the base PerfView product.
- Analyzer Analyzes MeasureWare data from multiple systems and displays data. You can view the data from multiple systems simultaneously. This is the base product.

In our example, we will be working with a single system. We'll take the MeasureWare data, collected over roughly a one-week period, and display some of it. In this example, we won't take data from several distributed systems and we'll use only one server in the example.

HP MeasureWare Agent produces log files that contain information about the system resource consumption. The longer HP MeasureWare Agent runs, the longer it records data in the log files. I am often called to review systems that are running poorly to propose system upgrades. I usually run HP MeasureWare Agent for a minimum of a week so that I obtain log information over a long enough period of time to obtain useful data. For some systems, this time period is months. For other systems with a regular load, a week may be enough time.

After having run MeasureWare for a week, I invoked PerfView to see the level of system resource utilization that took place over the week. The graphs we'll review are CPU, Memory, and Disk. Figure 13-9 shows Global CPU Summary for the week.

![](img/75f39fc91296b889c0653851accdfd46_947_0.png)

Figure 13-9 HP PerfView Global CPU Summary

You can adjust every imaginable feature of this graph with PerfView. Unfortunately, the color in this graph is lost in the book. The colors used allow you to discern the parameters when viewing the graph on the computer screen. Total CPU utilization is always the top point in the graph and it is the sum of system and user mode utilization.

Figure 13-9 shows classic CPU utilization with prime hours reflecting high CPU utilization and non-prime hours reflecting low CPU utilization. In some respects, however, this graph can be deceiving. Because there is a data point occurs every three hours, hence the eight ticks per 24-hour period, you don’t get a view of the actual CPU utilization during a much smaller window of time. We can’t, for instance, see precisely what time in the morning the CPU becomes heavily used. We can see that it is between the second and third tick, but this is a long time period - between 6:00 and 9:00 am. The same lack of granularity is true at the end of the day. We see a clear fall-off in CPU utilization between the fifth and seventh ticks, but this does not give us a well defined view. Figure 13-10 shows CPU utilization during a much shorter time window.

![](img/75f39fc91296b889c0653851accdfd46_948_0.png)

Figure 13-10 HP PerfView Global CPU Summary - Short Time Period

Figure 13-10 shows a finer granularity of CPU utilization during the shorter time window. The much finer granularity of this window makes clear the activity spikes that occur throughout the day. For instance, a clear login spike occurs at 8:30 am.

Memory utilization can also be graphed over the course of the week, as shown in Figure 13-11.

![](img/75f39fc91296b889c0653851accdfd46_949_0.png)

The user memory utilization is the bottom line of the graph, which roughly corresponds to the CPU utilization shown earlier. User memory utilization is low during non-prime hours and high during prime hours.

System memory utilization is the middle line of the graph, which remains fairly steady throughout the week.

Total memory utilization is always the top line of the graph, and it is the sum of system and user utilization. It rises and drops with user utilization, because system memory utilization remains roughly the same.

The three-hour interval between data points on this graph may not give us the granularity we require. Figure 13-12 shows memory utilization during a much shorter time window.

![](img/75f39fc91296b889c0653851accdfd46_950_0.png)

Figure 13-12 HP PerfView Global Memory Summary - Short Time Period

Figure 13-12 shows a finer granularity of memory utilization during the shorter time window. You can now see precisely how memory utilization is changing over roughly one day.

Disk utilization can also be graphed over the course of the week, as shown in Figure 13-13.

![](img/75f39fc91296b889c0653851accdfd46_951_0.png)

Figure 13-13 HP PerfView Global Disk Summary

Like the CPU and memory graph, this is an entire week of disk usage. Because many spikes occur on this graph, we would surely want to view and analyze much shorter time windows.

Figure 13-14 shows disk utilization during a much shorter time window.

![](img/75f39fc91296b889c0653851accdfd46_952_0.png)

Figure 13-14 HP PerfView Global Disk Summary - Short Time Period

This much shorter time window, of roughly three hours, shows a lot more detail. There are tremendous spikes in disk activity occurring in the middle of the night. These could take place for a variety of reasons, including batch job processing or system backup.

You are not limited to viewing parameters related to only one system resource at a time. You can also view the way many system resources are used simultaneously, as shown in Figure 13-15.

![](img/75f39fc91296b889c0653851accdfd46_953_0.png)

Many system resources are present on this graph, including CPU, disk, and memory. You would surely want to view a much shorter time period when displaying so many system resources simultaneously.

Figure 13-16 shows the same parameters during a much shorter time window.

![](img/75f39fc91296b889c0653851accdfd46_954_0.png)

Figure 13-16 HP PerfView *Global Summary* - Short Time Period

Figure 13-16 shows a finer granularity of the utilization of many system resources during the shorter time window. You can now view the ways in which various system resources are related to other system resources.

You can find the status of PerfView running on your system with a useful command called **perfstat**. The following example shows issuing the **perfstat** command with the *-?* option to see all perfstat options:

```
# perfstat -?

usage: perfstat [options]

    Unix option  Function
    ------------  -------------------------
    -?             List all perfstat options.
    -c             Show system configuration information.
    -e             Search for warnings and errors from
                   performance tool status files.
    -f             List size of performance tool status files.
    -p             List active performance tool processes.
    -t             Display last few lines of performance tool status files.
    -v             List version strings for performance tool files.
    -z             Dump perfstat info to a file and tar tape.
```

Using the -c option, you get information about your system configuration, as shown in the following listing:

```
# perfstat -c
*************( start of perfstat -c output ) ************
** perfstat for rp-ux6 on Fri May 15 12:20:06 EDT
*************( start of perfstat -c output ) ************
system configuration information:
uname -a: HP-UX ux6 B.11.00 E 9000/800 71763 8-user license
mounted file systems with disk space shown:
Filesystem	kbytes	used	avail %used Mounted on
/dev/vg00/lvol3	86016	27675	54736	34% /
/dev/vg00/lvol1	67733	44928	16031	74% /stand
/dev/vg00/lvol8	163840	66995	90927	42% /var
/dev/vg00/lvol7	499712	358775	132155	73% /usr
/dev/rp06vgtmp/tmp	4319777	1099297	3134084	26% /tmp
/dev/vg00/lvol6	270336	188902	76405	71% /opt
/dev/vgroot1/var	640691	15636	605834	3% /newvar
/dev/vgroot1/usr	486677	356866	115210	76% /newusr
/dev/vgroot1/stand	67733	45109	15850	74% /newstand
/dev/vgroot1/root	83733	21181	54178	28% /newroot
/dev/vgroot1/opt	263253	188109	67246	74% /newopt
/dev/vg00/lvol5	20480	1109	18168	6% /home
LAN interfaces:
Name	Mtu	Network	Address	Ipkts	Opkts
lo0	4136	127.0.0.0	localhost	7442	7442
lan0	1500	192.60.11.0	rp-ux6	7847831	12939169
*************( end of perfstat -c output ) ************
```
