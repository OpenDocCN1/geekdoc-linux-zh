
## 797

```
# showmount -e
/apply
/usr/users
/cdrom
```

## Showing System Swap

If your system has insufficient main memory for all the information it needs to work with, it will move pages of information to your swap area or swap entire processes to your swap area. Pages that were most recently used are kept in main memory, and those not recently used will be the first moved out of main memory.

System administrators spend a lot of time determining the right amount of swap space for their systems. Insufficient swap may prevent a system from starting additional processes, hang applications, or not permit additional users to get access to the system. Having sufficient swap prevents these problems from occurring. System administrators usually go about determining the right amount of swap by considering many important factors, including the following:

1. How much swap is recommended by the application(s) you run? Use the swap size recommended by your applications. Application vendors tend to be realistic when recommending swap space. There is sometimes competition among application vendors to claim the lowest memory and CPU requirements in order to keep the overall cost of solutions as low as possible, but swap space recommendations are usually realistic.
2. How many applications will you run simultaneously? If you are running several applications, sum the swap space recommended for each application you plan to run simultaneously. If you have a database application that recommends 200 MBytes of swap and a development tool that recommends 100 MBytes of swap, then configure your system with 300 MBytes of swap, minimum.
3. Will you be using substantial system resources on peripheral functionality such as NFS? The nature of NFS is to provide access to file systems, some of which may be very large, so this use may have an impact on your swap space requirements.

Swap is listed and manipulated on different UNIX variants with different commands. The following example shows listing the swap area on a Solaris system with `swap -l`.

```
# swap -l
swapfile dev swaplo blocks free
/dev/dsk/c0t3d0s1 32,25 8 263080 209504
```

These values are all in 512 KByte blocks. In this case, the free blocks are 209504, which is a significant amount of the overall swap allocated on the system.

You can view the amount of swap being consumed on your HP-UX system with `swapinfo`. The following is an example output of `swapinfo`:

```
# swapinfo
```

| TYPE | Kb AVAIL | Kb USED | Kb FREE | PCT USED | START/LIMIT | RESERVE | PRI | NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| dev | 49152 | 10532 | 38620 | 21% | 0 | - | 1 | /dev/vg00/lvol2 |
| dev | 86832 | 10888 | 759160 | 1% | 0 | - | 1 | /dev/vg00/lvol8 |
| reserve | 532360 | -532360 | | | | | | |
| memory | 816360 | 469784 | 346576 | 58% | | | | |

Following is a brief overview of what `swapinfo` gives you.

In the preceding example, the “TYPE” field indicated whether the swap was “dev” for device, “reserve” for paging space on reserve, or “memory.” Memory is a way to allow programs to reserve more virtual memory than you have hard disk paging space set up for on your system.

“Kb AVAIL” is the total swap space available in 1024-byte blocks. This includes both used and unused swap.

“Kb USED” is the current number of 1024-byte blocks in use.

“Kb FREE” is the difference between “Kb AVAIL” and “Kb USED.”

“PCT USED” is “Kb USED” divided by “Kb AVAIL.”

“START/LIMIT” is the block address of the start of the swap area.

“Kb RESERVE” is “-” for device swap or the number of 1024-byte blocks for file system swap.

“PRI” is the priority given to this swap area.

“NAME” is the device name of the swap device.

You can also issue the **swapon** command with a series of options. Here are some of the options you can include:

- -m to display output of **swapinfo** in MBytes rather than in 1024-byte blocks.
- -d prints information related to device swap areas only.
- -f prints information about file system swap areas only.

## sar: The System Activity Reporter

**sar** is another UNIX command for gathering information about activities on your system. You can gather data over an extended time period with **sar** and later produce reports based on the data. **sar** is similar among UNIX variants in that the options and outputs are similar. The Linux system I was using for the examples did not support **sar**, but the Solaris, HP-UX, and AIX systems had the same options and nearly identical outputs. The following are some useful options to **sar**, along with examples of reports produced with these options where applicable:

