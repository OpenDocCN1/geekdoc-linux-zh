# Install Linux

All you need to know to anchor Linux on your computer.

The Linux installation process is involved but it isn’t actually that cumbersome. The exact installation steps are slightly different for every distribution, but in general the distro’s graphical installer will guide you through the necessary steps pretty easily.

In essence, installing Linux is very similar to installing a piece of software, albeit with a few caveats:

# Disk partitioning

Unlike a piece of software, installing Linux requires you to create a dedicated partition on your hard disk. This isn’t an issue if Linux will be the only OS on this computer. However, if you’re installing Linux alongside another OS, such as Windows, you’ll have to take steps to preserve the existing data. Many Linux distros will offer to partition the disk for you automatically, though you can create partitions yourself with ease from within Windows using the Disk Management tool (see Make Room for Linux, below). The advantage of manually partitioning your disk is that you get to decide how much space to allocate to Linux.

When creating partitions remember to create two new partitions. The bigger one with at least 12GB of disk space is for the OS itself, which you’ll format as ext4. You’ll also need to create a second partition for what’s called swap space. In simple terms, the swap partition extends the amount of physical RAM on your computer. A general rule of thumb for computers with a small amount of RAM (one or two gigabytes) is to create a swap partition that’s twice as large as the amount of RAM on your computer. For computers with more RAM, it’s best to create a swap partition that’s the same size as the amount of RAM you have.

# Securing data

During the installation process, many distros including Fedora and Ubuntu will give you an option to encrypt the Linux partition. This option gives you an added layer of security by insulating your data from unauthorised access. To enable this option you will need to supply a passphrase which will then act as the key to unlock the data.

Another important step during installation is setting up a root account. On most distros this step is part of the user creation process where you define the login credentials of your regular user account. The regular user doesn’t have any permissions to modify the system while logging in as root gives you complete control over your system.

# Dual boot

One software you should be familiar with when installing Linux is the bootloader. It’s a small program that tells the computer where to find the different OSes on the disk. Most Linux distros use the Grub 2 bootloader. In general, you shouldn’t have to do anything here, even when installing Linux on a Windows 8 computer that uses the UEFI BIOS with Secure Boot enabled. The latest versions of most mainstream distros, including Ubuntu and Fedora install a UEFI-compatible bootloader that will work correctly out of the box. However, since different vendors implemented UEFI differently, you might not get to the Grub bootloader screen and instead end up booting straight into Windows after installing Linux. In such a case, you should consider enabling the Legacy BIOS mode wherein the UEFI firmware functions as a standard BIOS. The option to enable Legacy BIOS is under the UEFI settings screen.

# Testing before installation

Almost every mainstream distro, including Ubuntu, Fedora and Mageia allow you to boot into a ‘live’ environment, which lets you experience the distro without disturbing the contents of your hard disk. You can use the live environment to get familiar with the distro and also verify the compatibility of your hardware with the distro. Also note that Linux distributions are distributed as ISO images. You can burn them to a CD or DVD, depending on their size, using the option to burn ISO images. You can also transfer ISO images to a USB drive. There are tools, such as UNetbootin and Yumi that will create bootable USB drives with the ISO of your distro, while Mageia recommends using the Rufus utility.

# Make room for Linux: Resize a Windows partition

![](bbox=[0.08, 0.7, 0.33, 0.81])

![](bbox=[0.35, 0.7, 0.6, 0.81])

![](bbox=[0.62, 0.7, 0.87, 0.81])

# 1 Shrink Windows

Before you can partition your disk you’ll need to squeeze your Windows partition to free up some disk space for the new partition. Head to the Disk Management tool, and right-click your main partition that is typically assigned the drive letter C. Then select the Shrink Volume option from the pop-up menu.

# 2 Create new partition

The Shrink dialog box shows you the total size of the drive and the maximum amount of shrink space available. You cannot squeeze more space out of a drive than the size shown here. To create a new partition, specify the size of the partition in the space provided in MB and click Shrink to start the process.

# 3 Use the partition

After the process is complete, a new partition showing the amount of free, or unallocated, space appears next to the Windows C: drive partition. You can then point your Linux distro’s installer to this free space. Remember to repeat the process and create another partition for the swap space as well.