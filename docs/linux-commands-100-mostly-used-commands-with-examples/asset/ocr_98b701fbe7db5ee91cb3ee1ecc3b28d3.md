```
mpstat -A
```

# 40. sar: Collect, report, or save system activity information.

The `sar` command in Linux is used to collect, report, and save system activity information. It provides a wide range of statistics about the system's performance, including CPU utilization, memory usage, disk activity, network activity, and more. The data collected by `sar` can be useful for performance analysis and troubleshooting.

Examples:

+   1. Display CPU utilization statistics at 5-second intervals, 3 times:

```
sar -u 5 3
```

+   2. Display memory utilization statistics at 10-second intervals, 5 times:

```
sar -r 10 5
```

+   3. Display I/O and transfer rate statistics at 1-minute intervals indefinitely: