# TIP

The -xdev option prevents file systems other than the selected file system from being searched. This is a good way to cut out a lot of junk that may be output from the /proc file system. It could also keep large, remotely mounted file systems from being searched.

The next example is similar to the previous one, except that instead of looking for a user’s files, this command line looks for files that are larger than 1,000 KB (-size +1000k):

```
find / -xdev -size +1000k -print | xargs ls -lDS > /tmp/size
```

You can save yourself a lot of disk space by just removing some of the largest files that are no longer needed. Open the /tmp/size file in this example, and large files are sorted by size.

# Monitoring System Performance

If your Linux system is being used as a multiser computer, sharing the processing power of that computer can be a major issue. Likewise, any time you can stop a runaway process or reduce the overhead of an unnecessary program running, your Linux server can do a better job serving files, Web pages, or e-mail to the people who rely on it.

Utilities are included with Linux that can help you monitor the performance of your Linux system. The kinds of features you want to monitor in Linux include CPU usage, memory usage (RAM and swap space), and overall load on the system. The following sections describe tools for monitoring Linux.

# Watch Computer Usage with System Monitor

If you like visual representations of your system use, the System Monitor provides a great way to see how much your system is being used. To open the System Monitor from the System menu on the GNOME panel, select Administration > System Monitor. Figure 9-5 shows the System Monitor window with the Resources tab selected.

On the Resource Monitor window, lines scroll from right to left, indicating the percentage of your CPU being used as it rises and falls. You can also see how much of your total memory (RAM) is being used at the moment (and over time), as well as the amount of swap space being used. The bar at the bottom of the window shows the amount of data being sent and received over your computer’s network interfaces.

Click on the Processes tab to see a listing of processes that are running for the current user. Click on the columns in that tab to sort processes by name, memory use, percentage of CPU being consumed by the process, and process ID. There are also columns showing the security context of the process (if SELinux is enabled) and the arguments associated with the process.

Click on the File Systems tab to see the storage devices (hard disk partitions, CD, USB flash drive, or other) that are currently mounted on your computer. Click columns to sort the devices by device name, directory name, file system type, total disk space, free disk space, or used disk space.