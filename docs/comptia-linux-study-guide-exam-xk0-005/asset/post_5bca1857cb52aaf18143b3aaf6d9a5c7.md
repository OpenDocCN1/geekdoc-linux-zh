
![](img/c0a399aca0d18f8822d714ad0a173123_654_0.png)

If you find that the iostat utility is not installed on your system, install the sysstat package to obtain it. Package installation was covered in Chapter 13.

The syntax for the iostat command is as follows:

```
iostat  [OPTION]  [INTERVAL]  [COUNT]
```

If you simply enter iostat at the command line and press Enter, you’ll see a static summary of CPU, filesystem, and partition statistics since the system booted. However, in troubleshooting situations, this is not worthwhile. There are a few useful iostat options to use for troubleshooting:

- -y: Do not include the initial “since system booted” statistics.
- -N: Display registered device mapper names for logical volumes.
- -z: Do not show devices experiencing no activity.
- -p device: Only show information regarding this device.

The iostat command’s two arguments allow viewing of the statistics over time. The [INTERVAL] argument specifies how many seconds between each display, and [COUNT] sets the number of times to display. Keep in mind that if you use the -y option, you will not see the first statistics until after the set interval.

An example using iostat with appropriate options for a troubleshooting situation is shown in snipped in Listing 20.14. In this case, only two statistics are shown 5 seconds apart. You can see that there is a rather high I/O wait (%iowait column) percentage, indicating a potential problem.

### **Listing 20.14:** Troubleshooting I/O wait using the iostat utility

```
$ iostat -ynz 5 2
[...]
avg-cpu:  %user   %nice  %system  %iowait  %steal  %idle
          26.80     0.00     42.27     30.93     0.00     0.00

Device:            tps     kB_read/s     kB_wrtn/s     kB_read     kB_wrtn
sda               409.90          3.30       9720.72         16       47145
[...]
avg-cpu:  %user   %nice  %system  %iowait  %steal  %idle
          22.67     0.00     65.79     11.54     0.00     0.00

Device:            tps     kB_read/s     kB_wrtn/s     kB_read     kB_wrtn
sda               535.83          0.00       9772.77          0       48277
[...]
```

![](img/c0a399aca0d18f8822d714ad0a173123_655_0.png)

To locate the application or process causing high I/O, employ the `iostat` utility. It is typically not installed by default but is available in the `sysstat` package.

For problems with high I/O, besides employing different disk technologies, you will want to review the Linux kernel's defined *I/O scheduling*. I/O scheduling is a series of kernel actions that handle I/O requests and their associated activities. How these various operations proceed is guided by selecting a particular I/O scheduler, shown in Table 20.7, within a configuration file.

### TABLE 20.7 I/O schedulers

| Name | Description |
| --- | --- |
| cfq | Creates queues for each process and handles the various queues in a loop while providing read request priority over write requests. This scheduler is good for situations where more balance I/O handling is needed and/or the system has a multiprocessor. |
| deadline | Batches disk I/O requests and attempts to handle each request by a specified time. This scheduler is good for situations where increased database I/O and overall reduced I/O latency are needed, and/or an SSD is employed, and/or a real-time application is in use. |
| noop | Places all I/O requests into a single FIFO queue and handles them in order. This scheduler is good for situations where less CPU usage is needed and/or an SSD is employed. |

The configuration file used for determining which I/O scheduler to use is in a directory associated with each disk. Listing 20.15 shows how to find the various disk directories and their associated scheduler file on a Rocky Linux distribution.

### Listing 20.15: Locating a disk's scheduler file

```bash
# ls /sys/block
dm-0 dm-1 sda sdb sdc sdd sr0
#
# cat /sys/block/sda/queue/scheduler
[mq-deadline] kyber bfq none
#
```

The scheduler used for the sda disk, mq-deadline, is in brackets. To change the current I/O scheduler, you simply employ super user privileges and the echo command, as shown in Listing 20.16.

![](img/c0a399aca0d18f8822d714ad0a173123_655_0.png)

### Listing 20.16: Changing a disk's scheduler file temporarily

