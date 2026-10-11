
## Working with LVM

If you can set up your Linux install using Logical Volume Management then you’ll find yourself frustrated should you attempt to repartition using GParted – it’s simply won’t work. That’s not a problem though, because all you need is the right tool.

You can, of course, configure your partitions from the command line, but a better bet is to employ the user-friendly LVM utility. To do so, boot from your Live CD, then open Software Center and search for ‘LVM’. Select ‘Logical Volume Manager’ and click More Info > Use This Source > Install. Once installed, launch LVM and you’ll find a more pleasant environment to work in.

Start by resizing your root partition to free up available space: expand Logical View, select ‘root’ and click Edit Properties. Use the controls to shrink the partition to its desired size and click OK, then wait while the partition is resized. You can then switch to Logical View and click ‘Create New Logical Volume’ to set up any additional partitions you wish to create, including giving them a friendly name (such as ‘home’ for your home partition).

Don’t bother configuring a mount point at this stage – instead, follow steps four through to six of the walkthrough (see p120) once the partition is in place to finish configuring it.

![](img/420a7272a6efa239082a35eeadd9bc1d_92_0.png)

> The LVM utility (or as its package is called system-config-lvm) is the easiest partitioning tool to use on LVM-enabled setups.

![](img/420a7272a6efa239082a35eeadd9bc1d_92_1.png)

> Remember to take a full drive image of your hard disk before you begin partitioning it. Try Clonezilla.

In this tutorial we’ll cover partitioning using MBR, but the process is a similar one for GPT drives. We’re using Ubuntu 14.04.3 LTS, but you should be able to translate this to most Linux distros.

How your computer is currently partitioned depends on your individual circumstances. Or, of course, as well as the distro you use. To see how your drive has been partitioned, as well as see what type of partition scheme (MBR or GPT) has been implemented, open the Disks utility from the Dash. Select your drive from the left-hand pane and check the ‘Partitioning’ entry to see what scheme it’s been assigned.

Beneath this is the Volumes chart, which provides a graphical representation of your disk, revealing what partitions have been set up. The default Ubuntu 14.04 setup, eg, sees your drive partitioned into two: a main Linux partition that’s bootable, with all your applications, data and settings in addition to your Linux distro. There’s also a much smaller extended partition, inside which is the swap file volume.

Each partition on your hard drive is allocated a separate entry inside the /dev folder, which is where references to all the components that make up your PC are stored. Each physical hard drive is represented by three letters: hda, hdb and hdc are for those drives attached to older IDE controllers, and sda, sdb and sdc are for those attached to SCSI and newer SATA controllers.

Each physical drive’s partitions are represented in numerical terms eg sda1 or sdb5. Look under Device to see which entry has been assigned to the currently selected volume in Disks. One complication: you may have been provided with an option to use LVM (Logical Volume Management) during install – if this is the case, then on traditional MBR-based setups, you’ll see a small primary partition described as Linux (Bootable) and a much larger extended partition inside which is the Linux LVM volume.

The primary partition exists because extended partitions aren’t bootable, so the required boot files are placed on this small partition with the rest of your system left on the extended volume. (See Working with LVM box, above).

## Partition structure

Partitions are accessed through the file system by mounting them at a specific level. Linux structures its files, folders and partitions as a tree. When you start Linux, your primary boot partition is mounted first at / at the root (or ‘trunk’) of the tree. Other partitions can then be mounted at specific folder points above it in the tree – the /mnt and /media folders are a good choice for a partition that’s specifically been created for sharing, eg. It’s also where external partitions – eg from another operating system – are automatically mounted if the partition’s file system is recognised by Linux.

It’s also possible to mount partitions directly to key directories like /tmp (temporary files) or /home (the home directories of each user on your PC) when applicable – this provides a seamless and consistent experience regardless of whether you decide to set up dedicated partitions for key folders or not. Mount points are stored in the /etc/fstab file.

The best time to partition your drive is when you first set up Linux on an empty drive. (Check out the Partition box from Scratch box, p94, for details on how easy this is.)

You’ll also encounter partitioning when setting up a dual-boot system. In this event, things are made much easier if your existing OS is detected during the installation process – if it is the hard work of partitioning is done for you because the installer suggests a suitable partition layout, which you can tweak to your personal needs based on how much free space is currently available on the drive.

