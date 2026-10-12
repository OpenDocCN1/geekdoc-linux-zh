# Chapter 10: Understanding System Administration

ext2, or minux. The ext3 file system is also referred to as the Third Extended file system. The ext3 file system includes journaling features that improve a file system's ability to recover from crashes, as compared to ext2 file systems.

+   * **ext2** — The default file system type for versions of Red Hat Linux previous to 7.2. Features are the same as ext3, except that ext2 doesn't include journaling features.
+   * **ext** — This is the first version of ext3. It is not used very often anymore.
+   * **iso9660** — This file system evolved from the High Sierra file system (which was the original standard used on CD-ROM). Extensions to the High Sierra standard (called Rock Ridge extensions), allow iso9660 file systems to support long filenames and UNIX-style information (such as file permissions, ownership, and links). This file system type is used when you mount a CD-ROM.
+   * **kafs** — This is the AFS client file system. It is used in distributed computing environments to share files with Linux, Windows, and Macintosh clients.
+   * **minix** — This is the Minix file system type, used originally with the Minix version of UNIX. It only supports filenames of up to 30 characters.
+   * **msdos** — This is an MS-DOS file system. You can use this type to mount floppy disks that come from Microsoft operating systems.
+   * **vfat** — This is the Microsoft extended FAT (VFAT) file system.
+   * **umsdos** — This is an MS-DOS file system with extensions to allow features that are similar to UNIX (including long filenames).
+   * **proc** — This is not a real file system, but rather a file-system interface to the Linux kernel. You probably won't do anything special to set up a proc file system. However, the /proc mount point should be a proc file system. Many utilities rely on /proc to gain access to Linux kernel information.
+   * **reiserfs** — This is the ReiserFS journaled file system.
+   * **swap** — This is used for swap partitions. Swap areas are used to hold data temporarily when RAM is currently used up. Data is swapped to the swap area, then returned to RAM when it is needed again.
+   * **nfs** — This is the Network File System (NFS) type of file system. File systems mounted from another computer on your network use this type of file system.

> **CROSS-REFERENCE:** Information on using NFS to export and share file systems over a network is contained in Chapter 18.

+   * **hpfs** — This file system is used to do read-only mounts of an OS/2 HPFS file system.
+   * **ncpfs** — This relates to Novell NetWare file systems. NetWare file systems can be mounted over a network.