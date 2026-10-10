| Option Name | Meaning |
|---|---|
| -o *filename* | Saves data to the specified file in binary form. |
| -P *cpu* | Displays CPU use data. The *cpu* code may be a CPU number or ALL. |
| -r | Reports memory and swap space use information. This information is more detailed than that reported by the free utility. |
| -s `[hh:mm:ss]` | Sets the start time for data display. |
| -u | Reports CPU use data. This is the default. |
| -W | Displays swap statistics. |

The sar utility is useful for tracking down the source of system slowdowns. If you receive complaints that the computer slows down at particular times of the day, you can use sar to examine the load on memory, CPU, devices, and so on, throughout the day to look for patterns of what might be causing the slowdown. The tool is most helpful if you’re familiar with normal operations, so you may want to use it on a regular basis for a while, preferably on several Linux systems that perform different types of tasks, to see what sorts of loads occur on a variety of Linux systems.

# ### Obtaining Input/Output Statistics

The iostat utility is more specialized than sar, but it can still produce a wide range of system statistics. These include reports on CPU utilization, block device input/output, and Network File System (NFS) activity. Its syntax is similar to that of sar:

```
iostat [options] [interval [count]]
```

Table 3.5 summarizes some of the more common iostat options. If used without options, iostat produces a CPU report followed by a report on block devices, similar to what typing iostat -cd produces.

| Option Name | Meaning |
|---|---|
| -c | Creates a CPU utilization report |
| -d | Creates a device utilization report |