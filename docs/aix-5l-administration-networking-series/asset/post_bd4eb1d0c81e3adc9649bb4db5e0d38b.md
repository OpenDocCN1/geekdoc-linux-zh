
## The no Command

One very important command to know in AIX networking is the networking options, or **no**, command. As more and more networks are upgraded to gigabit Ethernet, as well as high-performance 100 megabit Ethernet networks, it is important to set the TCP send and receive spaces to 65535 in order to accommodate its “jumbo frames.” Whenever the TCP send or receive space parameters are changed, remember that the **inetd** daemon must be refreshed in order for the changes to take effect. An example of setting those parameters is as follows:

```
# no -O tcp_sendspace=65535
# no -O tcp_receivespace=65535
# refresh -s inetd
0513-095 The request for subsystem refresh was completed successfully.
```

For a detailed explanation of all the options available with the **no** command, please refer to the AIX 5L Version 5.1 Commands Reference that shipped with your copy of AIX 5L.

## The netstat Command

Traditionally, the **network** statistics, or **netstat**, command is used more for problem determination than for performance monitoring. It can, however, be used to determine the amount of traffic on the network to determine if performance problems are due to network congestion. To see the statistics for all configured interfaces on a system, enter the following command:

```
# netstat -I
```

| Name  | Mtu   | Network    | Address      | Ipkts | Ierrs | Opkts | Oerrs | Coll |
|-------|-------|------------|--------------|-------|-------|-------|-------|------|
| lo0   | 16896 | link#1     |              | 144834| 0     | 144946| 0     | 0    |
| lo0   | 16896 | 127        | localhost    | 144834| 0     | 144946| 0     | 0    |
| lo0   | 16896 | ::1        |              | 144834| 0     | 144946| 0     | 0    |
| en0   | 1500  | link#2     | 8:0:5:a:d2:a5| 0     | 0     | 112   | 0     | 0    |
| en0   | 1500  | 1.2.3      | Lazarus      | 0     | 0     | 112   | 0     | 0    |

- **Name** The name of the network interface. In our example system, there are only two network interfaces configured, lo0, which is the loopback device, and en0, a 10MB Ethernet card
- **MTU** The Maximum Transmission Unit size for the interface
- **Network** What network the interface is attached to
- **Address** The hardware address and name of the adapter. If the **-n** flag is specified, this will show the IP address of the interface instead of the name
- **Ipkts** Number of packets received (input) on the interface
- **Ierrs** Number of receive errors for the interface
- **Opkts** Number of packets sent (output) to the interface
- **Oerrs** Number of transmit errors for the interface
- **Coll** Number of collisions for the interface

From this report, we can see that this system does not have very much network traffic, since everything seems to be going through the loopback interface.

# AIX TUNING TOOLS

Up to this point, we have discussed tools that will offer a snapshot of exactly what the system is doing now. These tools are great for reacting to a bad situation and correcting it, also known as putting out fires, but our goal is to be proactive, not reactive, to our systems. We want to be able to know what direction the system is heading and to be able to anticipate changes that should be made before performance degrades to the point that the user community notices. In order to do that, we will need some tools to help us record and analyze trends.

## Traditional UNIX Tools

We have already discussed many of the traditional UNIX tools, such as *vmstat*, *vmtune*, *iostat*, and *netstat*. Without having to do too much work, it would be easy to create a script that could be run by *cron* that would collect data from these commands at regular times into a file that could be examined by a Systems Administrator for trend analysis. Just be sure to schedule a job to clean up old entries in the file; we don’t want to fill up a filesystem with performance data!

## The topas Command

Another traditional tool that captures much of the same data as these commands, and formats it into one easy-to-use screen, is the *topas* command. Running *topas* with no options produces the following screen:

![](img/82f851021955589d82b22750fb3b1646_582_0.png)

Here, in one screen, is a view of everything that we need to be concerned with: CPU performance, network interfaces, disk I/O, NFS I/O, and what the largest processes running on the system are. This screen will automatically refresh itself every two seconds, until you exit **topas**. While **topas** is a great tool, again it is only a snapshot of the system as it is right now; it will not help us to look for trends on the system.

## The sar Command

The **sar** command is used to gather statistical data about CPU usage. One of the nice features of **sar** is that it can break out the statistics for each processor in a multiprocessor system. Earlier in this chapter, we looked at using the **vmstat** command to view the percentage of CPU time that was being consumed by system, user, idle, and wait times. When using **vmstat** to report this, we are looking at an average of all the processors in the system. Using **sar**, we can break those numbers out by processor, as seen in the following example:

