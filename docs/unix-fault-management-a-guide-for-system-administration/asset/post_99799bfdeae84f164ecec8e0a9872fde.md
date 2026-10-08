
- Number of aborted transactions
- Response time of aborted transactions

Figure 7-3 shows how transaction information can be shown together with a service-level objective. The administrator wants to achieve transaction response times under five seconds. The graph shows the number and distribution of transactions that are meeting or exceeding the objective.

More than 600 metrics are accessible from GlancePlus. Some of these metrics are discussed in other chapters. The complete list of metrics can be found by using the online help facility. This information can also be found in the directory `/opt/perf/paperdocs/gp/C`. For further information, visit the HP Application and System Management Web site at `http://www.openview.hp.com/solutions/application/`.

## PerfView

PerfView is a graphical performance analysis tool from Hewlett-Packard. It is used to graphically display performance and system resource utilization for one system or for multiple systems simultaneously, so that comparisons can be made. A variety of performance graphs can be displayed. The graphs are based on data collected over a period of time, unlike the real-time graphs of GlancePlus. This tool runs on HP-UX or NT systems and works with data collected by MeasureWare agents.

**Figure 7-3** GlancePlus shows transaction data.

![](img/eae88b61ada165139a1d9b546a34140b_226_0.png)

PerfView has three main components:

- **PerfView Monitor**: Provides the ability to receive alarms. A textual description of an alarm can be displayed. Alarms can be filtered by severity, type, or source system. Also, after an alarm is received, the alarm can be selected, which displays a graph of related metrics. An operator can monitor trends leading to failures, and can then take proactive actions to avoid problems. Graphs can be used for comparison between systems and to show a history of resource consumption. An internal database is maintained that keeps a history of alarm notification messages.
- **PerfView Analyzer**: Provides resource and performance analysis for disks and other resources. System metrics can be shown at three different levels: process, application (configured by the user as a set of processes), and global system information. It relies on data received from MeasureWare agents on the managed nodes. Data can be analyzed from up to eight systems concurrently. All MeasureWare data sources are supported. PerfView Analyzer is required by both PerfView Monitor and PerfView Planner.
- **PerfView Planner**: Provides forecasting capability. Graphs can be extrapolated into the future. A variety of graphs (such as linear, exponential, s-curve, and smoothed) can be shown for forecasted data.

In addition to graphing and analyzing system resources, process and application resources can be graphed and analyzed using PerfView. PerfView can use the application definitions created by MeasureWare. PerfView can then be used to show a history of a specified application’s utilization. PerfView’s ability to show history and trend information can be helpful in diagnosing system problems. Graphing performance information can help you to understand whether a persistent problem exists or an anomaly is simply a momentary spike of activity.

To diagnose a problem further, PerfView Monitor can allow the user to change time intervals, to try to find the specific time a problem occurred. The graph is redrawn showing the new time period.

## Process Resource Manager

The Process Resource Manager is a resource management tool from Hewlett-Packard that is used to balance system resources among PRM groups. PRM groups are configured by the administrator and consist of a set of HP-UX users or applications. PRM is then used to give each PRM group a certain percentage of the CPU, real memory, or disk I/O bandwidth available on the system. PRM ensures that each PRM group gets a minimum percentage of the system’s resources, even during heavy loads. PRM can also ensure that a group does not get more than a configured percentage of the CPU.

PRM can be used in conjunction with HP GlancePlus to adjust the system configuration. For example, if an administrator detects unwanted system load for a PRM group, GlancePlus can be used to lower that group’s entitlement dynamically.

The PRM configuration file is /etc/prmconf. In this file, you specify the PRM groups and their desired resource entitlements. Both HP-UX users and applications can belong to PRM groups. An application is referenced by its executable path name. In cases in which alternate process names are specified when a process is started, these alternate process names can also be configured. Wildcards can be used if the exact alternate process name is not known in advance. In this way, PRM provides more granular control over Oracle applications, because the Oracle database server has one executable, but spawns processes for each database instance, with the instance name embedded in the process name.

