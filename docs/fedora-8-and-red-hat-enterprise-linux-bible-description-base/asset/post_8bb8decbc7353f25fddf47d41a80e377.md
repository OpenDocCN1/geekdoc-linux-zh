
/dev/sda1 99M 8.6M 86M 10% /boot
none 61M 0 61M 0% /dev/shm

From the output of df, you can see that the root of your Linux system (/) is on the /dev/sda2 partition and that the /dev/sda1 partition is used for /boot.

> CAUTION: Before using fdisk to change your partitions, I strongly recommend running the df -h command to see how your partitions are currently being defined. This will help reduce the risk of changing or deleting the wrong partition.

To use fdisk to change your partitions, begin (as root user) by typing:

```bash
# fdisk device
```

where *device* is replaced by the name of the device you want to work with. For example, here are some of your choices:

-   /dev/sda — For the first IDE or SCSI hard disk; sdb, sdc, and so on for other SCSI disks. (For Fedora 8, IDE hard drives no longer appear as hda, hdb, and so on.)
-   /dev/md0 — For a RAID device.

After you have started fdisk, type m to see the options. Here is what you can do with fdisk:

-   **Delete a partition** — Type d and you are asked to enter a partition number on the current hard disk. Type the partition number and press Enter. For example, /dev/sda2 would be partition number 2. (The deletion won't take effect until you write the change. Until then, it's not too late to back out.)
-   **Create a partition** — If you have free space, you can add a new partition. Type n and you are asked to enter 1 for a logical partition (5 or over) or p for a primary partition (1-4). Enter a partition number from the available range. Then choose the first cylinder number from those available. (The output from fdisk -l shown earlier will show you cylinders being used under the Start and End columns.)
-   Next, enter the cylinder number the partition will end with (or type the specific number of megabytes or kilobytes you want: for example, +50M or +1024K). You just created an ext3 Linux partition. Again, this change isn't permanent until you write the changes.
-   **Change the partition type** — Press t to choose the type of file system. Enter the partition number of the partition you want to change. Type the number representing the file system type you want to use in hexadecimal code. (Type L at this point to see a list of file system types and codes.) For a Linux file system, use the number 83; use 82 for a Linux swap partition. For a Windows FAT32 file system, you can use the letter b.
-   **Display the partition table** — Throughout this process, feel free to type p to display (print on the screen) the partition table as it now stands.
-   **Saving and quitting** — If you don't like a change you make to your partitions, press q to exit without saving. Nothing will have changed on your partition table. Before you write your changes, display the partition table again and make sure that it is what you want it to be. To write your changes to the partition table, press w. You are warned about how dangerous it is to change partitions and asked to confirm the change.

An alternative to the fdisk command is sfdisk. The sfdisk command is command line-oriented. Type the full command line to list or change partitions. (See the sfdisk man page for details.)

## Tips for creating partitions

Changing your disk partitions to handle multiple operating systems can be very tricky. Part of the reason is that each different operating system has its own ideas about how partitioning information should be handled, as well as different tools for doing it. Here are some tips to help you get it right.

-   If you are creating a dual-boot system, particularly for Windows ME or Windows XP, try to install the Windows operating system first. Otherwise, the Windows installation may make the Linux partitions inaccessible.
-   The fdisk man page recommends that you use partitioning tools that come with an operating system to create partitions for that operating system. For example, the DOS fdisk knows how to create partitions that DOS will like, and the Fedora or RHEL fdisk will happily make you Linux partitions. Once your hard disk is set up for dual boot, however, you should probably not go back to Windows-only partitioning tools. Use Linux fdisk or a product made for multiboot systems (such as Partition Magic).
-   You can have up to 63 partitions on an IDE hard disk. A SCSI hard disk can have up to 15 partitions. You probably won't need nearly that many partitions.

If you are using Fedora or RHEL as a desktop system, you probably don't need a lot of different partitions within your Linux system. There are, however, some very good reasons for having multiple partitions for Linux systems that are shared by a lot of users or are public Web servers or file servers. Multiple partitions within Fedora or RHEL offer these advantages:

-   **Protection from attacks** — Denial-of-service attacks sometimes take action that tries to fill up your hard disk. If public areas, such as /var, are on separate partitions, a successful attack can fill up a partition without shutting down the whole computer. Because /var is the default location for Web and FTP servers, and therefore might hold a lot of data, often entire hard disks are assigned to the /var file system alone.
-   **Protection from corrupted file systems** — If you have only one file system (/), corruption of that file system can cause the whole Fedora or RHEL system to be damaged. Corruption of a smaller partition can be easier to correct and can often allow the computer to stay in service while the corruption is fixed.

Here are some directories that you may want to consider making into separate file system partitions:

-   **/boot** — Sometimes the BIOS in older PCs can access only the first 1024 cylinders of your hard disk. To make sure that the information in your /boot directory is accessible to the BIOS, create a separate disk partition (of only about 100MB) for /boot and make sure that it exists below cylinder 1024. Then, the rest of your Linux system can exist outside of that 1024-cylinder boundary if you like. Even with several boot images, there is rarely a reason for /boot to be larger than 100MB. For newer hard disks, you can sometimes avoid this problem by selecting the Linux Mode check box during installation. Then the boot partition can be anywhere on the disk.
-   **/usr** — This directory structure contains most of the applications and utilities available to Fedora or RHEL users. Having /usr on a separate partition lets you mount that file system as read-only after the operating system has been installed. This prevents attackers from replacing or removing important system applications with their own versions that may cause security problems. A separate /usr partition is also useful if you have diskless workstations on your local network. Using NFS, you can share /usr over the network with those workstations.
-   **/var** — Your FTP (/var/ftp) and Web-server (/var/www) directories are, by default, stored under /var. Having a separate /var partition can prevent an attack on those facilities from corrupting or filling up your entire hard disk.
-   **/home** — Because your user account directories are located in this directory, having a separate /home partition can prevent an indiscriminate user from filling up the entire hard disk. (Disk quotas represent another way of controlling disk use. See Chapter 10.)
-   **/tmp** — Protecting /tmp from the rest of the hard disk by placing it on a separate partition can ensure that applications that need to write to temporary files in /tmp are able to complete their processing, even if the rest of the disk fills up.

Although people who use Fedora or RHEL casually rarely see a need for lots of partitions, those who maintain and have to recover large systems are thankful when the system they need to fix has several partitions. Multiple partitions can localize deliberate damage (such as denial-of-service attacks), problems from errant users, and accidental file system corruption.

## Using the GRUB boot loader

A boot loader lets you choose when and how to boot the bootable operating systems installed on your computer’s hard disks. GRUB is the only boot loader offered for you to configure during Fedora installation. (The LILO boot loader included with earlier versions of Fedora is no longer included as of Fedora Core 5.) The following sections describe the GRUB boot loader.

With multiple operating systems installed and several partitions set up, how does your computer know which operating system to start? To select and manage which partition is
