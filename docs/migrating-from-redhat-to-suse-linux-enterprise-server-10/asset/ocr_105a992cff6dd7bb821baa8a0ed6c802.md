+   - You can create extremely large logical volumes (Terabytes).

+   - You can add hard disks to the volume group in a running system, provided you have hot-swappable hardware capable of such actions.

+   - You can add logical volumes in a running system, provided there is free space in the volume group.

+   - You can use several hard disks with improved performance in the RAID 0 (striping) mode.

+   - There is no limit that is relevant in practice on the number of logical volumes (the limit in LVM version 1 was 256).

+   - The Snapshot feature enables consistent backups in the running system.

# **Configure Logical Volumes with YaST**

The following are the basic steps for configuring logical volumes (LVM) with YaST:

+   - Define the LVM Partitions (Physical Volumes) on the Hard Drive

+   - Create the Volume Group and Logical Volumes

+   - Access the YaST Module lvm_config

# **Define the LVM Partitions (Physical Volumes) on the Hard Drive**

During (or after) the installation of SUSE Linux Enterprise Server, you need to configure the LVM partition on the hard disk.

You can use YaST or fdisk to perform this task as described in “Configure Linux File System Partitions” on page 4-13.