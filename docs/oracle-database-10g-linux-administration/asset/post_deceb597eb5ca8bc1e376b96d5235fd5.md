
RAID0 is the most straightforward RAID level to calculate performance characteristics. Assuming access to the RAID0 volume is random, and assuming 175 IOPS per disk drive, the optimal number of IOPS to the volume is calculated using the following formula: `(# of reads) + (# of writes) = (175 * n)`, where *n* is the number of disk drives in the array. Thus, a ten-disk drive array could handle 1750 reads and writes per second.

```
    (# of reads) + (# of writes) = (175 * n)
```

RAID1 and RAID10 volumes incur the write penalty of two physical writes for each write to the logical volume. This is due to the fact that all of the data on a disk drive must be duplicated on its mirror. Thus, the optimal number of reads and writes on a RAID10 and RAID1 volume is calculated using the following formula: `(# of reads) + (# of writes * 2) = (175 * n)`, where *n* is the number of disk drives in the array. For a RAID1 array, *n* = 2.

```
    (# of reads) + (# of writes * 2) = (175 * n)
```

RAID5 volumes incur a penalty of four physical I/Os for every logical write. The old data and parity must be read, two XOR operations performed, and the new data and parity written. The optimal number of reads and writes on a RAID5 volume can be calculated using the following formula: `(# of reads) + (# of writes * 4) = (175 * n)`, where *n* is the number of disk drives in the array.

```
    (# of reads) + (# of writes * 4) = (175 * n)
```

### RAID Level Performance Comparison

Let's compare the different RAID levels.

- RAID0 is the highest performing RAID level, since there is no fault-tolerance overhead. However, the fact that there is no fault tolerance renders RAID0 unacceptable for most database operations.
- RAID1 and RAID10 incur a 2x penalty on writes. They have the best level of fault tolerance, but are also the most expensive.
- RAID5 has the worst write penalty, incurring four physical I/Os for each write operation. RAID5 provides fault-tolerance, but can only tolerate the loss of one disk drive in the volume. However, it is the most economical of the RAID levels.

None of the above mentioned RAID levels incur any penalty for reads.

### RAID Performance

As you have seen from this section, there are different performance characteristics for different RAID levels. RAID5 is very popular because of the economics involved, since you only lose one disk drive's worth of space while achieving some level of fault-tolerance. However, in most cases, RAID5 is not appropriate for use with Oracle.

My rule of thumb is not to use RAID5 unless the read/write ratio is 90/10. In other words, unless 90 percent of the I/O operations are reads, RAID5 is inappropriate. Of course, your mileage may vary, and if the I/O rate is sufficiently low, then this shouldn't be an issue.

When calculating how many IOPS per disk drive are being done at the physical level, remember to multiply the RAID5 writes by four. This can drastically change your resulting data. For fault-tolerance and performance, I prefer RAID10.

As you can see, there are several factors to consider when selecting a RAID level. In the next chapter, you will see how Oracle I/O considerations should also be taken into account when selecting a RAID level.

No matter what your hardware vendor tells you, I/O sizing is a big issue. Though state-of-the-art I/O subsystems have many features, such as large caches and multiple buses, it doesn't change the fact that if you don't have enough disk drives, your performance will suffer.

One of the commonest performance problems encountered is a lack of sufficient I/O capacity. As disk drives become larger and less expensive, there is a tendency to replace several smaller disk drives with one larger one. While this is a good value, your performance might suffer. Be sure to do proper I/O sizing before ordering your new I/O subsystem.

## Capacity Planning

Capacity Planning refers to a complex, ongoing performance study of hardware and software resource consumption on an existing system in order to prepare for the growth of the system's workload. These studies are prepared primarily to maintain the service-level agreement (SLA) as system resource usage increases. In other words, capacity planning is the art of sizing an already existing system in order to determine when you might run out of capacity.

In addition to projecting resource utilization, capacity planning allows you to project what-if scenarios on workloads. In a typical capacity planning study, the technician performing the task will have historic performance data stored in the database and will be able to project trends in the following areas:

- Normal growth of CPU utilization
- Disk usage
- Memory usage

The technician will also be able to project sudden rises in CPU, disk, and memory utilization caused by the addition of new users to the system.

These studies can be extremely detailed and can involve profiling the activities of specific users. This is valuable information because not only can you add hypothetical generic users to the system for resource projection purposes, but you can add specific users as well, such as General Ledger users, Accounts Payable users, and so on.

By performing capacity planning studies, IT management can have sufficient time to plan the addition of new hardware in order to maintain the service-level agreements currently in place. In some cases, tuning ideas can come out of capacity planning studies as well.

## Summary

This chapter has covered the basics of sizing and capacity planning, and has touched on many of the main areas of these fields. Sizing and capacity planning is a difficult science, as you can see from the various discussions in this chapter.

Sizing is very important, since incorrect sizing early in your hardware acquisition can result in a poorly configured system, and thus bad performance later on down the road. It is much more economical to properly size a system than it is to fix a poorly performing system already in use.

![](img/9479df2d00f5e62b87366b125224950f_154_0.png)

## CHAPTER 5

## Configuring the Linux System for Oracle

![](img/9479df2d00f5e62b87366b125224950f_155_0.png)

In order to run Oracle on Linux, it is first necessary to install and configure Linux in such a way that Oracle has sufficient resources. These resources might consist of things like sufficient memory, sufficient disk space, proper tuning, and so on. Once this has been completed, the Oracle installation can commence. After Oracle is installed, there are some specific choices you can make regarding your Oracle configuration in order to optimize performance on Linux.

In this chapter, both the Linux configuration for Oracle, and the Oracle configuration for Linux will be covered. As with many of the operating systems that Oracle supports, there are some Linux specifics you should be aware of. At the end of this chapter, you will be prepared to properly install and configure Linux and Oracle on Linux.

## Preinstallation Procedures for Linux

Several steps are required to properly configure your Linux system for Oracle. Some of these steps involve configuring the Linux kernel parameters correctly, while some involve setting up hardware devices correctly. Others determine storage setup, as well as how to size the system properly. In this section, all of these steps will be covered.

Only a few parts of the Linux configuration have to be carefully thought out before installing the operating system. The most important of these is the configuration of the Linux filesystems. Once this decision has been made and the operating system has formatted both the partitions and filesystems, it is impossible to change. In fact, in order to redo the basic Linux partitions, the OS must be reinstalled. Since this is quite unlikely in a production environment, typically you will have to live with your initial choices for quite a long time.

Other important components must be configured as part of the OS installation, but things like the Linux tunable parameters, networking, and other configuration parameters can always be changed later without having to reinstall the operating system.

In addition to the initial filesystem configuration, it is also important to choose the right Linux components. When prompted to install groups of packages for things like OS or software development, these should be chosen. During the initial installation it is easy to install groups of packages, whereas later it is more difficult, since the individual packages must be picked.

Before beginning the Linux installation (and subsequently the Oracle installation), you must verify that you have met certain minimum requirements. These requirements are necessary for the proper installation and configuration of the Oracle Database Server and must be taken into account when installing and configuring the Linux operating system.

### Minimum Requirements

The following minimum requirements must be met for the successful installation and configuration of the Oracle Database Server. If you cannot meet these requirements, your system should be reinstalled or your hardware upgraded so you can.