```
# echo "bfq" > /sys/block/sda/queue/scheduler
# cat /sys/block/sda/queue/scheduler
mq-deadline kyber [bfq] none
#
```

If you determine that due to hardware limitations, a new and different hard drive is needed to handle the required I/O levels, the *ioping* utility can help you in the testing process. The *ioping* utility is typically not installed by default, but it is commonly available in a distribution's standard repositories.

> The *ioping* utility can destroy data on your disk! Be sure to thoroughly understand the command's options before employing it. If you desire a safer alternative, take a look at the *stress-ng* tool. This utility allows you to conduct stress tests for disks, your network, a system's CPUs, and so on.

Using the *ioping* command, you can test disk I/O latency, seek rates, and sequential speeds. You can also try out asynchronous, cache, and direct I/O rates. A snipped example in Listing 20.17 shows a simple test that reads random data chunks (noncached) from a temporary file using the *ioping* command.

### Listing 20.17: Conducting a noncached read test using the *ioping* utility

```
# ioping -c 3 /dev/sda
4 KiB <<< /dev/sda [...]: request=1 time=20.7 ms (warmup)
4 KiB <<< /dev/sda [...]: request=2 time=32.9 ms
4 KiB <<< /dev/sda [...]: request=3 time=25.5 ms
--- /dev/sda (block device 15 GiB) ioping statistics ---
2 requests completed in 58.4 ms, 8 KiB read, 34 iops, 137.0 KiB/s
generated 3 requests in 2.03 s, 12 KiB, 1 iops, 5.92 KiB/s
min/avg/max/mdev = 25.5 ms / 29.2 ms / 32.9 ms / 3.72 ms
#
```

The added *-c 3* option specifies three tests. More thorough *ioping* tests help determine if a disk will work for a particular application's needs.

## Measuring Disk Performance

One benchmark that's helpful in determining the overall I/O performance for disk drives is the input/output operations per second (IOPS) value. This value is the number of input or output operations a storage device can perform in a second. The IOPS values provide a way to not only evaluate disk drive performance but compare different types of storage, such as a single SATA or SSD drive versus a RAID or LVM setup.

A popular tool in the Linux environment for determining IOPS values is the flexible I/O tool called fio. The tool is available as the fio package in both the Debian-based and Red Hat-based software repositories, and it must be installed manually.

The fio tool performs multiple read/write operations on a file and directory you specify, with a file size and block size that you specify. The larger the file, the more accurate the IOPS reading you'll obtain. Listing 20.18 shows an example of performing an fio test on a disk.

### **Listing 20.18:** Using the fio tool to determine disk I/O

```
# fio --randrepeat=1 --ioengine=libaio --direct=1
   --gtod_reduce=1 --name=fiotest --filename=fiotest --bs=4k
   --iodepth=64 --size=1G --readwrite=randrw --rwmxread=75

fiotest: (g=0): rw=randrw, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.19
Starting 1 process
fiotest: Laying out IO file (1 file / 1024MiB)
[...]
    read: IOPS=23.4k, BW=91.4MiB/s (95.9MB/s) (768MiB/8396msec)
      bw ( KiB/s): min=63425, max=101451, per=99.97%, avg=93588.81,
      stdev=9628.66, samples=16
    iops : min=15856, max=25362, avg=23396.88, stdev=2407.19, samples=16
   write: IOPS=7818, BW=30.5MiB/s (32.0MB/s) (256MiB/8396msec); 0 zone resets
      bw ( KiB/s): min=22658, max=33712, per=99.91%, avg=31245.31,
      stdev=2927.74, samples=16
    iops : min= 5664, max= 8428, avg=7811.06, stdev=732.05, samples=16
    cpu    : usr=2.80%, sys=34.02%, ctx=3045, majf=0, minf=7
    IO depths    : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
               submit: 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
               complete: 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
    issued rwt: total=196498,65646,0,0 short=0,0,0,0 dropped=0,0,0,0
    latency   : target=0, window=0, percentile=100.00%, depth=64
[...]
#
```
