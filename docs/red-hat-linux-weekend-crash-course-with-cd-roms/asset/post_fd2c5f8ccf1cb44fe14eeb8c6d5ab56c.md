
```
0 0 0 4724 1980 3416 18064 0 0 4 4 182 363 54 15 31
2 0 0 4724 1960 3416 18064 0 0 0 4 142 126 13 7 80
0 0 0 4724 1960 3416 18064 0 0 0 3 132 183 7 9 84
0 0 0 4724 1948 3416 18076 0 0 0 1 112 90 7 8 86
```

The tabular output is grouped into six categories of information, as indicated by the fields in the first line of output. The second line shows categories for each of the six major fields. You can interpret the six fields and their categories using the following table:

| Field Name | Description |
|---|---|
| Procs | Number of processes and their types: r = processes waiting to run; b = processes in uninterruptible sleep; w = processes swapped out, but ready to run |
| Memory | Information about physical memory and swap space usage (all numbers in kilobytes): swpd = virtual memory used; free = free physical memory; buff = memory used as buffers; cache = cached virtual memory |
| Swap | Amount of swapping (all numbers in kilobytes per second): si = amount of memory swapped in from disk; so = amount of memory swapped to disk |
| Io | Information about input and output (all numbers in blocks per second in which the block size depends on the disk device): bi = rate of blocks sent to disk; bo = rate of blocks received from disk |
| System | Information about the system: in = number of interrupts per second (including clock interrupts); cs = number of context switches per second — the number of times the kernel changes the running process |
| cpu | Percentages of CPU time used: us = percentage of CPU time used by user processes; sy = percentage CPU time used by system processes; id = percentage of time CPU is idle |

The first line of output following the two header lines shows the averages since the last reboot. After that, vmstat displays the 5-second average data seven more times over the next 35 seconds. In the vmstat utility's output, high values in the si and so fields indicate too much swapping. High numbers in the bi and bo fields indicate too much disk activity.

## Checking Disk Performance and Disk Usage

Red Hat Linux comes with the /sbin/hdparm program that you can use to check disk performance and usage. It controls IDE or ATAPI hard disks that are common on most PCs. One feature of the hdparm program is that the -t option enables you to determine the rate at which data can be read from the disk into a buffer in memory. For example, here’s the result of this command on my system:

```
/sbin/hdparm -t /dev/hda

/dev/hda:
  Timing buffered disk reads:  64 MB in 15.18 seconds =  4.22 MB/sec
```

As you can see, the command requires the IDE drive’s device name (/dev/hda) as an argument. If you have an IDE hard disk, you can try this command to see how fast data can be read from your system’s disk drive.

To display the space available in the currently mounted file systems, use the df command. If you want a more human-readable output from df, type the following command:

```
df -h
Filesystem     Size  Used Avail Use% Mounted on
/dev/hda2      1.9G  1.1G  765M  59% /
/dev/hda1      2.0G  1.8G  256M  88% /dos c
```

As this example shows, the -h option causes the df command to show the sizes in gigabytes (G) and megabytes (M).

To check the disk space a specific directory uses, employ the du command. You can specify the -h option to view the output in kilobytes (k) and megabytes (M), as shown in the following example:

```
du -h /var/log
12k     /var/log/httpd
4.0k    /var/log/news/OLD
8.0k    /var/log/news
4.0k    /var/log/vbox
20k     /var/log/samba
4.0k    /var/log/sa
576k    /var/log
```

The du command displays the disk space used by each directory and the last line shows the total disk space used by that directory. If you want to see only the total space used by a directory, type the -s option like this:

```
du -sh /home
16M      /home
```

## Exploring the /proc File System

You can find out a great deal about your Red Hat Linux system by consulting the contents of a special file system known as the /proc (also called the process file system) file system. It can help you monitor a wide variety of information about your system. In fact, you can even change kernel parameters through the /proc file system and thereby modify the system’s behavior.

The /proc file system is not a real directory on the disk, but a collection of data structures in memory (managed by the Linux kernel) that appears to the user as a set of directories and files.

You can access the /proc file system and navigate it just as you do any other directory, but you have to know the meaning of various files to interpret the information. Typically, you can use the cat or more command to view the contents of a file in /proc; the file’s contents provide information about some aspect of the system.

As with any directory, you may want to start by looking at a detailed directory listing of /proc. To do so, type ls -l /proc. In the output, the first set of directories (indicated by the letter d at the beginning of the line) represents the processes that are currently running on your system. Each directory that corresponds to a process has the process ID (a number) as its name.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_346_0.png)

You should also notice a very large file in the listing named /proc/kcore; that file represents the entire physical memory of your system. There is no physical file occupying that much space on your hard disk, so do not try to remove the file to reclaim disk space.

The /proc/cpuinfo file in /proc lists the key characteristics of your system, such as processor type and floating-point processor information. You can view the processor information by typing cat /proc/cpuinfo. For example, here is what I get when I type this command on my system:

```
cat /proc/cpuinfo
processor      : 0
vendor_id      : GenuineIntel
cpu family     : 5
model          : 4
model name     : Pentium MMX
stepping       : 3
cpu MHz        : 199.616468
fdiv_bug       : no
hlt_bug        : no
sep_bug        : no
f00f_bug       : yes
fpu            : yes
fpu_exception  : yes
cpuid level    : 1
wp             : yes
flags          : fpu vme de pse tsc msr mce cx8 mmx
bogomips       : 398.13
```

This output is from a 200MHz Pentium MMX system. The listing shows many interesting characteristics of the processor. Notice the line that starts with fdiv_bug. Remember the infamous Pentium floating-point division bug? The bug is in an instruction called fdiv (for floating-point division). Thus, the fdiv_bug line indicates whether this particular Pentium has the bug (fortunately, my system's processor does not).

The last line in the /proc/cpuinfo file shows the BogoMips for the processor, as computed by the Linux kernel when it boots. BogoMips is something that Linux uses internally to calibrate time delay loops.

Table 28-1 summarizes some of the files in the /proc file system from which you can get information about your Red Hat Linux system. You can view some of these files on your system to see what they contain.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_347_0.png)

Not all the files shown in Table 28-1 are present on your system. The contents of the /proc file system depends on the kernel configuration and the loaded driver modules (which, in turn, depend on your PC's hardware configuration).

## Table 28-1

Some Files and Directories in /proc

| Filename | Content |
|---|---|
| /proc/apm | Information about advanced power management (APM) |
| /proc/bus | Directory with bus-specific information for each bus type, such as PCI |
| /proc/cmdline | The command line used to start the Linux kernel (for example, auto BOOT_IMAGE=linux ro root=303) |
| /proc/cpuinfo | Information about the CPU (the microprocessor) |
| /proc/devices | Available block and character devices in your system |
| /proc/dma | Information about DMA (direct memory access) channels in use |
| /proc/filesystems | List of supported file systems |
| /proc/ide | Directory containing information about IDE devices |
| /proc/interrupts | Information about interrupt request (IRQ) numbers and how they are used |
| /proc/ioports | Information about input/output (I/O) port addresses and how they are used |
| /proc/kcore | Image of the physical memory |
| /proc/kmsg | Kernel messages |
| /proc/ksyms | Kernel symbol table |
| /proc/loadavg | Load average (average number of processes waiting to run in the last 1, 5, and 15 minutes) |
| /proc/locks | Current kernel locks (used to ensure that multiple processes do not write to a file at the same time) |
| /proc/meminfo | Information about physical memory and swap space usage |
| /proc/misc | Miscellaneous information |
