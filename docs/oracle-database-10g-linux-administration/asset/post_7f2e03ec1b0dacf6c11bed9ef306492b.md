
![](img/9479df2d00f5e62b87366b125224950f_142_0.png)

FIGURE 4-8. I/O queueing

In order to achieve this, we would optimally want to run the disk drives at the point on the chart known as the “knee of the curve”. This is the point where the slope of the curve starts to move sharply upwards and occurs at about 80 percent of capacity. Thus, random I/Os should optimally not exceed 126 I/Os per second in this example.

## Additional Considerations

In the previous two sections, you have seen that theoretically a disk drive can access data at the following rates:

- Sequential I/Os: 384 IOPS
- Random I/Os: 158 IOPS

In addition to the latencies incurred by the disk drive itself, other latencies can be incurred by the I/O controller and the operating system device driver. This additional latency can be small or large depending on how busy the device is. Since this additional latency is dependent on specifics of the I/O subsystem, it will not be covered here; however, you should be aware of it.

## RAID Disk Subsystems

There are several different types of I/O subsystems you can use with your computer systems. For database servers, RAID systems are probably the most popular. RAID systems come in a variety of different types and configurations, as you will see in this section.

The acronym RAID stands for Redundant Array of Inexpensive Disks. RAID I/O subsystems serve two main purposes. The first is to provide a fault-tolerant I/O subsystem. A fault-tolerant I/O subsystem is one that can survive the failure of a component in the system (usually a disk drive) without incurring any loss of data. The second purpose of a RAID subsystem is to allow multiple individual disk drives to be configured into a larger virtual disk drive. This is done for both the ease of administration and performance reasons.

The RAID subsystem can combine two or more disk drives into one larger logical disk drive by using disk striping. Disk striping takes the logical disk layout, and using different algorithms, places that data on two or more disk drives. Disk striping does not make a logical disk drive fault-tolerant, but it can improve disk access times by spreading I/Os among multiple disks. In addition, disk striping can be combined with fault-tolerant features of the controller.

Most RAID controllers offer a number of different options for configuring logical disk volumes using different striping options and different fault-tolerant RAID types. The different RAID configurations are commonly known as RAID levels and define how the data is striped across the different disks in the I/O subsystem. These different RAID levels offer different levels of fault-tolerance, different performance characteristics, and different costs. Some RAID levels involve disk striping and some RAID levels do not.

### Hardware vs. Software RAID

A RAID I/O subsystem can be formed either by purchasing a hardware RAID subsystem or by using software RAID. Both of these options have advantages and disadvantages.

The hardware RAID subsystem will have greater performance since other processes running on the system CPU will not affect it. In addition, hardware RAID subsystems can support features that software RAID subsystems may not be able to, such as hot-swappable disk drives and prefailure alerting. However, a hardware RAID subsystem can only be configured to stripe the drives that are attached to that controller, so the number of drives in a logical disk volume is limited to the number of drives that the controller can support. In addition, a hardware RAID subsystem can have a battery backed-up cache, whereas a software RAID system can’t.

Software RAID subsystems have a price advantage, since it is not necessary to purchase additional hardware. In addition, a software RAID subsystem can be configured to stripe across all of the disk drives in the system and is not limited by controllers. Thus, you can create a software RAID volume across disk drives that are attached to many I/O controllers.

It is also possible to use software striping to stripe hardware disk volumes that are logical RAID volumes on a hardware RAID controller. Thus, the two can be combined in order to create massive logical disk volumes. This is something I do not recommend due to the overhead involved in software RAID.

For the purposes of this book, since it is performance and stability focused, we will assume a hardware RAID device.

### Striping

Striping involves spreading data across multiple disk drives in order to create a logical disk drive that is larger than any individual disk drive in the system. Disk striping involves dividing the logical disk drive into pieces referred to as either stripes or chunks. Typically, these stripes are distributed to the individual disk drives in a round-robin fashion, as shown in Figure 4-9.

As mentioned previously, to the OS and to the users, the logical RAID volume appears as one large disk drive. If you are using a hardware RAID controller, the OS does not even know the difference. Striping is used in several of the different RAID levels supported by most RAID subsystems. In this section, we will examine the different RAID levels and how they operate.

### RAID0

RAID0 is disk striping with no fault-tolerance. Thus, RAID0 is not redundant. With a RAID0 configuration, you can stripe data across multiple disk drives in order to create a large logical disk volume. However, a failure of any of the disk drives in the volume will result in the loss of the entire logical volume.

RAID0 is disk striping only and typically works in a round robin fashion. RAID0 is the most economical of the RAID levels and provides the highest performance, as you’ll discover later in this section. You will see that, as in most things, there are tradeoffs. For instance, RAID0 provides high performance and value at the expense of no fault-tolerance.

![](img/9479df2d00f5e62b87366b125224950f_144_0.png)

### RAID1

RAID1 is also known as *disk mirroring*. In RAID1, all the data stored on a disk drive is duplicated on another disk in the array, as shown in Figure 4-10. Each time a write occurs to the logical disk, the data must be written to *both* physical disks before the logical write is considered completed. With disk mirroring, a single disk is mirrored to another disk; these disks can also be striped with other disks to form a larger logical volume. This combination of disk striping and mirroring is known as RAID10, RAID1+0, RAID0+1, or RAID 1/0 (depending on the manufacturer).

Because this mirroring is on a one-to-one basis, half of the disk drives in the system could actually fail (depending on which disks they are), and the system can still be operational. With most disk array controllers, you can split the mirror across SCSI buses. This arrangement allows for the failure of an entire SCSI bus (for example, a cabinet failure) without affecting operations.

With disk mirroring, you can use only half the disks in the system (the other half are used for the mirrors). In other words, if you use disk mirroring with two 18GB disk drives, you can use only 18GB of space. When writing, you get the benefit of only one disk in terms of performance because a logical write invokes two physical writes. You may see a benefit from reading from a mirrored drive. Some disk array controllers support split seeks, in which reads can occur simultaneously on different mirrored drives to different data. The disk with the heads closest to the requested data retrieves the data. Depending on the data access methods, this feature may or may not provide any benefits.

If you can afford the cost of disk mirroring, RAID1 is the best choice when fault tolerance is required. With disk mirroring, you achieve the highest level of protection as well as the fastest disk access possible for a fault-tolerant volume.

### RAID10

RAID10 is a combination of RAID0 and RAID1. With a RAID10 volume, each disk drive has its contents mirrored onto another disk drive and at the same time these mirrored disks participate as part of a stripe set, as shown in Figure 4-11.

![](img/9479df2d00f5e62b87366b125224950f_145_0.png)

FIGURE 4-10. A RAID1 configuration
