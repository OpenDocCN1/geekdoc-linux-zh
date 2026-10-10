A complete review of all the argument options and syntax for creating a DOS file system can be found in the man page for mkdosfs. The new file system must be mounted (as described in the following section) and then formatted with the mformat command.

# # Mounting File Systems

File systems in Unix are very flexible in that they need not be physically present on your computer; you can have network access to other file systems on other machines. The Linux file system structure (the Virtual File System we spoke of at the beginning of the chapter) makes it appear as if all the file systems, regardless of type and location, are local and mounted somewhere on the root file system. As the system administrator, you decide what file systems are to be made available and where they will be attached, or mounted, to the root file system. The standard arrangement of the file system tree is that installed by default by Fedora. The source of that standard arrangement is found in the file system hierarchy standards. Although a detailed discussion of those standards is beyond the scope of this section, they can be examined at http://www.pathname.com/fhs/. In this section, you learn how to mount file systems to the root file system and add file systems to the system, and you learn the traditional mount points of commonly used file systems as well.

In Linux (and its Unix cousins), all file systems—whether local, remote, images on a disk, or in memory—are mounted on a single point known as root (which is not the same as the root operator, also known as the super-user). This mount point is written as a forward slash, /, which is read and pronounced “root.” The resulting file directory hierarchy all starts from /. After they are mounted, the physical location of the files is unimportant because they all appear to be local.

Even if the file systems are different (FAT, ext2, HPFS, NTFS, and so on), the Linux kernel modules and the VFS make them all appear as part of the directory tree as native files. Listing the file systems as native file systems obviates the need for any applications to be aware of the physical location of the file or the true nature of the native file system. As a result, programming these applications is simplified because the applications have to work only with what they think are local, native files.

Any file system can be mounted anywhere, but some places are more traditional than others. Removable media devices are traditionally mounted under the /mnt directory (for example, CD-ROM drives on /mnt/cdrom). The /mnt directory is the traditional place to mount removable or remote file systems that are unrelated to the local system directories that branch from the root mount point.

# ## The mount Command

File systems are mounted with the mount command and unmounted, curiously enough, with the umount command.

During the installation, you have the opportunity to decide where and how your partitions will be mounted. You indicate your choices, and Fedora automatically stores them in /etc/fstab, the file system table, for you. The mount command looks at /etc/fstab