
of potential problems, scheduled maintenance can replace the unplanned downtime associated with a failed component.

Predictive Support uses a set of rules on a managed node to determine when events should be sent to the HP Response Center. These conditions can be updated periodically by downloading new rules from HP. Event correlation ensures that duplicate messages are suppressed and that the Response Center is not repeatedly warned of the same root problem.

Predictive Support analyzes on-board logs, system logs, and memory logs. The software can automatically dial the HP Response Center to transmit error data and logs, or the system administrator can initiate modem transmission. Similarly, Predictive Support software updates, to include new rules for generating predictive events, can be triggered automatically or controlled by the administrator. Configuration and administration is controlled through a menu-driven interface.

System logs are scanned for I/O errors and LPMCs. Logged data is analyzed for trends associated with specific disk or tape devices, such as correctable errors. LPMC records are analyzed for internal cache errors. Memory logs are also scanned to look for error rates exceeding specified thresholds.

The Response Center determines where a failed device is located, its model number, its manufacturer, and its serial number, so that repairs can be made. This information is sent in the failure notification messages.

HP Predictive Support does not help with other areas of system monitoring, such as resource and performance management. Also, the software runs only on HP-UX systems.

## HA Observatory

HA Observatory is a suite of tools used to detect and quickly diagnose system problems. The products include the Configuration Tracker, which keeps track of the server’s software configuration, Network Node Manager, and HP Predictive Support. A support system and network router are also maintained at the customer site.

HA Observatory relies on HP Predictive Support to report hardware failures. In addition, configuration information collected by the Configuration Tracker is available. The Configuration Tracker generates and maintains a snapshot of the configuration so that it can detect software configuration changes.

HA Observatory uses a secure network link to HP’s High Availability Support Center from a special system at the customer site. This support system, an HP 9000 Series 700 workstation, collects system configuration information from key servers and can be used to view network status and topology information. Hardware failure notifications and configuration information can be sent to HP. When permitted by the customer, HP support engineers can access the customer servers over the secure link to gather additional information.

HA Observatory is supported only on HP-UX systems and is available only to customers with BCS and CCS support contracts.

## Monitoring System Peripherals

When monitoring your UNIX server, you should not forget about the system peripherals, such as disk, tape, and printer devices.

### Disks

Disk devices store your corporate data, so ensuring their correct operation is critical. Disk monitoring should be included as part of any effort to monitor a system. Chapter 5 is dedicated to covering the tools for monitoring disk devices because of the importance and complexity of the subject.

### Tapes

By checking for tape hardware failures periodically, problems can be found before the tape drive is needed. For example, early detection and repair can result in the evening backup application running without delays.

You should use hardware monitors, such as the EMS Hardware Monitors, to ensure that your tape drives are healthy, so that backups may occur as scheduled. As mentioned earlier, a variety of tape-related errors can be detected, such as failed I/O operations to the tape, tape loader errors, and tape changer errors.

### Printers

This chapter discussed earlier how you can use MIB instrumentation to look for important system information. A Printer MIB specification typically is supported by modern network printer devices. The Printer MIB stores the status of the printer (online, offline, and so forth), as well as information about printer subcomponents, such as an empty printer tray. A tool such as IT/O can be used to enable monitoring of individual fields in the MIB, such as printer status.

Using the lpstat command, you can check the status of jobs in the print queue and verify that the print scheduler is running. Using lpstat with no options shows you information for all the printers connected to the system.

Some printer management software is also available. One example is HP JetAdmin software, which can be used to manage printers and monitor the status of jobs printing remotely. This host-based application provides real-time printer and job status information, as well as status updates, remote diagnostics and troubleshooting, an optional status log, and a remote front panel. The utilities are accessible through a graphical interface. Web JetAdmin software adds additional capabilities, such as the ability to view customized maps that show printer locations and status information from a Web browser.

Web JetAdmin 4 is an HP software application that is used to monitor all peripheral devices on the network from a Web browser. Maintenance and troubleshooting can be done on any MIB-compliant printer device, including ScanJet 5 scanners and HP SureStore CD-ROMs.

### Collecting System Performance Data

Users call their IT department when they have delays in accessing data or applications. Good tools are needed to help an operator pinpoint the source of the problem. This section covers some of the interesting performance and resource-utilization metrics, and the tools available to collect data about these metrics.

A wide range of conditions may result in resource and performance problems. Running out of available memory may be caused by a failure of a memory component or by a memory leak in an application. A sudden rise in CPU utilization could be an indication of processor failure or the introduction on the system of a CPU-intensive application. Analysis is needed to determine whether resource problems can be fixed with a configuration change, hardware repair, or other techniques.

Many important system resources have configured limits. The following system resource metrics are important to monitor:

- Number of named pipes
- Number of messages and message queues
- Number of system semaphores
- Amount of shared memory
- Number of open files
- Number of processes

Earlier, this chapter discussed some of the tools that can be used to check system resource usage. The **sar** and **sysdef** commands can compare current usage to configured limits. An EMS monitor is available to detect thresholds being exceeded for the following resources:

- Callout table
- Process table
- File descriptor table
- File lock table
- Shared memory
- System semaphores
- Message queues and message segments

The performance tools discussed in this section can also detect resource usage problems.

Some system performance monitoring is available from the **SAM Performance Monitors**, with which an administrator can obtain information on system, disk, and virtual memory activity, for example. Text-based information is displayed in a Motif window when one of the desired metrics is selected.

Having historical information is important, to understand how the system performance has varied over time. Knowing how your system behaves under normal conditions helps when trying to troubleshoot system performance problems. Note that the performance tools themselves impact the performance of the system, so you need to find a tool with low overhead.

This section describes some common tools for measuring and monitoring system performance. Here are some of the key metrics discussed in this section:

- **Buffer cache queue length**: Refers to the number of processes blocked that are waiting for updates to the buffer cache. If this value is high, it could be an indication of a memory bottleneck.
- **Context switches**: How often processes are being swapped out of the run queue.
- **CPU utilization**: Expressed as a percentage of time spent in various execution states. Low utilization indicates that the CPU spent the majority of its time in the idle state.
- **CPU run queue length**: The average number of processes in the run state waiting to be scheduled.
- **Memory utilization**: Usually expressed as a ratio of the amount of memory in use versus the total memory available.
- **Paging**: Refers to the transfer of data between virtual memory (disks) and physical memory.
- **Swapping**: Refers to the transfer of data between physical memory and a special virtual memory area reserved for swapping.

Performance tools, such as BMC PATROL and MeasureWare, don't always provide the same set of metrics on all platforms. For simplicity, this section focuses on the Sun Solaris and HP-UX platforms only. Also, these products are continually being enhanced, so the actual metrics available for use in your environment may not precisely match the information presented in this section.

### MeasureWare

HP MeasureWare Agent is a Hewlett-Packard product that collects and logs resource and performance metrics. MeasureWare agents run and collect data on the individual server systems being monitored. Agents exist for many platforms and operating systems, including HP-UX, Solaris, and AIX.

The MeasureWare agents collect data, summarize it, timestamp it, log it, and send alarms when appropriate. The agents collect and report on a wide variety of system resources, performance metrics, and user-defined data. The information can then be exported to spreadsheets or to performance analysis programs, such as PerfView. The data can be used by these programs to generate alarms to warn of potential performance problems. By using historical data, trends can be discovered. This can help address resource issues before they affect system performance.

MeasureWare agents collect data at three different levels: global system metrics, application, and process metrics. Global and application data is summarized at five-minute intervals, whereas process data is summarized at one-minute intervals. Important applications can be defined by an administrator by listing the processes that make up an application in a configuration file.
