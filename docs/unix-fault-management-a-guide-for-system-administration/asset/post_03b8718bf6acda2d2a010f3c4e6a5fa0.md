
ServerVision collects server performance data. Metrics include CPU utilization and swap space usage. The product can also be used to see which user is tying up system resources. ServerVision supports Sun Solaris, HP-UX, IBM AIX, NT, and other operating systems. It monitors and manages the performance of UNIX and NT servers, and provides system-wide metrics for use by other tools, such as PLATINUM's job scheduler, AutoSys. AutoSys provides dynamic load balancing and batch queue control.

WireTap shows the utilization of a network segment. The standard product categorizes network utilization by transport protocol, network protocol, application, and so forth. Optional modules can provide additional statistics for Oracle and Sybase requests, and for Web traffic.

TransTracker is a pre-deployment tool for measuring the system, database, and network usage of a transaction. Instead of requiring an application to be instrumented, TransTracker can identify transactions by collecting data from network packets.

WireTap can also be used to measure transaction response time. WireTap provides network monitoring by capturing packet-level data and categorizing it by protocol (such as HTTP or TCP). The user can identify SQL statements to look for, and can define alarm thresholds so that notification is sent when transaction response times are not being met. Web performance data for HTML requests can be provided, as well as Web server "hit" rates. Alarm information can be sent to the ProVision console or through an event adapter to the Tivoli Event Console.

PLATINUM provides a variety of database products. Solutions are available for database monitoring, database administration, and database performance bottleneck identification.

Database tools, such as Enterprise DBA and TSReorg, provide user administration, schema, and content management, as well as database reorganization. Enterprise DBA's administrative tasks can be done across different databases, with support for Oracle, Informix, and DB2 databases. Remote agents are used to perform the changes to the database. TSReorg supports both Oracle and Sybase databases. It can be used to reorganize database tables, indexes, and tablespaces. TSReorg is integrated with DBVision so that corrective actions can be automatically taken in response to an event. Tablespaces can be monitored with database reorganization triggered automatically. Tablespaces can be reorganized while the database stays online. TSReorg can also be used to view database structures graphically, showing where database fragmentation exists.

## Monitoring Features

ProVision includes agents to collect performance data and a GUI to show performance graphs. ProVision can be compared to the combination of MeasureWare and PerfView, products discussed later in this book.

Performance data can be accessed via the GUI console or a character-based interface. Both real-time and historical data can be presented. The console can display performance data from multiple database instances and servers. The information can be displayed as bar graphs, time-based graphs, charts, and tabular displays. You can also create your own display with your own combination of graphics.

ProVision enables you to configure alarms using multiple thresholds and varying severities. Actions can be configured at each severity level. Actions include several notification options, such as paging, e-mail, and SNMP traps. Corrective actions can also be configured. ProVision allows multiple actions to be configured that can be scheduled to run either simultaneously or sequentially.

## Monitor Discovery and Configuration

The DBVision and ServerVision instances to be monitored are defined during the installation and post-installation of ProVision. From the console, you can get summary statistics for each instance.

Some predefined alarms are provided by ProVision. You can also create your own alarms by specifying the metric and threshold condition. Alarm configuration is available from the console’s Control menu. The metric name needs to be entered manually, but you can find available metrics by using the Display menu. Menus associated with the graphs list available metrics. A wildcarding capability is also available. After specifying threshold information and actions, you may need to specify additional information, such as a mail recipient or pager number.

Before configuring an alarm, you may want to see which ones have already been defined. From the console, you can see a summary of the active alarms for all monitored instances.

## Monitor Developer’s Kit

PLATINUM Open Enterprise Management Services (POEMS) is a framework for plugging in additional monitoring capabilities. Tools using POEMS can take advantage of common services, including PLATINUM Director, event management, and communications.

## Notification Methods

Performance agents (scanners) collect data and store it in a shared memory segment, which is accessible to the archive and alarm background processes. The alarm process checks the data in the shared memory segment to determine whether alarm conditions are met.

When problems are detected, alerts can be sent to a pager, via e-mail, or to a centralized console receiving information from multiple databases or servers. Predetermined corrective actions can be taken in response to an event. These actions can be defined in customized scripts that are executed automatically.

Colors can be associated with each alarm severity when the events are shown in the Alarm window. The instance experiencing the alarm will also be highlighted within the GUI. An audible alarm is also provided at the console when the alarm arrives. Notification can be sent via e-mail or pager. Alarms can be sent to the management console or to any SNMP-capable management station using a predefined SNMP notification script.

A set of predefined corrective actions that can be used in response to alarms is provided, and you can define additional actions. Forwarding an alarm via pager or e-mail is an action that is supported. If multiple actions are provided for an alarm, they are executed in the order specified in the configuration.

A single alarm can have multiple actions associated with it. ProVision waits for a specified time and then takes the next corrective action. If the actions fix the condition, the alarm is cleared.

An alarm for a metric can have multiple thresholds associated with it. Each threshold is associated with a different severity level and can have a different troubleshooting or corrective action.

## Diagnostic Capabilities

The ProVision console has the ability to drill down from graphs to get additional information. You can also launch a UNIX command from within the console. From the ProVision console, you can get troubleshooting help after an alarm is received. An online reference guide, *Advisor*, provides a summary of the problem and instructions or suggestions on how to resolve an alarm condition.

The *Alarm Log*, which is accessible from the console, shows an event history along with the actions that have already been taken for the alarm. *Advisor* may also suggest other graphs to display for additional information. This instruction text can be included when an alarm is forwarded via e-mail.

A variety of tools are available for database administration. DBVision integrates with PLATINUM’s TSReorg product, which can be used to reorganize tablespaces or fix fragmentation problems. In addition to TSReorg, Enterprise DBA can be accessed, which provides the ability to manage users, database schemas, and database content.

## Additional Information

More information about PLATINUM ProVision can be obtained at http://www.platinum.com/products/provis/index.html.

## BMC PATROL

BMC Software provides monitoring capabilities through its PATROL software suite. PATROL is a system, application, and event management suite for system and database administrators. PATROL provides the basic framework for defining thresholds, sending and translating events, and performing other such tasks. PATROL consists of a console, intelligent agents, and Knowledge Modules (KMs). KMs are add-on products that contain the ability to monitor specific components. Three types of consoles are available:

- **Operator console**: Provides the graphical display and administration of systems and applications, as shown in Figure 3-5. Manual corrective actions are performed from here
- **Developer console**: Provides the capabilities for configuration and customization of remote agents and KMs
- **Event manager console**: Adds event filtering, correlation, sorting, and escalation facilities

BMC PATROL runs on a variety of operating systems, including UNIX, NT, OS/390, and NetWare. BMC also provides additional management software for mainframe environments.
