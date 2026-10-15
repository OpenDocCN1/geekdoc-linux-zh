
# Figure 5-39 Follow-up actions setting for a task

You can also specify access privileges to the task, such as read, run, or execute for different users and groups by clicking the Security tab within the window.

Now you can submit the task to the Task Center by clicking OK.

As in our example, the notification is specified to be sent to DB2's journal, so we can check the Journal for the running results.

To invoke the Journal, you can select Tools → Journal in the menu bar of the Task Center or Control Center, or other DB2 GUI tools where the Tools menu is available.

Here is the result for our sample task. You can get more details by right-clicking the result entry which corresponds to your task, then choose Show Results. Another window will pop up, and within that, you can get detailed information for

![](img/d95c931f4f3da4a6bd0ee55148fefad7_234_0.png)

The scheduling function is also available for many other DB2 Wizards or GUI tools such as export, import, load wizard, runstats, reorg, backup and restore. You can take advantage of these useful functions for task automation purposes in your environment.

# Up and Running with DB2 for Linux

# Monitoring DB2

This chapter discusses DB2’s monitoring features provided by Health Center and Health Monitor.

DB2 Universal Database Version 8 adds self-managing and resource tuning (SMART) database technology that lets database administrators choose to configure, tune and manage their databases with enhanced automation. SMART database management means administrators spend less time managing routine tasks and more time focussing on tasks that help enterprises gain and maintain a sustainable competitive advantage. Several tools are added or redesigned to support self-managing, self-optimizing and self-tuning requirements, such as Configuration Advisor, Health Center, Performance Expert, Recovery Expert, and so forth. These new tools make DB2’s configuration and maintenance tasks more smart and easy-to-use, and finally results in significant reduction of human intervention and cost reduction for the database system operation and maintenance.

This chapter gives an in-depth discussion of the Health Center and Health Monitor. Chapter 3, "Post installation tasks" on page 79 has detailed information regarding Configuration Advisor. For other DB2 monitoring tools, refer to their online help or specific documents for more information.

In addition, this chapter also discusses DB2 UDB and operating system log files which may provide more detailed information about certain problems and can help you further determine what the problem is and what the cause is. Afterwards you can take corrective actions based on the collected information.

Furthermore, some useful and popular tools from the operating system are also available to assist in monitoring the system resource usage and perform troubleshooting, and we also provide brief information about these tools.

# 6.1 Health Monitor and Health Center

With Version 8, DB2 introduces two new features to help you monitor the health of your DB2 systems: Health Monitor and Health Center. These tools add a management by exception capability to DB2 Universal Database by alerting you to potential system health issues. This enables you to address health issues before they become real problems that affect your system performance. Prior to using the Health Monitor and Health Center, you need to understand the concept of a health indicator which is briefed in the following paragraph.

# 6.1.1 Health Indicator

A health indicator is a measurement that gauges the healthiness of some aspect of an object. The health monitor uses these indicators to evaluate specific aspects of database manager or database performance.

DB2 comes with default settings for all health indicators. Using the Health Center, DB2 commands, or APIs, you can customize the settings of the health indicators, and define who should be notified and what script or task should be run if an alert is issued. For example, you can customize the alarm and warning thresholds for the amount of space used in a table space. You can also use DB2 commands or APIs to retrieve health information from the Health Monitor, allowing you to integrate DB2 Health Monitoring with existing system-wide monitoring solutions.

# 6.1.2 Health Monitor

The Health Monitor is a server-side tool that constantly monitors the health of the instance and all active database objects when DB2 is started. The Health Monitor automatically evaluates a set of health indicators, even without user interaction. If the current value of a health indicator is outside the acceptable operating range defined by its warning and alarm thresholds, the health monitor generates a health alert.

The Health Monitor gathers information about the health of the system using new interfaces that do not impose a performance penalty. It does not turn on any snapshot monitor switches to collect information. The Health Monitor is enabled by default when an instance is created; you can deactivate it using the database manager configuration parameter health_mon. If the Health Monitor finds that a defined threshold has been exceeded (for example, the available log space is not sufficient), or if it detects an abnormal state for an object (for example, an instance is down), the Health Monitor will raise an alert.
