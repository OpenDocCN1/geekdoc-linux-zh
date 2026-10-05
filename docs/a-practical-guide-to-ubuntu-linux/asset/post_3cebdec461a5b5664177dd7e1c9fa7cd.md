
# GRAPHICAL PARTITION EDITORS 71

![](img/45ff4cd21497435daa35084a84b95d07_121_0.png)

**Figure 3-17** The Prepare disk space screen showing a handle with a Windows partition occupying the entire disk

(page 76) on a system where a single Windows partition occupies the whole disk. This section describes how to use the ubiquity partition editor to resize a partition. See “Resizing a Partition” on page 65 for instructions on using parted to resize a partition.

This choice includes a slider with a handle that allows you to specify how you want to resize the partition. See Figure 3-17. Click and drag the handle to specify the new size of the partition you are resizing and, by default, the size of the new partition where Ubuntu will be installed.

- **Erase and use the entire disk**—Deletes all information on the disk and installs Ubuntu on the entire disk. After deleting information from the disk, this choice uses guided partitioning as explained on page 60.
- **Using the whole disk for Ubuntu is easy.** Before you start, make sure the disk does not contain any information you need. Once you rewrite the partition table, the data will be gone for good. If you are not sure about the contents of the disk, use *palimpsest* (page 66) to take a look.
- **Use the largest continuous free space**—Installs Ubuntu in the largest chunk of free space on the disk. Because free space holds no data, this technique does not change any data on the disk. This choice uses guided partitioning (as explained on page 60) on the free space. If an operating system occupies the existing partition, this choice sets up a dual-boot system (page 76).

## 3 STEP-BY-STEP INSTALLATION

![](img/45ff4cd21497435daa35084a84b95d07_122_0.png)

**Figure 3-18** An empty hard disk with a partition table

- **Specify partitions manually (advanced)**—Gives you total control over the size, placement, and naming of partitions where Ubuntu is installed.

When you are working with the Prepare disk space screen, click **Forward**.

## MANUAL PARTITIONING

This section explains how to use the ubiquity partition editor to create a partition on an empty hard disk. Figure 3-7 on page 61 shows the Prepare disk space screen for an empty hard disk. To create partitions manually, select **Specify the Partitions Manually (advanced)** and click *Forward*. The ubiquity partition editor displays a Prepare partitions screen that shows a device without any partitions—only free space. Before you create partitions, you must set up a new partition table. To do so, highlight the device name (e.g., */dev/sda*) and click **New partition table**. The partition editor confirms that you want to create a new, empty partition table. Click *Continue* to create a partition table that contains only free space. Now ubiquity displays a screen that looks similar to the one in Figure 3-18. (Note: 214,748 MiB [mebibytes; page 1159] equals 200 GB [gigabytes; page 1150] Figure 3-18 should show MiB in place of MB.) The hard disk at */dev/sda* has a partition table without any partitions; it contains only free space.

To create a partition, highlight the line containing **free space** in the Device column and click **Add**. The ubiquity partition editor displays a Create partition window (Figure 3-19), which asks you to specify whether you want to create a primary or logical partition (page 34), what size the partition should be (in megabytes), whether the partition should appear at the beginning or end of the free space, what

# GRAPHICAL PARTITION EDITORS 73

![](img/45ff4cd21497435daa35084a84b95d07_123_0.png)

type the partition should be (Use as), and what name the mount point (page 35) for the partition it should have. Because Linux does not mount a swap partition, you can specify a mount point for a type swap partition. If you are unsure of which type a partition should be, choose ext4 (page 505). Click OK.

After a few moments the Prepare partitions screen displays the new partition (Figure 3-20). To create another partition, highlight the line containing free space and repeat the preceding steps. Remember to create a swap partition (page 37). When you have finished creating partitions, click Forward.

The Prepare partitions screen displays five buttons immediately below the frame that lists the disks and partitions. Some of these buttons are grayed out (inactive)

![](img/45ff4cd21497435daa35084a84b95d07_123_1.png)

Figure 3-20 The Prepare partitions screen displaying a new partition

depending on what is highlighted in the frame above. The button labeled Revert is always active. When a device is highlighted, the button New Partition Table is active. Clicking this button creates a new partition, thereby destroying any existing partition table. Highlighting a partition gives you the choice of editing or deleting the partition. Editing a partition you created allows you to change only its type and mount point. You must delete and re-create.

## UPGRADING TO A NEW RELEASE

Upgrading a system is the process of installing a new release over an older one. All configuration files are preserved, but software is brought up to date.

## Upgrading from LTS

When you start the upgrade, the system checks if a new release is available. If so, it offers to upgrade the system.

## Watch for configuration files

During the installation phase, the system may ask how you want to handle configuration files. If you have made changes to these files, you can choose to keep your version or replace it with the new version provided by the release.
