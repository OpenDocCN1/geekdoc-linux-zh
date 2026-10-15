
## Example 6-11 Using iostat to get CPU and I/O statistics

```
[root@UDBLNX06 root]# iostat 1
Linux 2.4.18-14 (UDBLNX06)    11/06/2002

avg-cpu:  %user   %nice   %sys   %idle
         1.98    0.00    0.66   97.36

Device:         tps   Blk_read/s   Blk_wrn/s   Blk_read   Blk_wrtn
dev3-0        5.44      50.72     119.68    1269102    2994466
dev3-1        0.00       0.01       0.00        304          0

avg-cpu:  %user   %nice   %sys   %idle
        64.00    0.00   19.00   17.00

Device:         tps   Blk_read/s   Blk_wrn/s   Blk_read   Blk_wrtn
dev3-0      184.00    5120.00    3216.00      5120       3216
dev3-1        0.00       0.00       0.00          0          0

avg-cpu:  %user   %nice   %sys   %idle
        65.00    0.00   20.00   15.00

Device:         tps   Blk_read/s   Blk_wrn/s   Blk_read   Blk_wrtn
dev3-0      208.00    6144.00    3328.00      6144       3328
dev3-1        0.00       0.00       0.00          0          0

avg-cpu:  %user   %nice   %sys   %idle
        69.00    0.00   18.00   13.00

Device:         tps   Blk_read/s   Blk_wrn/s   Blk_read   Blk_wrtn
dev3-0      180.00    5136.00    3192.00      5136       3192
dev3-1        0.00       0.00       0.00          0          0
```

## 6.3.4 Sar

The sar command is an integrated and powerful System Activity Report (sar) utility. You can use it to collect and report CPU utilization, memory and swap space utilization statistics, I/O and transfer rate statistics, as well as network statistics, and so forth. You can save the output of the sar command into a designated file and retrieve information from that file at a later time.

The general syntax to run the sar command is:

```
sar [ options ] [ interval [ count ] ]
```

Table 6-3 gives some frequently used command options for sar which are extracted from sar's man pages.

## Table 6-3 Frequently used command options for sar

| Options | Description |
|---|---|
| -A | This is equivalent to specifying -bdcqrRuvvWy -I SUM -I PROC -n FULL -U ALL. |
| -b | Reports I/O and transfer rate statistics. |
| -c | Reports process creation activity. |
| -d | Reports activity for each block device. |
| -e | Sets the ending time of the report. |
| -f | Extracts records from filename (created by the -o filename flag). The default value of the filename parameter is the current daily data file, the /var/log/sa/sadd file. The -f option is exclusive of the -o option. |
| -n | Reports network statistics. |
| -o | Saves the readings in the file in binary form. |
| -q | Reports queue length and load averages. |
| -r | Reports memory and swap space utilization statistics. |
| -s | Sets the starting time of the data, causing the sar command to extract records time-tagged at, or following, the time specified. |
| -u | Reports CPU utilization. |
| -U | Reports CPU utilization for a given processor. |
| -v | Reports status of inode, file and other kernel tables. |
| -w | Reports system switching activity. |
| -x | Reports statistics for a given process. |

Some samples of using sar command are provided below. In Example 6-12, at first, sar is started with "-A" command option and the output is saved in sartest.bin file. For testing purpose, you can generate some CPU load for sar to report; for example, loading data into DB2 database in a multiple partition environment. Then you can obtain the desired report from the saved file for different system activities. For example:

```
sar -u -s 11:09:00 -f sartest.bin|more
```

The above command can be used to get CPU utilization information since a specified starting time.

```
sar -w -c -s 11:09:10 -e 11:09:25 -f sartest.bin|more
```

The above command can be used to get process creation/fork and system context switch information.

And the command below can be used to obtain network statistics for a specific network interface.

```
sar -n DEV -s 11:09:25 -f sartest.bin|egrep "eth0|IFACE"
```

See Example 6-12 for more details.

## Example 6-12 Using sar to monitor system activities

```
[root@UDBLNX06 root]# sar -A -o sartest.bin 2 20
[root@UDBLNX06 root]# sar -u -s 11:09:00 -f sartest.bin|more
Linux 2.4.18-14 (UDBLNX06) 11/07/2002

11:09:01 AM CPU %user %nice %system %idle
11:09:03 AM all 0.00 0.00 0.00 100.00
11:09:05 AM all 0.50 0.00 0.50 99.00
11:09:07 AM all 0.00 0.00 0.50 99.50
11:09:09 AM all 0.00 0.00 0.00 100.00
11:09:11 AM all 1.00 0.00 1.00 98.00
11:09:13 AM all 8.50 0.00 32.50 59.00
11:09:15 AM all 14.50 0.00 48.00 37.50
11:09:17 AM all 5.50 0.00 6.50 88.00
11:09:19 AM all 17.50 0.00 11.00 71.50
11:09:21 AM all 11.00 0.00 12.50 76.50
11:09:23 AM all 23.50 0.00 9.00 67.50
11:09:25 AM all 67.00 0.00 19.50 13.50
11:09:27 AM all 62.00 0.00 18.00 20.00
11:09:29 AM all 65.00 0.00 20.00 15.00
11:09:31 AM all 63.00 0.00 19.00 18.00
11:09:33 AM all 63.00 0.00 18.00 19.00
11:09:35 AM all 66.00 0.00 18.00 16.00
Average: all 27.53 0.00 13.76 58.71
```

```
[root@UDBLNX06 root]# sar -w -c -s 11:09:10 -e 11:09:25 -f sartest.bin|more
Linux 2.4.18-14 (UDBLNX06) 11/07/2002

11:09:11 AM proc/s
11:09:13 AM 3.00
11:09:15 AM 4.50
11:09:17 AM 1.50
11:09:19 AM 0.00
11:09:21 AM 2.00
11:09:23 AM 0.00
11:09:25 AM 0.00
Average: 1.83

11:09:11 AM cswch/s
```
