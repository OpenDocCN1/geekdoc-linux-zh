# Chapter 10: Understanding System Administration 445

![](bbox=[0.287, 0.098, 0.681, 0.335])

Figure 10-4: Join multiple RAID partitions to form a single RAID device.

+   6. You need to select the following information about your RAID device and click OK:
  - **Mount Point** — The point in the file system associated with the RAID device. You might be creating the RAID device for a part of the file system for which you expect to be a lot of hits on the hard disk (such as the /var partition).
  - **File System Type** — For a regular Linux partition, choose ext3. You can also select LVM, swap, or VFAT as the file system type.
  - **RAID Device** — The first RAID device is typically md0 (for /dev/md0).
  - **RAID Level** — Allowable RAID levels are RAID0, RAID1, and RAID5. RAID0 is for stripping dividing the device into stripes across RAID partitions you have selected. RAID1 is for mirroring so that the data is duplicated across all RAID partitions. RAID5 is for parity, so there is always one backup disk if a disk goes bad. You need at least three RAID partitions to use RAID5.
  - **RAID Members** — From the partitions you created, select which ones are going to be members of the RAID device you are creating.
  - **Number of spares** — Select how many spares are available to the RAID device.

The new RAID device should appear on the Disk Setup window. Click Next to continue with installation.

Once installation is complete, you can check your RAID devices by a variety of tools that come with Fedora or RHEL. Commands for working with RAID partitions can come in the dmraid package. Using dmraid commands, you can list and reconfigure your RAID partitions.