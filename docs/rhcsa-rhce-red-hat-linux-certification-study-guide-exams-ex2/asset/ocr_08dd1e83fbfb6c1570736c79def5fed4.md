Once in production, it's rare to install a new Linux system from scratch. Besides, Linux installation is easy, at least for anyone serious about Red Hat certification. Most administrators have to maintain existing systems. Critical skills related to filesystems include adding new partitions, creating logical volumes, setting up volume encryption, and more. In many cases, you'll want to make sure these filesystems are mounted automatically during the boot process, and that requires a detailed knowledge of the /etc/fstab configuration file.

Some filesystems, such as those available from unreliable network connections, should be mounted only on a temporary basis; that is the province of the automounter.

# INSIDE THE EXAM

Some of the RHCSA objectives listed in this chapter overlap and may be in part covered in multiple sections. The objectives all relate in some way to filesystem management and should be considered as a whole in this chapter.

+   - Add new partitions, logical volumes, filesystems, and swap areas to a system non-destructively
+   - List, create, delete, and set partition type for primary, extended, and logical partitions

# Partition Management

As in the real world, it is the results that matter. It doesn't matter whether you use Disk Druid, fdisk, or parted to create partitions. You can create new partitions at the command line or use GUI front ends to these tools such as the Disk Utility. Make sure that appropriate partitions meet the requirements of the exam. Just remember Disk Druid is available only during the installation process. The current RHCSA objectives include the following related requirements:

# Logical Volumes

Partitions are essential components of logical volumes. Related RHCSA objectives describe some of the skills required. For example, the following objective suggests that you need to know the process starting with the physical volume:

+   - Create and remove physical volumes, assign physical volumes to volume groups, create and delete logical volumes