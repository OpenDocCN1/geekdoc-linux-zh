
## System

Under ‘System’, you will have the option of reconfiguring the boot mode, creating a boot or module disk, or setting the language and time zone. In the “Configuration” manual, find all the necessary information.

## Sysconfig Editor

The files where the most important SuSE Linux settings are stored are located in the `/etc/sysconfig` directory. This directory used to be a central file, `/etc/rc.config`, where all the configurations were stored. The sysconfig editor presents the settings options in an easy-to-read manner. The values can be modified and subsequently added to the individual configuration files in this directory. In general, it is not necessary to manually edit them, however, because these files will automatically be adjusted when installing a package or configuring a service.

> **Caution**
>
> Do not modify the `/etc/sysconfig` files if you lack previous experience and knowledge. It could do considerable damage to your system.

![](img/a4b6c994843f3fbd688003f4cabfa48f_94_0.png)

*Figure 5.2: YaST2: Configuring the sysconfig Editor*

## Runlevel Editor

Runlevels in Linux are described in more detail in Section *Runlevels* on page 298 ff.

After this expert module starts, it will be initialized. The current default runlevel will be shown in the next dialog. This “operation mode” will start after your system boots. In SuSE Linux this is usually runlevel 5 (full multiuser operation with network and KDM, the graphical login). Runlevel 3 also works well (full multiuser operation with network). At this point, with the help of YaST2, a different default runlevel can be set. See Table 12.1 on page 299. ‘Edit’ continues to an overview of all the services and daemons, supplemented with information as to whether they have been activated on your system and for which runlevels. Highlight a line with the mouse and activate the check boxes for runlevels ‘0’, ‘1’, ‘2’, ‘3’, ‘5’, ‘6’, and ‘S’ and, with that, state which service or daemon should be activated for which runlevel. Runlevel 4 is undefined — this is always reserved for custom settings.

With ‘Start’ and ‘Stop’, decide whether a server should be started. The current status is checked via ‘Update’, if this has not already been done automatically. ‘Reset to default value’ allows you to restore the default settings to their initial state following installation. ‘Activate service’ will only appear if the service is currently disabled. ‘Reset all services to default value’ restores all services to their original state following installation. ‘Finish’ saves the system configuration.

> **Caution**
>
> Caution, no experiments here — this is an expert tool. If certain service settings are wrong, the system may not be able to be restarted, possibly requiring a reinstallation from scratch, or security gaps could turn up in your system.

## Expert Partitioner

The partitioning module enables editing and deletion of existing partitions, as well as the creation of new ones. Access Soft RAID and LVM configuration from here.

In normal circumstances, partitions are specified during installation. However, it is possible to integrate a second hard disk in an already existing Linux system. First, the new hard disk must be partitioned. Then it must be mounted and entered into the `/etc/fstab` file. It may be necessary to copy some of the data to move an `/opt` partition from the old hard disk to the new one.

Use caution if you want to repartition the hard disk you are working on — this is essentially possible, but you will have to reboot the system right afterwards. It is a bit safer to boot from CD and then repartition it. The ‘Experts…’ button reveals a pop-up menu containing the following commands:

- **Reread Partition Table**: Rereads the partition table from disk. For example, you will need this for manual partitioning in the text console.
- **Adopt Mount Points from Existing `/etc/fstab`**: This will only be relevant during installation. Reading the old `fstab` is useful for completely reinstalling your system rather than just updating it. In this case, it is not necessary to enter the mount points by hand.
- **Delete Partition Table and Disk Label**: This completely overwrites the old partition table. For example, this can be helpful if you have problems with unconventional disk labels. Using this method, all data on the hard disk will be lost.

## Logical Volume Manager (LVM)

The Logical Volume Manager (LVM) enables flexible distribution of hard disk space over several file systems. As it is difficult to modify partitions on a running system, LVM was developed: it provides a virtual “pool” (Volume Group — VG for short) of disk space, from which logical volumes (LV) can be generated if needed. The operating system will access these instead of the physical partitions.

Features:

- Several hard disks or partitions can be combined into a large logical partition.
- If a LV (e.g., `/usr`) is full, it can be enlarged with the appropriate configuration.
- With the LVM, you can even add hard disks or LVs in a running system. However, “hot-swappable” hardware, designed for these types of interventions, is required for this.

Implementing LVM already makes sense for heavily used home PCs or small servers. If you have a growing data stock, as in the case of databases, MP3 archives, or user directories, the Logical Volume Manager is just the right thing for you. This would allow you to create file systems that are larger than a physical hard disk. Another advantage of the LVM is that up to 256 LVs can be added. Keep in mind that working with the LVM is very different from working with conventional partitions.

Instructions and further information on configuring the “Logical Volume Manager” (LVM) can be found in the official LVM HOWTO and the SuSE documentation:

- http://www.sistina.com/lvm/Pages/howto.html
- http://www.suse.com/us/support/oracle/

## Soft RAID

The purpose of RAID (Redundant Array of Inexpensive Disks) is to combine several hard disk partitions into one large “virtual” hard disk for the optimization of performance and data security. Using this method, however, one advantage is sacrificed for another. ‘RAID level’ defines the pool and common access device of all hard disks, known as the RAID controller. A RAID controller mostly uses the SCSI protocol, because it can drive more hard disks better than the IDE protocol. It is also better able to process parallel running commands. Instead of a RAID controller, which can often be quite expensive, the Soft RAID is also able to take on these tasks. SuSE Linux offers the option of combining several hard disks into one Soft RAID system with the help of YaST2 — a very reasonable alternative to Hardware RAID.

### Customary RAID Levels

**RAID 0** This level improves the performance of your data access. Actually, this is not really a RAID, because it does not provide data backup, but the name “RAID 0” for this type of system has become the norm. With RAID 0, two or more hard disks are pooled together. The performance is very good — although the RAID system will be destroyed and your data lost, even if just one of the many remaining hard disks fails.

**RAID 1** This level provides more than adequate backup for your data, since the data is copied to another hard disk 1:1. This is known as “hard disk mirroring” — if a disk is destroyed, a copy of its contents is located on another one. All of them except one could be damaged without endangering your data. The writing performance suffers a little in the copying process when using RAID 1 (ten to twenty percent slower), but read access is significantly faster in comparison to any of the normal physical hard disks, because the data is duplicated so it can be scanned in parallel.

**RAID 5** RAID 5 is an optimized compromise between the two other levels in terms of performance and redundancy. The hard disk capacity equals the number of disks used minus one. The data is distributed over the hard disks as with RAID 0. “Parity blocks”, created on one of the partitions, are there for security reasons. They are linked to each other with XOR — thus enabling the contents, via XOR, to be reconstructed by the corresponding parity block in case of system failure. With RAID 5, no more than one hard disk can fail at the same time. If one is destroyed, it must be replaced as soon as possible to save the data.

Configuration instructions and more details for Soft RAID can be found in the HOWTOs at:

- `/usr/share/doc/packages/raidtools/Software-RAID-HOWTO.html`
- `http://www.LinuxDoc.org/HOWTO/Software-RAID-HOWTO.html`

or via a Linux RAID mailing list, such as:

- `http://www.mail-archive.com/linux-raid@vger.rutgers.edu`

There you will find help if unexpected complications arise.

## Miscellaneous

‘Miscellaneous’ gives the option of loading vendor driver CDs, viewing the start protocol (`/var/log/boot.msg`) and the system protocol (`/var/log/messages`), and configuring printers for CUPS and LPD. Instructions for this can be found in the “Configuration” manual.
