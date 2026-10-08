
the HP Resource and Performance Management Web site at http://www.openview.hp.com/solutions/application/.

## Oracle Management Pak

The Oracle Management Pak from Hewlett-Packard can be used to monitor Oracle databases and is used in conjunction with GlancePlus Pak 2000. You can also migrate from this single-server-environment solution to an enterprise solution simply by adding the intelligent agent for IT/O.

Numerous database metrics are available. Oracle Management Pak can report the status of the database instance, individual tablespaces and rollback segments, and configured Oracle background processes. The number of snapshot refresh errors can also be reported.

The following is a summary of the resource management metrics that are included for Oracle:

- Maximum number of sessions since server was last started
- Percentage of free tablespace to total available
- Number of free chunks in tablespace
- Number of segments that cannot add extents
- Number of segments approaching maximum extents
- Percentage of open cursors to total cursors configured
- Percentage of DML locks used
- Percentage of maximum processes used
- Percentage of enque resources used
- Number of current user logons
- Archive free-space percentage
- Space remaining on dump devices

In addition to resource management, the following Oracle performance metrics are available:

- Ratio of blocks read to physical reads
- Disk sort rate
- Percentage of memory sorts to total
- Average number of rows per sort
- Block buffer hit ratio (current and total)
- Dictionary cache hit ratio
- Library cache reload percentage
- Percentage of free memory to total shared pool memory
- Transaction commit rate
- Transaction rollback rate
- Percentage of rollbacks to commits
- Background checkpoint completion rate
- User call rate
- Ratio of recursive calls to user calls
- Percentage of chained rows fetched to total
- Rate at which full table scans occur
- Buffer busy rate
- Number of waits for redo log buffer space
- Percentage of rollback buffer waits to gets

All of the threshold monitoring and real-time graphs included with GlancePlus Pak 2000 can be applied to these database metrics as well.

## PerfView

PerfView is a graphical performance analysis tool from Hewlett-Packard. It is used to graphically display performance and system resource utilization for one system or for multiple systems simultaneously, so comparisons can be made. A variety of performance graphs can be displayed. The graphs are based on data collected over a period of time, unlike the real-time graphs of GlancePlus, which show only recent history. PerfView runs on HP-UX or NT systems and works with data collected by MeasureWare agents.

PerfView has three main components:

- **PerfView Monitor**: Provides the ability to receive alarms. A textual description of an alarm can be displayed. Alarms can be filtered by severity, type, or source system. Also, after an alarm is received, the alarm can be selected, which displays a graph of related metrics. An operator can monitor trends leading to failures, and can then take proactive actions to avoid problems. Graphs can be used for comparison between systems and to show a history of resource consumption. An internal database is maintained that keeps a history of alarm notification messages.
- **PerfView Analyzer**: Provides resource and performance analysis for disks and other resources. System metrics can be shown at three different levels: process, application (configured by the user as a set of processes), and global system information. It relies on data received from MeasureWare agents on the managed nodes. Data can be analyzed from up to eight systems concurrently. All MeasureWare data sources are supported. PerfView Analyzer is required by both PerfView Monitor and PerfView Planner.
- **PerfView Planner**: Provides forecasting capability. Graphs can be extrapolated into the future. A variety of graphs (such as linear, exponential, s-curve, and smoothed) can be shown for forecasted data.

In addition to graphing and analyzing system resources, process and application resources can be graphed and analyzed using PerfView. With PerfView, users can define the set of processes that make up an application. PerfView can then be used to show a history of a specified application’s utilization. PerfView’s ability to show history and trend information can be helpful in diagnosing system problems. Graphing performance information can help you understand whether a persistent problem exists or an anomaly is simply a momentary spike of activity.

With PerfView, you can analyze, alarm, forecast, and report on the Oracle Management Pak metrics and compare them with system, network, and application metrics. The graph in Figure 8-2 shows commit, or transaction, rates over time.

To diagnose a problem further, PerfView Monitor enables you to change time intervals, to try to find the specific time a problem occurred. The graph is redrawn showing the new time period.

PerfView is integrated with several other monitoring tools. You can launch GlancePlus from within PerfView by accessing the Tools menu. PerfView can be launched from the IT/O Applications Bank. When troubleshooting an event in the IT/O Message Browser window, you can launch PerfView to see a related performance graph.

When using IT/O with PerfView, the PerfView Monitor is disabled. The IT/O Message Browser should be used to view alarms, instead. When an alarm is received in IT/O, you can click the alarm to display a related PerfView graph.

In a single performance graph, PerfView can show information collected from multiple systems. The PerfView and ClusterView products have also been integrated, enabling you to select a cluster symbol on an HP OpenView submap and launch the PerfView application, to quickly show a performance comparison between all systems in the cluster.

## Figure 8-2 Graphing transaction rates in PerfView.

![](img/eae88b61ada165139a1d9b546a34140b_254_0.png)

For further information, visit the HP Resource and Performance Management Web site at http://www.openview.hp.com/solutions/application/.

## SMART Plug-Ins for Databases

IT/Operations is meant to provide a consistent interface for managing systems and networks. The goal of HP's SMART Plug-Ins (SPIs) is to extend support for applications and databases. SPIs are preconfigured solutions that are intended to be used with IT/O, although IT/O is not required. Today, SPIs exist for SAP R/3, Baan, Oracle, Informix, and Sybase.

SPIs for Databases provide the same set of metrics as provided by the Oracle Management Pak, plus the ability to report information via IT/O's reliable RPC mechanism, not via SNMP traps.

The tight integration between SPIs and IT/O means that other features are available to SPIs, such as event filtering and correlation, and task escalation. Events include built-in instructions and operator text that can aid in diagnosis and recovery. Corrective actions are predefined for many SPI events.

Figure 8-3 shows how the SPI for Informix integrates into IT/O. You can see the new message groups that were added for Informix by the SPI for Informix. The Application Group window shows all the database tools added for SPI for Informix. The Message Browser enables you to see messages about the Informix database.

Unlike EMS, which is focused on fault management, SPIs for Databases focus on database configuration and resource management. IT/O templates can specify different thresholds for different database instances. SPIs can verify that the database processes defined in Oracle's init.ora configuration file are actually running, and their performance can be monitored in GlancePlus and PerfView as a single application.

## BMC PATROL Knowledge Modules

BMC Software, Inc. provides monitoring capabilities through its PATROL software suite. With PATROL, you can define thresholds and send events to a console or to other management applications. PATROL consists of a console, intelligent agents, and more than 40 different monitoring programs, or Knowledge Modules (KMs). Each KM is optional, so you can pick the monitors that are best for your environment.

The console provides a centralized graphical display, with icons representing system components or other monitored components. Icons change color to correspond to their status. For example, an icon may change to red to represent a critical event on its node or component. The PATROL console also provides an Event Browser, in which you can filter, correlate, sort, and escalate events. Alarms can be configured so that events are sent to the console and shown in the Event Browser. Events can also be configured to go to HP OpenView IT/O or other SNMP-based management stations.

Intelligent agents provide the ability to discover the system, database, and application components in an enterprise. The agents reside on each server. On an ongoing basis, the agents