Normally, if one PRM group does not need its system resources, PRM allocates those resources to other groups that may need them. However, PRM can also help with capacity planning by allowing resource maximums to be specified. Thus, if an administrator knows that 25 percent more users will soon be on the system, the administrator can allocate a maximum of 80 percent of system resources to simulate the upcoming load.

PRM can also be used to dynamically adjust the workload in a high availability environment. For example, if three MC/ServiceGuard packages are each running with similar PRM entitlements, and one package fails to another system, this can be automatically detected and a new PRM configuration can be applied that gives the two remaining packages higher entitlements.

To check the actual resource usage of each PRM group, use the prmonitor command. GlancePlus can also show this information graphically.

## Controlling Application Performance

If a system performance problem exists, a performance monitoring tool, such as GlancePlus, can be used to find the main application or processes using the system resources. The problem may be due to a hung application that is holding key semaphores, a poorly structured application making unnecessary system calls or leaking memory, etc. A temporary solution may involve stopping and restarting the application. Longer-term solutions may involve restructuring the application, recompiling, or optimizing the program.

If a performance problem is due to multiple applications competing for system resources, you may want to use a product such as PRM to control resource allocation. PRM can ensure that critical applications get the appropriate resource entitlements. You may need to study the resource usage of competing applications on the system before you create the optimal PRM configuration.

## Recovering from Application Problems

Some application problems can be caused by accidental or inappropriate changes to application configuration files. EMS provides the capability to monitor these configuration files, and can report events whenever a change occurs. The text of the file can be included along with the event, which then can be used to provide a history of configuration changes so that an incorrect change can quickly be undone.

When a server has failed and can't be immediately repaired, high availability cluster software, such as MC/ServiceGuard, can be used to reduce the downtime associated with the failure and keep services available. MC/ServiceGuard can detect the failure of an application and automatically restart the application on another system in under one minute. Some preconfigured solutions already exist for some important applications, such as BEA Tuxedo, CICS, and NFS.

BMC's Application Service Assurance product can be used to provide application recovery. All the components of an application can be recovered to a specific point in time. This product supports many applications, including SAP R/3, PeopleSoft, Baan, and Oracle.

However, even with the kernel's ability to mask certain failure and the high availability software's ability to move applications to redundant servers, ultimately, you still need to repair failed components. For hardware problems, Support Tool Manager (STM) can provide fast diagnosis on HP-UX systems. SyMON can be used for Solaris environments. To fix OS problems, system vendors typically provide support information on their respective Web sites.

## Comparison of Application Monitoring Products

To monitor applications properly, being able to display them graphically is best. BMC PATROL can show process information in the PATROL Console. With the use of its specialized KMS, PATROL can also show icons for application instances, but displaying an arbitrary application can be difficult. IT/O provides only a system view in its windows, although Clusterview adds an application view when used with NNM or IT/O in an MC/ServiceGuard environment.

ClusterView can automatically detect an application failure and change the color of the application's icon. However, its diagnostic information is limited. EcoSNAP can detect application failures and send notifications through a variety of mechanisms. EMS supports more notification methods, but can't access all the diagnostic information available from EcoSNAP. MC/ServiceGuard, in addition to detecting failures, can restart applications.

The use of MC/ServiceGuard with EMS enables you to make explicit links between an application and its dependent resources. Those dependent resources are then monitored, and a failure directly results in an MC/ServiceGuard package failure. Although a resource configuration step is required, the effort saves time in troubleshooting the failures later, because the root cause is already provided.

Application performance data is available from a variety of products, including MeasureWare, BMC PATROL, and SMART Plug-Ins. BMC PATROL provides the most metrics for specialized applications, such as SAP R/3, but SMART Plug-Ins have the best integration with IT/O and PerfView, enabling event correlation and detailed performance graphs.
