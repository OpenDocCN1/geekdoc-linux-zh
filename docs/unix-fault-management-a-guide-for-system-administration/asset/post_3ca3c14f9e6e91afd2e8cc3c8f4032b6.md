
Oracle provides a function for calculating the elapsed time for duration events. Reports can also be generated on the frequency of different types of events, such as connection events. Statistics available include the minimum, maximum, and average times spent doing different events. The Oracle Trace APIs are listed with a brief description in Table 8-9.

## Oracle VS Tables

Oracle provides a set of virtual tables that can be used to access memory structures within the shared global area. Many of these tables contain database performance information that is continuously updated. Table 8-10 lists and describes the contents of some of the more interesting VS tables.

### Table 8-9 Oracle Trace APIs

| Name | Function |
| --- | --- |
| epc_init | Initial trace call; used to register facility with Oracle Trace |
| epc_add_reg_id | Adds a registration ID for a facility |
| epc_remove_reg_id | Removes a registration ID for a facility |
| epc_start_event | Records start of duration event |
| epc_end_event | Records end of duration event |
| epc_event | Records asynchronous event |
| epc_collect | Starts a collection from within a facility |
| epc_cancel | Stops a collection started by epc_collect |
| epc_bind | Binds a process to a collection that is already active |
| epc_flush | Writes collection data buffers to disk |
| epc_context | Stores collection data on per-thread basis |
| epc_delete_context | Indicates the end of thread |
| epc_set_cf_items | Sends cross-facility items to another process |
| epc_cf_value | Assigns values to cross-facility items |
| epc_get_cf_items | Obtains cross-facility items from another process |

### Table 8-10 Oracle VS Tables

| VS Table | Contains |
| --- | --- |
| V$DATABASE | Database information from the control file |
| V$FILESTAT | File read/write statistics |
| V$INSTANCE | Status information for the current instance |
| V$LIBRARYCACHE | Library cache performance information |
| V$LICENSE | Information on license limits |
| V$PROCESS | Process information |
| V$ROWCACHE | Data dictionary performance information |
| V$SESSION | Session information |
| V$SESSTAT | Information on the memory usage for each current session |
| V$SGA | Summary information on system global area |
| V$SGASTAT | Detailed information on system global area |
| V$SYSSTAT | Current system-wide value for each variable in V$SESSTAT |

To get a list of all available Oracle V$ performance monitoring tables, execute the following SQL query: `SELECT * FROM X$KQFVI;`

For more information on the V$ tables, consult Oracle's Oracle Server Tuning Guide and Oracle Server Reference manuals.

## GlancePlus Pak 2000

GlancePlus Pak 2000 is a product from Hewlett-Packard. It includes performance management, fault management, and real-time performance monitoring. It has three components:

- MeasureWare
- GlancePlus
- ITO/Special Edition

MeasureWare is an HP product that collects and logs resource and performance metrics. MeasureWare agents run and collect data on the individual server systems being monitored. Agents exist for many platforms and operating systems, including HP-UX, Solaris, and AIX.

The MeasureWare agents collect data, summarize it, timestamp it, log it, and send alarms when appropriate. The agents collect and report on a wide variety of system resources, performance metrics, and user-defined data. The information can then be exported to spreadsheets or to performance analysis programs, such as PerfView. The data can be used by these programs to generate alarms to warn of potential performance problems. By using historical data, you can discover trends, which can help you address resource issues before they affect system performance.

MeasureWare collects system, application, process, and transaction data. MeasureWare agents collect data at three different levels: global system metrics, application, and process metrics. Global and application data is summarized at five-minute intervals, whereas process data is summarized at one-minute intervals.

GlancePlus is a real-time, graphical, performance monitoring tool from Hewlett-Packard. It is used to monitor the performance and system resource utilization of a single system. You should use GlancePlus to see whether a performance problem can be isolated to the system or the database. Both Motif-based and character-based interfaces are available. The product can be used on HP-UX, Solaris, and many other operating systems.

GlancePlus collects information similar to MeasureWare, but samples data more frequently. GlancePlus can be used to graphically view current CPU, memory, swap, and disk activity, as well as utilization at the system level. It can also show application and process information. Transaction information can be shown if the MeasureWare Agent is installed and active.

ITO/Special Edition is the single-system version of ITO. From the Java-based GUI, you can view events from a single system in the Event Browser. Diagnostic tools are also provided from the GUI. ITO/Special Edition uses ITO's intelligent agent technology, which includes the ability to collect data from various sources and execute automated actions.

To monitor an application in GlancePlus or MeasureWare, the application must first be defined. To define important applications, you must first define the processes that comprise the application. This is done in the parrn file (located at /var/opt/perf/parrn), in which you list the process names that make up the application. Wildcards can be used if the exact names vary. For example, ora* could be used to define an application based on all processes beginning with ora. GlancePlus and MeasureWare summarize process information for processes listed in the application definition.

Customizable rules determine when a system performance problem should be sent as an alarm. In GlancePlus, the rules are managed by the GlancePlus Adviser. Choosing the Edit Adviser Syntax option on the Adviser menu enables you to see and modify all alarm conditions. The GlancePlus Adviser syntax file (/var/opt/perf/adviser.syntax) contains the symptom and alarm configuration. Additional syntax files can also be used. For MeasureWare, alarms are defined in the alarmdef file, located at /var/opt/perf/alarmdef.

In GlancePlus, alarms result in onscreen notifications, with color representing the criticality of an alarm. An alarm can also trigger a command or script to be executed automatically. Instead of sending an alarm, GlancePlus can print messages or notify you by executing a UNIX command, such as mailx, using its EXEC feature.

You can also have alarms sent according to conditions that are based on a combination of metrics. For example, a CPU bottleneck alarm can be based on the CPU use and CPU run queue length. MeasureWare agents provide these alarms to PerfView for analysis, and to the ITO management console. SNMP traps can also be sent at the time a threshold condition is met. Automated actions can be taken, or the operator can choose to take a suggested action.

Application- and transaction-level information is available. Transactions must be defined by the application using the ARM API. The following are some of the available metrics:

- Transaction average response time
- Distribution of transaction response times
- Number of aborted transactions
- Response time of aborted transactions

More than 600 metrics are accessible from GlancePlus and MeasureWare. The complete list of metrics can be found by using the product’s online help facility. On systems with GlancePlus Pak 2000 installed, this information can also be found in the directory /opt/perf/paperdocs/gp/C.

Hewlett-Packard also provides a separate product, the Process Resource Manager (PRM), which can be used to control CPU, memory, and disk utilization between users or applications. PRM has done some special integration with Oracle, as well. If PRM is being used, GlancePlus shows how well PRM application groups are staying within their resource entitlements. From GlancePlus, you can also change PRM process group entitlements.

Although MeasureWare provides extensive performance and resource information, it has limited configuration information and no data about system faults. For further information, visit
