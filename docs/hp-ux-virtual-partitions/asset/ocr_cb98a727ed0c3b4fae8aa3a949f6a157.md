![](bbox=[0.14, 0.1, 0.88, 0.67])

Figure 2-1 Virtual Partitions Software Stack

There are many components in Figure 2-1. We already have many of the components in this diagram on our system. Starting from the bottom we have the hardware, firmware, Virtual Partition Monitor (covered as part of the boot process in Chapter 3), and HP-UX 11i installed on two different disks. There are two HP-UX 11i instances shown in the leftmost two stacks of Figure 2-1. These are the operating systems we already have loaded.

The two HP-UX 11i instances can't run simultaneously on our L-Class system because we have not yet created our Virtual Partitions. Without Virtual Partitions created, we can boot HP-UX off of one or the other of these