```
# sar -u -P ALL 1 5

AIX Lazarus 1 5 000031037500 04/20/02

13:33:42 cpu user %sys %wio %idle
13:33:43 0 0 0 0 100
1 0 0 0 100
2 0 0 0 100
3 0 0 0 100
- 0 0 0 100
13:33:44 0 2 66 0 32
1 0 1 0 99
2 0 0 0 100
3 0 1 0 99
- 0 17 0 82
13:33:45 0 1 52 44 3
1 0 1 0 99
2 0 4 0 96
3 0 0 0 100
- 0 14 11 74
13:33:46 0 0 8 91 1
1 0 0 0 100
2 0 0 0 100
3 0 1 0 99
- 0 2 23 75
13:33:47 0 0 7 93 0
1 0 0 0 100
2 0 1 0 99
3 0 0 0 100
- 0 2 23 75
Average 0 1 27 46 27
1 0 0 0 100
2 0 1 0 99
3 0 0 0 100
- 0 7 11 81
```

Using the combination of the `-u` and `-P` flags, along with the `ALL` processors keyword, gave us the per-processor statistics sampled at one-second intervals and repeated five times. Two other important flags we should be familiar with are the `-o` and `-f` flags. The `-o` flag is used to output `sar` data to a binary file, and the `-f` flag is used to read from that file. Using these two flags, we could transfer the `sar` data to another system, and report on it there, thus minimizing the performance impact on the system we are analyzing.

If we take a look at the file `/var/spool/cron/crontabs/adm`, we will see that entries have already been made to allow `/usr/lib/sa/sa1` and `/usr/lib/sa/sa2` to collect performance data but are commented out. These two programs are special versions of `sar` that have been modified to be run by the `cron` daemon. See Chapter 28 for complete details on configuring system accounting and `sar`.

## Performance Diagnostic Tool

The Performance Diagnostic Tool (PDT) is an optionally installable tool within AIX that collects performance and configuration information and attempts to identify potential problems. It is installed via the file set `bos.perf.diag.tool`. After installation, it is activated by running the command `/usr/sbin/perf/diag_tool/pdt_config`. This command will cause appropriate entries to be placed into the `adm` crontab file that will allow the tool to begin periodically collecting data. By default, PDT will keep approximately one month's worth of performance data on the system and will e-mail a daily report to the `adm` user. This report is broken down into five sections: Header, Alerts, Upward And Downward Trends, System Health, and Summary. The following is an example of a PDT report:

```
Performance Diagnostic Facility 1.0

Report printed: Wed Apr 17 17:54:50 2002

Host name: Lazarus
Range of analysis includes measurements
from: Hour 12 on Tuesday, April 16th, 2002
to: Hour 17 on Wednesday, April 17th, 2002

Notice: To disable/modify/enable collection or reporting
execute the pdt_config script as root
------------------- Alerts ------------------------

### I/O CONFIGURATION

- Note: volume hdisk1 has 872 MB available for allocation
while volume hdisk0 has 148 MB available
- Physical volume hdisk2 is unavailable; (in no volume group)

### PAGING CONFIGURATION

- Physical Volume hdisk2 (type: SCSI) has no paging space defined
- Paging space paging00 on volume group rootvg is fragmented
- Paging space paging01 on volume group uservg is fragmented

### I/O BALANCE

- Phys. volume hdisk2 is not busy
volume hdisk2, mean util. = 0.00 %

### PROCESSES

- First appearance of 20642 (cpubound) on top-3 cpu list
(cpu % = 24.10)
- First appearance of 20106 (eatmem) on top-3 memory list
(Memory % = 8.00)

### FILE SYSTEMS

- File system hd2 (/usr) is nearly full at 100 %

### NETWORK

- Host ah0000e appears to be unreachable.
(ping loss % = 100) and has been for the past 4 days

------------------- Upward Trends ------------------------

### FILES

- File (or directory) /usr/adm/avgm SIZE is increasing
now, 20 KB and increasing an avg. of 2163 bytes/day
- File (or directory) /var/adm/rag/ SIZE is increasing
now, 677 KB and increasing an avg. of 11909 bytes/day

### FILE SYSTEMS

- File system hd9var (/var) is growing
now, 17.00 % full, and growing an avg. of 0.38 %/day
- File system lvo0 (/usr/vice/cache) is growing
now, 51.00 % full, and growing an avg. of 4.64 %/day
At this rate, lvo0 will be full in about 9 days
```
