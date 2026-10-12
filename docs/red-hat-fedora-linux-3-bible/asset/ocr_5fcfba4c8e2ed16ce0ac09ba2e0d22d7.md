> TIP: The `-xdev` option prevents file systems other than the selected file system from being searched. This is a good way to cut out a lot of junk that may be output from the `/proc` file system. It could also keep large remotely mounted file systems from being searched.

The next example is similar to the previous one, except that instead of looking for a user's files, this command line looks for files that are larger than 100 kilobytes (`-size 100k`):

```
# find / -size 100k -print | xdev -xdev | xargs ls -1ds > /tmp/size
```

You can save yourself a lot of disk space by just removing some of the largest files that are no longer needed. Open the `/tmp/size` file in this example and large files are sorted by size.

# Monitoring System Performance

If your Linux system is being used as a multiuser computer, sharing the processing power of that computer can be a major issue. Likewise, any time you can stop a runaway process or reduce the overhead of an unnecessary program running, your Linux server can do a better job serving files, Web pages, or e-mail to the people that rely on it.

Utilities are included with Linux that can help you monitor the performance of your Linux system. The kinds of features you want to monitor in Linux include CPU usage, memory usage (RAM and swap space), and overall load on the system. The following sections describe tools for monitoring Linux.

# Watch computer usage with System Monitor

If you like visual representations of your system use, the System Monitor provides a great way to see how much your system is being used. To open the System Monitor from the red hat menu, select System Tools \u2192 System Monitor. Figure 10-5 shows the System Monitor window with the Resource Monitor tab selected.

On the Resource Monitor window, lines scroll from right to left, indicating the percentage of your CPU being used as it rises and falls. You can also see how much of your total memory (RAM) is being used at the moment (or over time), as well as the amount of swap space being used. Scroll the devices at the bottom of the window to see the space being consumed on each of your hard disk partitions.

Click the Process Listing tab to see a listing of processes that are running currently. Click the columns in that tab to sort processes by name, user (who launched the process), memory use, percentage of CPU being consumed by the process, and process ID.