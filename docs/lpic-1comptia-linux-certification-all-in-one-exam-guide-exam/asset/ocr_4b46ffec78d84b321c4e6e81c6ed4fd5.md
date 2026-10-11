I then related that partitions can, occasionally, become damaged. If this happens, you can use the fsck utility to check and repair the partition. I pointed out that fsck is really a front end to various file system–specific repair utilities. I discussed how you can use the e2fsk utility to restore a damaged superblock.

I then looked at several file system maintenance utilities, including

+   - tune2fs
+   - reiserfstune
+   - dumpe2fs
+   - debugfs
+   - xfs_admin
+   - xfs_info
+   - xfs_metadump

I also looked at using the lsof command to check for open files in the file system. I also related that you can use the fuser command to display the PIDs of processes using specified files or file systems.

I then reviewed how mount can also be used to mount removable media in the file system. Just as partitions are mounted in a directory, removable devices are also mounted in a directory in the file system. You access these devices through the directory where they are mounted (called a mount point). I reviewed the procedure for mounting floppy diskettes, optical discs, USB devices, and FireWire devices. I pointed out that, if you don’t know what kind of file system is used by a removable device, you can use the -t auto option to allow the mount utility to automatically determine the correct parameter to use.

I ended this chapter by discussing how to back up your Linux file system. I emphasized the importance of conducting backups on a regular schedule. I then discussed the elements required to create a backup plan for your systems. The first step is to select a backup medium. I discussed the advantages and disadvantages of tape drives, recordable optical drives, and removable hard drives.

The next step is to select a backup strategy. I discussed how full, incremental, and differential backups work and how to combine them to design your own backup strategy. I also emphasized the importance of rotating your backup media as well as verifying your backup.

The next step is to determine your backup schedule and then to decide what to back up. I reviewed the directories in the file system that are commonly backed up, including /etc, /home, /opt, /root, /var, and /srv.

I ended the chapter by reviewing some of the Linux backup utilities that you can use to back up your system. I first reviewed the syntax for using tar, both with hard disks and with tape drives. I then reviewed the syntax for using cpio to create file archives. I discussed how to use gzip and bzip2 to compress/decompress tar and cpio archives. I also discussed how you can use dd to copy files and even create image files from entire disk partitions.