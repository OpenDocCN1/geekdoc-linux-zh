
## Monitored Components

  MeasureWare agents collect data at three different levels: global system metrics, application metrics, and process metrics. Global and application data is summarized at five-minute intervals, whereas process data is summarized at one-minute intervals. Important applications can be defined by an administrator by listing the processes that make up the application in a configuration file.

  In addition, optional modules for database and networking support are offered. MeasureWare also provides a DSI interface that enables you to pass your own data to the MeasureWare Agent.

  MeasureWare has database modules for collecting database metrics for Oracle, Sybase, and Informix databases. These modules can take advantage of all the standard monitoring features of MeasureWare, such as timestamping data, logging, and forwarding alarms to HP PerfView. However, this product is similar to another HP product for database performance information, the OpenView SMART Plug-Ins for databases. SPIs also feed information into MeasureWare, providing a consistent interface with other IT/O products.

  A more detailed list of metrics in each category can be found in the next few chapters on systems, disks, networks, applications, and databases. Although MeasureWare provides extensive performance and resource information, it offers limited configuration information and no data about system faults.

## Monitoring Features

  HP MeasureWare Agent software is installed on each managed system. The agents keep a history of a system's resource utilization, and the information can then be exported to spreadsheets or to performance analysis programs, such as HP PerfView. The data can be used by these programs to generate alarms to warn of potential performance problems. By using historical data, trends can be discovered, which can help to solve resource issues before they affect system performance.

  MeasureWare allows you to define alarm conditions. You can have alarms sent based on conditions that involve a combination of metrics. For example, a CPU bottleneck alarm can be based on the CPU use and CPU run queue length.

  MeasureWare agents provide alarms to PerfView for analysis, and to the IT/O management console. SNMP traps can also be sent by the MeasureWare Agent at the time threshold conditions are met. Automated actions can be taken, or the operator can choose to take a suggested action.

  You can configure alarms based on a combination of multiple metrics and on duration. In this way, rules can be used to ensure that messages are sent to an operator only when a real problem occurs.

  MeasureWare's extract command can be used to export data to other tools, such as spreadsheet programs.

  MeasureWare Service Reporter is a Web-based metrics tool for generating reports on network performance. Network performance can be compared to service-level agreements. Reports can show the actual response times for specific applications.

  MeasureWare can show application information, but an application first has to be defined. Application definitions can be used to summarize process-level data for all processes defined for an application.

  With PerfView, a system administrator can analyze, alarm, forecast, and report on the MeasureWare metrics. HP OpenView IT/O can then receive event messages from the MeasureWare Agent regarding alarm conditions. In fact, the MeasureWare Agent will detect an HP OpenView IT/O agent running on the system and automatically start sending alarms to it. Then, by clicking a database message sent to IT/O, for example, you can bring up PerfView to graph the related database and system information.

  MeasureWare requires approximately 1MB of memory for data collection, and 40MB of disk space is recommended for each month of data that needs to be stored. To ensure that the MeasureWare Agent is automatically restarted after a system reboot, make sure the file `/etc/rc.config.d/mwa` is configured with the parameter `MWA_START` equal to 1.

  MeasureWare is a complement to EMS and IT/O, providing performance data while EMS and IT/O focus on availability information. MeasureWare should be used when you need to see a history of resource values over time.

  MeasureWare agents gather information at one- and five-minute intervals. Other tools, such as EMS, can acquire information as frequently as every second. EMS monitors can also forward important information without waiting to be polled.

  The MeasureWare agents are available on HP-UX, IBM AIX, Sun Solaris, and NCR WorldMark systems.

## Monitor Discovery and Configuration

  When MeasureWare is activated, the data is automatically collected and analyzed at regular intervals. An administrator configures the alarm thresholds for notification.

  An ASCII file contains alarm definitions. To add or modify an alarm, you need to edit this file; no GUI is available. Validation is done to ensure that the syntax is correct. On HP-UX systems, this file is located at `/var/opt/perf/alarmdef`. To create an alarm, you need to know the available metrics to choose from. The online help facility can show you the data that is available, with descriptions of each metric.

  Applications can also be defined by an administrator by editing the parm file, located at `/var/opt/perf/parm`, by default. You can then monitor specific metrics for your application.

  To ensure that alarms are appropriate, you can use the `analyze` command from within MeasureWare's utility program to test alarm conditions. analyze looks at historical data and reports when alarms would have been sent. In this way, you can determine whether you have the appropriate alarm conditions.

  If you edit the parm or alarmdef file, you need to use the mwa command to instruct the MeasureWare Agent to reread the file.

  You can run the perfstats utility to check the status of a MeasureWare agent.

## Monitor Developer's Kit

  A few different ways exist to include your own performance instrumentation along with other MeasureWare data. Through the DSI API, custom applications can send information to MeasureWare to store. MeasureWare also can timestamp and provide summaries of this data.

  Additionally, the ARM APIs can be used with instrument applications so that transaction response times can be measured. This information can be passed along to MeasureWare agents for analysis. The ARM APIs are described in more detail in Chapter 7.

## Notification Methods

  MeasureWare agents collect information about system performance. Threshold events can be sent to PerfView, as alerts, or to IT/O, as opmsgs. You can also configure alarms to execute a UNIX command, such as mail, to send a notification.

  Alarm notification can be sent to PerfView, IT/O, or any SNMP-based management platform (such as Ucenter TNG) by using SNMP traps. Alarms can be sent to multiple destinations. MeasureWare can also be configured to execute an arbitrary UNIX command when the alarming threshold is reached. Custom applications that need to receive alarm information can be integrated in this way.

  If the MeasureWare Agent detects that a system is being managed by IT/O, it automatically sends alarms to IT/O.

## Diagnostic Capabilities

  MeasureWare is integrated with IT/O and PerfView. A MeasureWare alarm can be received by IT/O. Drilling down on an event can launch PerfView for further analysis.

## Additional Information

  The list of MeasureWare metrics varies from release to release. To verify that the metric you want is available, you can check the files under /opt/perf/paperdocs/mwa/C on a system where MeasureWare is installed.

  The MeasureWare Agent is available as a separate product and is also included as part of the GlancePlus Pak software bundle.

  For further information, visit the HP Resource and Performance Management Web site at http://www.openview.hp.com/solutions/application/.
