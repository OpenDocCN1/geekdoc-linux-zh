# 254 Part III ♦ Choosing and Installing a Linux Distribution

If you have used only Windows systems before, you probably never thought about partitions. whole hard disk assigned to C: With many Linux systems, you have the opportunity to view and change the default partitioning based on how you want to use the system.

During installation, systems as SUSE and Fedora let you your hard disk using graphical partitioning tools (Yast and Disk Druid, respectively). The following sections describe how to use Disk Druid (during installation) or fdisk. The section "Tips for Creating Partitions" for some ideas for creating disk partitions.

# Partitioning with Disk Druid Installation

During installation, Fedora gives you the opportunity to change how your hard disk is partitioned using a tool called Disk Druid. The Disk Druid screen is divided into two sections. The top shows general information about each hard disk. The bottom shows details of each partition. Figure 7-1 shows an example of the Disk Druid window.

![](bbox=[0.176, 0.413, 0.823, 0.725])

Figure 7-1: Partition your disk during Fedora installation from the Disk Setup window.

For each of the hard partitions, you can see:

+   * Device — The device name is what representing the hard partition in the /dev directory. Each partition device begins with two letters: hd for IDE disks, sd for SCSI disks, or rd for XD disks. After that is a single letter representing the number of the disk (disk 1 is a, disk 2 is b, disk 3