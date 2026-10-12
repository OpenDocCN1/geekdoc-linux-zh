![](bbox=[0.88, 0.17, 0.96, 0.25])

> > **CAUTION**
> > 
> > Notebook users should be careful when partitioning. Many notebooks use a special partition equal to the size of install RAM in order to perform suspend-to-disk or other hibernation operations. Always examine your computer's initial partitioning scheme if configuring a dual-boot system, and leave the special partition alone! One way around this problem is to use a software suspend approach as outlined at http://swsusp.sourceforge.net/.

# Hosting Parts of the Linux File System on Separate Partitions

Your choice of specific partitioning scheme will depend on how Fedora will be used. On a system being designed for expansion, greater capacity, or the capability to host additional software or users, you can use separate partitions to host various parts of the Linux file system. Some candidates for these separate partitions include

+   - `/home`—Users will store hundreds and hundreds of megabytes of data under their directories. This is important data, perhaps even more so than the system itself. Using a separate partition (on a different volume) to store this user data helps make the data easier to find and it segregates user and system data. You must decide ahead of time how much storage to allocate to users. For a single workstation, you should reserve several gigabytes of storage.

+   - `/opt`—As the home directory for additional software packages, this directory can have its own partition or remote file system. Fedora does not populate this directory, but it might be used by other software packages you install later. One gigabyte of storage should be adequate, depending on applications to be installed.

+   - `/tmp`—This directory can be used as temporary storage by users, especially if disk quotas are enforced; as such, it could be placed on its own partition. This directory can be as small as 100MB.

+   - `/usr`—This directory holds nearly all the software on a Fedora system and can become quite large if additional software is added, especially on a workstation configuration. Using a separate partition can make sense. A full install requires at least 6GB for this directory or more if additional software is added.

+   - `/var`—Placing this directory (or perhaps some of its subdirectories) on a separate partition can be a good idea, especially because security logs, mail, and print spooling take place under this tree. You should reserve at least one gigabyte of storage for `/var`, especially if using Fedora as a print server (as spooled documents will reside under `/var/spool`).

> > **TIP**
> > 
> > As a general rule, it is a good idea to segregate user and system data. Although a Linux system can be quickly restored, user data has a much greater value and can be much more difficult to replace. Segregating data can make the job of backing up and restoring much easier. If you ever have a problem accessing your partition, we recommend that you get the excellent Knoppix distribution that boots and runs entirely from CD. This will enable you to access your partitions and make any necessary repairs.