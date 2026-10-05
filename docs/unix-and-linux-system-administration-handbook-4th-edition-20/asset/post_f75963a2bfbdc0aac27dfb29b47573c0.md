
values are unique per core within a physical socket. Cores that support hyperthreading (duplication of CPU contexts without duplication of other processing features) are identified by an ht in the flags. If hyperthreading is actually in use, the siblings field for each core shows how many contexts are available on a given core.

Another command to run for information on dmidecode. It dumps the system's Desktop Management Interface (DMI, aka SMBIOS) data. The most useful option is -t type; Table 29.2 shows the valid types.

## Table 29.2 Type values for dmidecode-t

| Value | Description |
| --- | --- |
| 1 | System information |
| 2 | Base board Information |
| 3 | Chassis information |
| 4 | Processor information |
| 7 | Cache information |
| 8 | Port connector information |
| 9 | System slot information |
| 11 | OEM strings |
| 12 | System configuration options |
| 13 | BIOS language information |
| 16 | Physical memory array |
| 17 | Memory device |
| 19 | Memory array mapped address |
| 32 | System boot information |
| 38 | IPMI device information |

The example below shows typical information:

```
sudo dmidecode -t 4
# dmidecode 2.7
BIOS 2.2 present.

Handle 00004, DMI type 4, 32 bytes.
Processor Information
  Socket Designation: PGA 370
  Type: Central Processor
  Family: Celeron
  Manufacturer: GenuineIntel
  ID: 65 06 00 00 FF F9 83 01
  Signature: Type 0, Family 6, Model 6, Stepping 5
```

# Chapter 29 Performance Analysis

Bits of network configuration information are scattered about the system. **ifconfig -a** is the best source of IP and MAC information for each configured interface.

![](img/579efec8c67772f31ecf34844bbb71a2_1168_0.png)

On Solaris systems, the **psinfo** and **prtconf** are the best sources of information about CPU and memory resources, respectively. Example output for these commands is shown below.

```
solaris$ prinfo -v
Status of virtual processor 0 as of: 01/31/2010 21:22:00
onon-line 07/13/2009 15:55:48.
The sparcv9 processor operates at 1200 MHz,
and has a sparcv9 floating point processor.
Status of virtual processor 1 as of: 01/31/2010 21:22:00
onon-line 07/13/2009 15:55:49.
The sparcv9 processor operates at 1200 MHz,
and has a sparcv9 floating point processor.
solaris$ prtconf
System Configuration: Sun Microsystems sun4v
Memory size: 32640 Megabytes
System Peripherals (Software Nodes):
SUNW,Sun-Fire-T200
```

![](img/579efec8c67772f31ecf34844bbb71a2_1168_1.png)

Under HP-UX, **machinfo** is an all-in-one command you can use to investigate a machine's hardware configuration. Here's some typical output:

```
hp-ux$ sudo machinfo
CPU info:
1 Intel(R) Titanium 2 processor (1.5 GHz, 6 MB)
400 MT/s bus, CPU version B1

Memory: 4084 MB (3.99 GB)

Firmware info:
Firmware revision: 02.21
FP SAW driver revision: 1.18
BMC firmware revision: 1.50

Platform info:
Model: "ia64 hp server rx2600"
OS info:
Nename: hpxux11
Release: HP-UX B.11.31
Machine: ia64
```

![](img/579efec8c67772f31ecf34844bbb71a2_1168_2.png)

It takes a bit of work to find CPU and memory information under AIX. First the **lscfig** command to find the names of the installed processors.

```
aix$ lscfig | grep Processor
+ proc0                                     Processor
+ proc2                                     Processor
```

# Analyzing CPU usage

You can use **isattr** to extract a description of each processor:

```
aix5$ isattr -E -1 proc0
frequency      1898100000 Processor Speed False
smt_enabled    true Processor SMT enabled False
smt_threads    2 in Processor SMT threads False
state          enable Processor state False
type           PowerPC_POWER5 Processor type False
```

**isattr** can also tell you the amount of physical memory in the system:

