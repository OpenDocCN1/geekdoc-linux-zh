they need to save or use information from a particular device (such as a floppy disk or remote file system). Of course, any user can check this by typing the mount command.

# Mounting file systems

Most of your hard partitions are mounted automatically for you. When you installed Fedora or RHEL, you were asked to create partitions and indicate the mount points for those partitions. When you boot Fedora or RHEL, all partitions residing on hard disk should typically be mounted. For that reason, this section focuses mostly on how to mount other types of devices so that they become part of your Linux file system.

Besides being able to mount other types of devices, you can also mount other kinds of file systems on your Linux system. This means that you can store files from other operating systems or use file systems that are appropriate for certain kinds of activities (such as writing large block sizes). The most common use of this feature for the average Linux user, however, is to allow you to obtain and work with files from floppy disks and CD-ROMs.

# Supported file systems

To see file systems that are currently available to be used on your system, type cat/filesystems. The following file systems are supported in Linux, although they may not be in use at the moment or they may not be built into your current kernel (so they may need to be loaded as modules):

+   - adfs— This is the acorn file system, which is the standard file system used on RISOS operating systems.
- befs— This is the file system used by the BeOS operating system.
- cifs— The Common Internet File System (CIFS) is the virtual file system used to access remote servers that comply with the SNIA file specification. CIFS is an attempt to refine and standardize the SMB protocol used by Samba and Windows file sharing.
- ext3— The ext file systems are the most common file systems used by Linux. The ext3 file system was new for Red Hat Linux 7.2 and is currently the default file system in many Linux systems (including Fedora and RHEL). The root file system (/) is typically ext3 (although you can use other file systems as well). The ext3 file system is also referred to as the Third Extended file system. The ext3 file system includes journaling features that improve a file system's ability to recover from crashes, as compared to ext2 file systems.
- ext4— An enhancement to ext3, this type of file system performs and scales better to larger numbers of files. Fedora 9 introduced the ext4 file system type as a preview release. With Fedora 10, you can use ext4 file systems, but ext4 is still considered experimental.
- ext2— The default file system for versions of Red Hat Linux previous to 7.2. Features are the same as ext3, except ext2 doesn't include journaling features.