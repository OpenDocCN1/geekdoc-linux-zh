
the -t option to determine the rate at which data is read from the disk into a buffer in memory. Here's the result of typing /sbin/hdparm -t /dev/hda on one system:

```
/dev/hda:
Timing buffered disk reads: 178 MB in 3.03 seconds = 58.81 MB/sec
```

The command requires the IDE drive’s device name (/dev/hda for the first hard drive and /dev/hdb for the second hard drive) as an argument. If you have an IDE hard drive, you can try this command to see how fast data is read from your system’s disk drive.

To display the space available in the currently mounted file systems, use the df command. If you want a more readable output from df, type the following command:

```
df -h
```

Here’s typical output from this command:

```
Filesystem Size Used Avail Use% Mounted on
/dev/hda5 7.1G 3.9G 2.9G 59% /
/dev/hda3 99M 18M 77M 19% /boot
none 125M 0 125M 0% /dev/shm
/dev/scd0 2.6G 0 100% /media/cdrecorder
```

As this example shows, the -h option causes the df command to display the sizes in gigabytes (G) and megabytes (M).

To check the disk space being used by a specific directory, use the du command. You can specify the -h option to view the output in kilobytes (K) and megabytes (M), as shown in the following example:

```
du -h /var/log
```

Here’s typical output from that command:

```
152K /var/log/cups
4.0K /var/log/vbox
4.0K /var/log/httpd
508K /var/log/gdm
4.0K /var/log/samba
8.0K /var/log/mail
4.0K /var/log/news/OLD
8.0K /var/log/news
4.0K /var/log/squid
2.2M /var/log
```

The du command displays the disk space used by each directory, and the last line shows the total disk space used by that directory. If you want to see only the total space used by a directory, use the -s option. Type du -sh /home to see the space used by the /home directory, for example. The command produces output that looks like this:

```
89M  /home
```

## Viewing System Information with the /proc File System

Your Linux system has a special /proc file system. You can find out many things about your system from this file system. In fact, you can even change kernel parameters through the /proc file system (just by writing to a file in that file system), thereby modifying the system’s behavior.

The /proc file system isn’t a real directory on the hard drive but a collection of data structures in memory, managed by the Linux kernel, that appears to you as a set of directories and files. The purpose of /proc (also called the process file system) is to give you access to information about the Linux kernel, as well as help you find out about all processes currently running on your system.

You can access the /proc file system just as you access any other directory, but you have to know the meaning of various files to interpret the information. Typically, you use the cat or more command to view the contents of a file in /proc. The file’s contents provide information about some aspect of the system.

As with any directory, start by looking at a detailed directory listing of /proc. To do so, log in as root and type ls -l /proc in a terminal window. In the output, the first set of directories (indicated by the letter d at the beginning of the line) represents the processes currently running on your system. Each directory that corresponds to a process has the process ID (a number) as its name.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_318_0.png)

Notice also a very large file named /proc/kcore; that file represents the entire physical memory of your system. Although /proc/kcore appears in the listing as a huge file, no single physical file occupies that much space on your hard drive, so don’t try to remove the file to reclaim disk space.

Several files and directories in /proc contain interesting information about your Linux PC. The /proc/cpuinfo file, for example, lists the key characteristics of
your system, such as processor type and floating-point processor information. You can view the processor information by typing cat /proc/cpuinfo. Here's what appears when cat /proc/cpuinfo is run on a sample system:

```
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 42
model name : Intel(R) Core(TM)i5-2410M CPU 2.30GHz
stepping : 7
cpu MHz : 2294.764
cache size : 3072 KB
physical id : 0
siblings : 4
core id : 0
cpu cores : 2
apicid : 0
initial apicid : 0
fpu : yes
fpu_exception : yes
cpuid level : 13
wp : yes
flags : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca
    cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe
    pni monitor ds_cpl cid
bogomips : 4589.52
```

This output is from an Intel Core i5-2410M system (2.30 GHz x 4). The listing shows many interesting characteristics of the processor. The last line in the /proc/cpuinfo file shows the BogoMIPS for the processor, as computed by the Linux kernel when it boots. (BogoMIPS is something that Linux uses internally to time-delay loops.)

