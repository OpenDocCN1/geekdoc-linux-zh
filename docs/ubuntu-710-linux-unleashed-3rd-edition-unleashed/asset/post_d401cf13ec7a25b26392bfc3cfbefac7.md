
## Choosing a Partitioning Scheme

As with deployment and installation of Linux, partitioning your hard drive to accept Ubuntu requires some forethought, especially if the target computer is going to be used other than as a home PC on which to learn Linux. If Linux is to be the only resident operating system, you can have the installer automatically create and use a partition scheme according to the type of installation you select during the install. If you plan to have a dual-boot system in which you can boot Linux or another operating system, you have to manually partition your hard drive before and possibly during the install.

The simplest and most basic partitioning scheme for a Linux system requires a Linux native root partition and a swap partition. On a single-drive system with 12GB storage and 512MB RAM, the scheme might look like this:

| Hard Drive Partition | Mount Point | Size |
|---|---|---|
| /dev/sda1 | / | 10.74GB |
| /dev/sda2 | swap | 1GB |

On a system running Windows, the scheme might look like this:

| Hard Drive Partition | Mount Point | Size |
|---|---|---|
| /dev/sda1 | /media/dos | 4GB |
| /dev/sda2 | / | 7.74GB |
| /dev/sda3 | swap | 1GB |

> CAUTION
> Notebook users should be careful when partitioning. Some notebooks use a special partition equal to the size of install RAM in order to perform suspend-to-disk or other hibernation operations. Always examine your computer's initial partitioning scheme if configuring a dual-boot system, and leave the special partition alone! One way around this problem is to use a software suspend approach as outlined at www.suspend2.net/.

## Hosting Parts of the Linux File System on Separate Partitions

Your choice of specific partitioning scheme will depend on how Ubuntu will be used. On a system being designed for expansion, greater capacity, or the capability to host additional software or users, you can use separate partitions to host various parts of the Linux file system. Some candidates for these separate partitions include

- /home—Users will store hundreds and hundreds of megabytes of data under their directories. This is important data, perhaps even more so than the system itself. Using a separate partition (on a different volume) to store this user data helps make the data easier to find and it segregates user and system data. You must decide ahead of time how much storage to allocate to users. For a single workstation, you should reserve several gigabytes of storage.
- **/opt**—As the home directory for additional software packages, this directory can have its own partition or remote file system. Ubuntu does not populate this directory, but it might be used by other software packages you install later. One gigabyte of storage should be adequate, depending on applications to be installed.
- **/tmp**—This directory can be used as temporary storage by users, especially if disk quotas are enforced; as such, it could be placed on its own partition. This directory can be as small as 100MB.
- **/usr**—This directory holds nearly all the software on a Ubuntu system and can become quite large if additional software is added, especially on a workstation configuration. Using a separate partition can make sense. A full install requires at least 6GB for this directory or more if additional software is added.
- **/var**—Placing this directory (or perhaps some of its subdirectories) on a separate partition can be a good idea, especially because security logs, mail, and print spooling take place under this tree. You should reserve at least one gigabyte of storage for /var, especially if using Ubuntu as a print server (as spooled documents will reside under /var/spool).

## TIP

As a general rule, it is a good idea to segregate user and system data. Although a Linux system can be quickly restored, user data has a much greater value and can be much more difficult to replace. Segregating data can make the job of backing up and restoring much easier. If you ever have a problem accessing your partition, we recommend that you get the excellent Knoppix distribution that boots and runs entirely from CD. This will enable you to access your partitions and make any necessary repairs.

## Reference

- http://www.yale.edu/pclt/BOOT/DEFAULT.HTM—A basic primer to partitioning that is operating system nonspecific.
- http://www-1.ibm.com/linux/—Home page for Linux at IBM, with links to products, services, and downloads.
- http://www-124.ibm.com/developerworks/opensource/linux390/—Home page for IBM S/390 Linux solutions.
- http://www.dell.com/linux/—Dell Computer's Linux information pages.
- http://hardware.redhat.com/hcl/—Entry point to Red Hat's hardware compatibility database.
- http://www.linux1394.org/—Home page for the Linux FireWire project, with information regarding the status of drivers and devices for this port.
