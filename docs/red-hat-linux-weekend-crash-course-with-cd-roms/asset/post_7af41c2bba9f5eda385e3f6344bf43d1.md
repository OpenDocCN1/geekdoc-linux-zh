
![](img/eef64cc01382a4448bc55a2ee7dcc4ca_44_0.png)

### Figure 2-1

Selecting a keyboard type during Red Hat Linux installation

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_44_1.png)

### Figure 2-2

Configuring your mouse during Red Hat Linux installation

If you select a mouse with a serial interface, you are asked to specify the serial port where the mouse is connected. For COM1, specify /dev/ttyS0 as the device; for COM2, the device name is /dev/ttyS1.

- 4. The installation program displays a welcome message that provides some helpful information, including a suggestion that you access the online manuals at http://www.redhat.com. Click the Next button to proceed to the next step.
- 5. The installation program displays a screen asking if you want to install a new system or upgrade an older Red Hat installation.

For a new installation, the installation program requires you to select the installation type — Workstation, Server, or Custom. The Workstation and Server installations simplify the installation process by partitioning the disk in a predefined manner. A Workstation-class installation deletes all currently existing Linux-related partitions. A Server-class installation deletes all existing disk partitions, including any existing Windows partitions. For maximum flexibility (so you can specify how the disk is used), select the Custom installation.

The next major phase of installation involves partitioning the hard disk for use in Red Hat Linux.

## Partitioning the Hard Disk for Red Hat Linux

Like MS-DOS, Red Hat Linux requires you to partition and prepare a hard disk before you can install Red Hat Linux. For a new PC, you usually do not perform this step. This is because the vendor normally takes care of preparing the hard disk and installing Windows and all other applications on the hard disk. Because you are installing Red Hat Linux from scratch, however, you have to perform this crucial step yourself. As you see in the following sections, this task is just a matter of following instructions.

The Red Hat Linux installation program runs Disk Druid — a utility program that enables you to partition the disk and, at the same time, specify which parts of the Linux file system you want to load on which partition.

Before you begin to use Disk Druid to partition your disk, you need to know how to refer to the disk drives and partitions in Linux. Also, you should understand the terms mount points and swap partition. In the next three sections, you learn these terms and concepts and then proceed to use Disk Druid.

## Naming disks and devices

The first step is to understand how Red Hat Linux refers to the various disks. Linux treats all devices as files and has actual files that represent each device. In Red Hat Linux, these device files are located in the /dev directory. If you are new to UNIX, you may not yet know about UNIX filenames. But you will learn more as you continue to use Red Hat Linux. If you know how MS-DOS filenames work, you will find that Linux filenames are similar. However, they have two exceptions: they do not use drive letters (such as A: and C:) and they substitute the slash (/) for the MS-DOS backslash (\) as the separator between directory names.

Because Linux treats a device as a file in the /dev directory, the hard disk names start with /dev. Table 2-1 lists the hard disk and floppy drive names that you may have to use.

Table 2-1
Hard Disk and Floppy Drive Names

| Name | Description |
|------|-------------|
| /dev/hda | First Integrated Drive Electronics (IDE) hard drive (the C: drive in DOS and Windows) |
| /dev/hdb |  |
| /dev/sda | First Small Computer System Interface (SCSI) drive |
| /dev/sdb | Second SCSI drive |
| /dev/fd0 | First floppy drive (the A: drive in DOS) |
| /dev/fd1 | Second floppy drive (the B: drive in DOS) |

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_46_0.png)

When Disk Druid displays the list of partitions, the partition names take the form hda1, hda2, and so on. Linux constructs each partition name by appending the partition number (1 through 4 for the four primary partitions on a hard disk) to the disk's name. Therefore, if your PC's single IDE hard drive has two partitions, notice that the installation program uses hda1 and hda2 as the names of these partitions.

## Mounting a file system on a device

