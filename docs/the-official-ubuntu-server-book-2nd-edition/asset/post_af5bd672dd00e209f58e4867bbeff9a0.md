
## CHAPTER 10
## Fault Tolerance

![](img/304f637afcecc491b152ee8ac5afadee_389_0.png)

### Test your redundancy.

As with backups, if you haven’t tested your fault tolerance, then you don’t have fault tolerance. If possible, before you deploy a new redundant system such as Ethernet bonding or server clustering, be sure to simulate failures and understand both how the system responds to a failure as well as how it responds once the fault has been repaired. Systems can behave very differently in both how they handle a fault and how they resume after the fault is repaired, all based on how you configure them. This testing phase is also a good time to test any monitoring you have put in place to detect these failures.

### Eliminate any single points of failure.

While having some redundancy is better than having none, try to go through the entire server stack and identify and eliminate any single points of failure. For instance, if you have set up redundant power sources for your data center and each server has a power supply hooked into one of the power sources, it is less useful if the servers are connected to one switch with a single power supply. For larger operations, even a data center itself is seen as a single point of failure, so in those cases servers are distributed across multiple data centers in entirely different geographical locations.

### Respond to failures quickly.

When a component fails, try to identify and repair the problem as soon as you can. In RAID, for instance, many sysadmins set up a disk as a hot spare so that the moment a disk fails, a replacement can take its place. Provided the hot spare syncs before another drive fails, the data will still be intact. While you can’t do this with every component, when you do have a fault, try to repair it before you lose the fail-over side as well.

## RAID

The piece of server hardware most likely to fail is your hard drive, so if you want a fault-tolerant system, hard drive redundancy should be your first priority. This is generally accomplished using RAID. RAID stands for Redundant Array of Inexpensive Disks, although some people say it stands

for Redundant Array of Independent Disks (those people must have priced out fiber channel drives).

RAID is generally referred to as either hardware or software RAID. With hardware RAID, your server has a component either built into the motherboard or available as an add-on card to which your hard drives connect. This hardware supports various RAID levels and typically has its own processor and memory to perform any calculations (such as parity calculations on RAID 5). The card then presents the storage as a single device (sometimes as a generic SCSI drive and other times as a different block device, depending on the vendor) that you can partition, format, and use. Any configuration, recovery, or monitoring typically requires special software on the host or work within the BIOS.

With software RAID, the operating system implements the RAID algorithms using the regular CPU with a driver or module. On Linux you can see both the original drives and partitions as well as a special device that represents the RAID storage. The advantage of Linux software RAID is that it doesn’t require any special vendor support under Linux, and it actually performs surprisingly well, is surprisingly stable, and is free. Also, unless you invest in high-end RAID cards, Linux software RAID provides more flexibility in how you can expand a RAID. For the rest of the chapter I focus on Linux software RAID, and I will discuss how you can migrate a system from a single drive to RAID and from RAID 1 to RAID 5, as well as how to add a drive to a RAID 5 array.

> **NOTE** There’s a third type of RAID that falls somewhere between hardware and software RAID. It can be found in cheap RAID cards that these days are even built into many desktop motherboards. Although there is hardware involved, the RAID itself is implemented via a driver that runs on the host, so it uses the host CPU. In addition, this hybrid RAID requires a vendor-specific driver so the OS can see the RAID drive.

## RAID Levels

There are a number of different ways to implement RAID. Each has advantages and disadvantages, depending on what you want to accomplish. Next I cover the Linux software RAID types you are most likely to use.
