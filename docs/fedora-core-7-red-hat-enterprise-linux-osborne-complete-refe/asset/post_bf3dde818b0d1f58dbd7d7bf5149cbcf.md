
## Partition

The partition screen will display a pop-up menu with the automatic partition selections, which provides four options: Remove All Partitions on selected drive and create default layout, Remove Linux partitions on selected drive and create default layout, Use Free Space on selected drive and create default layout, and Create custom layout. For the first three, default partitions will be created. The Remove All Linux Partitions option (2) is selected by default.

- **Remove Linux partitions on selected drives** This removes just Linux partitions that are already on your disks. Any Windows or other OS partitions will remain untouched.
- **Remove all partitions on selected drives** This removes all the partitions on the disk, effectively erasing it. You will lose any existing partitions, including Windows partitions.
- **Use existing free space on selected drives** This is for disks that might be partially used, such as a partition for Windows that uses only part of the hard disk. This assumes that there is a significant amount of free space already on the disk.
- **Create custom layout** This options open Partd directly and lets you create your own partitions or manually select current ones. This option provides the most control, but you need to know how partitions work and how they are implemented on a hard drive.

In a pane below the options is a list of all the hard drives on your system. You can select the one you want Linux installed on. If you have only one, it will be selected for you.

An option at the bottom of the screen lets you review all your partitions in Partd, letting you modify them if you need to. This will not be checked by default. Check this to see exactly how Partd will partition your system. You can also make changes if needed.

- **Review and modify partitioning layout** This allows you to make changes manually to the partitions as well as see exactly what partitions will be created on your drives. Like the Create custom layout option you are place in the Partd partition manager where you can modify your partitions as you wish.

If you want to organize your data using several partitions, such as /home, /, and /var, as well as boot, you will have to manually configure them. Automatic partitioning will set up a boot partition and an LVM Linux partition only.

The Advanced Storage Configuration button lets you either select an iSCSI device or disable your motherboard RAID device controller (dmraid).

## Custom and Review Partitioning

If you choose the Create custom layout option or checked the Review option, the partitioning screen is displayed, placing you into the Partd partition configurator. Here, you can manually create Linux partitions or select the one where you want to install Fedora. The top pane lists the hard drives with their partitions on your computer (many computers will have only one hard drive), and the lower pane lists the partitions. Selecting a hard drive will list its partitions. The buttons above the partitions pane enable you to create, edit, and delete partitions. The Partitions screen is actually an interactive interface where you configure partitions as well as create new ones.

If you are reviewing after default partitioning, then the hard disk partitions set up for you will be displayed. The panel will show the specific partitions that will be created for your system.

If you are formatting any old Linux partitions that still have data on them, a dialog box will appear listing them and asking you to confirm that you want to format them (new Linux partitions that you created will automatically be formatted). If you already have a Linux system, you will most likely have several Linux partitions already. Some of these may be used for just the system software, such as the boot and root partitions. These should be formatted. Others may have extensive user files, such as a /home partition that normally holds user home directories and all the files they have created. You should not format such partitions.

### Recommended Partitions

If you are manually creating your partitions, you are required to set up at least two Linux partitions: a swap partition and a root partition. The root partition is where the Linux system and application files are installed. In addition, it is recommended that you also set up a boot partition that would contain just your Linux kernel, and a /home partition that would hold all user files. Separating system files on the root and boot partitions from the user files on the home partition allows you to replace the system files should they ever become corrupt, without touching the user files. Similarly, if just your kernel becomes corrupt, you would have to replace only the kernel files on your boot partition, leaving the system files on the root partition untouched. This strategy of separating system directories into different partitions can be carried further to ensure a more robust system. For example, the /var directory, which now holds Web and FTP server files, can be assigned its own partition, physically separating the servers from the rest of your system. The /usr directory, which holds most user applications, can be placed in its own partition and then be shared and mounted by other systems. One drawback to this strategy is that you would need to know ahead of time the maximum space you would want to use for each partition. For system and kernel files, this can be easily determined, but for directories whose disk usage can change dramatically, like /home, /var, and even /usr, this can be difficult to determine. As an alternative to creating separate physical partitions for each directory, you could use logical volumes (described later). A basic partition configuration is shown here:

- **Swap partition** No mount point
- **/** Root partition for system files (and all other files if no other partition is defined)
- **/boot** Boot partition holding the Linux kernel (approximately 200 MB)
- **/home** User home directories and files

Except for the swap partition, when setting up a Linux partition, you must specify a mountpoint. A mountpoint is a directory where the files on that partition are connected to the overall Linux file structure for your system. The mountpoint for your root partition is the root directory, represented by a single slash (/). The mountpoint for your boot partition is the path /boot. For a user's partition, it would be /home.

The size of the swap partition should be the same size as your RAM memory, with a recommended minimum size of 64 MB. With 512 MB of RAM, you could use a 512 MB swap partition. If your disk space is limited, you should make your swap size at least 64 MB.

### Creating Partitions

To create the new partition, click the New button to display a dialog box where you can enter the mountpoint, the size (in megabytes), the partition type, and the hard disk on which you want to create the partition. By default you can select a fixed size, specifying the megabytes to use. You can also select a *“Fill to maximum allowable size”* option to have the partition automatically expand to the size of the remaining free space on the disk. You can have this option selected for more than one partition. In that case, the partition size will be taken as a required minimum and the remaining free space will be shared equally among the partitions. For partition type, select ext3 for standard Linux partitions and select the Linux swap type for your swap partition. You can even use Parted to create Windows vfat partitions (16 bit). There are five kinds of partitions supported during installation, ext2, ext3, swap, physical volume, software RAID, and vfat. The ext2 partition is an older form of the Linux standard partition type, ext3. You would use software RAID if you are setting up RAID arrays using the Linux RAID software instead of your motherboard RAID device support. Physical volumes is used to set up Logical volumes. If you choose to set up default partitions, you will see that a physical volume has already been created (root pv), with a corresponding Logical group and its volumes on which your swap and root partitions reside.

To make any changes later, you can edit a partition by selecting it and clicking the Edit button.

## Logical Volumes

Fedora also supports Logical Volume Management (LVM), letting you create *logical volumes*, which you can use instead of using hard disk partitions directly. Logical volumes are implemented by Logical Volume Management (LVM). They provide a more flexible and powerful way of dealing with disk storage, organizing physical partitions into logical volumes in which memory can be managed easily. Disk storage for a logical volume is treated as one pool of memory, though the volume may in fact contain several hard disk partitions spread across different hard disks. There is one restriction. The boot partition cannot be a logical volume. You still have to create a separate hard disk partition as your boot partition with the */boot* mountpoint in which your kernel will be installed. If you selected default partitioning, the */boot* partition will have already been set up for you, along with an LVM volume partition for the rest of the system.

If you choose to let the install program set up a default partition layout for you, a logical group will be set up with volumes for both the swap and root partitions. The logical group will be labeled Logical0 by default. You can elect to change this name later by editing its properties with logical volume manager, system-config-lvm.

Creating logical volumes involves several steps. First you create physical LVM partitions, then the volume groups you place these partitions in, and then from the volume groups you create the logical volumes, for which you then specify mountpoints and file system types. To create your physical LVM partitions, click New and select Physical Volume (LVM) for the File System Type. Create an LVM physical partition for each partition you want on your hard disks. Once you have created LVM physical partitions, you click the LVM button to create