In Red Hat Linux, you use a physical disk partition by associating it with a specific part of the file system. This is a hierarchical arrangement of directories — a directory tree. If you have more than one disk partition (you may have a second disk with a Linux partition), you can use all of them in Red Hat Linux under a single directory tree. All you have to do is decide which part of the Linux directory tree should be located on each partition — a process known in Linux as mounting a file system on a device. (The disk partition is a device.)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_47_0.png)

The term mount point refers to the directory you associate with a disk partition or any other device.

Suppose that you have two disks on your PC, and you have created Linux partitions on both disks. Figure 2-3 illustrates how you can mount different parts of the Linux directory tree (the file system) on these two partitions.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_47_1.png)

### Figure 2-3
An example of mounting the Red Hat Linux file system on two disk partitions

## Understanding swap partition

Most advanced operating systems support the concept of virtual memory, in which part of your system’s hard disk functions as an extension of the physical memory (RAM). When the operating system runs out of physical memory, it can move (or swap out) the contents of currently unneeded parts of RAM to make
room for a program that needs more memory. When the operating system needs to access anything in the swapped-out data, it has to find something else to swap out and then it swaps in the required data from disk. This process of swapping data back and forth between the RAM and the disk is also known as paging.

Because the disk is much slower than RAM, the system’s performance is slower when the operating system has to perform a lot of paging. However, virtual memory enables you to run programs that you otherwise can’t run.

Red Hat Linux supports virtual memory and can make use of a swap partition. When you create the Linux partitions, you should also create a swap partition. With the Disk Druid utility program, described in the next section, it is simple to create a swap partition. Simply mark a partition type as a swap device and Disk Druid performs the necessary tasks.

## Preparing disk partitions for Red Hat Linux

After you select Custom installation, a screen prompts you for the method you want to use to partition the disk — the choices are the Linux fdisk program or Disk Druid. You should select Disk Druid and click the Next button. You should then see the Disk Druid screen (as shown in Figure 2-4).

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_48_0.png)

### Figure 2-4
Disk Druid screen from Red Hat Linux installation program

Disk Druid gathers information about the hard drives on your system and displays a list of disk drives in the lower part of the screen and the current partition information for one of the drives in the Partitions list in the upper part. For each partition, Disk Druid shows five fields:

- **Mount Point** indicates the directory where the partition will be mounted. For example, if you have only one partition for the entire Linux file system, the mount point will be the root directory (/). For the swap partition, this field shows <Swap>. If this field appears as <not set>, you have to specify a mount point. To do so, select the partition and click the Edit button.
- **Device** refers to the partition’s device name. For example, hda1 is the first partition on the first IDE drive.
- **Requested** field shows how much space the partition has. For example, if the partition has 256MB of space, this field appears as 256M.
- **Actual** field shows the amount of disk space the partition is using. Usually, the Requested and Actual fields are the same, but they may differ for partitions that can grow in size.
- **Type** field shows the partition’s type, such as Linux Native or DOS.

If there are no partitions defined, the table in the Partitions list is empty. You have to add new partitions by clicking the Add button.

You perform specific disk setup tasks in Disk Druid through the five buttons that run across the middle of the screen. Specifically, the buttons perform the following actions:

- **Add** enables you to create a new partition, assuming there is enough free disk space available. When you click this button, another dialog box appears in which you can fill in information necessary to create a partition.
- **Edit** enables you to alter the attributes of the partition currently highlighted in the Partitions list. You make changes to the current attribute in another dialog box that appears when you click the Edit button.
- **Delete** removes the partition currently highlighted in the Partitions list.
- **Reset** causes Disk Druid to ignore any changes that you may have made.
- **Make RAID Device** sets up a RAID (Redundant Array of Inexpensive Disks) device — a technique that combines multiple disks to improve reliability and data transfer rates. There are several types of RAID configurations. This button is active only if your system has the hardware necessary to support a RAID device.
