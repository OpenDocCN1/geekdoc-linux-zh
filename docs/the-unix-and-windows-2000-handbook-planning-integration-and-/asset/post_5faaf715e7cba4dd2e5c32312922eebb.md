
performance monitoring and reviews performance logging files. The second subsection highlights tools and commands that allow the system administrator to tune the performance of a Windows 2000 workstation or server.

## WINDOWS 2000 PERFORMANCE-MONITORING COMMANDS

This subsection contains Windows 2000 tools that monitor the four major performance components described previously in this chapter. The tools covered in this subsection allow a system administrator to interactively monitor the utilization and performance of a Windows 2000 workstation. The tools can also be utilized to capture data to log files or send alerts when performance thresholds are exceeded. It is important to take advantage of all the tools in this subsection to monitor the performance of a Windows 2000 workstation.

## Performance Logs and Alerts

Configuring logging and alerts should be part of the installation procedure for all systems. It is important that performance statistics be captured on all Windows 2000 workstations and servers. Table 14.8 contains counters that should be logged as a minimum for a server. A server will include additional counters that pertain to specific services it is providing. Keep in mind that these logging and alert processes consume system resources. Items logged from Table 14.8 will create a binary file of approximately 200KB in a 24-hour period, with samples taken every 15 seconds. Try to keep counters to a minimum and the sampling rate at a reasonable level or your disks will be filled with log files. Let's go through the procedures to set up logging and alerts for the counters in Table 14.8.

- 1. Open the Control Panel using the following sequence: Start→Settings→Control Panel.
- 2. Double-click Administrative Tools.
- 3. Double-click Performance (see Figure 14.11).
- 4. Double-click Performance Logs and Alerts.
- 5. Click Counter Logs or Alerts.
- 6. Right-click in the right side of the window. Next, highlight New, and then select Create New Log Settings.
- 7. Specify a meaningful log file name. For this example, we used MinWrkStat. You are then presented with the screen in Figure 14.12. The next four sections will cover each tab page in Figure 14.12.

## Table 14.8 Counters to be logged

| Performance Object | Performance Counter | Definition |
|---|---|---|
| Memory | Available Bytes | Physical memory available in bytes |
| Memory | %Committed Bytes in Use | Ratio of committed bytes to memory |
| Network Interface | Bytes Total/Sec | Bytes input and output on the network interface |
| PhysicalDisk | %Disk Time | Percentage of time disk is busy reading or writing |
| PhysicalDisk | Disk Bytes/sec | Bytes transferred to disk during read or write operations |
| Processor | %Processor Time | Percentage of time processor is executing a non-idle thread |
| System | Processor Queue Length | Threads in queue ready to run |

![](img/415c89a1ede71e11e5040a0038b6916c_609_0.png)

Figure 14.11 Performance Monitor main screen.

## Figure 14.12
New log creation screen.

![](img/415c89a1ede71e11e5040a0038b6916c_610_0.png)

The General and Schedule tabs are similar for counter logs and alerts, except the Counter Logs menu contains a Log Files tab and the Alerts menu has an Action tab.

### General Tab (Counter Logs and Alerts)

The first page in setting up counterlogs and alerts is the General page. The General page allows you to add counters and set the sampling rate. You must select at least one counter or alert on this page to access the other tabs on this screen. This configuration page is reached via the steps outlined in the "Logging and Alert" section. Execute the following steps to add the counters from Table 14.8:

- 1. Click Add (Figure 14.13)
- 2. Select Use local computer counters. This allows you to save these settings and use them on other Windows 2000 workstations.
- 3. Select a Performance object, then highlight the associated counter from the table. Clicking the Explain button will display a definition for each Performance counter highlighted.
- 4. Highlight the associated counter.
- 5. Highlight the instance. For multiple processors or disk drives, you have the option of selecting an individual item or selecting all instances.
