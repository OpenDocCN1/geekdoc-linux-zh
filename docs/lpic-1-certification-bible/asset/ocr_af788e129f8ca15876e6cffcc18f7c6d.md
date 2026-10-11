```
"""
First DMA channel 1.
8 bit DMA only
Logical device is a bus master
DMA may execute in count by byte mode
DMA may not execute in count by word mode
DMA channel speed in compatible mode
(DMA 0 (CHANNEL 1))
# Next DMA channel 5.
16 bit DMA only
Logical device is a bus master
DMA may execute in count by byte mode
DMA may execute in count by word mode
DMA channel speed in compatible mode
Logical device decodes 16 bit I/O address lines
Minimum I/O base address 0x0220
Maximum I/O base address 0x0220
I/O base alignment 1 bytes
Number of I/O addresses required: 16
(IO 0 (SIZE 16) (BASE 0x0220))
(NAME "CTL0028/1530224[0][Audio]" )
(ACT Y)
"""
```

You must also be sure to uncomment the final (ACT Y) line so that the card is activated. For each device detected by pnpdump you need to manually set the configuration options. Once you are satisfied with your settings, you should run the isapnp command or reboot the system. Once isapnp has been run, you can load the driver for the configured hardware.

![](bbox=[0.11, 0.6, 0.21, 0.64])

Hardware drivers and modules are covered in more detail in Chapter 13.

# Partitioning Schemes

![](bbox=[0.11, 0.71, 0.21, 0.73])

# 2.2 Linux Installation and Package Management

+   - **Design hard-disk layout.** Design a partitioning scheme for a Linux system, depending on the hardware and system use (number of disks, partition sizes, mount points, kernel location on disk, swap space).

Unlike most other operating system installs you may be familiar with, Linux installs are not always to one large partition. *Partitions* are used to section up disk space in to smaller logical blocks. In the UNIX world, partitions are sometimes known as volumes. Splitting up the drive(s) into multiple partitions gives you flexibility, stability, and easier maintenance.

When building a server, you most likely want to put the following directories, the standard directories that all Linux systems will have, on separate volumes.

![](bbox=[0.11, 0.92, 0.21, 0.96])

You can find most of these directories covered in more detail in Chapter 6.