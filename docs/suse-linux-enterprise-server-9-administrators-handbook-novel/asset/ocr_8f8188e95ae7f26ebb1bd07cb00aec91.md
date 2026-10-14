one root partition. If you have more than 4GB of disk space, create a swap partition, a 1GB root partition, a 4GB /usr partition, a 4GB /opt partition, a 1GB /var partition, and assign the remaining space to /home.

# TIP

Some (mostly commercial) packages put their data in /opt while the applications themselves are placed in /usr/bin; one example is Mozilla. Therefore, you may either want to create a separate partition for /opt or make the root partition large enough.

+   - **Hard disk configuration**—SLES 9 supports industry standard hard drives, such as IDE and SCSI (including iSCSI devices). Often, servers use RAID disks for fault tolerance, so you should give some thought to the RAID level you want to use. SLES 9 offers the option of combining several hard drives into one "soft RAID" system with the help of YaST, as an alternative to hardware RAID. SLES's software RAID can be configured as RAID-0, RAID-1, or RAID-5. Note that SUSE products with the 2.6 kernel do not currently support SATA RAID. Either use the SATA drives as a straight block device or a block device with Linux software RAID.

# NOTE

A block device (such as a hard disk) is one that sends blocks of data with each read or write, as opposed to a character device (such as a keyboard), in which only one character can be sent or received at a time.

+   - **Filesystem type selection**—SUSE LINUX supports a variety of filesystem types, ranging from the legacy ext2 to Reiser or JFS. If you require secure file deletion, use ext2. And if you need performance and fault tolerance, Reiser is a good choice. Refer to Table 1.3 to ensure the filesystem type you select supports your file size requirements. You should also decide whether you want to encrypt the filesystem for security purposes. Find out more in Chapter 6, “Filesystem Security.”

+   - **Bootloader selection**—Two industry standard bootloaders are available for most Linux distributions: LILO (Linux Loader) and GRUB (GRand Unified Bootloader). The matter of using one over another is mostly a personal choice (not too different from the notorious vi versus emacs or KDE versus GNOME verbal battles). Because LILO has been around for a much longer time than GRUB, many seasoned Linux administrators