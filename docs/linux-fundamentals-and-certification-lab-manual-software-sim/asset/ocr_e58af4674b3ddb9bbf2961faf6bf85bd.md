Then type **m** for the menu and the following is displayed:

```
Command (m for help): m
Command action
a toggle a bootable flag
b edit bsd disklabel
c toggle the dos compatibility flag
d delete a partition
l list known partition types
m print this menu
n add a new partition
o create a new empty DOS partition table
p print the partition table
q quit without saving changes
s create a new empty Sun disklabel
t change a partition's system id
u change display/entry units
v verify the partition table
w write table to disk and exit
x extra functionality (experts only)
```

The commands you need to know are d, n, p, q, and w. If this is a new installation and there are any existing partitions (option p shows existing partitions), you need to delete an existing partition (option d deletes existing partitions). After the existing partitions are deleted you must create a new partition (option n creates a new partition). A new partition can be primary or extended. Remember that you can have four primary partitions, or three primary partitions and one extended partition. After you select p for primary you are asked for the partition number (1–4), then the first cylinder. If you are using the entire disk, the first cylinder is 1. You then enter the last cylinder (a maximum value range is displayed). If you do not want to use the remainder of the disk for this partition, you must enter a value for the last cylinder that is something less than the maximum. You have told Linux what you want, but it won't create or delete partitions until you save the results (option w writes the new partition table to disk and exits). You can abort the process by quitting without saving (option q quits without saving changes). Remember that logical partitions are always numbered 5 and up.

Some versions of Linux require a reboot after partitioning a drive (pre-2.2 kernels). Linux will report that it needs to reboot. After rebooting, you are ready to format the disk drive. Formatting is accomplished through the mkfs command. If you added a second drive to IDE 1 (second master) and created one partition, the following command:

```
# mkfs -t ext3 -j /dev/hdc1
```

will format the drive.

After mkfs has finished formatting, it is time to mount the drive. This is easily done and is covered in Chapter 4.

# ■ INSTALLING A SCSI HARD DRIVE

SCSI devices are identified by an identification (ID) number that is configured by jumper settings selected to assign a value of 0 to 15. Other jumper settings are usually available to set SCSI termination. SCSI controllers and drives have different sets of instructions for installation. You should contact the manufacturer for detailed instructions on configuring these devices. Installing a SCSI driver in Linux is the same as with an IDE drive, except the device name will be /dev/sd* instead of /dev/hd*.

The first thing you do is set the drive SCSI ID and other operating options. The SCSI ID is generally set with a jumper and is an identity value of 0 to 15, as shown in Figure 2–7.