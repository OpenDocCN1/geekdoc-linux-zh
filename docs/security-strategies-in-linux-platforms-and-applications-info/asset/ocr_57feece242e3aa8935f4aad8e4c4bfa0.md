# CHAPTER 14 | Detecting and Responding to Security Breaches

# 421

```
top - 17:33:44 up 3 days, 22:35, 5 users, load average: 1.20, 0.98, 0.78
Tasks: 173 total, 2 running, 171 sleeping, 0 zombie, 0 stopped
Cpu(s): 27.5us, 3.7sy, 0.0ni, 67.6wa, 0.0id, 1.0hi, 0.3si, 0.0st
Mem: 868808K total, 271734K used, 595524 free, 29795 buff
Swap: 1998808 total, 401880 used, 1597028 free, 1831672 free
```

> FIGURE 13-1
The top command provides a view of active processes.

| PID | USER VIRT RES SHR SFL SGL TSU %CPU %MEM TIME COMMAND |
|---|---|---|---|---|---|---|---|---|---|---||
| 30621 | member | 0 036m 375m 36m R 1 0 | 32 11.4 16:59.01 firefox |
| 7136 | root | 0 045m 14m 73m S 1 0 | 10 2.3 15:12.79 sqx |
| 7027 | member | 0 067a 049m 15m S 1 0 | 6 1.4 19:42.06 gnome-panel |
| 67823 | member | 0 000m 000m 000m S 1 0 | 0 0.0 00:18 gasterik |
| 7788 | member | 0 0136 5032 3076m S 1 0 | 3 0.1 27:16.02 at-spi-registry |
| 27348 | root | 0 0220 04864 1956m S 1 0 | 8 0.5 00:07.84 screenshot |
| 7986 | member | 0 0220 04864 195m S 1 0 | 5 0.7 06:13.02 lettuce |
| 7913 | member | 0 0170 6008 4452m S 1 0 | 2 0.2 03:48.05 gnome-screen |
| 8077 | member | 0 069m 837m 394m R 1 0 | 11 1.8 20:50.33 soft-bin |
| 15521 | member | 0 000m 000m 000m S 1 0 | 6 0.2 03:26.20 crowd |
| 24934 | member | 0 04936 15m 8964m S 1 0 | 0 0.5 07:57.62 notification-da |
| 80988 | member | 0 0138 105m 8338m S 1 0 | 1 3.2 11:36.88 gnome-netstatus |
| 7842 | root | 0 0330 108m 908m S 1 0 | 0 0.0 01:01.11 half-addon-str |
| 7933 | member | 0 000m 000m 000m S 1 0 | 0 0.1 01:40.52 gnome-terminal |
| 20897 | member | 0 0532 2814 1952m S 1 0 | 0 0.1 01:35.80 bash |
| 1 | root | 0 0244 1688 544 S 2 0 | 0 0.0 01:41.18 init |
| 2 | root | 0 15 -5 0 0 S 2 0 | 0 0.0 00:09.00 kithreadd |

# The System Status Package

The system status package, known as sysstat, includes a number of commands that can report status in a regular log. It includes the basic information associated with the top command, reported on a regular basis. Once the sysstat package is loaded and started, you can list the system status for the current day with the following command:

```
# sar A
```

Unfortunately, the Ubuntu version of the sysstat package can collect only one month's worth of data daily. if you're paying attention, that should be enough. If you want to view a report from the 13th of the month, use the following command:

```
# sar -f /var/log/sa/sa13
```

While the system status package configured for Red Hat Linux (RHEL) collects data for only seven days, it can be configured for many days as needed using the /etc/sysconfig/sysstat configuration file.

# For Additional Analysis

If you suspect a suspicious file or process, further investigation may be warranted. The following commands can help in that investigation: lsof, ldd, and trace.

# Analyze Processes with lsof

The lsof command lists all files opened by currently running processes. The use of the lsof -ni command to identify network-related processes was described in Chapter 13. A variation of that command is used later in this chapter to help diagnose problems on a possibly compromised system.