```
aix5$ isattr -E -1 sys0 -a realm
realmem       4014080 Amount of usable physical memory in Kbytes
```

# Gathering performance data

Most performance tools tell you what's going on at a particular point in time. However, the number and character of loads probably changes throughout the day. Be sure to gather a cross-section of data before taking action. The information on system performance becomes clear only after a long period (a month or more) of data collection. It is particularly important to collect data during periods of peak use. Resource limits and system misconfigurations are often visible when the machine is under heavy load.

# Analyzing CPU usage

You probably want to gather three kinds of CPU data: overall utilization, load averages, and per-process consumption. Overall utilization can help identify systems on which the CPU's speed is itself the bottleneck. Load averages give you an impression of system performance. Per-process CPU data can identify specific processes that hogging resources. You can obtain summary information with the **vmstat** command. **vmstat** takes two arguments: the number of seconds to monitor the system for and the number of reports to provide. If you don't specify the number of reports, **vmstat** runs until you press <Control-C>. The first line of data returned by **vmstat** reports averages since the system was booted. The subsequent lines are averages within the previous period, which defaults to five. For example:

```
$vmstat 5 0
procs ----------memory-----------swap----io----system----cpu----
r swpd free buff cache in cs us id
1 10 260356 428776 487092 0 0 7441 65 1063 85 25 1
1 10 2570324 428812 510196 0 0 4613 11 1054 73 25 1
1 10 2539028 428852 535636 0 0 5099 13 1057 52 91 9
1 10 2472340 428920 581588 0 0 4536 10 1056 4686 37 1
3 0 2440276 428960 605728 0 0 48218 21 1060 4943 20 3 77
```

After example columns shows how CPU utilization stats are fairly across consistent patterns. User time, system (kernel) time, idle time, and waiting for I/O are shown in the us, sy, and id columns on the far right. CPU numbers that are heavy on user time generally indicate computation, and high system numbers indicate that processes are making a lot of system calls or are performing lots of I/O.

A rule of thumb for general-purpose compute servers that served well over the years is that the system should spend approximately 50% of its time in user space and 50% in system space; the overall idle percentage should be non-zero. If you are dedicating a server to a single CPU-intensive application, the majority of time should be spent in user space.

The cs column shows context switches per interval (that is, the number of times the kernel changed which process was running). The number of interrupts per interval (usually generated by hardware devices or components of the kernel) is shown in the id column. Extremely high cs or in values typically indicate a misbehaving or misconfigured hardware device. The other columns are useful for memory and disk analysis, which we discuss later in this chapter.

Long-term averages of the CPU statistics let you determine there is enough power to go around. If the CPU spends part of its time in the idle state, there are cycles to spare. Upgrading to a faster CPU will not do much to improve the overall throughput of the system, though it may speed up individual operations.

As you can see from this example, the CPU generally flips-flops back and forth between heavy use and idleness. Therefore, it's important to observe these numbers as an average over time. The smaller the monitoring interval, the less consistent the results.

On multiprocessor machines, most tools present an average of statistics across all processors. On Linux, Solaris, and AIX, the mpstat command generates vmstat-like output for each individual. The -P flag lets you report on. mpstat is useful for debugging software that reports symmetric multiprocessing—it's also enlightening to see how efficient your system uses multiple processors. Here's an example that shows the status of each of four processors:

```
mpstat -P ALL
08:13:38 PM CPU %user %nice %sys %iowait %irq %soft %idle intr/
08:13:38 PM 0 1.02 0.00 0.49 1.29 0.04 0.03 96.79 473.93
08:13:38 PM 1 0.28 0.00 0.22 0.71 0.00 0.01 98.76 232.86
08:13:38 PM 2 0.42 0.00 0.36 1.32 0.00 0.05 97.84 293.85
08:13:38 PM 3 0.38 0.00 0.30 0.94 0.01 0.05 98.32 295.02
```

On a workstation with only one user, the CPU generally spends most of its time idle. When you render a web page or switch windows, the CPU is heavily for a short period. In this situation, information about long-term average CPU usage is not meaningful.
