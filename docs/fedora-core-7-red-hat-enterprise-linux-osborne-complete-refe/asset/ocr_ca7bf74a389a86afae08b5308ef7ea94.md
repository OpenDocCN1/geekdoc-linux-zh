Place rules you want loaded automatically in the /etc/audit/audit.rules. The **sample.rules** file in the /usr/share/doc/auditd\* directory lists rule examples. You can also create a specific file of audit rules and use **auditctl** with the -R option to read the rules from it.

# ## Performance Analysis Tools and Processes

Linux treats each task performed on your system as a process, which is assigned a number and a name. You can examine these processes and even stop them. Fedora provides several tools for examining processes as well as your system performance. Easy monitoring is provided by the GNOME System Monitor (System | Administration | System Monitor). Other tools are also available, such as GKrellM and KSysguard. A number of utilities on your system provide detailed information on your processes, as well as other system information such as CPU and disk use (see Table 27-10). Although these tools were designed to be used on a shell command line, displaying output in text lines, several now have KDE and GNOME versions that provide a GUI interface for displaying results and managing processes.

| Performance Tool | Description |
| :--- | :--- |
| vmstat | Performance of system components |
| top | Listing of most CPU-intensive processes |
| free | Listing of free RAM memory |
| sar | System activity information |
| iostat | Disk usage |
| GNOME System Monitor | System monitor for processes and usage monitoring (System | Administration | System Monitor) |
| GKrellM | Stackable, flexible, and extensible monitoring tool that displays information on a wide variety of system, network, and storage operations, as well as services, easily configurable with themes |
| KDE Task Manager and Performance Monitor | KDE system monitor for processes and usage monitoring |
| Fisk | Monitoring tool for system processes |
| System Tap | Tool to analyze performance bottlenecks |
| GNOME Power Manager | Manage power efficiency features of your system |
| cpuspeed | Implement CPU speed reduction during idle times (AMD and Intel Cool and Quiet). |

TABLE 27-10 Performance Tools