That’s not a practical route for most people to take – and thankfully there are third-party tools that can repartition your drive without data loss, although it’s important to note there’s always an element of risk involved. That’s why it pays to take a full drive image of your current setup now, so if things go wrong you can reset and start again. Use a tool like Clonezilla (http://clonezilla.org) or create a snapshot if you’re running your installation in a virtual machine. It also pays to sit down and work out what your requirements are and how much space you have to play with. In the first instance, decide what additional partitions you wish to create and what you're creating them for. If it's to protect them against a reinstall or possible corruption on the main drive, then they can be housed on the same partition: remember that you could have provided some protection against data loss, it's not a substitute for backing up.

If you're looking to boost performance by moving key folders – your *swap* file, perhaps, or the *usr* folder where programs are stored – then these will need to be housed on a separate physical drive to the one Linux is running on.

Other considerations include the size of each partition – this depends on its use, and how much spare space you have. Start by right-clicking the folder in question in your file manager and selecting *Properties*. This is technically the minimum amount of space you'll need to allocate the partition, but think what else might need to be stored in the folder and add on the extra space accordingly. Note: you'll be taking space from your primary partition for the new volume, which may limit how much space you can assign to it.

Other considerations: should the partition be primary or extended? If you only plan to create a single additional partition then simply resize your system partition and create a new primary partition on its place. If you plan to create a number of partitions on your main drive, then using the extended partition is advised (*see boxout, below*).

You'll also have to decide what file system to assign the new partition. If you're creating dedicated partitions for folders like *home* or *var*, then you'll want to make these the same as your primary Linux partition (typically ext3 or ext4). The same is true for partitions you plan to use as shared folders over your network. Indeed, the only time you'll want to change the file type is if you're creating a partition that you plan to share with a Windows installation on the same PC, in which case choose FAT32 or NTFS.

- **As long as Ubuntu recognises the OS that you're trying to install alongside, the partitioning process is easy.**

![](img/420a7272a6efa239082a35eeadd9bc1d_93_0.png)

## Devices: Drive partitioning

> **Quick tip**
> It's possible to add a new partition to *fstab* without editing it directly – open the *Disks* utility, select your partition and choose More Actions > Edit Mount Options, to do so. You can't, however, add the 'pass' field using this method, preventing the partition being checked for errors at startup.

## Partition from scratch

The best time to partition is when you're setting up a fresh install. In Ubuntu, when prompted to erase the disk, select *Something else* and click 'Continue'. You'll see a table on `/dev/sda` – set up. Click the 'New Partition Table...' button, read the warning and click *Continue*: Now select the free space and click the + button next to *Change* to create a partition.

Let's begin with the main system partition. This can be as little as 15-20GB space, but make it larger if necessary. Once you've calculated how much you need in gigabytes, multiply it by 1,024 and enter the figure in the *Size* box. Leave *Primary*, 'Beginning of this space' and 'Ext4' journaling file system' selected, choose */* Under Mount point and click *OK*.

Select the remaining free space and click + again. Click the *Use as* drop-down menu and select *Swap area*. Set the partition type as *Logical*, but set its location to 'End of this space'.

What size (in MB) it should be depends – a rule of thumb is to make it the same size as the RAM installed in your PC (make it double the size if you have 1GB or less). Click *OK*.

Finally, select the remaining free space and click + again. Leave the size, type, location and *Use* as *Settings* as they are, and finally set the 'Mount point' to */home*. Click 'Install Now' followed by 'Continue' to set up your partitions and install Ubuntu.

When it comes to actually partitioning your drive, then the best tool to use already lives on your Ubuntu Live CD and it's *GParted*, a user-friendly graphical front end that makes resizing partitions simple (while also providing a handy graphical overview of the physical layout of your hard drive). You'll need to boot from this to resize your system drive anyway, so you might as well perform all your partitioning needs while outside your main Linux install.

## Partitioning tools

You can also run GParted from its own standalone bootable install on CD or USB from `www.gparted.org/livedd.php`. Make sure you pick the right architecture, which is typically i586 for older, 32-bit computers, and amd64 for newer 64-bit machines with UEFI rather than legacy BIOS. Users of 32-bit can also experiment with the i686-PAE build if they find the i586 build is a bit sluggish.

The step-by-step guide (*see right*) reveals how to shrink your main partition before creating a second primary partition alongside it using GParted from the Ubuntu live CD. If you'd rather create your new partition or partitions inside the extended partition, then the procedure is slightly different.

First, resize the system partition as outlined in the walkthrough. Once done, you need to extend the small extended partition that contains your *swap* file to take up all the remaining free space.

This can't be done while the *swap* file is in use, so right-click the *swap* partition in GParted and choose *Swap off*. Once done, you'll be able to right-click the extended partition and choose *Resize/Move*. Type 0 (zero) into the 'Free space preceding' box and click *Resize/Move* to quickly allocate all available space to the partition. You can now partition the free space as you wish without worrying about running out of available partitions – just make sure you calculate how much space each partition is likely to need and assign it accordingly, and don't forget to click the 'Apply' button when you're done.

The tools we've mentioned are pretty smart on the whole, but potentially dangerous task, which is why taking a full system backup before you begin is essential. If you run into problems, check out the GParted help pages at `http://gparted.org/help.php`. You'll find handy links to an FAQ with, among other helpful things, a guide to fixing problems with *Grub*.

You may run into problems when attempting to mount new partitions into key folders such as your *home* folder. If Linux throws an error on startup, press m to manually recover from it, then type `sudo nano /etc/fstab` to examine the file and check there are no errors preventing the partition from mounting correctly. If you can't find any problems, delete the line, save the file and restart before investigating.
