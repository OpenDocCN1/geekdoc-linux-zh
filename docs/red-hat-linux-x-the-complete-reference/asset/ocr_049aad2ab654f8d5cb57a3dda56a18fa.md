Replace the x with one of the following letters, depending on the interface the unit is connected to, and whether it is configured as master or a slave:

+   - a First IDE controller master
+   - b First IDE controller slave
+   - c Second IDE controller master
+   - d Second IDE controller slave

Note As each screen appears in the installation, default entries will be already selected, usually by the autoprobing capability of the installation program. Selected entries will appear highlighted. If these entries are correct, you can simply click Next to accept them and go on to the next screen.

# Partitions, RAID, and Logical Volumes

You will initially be asked to set up and designate the Linux partitions and hard disk configurations you want to use on your hard drives. Red Hat provides automatic partitioning options if you just want to use an entire single hard drive for your Linux system. To manually configure your hard disks, Red Hat provides a very detailed and graphic-oriented partitioning tool called Disk Druid. With Disk Druid, you can create specific partitions, or configure RAID devices, or set up logical volumes (see Chapter 31).

Once you have configured your hard disks, your partitions will be formatted. If you are formatting any old Linux partitions that still have data on them, a dialog box will appear listing them and asking you to confirm that you want to format them (new Linux partitions that you created will automatically be formatted). If you already have a Linux system, you will most likely have several Linux partitions already. Some of these may be used for just the system software, such as the boot and root partitions. These should be formatted. Others may have extensive user files, such as a /home partition that normally holds user home directories and all the files they have created. You should not format such partitions.

# Recommended Partitions

If you are manually creating your partitions, you are required to set up at least two Linux partitions: a swap partition and a root partition. The root partition is where the Linux system and application files are installed. In addition, it is recommended that you also set up a boot partition that would contain just your Linux kernel, and a /home partition that would hold all user files. Separating system files on the root and boot partitions from the user files on the home partition allows you to replace the system files should they ever become corrupt without touching the user files. Similarly, if just your kernel becomes corrupt, you would have to replace only the kernel files on your boot partition, leaving the system files on the root partition untouched. This strategy of separating system directories into different partitions can be carried further to ensure a more robust system. For example, the /var directory, which now holds Web and FTP server files, can be assigned its own partition, physically separating the servers from the rest of your system. The /usr directory, which holds most user applications can be placed in its own partition and then be shared and mounted by other systems. One drawback to this strategy is that you would need to know ahead of time the maximum space you would want to use for each partition. For system and kernel files, this can be easily determined, but for directories whose disk usage can change dramatically, like /home, /var, and even /usr, this can be difficult to determine. As an alternative to creating separate physical partitions for each directory, you could use logical volumes (described later). A basic partition configuration is shown here:

+   - Swap partition no mount point
+   - / Root partition for system files (and all other files if no other partitions are defined)
+   - /boot Boot partition holding the Linux kernel (200MB approximately)
+   - /home User home directories and files

Except for the swap partition, when setting up a Linux partition, you must specify a mountpoint. A mountpoint is a directory where the files on that partition are connected to the overall Linux file structure for your system. The mountpoint for your root partition is the root directory, represented by a single slash, /. The mountpoint for your boot partition is the path /boot. For a user's partition, it would be /home.

The size of the swap partition should be the same size as your RAM memory, with a recommended minimum size of 64MB. With 512MB of RAM, you could use a 512MB swap partition. If you have a large amount of RAM, you can make the swap partition the same size. If your disk space is limited, you should make your swap size at least 64MB.