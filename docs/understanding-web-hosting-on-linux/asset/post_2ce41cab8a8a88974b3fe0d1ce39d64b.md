
Installation 35

It is highly recommended that you take the time to read the help presented on each of the installation dialog screens to guide you on your selections. Red Hat will preselect options wherever possible, and whenever it can, offer a suggestion as to what your response should be (?).

## These Are Your Options...

The next screen presented to you is the Install Options screen. Here, you can select the type of installation you intend to perform. If Red Hat has a preexisting Red installation, it will automatically select the option to upgrade. If we assume that you're starting with a clean disk, the install option should be selected already, as well the workstation type, which is for most installations.

If you read the help text provided on the Install Options screen, you'll note that the workstation and laptop options are similar, and permit Linux to be installed on a system that already has another operating system, assuming you have some free, unpartitioned space on your hard drive. The software installed during a workout/laptop installation is primarily what would be employed by a single user, including the X Window system. Both of these options partition your drive as mentioned earlier, with space for swap, /boot and everything else as root (/).

The server installation option installs software that would be used by an Internet server, including the Apache Web server and the PostgreSQL database management system. Conspicuously missing is the X Window, a reasonable option for a server, since it frequently runs without a monitor.

Note: The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The final installation option, "custom system," allows you to select how you want the drive(s) partitioned as well as which packages you want installed. We assume that you are installing Linux on a system that will be used as both a server (so others can connect to your system) and a workstation (where you'll design your Web site and connect to other Web servers). The custom system option provides the means to create such a system, ensure that Custom System is selected, and click Next.

If the hard drive in your system has been wiped clean, you'll get an error message stating that the partition table is corrupt and needs to be initialized. Click OK and continue. In any case, you'll arrive at the Partition screen. Once again, take the time to read the help information. Select the option to "manually partition with Disk Druid," and click Next.

The next screen, Partitions, is divided into three parts. At the left is the omnipresent help. On the upper right is a list of all partitions you have already created, along with their mount points and types. At the bottom right is a list of the hard drive(s) installed on your system and the percentage of space used on each. For this exercise, we assume that you have only one installed drive.

Begin partitioning the drive by clicking Add. You'll be supplied with a dialog box that requests the following:

- The mount point for the partition
- The size of the partition
- Whether Disk Druid should use the remainder of the drive for this partition
- The kind of partition you are creating
- The drives available on your machine

Using the drop-down arrow on the Mount Point box, and select /boot to indicate that you are creating the partition for /boot. Next, enter 16 into the Size (Megs) box to indicate that it should be 16 Mb (which is the size Red Hat creates in workstation or system installations). Ensure that the “Using remaining space?” check box is unchecked, since you don't want a single partition mounted /boot! The correct type of partition is Linux native, which should already be selected. Finally, if you have only one drive, hda (or sda, a SCSI machine) will already be selected. If not, select it, and deselect any of the other drives. Double-check your work, and when you're satisfied, click OK.

The partition you just will appear in the upper right. Do not be concerned if the number under Requested headers differs from that under the Actual heading. This is caused by the geometry of your hard disk. Disk Druid will find the closest size that will allow the partition to be on a cylinder boundary.

Next, you need to create a swap partition. Interestingly, Red Hat creates a 64 Mb swap partition if you select automatic partitioning on a custom system, workstation, or laptop installation. If you select a server installation, it creates a 256 Mb swap partition. Red Hat's own Installation Guide is very helpful in answering the question of what size you should use for the swap partition because it diverges from what the program will create (“Do what I say, not what I do”).

The traditional answer is calculated by this formula: multiply the physical memory in the machine by two. Thus, a machine with 128 Mb of RAM would have a 256 Mb swap partition. Adding to the confusion, however, the latest reports say the 2.4 version of the kernel is more aggressive in its use of swap space. Recommendation is to use 256 Mb for swapping if you have a hard drive large enough to accommodate it; otherwise, use the RAM-times-two factor. In any event, don't make it larger than 512 Mb. Later, you'll be able to see the results of your selection are, and if you need, you can add additional swap space.

To create the swap partition, click Add as before, but leave the mount point blank. Insert 256 (or your chosen size) in the Size box; then using the drop-down box, select Linux Swap for your partition, and click Next.

Note: The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.

The server installation assumes that the entire system is to be used for a Linux server. It will delete all operate from drives connected to your system, regardless of operating system, and configure the drives for its own use. If you ever decide to do a server installation, be sure to keep this in mind.
