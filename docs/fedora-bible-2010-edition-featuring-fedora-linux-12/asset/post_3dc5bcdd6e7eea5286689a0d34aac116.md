
multiple partitions for Linux systems that are shared by a lot of users or are public Web servers or file servers. Multiple partitions within Fedora offer these advantages:

- **Protection from attacks** — Denial-of-service attacks sometimes take action that tries to fill up your hard disk. If public areas, such as /var, are on separate partitions, a successful attack can fill up a partition without shutting down the whole computer. Because /var is the default location for Web and FTP servers, and therefore might hold a lot of data, often entire hard disks are assigned to the /var file system alone.

- **Protection from corrupted file systems** — If you have only one file system (/), corruption of that file system can cause the whole Fedora system to be damaged. Corruption of a smaller partition can be easier to correct and can often allow the computer to stay in service while the corruption is fixed.

Here are some directories that you may want to consider making into separate file system partitions:

- /boot — Sometimes the BIOS in older PCs can access only the first 1024 cylinders of your hard disk. To make sure that the information in your /boot directory is accessible to the BIOS, create a separate disk partition (of at least 500MB) for /boot and make sure that it exists below cylinder 1024. Then, the rest of your Linux system can exist outside of that 1024-cylinder boundary if you like. For newer hard disks, you can sometimes avoid this problem by selecting the Linear Mode check box during installation. Then the boot partition can be anywhere on the disk.

- /usr — This directory structure contains most of the applications and utilities available to Fedora users. Having /usr on a separate partition enables you to mount that file system as read-only after the operating system has been installed. This prevents attackers from replacing or removing important system applications with their own versions that may cause security problems. A separate /usr partition is also useful if you have diskless workstations on your local network. Using NFS, you can share /usr over the network with those workstations.

- /var — Your FTP (/var/ftp) and Web server (/var/www) directories are, by default, stored under /var. Having a separate /var partition can prevent an attack on those facilities from corrupting or filling up your entire hard disk. Often this partition is highly utilized and grows in size over time.

- /home — Because your user account directories are located in this directory, having a separate /home partition can prevent an indiscriminate user from filling up the entire hard disk. (Disk quotas represent another way of controlling disk use. See Chapter 9.) Also, some people have a separate /home partition so they can re-install the operating system, erasing the root (/) partition, and simply remounting the /home partition.

- /tmp — Protecting /tmp from the rest of the hard disk by placing it on a separate partition can ensure that applications that need to write to temporary files in /tmp are able to complete their processing, even if the rest of the disk fills up.

Although people who use Fedora casually rarely see a need for lots of partitions, those who maintain and have to recover large systems are thankful when the system they need to fix has several partitions. Multiple partitions can localize deliberate damage (such as denial-of-service attacks), problems from errant users, and accidental file system corruption.

## Installing Fedora on an Intel-based Mac

The latest Apple computers feature Intel-based computer architecture. The Fedora Project has enhanced Fedora so that it can be installed (either by itself or dual-booting with Mac OS X) on recent Apple hardware. Reasons you might want to install Fedora on one of these "MacTel" computers include:

- **Dual booting** — You might like the Mac OS X desktop (Aqua) and proprietary applications (such as iPhoto or iTunes) for yourself or family members some of the time. However, you might sometimes want access to server applications, administration tools, development environment, or thousands of free applications you can get with Fedora.
- **Fedora only** — Although you pay a bit of a premium for Apple hardware (though not as much as you used to), you might like the form, features, and performance of those cute Apple Mac computers enough to pay a bit extra to have it as your primary desktop Fedora computer.

This section describes how to start with an Intel-based Apple Mac computer (I used a Mac Mini for this example) and configure it to either dual boot with Mac OS X or run Fedora alone.

> **CAUTION:** Installing Fedora on Intel-based hardware is still a technology that is experimental in the Fedora community. Some hardware components still require extra tweaking or won’t work at all. I recommend that you don’t do this procedure if you can’t afford the possibility that your disk may be blown away and have to be reinstalled from scratch.

### Before installing Fedora on your Mac

Let’s start with a reminder that this procedure is only for Apple Mac computers that are based on Intel architecture. I ran this procedure on a new Mac Mini 1.1 (Intel Core Duo CPU, 512MB RAM). However, the same procedure should work for Intel-based iMac, MacBook, MacBook Pro, or Mac Pro computers.

This procedure is not for Macs with PowerPC architectures. Fedora does support that configuration, but you need to download the ppc installation media from Fedora instead of using the DVD that comes with this book. (Get the media for installing on PowerPCs from `http://fedoraproject.org/wiki/distribution/Download`.)

When you purchase your Mac, the entire hard disk is devoted to Mac OS X. To keep your Mac OS X installation on the computer (so you can boot either Mac OS X or Fedora), you need to reduce the amount of space devoted to Mac OS X. Then you need to use that space to create one or more partitions for installing Fedora.

Although the procedure for resizing and repartitioning your disk is fairly safe, there is some risk that you could corrupt your Mac OS X partition or make the machine (temporarily) unbootable. For that reason, before starting the procedure that follows, please ...

... BACK UP ANY IMPORTANT DATA!

## Installing Fedora

Mac OS X Leopard and higher versions offer software called Boot Camp that can be used to resize Mac hard disks (using the default HFS+ file system type). The following procedure describes how to update your firmware, resize your disk, and install Fedora.

1. **Check for firmware updates** — Update your Mac OS X system to the latest firmware. Refer to the Mac OS X Firmware Updates page for information on how to do that (`http://support.apple.com/kb/HT1237`). Then go to Apple Downloads (`http://www.apple.com/support/downloads/`) to get the firmware update, if necessary.

2. **Run Boot Camp** — Start Boot Camp Assistant (it's located in the Utilities folder). Because your interest in Boot Camp is to resize the Mac disk partition, skip the request to burn a Mac CD. Then move the divider to choose how much disk space will be devoted to Mac OS X and how much to Windows (you're going to be using the Windows area for Linux instead of Windows). Select the Partition button when each operating system has the disk space you want. (I chose to create a 10GB Windows partition.)

> **NOTE:** Because Boot Camp is no longer available for Mac OS X versions prior to Leopard, there is no official way to resize your disk to allow multiple boot partitions on your Mac. However, in theory you should be able to use a partitioning tool that supports HFS+ resizing to prepare your disk to install Fedora along side Mac OS X. Refer to Chapter 2 for information on how GParted or QTParted can be used to resize partitions, such as HFS+ partitions. If you decide to try it, your results come without warranty. (In other words, you're on your own.)

3. **Insert Fedora DVD** — When partitioning is done, instead of inserting a Windows Installation CD as requested, insert a Fedora installation CD or DVD and click Restart Mac OS X or Install Windows to reboot the computer. When the computer reboots, you should see the Fedora installer boot screen.

4. **Install Fedora** — Begin a normal Fedora install (as described earlier in this chapter), with just a couple of notes:

    - **Partitioning** — Default partitioning by the Fedora installer should work properly (leaving your Mac HFS+ partition alone and creating a Fedora /boot and LVM partition using the rest of the space).
    - **Boot loader** — Again, the installer should do the correct thing and configure the boot loader to be installed on a Fedora partition and not in the master boot record, as would
