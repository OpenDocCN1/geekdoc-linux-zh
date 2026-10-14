
To perform a detailed analysis of your system, select one of the four scanning buttons in the toolbar:

- **Scan Home:** to analyze the folders contained in your home folder
- **Scan Filesystem:** to analyze the entire filesystem
- **Scan Folder:** to single out a folder to analyze
- **Scan Remote Folder:** to scan a remote filesystem

Be careful when selecting to scan the entire filesystem or a remote filesystem. Analyzing the disk space requires reading the entire disk area. This process can take some time, depending on the size of the disk and, in the case of a remote scan, network connectivity speeds.

The result of a complete scan is shown in Figure 18-10.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_468_0.png)

**Figure 18-10:** A complete disk scan analysis.

The treemap view can seem confusing at first, but once you get the hang of it you’ll see that you can glean quite a bit of information from the treemap.

The treemap works from the core of the diagram outward. The core represents the top level of the tree. In my example, because I performed a home scan, the core is my home folder, /home/rich. If you hover the mouse pointer over the core, it shows the name of the folder and the amount of disk space used by that folder.

The next layer of rings depicts the next level of folders. In my home folder I have three subfolders. Each subfolder is a section of the first-layer ring, and its size is relative to the amount of used disk space in that subfolder.

The second layer of rings relate to the first layer. If there are subfolders beneath a subfolder, they appear in the second layer of rings, above their parent folder. Again, each folder in the second layer has a size relative to the amount of disk space it uses.

This process continues for however many subfolders are contained in the filesystem being analyzed. You can quickly spot areas that use the most disk space by looking at the relative size of the ring sections (you can compare ring section sizes only on the same layer). This tool provides a great way to see at a glance where all of your disk space is going!

## Summary

This chapter discussed some of the system administration utilities provided in the Ubuntu workstation. The System Monitor allows you to monitor and control processes running on the system, as well as view the current CPU, memory, network, and disk utilization on that system.

The System Log Viewer provides an easy way to view all of the log files available in the Ubuntu workstation from a single window. You can view those log files, plus look at the daily log files from separate days that are stored on the system.

The Services Settings window allows you to view and change which system services are started when the system boots. You can select which services start, what system runlevel they start in, and the priority (order) in the runlevel that they start.

Separate from the Services Settings window, the Sessions Preferences window allows you to configure the individual applets and programs that automatically start when you log into your desktop. The Sessions Preferences window provides options for selecting which applets and programs start, for viewing which applets and programs are currently running in your session, and for saving your session settings so that the same applets and programs start the next time you log in.

The last section of this chapter discussed how to use the Disk Usage Analyzer tool. This tool helps you identify the areas in a filesystem that use the most amount of disk space. The Disk Usage Analyzer scans a disk area (or the entire disk) and provides a graphical treemap of the results. Each ring on the treemap represents a folder level in the filesystem hierarchy. Folders at the same level in the same ring are depicted with sizes relative to the amount of disk space they use.

In the next chapter we’ll take a look at the Ubuntu command line. The command-line interface can come in handy when trying to administer your system because it’s often quicker to enter commands than to interact with a graphical tool.
