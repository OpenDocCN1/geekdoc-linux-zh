Another useful metric to pull from sar is disk statistics. The -b option gives you a basic list of disk I/O information:

```
```text
$ sar -b
Linux 2.6.24-22-server (kickseed)  01/07/2009

07:44:20 PM        tps     rtps     wtps   bread/s   bwrtn/s
07:45:01 PM       8.03     0.00     8.03      0.00    106.61
07:55:01 PM       8.78     0.14     8.64      3.35    127.59
08:05:01 PM       7.16     0.00     7.16      0.00     61.14
08:15:01 PM       8.17     0.14     8.03      5.82    139.02
08:25:01 PM       9.50     0.06     9.44      4.09    212.62
08:35:01 PM       8.27     0.00     8.27      0.01     74.66
08:45:01 PM       8.04     0.00     8.04      0.00     71.51
08:55:01 PM       7.64     0.00     7.64      0.00     66.46
09:01:18 PM       7.11     0.00     7.11      0.36     63.73
09:05:01 PM       7.61     0.00     7.61      0.00     72.11
Average:          8.11     0.04     8.06      1.67    102.52
```
```

Here you can see the number of total transactions per second (tps) plus how many of those transactions were reads and writes (rtps and wtps respectively). The bread/s column doesn’t measure bread I/O but instead tells you the average number of bytes read per second. The bwrtn/s similarly tells you average bytes written per second.

There are tons of individual arguments you can pass sar to pull out specific sets of data, but sometimes you just want to see everything all at once. For that just use the -A option. That will output all of the statistics from load average, CPU load, RAM, disk I/O, network I/O, and all sorts of other interesting statistics. This can give you a good idea of what sorts of statistics sar can output, so you can then read the sar manual (type man sar) to see what flags to pass sar to see particular statistics.

Of course, so far I’ve just listed how to pull all of the statistics for the current day. Often you want data from only a portion of the day. To pull out data for a certain time range, use the -s and -e arguments to specify the starting time and ending time you are interested in, respectively. For instance, if I wanted to pull CPU data just from 8:00 p.m. to 8:30 p.m., I would type

```
```text
$ sar -s 20:00:00 -e 20:30:00
```
```