Table 1-6 summarizes some of the files in the /proc file system that provide information about your Linux system. You can view some of these files on your system to see what they contain but note that not all files shown in Table 1-6 are present on your system. The specific contents of the /proc file system depend on the kernel configuration and the driver modules that are loaded (which in turn depend on your PC's hardware configuration).

![](img/322157d1fa7d965f05bcd68ed0ffc36b_319_0.png)

You can navigate the /proc file system just as you'd work with any other directories and files in Linux. Use the more or cat command to view the contents of a file.

## TABLE 1-6 Some Files and Directories in /proc

| File Name | Content |
|---|---|
| `/proc/acpi` | Information about Advanced Configuration and Power Interface (ACPI) — an industry-standard interface for configuration and power management on laptops, desktops, and servers. |
| `/proc/bus` | Directory with bus-specific information for each bus type, such as PCI. |
| `/proc/cmdline` | The command line used to start the Linux kernel (such as ro root=LABEL=/ rhgb). |
| `/proc/cpuinfo` | Information about the CPU (the microprocessor). |
| `/proc/devices` | Available block and character devices in your system. |
| `/proc/dma` | Information about DMA (direct memory access) channels that are used. |
| `/proc/driver/rtc` | Information about the PC's real-time clock (RTC). |
| `/proc/filesystems` | List of supported file systems. |
| `/proc/ide` | Directory containing information about IDE devices. |
| `/proc/interrupts` | Information about interrupt request (IRQ) numbers and how they're used. |
| `/proc/ioports` | Information about input/output (I/O) port addresses and how they're used. |
| `/proc/kcore` | Image of the physical memory. |
| `/proc/kmsg` | Kernel messages. |
| `/proc/loadavg` | Load average (average number of processes waiting to run in the past 1, 5, and 15 minutes). |
| `/proc/locks` | Current kernel locks (used to ensure that multiple processes don't write to a file at the same time). |
| `/proc/meminfo` | Information about physical memory and swap-space usage. |
| `/proc/misc` | Miscellaneous information. |
| `/proc/modules` | List of loaded driver modules. |
| `/proc/mounts` | List of mounted file systems. |
| `/proc/net` | Directory with many subdirectories that contain information about networking. |
| `/proc/partitions` | List of partitions known to the Linux kernel. |
| `/proc/pci` | Information about PCI devices found on the system. |
| `/proc/scsi` | Directory with information about SCSI devices found on the system (present only if you have a SCSI device). |
| `/proc/stat` | Overall statistics about the system. |
| `/proc/swaps` | Information about the swap space and how much is used. |
| `/proc/sys` | Directory with information about the system. You can change kernel parameters by writing to files in this directory. (Using this method to tune system performance requires expertise to do properly.) |
| `/proc/uptime` | Information about how long the system has been up. |
| `/proc/version` | Kernel version number. |

## Understanding Linux Devices

Linux treats all devices as files and uses a device just as it uses a file — opens it, writes data to it, reads data from it, and closes it when finished. This ability to treat every device as a file is possible because of *device drivers*, which are special programs that control a particular type of hardware. When the kernel writes data to the device, the device driver does whatever is appropriate for that device. When the kernel writes data to the DVD drive, for example, the DVD device driver puts that data on the physical medium of the DVD disk.

Thus, the device driver isolates the device-specific code from the rest of the kernel and makes a device look like a file. Any application can access a device by opening the file specific to that device.

### Device files

Applications can access a device as though it were a file. These files, called *device files*, appear in the `/dev` directory in the Linux file system.

If you use the `ls` command to look at the list of files in the `/dev` directory, you see several thousand files. These files don’t mean that your system has several thousand devices. The `/dev` directory has files for all possible types of devices, which is why the number of device files is so large.

How does the kernel know which device driver to use when an application opens a specific device file? The answer is in two numbers called the *major* and *minor device numbers*. Each device file is mapped to a specific device driver through these numbers.