- **sar -o** Save data in a file specified by “o.” After the file name, you would usually also enter the time interval for samples and the number of samples. The following example shows saving the binary data in file /tmp/sar.data at an interval of 60 seconds 300 times:

```
# sar -o /tmp/sar.data 60 300
```

The data in /tmp/sar.data can later be extracted from the file.

- **sar -f** Specify a file from which you will extract data.

- **sar -u** Report CPU utilization with the headings %usr, %sys, %wio, %idle with some processes waiting for block I/O, %idle. This report is similar to the iostat and vmstat CPU reports. You extract the binary data saved in a file to get CPU information, as shown in the following example. The following is a **sar -u** example:

```
# sar -u -f /tmp/sar.data

Header Information for your system
12:52:04   %usr   %sys   %wio   %idle
12:53:04      62     4     5      29
12:54:04      88     5     3       4
12:55:04      94     5     1       0
12:56:04      67     4     4      25
12:57:04      59     4     4      32
12:58:04      61     4     3      32
12:59:04      65     4     3      28
13:00:04      62     5    16      17
13:01:04      59     5     9      27
13:02:04      71     4     3      22
13:03:04      60     4     4      32
13:04:04      71     5     4      20
13:05:04      80     6     8       7
13:06:04      56     3     3      37
13:07:04      57     4     4      36
13:08:04      66     4     4      26
13:09:04      80    10     2       8
13:10:04      73    10     2      15
13:11:04      64     6     3      28
13:12:04      56     4     3      38
13:13:04      55     3     3      38
13:14:04      57     4     3      36
13:15:04      70     4     5      21
13:16:04      65     5     9      21
13:17:04      62     6     2      30
13:18:04      60     5     3      33
13:19:04      77     3     4      16
13:20:04      76     5     3      15
14:30:04      50     6     6      38
14:31:04      57    12    19      12
14:32:04      51     8    20      21
14:33:04      41     4     9      46
14:34:04      43     4     9      45
14:35:04      38     4     6      53
14:36:04      38     9     7      46
14:37:04      46     3    11      40
14:38:04      43     4     7      46
14:39:04      37     4     5      54
14:40:04      33     4     5      58
14:41:04      40     3     3      53
14:42:04      44     3     3      50
14:43:04      27     3     7      64
Average        57     5     8      30
```

- **sar -b** Report buffer cache activity. A database application such as Oracle would recommend that you use this option to see the effectiveness of buffer cache use. You extract the binary data saved in a file to get CPU information, as shown in the following example:

```
# sar -b -f /tmp/sar.data
Header information for your system

12:52:04 breads/s freads/s wroache lwrite/s lwrit/s wreache pread/s pwrite/s
12:53:04 5 608 38 1 11 95 0 0
12:54:04 7 759 99 0 14 99 0 0
12:55:04 2 1733 166 4 24 83 0 0
12:56:04 1 836 100 1 18 96 0 0
12:57:04 0 623 100 2 21 92 0 0
12:58:04 0 779 100 1 16 94 0 0
12:59:04 0 1125 100 0 14 98 0 0
13:00:04 2 1144 100 9 89 89 0 0
13:01:04 10 899 99 11 76 86 0 0
13:02:04 0 1156 100 0 14 99 0 0
13:03:04 1 578 100 2 12 88 0 0
13:04:04 5 1251 100 0 12 99 0 0
```

## sar -d

Report disk activity. You get the device name, percent that the device was busy, average number of requests outstanding for the device, number of data transfers per second for the device, and other information. You extract the binary data saved in a file to get CPU information, as shown in the following example:

```
# sar -d -f /tmp/sar.data
Header information for your system
12:54:04  device  %busy  avgqu   ...  ...  ...  ...  ...  ...
c0t6d0    0.95    1.41   1       ...  ...  4   ...  ...  ...  ...
```

![img/eff8b9287a5f38c5adf538f24aacf29e_802_0.png](img/eff8b9287a5f38c5adf538f24aacf29e_802_0.png)

