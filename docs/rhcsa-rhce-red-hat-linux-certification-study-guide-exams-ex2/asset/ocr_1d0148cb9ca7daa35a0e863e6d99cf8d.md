In any case, the RAID configured on RHEL 6 is software RAID. The acronym, Redundant Array of Independent Disks, is somewhat misleading, as software RAID is usually based on independent partitions. Redundancy comes from the use of partitions from different physical hard drives.

# Partition Creation Exercises

Now return to the installation process. If you followed the steps described so far in this chapter and the system has sufficient RAM, you should see the Disk Druid Please Select A Device screen shown in Figure 1-8.

At this screen, you have the opportunity to configure partitions, logical volumes, and RAID arrays.

+   I. Configure standard partitions as described earlier, in Table 1-1. Larger partitions are acceptable if you have the space. They would be necessary if you're creating the physical host system that will contain the VMs. The Create button supports the creation of standard partitions, logical volumes, and RAID arrays, as shown in Figure 1-9. Select Standard Partition and click Create to continue.

FIGURE 1-9

You can create a variety of storage devices..

![](bbox=[0.42, 0.6, 0.78, 0.88])