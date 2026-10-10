You can also configure the Linux kernel loaded by the live OS to use the / (root) filesystem on the hard disk. To do this, simply mount the / (root) filesystem on your local disk under an empty directory in the live OS (e.g., /mnt) and then type chroot /mnt at the command prompt. The chroot command will then change the root of the live OS to the /mnt directory, which is actually the / (root) filesystem on the local disk. From this point onward, you will have root user access to any commands on your / (root) filesystem, as you normally would if you had booted your Linux system on the hard disk. For example, if you run the passwd command (used for changing user passwords), you'll actually be changing the password for the root user on the Linux system installed on the hard drive. This is often used to recover a locally accessible Linux system if the root password has been lost or forgotten.

It is also important to note that this feature is not limited to live installation media. If you install Linux from standard installation media, the welcome screen will often provide a system rescue option that will allow you to boot a small live Linux system that does not contain a GUI environment. This small live Linux system contains the same recovery utilities (fdisk, parted, e2mkfs, fsck, etc.) and will allow you to mount the / (root) filesystem on your hard disk as well as run the chroot command to switch your live Linux system to it.

# # Chapter Summary

+   Linux servers typically use far more hardware than desktop systems. This hardware is installed in a rack using a rackmount form factor.

+   Many different SCSI standards have been developed since 1986. Parallel SCSI hard disks are uniquely identified by a SCSI ID and attach to a controller via a terminated cable. SAS is a newer SCSI technology that transfers information to hard disks using a serial cable. iSCSI is a SAN technology used to transfer information from iSCSI initiators to iSCSI targets across a TCP/IP network.

+   RAID is often used within Linux servers to combine several hard disks into a single volume for speed or fault tolerance. It can be implemented by software that runs within the OS, hardware on a hard disk controller card, or by the system BIOS.

+   The different levels of RAID determine how disks are combined and written to. RAID level 0 is not fault tolerant, whereas RAID levels 1 through 6 provide fault tolerance for data in the event of hard disk failure.

+   ZFS is a high-performance, fault tolerant filesystem that is commonly installed on Linux servers. ZFS provides much of the same functionality as RAID, using storage space that spans a wide range of different storage devices, including local disks, SANs, shared devices, large raw files, and remote shares.

+   Linux server distributions do not contain a GUI environment and are often administered remotely. They have an installation process that requires additional information compared to other Linux distributions.

+   Unsupported hardware, defective RAM, overclocked CPUs, and improper RAM settings can cause a Linux installation to fail.

+   The /proc directory contains information regarding detected hardware on the system and is useful when verifying whether an installation was successful.

+   You can use the bootable OS found on standard and live Linux installation media to access and repair a damaged Linux installation.